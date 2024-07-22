# 상속
- 상속이란 우리가 일반적으로 알고있는 의미와 비슷하다.
- 부모가 자식에게 무언가를 물려주는 것을 상속이라고 부르는 것처럼, 자바에서도 부모 역할을 하는 클래스가
- 자식 역할을 하는 클래스에게 클래스 멤버와 메서드를 물려주는것을 상속이라고 한다
- 상속은 클래스를 재사용하기 때문에 중복을 줄여주고 수정을 최소화하는 특징을 가지고 있다.

```
상속해주는 클래스를 부모클래스, 상위클래스, 기반클래스 라고한다.
상속받는 클래스를 자식클래스, 하위클래스, 파생클래스 라고한다.
```

## inheritance 패키지 생성하기
- 자바에서 상속을 구현하는 방법은 자식 클래스를 선언할 때, extends라는 키워드를 사용해 상속받을 클래스를 지명한다.
- 자식 클래스에서 선택받은 클래스는 부모 클래스 역할을 하게 된다.

```java
class A{ //부모 클래스는 자식 클래스에서 지명받기 전에는 부모 클래스 역할을 하지 않는다.
    ...
}

class B extends A{//B클래스에서 extends A를 작성함으로써 A는 B의 부모클래스가 되고, B클래스는 A클래스의 자식 클래스가 된다.
    ...
}
```
### Book클래스 생성하기
```java
package inheritance;

public class Book {
	String title;
	int price;
	
	void ifno() {
		System.out.println("책의 제목은 : " + title+"이고, 가격은 "+price+"원입니다.");
	}
}
```

### Comic클래스 생성하기
```java
package inheritance;

public class Comic extends Book{ //Book클래스 상속받는 자식 클래스 Comic
	//Comic클래스에서는 아무것도 구현하지 않았음
}
```

### BookMain클래스 생성하기
```java
package inheritance;

public class BookMain {
	public static void main(String[] args) {
		
		Comic comicBook = new Comic();
		comicBook.title = "포켓몬";
		comicBook.price = 4500;
		comicBook.info();
	}
}
```
## 상속에서의 생성자
- 자식 클래스의 객체를 생성할 때, 자식 클래스는 자식의 생성자를 통해 자식 객체를 생성한다.
```java
Comic comicBook = new Comic();
```
- 특별한 역할을 하지 않는 기본 생성자는 비어있는 것이 맞다.
- 하지만 자식 클래스의 기본 생성자는 다르다.
- 필드 초기화와 같은 특별한 역할을 하고 있지 않더라도 super()라는 메서드를 가지고 있다.

### super()
- this()가 같은 클래스의 다른 생성자를 호출할 때 사용된다면, super()메서드는 부모 클래스의 생성자를 호출할 때 사용한다.

```java
Comic(){
    super();//부모클래스에 기본생성자만 있다면 생략이 가능하다.
}
```
- 자식 클래스로 객체를 생성하기 위해 기본 생성자가 호출되면, super()라는 메서드를 통해 Book(부모클래스)의 기본 생성자를 호출한다.
- 그렇게 부모 객체를 먼저 생성한 후, 부모 객체를 감싸고 자식 객체를 생성한다.
- 자식 객체 안에는 부모 객체가 들어있게 된다.
- 따라서, 개발자가 직접 생성자를 선언할 때도 자식 클래스에서는 반드시 부모 클래스의 생성자를 호출해줘야 한다.
<br><br>

- 만약, 부모 클래스의 생성자가 호출될 때 매개변수로 값을 전달받아 부모 클래스의 필드들을 초기화 하도록 구현되어 있다면.
```java
부모클래스(매개변수1,매개변수2){
    this.필드1 = 매개변수1;
    this.필드2 = 매개변수2;
}
```
```java
자식클래스(매개변수1,매개변수2){
    super(매개변수1,매개변수2);
}
```

### Person클래스 생성하기
```java
package inheritance;

public class Person {
	String name;
	int age;
	
	public Person(String name,int age) {
		this.name = name;
		this.age = age;
	}
}
```

### Customer클래스 생성
```java
package inheritance;

public class Customer extends Person {
	int memberId;
	
	public Customer(String name,int age, int memberId) {
		super(name,age);
		this.memberId = memberId;
	}
	
	void eneter() {
		System.out.println("회원번호 : " + memberId +" (" + name+", "+age+"세) 님 입장하셨습니다.");
	}
}
```

