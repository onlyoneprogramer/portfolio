테스트 케이스	내용
TC1	BPFdoor가 특정 포트에 숨겨진 채 리스닝, 외부 접근 시에만 활성화
TC2	syscall table에 bpf(), connect() 등의 항목을 후킹
TC3	netfilter hook에 eBPF map 연결 후 행동 조작
TC4	LKM을 통해 bpf syscall을 감싸는 루틴 삽입
TC5	agent-main이 강제 종료됨 (공격자에 의한 제거 시나리오)
TC6	하이퍼바이저 접근 로그 위조 및 은폐 시도

4.4 실험 결과 및 분석
4.4.1 탐지 정확도
시나리오	탐지 여부 (VMI)	탐지 여부 (Agent)	탐지 여부 (Integrity)
TC1	            ✔	            ✔	                ❌
TC2	            ✔	            ❌	               ✔
TC3	            ✔	            ✔	                ✔
TC4	            ✔	            ❌	               ✔
TC5	            ❌	           ✔	               ❌
TC6	            ✔	            ✔	                ❌
