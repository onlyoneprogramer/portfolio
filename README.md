# 👋 이진호 | Kernel-Level Security Engineer (eBPF / Linux)

> 커널 레벨에서 탐지되지 않던 위협을 식별하고,  
> 실제 운영 환경에 적용 가능한 구조로 구현하는 엔지니어

- eBPF 기반 커널 행위 추적 및 탐지 시스템 설계/구현
- Red Team 10년 경험 기반 공격 시나리오 중심 탐지 모델 설계
- PoC → 운영 구조까지 연결 가능한 실전형 엔지니어

---

## 🚀 Summary

10년 이상 Red Team 및 침해사고 대응 경험을 바탕으로  
**커널·네트워크 레벨 위협을 “탐지 가능한 구조”로 만드는 작업**을 수행해왔습니다.

단순 분석이 아닌 아래 전 과정을 직접 수행합니다:

- 탐지 가능성 정의  
- 구조 설계  
- PoC 검증  
- 운영 적용  

특히 eBPF 기반 커널 이벤트 추적을 활용하여  
기존 EDR/XDR이 탐지하지 못하는 영역을 보완하는 기술에 집중하고 있습니다.

---

## 🛡️ Core Project

### BPFdoor Detection Engine (eBPF 기반 커널 위협 탐지)

**한 줄 요약**  
기존 보안 솔루션이 탐지하지 못하는 커널 레벨 백도어를 식별하는 탐지 엔진 PoC

**기간**: 2025.05 ~ 2025.09  

---

### 📌 Problem

- BPFdoor와 같은 커널 레벨 은닉형 백도어는 기존 EDR/로그 기반 탐지에서 식별 어려움
- 유저 영역 로그 기반 탐지는 행위 은닉에 취약

---

### ⚙️ Solution

- eBPF 기반 커널 이벤트 추적 시스템 설계
- 프로세스 / 소켓 / 패킷 레벨 행위 수집 및 상관 분석
- 공격 흐름 기반 탐지 모델 정의 (행위 기반 탐지)
- 탐지 → 차단 확장 가능 구조 설계

---

### 📊 Result

- 커널 레벨 행위 추적 기반 탐지 PoC 개발 완료
- 기존 로그 기반 탐지 대비 탐지 가능 영역 확장
- 다양한 공격 시나리오 기반 탐지 로직 검증

> ※ (추가 추천)
> - 이벤트 처리량: 초당 XXXX건
> - CPU 오버헤드: X% 이하
> - 탐지 시나리오: XX개 이상

---

### 🧠 Impact

- 커널 레벨 위협 대응 가능성 검증
- EDR / 에이전트 구조로 확장 가능한 설계 확보

---

### 🧠 Tech

`C`, `eBPF`, `Linux Kernel`

---

## 🤖 System Architecture Project

### 실시간 센서/로봇 모니터링 시스템

**한 줄 요약**  
실시간 이벤트를 운영 가능한 구조로 재설계한 시스템

**기간**: 2025.11 ~ 2025.12  
**규모**: 로봇 4대 / 센서 40개

---

### 📌 Problem

- 데이터 흐름 불명확 (책임 경계 없음)
- 실시간 처리와 저장 로직 혼재
- 장애 발생 시 원인 추적 어려움

---

### ⚙️ Solution

- `Sensor → Agent → Backend → Web` 구조 설계
- 이벤트 처리 파이프라인 구축  
  (수집 → 검증 → 표준화 → 저장)
- Hot Path / Cold Path 분리
- WebSocket 기반 실시간 처리

---

### 📊 Result

- 40개 센서 실시간 처리 구조 안정화
- 장애 원인 추적 가능 구조 확보
- 운영 및 디버깅 도구로 활용 가능

---

### 🧠 Tech

`Spring`, `WebSocket`, `PostgreSQL`

---

## 🏢 Backend Project

### ERP System (0 → 1 구축)

**한 줄 요약**  
복잡한 도메인을 구조화하고 성능 병목을 해결한 시스템

**기간**: 2024.01 ~ 2024.05  
**역할**: 단독 개발

---

### 📌 Problem

- 복잡한 도메인 + 잦은 요구사항 변경
- 성능 저하 및 데이터 일관성 문제

---

### ⚙️ Solution

- 도메인 기반 모듈 설계
- 병목 구간 식별 후 쿼리 및 인덱스 최적화
- API 구조 재설계 (데이터 흐름 기반)

---

### 📊 Result

- 응답 속도 40% 이상 개선
- 유지보수 가능한 구조 확보

---

### 🧠 Tech

`Java`, `Spring`, `MySQL`

---

## 🧩 Additional Experience

- MES 시스템 입력 검증 및 RBAC 설계
- 급여 시스템 감사 추적 구조 설계
- 침해사고 대응 및 협업 경험 (Red Team 10년)

---

## 🛠 Core Skills

### Security / Kernel
- eBPF 기반 이벤트 추적
- Kernel / Network 행위 분석
- 공격 시나리오 기반 탐지 설계

### Backend / System
- 시스템 아키텍처 설계 (0→1)
- 이벤트 처리 파이프라인 설계
- Observability 및 운영 구조 설계

### Languages
`C`, `Java`, `Python`, `C#`

### Environment
`Linux`, `Spring Boot`, `PostgreSQL`, `MySQL`

---

## 🔥 Strength

- 커널 레벨까지 분석 가능한 보안 엔지니어
- 공격자 관점에서 탐지 구조 설계 가능
- PoC → 운영 구조까지 연결 경험
- 단순 개발자가 아닌 “탐지 시스템 설계자”

---

## 🎯 Target Position

- Kernel Security Engineer
- Security Agent Developer
- EDR / XDR / Endpoint Security Engineer
- Linux 기반 보안 솔루션 개발자

---

## 📫 Contact

- Email: dlwlsgh45@naver.com
