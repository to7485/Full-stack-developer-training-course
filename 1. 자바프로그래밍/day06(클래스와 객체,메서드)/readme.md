# 클래스

## 객체지향 프로그래밍
- 객체 지향 프로그래밍이란, 말 그대로 객체를 지향하는 프로그래밍 방법을 말한다.
- 객체란 우리 실생활에 존재하는 모든것으로 생각할 수 있다.
- 객체는 일반적으로 상태를 표현할 수 있고, 우리가 행동으로 실행할 수 있는 모든것들을 의미한다.
- 이런 객체를 중심으로 프로그램 구조를 설계하고 프로그래밍 하는 것을 객체 지향 프로그래밍이라고 한다.

## 클래스란?
- 객체를 생성하기 위한 설명서이다.
- 어떤 물건을 만들기 위한 메뉴얼이라고 생각하면 된다.
- 클래스를 기반으로 객체를 생성해야 한다.
- 하나의 설명서로 여러개의 물건을 만들 수 있듯이, 자바에서는 하나의 클래스로 여러 개의 객체를 생성할 수 있다.

## 클래스의 종류
- 실행용 클래스 
  - 프로그램 전체에서 단 하나의 클래스로, 프로그램의 실행을 맡고 있다.
  - main메서드를 갖고 있으며, 다른 클래스에서 사용하지 않는다.
- 객체 생성용 클래스
  - 다른 클래스에서 사용할 목적으로 선언되는 클래스 입니다.
- 하나의 클래스가 위 두 가지 용도의 역할을 모두 수행할 수 도 있다.
- 하지만 유지 보수와 객체 지향 프로그래밍의 특징인 모듈화를 고려해 별도로 분리하여 작성하는 것이 좋다.
- 일반적으로 하나의 프로그램에서 실행용 클래스 1개를 제외한 나머지 클래스는 모두 참조용 클래스이다.

## 클래스의 선언
```java
접근제한자 class 클래스명{

}
```
### 클래스 이름을 작성하는 규칙
- 영어 대소문자를 사용할 수 있으며 보통 첫 글자는 대문자를 사용한다.
- 숫자를 사용할 수 있으나 첫 글자로는 사용할 수 없습니다.
- 특수문자는 $,_만 가능합니다.
- 자바 예약어(키워드)는 사용할 수 없습니다.

## Cat 클래스 만들기
```java
public class Cat {

}
```

## 객체변수 선언하기
- 객체를 담을 수 있는 변수 선언해보기
```
클래스명 객체명;
Cat c
```

## 객체변수에 대입하기
- 선언한 객체 변수에 객체를 생성해 대입해보기
```java
객체명 = new 클래스명();
```
- 객체를 생성하는 키워드는 new이다.
- 클래스를 이용해 객체를 생성할 수 있도록 도와준다.

## CatMain클래스 만들기
```java
public class CatMain {
	public static void main(String[] args) {
		
		Cat c = new Cat();
	}
}
```
- 클래스는 일반적으로 하나의 소스 파일에 하나의 클래스를 선언합니다.
- 하나의 파일에서 여러개의 클래스를 선언한다면 파일이름과 같은 클래스에만 public을 사용해야 한다.

## Ex1_Class 클래스 작성
```java
package test;

class Cat{ //참조용 클래스의 선언
	
}

public class Test{
	public static void main(String[] args) {
		Cat c = new Cat();
		
	}
}
```
- 하지만 코드를 컴파일한 결과물은 코드 파일을 각각 작성한 것과 동일하게 각 class별로 도출되어 2개가 생성된다.
- 파일 분리 여부와 상관 없이 결과물이 같기 때문에, 분리 여부는 개발자가 원하는 대로 작성해도 무방하다.
- 그러나 추후 유지보수의 편리성과 클래스 재사용을 고려해 하나의 파일에 한 개의 클래스를 작성하는 것을 추천합니다.

# 클래스의 구성
- 클래스를 구성하는 요소는 3가지가 있다.

## 필드(field)
- 객체가 가져야할 데이터의 상태를 저장하는 변수를 말한다.
- 필드, 전역변수, 멤버 변수 라고 부르는데 다 같은말이다.
- 필드의 값을 초기화 하지 않으면 객체 생성시 자동으로 기본값으로 초기화 된다.

