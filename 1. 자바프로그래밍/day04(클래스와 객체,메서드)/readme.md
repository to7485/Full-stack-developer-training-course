# 클래스

## 객체지향 프로그래밍(OOP : Object-Oriented Programming)
- 객체 지향 프로그래밍이란, 말 그대로 객체를 지향하는 프로그래밍 방법을 말한다.
- 객체란 우리 실생활에 존재하는 모든것으로 생각할 수 있다.
- 객체는 일반적으로 상태를 표현할 수 있고, 우리가 행동으로 실행할 수 있는 모든것들을 의미한다.
- 이런 객체를 중심으로 프로그램 구조를 설계하고 프로그래밍 하는 것을 객체 지향 프로그래밍이라고 한다.

## 클래스란?
- 객체를 생성하기 위한 설명서이다.
- 어떤 물건을 만들기 위한 메뉴얼이라고 생각하면 된다.
- 클래스를 기반으로 객체를 생성해야 한다.
- 하나의 설명서로 여러개의 물건을 만들 수 있듯이, 자바에서는 하나의 클래스로 여러 개의 객체를 생성할 수 있다.

## 클래스의 선언
- 첫날부터 클래스를 만들어서 사용해왔다.
- 자바 프로그래밍의 기반이 클래스이기 때문이다.
- 우리가 사용해온 클래스의 기본 구조는 다음과 같다.
```java
접근제한자 class 클래스명{

}

접근제한자 : 클래스의 접근 범위를 제한한다.
class : class를 선언함을 뜻한다.
클래스명 : 변수처럼 이름을 가지고, 객체를 생성할 때 사용한다.
```
- 그동한 사용해왔던 클래스는 "실행용"클래스로, 프로그램의 실행을 전적으로 맡고 있다.

## 클래스의 종류
### 실행용 클래스 
- 프로그램 전체에서 단 하나의 클래스로, 프로그램의 실행을 맡고 있다.
- main메서드를 갖고 있으며, 다른 클래스에서 사용하지 않는다.
### 객체 생성용 클래스
- 다른 클래스에서 사용할 목적으로 선언되는 클래스 입니다.

```
하나의 클래스가 위 두 가지 용도의 역할을 모두 수행할 수 도 있다.
하지만 유지 보수와 객체 지향 프로그래밍의 특징인 모듈화를 고려해 별도로 분리하여 작성하는 것이 좋다.
일반적으로 하나의 프로그램에서 실행용 클래스 1개를 제외한 나머지 클래스는 모두 참조용 클래스이다.
```

### 클래스 이름을 작성하는 규칙
- 영어 대소문자를 사용할 수 있으며 보통 첫 글자는 대문자를 사용한다.
- 숫자를 사용할 수 있으나 첫 글자로는 사용할 수 없습니다.
- 특수문자는 $,_만 가능합니다.
- 자바 예약어(키워드)는 사용할 수 없습니다.

### Cat 클래스 만들기
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

### CatMain클래스 만들기
```java
public class CatMain {
	public static void main(String[] args) {
		
		Cat c = new Cat();
	}
}
```
- 클래스는 일반적으로 하나의 소스 파일에 하나의 클래스를 선언합니다.
- 하나의 파일에서 여러개의 클래스를 선언한다면 파일이름과 같은 클래스에만 public을 사용해야 한다.

### Main01 클래스 작성
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
- 클래스를 구성하는 요소는 필드,메서드, 생성자 3가지가 있다.

## 필드(field)
- 객체가 가져야할 데이터의 상태를 저장하는 변수를 말한다.
- 필드, 전역변수, 멤버 변수 라고 부르는데 다 같은말이다.
- 필드의 값을 초기화 하지 않으면 객체 생성시 자동으로 기본값으로 초기화 된다.

### Car클래스 만들기

```java
package test3;

public class Car {
	//int wheel; //필드 선언
	int wheel = 4; //초기화를 할 수도 있다.
}
```
- 만약 클래스를 선언할 때, 필드의 값을 초기화 하지 않으면 객체 생성 시 자동으로 기본값으로 초기화된다.
<table>
	<tr>
		<th>구분</th>
		<th>분류</th>
		<th>자료형</th>
		<th>초기값</th>
	</tr>
	<tr>
		<td rowspan="4">기본 자료형</td>
		<td>정수형</td>
		<td>byte<br>short<br>int<br>long<br></td>
		<td>0<br>0<br>0<br>0L</td>
	</tr>
	<tr>
		<td>문자형(정수)</td>
		<td>char</td>
		<td>\u0000(공백)</td>
	</tr>
	<tr>
		<td>실수형</td>
		<td>float<br>double</td>
		<td>0.0F<br>0.0</td>
	</tr>
	<tr>
		<td>논리형</td>
		<td>boolean</td>
		<td>false</td>
	</tr>
	<tr>
		<td rowspan="2" colspan="2" align="center">참조 자료형</td>
		<td>배열</td>
		<td>null</td>
	</tr>
	<tr>
		<td>클래스</td>
		<td>null</td>
</table>

