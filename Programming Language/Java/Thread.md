## <u>[쓰레드]</u>

<br>

### _`멀티 쓰레드`_

<br/>

> 쓰레드

- 프로세스: 실행 중인 하나의 애플리케이션(프로그램)
- 쓰레드: 프로세스 내에서 작업을 처리하기 위한 <u>코드 실행 흐름</u>
- 프로세스 시작되면 메인 쓰레드가 생성되고, 프로세스 시작

- **_멀티 쓰레드_**

  - 하나의 프로세스 내에 두 개 이상의 쓰레드가 있을 경우
  - 각각의 쓰레드는 해당 작업을 처리하기 위해 별도의 코드 실행 흐름 생성 <br/>
    ex) 다중 채팅 시스템
  - 멀티 프로세스: 운영체제에서 여러 개의 프로세스들이 동시에 실행됨
  - 멀티 쓰레드: 하나의 프로세스 내에 여러 개의 작업 동시에 처리

<br/>

> 메인 쓰레드

- 모든 자바 애플리케이션은 메인 스레드가 main() 메소드 실행하면서 시작됨
- main() 메소드의 첫 코드부터 아래로 순차적 실행
- 필요에 따라 다른 작업 쓰레드들을 만들어 병렬로 실행 가능
- 대부분 쓰레드 끝나는 시점 다름
- 프로세스 내에서 실행 중인 쓰레드가 하나라도 있으면 프로세스 종료 X <br/>
  (main 쓰레드가 종료되었다고 해서 프로세스 종료 X)

<br/>

> 작업 쓰레드 생성과 실행

- 멀티 쓰레드 애플리케이션 개발 위해 몇 개의 작업을 병렬로 실행할 지 우선 결정
- 각 작업별 쓰레드 생성 방법

  1. Thread 클래스로부터 직접 Thread 객체 생성

     - Thread thread = new Thread(Runnable target);
     - Runnable 구현 객체: 쓰레드가 처리해야 할 하나의 작업 <br/>
       (Runnable은 interface type)

       ```java
       // [방법1] - Runnable 구현한 명시적 클래스에서 run() 재정의
       class Task implements Runnable {
         @Override
         public void run() {
           쓰레드가 실행할 코드;
         }
       }

       Runnable task = new Task();
       Thread thread = new Thread(task);

       // [방법2] - 익명 구현 객체로 run() 재정의
       Thread thread = new Thread(new Runnable() {
         @Override
         public void run() {
           쓰레드가 실행할 코드;
         }
       }

        // 작업 쓰레드 실행 (새로운 코드 실행 흐름 생성됨)
        thread.start()
       ```

     <br/>

  2. Thread 하위(자식) 클래스로부터 생성

     - Thread의 하위 클래스로 작업 스레드 정의하면서 작업 내용 포함

       ```java
       // [방법1] - Thread 상속한 명시적 자식 클래스에서 run() 재정의
       public class WorkerThread extends Thread {
         @Override
         public void run() {
           쓰레드가 실행할 코드;
         }
       }

       Thread thread = new WorkerThread();

       // [방법2] - 익명 자식 객체로 run() 재정의
       Thread thread = new Thread() {
         @Override
         public void run() {
           쓰레드가 실행할 코드;
         }
       }

       // 작업 쓰레드 실행
       thread.start();
       ```

<br/>

> 동기화 메소드

#

## [Note]

- Toolkit 클래스; java.awt package; java UI 프로그램 개발 시 활용
- 새로운 쓰레드 실행 위해서는 쓰레드 생성 후 start() 반드시 호출!

#

### [Reference]

[Reference0](https://cafe.naver.com/thisisjava/25116)
<br/>