```java
package test3;

public class Car {
	//int wheel; //필드 선언
	int wheel = 4; //초기화를 할 수도 있다.

	wheel = 5; //필드에 새로운 값을 넣는것도 가능하다.
}
```
- 필드는 클래스에 포함된 요소이자, 객체를 생성한 후 객체가 가지는 데이터이기도 합니다.
- 따라서 객체를 생성한 후 그 객체의 필드를 사용할 수 있다.
```java
객체명.필드명
```
```java
package test3;

public class CarMain {
	public static void main(String[] args) {
		Car c = new Car();
		System.out.println("wheel의 개수는 " + c.wheel + "개입니다."); //필드의 값 출력
		
		c.wheel = 5;
		System.out.println("wheel의 개수는 " + c.wheel + "개입니다.");
	}
}

```

## 메서드
- 메서드란 클래스 안에서 특정 기능을 수행하기 위해 코드들을 따로 하나의 블록으로 묶어놓은 집합이다.
- 필요에 따라 이 집합을 호출해 사용할 수 있다.
- 우리는 메서드를 구현함으로써, 같은 내용의 코드를 반복적으로 작성해야 하는 상황을 피할 수 있다.
- 반복되는 문장들을 묶어서 메서드로 작성해 놓으면 필요할 때마다 재사용이 가능하며 중복된 코드를 제거할 수 있다.

#### 메서드의 선언
- 메서드는 크게 머리(header)와 몸체(body)로 구성되어 있다.
```java
접근제한자 반환형 메서드명(파라미터){ //머리
	작업할 내용
	return 반환값;
}
```
### 접근제한자
- 접근제한자는 클래스/메서드/필드에 대한 접근을 어디범위까지 제한하느냐에 대한 지시어이다.
1. public : 모든 접근을 허용. 같은 프로젝트 내의 모든 객체들이 사용할 수 있도록 허용.
2. private : 현재 클래스 내에서만 사용을 허가.
3. protected : 상속관계의 객체들에만 사용을 허가.
4. default : 같은 패키지(폴더)내의 객체에만 사용을 허가(아무것도 쓰지 않으면 default)

### 반환형
- 반환형은 메서드가 처음부터 끝까지 수행을 마친 후에 반환해야 할 값이 있을 경우에 기입.
- int, String, boolean등 기본자료형을 포함하여 사용자가 만든 객체로도 반환이 가능.
- 아무것도 반환하지 않을때는 void

### 메서드명(함수명)
- 메서드명은 말그대로 메서드의 이름(첫글자는 소문자로 시작한다.)

### 파라미터(매개변수,인자,아규먼츠)
- 파라미터는 외부에서 해당 메서드를 통해 특정 값을 전달하고자 할 때, 그 특정 값을 받아서 처리할 수 있도록 하는 역할을 하는 변수
- 소괄호 안에 어떤 형태로 값을 받을것인지 선언하면 된다.

```java
package test3;

public class Book {
	public void count(int bookNum) {
		System.out.println("책은 " + bookNum+"권 입니다.");
	}
}
```

```java
package test3;

public class BookMain {
	public static void main(String[] args) {
		Book myBook = new Book(); //객체 생성
		myBook.count(3); //myBook 인스턴스 count메서드 호출
	}
}
```
- 파라미터의 개수에는 제한이 없다.
- 2개 이상의 파라미터를 정의할 때는 콤마(,)를 기준으로 변수를 여러개 만들면 된다.
```java
접근제한자 반환형 메서드명(자료형 변수명1,자료형 변수명2...){

}
```

### return
- 함수에서 모든 작업을 마치고 경우에 따라 실행한 결과를 호출한곳으로 다시 돌려주기도 한다.
- 이것을 '반환한다'라고 표현한다
- 반환하는 결과값을 '반환값'이라고 부르기도 한다.
- 리턴값이 있을 경우에는 리턴할 데이터의 타입이 무엇인지 반환형에 기재해줘야 한다.
- 리턴값이 없는 경우 메서드를 종료하기 위해 return을 사용할 수 있다.
#### Bus클래스
```java
package test3;

public class Buss {

	public void take(int m) {
		while(true) {
			if(m < 3000) {
				System.out.println("교통카드를 충전하러 값니다.");
				return;
			}
			System.out.println("버스를 탑니다.");
			m-=1250;
		}
	}
}
```
#### BusMain클래스
```java
package test3;

public class BusMain {

	public static void main(String[] args) {
		int money = 10000;
		Bus bus = new Bus();
		bus.take(money);
	}
}
```
## 메서드 사용
- 구현한 메서드를 사용하는 방법은 필드의 사용법과 동일하다
- 메서드를 선언한 클래스안에서 메서드를 사용할 때는 단순히 메서드명만 호출하면되지만
- 다른 클래스에서 메서드를 사용하려면 객체를 ㅁ너저 생성한 후 참조 변수를 이용해 그 객체의 메서드를 이용해야 한다.
- 객체가 존재해야 메서드도 존재하기 때문이다.

