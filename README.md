# 👋 이진호 | Red Team Security Engineer (10+ Years)

> 🔥 커널 레벨 은닉형 백도어(BPFdoor) 탐지 PoC 개발  
> 🔥 레드팀 10년 + 침해사고 대응 및 협업 경험  
> 🔥 0→1 아키텍처 설계 및 실서비스 구축

---

## 🚀 Summary

10년 이상 레드팀에서 활동하며 커널·네트워크 기반 공격 분석 및 방어 설계를 수행해왔습니다.

- eBPF 기반 BPFdoor 탐지 PoC 개발
- ERP 시스템 성능 개선 (응답 속도 40%+ 향상)
- 실시간 센서/로봇 시스템 아키텍처 설계 및 운영 구조 정립

이론이 아닌, **실제 환경에서 검증된 구조를 설계하고 구현하는 엔지니어**입니다.

---

## 🛡️ BPFdoor Detection Research (핵심 프로젝트)

**한 줄 요약**: 커널 레벨 은닉형 백도어 위협을 모델링하고, 탐지/차단 지점을 정의 후 PoC로 검증

**기간**: 2025.05 ~ 2025.09  

### 📌 Problem
기존 보안 솔루션으로는 커널 레벨 은닉형 백도어(BPFdoor) 탐지가 어려움

### ⚙️ Solution
- eBPF 기반 커널 이벤트 추적 및 행위 분석
- 비정상 프로세스 및 네트워크 패턴 탐지 로직 설계
- 공격 흐름 기반 탐지/차단 모델 정의

### 📊 Result
- PoC 개발 완료
- 기존 방식 대비 탐지 가능 영역 확장
- 논문 및 특허 초안 작성

### 🧠 Impact
- 커널 레벨 위협 대응 가능성 검증
- 실서비스 적용 가능한 탐지 구조 설계

### 🧠 Tech
C, eBPF, Linux Kernel

---

## 🤖 웹 기반 로봇·센서 모니터링 시스템

**한 줄 요약**: 실시간 이벤트 스트림을 수집·검증·가공하여 운영/디버깅 가능한 구조로 재설계

**기간**: 2025.11 ~ 2025.12  
**규모**: 로봇 4대 / 센서 40개

### 📌 Problem
- End-to-End 구조 부재
- 데이터 흐름 및 책임 경계 불명확
- 실시간 처리와 이력 저장 로직 혼재

### ⚙️ Solution
- `Sensor → Edge/Agent → Backend → Web` 구조로 레이어링
- 이벤트 수집 → 정합성 검증 → 표준 포맷 변환 파이프라인 구축
- Hot Path / Cold Path 분리로 성능 및 확장성 확보
- WebSocket 기반 실시간 상태 반영

### 📊 Result
- 40개 센서 실시간 이벤트 처리 구조 확립
- 장애 원인 추적 가능 구조 구축
- 모니터링 시스템을 운영/디버깅 도구로 활용 가능하게 개선

### 🧠 Tech
Spring, WebSocket, PostgreSQL

---

## 🏢 ERP System (0 → 1 구축)

**한 줄 요약**: 복잡한 ERP 도메인을 모듈화하고 성능 병목을 실측 기반으로 개선

**기간**: 2024.01 ~ 2024.05  
**역할**: 단독 개발

### 📌 Problem
- 복잡한 도메인 + 잦은 요구사항 변경
- 성능 병목 및 데이터 일관성 문제

### ⚙️ Solution
- 도메인 단위 모듈화 및 API 구조 정리
- 병목 구간 식별 후 쿼리 및 인덱스 최적화 반복 적용
- 실제 데이터 흐름 기반 API 재설계

### 📊 Result
- 모듈화된 엔터프라이즈 구조 구축
- RESTful API 기반 데이터 흐름 정립
- 응답 속도 **40% 이상 개선**

### 🧠 Tech
Java, Spring, MySQL

---

## 🧩 Other Projects

### MES 모듈 개발
- 입력 검증 및 예외 처리 강화로 데이터 신뢰성 확보
- RBAC 기반 접근 제어 설계

### 스마트 급여 관리 시스템
- 복잡한 급여 정책을 케이스 기반으로 검증
- 감사 추적 가능한 데이터 구조 설계

---

## 🧪 In Progress

### 차세대 커널 위협 탐지·대응 솔루션
- 커널 위협 탐지 → 운영 → 자동화 대응까지 확장 가능한 구조 연구 중

---

## 🛠 Core Skills

### Security / System
- Red Team / 침해사고 대응
- Kernel & Network Analysis
- eBPF 기반 탐지 구조 설계

### Backend / Engineering
- 시스템 아키텍처 설계 (0→1)
- Observability / 운영 구조 설계
- API 및 데이터 흐름 설계

### Languages
- C, Java, C#, Python

### Tech Stack
- Spring / Spring Boot
- WebSocket
- PostgreSQL / MySQL
- Linux

---

## 🔥 Strength

- 커널 레벨까지 분석 가능한 보안 엔지니어
- 공격자 관점에서 방어 구조 설계 가능
- PoC → 운영 구조까지 연결 가능한 경험
- 0→1 시스템 설계 및 실제 서비스 구현 경험

---

## 📫 Contact

- Email: (dlwlsgh45@naver.com)
