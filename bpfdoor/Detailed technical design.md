# BPF Backdoor 대응 고신뢰 보안 시스템 상세 기술 설계서

## 1. 시스템 개요

* **시스템 명**: BPF Backdoor 대응 고신뢰 보안 시스템
* **설계 목적**: 커널 레벨에서 은닉되는 eBPF 기반 백도어 및 rootkit 등을 실시간으로 탐지하고, 시스템 이상 발생 시 자동 대응 및 복구 기능 제공
* **대상 환경**: 가상화 기반 인프라 (VM), 중요 인프라 서버 (금융, 공공, 국방 등)

---

## 2. 전체 아키텍처

```text
+------------------------------+
|   Hypervisor (Xen/KVM/ESXi) | <--- 외부 감시 (VMI)
+------------------------------+
          |
          v
+------------------------------+
| Guest OS: Hardened Kernel   |
| (RO modules + LSM Hooks)    |
+------------------------------+
          |
+------------------------------+
| Secure Dual-Agent System    |
| [Kernel Agent] + [User Agent] |
| - Watchdog Mutual Verification |
+------------------------------+
          |
+------------------------------+
| IMA + Secure Boot + TPM 2.0 |
| (Boot-time Integrity Check) |
+------------------------------+
```

---

## 3. 구성요소별 기술 세부사항

### 3.1 Hypervisor & VMI

* **역할**: Guest OS 외부에서 비침입형 메모리 모니터링
* **기술 스택**: LibVMI, Volatility Framework, Xen/KVM with introspection enabled
* **감시 항목**:

  * `bpf_prog` 구조체의 존재 및 메모리 위치
  * suspicious kernel code injection
  * guest OS의 프로세스 테이블 상태

### 3.2 Guest OS: Hardened Kernel

* **커널 보강 요소**:

  * Loadable Kernel Module (LKM) 금지 또는 검증
  * `sys_call_table` 보호 및 Read-Only 처리
  * eBPF syscall 감시 및 제한 (`bpf()` 인터페이스 추적)
* **보안 정책 적용**:

  * SELinux or AppArmor 기반 정책
  * LSM Hook (`inode_permission`, `file_open`, `bprm_check`) 확장

### 3.3 Dual-Agent 시스템

#### Kernel Agent

* **기능**: 커널 내부 이벤트 추적 (kprobe, tracepoint)
* **모니터링 항목**:

  * `bpf_prog_load` syscall
  * `/sys/fs/bpf/` 접근 추적
  * suspicious netfilter hook 설치 여부 확인

#### User Agent

* **기능**: 상위 제어/분석 및 복구 수행
* **기능 세부**:

  * Agent1/2 상호 감시 및 헬스 체크
  * Agent1 장애 시, Agent2가 자동 복구
  * 탐지 시 대응 로직 실행:

    * `kill -9`로 공격자 프로세스 제거
    * `ip link set down <if>`으로 NIC 격리
    * 로그 백업 및 `reboot` 실행

#### Agent 통신

* **채널**: UNIX Domain Socket 또는 Named Pipe
* **무결성 확인**:

  * SHA256 + TPM PCR 비교
  * runtime hash와 IMA 측정값 비교

### 3.4 TPM + IMA + Secure Boot

* **TPM 2.0**: 부팅 시 PCR 측정값을 기반으로 Agent 실행 무결성 보장
* **IMA**:

  * Agent 실행 시 Appraise 정책 적용
  * 무결성 로그 생성 및 비교
* **Secure Boot**: 부팅 로더 및 커널 무결성 검증

---

## 4. 위협 모델 및 대응 전략

| 위협 유형         | 탐지 기술                      | 대응 방식                |
| ------------- | -------------------------- | -------------------- |
| eBPF 도어킷 삽입   | Kprobe + bpftool 검사        | 해당 프로세스 kill, 로그 수집  |
| Agent 실행파일 변조 | TPM PCR, IMA Appraise      | Agent2 복원, 로그 전송     |
| 루트킷 로딩        | LSM Hook, syscall table 감시 | 커널 패닉 유도 or 재부팅      |
| 네트워크 데이터 탈취   | NIC 트래픽 이상 감지              | NIC down + 프로세스 kill |

---

## 5. 자동 복원 메커니즘

* **systemd 서비스 단 구성**

```ini
[Service]
ExecStart=/usr/bin/agent1
Restart=always
RestartSec=1s
WatchdogSec=5s
```

* **Agent2 복구 절차**:

  1. Agent1 하트비트 미응답 시 3회 이상 감지
  2. Agent1 프로세스 강제 종료 후 파일 무결성 재확인
  3. 백업 경로에서 복사 및 재실행

---

## 6. 로그 및 증거 보존

* **로그 저장 경로**: `/var/log/secure-agent/` 아래 JSON 형식 저장
* **로그 항목**: 타임스탬프, 이벤트명, 대상 프로세스, 대응 결과
* **원격 전송**: syslog-ng 또는 rsyslog + TLS로 전송 가능
* **메모리 스냅샷 수집**: Volatility + VMI 이용해 주기적으로 snapshot 생성

---

## 7. 테스트 및 PoC 계획

| 테스트 항목    | 시나리오                           | 기대 결과                    |
| --------- | ------------------------------ | ------------------------ |
| eBPF 삽입   | `bpftool prog load`로 은닉 BPF 삽입 | Agent 감지 후 kill 및 reboot |
| Agent1 중단 | SIGKILL 전달                     | Agent2가 로그 기록 후 복원       |
| NIC 탈취    | TCP/UDP leak 프로세스 생성           | NIC 격리 + 로그 전송           |
| 실행파일 변조   | agent1 바이너리 SHA 변경             | TPM PCR mismatch → 실행 차단 |

---

## 8. 결론 및 확장 계획

* **보안 수준**: 고급 (APT 대응 가능)
* **적용 분야**: 방위 산업, 정보보안 솔루션, 클라우드 보안 VM 모니터링
* **확장 제안**:

  * 머신러닝 기반 이상행위 자동 Rule 생성
  * 실시간 정책 조정 가능 UI 제공 (관리 서버)
  * eBPF 기반 방어 로직 자체의 정적 분석 도구 개발
