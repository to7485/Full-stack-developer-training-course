# 스레드
- 우리는 컴퓨터로 문서를 작성하면서 동시에 음악을 듣고, 메신저를 사용할 수 있다.
- 이처럼 동시에 두 가지 이상의 작업을 처리하는 것을 '멀티태스킹'이라고 한다.
- 컴퓨터는 어떻게 여러 가지 작업을 동시에 할 수 있을까?
- 컴퓨터에는 멀티태스킹을 위해 '프로세스'와 '스레드'라는 두 가지 도구가 있다.

## 프로세스
- 컴퓨터에 저장되어 있는 파일을 실행하는 순간 메모리에 올라가고 동작하게 되는데 이 상태를 프로세스 라고 한다.
- 프로세스는 독립적으로 메모리에 등록되므로 여러 개의 프로그램을 동시에 실행할 수 있다.

## 스레드
- 프로스세 내부에 존재하면서 실행 흐름을 나타내는 것

## 프로세스가 실행되는 방식
1. 시간 분할 방식 : 모든 프로세스에게 동일한 시간을 할당하고 골고루 실행되는 방식
2. 선점형 방식 : 각각의 프로세스에게 우선 순위를 부여하고 높은 순으로 실행되는 방식


## jvm이 스레드 처리시 하는 일
- 스레드 스케쥴링
- 스레드가 몇 개 존재하는지
- 스레드가 실행되는 프로그램 코드의 메모리 위치가 어딘지
- 현재 스레드의 상태는 무엇인지
- 스레드의 우선순위는 몇인지

## 개발자가 스레드 처리시 하는 일
- 자바 스레드로 작동할 작업이 무엇인지 코드로 작성
- 스레드 코드가 실행할 수 있도록 JVM한테 요청

## 스레드의 생성
- 스레드를 생성하는 방법에는 두 가지가 있다.

### ThreadTest클래스
```java
public calss ThreadTest extends Thread{
	public void run() { //run()메서드 오버라이딩
		//작업할 내용
	}
}
```

### RunnableTest클래스
```java
public calss RunnableTest implements Runnable{
	public void run() { //run()메서드 오버라이딩 필수!
		//작업할 내용
	}
}
```

### ThreadMain
```java
public class ThreadMain{
    public static void main(String[]args){
	ThreadTest t1 = new ThreadTest(); //객체생성
	t1.start();

	러너블 인터페이스 구현시 스레드 코드가 실행할 수 있도록 JVM에 요청
	ThreadTest t2 = new ThreadTest(); //객체 생성
	Thread t = new Thread(t2);
	t.start();
  }
```

## ThreadTest클래스에 코드 수정하기
```java
public class MyThread extends Thread{

	@Override
	public void run() {
		//프로세스의 독립적인 수행을 위한 영역
		for (int i = 0; i < 10; i++) {
			System.out.println("스레드 진행 중"+i);
		}
	}
}
```

## RunnableTest클래스 코드 수정하기
```java
public class MyThread2 implements Runnable{
	@Override
	public void run() {
		//프로세스의 독립적인 수행을 위한 영역
		for (int i = 0; i < 10; i++) {
			System.out.println("러너블 진행중"+i);
		}
	}
}
```

## ThreadMain클래스에 코드 추가하기
```java
public class ThreadMain {
	public static void main(String[] args) {
		
		MyThread t = new MyThread();
		t.start();//run()메서드를 호출하는 메서드
		//t.run();은 run()메서드를 독립적으로 수행하지 못한다.
		//즉, 일반 메서드처럼 호출해버림.
		//run()메서드의 내용을 별개로 수행하고 싶다면
		//t.start()를 이용해야 함.

		MyThread2 th2 = new MyThread();
		Thread t = new Thread(th2);
		t.start();
		
		for(int I = 0; i< 10; I++) {
			System.out.println("메인함수 실행중" + I);
		}
	}
}
```

## 익명클래스를 람다식으로 표현하기
- Runnable인터페이스를 상속해 구현하지 않고, 익명클래스로 만들어서 사용한다.
```java
package test;

public class Test {
	public static void main(String[] args) {
		//Runnable 인터페이스를 익명 객체로 처리
		Runnable white = () -> {
			while(true) {
				System.out.println("백기 올");
			}
		};
		
		Thread whiteFlag = new Thread(white);
		whiteFlag.start();
		
	}
}
```

## 스레드의 이름,상태,순위
- Thread클래스의 주요 메서드

