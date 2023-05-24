# git project
* top, ps, jobs, kill 명령어 조사
---

## top 명령어
### 개념
top 명령어는 메모리 사용량, CPU 사용량 등을 나타내주며 top를 실행하는 동안 시스템의 프로세스와 메모리 사용상태를 5초의 간격으로 업데이트 하여 화면에 출력한다.

### 명령어 사용시 출력예시
![image](https://github.com/Yhyun22/gitproject/assets/133829796/581f06f3-5474-4221-8d23-36d969145192)

출력 화면에는 많은 정보가 나오는데 한줄한줄 살펴보면

#### 1.서버 정보
![image](https://github.com/Yhyun22/gitproject/assets/133829796/b70cf1fe-8ab3-41ae-9a01-63c6b1f79e11)

 top - XX:YY:ZZ, up X days, XX:YY, X users, load average
  * top - XX:YY:ZZ >> 현재 서버의 시간 XX시 YY분 ZZ초
  * up X days >> 현재 까지 X일째 가동중
  * XX:YY >> 현재 까지 XX:YY분째
  * X users >> X명의 사용자 접속 중
  * load average : X, Y, Z >> CPU의 부화율 좌측부터 1분, 5분, 15분의 평균측정

#### 2.프로세스 정보
![image](https://github.com/Yhyun22/gitproject/assets/133829796/208a431b-db80-4648-a208-3ef479003ffb)

Tasks:X total, X running, X sleeping, X stopped, X zombie
  * Tasks:X total >> 총 X개의 프로세스가 가동중
  * X running >> X개의 프로세스 실행 중
  * X sleeping >> X개의 프로세스 대기 중
  * X stopped >> X개의 프로세스 멈춤
  * X zombie >> X개의 좀비상태

#### 3.CPU 정보
![image](https://github.com/Yhyun22/gitproject/assets/133829796/83111495-346b-4fec-9ae4-71d72a9cf95c)

* us >> user. 사용자 공간에서 사용중인 CPU 비중 
  us 란? 
프로세스의 우선순위 기본값보다 높은 우선순위로 사용자 공간에서 실행된 시간
* sy >> system 레벨에서 사용중인 CPU 비중 
* ni >> nice 값. 낮을수록 우선순위가 높음. 
  nice 값이란? 
 프로세스의 우선순위 기본값보다 낮은 우선순위로 사용자 공간에서 실행된 시간. 
* id >> 유휴 상태의 CPU 비중 
* wa >> wait. 시스템이 I/O (입출력) 요청을 처리하지 못한 상태에서 CPU IDLE 상태 비중  

#### 4.메모리 정보
![image](https://github.com/Yhyun22/gitproject/assets/133829796/2b33a88b-a072-4a16-9e95-beac171add39)

1 Mem
  * X total >> 전체적인 물리적 메모리 
  * X free >> 사용되지 않는 여유 메모리 
  * X used >> 사용중인 메모리 
  * X buff/cache >> 버퍼된 메모리 


2 Swap
  * X total > 전체 swap 메모리 
  * X free > 사용되지 않은 여유 swap 메모리
  * X used > 사용중인 swap 메모리 
  * X avail mem > 새로운 애플리케이션을 시작할 수 있는 메모리 양  

#### 이하 화면은 프로세스 상태
  ![image](https://github.com/Yhyun22/gitproject/assets/133829796/9fde4ab5-7af5-4f4e-86b9-fa9803376254)

  * PID >> 프로세스 ID
  * USER >> 프로세스 실행시킨 사용자 ID
  * PR >> priority 프로세스 우선순위 
  * NI >> NICE값. 일의 nice value 값. 낮을수록 우선순위가 높음.
  * VIRT >> 가상 메모리의 사용량 ( swap + RES)
  * RES >> resident size 현재 페이지가 상주하고 있는 크기 
  * SHR >> 분할된 페이지, 프로세스에 의해 사용된 메모리를 나눈 메모리의 총합
  * S  >> 프로세스의 상태 : [ S : Sleeping / R : Running / W: sWapped out process / Z: Zombies ]
  * %CPU >> 프로세스가 사용하는 CPU의 사용률
  * %MEM >> 프로세스가 사용하는 메모리의 사용률
  * COMMAND >> 실행된 명령어 
---
## ps 명령어
### 개념
ps 명령어는 현재 실행중인 프로세스의 목록을 보는 명령어로 top명령어와 유사하다

### 옵션을 사용하지 않고 명령어 사용시 출력예시
![image](https://github.com/Yhyun22/gitproject/assets/133829796/5e122fbf-779a-471f-806f-bd652fa67f8c)

| PID     | TTY                | TIME | CMD|
|----------- |:---------------:| ------:|-----|
|274022 | pts/3| 00:00:00| bash|
|274343 | pts/3| 00:04:00| a.out|
|273214 | pts/3| 00:00:00| ps|


#### 기본화면 출력항목 설명
  * PID >> 프로세스의 식별번호
  * TTY >> 프로세스와 연결된 터미널
  * TIME >> 총 CPU 사용시간
  * CMD >> 실행된 프로세스의 이름 또는 실행된 명령

### ps명령어는 다양한 옵션부여 가능( ps [option] )

#### 자주사용하는 명령어 4가지

  1 -ef >> 모든 프로세스를 풀 포맷으로 출력 
  
  2 aux >> 실행중인 모든 프로세스 확인
  
  3 auxf >> 실행중인 프로세스를 트리구조로 출력
  
  4 auxfww >> 실행중인 프로세스를 트리구조 + 모든 실행중인 옵션 확인가능
  
#### 그외에 명령어
  * -A >> 모든 프로세스 출력
  * -e >> 커널 프로세스를 제외한 모든 프로세스 출력
  * -f >> full 포맷 출력
  * -l >> 긴 포맷으로 출력
  * -M >> 64비트 프로세스 출력
  * -p >> 특정 PID를 지정할 때 사용
  * -r >> 현재 실행중인 프로세서 출력
  * u >> 프로세스 소유자 기준으로 출력


__풀 포맷 출력 결과
![image](https://github.com/Yhyun22/gitproject/assets/133829796/4ae571b1-b98a-44a4-b7c1-d85b0e081cd1)

__긴 포맷 출력 결과 
![image](https://github.com/Yhyun22/gitproject/assets/133829796/b134e90d-3da6-4b47-89eb-9ffedb5b1c8c)

---

## jobs 명령어
### 개념
jobs명령어는 작업의 상태를 표시하는 명령어이다.

### 명령어 사용시 출력될 수 있는 상태값
|상태 | 설명|
|-----|-----|
|Running|작업이 계속 진행중|
|Done| 작업이 완료되어 0을 반환|
|Done(code)|작업이 종료되었으며 0이 아닌 코드 반환|
|Stopped|작업 일시중단|
|Stopped(SIGTSTP)|SIGTSTP시그널이 작업을 일시중단|
|Stopped(SIGSTOP)|SIGSTOP시그널이 작업을 일시중단|
|Stopped(SIGTTIN)|SIGTTIN시그널이 작업을 일시중단|
|Stopped(SIGTTOU)|SIGTTOU시그널이 작업을 일시중단|

### 출력 예시
```bash
[15:51:12 oss]$ jobs
[1]   Stopped                 vi
[2]-  Stopped                 vi
[3]+  Stopped                 vi
```
### jobs의 다양한 옵션
  * jobs또한 옵션과 함께 사용가능
    jobs [옵션][작업번호]

#### 옵션종류
  * -l >> 프로세스 그룹ID를 state 필드 앞에 출력
  * -n >> 프로세스 그룹 중에 대표 프로세스 ID출력
  * -p >> 각 프로세스 ID에 대해 한 행씩 출력
  * command >> 지정한 명령어 실행
---

## kill 명령어
### 개념
kill 명령어는 주로 프로세스를 종료할때 사용한다. 리눅스에서 작업할때 응용프로그램이나 프로세스가 멈출때 사용한다.

#### 사용 방법
kill 명령어의 기본 형태는 다음과 같다.
```bash 
$ kill [option] [pid]
```
  __프로세스를 종료하기 위해서 PID를 알아야하기에 ps명령어가 함께 사용된다.

#### 옵션 종류
  * -9 >> 프로세스아이디(PID)를 직접 지정하여 종료시 사용됨
  * -l >> 지원하는 시그널의 목록을 확인할 수 있다. (프로그램을 강제 종료하는 kill은 9번시그널에 해당한다)