- 필드는 클래스에 포함된 요소이자, 객체를 생성한 후 객체가 가지는 데이터이기도 하다.
- 따라서 객체를 생성한 후 그 객체의 필드를 사용할 수 있다.
```java
객체명.필드명

객체명 : 클래스를 이용해 만든 객체의 이름
필드명 : 만든 객체가 가지고 있는 필드의 이름
```

### CarMain클래스 만들기
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
- 객체의 기능을 담당하는 중괄호({})블록을 말한다.
- 특정 기능을 수행하는 코드를 따로 빼서 중괄호 안에 작성하며, 1개의 메서드는 일반적으로 1개의 기능을 수행한다.

### 메서드의 선언
- 메서드는 다음과 같이 선언한다.
```java
반환형 메서드명(파라미터){ //머리
	작업할 내용
	return 반환값;
}
```

### 메서드 구현하기
```java
public class Car{
	int wheel;

	void ride(){
		System.out.println("달립니다");
	}
}
```

### 메서드의 사용
- 구현한 메서드를 사용하는 방법은 필드의 사용법과 동일하다.
- 메서드를 선언한 클래스 안에서 메서드를 사용할 때는 단순히 메서드명만 호출하면 되지만, 다른 클래스에서 메서드를 사용하려면 객체를 먼저 생성한 후 참조 변수를 이용해 그 객체의 메서드를 사용해야 한다.
- 개체가 존재해야 메서드도 존재하기 때문이다.

### 함수의 작동 원리
- 메서드를 호출하면 블록 안에 있는 코드들이 위에서 순차적으로 모두 실행되고 경우에 따라 실행한 결과를 호출한 곳으로 돌려준다. 
- 이를 '반환한다'라고 표현하고, 반환하는 결과값을 '반환값(리턴값)'이라고 한다.
- 리턴값이 있을 경우에는 리턴할 데이터의 타입이 무엇인지 메서드명()앞에 반환 타입을 기재해줘야 한다.
- 반환형은 메서드가 처음부터 끝까지 수행을 마친 후에 반환해야 할 값이 있을 경우에 기입.
- int, String, boolean등 기본자료형을 포함하여 사용자가 만든 객체로도 반환이 가능.
- 아무것도 반환하지 않을때는 void

```java
클래스명 객체명 = new 클래스명(); //객체의 생성
객체명.메서드명();//생성한 객체의 메서드 호출(사용)
```

```java
public class Main{
	public static void main(String[] args){
		Car c = new Car();
		//메서드의 호출
		c.ride();
		c.ride();
		c.ride();
	}
}
```
- 메서드를 한 번 선언해 두면 필요할 때마다 여러 번 호출하여 사용할 수 있다.
- 즉, 메서드를 사용하면 반복적인 프로그래밍을 보다 쉽고 간단하게 해결할 수 있다.

### 메서드 이름 짓기
- 메서드의 이름은 그 기능을 명확하게 설명해줄 수 있게 작성하는 것이 좋다.
- 메서드명을 작성하는 규칙 역시 변수를 작성하는 규칙과 동일하다.

## 생성자(constructor)
- 메서드 중 객체를 생성할 때 반드시 호출해야 하는 특수한 기능을 하는 메서드 이다.
- 이 메서드는 객체를 생성하면서 객체 변수를 초기화하는 역할을 하기 때문에 생성자라고 부른다.

```
클래스명 객체명 = new 클래스명();
```
- 생성자라는 메서드는 클래스명과 이름이 같아야 한다.
- 우리는 생성자라는 메서드를 선언한적이 없음에도 호출하여 객체를 생성해 왔다.
- 그 이유는 우리가 직접 선언하지 않아도 기본 생성자가 자동으로 생성되고 우리 눈에만 보이지 않기 때문이다.

### Car클래스에 생성자 선언하기
```java
public class Car{
	int wheel;

	//기본생성자
	Car(){

	}

	void ride(){
		System.out.println("달립니다");
	}
}
```
- 생성자를 통해 객체 변수를 초기화 한다는 말은, 단순히 어떤 값을 초기화 한다는 뜻이 아니다.
- 필드와 메서드를 호출하는 등 객체를 사용학 위해서는 객체 변수가 메모리에 올라가야 하는데, 이렇게 메모리에 객체를 올려주는 역할을 하기 때문이다.

## 정적 멤버와 static
- 클래스 안에서 선언된 필드와 메서드를 클래스 멤버라고도 부른다.
- 클래스에 포함된 요소라는 의미로 '멤버'라는 용어를 사용한다.
#### 모든 객체가 동일한 값을 가져야할 때 각 객체의 멤버로 만들어야 할까???

### Family클래스 생성하기
```java
package member;

public class Family { //클래스 선언
	String name; //구성원 이름
	int age; //구성원 나이
	String address = "서울";//구성원 주소
}
```

### FamilyMain클래스 생성하기
```java
package member;

public class FamilyMain {
	public static void main(String[] args) {
		Family father = new Family();
		Family son = new Family();
		
		father.address = "인천";
		System.out.println(son.address);
	}
}
결과 : 서울
```
- 같은 집으로 함께 이사를 한 가족이라도 하나의 객체의 주소만 변경했더니 아들 객체의 주소는 바뀌지 않은 것을 알 수 있다.
- 모든 객체의 필드 값이 같아야 한다면 매우 불편한 상황이 될 수 있다.
- 일반적으로 각 객체가 가지게 되는 필드와 메서드를 인스턴스 멤버 라고 한다.
- 모든 객체들이 공유하며 사용하는 하나의 필드와 메서드를 정적 멤버라고 부른다.

