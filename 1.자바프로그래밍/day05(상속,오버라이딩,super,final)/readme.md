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


# 2차 상속
- 우리는 누군가의 자식이 될 수 있지만 누군가의 부모도 될 수 있듯이,
- 상속 역시 원한다면 다음 세대에게, 또 다음 세대로 이어질 수 있다.
- 자바도 마찬가지로 한 번에 상속에서 끝내지 않고 2차,3차 ... N차까지 원하는 만큼 상속을 이어받을 수 있다.

## Car 클래스
```java
package test3;

public class Car {
	public void ride() {
		System.out.println("달립니다.");
	}
}
```

## Bus클래스
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

## SchoolBus클래스
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

## CarMain 클래스
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

# final 클래스와 final 메서드
- final키워드는 상수를 뜻하는 키워드로, 필드 앞에 선언하여 사용한다.
- 초기화 이후 값을 바꿀 수 없으며 시간이 지나도 처음 정의된 상태가 변하지 않는다는 의미를 가지고 있다.
- 이 키워드는 메서드와 클래스에도 사용할 수 있다.

## final 클래스
- 클래스 앞에 final을 추가할 경우, 이 클래스는 상속의 마지막 클래스임을 뜻한다.
- 어떠한 클래스도 이 클래스의 자식 클래스가 될 수 없고, 자연스럽게 이 클래스는 어떤 클래스의 부모클래스가 될 수 없다.

```java
package test4;

public final class Parent {

}
```

```java
package test4;

public class Child  extends Parent{

}
```

## final 메서드
- 메서드 앞에 final을 추가하게 되면 상속은 받더라도, 오버라이딩 할 수 없는 메서드를 뜻한다.
- 즉, 자식 클래스이더라도 부모 클래스에 final로 선언된 메서드는 자식 클래스에서 오버라이딩 하지 못하고 있는 그대로 사용해야 한다.

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
