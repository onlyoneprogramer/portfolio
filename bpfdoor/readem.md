# BPF Backdoor 대응 고신뢰 보안 시스템 설계서

## 1. 시스템 개요

* **시스템 명**: BPF Backdoor 대응 고신뢰 보안 시스템
* **목표**: eBPF 도어킷을 포함한 커널 수준 위협에 대한 탐지, 대응, 복원 구조 확보
* **기대 효과**: 커널 및 사용자 공간의 위협에 대한 상시 감시 및 복원

---

## 2. 구성 요소

| 구성 요소            | 설명                                              |
| ---------------- | ----------------------------------------------- |
| Hypervisor + VMI | VM 외부에서 Guest OS 상태 모니터링 (LibVMI, Volatility 등) |
| Guest OS         | Hardened Linux 커널, LSM Hooks, Read-Only 모듈      |
| Kernel Agent     | Kprobe 또는 eBPF를 이용한 내부 커널 감시                    |
| User Agent       | 공격 탐지 및 대응 수행 (kill, NIC 격리, reboot 등)          |
| TPM + IMA        | 부팅 시 무결성 검증, Agent 변조 감지                        |

---

## 3. 보안 흐름도

1. **시스템 부팅**

   * Secure Boot → IMA → TPM PCR 체크 → Agent 실행

2. **상시 감시 단계**

   * User Agent ↔ Kernel Agent 감시
   * Hypervisor에서 메모리 감시 (BPF 객체, 프로세스 상태)

3. **침해 발생 시 대응 단계**

   * Agent1 이상감지 → Agent2가 프로세스 kill
   * 네트워크 격리 → 로그 백업 → 시스템 재부팅

---

## 4. 기술 세부사항

* **eBPF 탐지 방식**: `kprobe/bpf_prog_load`, `tracefs`, `bpftool`, `/sys/kernel/bpf`
* **Agent 감시 방식**:

  * PID/Hash 기반 무결성 체크
  * IPC (소켓/파이프) 하트비트 기반 헬스 체크
* **복원 메커니즘**:

  * systemd service를 통한 자동 재실행
  * Fallback script (`initrd` 또는 recovery mode 활용)
* **TPM 활용**:

  * `tpm2-pcrread` 통한 부팅시 integrity 확인
  * TPM EventLog 분석

---

## 5. 위협 모델 및 방어 전략

| 위협       | 탐지 방식                         | 대응 방식              |
| -------- | ----------------------------- | ------------------ |
| BPF 도어킷  | bpf\_prog\_load 감시, map 객체 확인 | 해당 프로세스 kill       |
| Agent 변조 | hash 변경 감지, 실행 파일 Appraise    | Agent2 복원 실행       |
| 루트킷 삽입   | syscall table 무결성, LKM 감시     | 재부팅 및 LKM 해제 시도    |
| 네트워크 탈취  | NIC 트래픽 이상 감지                 | NIC 다운 및 isolation |

---

## 6. 로그 및 포렌식 대응

* Agent 로그 → Syslog, Journald, 외부 로그 서버
* VMI → Guest 메모리 Snapshot 수집
* TPM 로그 → 부팅/실행 변조 여부 확인

---

## 7. 테스트 시나리오 및 PoC 계획

| 테스트 항목       | 테스트 내용              | 예상 결과        |
| ------------ | ------------------- | ------------ |
| Agent1 강제 종료 | Agent2의 복원 동작 확인    | Agent1 재시작   |
| eBPF map 조작  | User Agent가 탐지 여부   | 탐지 후 로그 전송   |
| 커널 모듈 은닉 시도  | LSM + User Agent 감지 | 재부팅 및 log 보존 |

---

## 8. 결론 및 보안 등급 평가

* **보안 등급**: 고급 (APT 대응 수준)
* **적용 대상**: 금융, 국방, 정부, SOC, 보안 솔루션 기업
* **추후 확장 방향**:

  * 머신러닝 기반 이상 탐지
  * 정책 기반 자동 방어 Rule Engine