```java
클래스명 객체명 = new 클래스명();
객체명.메서드명();
```
- Car 클래스에 코드 추가하기
```java
package test3;

public class Car {
	int wheel = 4; //필드 선언
	
	public void ride() {
		System.out.println("달립니다.");
		System.out.println("씽씽");
	}
}
```
- CarMain클래스에서 메서드 호출하기
```java
package test3;

public class CarMain {
	public static void main(String[] args) {
		Car c = new Car();
		System.out.println("wheel의 개수는 " + c.wheel + "개입니다."); //필드의 값 출력
		
		c.wheel = 5;
		System.out.println("wheel의 개수는 " + c.wheel + "개입니다.");
		
		c.ride();
		c.ride();
		c.ride();
	}
}
```
# 자바의 변수와 생명주기
- 자바에는 4가지 종류의 변수가 있다.

## 변수의 종류
1. 지역변수(local variable) : 중괄호 지역 내에서 선언된 변수
2. 매개변수(parameters) : 메서드에 넘겨주는 변수
3. 인스턴스(객체)변수(instance variable) : 참조용 클래스 안에서 만들어진 변수
    - 객체가 생성될 때 객체별로 다른 값을 가질 수 있다.
5. 클래스변수(class variable) :참조용 클래스 안에서 만들어지지만 타입 앞에 static이 있는 변수
    - 인스턴스 변수는 객체마다 다른 값을 가지지만 클래스 변수는 모든 객체가 고유한 값을 갖는다. 

## 변수의 생명주기
1. 지역변수 : 지역변수를 선언한 중괄호 내에서만 유효하다.
2. 매개변수 : 메서드가 호출될 때 만들어지고, 메서드가 끝나면 소멸한다.
3. 인스턴스(객체)변수 : 객체가 생성될 때 만들어지고, 그 객체를 참조하고 있는 변수가 없으면 소멸된다.
    - 가비지 콜렉터(Garbage Collector)가 알아서 메모리를 청소
4. 클래스변수 : 클래스가 처음 호출될 때 생명이 시작되고, 자바 프로그램이 끝날 때 소멸된다.

## 클래스의 로딩
- 자바의 클래스들이 언제 어디서 메모리에 올라가고 클래스 멤버들이 초기화 되는 방법

### JVM의 클래스 로더(class Loader)
- 클래스 로더는 컴파일된 자바의 클래스파일(.class)을 동적으로 로드한다.
- JVM의 메모리 영역인 데이터 영역에 배치하는 작업을 수행한다.
- class파일을 로딩하는 순서
    1. Loading(로드):클래스 파일을 가져와서 JVM의 메모리에 로드한다.
    2. Linking(링크) : 클래스 파일을 사용하기 위해 검증하는 과정
    3. Initializtion(초기화) : 클래스 변수들을 적절한 값으로 초기화 한다.
- 유의할 점은 Loading 기능은 한번에 메모리에 올리지 않고, 어플리케이션에서 필요한 경우 동적으로 메모리에 적재하게 된다는 점이다.
- 곰곰히 생각해보면 언제 어디서 사용될지 모르는 static 멤버들을 처음에 전부 메모리에 올린다는건 비효율적이다.
- JVM은 실행될때 모든 클래스를 메모리에 올려놓지 않고, 그때 마다 필요한 클래스를 메모리에 올려 효율적으로 관리하는 것이다.