### 정적 멤버
- 필드와 메서드를 선언할 때 static이라는 키워드가 붙은 멤버를 말한다.


### static키워드
- 사전적으로 '고정된'이라는 뜻을 가지고 있다.
- 프로그래밍 언어에서 static은 '클래스에 고정되었다'라는 의미로 사용되고 있다.
- 쉽게 말해서 객체가 아닌 클래스에 의존적인 요소라고 생각하면 된다.
- 멤버 앞에 static 키워드를 붙히게 되면, 다른 멤버들과 달리 객체를 생성하지 않고 바로 사용할 수 있다.
- **그 이유는 객체를 생성할 때 메모리에 올라가는 것이 아니라, 프로그램이 실행될 때 메모리에 올라가고 프로그램이 종료될 때 메모리에서 사라지기 때문이다.**

### 호출방법
```
클래스명.필드;
클래스명.메서드명();
```

### Student클래스 생성하기
```java
package member;

public class Student {
	static String schoolName = "코리아 고등학교"; //정적 멤버 선언
	
	static void goToSchool() {
		System.out.println("학교에 갑니다");
	}
}
```

### StudentMain클래스 생성하기
```java
package test2;

public class StudentMain {
	public static void main(String[] args) {
		System.out.println(Student.schoolName);
		Student.goToSchool();
	}
}
결과
코리아 고등학교
학교에 갑니다.
```
- 정적 멤버의 경우, 객체마다 가지는 데이터 기능이 아니기 때문에 모든 객체가 같은 값을 가져야 할 경우에 사용하는 것이 효율적이다.
- 따라서 각 클래스의 멤버를 선언할 때는 충분히 고려한 후 정적 멤버로 선언할지에 대한 결정을 내리는 것이 좋다.

### Student클래스에 코드 추가하기
```java
package test2;

public class Student {//클래스 선언
	static String schoolName = "코리아 고등학교";//정적 필드 선
	String studentName; //인스턴스 필드 선
	
	static void goToSchool() { //정적 메서드 선언
		System.out.println("학교에 갑니다.");
	}
	
	void hello() { //인스턴스 메서드 선언
		System.out.println("안녕하세요, 제 이름은 " + studentName + "입니다.");
	}
}
```

### StudentMain클래스에 코드 추가하기
```java
package test2;

public class StudentMain {
	public static void main(String[] args) {
		Student stu1 = new Student();
		stu1.studentName = "김고이";
		stu1.hello();
		System.out.println("학교는 " + Student.schoolName + "입니다.");
		Student.goToSchool();
		System.out.println("----------------------");
		Student stu2 = new Student();
		stu2.studentName = "김고";
		stu2.hello();
		System.out.println("학교는 " + Student.schoolName + "입니다.");
		Student.goToSchool();
	}
}
결과
안녕하세요, 제 이름은 김고이입니다.
학교는 코리아 고등학교입니다.
학교에 갑니다.
----------------------
안녕하세요, 제 이름은 김고입니다.
학교는 코리아 고등학교입니다.
학교에 갑니다.
```
- 정적 멤버를 호출할 때, 객체 변수를 통해 호출할수도 있습니다.
```
Student stu1 = new Student();
System.out.println(stu1.schoolName);
```

# 메서드
- 클래스 안에서 특정 기능을 수행하기 위해 코드들을 따로 하나의 블록으로 묶어놓은 집합을 말한다.
- 필요에 따라 이 집합을 호출해 사용할 수 있다.

## 메서드 사용의 이점
- 메서드를 구현함으로써, 같은 내용의 코드를 반복적으로 사용하는 것을 피할 수 있다. 
- 반복되는 문장들을 묶어서 메서드로 작성해놓으면 필요할 때마다 재사용이 가능하기 때문이다.
- 코드의 집합을 따로 분리하는것을 "모듈화"라고 한다.
- 모듈화를 하면 코드를 읽을 때 가독성이 좋아지며, 프로그램을 수정할 때 더욱 빠르고 쉽게 할 수 있다.

## 메서드 선언
- 메서드는 크게 선언부(signature)와 실제 영역(body)로 구성되어 있다.
```java
접근 제한자 반환타입 메서드명(){
	//기능을 수행하는 코드
}
```

### 접근제한자
- 접근제한자는 클래스/메서드/필드에 대한 접근을 어디범위까지 제한하느냐에 대한 지시어이다.
1. public : 모든 접근을 허용. 같은 프로젝트 내의 모든 객체들이 사용할 수 있도록 허용.
2. private : 현재 클래스 내에서만 사용을 허가.
3. protected : 상속관계의 객체들에만 사용을 허가.
4. default : 같은 패키지(폴더)내의 객체에만 사용을 허가(아무것도 쓰지 않으면 default)

