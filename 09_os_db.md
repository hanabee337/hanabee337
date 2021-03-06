#Day9
#운영체제와 데이터 베이스
###운영체제
**운영체제**란 시스템 소프트웨어의 일종.
하드웨어 <-> 운영체제<->응용 프로그램<->사용자  
다양한 운영체제가 존재하는 이유?why? win,linux,ios, android 등등  
운영체제가 필요한 이유? 범용적으로 h/w를 사용할 수 있게 해 줄 수 있는s/w가 필요하였음. why?  
각각의 응용 프로그램의 기능에 맞춰서 컴퓨터를 세팅하는 것이 비효율적.  
Linux 계열에도 다양한 oS, android,ubuntut, fedora, 등등..요구하는 기능들이 서로 달랐음.  
운영체제는 자신의 목적에 맞게 개선되어왔다.  
windows는 범용이 목적, 반대 급부로 어느 하나에도 최적화 되어 있지 않다는 의미.  
즉, 안정성이 Linux, Unix, Win 중에서 가장 낮다.  
그래서, 안정성이 요구되는 은행, 금웅권에선 Unix 계열 OS를 사용한다.

####운영체제의 역할
1. 시스템 하드웨어 관리 -> 사용자 프로그램의 오류나 잘못된 자원 사용을 감시.  
압출력 장치 등의 자원에 대한 연산과 제어를 관리.  
2. (가상) 시스템 서비스 제공 -> 사용자에게 컴퓨터의 프로그램을 쉽고 효율적으로 실행할 수 있는 환경.  
예)폴더같은 걸로 파일에 access하는 것.  
이런 환경이 없다면 직접 하드디스크 특정 sector를 뒤져서 파일에 저장된 위치를 찾아야 하는 번거로움을 없애줌.   
3. 자원관리->컴퓨터 시스템 하드웨어 및 소프트웨어 자원을 여러 사용자 간에 효율적 할당, 관리, 보호. why?  
자원 관리가 필요하지? 자원(메모리)이 한정적이니까.

####프로세스 관리 : 프로세스란?
보조기억장치에 저장된 프로그램을 CPU가 호출하면 주기억장치(RAM)에 loading됨.  
즉, 잠자고 있던 프로그램을 호출하여 주기억장치에서 현재 실행되고 있는 프로그램을 프로세스라고 한다.  

####프로세스 상태
생성 : 프로세스가 생성, 
준비 : cpu에 의해 프로세스가 실행되기를 기다림.  
      중간에 다른 인터럽트에 의해 중단되면 실행에서 준비상태로 이전  
      (why? -> cpu가 다른 프로세스들도 처리해야 하므로). 
실행: cpu에 의해 프로세스가 실행  
대기: 어떤 사건(event)이 일어나기를 기다림. idle 상태. 
종료: 프로세스의 종료

1.5ghz : 1.5 X 2^30(giga) x 64bit : cpu가 1초에 처리하는 양.  

####프로세스 scheduling
1. FCFS : 준비  상태 큐에 도착한 순서에 따라 차례로 cpu를 할당.  
문제점:우선순위가 밀림. 앞에 먼저 도착한 놈이 너무 무거운 놈이면 뒤의 놈들은 다 wait해야만 함.  
2. SJF : 실행 시간이 가장 짧은 프로세스에게 cpu 먼저 할당. 평균 대기시간이 가장 적은 알고리즘.  
         실행 시간이 긴 프로세스는 우선순위에 밀려 무한 연기상태 발생가능.  
3. round robin : 시분할 시스템을 위해 고안된 방식. fcfs 변형. 각 프로세스 시간 할달량 동안만 실행.  
                 완료되지 않으면 다음 프로세스에게 cpu를 넘겨주고 준비상태 큐의 가장 뒤로 배치.  
                 할당된 시간이 클수록 fcfs과 비슷. 할당 시간이 작을 수록 context switch와 오버헤드가 자주 발생.  
4. priority based: 각 프로세스마다 우선순위 부여. 우선순위가 동일한 경우 fcfs 기법을 할당.  
                   가장 낮은 순위를 부여받은 프로세스의 무한 연기 발생가능.  
5. multi queue : 프로세스를 특정 그룹으로 분류할 수 있는 경우, 그룹에 따라 각기 다른 준비단계 큐 사용.  
                 준비상태 큐 마다 다른 스케쥴링 기법 사용가능. 다른 준비상태 큐로 이동 불가.  
                 하위단계 준비 큐에 있는 프로세스를 실행하는 도중이라도 상위 단계 준비상테 큐에 프로세스가 들어오면  
                 상위단계 프로세스에게 cpu를 할당.  

####주기억장치
**단순관리**
-> cpu에서 메모리가 부족하면 응용프로그램에 유휴 메모리 반납하라는 command를 보냄.  
   즉, 응용 프로그램이 cpu command에 맞는 처리를 해주어야 한다.  
응용 프로그램이 리소스를 너무 많이 차지하거나 read-only 영역을 access 하는 경우 등을  
운영체제는 monitoring하고 있다.  

**가상 메모리**
-> 보조기억 장치를 주기억장치처럼 활용.  
   주기억장치의 메모리 공간이 부족할 경우,  
   cpu에서는 보조기억장치의 일부를 주기억장치의 일부처럼 간주하여 사용할 때,  
   사용된 보조기억장치의 일부분을 가상 메모리라 한다.    
   가상 메모리는 성능에 치명적...    
RAM disk는 반대 개념: 보조기억장치는 속도가 너무 느리니,    
주기억장치의 일부를 보조기억장치의 일부처럼 할당하여 읽고 쓰는 작업을 진행.  