### 메모리에 올라가는 시점
1. 객체를 생성했을 때
2. static 변수의 호출 : 클래스 내부의 static멤버를 호출하면, 객체화 하지 않아도 클래스가 로드된다.
3. static 메서드 호출 : static변수를 호출한것과 같이 클래스가 로드된다.
4. 내부클래스 호출 : 내부클래스의 객체를 생성하기 위해선 외부클래스의 객첼르 먼저 생성해야 한다.

- Ex2_valueTest 패키지 생성

## ValueTestMain클래스 작성하기
```java
public class ValueTestMain {
	public static void main(String[] args) {
		// 변수 선언과 값대입
		int su = 100;

		// test라는 메서드를 호출하기 위해 test메서드를 가지고 있는
		// 클래스를 생성한다.
		ValueTest vt = new ValueTest();//명시적 객체 생성
		vt.test(su);// su에 있는 값이 복사되어 전달된다.

		System.out.println("su: " + su);
		
	}
}
```

## ValueTest클래스 작성하기
```java
public class ValueTest {
	
	public void test(int n){
		n++;
		System.out.println("n : " + n);
	}// 메서드의 기능이 모두 끝났으면 호출한 곳으로 돌아간다.
	// 이때 반환형이 있으면 반환값을 가지고 돌아가지만
	// 반환형이 없는 void라면 빈손으로 돌아간다. 그리고 
	// 지역변수 n은 소멸된다.
}
```

# 메서드 실습
- Ex3_methodTest 패키지 작성

## MethodTest클래스작성하기
```java

public class MethodTest {

//배열의 최대값을 찾는 maxFinder메서드
public void maxFinder(int[] arr) {
	//탐색 알고리즘
	int max = arr[0];
	for(int x : arr) {
		if(x > max) max = x;
	}
	
	System.out.println("최대값 : " + max);
}

//main 함수에서 반지름을 받은 후 원의 넓이를 구하는 메소드 circleArea을 만들고
//원의 둘레를 구하는 메소드 circleRound를 만들어라
//단, circleArea 메소드는 함수 안에서 출력문을 출력하고
//circircleRound 메소드는 round 값을 리턴받아서 main함수에 출력하라
//(원의 넓이 구하는 공식 : 3.14 * 반지름 * 반지름, 원의 둘레 구하는 공식 : 2 * 3.14 * 반지름)
	public void circleArea(int radius) {
		double area = radius*radius*3.14;
		System.out.println("원의 넓이 : " + area);
	}
	
	public double circleRound(int radius) {
		double round = 2*3.14*radius;
		return round;	
	}

//arithmetic 함수를 만든 후 두 숫자를 입력받고 두 숫자의 덧셈,뺄셈,곱셈,나눗셈,나머지를
//출력한 후 main함수에서 호출하세요
	public void arithmetic(int su1, int su2) {
		System.out.println("덧셈결과 ->" + (su1+su2));
		System.out.println("뺄셈결과 ->" + (su1-su2));
		System.out.println("곱셈결과 ->" + (su1*su2));
		System.out.println("나눗셈몫 ->" + (su1/su2));
		System.out.println("나눗셈 나머지 ->" + (su1%su2));
	}

//main 함수에서 섭씨로 변화하고 싶으면 1, 화씨로 변화하고 싶으면 2를 입력받고 
//fahrenheitToCelsius함수를 통해서 화씨를 섭씨로 celsiusToFahrenheit 함수를 통해서 섭씨를 화씨로 바꿔
//출력하는 프로그램을 만드시오
//(화씨 = 1.8 * 섭씨 + 32, 섭씨 = (화씨 - 32) / 1.8)

public void celsiusToFahrenheit() {
		Scanner scan = new Scanner(System.in);
		
		double cel;
		double faher;
		
		System.out.printf("섭씨를 입력하세요 : ");
		
		cel = scan.nextInt();
		
		faher = 1.8 * cel + 32;
		
		System.out.println("화씨로 변화된 온도는 " + faher +"입니다." );
	}
	
	public void fahrenheitToCelsius() {
		Scanner scan = new Scanner(System.in);
		
		double cel;
		double faher;
		
		System.out.printf("화씨를 입력하세요 : ");
		faher = scan.nextInt();
		
		cel = (faher - 32) / 1.8;
		
		System.out.println("섭씨로 변화된 온도는 " + cel + "입니다.");
		
	}
}
```
## MethodTestMain클래스작성하기
```java
package test3;

import java.util.Scanner;

public class MethodTestMain {

	public static void main(String[] args) {
		Scanner sc = new Scanner(System.in);
		System.out.print("반지름을 입력하세요 : ");
		int radius = sc.nextInt();
		MethodTest mt = new MethodTest();
		
		mt.circleArea(radius);
		double round = mt.circleRound(radius);
		
		System.out.printf("원의 둘레 : %.2f\n",round);
	----------------------------------------------------------------
	
		System.out.print("첫번째 숫자를 입력하세요 : ");
		int su1 = sc.nextInt();
		System.out.print("두번째 숫자를 입력하세요 : ");
		int su2 = sc.nextInt();
		
		mt.arithmetic(su1, su2);
	}

	----------------------------------------------------------------
	
		System.out.print("1을 누르면 섭씨, 2를 누르면 화씨로 변경합니다.");
		int select = sc.nextInt();
		
		switch(select) {
		case 1:
			fahrenheitToCelsius();
			break;
		case 2:
			celsiusToFahrenheit();
			break;
		}
}

```