### 반환타입(return Type)
- 메서드를 호출하면 메서드는 블록 안에 있는 코드들을 실행한 후 결과값을 반환한다.
- 이때 결과값을 어떤타입으로 반환할것인지 미리 정해주는것이다.
- 반환값이 없는 경우 타입으로 'void'를 쓰면 된다.

### 메서드명(함수명)
- 메서드명은 말그대로 메서드의 이름(첫글자는 소문자로 시작한다.)
- 메서드를 호출할 때 사용한다.
### Method01클래스 생성
```java
package method;

public class Method01 {
	public static void main(String[] args) {
		printHello(); //main메서드 안에서 printHello()메서드 호
	}
	
	static void printHello() {
		System.out.println("안녕하세요");
		System.out.println("만나서 반갑습니다.");
	}
}
```
- main메서드도 static으로 프로그램 시작과 함께 메모리에 올라가 있다.
- 따라서 main안에서 메서드를 호출하기 위해서는 호출하는 메서드가 메모리에 올라가 있어야 한다.

### 메서드를 메모리에 올리는 두 가지 방법
- 객체 생성용 클래스에 있는 경우
  - 인스턴스 메서드 : 객체를 생성함과 동시에 객체의 멤버들이 메모리에 올라간다. 따라서 객체를 생성한 후 사용할 수 있다.
  - 정적 메서드 : 프로그램 시작과 동시에 메모리에 자동으로 올라가기 때문에 바로 사용할 수 있다.
- 실행용 클래스에 있는 경우
  - 객체를 생성할 방법이 없기 때문에, 메서드가 무조건 static으로 선언되어야 한다.

## 메서드의 호출
- 메서드는 다른 메서드에서 호출되어 사용된다.
```
클래스명 변수명 = new 클래스명(); -> 객체를 생성하여 변수에 담기
변수명.메서드명();
```

- 메서드는 클래스 안에서 선언되므로 메서드를 사용하기 위해서는 해당 클래스의 객체부터 생성해야 한다.

### Jogger클래스 생성하기
```java
package method;

public class Jogger {

	void run() {
		System.out.println("run run run!!");
	}
}
```

### JoggerMain클래스 생성하기
```java
package method;

public class JoggerMain {
	public static void main(String[] args) {
		Jogger jogger = new Jogger(); //객체 생성
		jogger.run(); //jogger인스턴스의 run()메서드 호출
	}
}
결과
run run run!!
```
### 2개 이상의 메서드 선언하기
- 메서드는 같은 클래스에 있는 필드를 사용할 수 있다.
- 하나의 클래스에 2개 이상의 메서드를 사용하는 것 역시 가능하다.
### Jogger클래스에 코드 추가힉
```java
package method;

public class Jogger {

	String name; //조거의 이름
	
	void run() {
		System.out.println("run run run!!");
	}
	
	void sayName() {
		System.out.println("제 이름은 : " + name + "입니다.");
	}
}
```
### JoggerMain에 코드 추가하기
```java
package method;

public class JoggerMain {
	public static void main(String[] args) {
		Jogger jogger = new Jogger(); //객체 생성
		jogger.name = "김나비";
		jogger.sayName();
		jogger.run(); //jogger인스턴스의 run()메서드 호출
	}
}
결과
제 이름은 : 김나비입니다.
run run run!!
```


### 매개변수
- 특정 기능을 수행하기 위한 메서드는 기능을 수행할 때 사용할 값(인수)를 전달받을 수 있다.
- 매개변수는 사용할 값을 받는 변수이다.

```java
접근제한자 반환타입 메서드명(자료형 변수명){
	//기능을 수행할 코드
}
```
- 매개변수는 '매개변수의 자료형'과'매개 변수명'으로 선언할 수 있다.
```java
				  int number;
전달받을 값의 자료형 ┘ 	  └ 메서드 안에서 사용할 이름

```
### Book클래스 생성하기
```java
package test3;

public class Book {
	public void count(int bookNum) {
		System.out.println("책은 " + bookNum+"권 입니다.");
	}
}
```
### BookMain클래스 생성하기
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
### Calc클래스 생성하기
```java
package method;

public class Calc {

	void sum(int num1, int num2) {
		System.out.println("두 수의 합은 : " + (num1 + num2) + "입니다.");
	}
}
```

### CalcMain클래스 생성하기
```java
package method;

public class CalcMain {
	public static void main(String[] args) {
		Calc calc = new Calc();
		calc.sum(5, 3);
		calc.sum(10, 7);
	}
}
```
- 다른 자료형 2개를 매개변수로 받는 메서드

### Person클래스 생성하기
```java
package method;

public class Person {
	void introduce(String name, int age) {
		System.out.println("제 이름은 " + name+"이고, 나이는" + age+"세입니다.");
	}
	
	void hello() {
		System.out.println("안녕하세요");
	}
}
```

### PersonMain클래스 생성하기
```java
package method;

public class PersonMain {
	public static void main(String[] args) {
		Person hong = new Person();
		hong.introduce("홍길동", 20);
		hong.hello();
	}
}
결과
제 이름은 홍길동이고, 나이는20세입니다.
안녕하세요
```
- 배열을 매개변수로 받는 메서드