### PersonMain클래스 생성하기
```java
package inheritance;

public class PersonMain {
	public static void main(String[] args) {
		Customer c1 = new Customer("박자바", 25, 11111);
		c1.enter();
		
		Customer c2 = new Customer("송코딩", 20, 22222);
		c2.enter();
	}
	
} 
결과
회원번호 : 11111 (박자바, 25세) 님 입장하셨습니다.
회원번호 : 22222 (송코딩, 20세) 님 입장하셨습니다.
```

## 오버라이딩(Overriding)
- 부모클래스를 상속받은 자식 클래스는 부모 클래스의 필드와 메서드를 가져와서 그대로 사용할 수 있습니다.
- 하지만 필요하다면, 자식 클래스가 상속받은 메서드의 내용을 변경해서 사용할 수도 있다.
- 우리는 이렇게 상속받은 메서드를 변경해서 다시 구현하는 것을 '오버라이딩(overriding)'이라고 한다.

### 오버라이딩 규칙
1. 부모클래스의 메서드명, 반환타입, 매개변수가 동일해아 한다.
2. 부모클래스의 메서드보다 접근 제한 범위를 줄일수는 있으나, 넓힐수는 없다.

### Computer클래스 생성
```java
package inheritance;

public class Computer {
	void powerOn() {
		System.out.println("삑~ 컴퓨터가 켜졌습니다.");
	}
	
	void powerOff() {
		System.out.println("컴퓨터가 종료됩니다.");
	}
}
```

### Samsong클래스 생성하기
```java
package inheritance;

public class Samsong extends Computer{
	@Override

	void powerOn() {
		System.out.println("아이 러브 삼송");
	}
}
```

### ComputerMain클래스 생성하기
```java
package inheritance;

public class ComputerMain {
	public static void main(String[] args) {
		Samsong s = new Samsong();
		s.powerOn();
		s.powerOff();
		
		Computer c = new Computer();
		c.powerOn();
		c.powerOff();
	}
}
결과
아이 러브 삼송
컴퓨터가 종료됩니다.
삑~ 컴퓨터가 켜졌습니다.
컴퓨터가 종료됩니다.
```
- 자식 클래스에서 오버라이딩된 메서드는 자식 객체를 통해 호출하게 되면 자식 클래스에서 구현한 메서드가 실행된다.
- 부모 객체를 통해 호출하면 자식 클래스와는 상관없이 부모 클래스의 원래 메서드로 호출되는것을 확인할 수 있다.

### @Override 어노테이션
- 자바에서 @키워드를 어노테이션이라고 부른다.
- 주석과 마찬가지고 코드를 실행하는데 직접적인 형향을 미치지는 않는다.
- 자동완성으로 오버라이딩을 구현하면, 자동으로 @Override가 메서드 상단에 추가된다.
- 생략해도 괜찮지만, 컴파일러에게 오버라이딩된 메서드라고 한번 더 짚어줌으로써 오타가 났을 때 오류를 발생시켜주기 때문에 실수를 줄일 수 있다.


## super키워드
- super키워드는 부모 클래스에서 상속받은 필드나 메서드를 자식 클래스에서 참조하는 데 사용하는 참조변수이다.
```
super.메서드명();
```
### Samsong클래스 코드 추가하기
```java
package inheritance;

public class Samsong extends Computer{
	@Override
	void powerOn() {
		super.powerOn();
		System.out.println("아이 러브 삼송");
	}
}
```
- main에서 실행하면 다음과 같은 결과를 얻을 수 있다.
```
삑~ 컴퓨터가 켜졌습니다.
아이 러브 삼송
컴퓨터가 종료됩니다.
삑~ 컴퓨터가 켜졌습니다.
컴퓨터가 종료됩니다.
```
- 이렇게 자바에서는 super참조 변수를 사용해 부모 클래스의 멤버에 접근할 수 있다.
- this와 마찬가지로 super 참조 변수를 사용할 수 있는 대상도 인스턴스 메서드뿐이며, 클래스 메서드에서는 사용할 수 없다.


# 상속에서의 생성자
- 모든 클래스는 생성자를 가진다.
- 그렇다면, 상속 관계에서 부모 클래스의 생성자와 자식 클래스의 생성자는 어떻게 사용해야 할까?