# setter&getter
- 객체 지향 프로그래밍에서 객체의 데이터는 객체 외부에서 직접적으로 접근하는것을 막는다.
- 객체 데이터를 외부에서 읽고 변경 시 객체의 무결성이 깨질 수 있기 때문이다.
- 예를들어 자동차의 속도는 음수가 될 수 없는데, 외부에서 음수로 설정하면 무결성이 깨진다.
- 따라서 객체 지향 프로그래밍에서는 메서드를 통해 데이터를 변경하는방법을 선호한다.
- 데이터는 외부에서 접근하지 않도록 막고, 메서드는 공개를 해서 외부에서 메서드를 통해 데이터에 접근하도록 유도한다.

## setter
- 외부에서 메서드를 통해 데이터에 접근하고 검증할 수 있도록 유도하는 것
```java
public void setSpeed(int speed) {
	if(speed < 0) {
		this.speed = 0;
		return;
	} else {
		this.speed = speed;
	}
	
}
```
## getter
- private 필드를 객체 외부에서 값을 불러오기 위해 구현하는 메서드를 getter라고한다.
- private 필드는 객체 외부에서는 접근이 불가능하지만, 필드가 선언된 클래스에서는 어디서든 접근이 가능하다.
- 따라서 메서드를 통해서 값을 전달해 줄 수 있다.
```java
public int getSpeed() {
	return speed;
}
```
## setter&getter 실습
```java
package test3;

public class Car {
	//필드(인스턴스 변수, 객체 변수, 멤버 변수)
	private int speed;
	private boolean stop;
	
	public int getSpeed() {
		return speed;
	}
	
	public void setSpeed(int speed) {
		if(speed < 0) {
			this.speed = 0;
			return;
		} else {
			this.speed = speed;
		}
		
	}
	
	public boolean isStop() {
		return stop;
	}
	
	public void setStop(boolean stop) {
		this.stop = stop;
		this.speed = 0;
	}
}
```
```java
package test3;

public class CarTest {
	public static void main(String[] args) {
		Car myCar = new Car();
		
		//잘못된 속도 변경
		myCar.setSpeed(-50);
		
		System.out.println("현재 속도 : " + myCar.getSpeed());
		
		//올바른 속도 변경
		myCar.setSpeed(60);
		
		//멈춤
		if(!myCar.isStop()) {
			myCar.setStop(true);
		}
		
		System.out.println("현재 속도 : " + myCar.getSpeed());
	}
}

```