|메서드|설명|
|-----|-----|
|static Thread currentThread()|현재 수행되는 스레드 객체를 리턴|
|String getName() | 스레드의 이름을 반환
|void setName(String name) | 스레드의 이름을 지정|
|int getPriority()|스레드의 우선순위를 반환|
|void setPriority(int new Priority)|스레드의 우선순위를 지정|
|void start() | 스레드를 시작|

## ThreadName 클래스 생성
```java
public class ThreadName extends Thread {
	@Override	
	public void run() {
		this.setName("Thread3");
		System.out.println("현재실행되고있는스레드의이름: Thread.currentThread().getName());
		System.out.println("현재실행되고있는스레드의상태: Thread.currentThread().getState());
		System.out.println("현재실행되고있는스레드의우선순위: Thread.currentThread().getPriority);
	}
}
```

## MainThread클래스 생성
```java
public static void main(String [] args) {

	ThreadName tn = new ThreadName();
	tn.start();

	System.out.println("현재실행되고있는스레드의이름: Thread.currentThread().getName());
	System.out.println("현재실행되고있는스레드의상태: Thread.currentThread().getState());
	System.out.println("현재실행되고있는스레드의우선순위: Thread.currentThread().getPriority);
}
```

## 스레드 상태
- 스레드는 생성하고 실행, 종료되기까지 다양한 상태를 가진다.
- 각 스레드의 상태는 스레드 클래스에 정의되어 있으며, Thread.State 타입으로 알 수 있다.
- 스레드 상태에 따라 6개의 타입으로 분류하고 있다.

|상태|상수|설명|
|---|----|---|
|생성|NEW|스레드 객체가 생성되었지만 아직 start()메서드가 호출되지 않은 상태|
|대기|RUNNABLE|실행 대기 또는 실행 상태로 언제든지 갈 수 있는 상태|
|일시정지|WATING<br>TIMED_WATING<br>BLOCKED|다른 스레드가 종료될 때까지 대기하는 상태<br>주어진 시간동안 대기하는 상태<br>락이 풀릴 때까지 대기하는 상태|
|종료|TERMINATED|수행을 종료한 상태|

## 1. New와 RUNNABLE,TERMINATED
- 처음 스레드가 생성되면 스레드는 NEW 상태가 된다.
- 생성 이후에 start() 메서드를 실행하면 스레드는 RUNNBLE 상태로 변하고
- 시작 이후에 스레드가 조욜되면 TERMINATED상태가 된다.

## 2.WAIT
- 스레드 WAIT 상태는 필요에 의해서 스레드를 잠시 멈춤 상태로 두는 것
- 스레드를 잠시 멈춤 상토래 만들 때는 일정 시간을 지정하거나, 멈춤 상태의 락이 풀릴 때까지 대기하도록 만들 수 있다.

## 상태변화 메서드
- 스레드의 상태를 변화시키는 다양한 메서드에 대해서 알아보자

|메서드|설명|
|-----|-----|
|static void sleep(long millis) | millisecond에 지정된 시간만큼 대기|
|void join()|현재 스레드는 join()메서드를 호출한 스레드가 종료할 때까지 대기|
|static void yield()| 수행중인 스레드 중 우선순위가 같은 스레드에게 제어권을 넘긴다.|


## sleep()메서드
- sleep(int mils)메서드는 주어진 시간 동안 스레드를 정지시키는 메서드이다.
- 해당 기능은 모든 스레드를 대기시켜주며, 주어진 시간이 지나면 풀리게 된다.

### SleepThread클래스 생성
```java
public class SleepThread extends Thread{
	public void run() {
		System.out.println("카운트다운 5초");
		for(int I = 5; i>=0; I--) {
			if(i!=0) {
				try{
					Thread.sleep(1000);//1000당 1초
				} catch(Exception e) {

				}//catch
			}//if
		}//for
		System.out.println("종료!");
	}
}
```
### SleepMain 클래스 생성
```java
public class SleepMain{
	public static void main(String[] args) {
		SleepThread st = new SleepThread();
		st.start();
	}
}
```

#### 스레드 동기화(Synchronized)
- 휴대폰으로 음악이나 영상을 동기화 하게되면, 동기화가 끝날때까지 휴대폰은 다른작업을 할 수가 없다.
- 두 개 이상의 스레드가 하나의 자원을 공유할 경우, 동기화 문제가 발생한다.
- 변수는 하나인데, 두 개의 스레드가 동시에 한 변수의 값을 변경하다가 오류가 발생할수도 있기 때문입니다.
- 예를 들어, 내가 컴퓨터로 작업을 하다가 잠시 자리를 비운 사이에 누군가가 내 컴퓨터에 손을 대서 내가 하고 있던 작업내용을 바꿔버리지 못하게 하기 위해서, 내 문서작업이 끝날때까지 다른사람이 손대지 못하도록 컴퓨터를 잠궈둘 필요가 있다.
- 이처럼 특정 스레드들이 공유하는 한 개의 자원을 사용중일 때, 현재 자원을 사용중이지 않은 다른스레드가 작업을 수행하지 못하게 하기 위해 동기화가 필요하다.