### Parent클래스 정의
```java
public class Parent {
	public Parent() {
		System.out.println("부모(Parent)클래스");
	}//생성자
}
```
![image](https://user-images.githubusercontent.com/54658614/220525863-1dacfa56-1566-4f61-abf3-95609102dc9f.png)

### Child클래스 정의
```java
public class Child extends Parent{

	//super : 부모 클래스
	public Child() {
		parent(); super(); //부모클래스의 생성자 호출
		System.out.println("자식(Child)클래스");
	}//생성자
}
```
- 자식 클래스로 객체를 생성하기 위해 기본 생성자가 호출되면, super()라는 메서드를 통해 부모클래스의 기본 생성자를 호출한다.
- 그렇게 부모 객체를 먼저 생성한 후, 부모 객체를 감싸고 자식 객체를 생성한다.
- 즉, 자식 객체 안에는 부모 객체가 들어있게 된다.

### SuperMain클래스 정의
```java
public class SuperMain{
	public static void main(String[] args) {
		Child c = new Child();
	}//main
}
```

### Parent클래스에 코드 추가( 파라미터를 받는 생성자)
```java
public class Parent {
	public Parent(int n) {
		System.out.println("부모(Parent)클래스" + n);
	}//생성자
	public int result() {
		return 100;
	}
}
```
### Child클래스에 코드 추가
```java
public class Child extends Parent{
	public Child() {
		super(1); //부모클래스의 생성자 호출
		System.out.println("자식(Child)클래스");
	}//생성자

	@Override
	public int result() {
		//super.result() : parent클래스의 result()메서드 호출
		return super.result();
	}
}
```
### SuperMain클래스 주석추가
```java
public class SuperMain {
	public static void main(String[] args) {
		Child ch = new Child();

	}
}
```

## 접근 제한자
### 1. 제한자
- 클래스, 변수 또는 메서드의 선언부에 함게 사용해 부가적인 의미를 부여하는 키워드
- 경우에 따라 여러 개를 조합해 사용할 수 있지만, 접근 제한자의 경우 하나만 선택해서 사용해야 한다.

### 2. 접근제한자
- 클래스나 멤버에 접근 가능한 범위를 제한하는 키워드
- 객체 지향 프로그래밍의 특징 중 한 가지인 정보 은닉을 지키기 위한 중요한 부분이다.
```
- public : 제한 없이 모든 패키지, 모든 클래스에서 접근 가능하다.
- protected : 같은 패키지 안에서 접근 가능하며, 다른 패키지라도 자식클래스라면 접근이 가능하다.
- default : 같은 패키지 내에서만 저근이 가능하다.
- private : 같은 클래스 내에서만 접근 가능하다.
```
### 클래스의 접근제한자
- 클래스는 접근 제한자로 public과 default만 가질 수 있다.
- private과 protected의 경우, 클래스 멤버들을 위한 접근 제한자로 클래스 외부에서 접근을 막을지 말지에 대한 접근을 제한하는 용도로 사용되기 때문에 클래스의 접근 제한자로 사용될 수 없다.

### public
- 접근 제한자 중에서 가장 사용 범위가 큰 제어자이다.
- public으로 선언된 클래스와 멤버들은 같은 패키지는 물론 다른 패키지의 클래스에서도 접근할 수 있다.
```
public 클래스/생성자 : 모든 패키지, 모든 클래스 어디서나 해당 클래스로 객체를 생성할 수 있다.
public 멤버(필드, 생성자,메서드) : 모든 패키지, 모든 클래스 어디서나 객체를 통해 접근할 수 있다.
```

### PublicA클래스 생성
```java
package modifier;

public class PublicA {
	public int a;
	
	public PublicA(int a) {
		this.a = a;
	}
	
	public void printA() {
		System.out.println("PublicA 클래스의 printA() 메서드이다.");
	}
}
```

### PublicB클래스 생성
```java
package modifier;

public class PublicB {
	public static void main(String[] args) {
		PublicA a = new PublicA(10);
		a.printA();
	}
}
```

### 객체 지향의 특징
- 캡슐화
  - 객체 내부의 멤버(필드,메서드 등)를 객체 외부에서 볼 수 없도록 캡슐화 한다.
  - 접근이 필요한 경우 public 메서드를 활용해 접근 허용하고, 이외의 값들은 모두 캡슐화를 통해 정보를 은닉한다.
- 추상화
  - 공통된 기능과 정보를 추출해 객체화한다.
- 상속
  - 미리 정의된 부모 클래스의 모든 멤버를 자식 클래스가 물려받는다.
- 다형성
  - 하나의 방법으로 여러 객체를 호출하여 사용할 수 있다.

### default
- 접근제한자를 따로 명시하지 않는다면 클래스와 멤버들은 자동으로 default를 가진다.
- default로 선언된 클래스와 멤버들은 같은 패키지 안에서는 어디든지 접근 및 사용이 가능하지만 다른 패키지에서는 접근이 불가능하다.
```
default 클래스/생성자 : 같은 패키지 내에서 어디서나 호출이 가능하며, 객체를 생성할 수 있다.
default 필드/메서드 : 같은 패키지 내에서 제한 없이 접근 및 사용할 수 있다.
```

### DefaultC클래스 생성하기
```java
package modifier;

class DefaultC {
	public int varableC; 
}
```

### PublicA클래스에 코드 추가하기
```java
package modifier;

public class PublicA {
	public int a;
	
	public PublicA(int a) {
		this.a = a;
	}
	
	public void printA() {
		System.out.println("PublicA 클래스의 printA() 메서드이다.");
	}
	
	DefaultC dc = new DefaultC(); //같은 패키지이기 때문에 객체생성 가능
	void methodA() {
		dc.varableC = 20; //public으로선언된 필드도 객체를 통해 접근 가능
	}
}
```

### PublicB클래스 생성
```java
package access;
import modifier.*;


public class PublicB {
	public static void main(String[] args) {
		DefaultC c = new DefaultC();//The type DefaultC is not visible
		//c.varableC = 10; 필드가 public이더라도 객체를 생성하지 못하기 때문에 사용할 수 없다.
	}
}
```

### protected
- 클래스 멤버를 위한 제한자로, 클래스의 접근 제한자로 사용하지 않는 protected는 상속과 관련있는 제한자이다.
- protected라는 이름처럼 조금 특별하게 클래스 멤버를 보호하고 있다.
- default처럼 같은 패키지 안에서 접근과 사용을 허가하지만, 다른 패키지에서의 접근을 완전히 제한하는 것이 아닌 "해당 클래스와 상속 관계에 있는 자식 클래스"라면 다른 패키지라도 접근 및 사용이 가능하다.
- 즉, 같은 패키지에서 접근이 가능하며, 다른 패키지라면 자식 클래스만 접근을 허용한다.

```
protected 생성자 : 같은 패키지의 클래스에서 생성자를 호출해 객체를 생성할 수 있다.
또한 다른 패키지더라도 해당 클래스의 자식 클래스라면 생성자를 호출해 객체를 생성할 수 있다.
protected 필드/메서드 : 같은 패키지의 클래스에서 접근 및 사용할 수 있으며, 해당 클래스의 자식 클래스라면 다른 패키지에서도 사용할 수 있다.
```

### modifier패키지에 Parent클래스 생성하기
```java
package modifier;

public class Parent {
	protected void accessProtected() {
		System.out.println("Protected 멤버에 접근하였습니다.");
	}
}
```

### access패키지에 Child클래스 생성하기
- 다른 패키지에 있지만
```java
package modifier;

import access.Parent;

public class Child extends Parent{
	void accessTest() {
		super.accessProtected(); //protected 키워드가 붙은 메서드도 이런식으로 접근이 가능하다.
		
		Parent p1 = new Parent();
		//p1.accessProtected(); 자식 클래스더라도, 객체로 접근하는것은 불가능하다.
	}
}
```

### access패키지에 NotChild클래스 생성하기
- 다른패키지에 있고 상속도 안받았기 때문에 안된다.
```java
package access;

import modifier.Parent;

public class NotChild {
	void accessTest() {
		Parent p2 = new Parent();
		//p2.accessProtected(); 에러
	}
}
```

### private
- 가장 사용 범위가 좁은 클래스 멤버를 위한 제한자이다.
- 클래스가 public/default이더라도, private로 선언된 멤버들은 클래스 외부에서 접근이 불가능하다.
- 오직 선언된 클래스 내부에서만 접근하여 사용할 수 있다.
- 따라서 private멤버는 public인터페이스를 직접 구현하지 않고, 클래스 내부의 세부적인 동작을 구현하는 데 사용된다.
```
private 생성자 : 클래스 외부에서 객체를 생성할 수 없으며, 클래스 내부에서만 생성자를 호출해 객체를 생성할 수 있다.

private 필드/메서드 : 클래스 외부에서 접근할 수 없으며, 클래스 내부에서만 사용할 수 있다.
```

### PublicA 클래스의 생성자를 private으로 만들기
```java
package modifier;

public class PublicA {
	public int a;
	
	private PublicA(int a) {
		this.a = a;
	}
	
	public void printA() {
		System.out.println("PublicA 클래스의 printA() 메서드이다.");
	}
	
	DefaultC dc = new DefaultC();
	void methodA() {
		dc.varableC = 20;
	}
}
```
- PublicB클래스를 확인하면 생성자부분에서 에러가 나는것을 확인할 수있다.

## 2차 상속
- 우리는 누군가의 자식이 될 수 있지만 누군가의 부모도 될 수 있듯이,
- 상속 역시 원한다면 다음 세대에게, 또 다음 세대로 이어질 수 있다.
- 자바도 마찬가지로 한 번에 상속에서 끝내지 않고 2차,3차 ... N차까지 원하는 만큼 상속을 이어받을 수 있다.
```
A 클래스 ← B 클래스 extends A 클래스 ← C클래스 extends D 클래스 ...  ← 
```

### Car 클래스
```java
package test3;

public class Car {
	public void ride() {
		System.out.println("달립니다.");
	}
}
```

### Bus클래스
```java
package test3;

public class Bus {
	
	int peopleNum;

	public Bus(int peopleNum) {
		this.peopleNum = peopleNum;
	}
	
	public void takePerson() {
		System.out.println("승객이 버스에 탔습니다.");
		peopleNum++;
	}
}
```

### SchoolBus클래스
```java
package test3;

public class SchoolBus extends Bus {

	public SchoolBus(int peopleNum) {
		super(peopleNum);
		// TODO Auto-generated constructor stub
	}
	
	@Override
	public void takePerson() {
		super.takePerson();
		System.out.println("학생들이 자리에 모두 착석하고 출발합니다.");
	}
	
	@Override
	public void ride() {
		System.out.println("시속 50km/h로 천천히 달립니다.");
	}
	
}
```

### CarMain 클래스
```java
package test3;

public class CarMain {
	public static void main(String[] args) {
		SchoolBus sb = new SchoolBus(10);
		sb.takePerson();
		sb.ride();
	}
}
```

## final 클래스와 final 메서드
- final키워드는 상수를 뜻하는 키워드로, 필드 앞에 선언하여 사용한다.
- 초기화 이후 값을 바꿀 수 없으며 시간이 지나도 처음 정의된 상태가 변하지 않는다는 의미를 가지고 있다.
- 이 키워드는 메서드와 클래스에도 사용할 수 있다.

## final 클래스
- 클래스 앞에 final을 추가할 경우, 이 클래스는 상속의 마지막 클래스임을 뜻한다.
- 어떠한 클래스도 이 클래스의 자식 클래스가 될 수 없고, 자연스럽게 이 클래스는 어떤 클래스의 부모클래스가 될 수 없다.

```java
public final class Parent {

}
```
- final 클래스를 상속받고자 시도한다면 에러가 발생한다.
```java
public class Child  extends Parent{

}
```

## final 메서드
- 메서드 앞에 final을 추가하게 되면 상속은 받더라도, 오버라이딩 할 수 없는 메서드를 뜻한다.
- 즉, 자식 클래스이더라도 부모 클래스에 final로 선언된 메서드는 자식 클래스에서 오버라이딩 하지 못하고 있는 그대로 사용해야 한다.

```java
접근제한자 final 반환형 메서드명(매개변수1,매개변수2...){

}
```

### Book클래스
```java
package test4;

public class Book {
	String title;
	String author;
	
	public Book(String title, String author) {
		this.title = title;
		this.author = author;
	}
	
	public final void info_title() {
		System.out.println("책의 제목은 " + title + "입니다.");
	}
	
	public void info_author() {
		System.out.println("책의 저자는 " + author + "입니다.");
	}
}
```

### Comic클래스
```java
package test4;

public class Comic extends Book{

	boolean isColor;
	
	public Comic(String title, String author, boolean isColor) {
		super(title, author);
		this.isColor = isColor;
		
	}
	
	//부모클래스에서 final로 선언된 메서드를 오버라이딩 시도하면 에러가 발생한다.
//	@Override
//	public void info_title(){
//		
//	}
	
	@Override
	public void info_author() {
		System.out.println("이 만화책의 저자는 " + author+"입니다.");
	}
	
	public void info_color() {
		if(isColor) {
			System.out.println("이 만화책은 컬러입니다.");
		} else {
			System.out.println("이 만화책은 흑백입니다.");
		}
	}
 
}

```

### BookMain
```java
package test4;

public class BookMain {
	public static void main(String[] args) {
		Comic comicBook = new Comic("주머니 괴물", "미상", true);
		comicBook.info_title();
		comicBook.info_author();
		comicBook.info_color();
	}
}
```

### 생성자에는 final을 추가할 수 없다.
- 생성자는 접근제한자(public,protected,private)만 추가할 수 있다.
- 따라서 클래스를 final로 선언하더라도 생성자를 final로 선언할 수 없다.