### Calc클래스에 코드 추가하기
```java
package method;

public class Calc {

	void sum(int num1, int num2) {
		System.out.println("두 수의 합은 : " + (num1 + num2) + "입니다.");
	}
	
	void sum(int[] nums) {
		int result = 0;
		for(int i = 0; i < nums.length; i++) {
			result += nums[i];
		}
		System.out.println("숫자들의 합은 : " + result + "입니다.");
	}
}
```

### CalcMain클래스에 코드 추가하기
```java
package method;

public class CalcMain {
	public static void main(String[] args) {
		Calc calc = new Calc();
		calc.sum(5, 3);
		calc.sum(10, 7);
		
		int []nums = {100,200};
		calc.sum(nums);
	}
}
```

### return
- 함수에서 모든 작업을 마치고 경우에 따라 실행한 결과를 호출한곳으로 다시 돌려주기도 한다.
- 이것을 '반환한다'라고 표현한다
- 반환하는 결과값을 '반환값'이라고 부르기도 한다.
- 리턴값이 있을 경우에는 리턴할 데이터의 타입이 무엇인지 반환형에 기재해줘야 한다.
- 리턴값이 없는 경우 메서드를 종료하기 위해 return을 사용할 수 있다.
```
접근제한자 반환타입 메서드명(){
	//기능을 수행할 코드들
	...
	return 결과값;
}
```
- 매개변수와 마찬가지로 리턴값의 자료형은 제한이 없다.
- 자바에서 사용하는 모든 자료형을 반환타입으로 사용할 수 있다.

### Calc클래스 수정하기
```java
package method;

public class Calc {

	void sum(int num1, int num2) {
		System.out.println("두 수의 합은 : " + (num1 + num2) + "입니다.");
	}
	
	//반환값의 타입과 일치시켜준다.
	int sum(int[] nums) {
		int result = 0;
		for(int i = 0; i < nums.length; i++) {
			result += nums[i];
		}
		//System.out.println("숫자들의 합은 : " + result + "입니다.");

		return result; //모든 기능을 수행한 값을 반환한다.
	}
}
```

### CalcMain클래스 수정하기
```java
package method;

public class CalcMain {
	public static void main(String[] args) {
		Calc calc = new Calc();
		calc.sum(5, 3);
		calc.sum(10, 7);
		
		int []nums = {100,200};
		//calc.sum(nums);
		System.out.println("숫자들의 합은 " + calc.sum(nums)+"입니다.");
	}
}
```
- 메서드를 호출한 위치가 메서드를 실행하고 반환된 결과값으로 치환되었다.
- 변수에 저장하지 않고 바로 치환하여 사용할 수도 있으며, 필요에 따라 저장하여 결과값을 활용할 수도 있다.

### 반환받은 값을 변수에 저장하는 메서드
### MidTerm클래스 생성하기
```java
package method;

public class MidTerm {
	public int score(int[] scores) {
		int result = 0;
		for(int i = 0; i < scores.length; i++) {
			result += scores[i];
		}
		return result;
	}
}
```

### MidTermMain클래스 생성하기
```java
package method;

public class MidTermMain {
	public static void main(String[] args) {
		int [] studentA = {97,53};
		int [] studentB = {97,66};
		
		MidTerm mid = new MidTerm(); //MidTerm 객체 생성
		int sumA = mid.score(studentA); //메서드를 호출한 결과값을 sumA에 저장
		int sumB = mid.score(studentB); //메서드를 호출한 결과값을 sumB에 저장
		
		if(sumA > sumB) {
			System.out.println("A학생의 중간고사 총점이 더 높습니다.");
		} else if(sumA < sumB) {
			System.out.println("B학생의 중간고사 총점이 더 높습니다.");
		} else {
			System.out.println("두 학생의 중간고사 총점이 같습니다.");
		}
	}
}
```
### 메서드를 빠져나가기 위한 return
#### Bus클래스
```java
package test3;

public class Buss {

	public void take(int m) {
		while(true) {
			if(m < 3000) {
				System.out.println("교통카드를 충전하러 갑니다.");
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

# setter&getter
- 지금까지 객체의 필드를 객체의 내부뿐만 아니라 객체 밖에서도 마음껏 사용할 수 있었고, 마음대로 값을 바꿀수도 있었다.
## 필드에 직접 접근했을 때의 문제점
### Person클래스 수정하기
```java
package method;

public class Person {
//	void introduce(String name, int age) {
//		System.out.println("제 이름은 " + name+"이고, 나이는" + age+"세입니다.");
//	}
//	
//	void hello() {
//		System.out.println("안녕하세요");
//	}
	
	int age;
}
```

### PersonMain클래스 수정하기
```java
package method;