#### SynchronizedEx 클래스 정의
```java
public class SynchronizedEx implements Runnable{

	private long money = 10000;//잔액
	//money로 셋터겟터부터 만듦
	//run()정의
	
	@Override
	public void run() {
		
		//synchronized키워드를 사용하면 
		//해당 키워드가 명시되어있는 영역이 마무리 될 때까지
		//다른 스레드에서 접근하지 못하게 된다.
		synchronized (SynchronizedEx.class) { //this
			
			for(int i = 0; i < 10; i++){
				
				try {
					Thread.sleep(500);
				} catch (Exception e) {
					e.printStackTrace();
				}
					
				if(getMoney() <= 0)
					break;//잔액이 0이면 for문을 탈출
				//Main까지 만들어 결과 찍어서 보여준 후에
				//if문 주석달고 son이 구동되는 것도 확인해보자.
				//그리고 위의 synchronized (SynchronizedEx.class) 영역도 주석처리해서
				//엄마와 아들이 동시에 돈을 찾는 현상도 확인해보자
				
				//outMoney()함수 먼저 정의한 후에 추가
				outMoney(1000);
			}//for
		}//synchronized
	}//run()

	public long getMoney() {
		return money;
	}

	public void setMoney(long money) {
		this.money = money;
	}
	
	public void outMoney(long howMuch){//출금...ㅠㅠ;; 영어모름ㅠ
				
		//해당 스레드의 이름을 가져옴.
		//이름은 해당 스레드를 생성하는 클래스에서 기재하게 됨
		String threadName = Thread.currentThread().getName();
		
		if(getMoney() > 0){//잔액이 0이상일때 출금가능
		   money -= howMuch;//잔액에서 출금액을 마이너스		
		   System.out.println(threadName + " - 잔액 : " + getMoney() + "원");
			
		}else{
			System.out.println(threadName + " - 잔액이 없습니다.");
		}
	}
}
```
#### SyncMain 클래스 정의

```java
public class SyncMain {
	public static void main(String[] args) {
		SynchronizedEx atm = new SynchronizedEx();
		Thread mom = new Thread(atm, "엄마");
		//Thread.currentThread().getName();이 "엄마"가 된다.

		Thread son = new Thread(atm, "아들");
		
		mom.start();
		son.start();
	}
}
```

## wait()와 notify()
- 여러 개의 스레드가 동시에 동작하다 보면, 하나의 스레드가 완료되어야 다음 스레드가 동작할 수 있는 경우가 있다.
- 예를 들어 한쪽에서는 물건을 나르고, 다른 한쪽에서는 물건을 쌓는 스레드가 있다고 가정해보자.
- 만약 쌓을 물건이 없다면 물건을 나르는 스레드는 할일이 없어진다.
- 이때, 물건을 나르는 스레드를 잠시 중지시키고, 물건이 오면 다시 나르도록 할 수 있다.
- wait()메서드는 스레드를 대기시키고, notify()메서드는 대기중인 스레드를 다시 동작시킬 때 사용한다.
- 두 개 이상의 스레드가 구동중일 때 한 개의 동기화 스레드가 작업을 완전히 마칠때까지 기다렸다가 다른 스레드의 작업이 수행되는 것이 아니라 동기화 진행중에 일시적으로 스레드를 정지시키고 다른 스레드가 작업을 할 수 있다.

### Storage클래스
```java
package test;

public class Storage {
	private int stackCount = 10;
	public synchronized void addStack(int stackCount) {
		this.stackCount += stackCount;
		if(this.stackCount >= 10) {
			System.out.println("== 스레드 깨우기 ===");
			notify();
			//wait()을 만나 대기상태에 빠진 스레드는 notify()를 만나 재 구동된다.
		}
	}
	
	public synchronized void popStack(int leaveCount) {
		try {
			if(leaveCount > this.stackCount) {
				this.stackCount = 0;
			} else {
				this.stackCount -= leaveCount;
			}
			
			if(this.stackCount == 0) {
				System.out.println("== 짐 없음 대기 ===");
				wait();
				//스레드가 진행중에 wait()을 만나면 일시적으로 정지된다.
				//스레드가 구동되고 있을 때 일시적으로 대기상태에 보내고, 다른 스레드에게 제어권을 넘긴다.
				System.out.println("==짐 없음 대기완료===");
			}
		} catch (Exception e) {
			// TODO: handle exception
		}
	}
	
	public int getStackCount() {
		return this.stackCount;
	}
}
```

