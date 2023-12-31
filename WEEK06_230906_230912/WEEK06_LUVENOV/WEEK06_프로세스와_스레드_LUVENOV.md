# WEEK06_CPU 스케줄링 알고리즘

---

# 3.4 CPU 스케줄링 알고리즘

---

- CPU 스케줄러는 CPU 스케줄링 알고리즘에 따라 프로세스에서 해야 하는 일을 스레드 단위로 CPU 할당

![Untitled](WEEK06_CPU%20%E1%84%89%E1%85%B3%E1%84%8F%E1%85%A6%E1%84%8C%E1%85%AE%E1%86%AF%E1%84%85%E1%85%B5%E1%86%BC%20%E1%84%8B%E1%85%A1%E1%86%AF%E1%84%80%E1%85%A9%E1%84%85%E1%85%B5%E1%84%8C%E1%85%B3%E1%86%B7%2078c68139943e406ea0136abc365bb5b8/Untitled.png)

- 프로그램이 실행 시 CPU 스케줄링 알고리즘이 어떤 프로그램에 CPU 소유권을 줄 것인지 결정
- **CPU 이용률은 높게**, **주어진 시간에 많은 일을 수행하도록**, **준비 큐에 있는 프로세스는 적게**, **응답 시간은 짧게** 설정하도록

## 3.4.1 비선점형 방식(non-preemptive)

- 프로세스가 스스로 CPU 소유권을 포기하는 방식이며, 강제로 프로세스 중지 X
- 컨텍스트 스위칭으로 인한 부하가 적음

### FCFS(First Come, First Served)

- 가장 먼저 온 것을 가장 먼저 처리하는 알고리즘
- 단점 : 길게 수행되는 프로세스 때문에 ‘준비 큐에서 오래 기다리는 현상(convoy effect)’ 발생

### SJF(Shortest Job First)

- 실행 시간이 가장 짧은 프로세스를 가장 먼저 실행하는 알고리즘
- 긴 시간을 가진 프로세스가 실행되지 않는 현상(starvation)이 일어나며 평균 대기 시간 가장 짧음
- BUT 실제로는 실행 시간을 알 수 없기 때문에 과거의 실행 시간을 토대로 추측해서 사용

### 우선 순위

- 기존 SJF 스케줄링의 경우 긴 시간을 가진 프로세스가 실행되지 않는 현상 존재
- 오래된 작업일수록 우선 순위를 높이는 방법(aging**)**을 통해 단점을 보완한 알고리즘

## 3.4.2 선점형 방식(preemptive)

- 현대 운영체제가 사용하는 방식
- 현재 사용 중인 프로세스를 알고리즘을 통해 중단시키고 강제로 다른 프로세스에 CPU 소유권을 할당하는 방식

### 라운드 로빈(RR, Round Robin)

- 현대 컴퓨터가 쓰는 스케줄링인 우선순위 스케줄링(priority scheduling)의 일종
- 각 프로세스에 동일한 할당 시간 배정 후 해당 시간 내에 종료되지 않으면 다시 준비 큐(ready queue)의 뒤로 이동
    
    ex ) q만큼의 할당 시간이 부여되었고 N개의 프로세스가 운영된다고 하면 (N-1)&q 시간이 지나면 자기 차례가 오게 됨
    
- 할당 시간이 너무 크면 FCFS가 되고 짧으면 컨텍스트 스위칭이 잦아져 오버헤드 발생(비용 ↑)
- 일반적으로 전체 작업 시간은 길어지나 평균 응답 시간은 짧아진다는 특징 존재
- 로드밸런서에서 트래픽 분산 알고리즘으로도 사용

### SRF(Shorttest Remaining Time First)

- 중간에 더 짧은 작업이 들어오면 수행하던 프로세스 중지 후 해당 프로세스 수행
    
    ↔ SJF : 중간에 실행 시간이 더 짧은 작업이 들어와도 기존 짧은 작업을 모두 수행하고 그 다음 짧은 작업 수행
    

### 다단계 큐

- 우선순위에 따른 준비 큐를 여러 개 사용하고, 큐마다 라운드 로빈이나 FCFS 등 다른 스케쥴링 알고리즘을 적용한 것을 의미
- 큐 간의 프로세스 이동이 불가하므로 스케줄링 부담이 적으나 유연성이 떨어짐

![Untitled](WEEK06_CPU%20%E1%84%89%E1%85%B3%E1%84%8F%E1%85%A6%E1%84%8C%E1%85%AE%E1%86%AF%E1%84%85%E1%85%B5%E1%86%BC%20%E1%84%8B%E1%85%A1%E1%86%AF%E1%84%80%E1%85%A9%E1%84%85%E1%85%B5%E1%84%8C%E1%85%B3%E1%86%B7%2078c68139943e406ea0136abc365bb5b8/Untitled%201.png)