public class PersonMain {
	public static void main(String[] args) {
		Person hong = new Person();
//		hong.introduce("홍길동", 20);
//		hong.hello();
		hong.age = -30;
		
		System.out.println("hong의 나이는 " + hong.age+"세입니다.");
	}
}
```
- 사람의 나이는 음수가 될 수 없음에도 age값을 음수로 바꿀 수 있었다.
- 이처럼 객체 밖에서 필드에 마음대로 접근할 수 있고 값을 변경할 수 있다면, 문제가 생길 가능성이 있다.
- 이런 문제를 예방하기 위해 객체 지향 프로그래밍에서는 메서드를 통해서 필드의 값을 불러오고, 필드의 값을 변경하는 방법을 이용한다.

### 메서드를 통해 필드에 접근할 때 장점
- 필드를 보호할 수 있다.
- 메서드에서 필드에 들어갈 값을 검증한 후 필드에 대입할 수 있다.
- 외부에서 사용할 필드의 값을 정제한 후 값을 제공할 수 있다.

## setter
- 외부에서 메서드를 통해 데이터에 접근하고 검증할 수 있도록 유도하는 메서드의 개념

### Person클래스에 코드 추가하기
```java
public void setAge(int num) {
	if(num <= 0) {// 만약, age에 넣으려는 값이 0보다 작거나 같다면
		System.out.println("잘못된 수를 입력하셨습니다. 1 이상의 값으로 설정하세요");
		return; //메서드 종료
	} else {
		age = num; //age필드에 num을 저장
	}
}
```
- 일반적으로 setter메서드를 사용할 때는, 필드의 값을 객체 외부에서 직접 넣지 못하도록 필드에 접근을 제한한다.
- 필드가 선언되어 있는 클래스에서만 접근이 가능하도록 private 접근제한자를 붙힌다.
```java
private int age;
```
- 필드를 private으로 선언함으로써 필드를 한층 더 보호할 수 있으나, 객체의 외부에서 그 필드에 대한 값을 불러오는 것 또한 불가능해졌다.

## getter
- private 필드를 객체 외부에서 값을 불러오기 위해 구현하는 메서드를 getter라고한다.
- private 필드는 객체 외부에서는 접근이 불가능하지만, 필드가 선언된 클래스에서는 어디서든 접근이 가능하다.
- 따라서 메서드를 통해서 값을 전달해 줄 수 있다.

### Person클래스에 코드 추가하기
```java
public int getAge() {
	return age;
}
```

### PersonMaim클래스 코드 수정하기
```java
package method;