### ThreadWaitExample클래스
```java
package test;

class AddStackThread extends Thread{
	private Storage stroage;
	public AddStackThread(Storage storage) {
		this.stroage = storage;
	}
	
	@Override
	public void run() {
		try {
			while(true) {
				Thread.sleep(1000);
				if(this.stroage.getStackCount() == 0) {
					System.out.println("짐 10개 추기");
					this.stroage.addStack(10);
				}
			}
		} catch (Exception e) {
			// TODO: handle exception
		}
	}
}

class PopStackThread extends Thread{
	private Storage storage;
	public PopStackThread(Storage storage) {
		this.storage = storage;
	}
	
	@Override
	public void run() {
		try {
			while(true) {
				Thread.sleep(1000);
				System.out.println("짐 5개 나르기");
				this.storage.popStack(5);
			}
		} catch (Exception e) {
			// TODO: handle exception
		}
	}
}


public class ThreadWaitExample {
	public static void main(String[] args) {
		Storage s = new Storage();
		AddStackThread add = new AddStackThread(s);
		PopStackThread pop = new PopStackThread(s);
		
		add.start();
		pop.start();
	}
	
	
}
```

#### Account클래스 정의
```java
public class Account {
	
	int balance = 1000;//잔액
	
	//출금메서드
	public synchronized void withdraw(int money){
		
		//잔액이 출금액보다 적을 경우
		if(balance < money){
			
			try {
				
				wait();//스레드가 일시적으로 정지상태에 빠짐
				
			} catch (Exception e) {
				// TODO: handle exception
			}						
		}
		
		balance -= money;
	}//withdraw()
	
	//입금메서드
	public synchronized void deposit(int money){
		balance += money;
		notify();//정지된 스레드를 실행
	}
}
```

#### AccountThread클래스 생성

```java
public class AccountThread implements Runnable{

	Account acc;//Account객체 준비
	
	//생성자 정의
	public AccountThread(Account acc) {
		this.acc = acc;
	}
	
	@Override
	public void run() {

		while(true){
			
			try {
				
				Thread.sleep(500);
				
			} catch (Exception e) {
				// TODO: handle exception
			}			
			
			//출금액을 100 ~ 300원 사이의 난수로 지정
			int money = (new Random().nextInt(3) + 1) * 100;
			acc.withdraw(money);
			System.out.println("잔액 : " + acc.balance);
		}
	}
}
```
#### AccountMain클래스 정의
```java
public class AccountMain {
	public static void main(String[] args) {

		Account acc = new Account();

		Runnable r = new AccountThread(acc);
		Thread t1 = new Thread(r);

		t1.start();//스레드 구동

		//스레드와는 별개로 값을받아 입금 시키는
		//코드를 수행할 while()문
		while(true){
			Scanner scan = new Scanner(System.in);
			int n = scan.nextInt();
			acc.deposit(n);
		}
	}
}
```

## yield()메서드
- 스레드 자신에게 주어진 실행시간을 다음 차례의 스레드에게 양보(yield)한다.
- 예를 들어 스케쥴러에 의해 1초의 실행시간을 할당받은 스레드가 0.5초의 시간동안 작업한 상태에서 yield()가 호출되면
- 나머지 0.5초는 포기하고 다시 실행대기 상태가 된다.

### YieldTest
```java
public class YieldExample {
    public static void main(String[] args) {
        Thread producerThread = new Thread(new Producer());
        Thread consumerThread = new Thread(new Consumer());

        producerThread.start();
        consumerThread.start();
    }
}

class Producer implements Runnable {
    @Override
    public void run() {
        for (int i = 1; i <= 5; i++) {
            System.out.println("Producer: " + i);
            Thread.yield(); // 다른 스레드에게 CPU 양보
        }
    }
}

class Consumer implements Runnable {
    @Override
    public void run() {
        for (int i = 1; i <= 5; i++) {
            System.out.println("Consumer: " + i);
            Thread.yield(); // 다른 스레드에게 CPU 양보
        }
    }
}
```

## 데몬스레드
- 데몬 쓰레드는 다른 일반 쓰레드의 작업을 돕는 보조적인 역할을 수행하는 쓰레드이다.
- 함께 구동중인 일반 스레드가 종료되면 데몬스레드도 함께 종료된다.
- 예를들어 문서를 작성하는 도중에 3초 간격으로 자동 세이브가 필요하다고 가정하여 코드를 작성해 보자.

