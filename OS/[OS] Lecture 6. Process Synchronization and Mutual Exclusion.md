# [OS] Lecture 6. Process Synchronization and Mutual Exclusion



## 1. `동기화(Process Synchronization)`란?

> `다중 프로그래밍 시스템` 에는 여러 개의 프로세스가 존재. 이 때 프로세스 들은 독립적으로 동작하기 때문에 `공유자원` 혹은 `데이터`가 있을 때, 문제가 발생할 수 있다.
>
> **즉,  `동기화(Synchronizaion)`을 통해 프로세스 들이 서로 동작을 맞추고, 정보를 공유하게 된다!**



- 비동기적(Asynchronous)

  - 프로세스들이 서로에 대해 모름

- 병행적(Concurrent)

  - 여러개의 프로세스들이 동시에 시스템에 존재

  -> `병행` 수행중인 `비동기적 프로세스`들이 공유 자원에 동시에 접근 할 때, 문제 발생 가능!!



### 용어 정리

- `Shared data(공유 데이터)` or `Critical data`
  - 여러 프로세스들이 공유하는 데이터
- `Critical section(임계 영역, CS)`
  - 공유 데이터를 접근하는 코드 영역(Code Segment)
- `Mutual exclusion(상호배제)`
  - 둘 이상의 프로세스가 동시에 `Critical Section`에 진입하는 것을 막는 것



### 기계어(Machine instruction)의 특성

- Atomicity(원자성)
- Indivisible(분리 불가능)
- **한 기계어 명령의 실행 도중에 인터럽트 받지 않음**



![image-20210630201255523]([OS] Lecture 6. Process Synchronization and Mutual Exclusion.assets/image-20210630201255523.png)



- `Race Condition`
  - 수행 순서에 따라 결과가 달라질 수 있는 경우
  - 이러면 안돼!!!



## 2. Mutual Exclusion(상호배제)



![image-20210630201406253]([OS] Lecture 6. Process Synchronization and Mutual Exclusion.assets/image-20210630201406253.png)

- 누군가 Critical Section에 있다면 다른 친구가 진입 금지!!!



### 2-1. Mutual Exclusion Methods

- `Mutual Exclusion primitives`       *`Primitive` : 기본연산 정도로 해석하면 된다.
  - enterCS() primitive
    - Critical Section 진입 전 검사
    - 다른 프로세스가 Critical section 안에 있는지 검사
  - exitCS() primitive
    - Critical setcion을 벗어날 때의 후처리 과정
    - Critical section을 벗어남을 시스템이 알림
- `Requirements for ME primitives`
  - **Mutual exclusion (상호 배제)**
    - Critical Section(CS) 에 프로세스가 있으면, 다른 프로세스의 진입을 금지
  - **Progress (진행)**
    - CS 안에 있는 프로세스 외에는, 다른 프로세스가 CS에 진입하는 것을 방해하면 안됨.
  - **Bounded waiting (한정 대기)**
    - 프로세스의 CS 진입은 유한시간 내의 허용되어야 함

​	

### 상태 1

![image-20210630202147429]([OS] Lecture 6. Process Synchronization and Mutual Exclusion.assets/image-20210630202147429.png)

-  **`Progress (진행)` 조건 위배**
  - 한 프로세스가 죽었거나, 다른 프로세스가 먼저 준비가 됐을 때, 들어갈 수 없다



### 상태 2

![image-20210630202315204]([OS] Lecture 6. Process Synchronization and Mutual Exclusion.assets/image-20210630202315204.png)

- **`Mutual exclusion` 조건 위배**
  - 중간에 `Preemption`된다면 CS안에 둘이 들어가는 상황 발생 가능



### 상태 3

![image-20210630202609082]([OS] Lecture 6. Process Synchronization and Mutual Exclusion.assets/image-20210630202609082.png)

- **`Progress`, `Bounded waiting` 조건 위배**
  - 중간에 `Preemption` 됐을 때, 둘다 `while`문에서 대기하는 상황이 발생할 수 있음



## 2-2. Mutual Exclusion Solution

- SW solutions
  - Dekker's algorithm (Peterson's algorithm)
  - Dijstra's algorithm, Knuth's algorithm, Eisenberg and McGuire's algorithm, Lamport's algorithm
- HW solutions
  - TestAndSet(TAS) instruction
- OS supported SW solution
  - Spinlock
  - Semaphore
  - Eventcount/sequencer
- Language-Level solution
  - Monitor



## 2-3. Dekker's Algorithm

- Two Process ME을 보장하는 최초의 알고리즘
- 위의 Version1과 Version3를 합친 형태



![image-20210701000948767]([OS] Lecture 6. Process Synchronization and Mutual Exclusion.assets/image-20210701000948767.png)





## 2-4. Peterson's Algorithm

- `Dekker's Algorithm`보다 간결하게 구현



![image-20210701001204253]([OS] Lecture 6. Process Synchronization and Mutual Exclusion.assets/image-20210701001204253.png)









###### 	*이  [강의](https://www.youtube.com/playlist?list=PLBrGAFAIyf5rby7QylRc6JxU5lzQ9c4tN)를 통해 공부하고 배운 내용을 정리하였습니다.