# 사용자 정의 클래스와 메서드 실습문제
```java
//클래스로 계산기 만들어보기 문제.
/*
* 첫번째 숫자 입력 : 5
* 두번째 숫자 입력 : 10
* 연산기호 입력 : +
* 결과 : 15
* 
* Scanner를 사용해 
* 숫자 두 개와 연산기호를 받은 뒤 계산해주는 클래스를 만들고 실행하기
* 
* 참고: String의 비교는 ==아닌 String변수.equals("비교값")으로 한다
*  if(str.equals("+"))
*  else if(str.equals("-"))
*  else if(str.equals("*"))
*  else if(str.equals("/"))
*/


//풀이
public class CalTest {
	
	public int getResult(int n1, int n2, String str){
		
		if(str.equals("+"))
			return n1 + n2;
		else if(str.equals("-"))
			return n1 - n2;
		else if(str.equals("*"))
			return n1 * n2;
		else if(str.equals("/"))
			return n1 / n2;
		else{
			System.out.println("연산기호가 올바르지 않습니다.");
			return -1;
		}
	}
}

//CalMain클래스 구현
public class CalMain {
	public static void main(String[] args) {
		int n1, n2;
		String str;
		CalTest cal = new CalTest();
		
		Scanner sc = new Scanner(System.in);
		System.out.print("첫번째 숫자 입력 : ");
		n1 = sc.nextInt();
		
		System.out.print("두번째 숫자 입력 : ");
		n2 = sc.nextInt();
		
		System.out.print("연산기호 입력 : ");
		Scanner sc2 = new Scanner(System.in);
		str = sc2.next();//next와 nextLine차이점 설명

		System.out.print(“결과 : ”);
		System.out.println(cal.getResult(n1, n2, str));
	}
}
-----------------------------------------------------------------------
구구단 출력하기

문제설명 :
TimesTable클래스를 만들고

showTable()메서드를 정의한다.
showTable()메서드에는 구구단을 출력하는 코드를 작성.

TimesTableMain클래스를 만들어 TimesTable객체를 생성하고 
이를 이용하여 아래와같은 결과를 출력하자.

Scanner를 통해 값을 받는 작업은 반드시 TimesTableMain클래스에서 하도록 한다.

출력할 단을 입력 : 5
5단
5 * 1 = 5
5 * 2 = 10
5 * 3 = 15
5 * 4 = 20
5 * 5 = 25
5 * 6 = 30
5 * 7 = 35
5 * 8 = 40
5 * 9 = 45

풀이 :
TimesTable클래스 생성
public class TimesTable {		
	
	public void showTable(int num){
		
		System.out.println(num + "단");
		
		for(int i = 1; i <= 9; i++){		
			System.out.println(
				num + " * " + i + " = " + (num * i));
		}
	}
}
TimesTableMain클래스 생성
public class TimesTableMain {
	public static void main(String[] args) {
		
		int num;
		
		TimesTable tt = new TimesTable();
		
		System.out.print("출력할 단을 입력 : ");
		Scanner scan = new Scanner(System.in);
		
		num = scan.nextInt();
		
		tt.showTable(num);
	}
}
------------------------------------------------------------------
자바문제2(업다운)

문제설명 : 
Start클래스를 생성하여 1 ~ 50사이의 난수를 발생시킨다.
메인클래스를 만들고 사용자가 키보드를 통해 정수를 입력받는다.
Start클래스에서 사용자가 입력한 숫자를 판단하여 
발생한 난수보다 크다면 DOWN!! 작다면 UP!!을 출력.
사용자가 입력한 숫자와 발생한 난수가 같을경우에 프로그램을 종료시키며
몇회만에 정답을 맞췄는지 판단해보자.
단, 정답을 맞춘 경우 프로그램의 종료는 Start클래스가 아닌 
메인클래스에서 이루어 지도록 한다.

실행한 결과

숫자입력 : 30
Down!!
숫자입력 : 15
Up!!
숫자입력 : 25
3회 만에 정답!!!!


public class Start {

	Random rnd = new Random();
	
	int rnum = rnd.nextInt(50)+1;
	int count = 1;
	public String check(int number) {
		if(number == rnum) {
			return "정답!";
		} else if(number >rnum) {
			return "DOWN!";
		} else {
			return "UP!";
		}
	}
}

main
public class StartMain {
	public static void main(String[] args) {
		Scanner sc = new Scanner(System.in);
		
		
		Start s = new Start();
		
		while(true) {
			System.out.print("숫자입력 : ");
			int number = sc.nextInt();
			if(s.check(number).equals("정답!")) {
				System.out.println(s.count+"회 만에 정답");
				break;
			} else {
				System.out.println(s.check(number));
				s.count++;
			}
			
		}
	}
}

---------------------------------------------------------------
클래스를 이용한 입출금 로직 구현

문제설명 :
UserInfo클래스를 만든 뒤, 금액을 저장할 money라는 변수를 만든다.

deposit(int money)메서드를 만들어 유저가 돈을 입금했을 경우를 처리.

withdraw(int money)메서드를 만들어 유저가 돈을 출금했을 경우를 처리.
단 이 메서드에는 출금하고자 하는 돈 보다 잔액이 적을경우 잔액이 부족하다는 메시지가 출력되도록 한다.

showMoney()메서드를 만들어 현재 잔액을 반환하도록 한다.

UserInfo클래스는 여기까지. 
Main클래스를 새로 만들어 UserInfo형 객체를 생성한 뒤 아래의 결과가 나오도록 해보자.

1.입    금 : 
2.출    금 : 
3.잔액확인 : 
4.종    료 : 
1
---입   금---
입금할 금액을 입력 : 1000
입금성공

----------------------

1.입    금 : 
2.출    금 : 
3.잔액확인 : 
4.종    료 : 
3
---잔액확인---
1000원

----------------------

1.입    금 : 
2.출    금 : 
3.잔액확인 : 
4.종    료 : 
2
---출   금---
출금할 금액을 입력 : 5000
잔액부족


풀이 :
UserInfo클래스 생성
public class UserInfo {

	private int money; //잔액

	public void deposit(int money){
		System.out.println("입금성공");
		this.money += money;
	}

	public void withdraw(int money){

		if(this.money - money < 0){
			System.out.println("잔액부족");

		}else{
			System.out.println("출금성공");
			this.money -= money;
		}
	}
	
	public int showMoney(){
		return money;
	}
}


Main클래스 생성
public class Main {
	public static void main(String[] args) {

		int select;
		int money;

		UserInfo ui = new UserInfo();

		outer : while(true){
			System.out.println("1.입    금 : ");
			System.out.println("2.출    금 : ");
			System.out.println("3.잔액확인 : ");
			System.out.println("4.종    료 : ");

			Scanner scan = new Scanner(System.in);
			select = scan.nextInt();

			switch (select) {
			case 1:
				System.out.println("---입   금---");
				System.out.print("입금할 금액을 입력 : ");
				money = scan.nextInt();	
				ui.deposit(money);	
				break;

			case 2:
				System.out.println("---출   금---");
				System.out.print("출금할 금액을 입력 : ");
				money = scan.nextInt();	
				ui.withdraw(money);
				break;
				
			case 3:
				System.out.println("---잔액확인---");
				System.out.println(ui.showMoney() + "원");
				break;
				
				default :
					System.out.println("종료");
					break outer;//while문 탈출
			}
			
			System.out.println("----------------------");
		}//outer : while문의 끝
	}
}

-----------------------------------------------------------------

자바 강의 1주차(3) 문제(배열을 이용한 그래프)

Graph라는 이름의 메인 클래스를 만들어 0 ~ 9사이의 난수를 100개 저장하는 배열을 만들고, 해당 배열이 가지고 있는 각 방의 난수를 판별하여 그래프화 해 보자.

단, 발생한 난수의 그래프화 작업은 PrintGraph클래스가 하도록 한다.

결과:
0507...... //난수 100개
0의 갯수 : ############ 12
1의 갯수 : ######### 9
2의 갯수 : ########### 11
3의 갯수 : ######## 8
4의 갯수 : ############## 14
5의 갯수 : ####### 7
6의 갯수 : ######### 9
7의 갯수 : ############# 13
8의 갯수 : ####### 7
9의 갯수 : ########## 10

풀이 :
PrintGraph클래스 생성
public class PrintGraph {
	
	public String print(char ch, int num){
		char[] val = new char[num];
		String str = "";
	for(int i = 0; i < val.length; i++){
	
str += val[i] = ch;
}
		return str;
	}
}

Graph클래스 생성
public class Graph {
	public static void main(String[] args) {
	
int[] num = new int[100];//난수를 담을 배열
	
int[] count = new int[10];//발생한 난수가 각각 몇 개인지 저장할 배열
	for(int i = 0; i < num.length; i++){
	
//0 ~ 9사이의 난수
System.out.print(num[i] = new Random().nextInt(10));
}
	System.out.println();
	for(int i = 0; i < num.length; i++){
	count[num[i]]++;
	PrintGraph pg = new PrintGraph();
		for(int i = 0; i < count.length; i++){
			System.out.println(i + "의 갯수 : " + pg.print('#', count[i]) + " " + count[i]);
        }	
    }
}
```