### DaemonTest
```java
package test;

public class DaemonMain {
    public static void main(String[] args) {
        // 데몬 스레드를 생성합니다.
        Thread daemonThread = new Thread(new MyDaemonRunnable());
        
        // 데몬 스레드로 설정합니다.
        daemonThread.setDaemon(true);
        
        // 데몬 스레드 시작
        daemonThread.start();
        
        // 메인 스레드에서 1부터 15까지 출력합니다.
        for (int i = 1; i <= 15; i++) {
            System.out.println(i);
            
            try {
                Thread.sleep(1000); // 1초 대기
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
        }
        
        System.out.println("메인 스레드 종료");
    }
}

class MyDaemonRunnable implements Runnable {
    @Override
    public void run() {
            try {
                
                for (int i = 1; i <= 15; i++) {
                    System.out.println("저장되었습니다");
                    Thread.sleep(3000); // 3초 대기
                }
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
        
    }
}
```

### 문제1
- 스캐너를 이용하여 키보드에서 숫자를 입력받고
- 스레드에서 입력받은 숫자가 1씩 감소하다가 0이 되었을 때
- "종료"라는 메시지와 함께 스레드를 빠져나오도록 만들어보자.

### ThreadCount클래스 생성
```java
public class ThreadCount implements Runnable{

	private int n;
	
	public ThreadCount(int n) {
		this.n = n;
	}

		public void run() {		
		for(int i = n; i >= 0; i--){
			
			try {
				System.out.println(i);
				Thread.sleep(1000);
				
			} catch (Exception e) {
			}
		}
		System.out.println("종료");
	}
```

### ThreadCountMain클래스 생성
```java
	public static void main(String[] args) {

		System.out.print("값을 입력 : ");
		Scanner scan = new Scanner(System.in);

		ThreadCount t = new ThreadCount(scan.nextInt());
		Thread tt = new Thread(t);		
		tt.start();
	}

}
```

### 문제2
- QuizThread클래스를 만들어 스레드를 상속 받는다.
- startGame()메서드를 만들고 그 안에서 1 ~ 100사이의 난수 두 개를 더하는 문제를 출제
- 키보드에서 답을 입력하여 5문제가 정답처리 될 때까지 로직을 반복한다.
- 정답을 맞히고 난 후에 모든 문제를 맞히는데 몇 초가 걸렸는지를 화면에 출력하며 프로그램 종료.
- QuizMain클래스를 만들고 이 메인 클래스에서는
```java
QuizThread qt = new QuizThread();
		qt.start();//스레드 구동
		qt.startGame();//문제풀이 함수
```
- 위의 세 줄 이외의 다른 코드는 추가하지 않도록 한다.
- 단, 사용자가 문제의 정답으로 정수 이외의 문자를 입력했을 경우에
- "정답은 정수로 입력하세요"라는 문장이 출력되도록 한다.
```java
---------실행 결과----------- 

23 + 48 = 71
정답!!
66 + 100 = 166
정답!!
68 + 52 = 1
오답
61 + 51 = 112
정답!!
9 + 48 = 57
정답!!
53 + 28 = 81
정답!!
결과 : 24초...
```

### QuizThread클래스 생성
```java
public class QuizThread extends Thread{

	int su1, su2;
	int timer = 0;
	int playCount = 0;
	boolean isCheck = true;
	final int FINISH = 5;//출제 문제 갯수

	public void startGame(){

		while(isCheck){

			try {
				su1 = new Random().nextInt(100) + 1;
				su2 = new Random().nextInt(100) + 1;
				System.out.print(su1 + " + " + su2 + " = ");
				Scanner scan = new Scanner(System.in);
				int result = scan.nextInt();

				if(result == (su1 + su2)){
					System.out.println("정답!!");
				}else{
					System.out.println("오답");
					continue;
				}	

				playCount++;

				if(playCount == FINISH){
					System.out.println("결과 : " 
							       + timer + "초...");
					isCheck = false;
				}
				
			} catch (Exception e) {
				System.out.println("정답은 정수로 입력하세요");
			}
		}
	}

	@Override
	public void run() {

		while (isCheck) {

			try {
				Thread.sleep(1000);
				timer++;

			} catch (Exception e) {
				// TODO: handle exception
			}			
		}
	}
}
```
### QuizMain클래스 생성
```java
public class QuizMain {
	public static void main(String[] args) {

		QuizThread qt = new QuizThread();
		qt.start();
		qt.startGame();
		
	}
}
```




