# 👋 이진호 | Kernel-Level Security Engineer
**eBPF / Linux 기반 커널 위협 탐지 시스템 설계자**

> 탐지되지 않던 위협을 발견하는 것이 아니라,  
> **탐지할 수 있는 구조로 문제를 재정의하는 엔지니어**

- Red Team 10년 경험 기반 **공격자 관점 문제 정의**
- eBPF 기반 **커널 행위 추적 및 탐지 구조 설계**
- PoC → 운영 구조까지 연결하는 **실전형 시스템 설계 능력**

---

## 🚀 Summary

10년간 Red Team 및 침해사고 대응을 수행하며  
단순히 “공격을 수행하는 것”이 아니라

👉 **“왜 기존 방식으로는 탐지/공격이 안 되는가”를 구조적으로 분석**

이 경험을 바탕으로:

- 탐지 불가능 영역 정의
- 커널/네트워크 레벨 구조 재설계
- PoC 검증
- 운영 가능한 시스템으로 확장

👉 **문제를 해결하는 것이 아니라, 문제 자체를 재정의하는 방식으로 접근**

---

# 🛡️ Core Project

## BPFdoor Detection Engine
**eBPF 기반 커널 레벨 위협 탐지 시스템**

### 🧠 한 줄 요약
> “탐지되지 않던 위협”이 아니라  
> **탐지할 수 없는 구조를 탐지 가능한 구조로 재설계**

---

### 📌 Problem

- 커널 은닉형 백도어는 기존 EDR로 탐지 어려움
- 로그 기반 탐지는 유저 영역 의존 → 구조적 한계

👉 단순 기술 문제가 아니라  
**탐지 관점 자체의 문제**

---

### 🔥 Insight

> “이건 탐지 기술 문제가 아니라  
> **관찰 위치(Observation Layer)의 문제다**”

- 유저 영역이 아닌  
👉 **커널 레벨에서 직접 행위 관찰 필요**

---

### ⚙️ Solution

- eBPF 기반 커널 이벤트 추적 시스템 설계
- 프로세스 / 소켓 / 패킷 단위 행위 수집
- 이벤트 간 상관관계 분석 구조 설계
- 공격 시나리오 기반 탐지 모델 정의

👉 **행위 흐름 기반 탐지 구조 설계**

---

### 📊 Result

- 커널 레벨 행위 기반 탐지 PoC 개발 완료
- 기존 로그 기반 대비 탐지 범위 확장
- 다양한 공격 시나리오 검증

---

### 🧠 Impact

- 커널 레벨 위협 대응 가능성 검증
- EDR/에이전트 구조로 확장 가능한 기반 확보

---

### 🧠 Tech
C, eBPF, Linux Kernel

---

# 🤖 System Architecture Project

## 실시간 센서/로봇 모니터링 시스템

### 🧠 한 줄 요약
> 동작하는 시스템이 아니라  
> **문제 발생 시 이해 가능한 구조로 재설계**

---

### 📌 Problem

- 데이터 흐름 불명확 (책임 경계 없음)
- 실시간 처리 + 저장 로직 혼재
- 장애 발생 시 원인 추적 어려움

---

### 🔥 Insight

> “문제는 성능이 아니라  
> **구조가 관찰 불가능한 것**”

---

### ⚙️ Solution

- Sensor → Agent → Backend → Web 구조 설계
- 이벤트 처리 파이프라인 구축  
  (수집 → 검증 → 표준화 → 저장)
- Hot Path / Cold Path 분리
- WebSocket 기반 실시간 처리

---

### 📊 Result

- 40개 센서 실시간 처리 안정화
- 장애 원인 추적 가능 구조 확보
- 운영/디버깅 가능한 시스템으로 개선

---

### 🧠 Tech
Spring, WebSocket, PostgreSQL

---

# 🏢 Backend Project

## ERP System (0 → 1 구축)

### 🧠 한 줄 요약
> 복잡한 도메인을 단순화한 것이 아니라  
> **변화 대응 가능한 구조로 재설계**

---

### 📌 Problem

- 복잡한 도메인 + 잦은 요구사항 변경
- 성능 저하 및 데이터 일관성 문제

---

### 🔥 Insight

> “문제는 로직이 아니라  
> **도메인 구조가 흐름을 반영하지 못하는 것**”

---

### ⚙️ Solution

- 도메인 기반 모듈 구조 설계
- 데이터 흐름 중심 API 설계
- 병목 구간 식별 및 쿼리 최적화

---

### 📊 Result

- 응답 속도 40% 이상 개선
- 유지보수 가능한 구조 확보

---

### 🧠 Tech
Java, Spring, MySQL

---

# 🧩 Additional Experience

- MES 입력 검증 및 RBAC 설계
- 급여 시스템 감사 추적 구조 설계
- 침해사고 대응 및 Red Team 협업 (10년)

---

# 🛠 Core Skills

### Security / Kernel
- eBPF 기반 이벤트 추적
- Kernel / Network 행위 분석
- 공격 시나리오 기반 탐지 설계

### Backend / System
- 시스템 아키텍처 설계 (0→1)
- 이벤트 처리 파이프라인 설계
- Observability 설계

### Languages
C, Java, Python, C#

---

# 🔥 Strength

- 커널 레벨까지 내려가 문제를 재정의하는 능력
- 공격자 관점 기반 탐지 구조 설계
- PoC → 운영 구조까지 연결 경험

👉 단순 개발자가 아닌  
**문제 정의부터 시작하는 시스템 설계자**

---

# 🎯 Target Position

- Kernel Security Engineer  
- Security Agent Developer  
- EDR / XDR Engineer  
- Linux 기반 보안 솔루션 개발자  

---

# 📫 Contact

Email: dlwlsgh45@naver.com