public class PersonMain {
	public static void main(String[] args) {
		Person hong = new Person();
//		hong.introduce("홍길동", 20);
//		hong.hello();
		//hong.age = -30;
		hong.setAge(-30);
		hong.setAge(30);
		System.out.println("hong의 나이는 " + hong.getAge()+"세입니다.");
	}
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

# 생성자
- 클래스를 구성하는 구성요소중 하나인 생성자는, 객체를 생성할 때 호출되어 객체의 초기화를 담당하는 특별한 메서드이다.
- 객체를 생성하고 초기화하기 위해서는 반드시 생성자를 호출해야 한다.
- 따라서 객체를 생성해야 하는 참조용 클래스는 모두생성자를 가지고 있다.

## 생성자의 정의
- 생성자는 반환값이 없지만, 반환 타입을 아예 작성하지 않는다.(void로도 적지 않는다.)
- 생성자는 초기화를 위한 데이터를 인수로 전달받을 수 있다.
```java
접근제어자 클래스명 (매개변수1,매개변수2...){

}
```

## 생성자의 호출 위치
- 일반 메서드들과는 다르게, 생성자를 호출하는곳이 정해져있다.
- 생성자는 클래스를 기반으로 객체를 생성할 때, 객체의 초기화를 담당하는 역할을 하므로 객체를 생성할 때만 호출할 수 있다.

## 생성자 호출 방법
- 생성자를 호출할 때는 new 키워드를 함께 사용한다.
```java
클래스명 객체명 = new 클래스명();
					  ㄴ 이 메서드가 생성자이다.
```

## constructer패키지 생성하기
### Snack 클래스 만들기
```java
package constructor;

public class Snack {
	int price;
	
	void info() {
		System.out.println("과자의 가격은 " + price + "원입니다.");
	}
}

```
### SnackMain클래스 정의
```java
package constructor;

public class SnackMain {
	public static void main(String[] args) {
		Snack chip = new Snack(); //객체 생성 및 초기화
		chip.price = 2000; //객체 필드 설정
		chip.info(); //객체 메서드 호출
	}
}
```
- 객체의 필드에 데이터를 삽입하고, 메서드를 사용하기 위해 생성자를 통해 객체를 생성하고 사용할 준비를 한다.
- 하지만 우리는 클래스에 Snack()생성자를 선언한적이 없는데 어떻게 상요할 수 있는것일까??

## 기본생성자
- 자바의 모든 클래스에는 하나 이상의 생성자가 정의되어야 있어야 한다.
- 클래스를 생성하면서 개발자가 직접 생성자를 선언하지 않았지만, 자바 컴파일러가 기본생성자를 자동으로 제공해주고 있다.
- 다만, 컴파일러의 눈에만 보일 뿐 우리가 보는 코드에는 생략되어 있다.

```java
package constructor;

public class Snack {
	int price;
	
	public Snack() { //기본생성자
					//안에는 텅 비어있음
	}
	
	void info() {
		System.out.println("과자의 가격은 " + price + "원입니다.");
	}
}
```
- 기본 생성자는 파라미터가 별도로 없으며, 중괄호{}블록 안에 코드가 없는 비어있는 생성자를 말한다.
- 기본생성자는 개발자기 직접 선언하지 않았을 때만 컴파일러가 자동으로 추가한다.
- 만약 개발자가 직접 생성자를 선언한다면, 컴파일러는 선언된 생성자를 사용한다.

## 생성자 선언 이유
- 생성자는 객체를 생성함과 동시에 객체를 초기화 할 수 있다.
- 생성자를 통해 객체를 초기화한다는 것은 필드와 메서드를 호출하는 등 객체를 사용하기 위해 객체를 메모리에 올린다는 의미이다.
- 생성자를 통해 객체를 메모리에 올림과 동시에, 더 나아가 객체 멤버에 접근이 가능하므로 일반적인 메서드처럼 객체 멤버의 데이터를 초기화 할 수 있다.
- 메서드를 호출해서 파라미터에 값을 전달했던 것처럼, **생성자 역시 파라미터를 통해 값을 전달할 수 있다.**

### Snack클래스 코드 추가하기
```java
package constructor;

public class Snack {
	int price;
	
	public Snack(int p) { //기본생성자
		price = p;
	}
	
	void info() {
		System.out.println("과자의 가격은 " + price + "원입니다.");
	}
}
```

```java
package constructor;

public class SnackMain {
	public static void main(String[] args) {
		Snack chip = new Snack(5000); //객체 생성 및 초기화
		//chip.price = 2000; //객체 필드 설정
		chip.info(); //객체 메서드 호출
	}
}
```
- 생성자를 통해 필드를 초기화 했으므로 chip.price로 필드에 접근하여 값을 주지 않아도 필드에 값이 들어가있음을 확인할 수 있다.
- 물론 생성자를 통하지 않고 클래스에서 필드를 선언할 때 필드를 초기화할 수도 있다.

```java
public class Snack{
	int price = 2000;
	...
}
```
- 위와 같은 클래스로 객체를 만들 경우 모든 과자의 가격이 2000원으로 생성된다.
- 과자의 가격이 모두 2000원으로 동일하다면 효과적인 방법일 것이다.
- 하지만 과자마다 가격이 다르다면 생성자를 통해 가격을 전달하고 객체를 생성하는 것이 더 효율적일 수 있다.
```java
Snack potatoChip = new Snack(2000);
Snack potatoChip = new Snack(1800);
```

- 일반적인 메서드와 마찬가지로, 파라미터를 2개 이상 전달할 수 있다.

## Person 클래스
```java
public class Person {
	int age;
	String name;

	//예를들어서 나이와 이름, 전화번호를 알아야 친구가 된다고 가정을 해볼게요.
	//이중에 한가지라도 빼먹고 안쓰면 문제가 있는거에요 써먹기 불가능한 객체가 될수도 있다는거죠.

	//똑같은걸 계속 만드려고 한다면 기본생성자에 값을 넣어놓는것도 좋은 방법
	//pbulic Person() {
	//	age = 40;
	//	name = "노태문";
	//}

	//빈공간에서 cntl + space bar 기본생성자 생성
	//임의로 새로운 생성자를 정의한 순간부터 기본생성자는 쓸 수 없다.
	public Person(int age, String) {
		this.age = age;
		this.name = name;

	}

	public void introduce() {
		System.out.printf("안녕하세요. 저는 %d살 %s입니다.", age,name);
	}
}
```
## PMain 클래스
```java
public class PMain{
	public static void main(String[] args) {
		
		Person p1 = new Person(20,"홍길동");
		Person p2 = new Person(30,"김자바");

		p1.introduce();
		p2.introduce();
		
}
```

## 생성자 오버로딩
- 생성자에 전달할 매개변수가 부족하면 어떤일이 발생할까??
### Phone 클래스
```java
package test3;

public class Phone {
	String brand;
	int series;
	String color = "검정색";
	
	public Phone(String b, int s, String c) {
			brand = b;
			series = s;
			color = c;
	}
	
	public void phoneInfo() {
		System.out.println(color + " " + brand + " " + series);
	}
}
```
### PhoneMain클래스
```java
package test3;

public class PhoneMain {
	public static void main(String[] args) {
		Phone p1 = new Phone("갤럭시",1,"흰색");
		Phone p2 = new Phone("아이폰",1);
	}
}
```
- 생성자에 전달할 매개변수가 부족하면, 객체를 생성할 수 없다.
- 선언된 생성자의 형태에 맞게 매개변수를 전달해 줘야 하기 때문이다.
- 클래스 내부에 선언된 필드의 기본값을 그대로 사용하고 싶다면 파라미터가 부족하다고 생성하지 못할 이유가 없어야 한다.
- 이 경우 자바에서는 생성자를 여러 개 선언하는 것을 허용하고 있다.
- 외부에서 제공할 수 있는 데이터만큼만 매개변수로 전달하여 객체를 생성할 수 있다.
- 생성자를 다양한 형태로 선언하는 것을 '생성자 오버로딩'이라고 한다.

### 오버로딩 규칙
1. 매개변수의 개수가 다를 때
2. 매개변수의 개수가 같아도 자료형이 다를 때
3. 생성자나 메서드의 이름은 그대로 사용해야 한다.


### Phone클래스에 코드추가하기
```java
package test3;

public class Phone {
	String brand;
	int series;
	String color = "검정색";

	public Phone(String b, int s) {
		brand = b;
		series = s;
	}

	public Phone(String b, int s, String c) {
		brand = b;
		series = s;
		color = c;
	}

	public void phoneInfo() {
		System.out.println(color + " " + brand + " " + series);
	}
}
```

## 여러개의 생성자를 선언해보기
### Book 클래스
```java
package test3;

public class Book {
	String title = "제목없음";
	int series = 1;
	int page = 100;
	
	public Book() {
		// TODO Auto-generated constructor stub
	}
	
	public Book(String t) {
		title = t;
	}
	public Book(String t, int p) {
		title = t;
		page = p;
	}
	public Book(int s, String t) {
		series = s;
		title = t;
	}
}
```
### BookMain클래스
```java
package test3;

public class BookMain {
	public static void main(String[] args) {
		Book b1 = new Book();
		System.out.println("b1.title : " + b1.title);
		System.out.println("b1.series : " + b1.series);
		System.out.println("b1.page : " + b1.page);
		
		Book b2 = new Book("멘토시리즈 자바");
		System.out.println("b2.title : " + b2.title);
		System.out.println("b2.series : " + b2.series);
		System.out.println("b2.page : " + b2.page);
		
		Book b3 = new Book("신데렐라",170);
		System.out.println("b3.title : " + b3.title);
		System.out.println("b3.series : " + b3.series);
		System.out.println("b3.page : " + b3.page);
		
		Book b4 = new Book(5,"노인과 바다");
		System.out.println("b4.title : " + b4.title);
		System.out.println("b4.series : " + b4.series);
		System.out.println("b4.page : " + b4.page);
	}
}
```

# this와 this()
- 변수명을 지을 때, 최대한 구체적이고 명확하게 작명하는 것이 보다 효율적인 코드를 작성하는데 도움이 된다는 것을 알고있다.
- 함수나 생성자에서 매개변수는 클래스의 필드보다 우선순위가 높아서, 대입연산자를 기준으로 왼쪽/오른쪽 변수 모두 매개변수를 뜻하게 된다.
- 매개변수에 매개변수를 넣는 의미없는 코드가 된다.
- 이러한 상황을 해결하기 위해 this키워드를 사용한다.

## this
- 객체 자기 자신 스스로 참조
- this 참조 변수는 객체가 자기 자신을 참조하는데 사용하는 변수이다.
- this를 필드에 붙여서 사용하면, 중괄호{}안에서도 같은 이름의 매개변수와 필드를 구분해서 사용할 수 있다.
```java
this.필드 = 매개변수명;
```

### Student.java
```java
package test3;

public class Student {
	String name;
	int age;
	int studentID;
	
	public Student(String name, int age, int studentID) {
		this.name = name;
		this.age = age;
		this.studentID = studentID;
	}
}

```

## this()
- 현재 클래스에 선언되어있는 생성자를 가리킬 수 있는 키워드이다.

### this(매개변수1,매개변수2)
- this()메서드는 같은 클래스 안에 있는 생성자 중 매개변수의 개수, 자료형, 순서에 맞는 다른 생성자를 호출하는 메서드로 생성자 내부에서만 사용할 수 있다.

### Phone.java
```java
package test3;

public class Phone {
	String brand;
	int series;
	String color = "검정색";

	public Phone(String b, int s) {
		brand = b;
		series = s;
	}

	public Phone(String b, int s, String c) {
		//brand = b;
		//series = s;
		this(b,s); //this()는 첫줄에서만 사용할 수 있다.
		color = c;
	}

	public void phoneInfo() {
		System.out.println(color + " " + brand + " " + series);
	}
}
```
# 메서드 오버로드
- 오버로드은 메서드의 '중복정의' 라고 하며, 하나의 클래스 내에서 같은 이름을 가진 메서드(함수)가 여러개 정의되는 것을 말한다.
- 메서드들을 같은 이름으로 작업할 수 있다는 의미이다.

```java
public class Overload {
  
	public void result() {
		System.out.println("인자가 없는 메서드");
		//return; 강제로 끝내고 싶을 때는 return을 써도 됨.
		// 대신 void 일때는 return에 아무 값도 실을 수 없음 사실 void일때는 return을 쓰는 경우도 거의 없고 쓸 필요도 없음
	}

	//메서드 이름이 같기 때문에 오류가 나는게 당연하다.
	pulic void result( int n ) {
		System.out.println("정수를 인자로 받는 메서드");
	}
	public void result( char n) {
		System.out.println("문자를 인자로 받는 메서드");
	}
	public void result( String s, int n) {
		System.out.println("문자열, 정수를 인자로 받는 메서드");
	}

	public void result( int n, String s) {
		System.out.println("정수, 문자열을 인자로 받는 메서드");
	}
}
```	

```java
public class OverloadingMain {
	public static void main(String[] args) {

	Ex1_Overload ov = new Ex1_Overload();
	ov.result();
	ov.result(10);
	ov.result('A'); //인자를 char로 받으면 65를 넣어도 'A'가 출력되긴함.
	ov.result("hi",10);
	ov.result(10,"hi");
  }
}
```