Appl <-> OS <-> H/W  
-> h/w 통제, 관리 하는 기능을 kernel에서 함. 운영체제의 핵심.    
   그 외는 user interface, ux 등의 기능 등이 OS에서 수행한다.  
   표준화된 드라이버들은 커널단에서 처리가 가능하나, 제조사들마다 h/w 표준이 다른 경우,    
   이를 지원하기 위해 드라이버가 존재한다.  

*SSD : random access  방식으로 데이타 접근.(주소 어드레스와 데이터 어드레스)

**파일관리**
-> cpu는 인덱스 테이블을 참조하여 해당 파일의 위치를 알아냄.  
   특정 파일을 저장하게 되면, 이 파일에 대한 관련 정보를 인덱스 테이블에 저장해 놓는다.  
   포맷이라고 하는 동작이 결국 인덱스 테이블(파일 시스템)을 날려 버리는 것이다.  
   파일시스템을 날려버려도 복원 업체에서는 파일 시스템 포맷에 의한 분석이 가능하므로 복원이 가능함.  
**파일 시스템** : 파일과 그 안에 든 자료를 저장하고 찾기 쉽게 유지,관리하는 방법을 말함.  
 
운영 체제마다 파일 시스템이 다르다. 그리고, 파일 시스템마다 인덱스 테이블이 다르다.  
파일 경로를 표현하는 방식이 서로 다르다는 의미.  
파일 확장자를 변경해도 파일의 내용이 바뀌는 것이 아니므로 정상 동작을 한다.  
예) text.txt -> text.exe로 바꾸어도 메모장에서 읽어 볼 수 있다.  
확장자는 단지 파일의 identity를 user에게 알려주는 힌트일 뿐.  
파일의 정보는 모두 인덱스에 저장되어 있기 때문에  
확장자가 변경이 되어도 정상동작이 가능한 것임.  

조각모음이란 메모리가 조금씩 조각난 메모리들을 물리적으로 하나로 이어서 재배치하는 것임.  
mac에선 조각나 떨어져 있는 메모리들에 대한 정보를 알아서  
파일 시스템에 저장해서 window처럼 조각모음이 없다.  

가상 메모리는 SSD에선 비추. 가상 메모리란 보조기억장치를 주기억장치처럼 쓴다는 건데..  
주기억장치는 cpu에서 자주 access하므로 cell의 수명이 쩗아지게 된다.  

###**커널**
운영체제의 핵심.
보안, 자원관리, 추상화(?)
각자 운영체제마다 고유의 커널이 있음.

**생각해보기**
컴퓨터에서 mp3 player를 동작시켰을 때, 컴퓨터에서 일어나는 flow를 생각해보기.  
1. 마우스등의 인터페이스로 해당 프로그램 클릭.  
2. 마우스를 움직이므로 인터럽트 발생. 배경 화면 및 아이콘 refreshing.  
3. 마우스로 클릭시 이벤트 발생.   
4. 해당 파일에 대한 위치 정보 확인  
5. 해당 프로그램을 메인 메모리로 loading  
6. 그럼, app은 cpu로부터 해당 파일의 위치를 알고 실행함.  

##연산 프로세스 과정(동작체험)
1. 사용자 : 연산명령을 입력장치를 통해 전달
2. 입력장치 : 응용프로그램에게 사용자입력 전달
3. 응용프로그램: 주기억장치로 명령 복사
4. 주기억장치: cpu로 명령 복사
5. cpu: 명령 수행 후 주기억장치로 결과 복사
6. 응용프로그램: 결과값을 보조기억장치에 저장
7. 응용프로그램: 결과값을 출력장치로 전달
8. 출력장치:사용자에게 전달
 
 **멀티태스킹**
 1. 싱글코어 멀티태스킹
 2. 멀티코어 멀티태스킹
  
  
#데이터베이스
방대한 양의 정보 및 데이터에 대한 체계적 관리, 운영하는 시스템
모아놓은 데이터를 어떻게 효율적으로 저장을 하고  
쉽게 꺼내 쓸 수 있을까에 대한 관리 시스템.


#자료구조 vs 데이터 베이스
자료구조 : 대부분 주기억장치에서 이루어질 내용
데이터 베이스: 대부분 보조기억장치에서 이루어질 내용

**데이터 베이스의 종류**
관계형 : 대규모에서 많이 쓰임. 다른 데이터 베이스에 비해 속도가 빠름.  
설계 수정, 구조 변경(추가, 삭제)등의 DB migration이 어렵다.  
데이터들의 관계를 토대로 만든 시스템이 관계형 DB.  
따라서, 초기에 효율적으로 설계하는 것이 어렵다. 이러한 과정을 정규화라고 한다.
키값형:
객체형:
문서형:
컬럼형:  
    
#DBMS
데이터베이스의 운영체제.
DB에 접근할 수 있는 기능을 제공하는 시스템 소프트웨어이다.
종류) MySQL, SQLite...
DBMS마다 제공하는 기능이 다르다. 업체는 목적에 맞는 DBMS를 사용한다.

**DB != DBMS**
DB는 관계형, 객체형...  
DBMS는 MySQL, SQLite...  

##SQL
DBMS를 통해 데이터를 관리하기 위한 구조화된 질의문을 작성하기 위한 언어.
관계형 데이터 베이스 관리 시스템에서 사용.
(Django에서는 관계형 DB를 사용하지 않지만, 현업에서는 관계형 DB, SQL을 쓰는 데가 많음)
