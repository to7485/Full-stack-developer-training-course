# 클래스에서의 타입변환
- 타입 변환은 타입을 다른 타입으로 변환하는 것이다.
- 자바에서는 다음과 같이 두 가지의 대표적인 타입 변환이 있다.
    1. 자료형 변환 
    2. 클래스의 객체 타입 변환
- 클래스의 타입 변환도 마찬가지로 자동 형 변환과 강제 형 변환이 있다.
- 단, 자료형에 비해 타입 변환이 가능한 범위가 상당이 좁다.
- 클래스의 타입 변환은, 서로 상속 관계에 있는 클래스 사이에서만 변환할 수 있다.

## 클래스의 자동 타입 변환
- 자료형에서의 자동 형 변환과 마찬가지로 개발자가 직접 명시하지 않아도 자동으로 타입 변환이 일어나는 것을 '클래스 자동 타입 변환'이라고 한다.
- 클래스 자동 타입 변환은 상속 관계에 있는 자식 클래스의 객체를 부모 타입의 객체로 변환하는 것을 말한다.
```java
부모클래스명 객체명 = new 자식클래스명();
```
- 이미 만들어진 자식 객체를 부모 타입으로 변환하려고 할 때는 다음과 같이 구현한다.
```java
부모 클래스명 객체명 = 자식객체;
```
## Ex1_class_casting
```java
package test;

class Parent{};

class Child extends Parent{};

public class Test {
	public static void main(String[] args) {
		Parent p1 = new Parent(); //p1 객체 생성
		Child c1 = new Child(); //c1 객체 생성
		
		Parent p2 = new Child(); // 자동 타입 변환
		Parent p3 = c1;			 // 자동 타입 변환
		//Child c2 = p1; 자동 타입 변환이 되지 않음
		
		
		//기본 자료형끼리 비교를 할 때 == 연산자는 값이 같은지 비교하지만
		//객체끼리 비교를 할 때 == 연산자는 주소값이 같은 비교합니다.
		if (p3 == c1) {
			System.out.println("p3와 c1은 같은 객체를 참조하고 있습니다.");
		}
	}
}
```
- 우리는 p3와 c1이 같은 객체를 참조하고 있음을 알 수 있다.
- 즉, Child타입의 Child객체 c1의 타입을 Parent로 변환해 만든 p3는 여전히 c1 객체라는것을 확인할 수 있다.
- 타입을 변환한다고 객체가 바뀌는게 아니라, 객체는 보존되고 사용만 부모 객체처럼 한다.
- 자동 타입 변환은 반드시 자식 클래스의 객체를 부모 타입으로 변환할 때 적용할 수 있다.
- 1차 상속관계가 아니더라도 상위 계층의 타입으로 변환할 수 있다.
- 하지만 같은 상위 계층을 가지고 있더라도, 타입 변환을 시도하려는 두 클래스 간의 상속 관계가 없다면 타입 변환은 불가능하다.

## Ex2_class_casting
```java
package test;

class Car{};
class Bus extends Car{};
class SchoolBus extends Bus{};

class OpenCar extends Car{};
class SportCar extends OpenCar{};

public class Test {
	public static void main(String[] args) {
		Car c1 = new SchoolBus(); //1차 상속 관계가 아니더라도 자동 타입 변환 가능
		Bus b1 = new Bus();
		Bus b2 = new SchoolBus();
		
		Car c2 = new OpenCar();
		OpenCar oc = new SportCar();
		
		//Bus b3 = new OpenCar(); 오류
		//Bus b4 = new SportCar(); d오류
	}
}
```
- 타입을 부모 타입으로 변환한 객체는, 더 이상 자신의 클래스에 부모 클래스와 별개로 추가한 멤버들을 사용할 수 없다.
- 부모 클래스에 선언된 멤버만 사용할 수 있다.
- 단, 부모 클래스의 메서드를 오버라이딩 한 경우 메서드의 경우에는 자식 객체의 것을 호출할 수 있다.

### 자식 객체의 메서드가 호출되는 이유
- 메서드가 실행 시점에서 성격이 결정되는 동적바인딩 때문이다.
- 프로그램의 컴파일 시점에는 실행되는 메서드가 부모클래스의 것인지 하위클래스의 것인지 알기 어렵다.
- 실행 시점에 동적 바인딩이 일어나 부모가 자식 클래스의 멤버함수를 접근하여 실행할 수 있다.

### 동적바인딩의 작동
1. 클래스 계층구조
    - 자바에서 동적바인딩은 클래스 계층 구조에서 발생한다.
    - 상속하거나 인터페이스를 구현함으로써 계층을 갖는다.
    - 이 계층에서 메서드 오버라이딩이 가능하기 때문이다.
2. 메서드 오버라이딩
    - 자식 클래스는 부모 클래스의 메서드를 재정의(오버라이딩)할 수 있다.
    - 이 때, 자식 클래스에서 부모 클래스의 동일한 이름과 시그니처(함수명,매개변수 개수, 매개변수의 자료형)를 가진 메서드를 재정의한다.
3. 실행시 동적 바인딩
    - 객체가 생성되고 메서드가 호출될 때, 실제로 실행될 메서드는 객체의 실제 타입에 따라 결정된다.
    - 메서드 호출시 객체의 클래스 타입을 기반으로 어떤 메서드를 호출할지 동적으로 결정된다.
  
## Calendar클래스
```java
package test;

public class Calendar {
	String color;
	int months;
	
	public Calendar(String color, int months) {
		this.color = color;
		this.months = months;
	}
	
	public void info() {
		System.out.println(color + " 달력은 " + months + "월까지 있습니다.");
	}
	
	public void hanging() {
		System.out.println(color +"달력을 벽에 걸 수 있습니다.");
	}
}
```
## DeskCalendar클래스
```java
package test;

public class DeskCalendar extends Calendar {
	String color;
	int months;
	public DeskCalendar(String color, int months) {
		super(color,months);
	}
	
	@Override
	public void info() {
		System.out.println(color+"달력을 벽에 걸기 위해 고리가 추가로 필요합니다.");
	}
	
	public void onTheDesk() {
		System.out.println(color+" 달력을 책상에 세울 수 있습니다.");
	}
}
```

## CalendarMain클래스
```java
package test;

public class CalendarMain {

	public static void main(String[] args) {
		DeskCalendar dc = new DeskCalendar("보라색", 6);
		dc.info();
		dc.hanging();
		dc.onTheDesk();
		
		System.out.println();
		
		Calendar c = new DeskCalendar("검은색", 12);
		c.info();
		c.hanging(); //오버라이드된 메서드가 호출된다.
		//c.onTheDesk(); 에러
	}
}
```
- 타입 변환으로 생성된 c 객체는 Calendar타입을 가졌지만, DeskCalendar의 객체이기 때문에 DeskCalendar의 hanging()을 호출했다.
- 클래스 타입 변환을 한 객체는, 더이상 자식 클래스만의 멤버들을 호출할 수 없다.
- DeskCalendar객체임에도 Calendar타입을 가졌기 때문에, DeskCalendar의 멤버에는 접근할 수 없다.

## 클래스의 강제 타입변환
- 위의 코드에서 객체 c처럼 자식 타입에서 부모 타입으로 타입 변환을 했지만 자식 클래스의 멤버에게 접근하고 싶을 때가 생길 수 있다.
- 자바의 규약으로 자식 클래스의 멤버에 접근할 수 없으므로 이러한 경우 다시 DeskCalendar타입으로 변경해서 접근할 수 있도록 해야 한다.
- 우리는 이를 '클래스의 강제 타입 변환'이라고 부른다.
- 자식 객체가 부모 타입으로 자동 타입 변환을 한 후, 다시 자식 타입으로 변환하는 것을 말한다.

```java
일회성으로 타입 변환이 필요할 때는
((자식클래스명)객체명).메서드명();

자식클래스의 멤버에 접근이 여러번 필요한 경우
객체명 = (자식클래스명)부모타입;
```
### Bike클래스
```java
package test;

public class Bike {
	String riderName;
	int wheel = 2;
	
	public Bike(String riderName) {
		this.riderName = riderName;
	}
	
	public void info() {
		System.out.println(riderName + "의 자전거는 " + wheel +"발 자전거입니다.");
	}
	
	public void ride() {
		System.out.println("씽씽");
	}
}
```

### FourWheelBike클래스
```java
package test;

public class FourWheelBike extends Bike{

	public FourWheelBike(String riderName) {
		super(riderName);
		// TODO Auto-generated constructor stub
	}

	@Override
	public void info() {
		// TODO Auto-generated method stub
		super.info();
	}
	
	public void addWheel() {
		if(wheel == 2) {
			wheel = 4;
			System.out.println(riderName+"의 자전거에 보조 바퀴를 부착하였습니다.");
		} else {
			System.out.println(riderName+"의 자전거에 이미 보조 바퀴가 부착되어 있습니다.");
		}
	}
}
```

### BikeMain클래스
```java
package test;

public class BikeMain {
	public static void main(String[] args) {
		Bike b = new FourWheelBike("윤기");
		b.info();
		b.ride();
		//b.addWheel(); 부모 타입으로는 불가
		
		System.out.println();
		
		FourWheelBike fwb = (FourWheelBike)b;
		fwb.addWheel();
		fwb.info();
		fwb.ride();
	}
}
```
- 자식 타입으로 다시 변환을 해줌으로써 부모 타입에서는 사용하지 못했던 자식의 멤버들을 모두 사용할 수 있게 되었다.
- 단, 모든 부모 타입 객체를 자식 타입으로 변환할 수 있는 것은 아니다.
- 반드시 부모 타입으로 자동 타입 변환되었던 자식 객체를 다시 자식 타입으로 변환할 때만 강제 타입 변환을 사용할 수 있다.

## 다형성
- 다형성은 객체 지향 프로그래밍의 대표적인 특징 중 하나로, 하나의 타입으로 다양한 객체를 사용할 수 있다는것을 의미한다.
- 자바에서는 앞에서 학습한 타입 변환을 통해, 부모 클래스의 타입 하나로 여러 가지 자식 객체들을 참조하여 사용함으로써 다형성을 구현할 수 있다.
- 클래스의 타입 변환이 존재하는 이유는 다형성을 구현하기 위함이라고 할 수 있다.
- 완벽한 다형성을 구현하기 위해서는 상속 + 메서드 오버라이딩 + 클래스 타입변환 이 세가지 개념을 합쳐야 한다.
- 객체가 특정 클래스의 필드가 되면서, 하나의 부품처럼 사용될 수 있다.
- 이때, 부품을 교체할 일이 생긴다면 우리는 다형성을 구현함으로써 코드 수정을 최소화할 수 있다.

### Computer클래스
```java
package test;

public class Computer {
	public void powerOn() {
		System.out.println("삑- 컴퓨터가 켜졌습니다.");
	}
	
	public void powerOff() {
		System.out.println("컴퓨터가 종료됩니다.");
	}
}
```

### Samsung클래스
```java
package test;

public class Samsung extends Computer{
	@Override
	public void powerOn() {
		super.powerOn();
		System.out.println("아이 러브 삼송");
	}
	
}
```
### ComputerRoom클래스
```java
package test;

public class ComputerRoom {
	Samsung com1;
	Samsung com2;
	
	public void allPowerOn() {
		com1.powerOn();
		com2.powerOn();
	}
	
	public void allPowerOff() {
		com1.powerOff();
		com2.powerOff();
	}
}
```

### ComMain클래스
```java
package test;

public class ComMain {

	public static void main(String[] args) {
		ComputerRoom cr = new ComputerRoom();
		cr.com1 = new Samsung();
		cr.com2 = new Samsung();
		
		cr.allPowerOn();
		cr.allPowerOff();
		
		System.out.println();

	}
}
```
- 지금까지는 사용하는데 아무런 불편함이 없다.
- 하지만 컴퓨터실에 있는 컴퓨터 두대를 LZ컴퓨터로 바꾸고 싶다면 어떻게 해야할까??

### LZ클래스
```java
package test;

public class LZ extends Computer{
	
	@Override
	public void powerOn() {
		super.powerOn();
		System.out.println("사랑해요 LZ");
	}
}
```

### ComputerRoom 클래스 수정하기
```java
package test;

public class ComputerRoom {
	//Samsung com1;
	//Samsung com2;
	
	//LZ com1;
	//LZ com2;

	//매번 다른 브랜드의 컴퓨터로 바꾸기 위해 코드를 수정하면 피곤해지기도 하고
	//실수를 할 위험성도 커진다.

	//클래스의 타입변환을 사용하면 보다 간결하게 해결할 수 있다.
	Computer com1;
	Computer com2;
	
	public void allPowerOn() {
		com1.powerOn();
		com2.powerOn();
	}
	
	public void allPowerOff() {
		com1.powerOff();
		com2.powerOff();
	}
}

```
- 객체를 변경하기 위해 여러 가지 코드를 수정하는 것은 상당히 위험도가 높은 작업이다.
- 실무에서의 프로그램은 코드의 양이 많아지고, 수 많은 객체거 서로 얽혀서 복잡한 로직으로 구현되어 있다.
- 그렇기 때문에 수정을 최소화 하는것이 좋다.

### ComMain클래스 수정하기
```java
package test;

public class ComMain {

	public static void main(String[] args) {
		ComputerRoom cr = new ComputerRoom();
		//cr.com1 = new Samsung();
		//cr.com2 = new Samsung();
		cr.com1 = new LZ();
		cr.com2 = new LZ();
		
		cr.allPowerOn();
		cr.allPowerOff();
		
		System.out.println();

	}
}
```

## instancdof연산자
- 부모 타입으로 타입이 변환되어 저장된 변수는 안에 어떤 객체가 담겨 있는지 직접 확인하지 않는 이상 내부 객체를 알기 쉽지 않다.
- 오버라이딩된 메서드가 있다면 확인이 쉽겠지만, 부모클래스를 같이 상속받고 있는 다른 클래스 또는 부모클래스와 구별할 수 있는 특정 멤버가 없다면 어떻게 구별해야 할까?
- instanceof연산자의 특징
    -  A instanceof B : A 객체가 생성될 때 B 타입으로 생성되었는지 확인하는 연산자
    -  맞으면 true, 아니면 false를 반환하며 만약 null을 가리키고 있으면 false를 반환한다.

### 객체 instanceof타입(클래스명)
```
- instanceof 기준으로 왼쪽 객체가 생성될 때 오른쪽 타입으로 생성되었는지 확인하는 연산자이다.
- 맞으면 true, 아니면 false를 반환하며 만약 null을 가리키고 있으면 false를 반환한다.
```

## FarmTest클래스
```java
package test;

class Animal{}
class Pig extends Animal{}
class Cow extends Animal{}

class Farm{
	public void sound(Animal animal) {
		if(animal instanceof Pig) {
			System.out.println("꿀꿀");
		} else {
			System.out.println("음메");
		}
	}
}


public class FarmTest {
	public static void main(String[] args) {
		Farm f = new Farm();
		Pig p = new Pig();
		Cow c = new Cow();
		f.sound(p);
		f.sound(c);
	}
}
```
### instanceof 연산자와 '=='연산자의 차이
- A instanceof B : 객체변수 A가 객체의 타입 B로 생성된것인지 확인
- C == D : 객체 변수 C와 객체 변수 D가 같은 객체를 참조하고 있는지 확인한다.

### Instanceof클래스 생성하기
```java
package class_casting;

class Animal{};
class Pig extends Animal{};

public class Instanceof {
	public static void main(String[] args) {
		Pig p1 = new Pig();
		Pig p2 = new Pig();
		
		Animal a = p1;
		
		if( a instanceof  Pig) {
			System.out.println("객체 변수 a는 Pig타입으로 생성된 객체이다.");
		}
		
		if(a == p1) {
			System.out.println("a와 p1은 같은 객체를 참조하고 있다.");
		}
		
		if(a != p2) {
			System.out.println("a와 p2는 같은 객체를 참조하고 있지 않다.");
		}
	}
}
```

## 오버라이딩으로 해결하기
- instanceof 연산자를 사용하지 않고도, 오버라이딩을 사용해 같은 문제를 해결할 수 있다.
```java
package test;

class Animal{
	public void cry() {};
}
class Pig extends Animal{
	@Override
	public void cry() {
		System.out.println("꿀꿀");
	}
}
class Cow extends Animal{
	@Override
	public void cry() {
		System.out.println("꿀꿀");
	}
}

class Farm{
	public void sound(Animal animal) {
		animal.cry();
	}
}


public class FarmTest {
	public static void main(String[] args) {
		Farm f = new Farm();
		Pig p = new Pig();
		Cow c = new Cow();
		f.sound(p);
		f.sound(c);
	}
}
```

## 오버로딩과 오버라이딩
- 객체 지향 프로그래밍에서 다형성을 얘기할 때 빼놓을 수 없는 것이 바로 오버로딩과 오버라이딩이다.
- 비슷한 기능을 하고 중복되는 구현이 필요하지만 우리는 오버로딩과 오버라이딩을 적절히 사용할 수 있다면, 중복이 없는 최소한의 코드로 원하는 기능을 모두 구현해낼 수 있다.

### 오버로딩
- 자바는 매개변수의 자료형/개수/순서를 기반으로 메서드를 구별하므로 하나의 클래스 안에서 같은 이름의 메서드를 여러 개 구현하고 필요에 따라 메서드를 선택해 사용할 수 있다.
### 오버라이딩
- 부모 클래스에게 상속받은 메서드를 재정의하여 자식 클래스용 메서드를 구현하고 자식 객체를 통해 메서드를 호출하면 오버라이딩된 메서드가 호출된다.


<br>

**간단히 정리하자면 오버로딩은 새로운 메서드를 정의하는 것이며, 오버라이딩은 상속받은 기존의 메서드를 재정의하는 것을 말한다.**

### InheritanceMethodTest클래스 생성하기
```java
package class_casting;

class Parent{
	public void display() {
		System.out.println("부모 클래스의 display()메서드이다.");
	}
}

class Child extends Parent{
	
	//오버라이딩 된 display()메서드
	@Override
	public void display() {
		System.out.println("자식 클래스의 display() 메서드이다.");
	}
	
	//오버로딩된 display()메서드
	public void display(String str) {
		System.out.println(str);
	}
}

public class Inheritance {
	public static void main(String[] args) {
		Child ch = new Child();
		ch.display();
		ch.display("오버로딩된 display()메서드입니다.");
	}
}
```
# 추상화
- 공통성과 본질을 모아 추출하는것
- 기존 클래스들의 공통적인 요소를 모아 상위 클래스를 만들어내는 기술
- 공통적인 속성과 행위를 모아 정의하면, 반복적인 코드를 줄일수 있고, 보다 효과적인 클래스간의 관계를 설정하여 유지보수가 용이해진다.

```
- 바로 전에 작성했던 FarmTest에서 메서드 오버라이딩을 이용하여 처리한 경우를 다시한번 살펴보자.
- Animal클래스의 cry()메서드가 텅 비어있는 것을 확인할 수 있다.
- Animal 객체를 통해 직접 cry()메서드를 호출할 일은 없지만,
- Animal클래스를 상속받은 자식 클래스들이 cry()메서드를 오버라이딩 하여 재정의 하고
- 타입변환을 통해서 그 메서드를 사용하기 위함이었다.
```

## 추상메서드
- 선번부만 작성하고 구현부는 작성하지 않고 남겨둔 미완성 메서드를 '추상 메서드'라고 한다.
- 다형성을 위해 메서드의 선언은 통일해야 하지만, 실제로 구현하는 내용은 자식클래스마다 달라야 할 때
- 부모 클래스의 메서드는 비워두고 자식 클래스에서 오버라이딩하여 구현을 할 수 있다.
- 추상 메서드를 선언할 때 abstract 키워드를 함께 표기해야 한다.
- 또한 메서드의 구현부인 중괄호{} 대신 구현부가 없다는 의미로 세미콜론(;)를 쓴다.

```java
[접근제한] abstract [반환형] [메서드명](파라미터1,파라미터2);
abstract [접근제한] [반환형] [메서드명](파라미터1,파라미터2);
```
## 추상 클래스(abstract class)
- 추상메서드가 한 개 이상 정의되어 있는 클래스를 추상 클래스라고 한다.
- 추상 메서드를 포함하고 있다는 것을 제외하고 일반 클래스와 다르지 않다.
- 추상 클래스에도 생성자가 있으며, 멤버변수와 메서드도 가질 수 있다.
- 추상 클래스 또한 abstract를 통해 자신이 추상클래스임을 명시해줘야 한다.
```java
[접근제한] abstract class [클래스명]{
	//필드
	//생성자
	//메서드(추상메서드 포함)
}
```
### 추상 클래스의 특징
- 일반 클래스 처럼 독립적으로 생성자를 호출해 객체를 생성할 수 없다.
- 자식 클래스의 생성자에 super()를 총해 추상 클래스의 생성자를 호출하여 부모 객체를 생성한 후 자식 객체를 생성한다.

### Receipt클래스 만들기
```java
package abstrarct;

public abstract class Receipt {
	String chef;
	
	public Receipt(String chef) {
		this.chef = chef;
	}
	
	void info() {
		System.out.println("이 레시피는 " + chef+"님의 레시피입니다.");
	}
}
```

### PastaReceipt클래스 만들기
```java
package abstrarct;

public class PastaReceipt extends Receipt{

	public PastaReceipt(String chef) {
		super(chef); //부모클래스의 생성차 호출
	}
	
	void makeSource() {
		System.out.println("파스타 소스를 직접 만듭니다.");
	}
}
```

### StakeReceipt클래스 만들기
```java
package abstrarct;

public class StakeReceipt extends Receipt{

	public StakeReceipt(String chef) {
		super(chef);
	}

	void grillStake() {
		System.out.println("스테이크를 맛있게 굽습니다.");
	}
	
}
```

### ReceiptMain클래스 정의
```java
package abstrarct;

public class ReceiptMain {
	public static void main(String[] args) {
		//Receipt r = new Receipt(); -> 추상클래스는 직접 객체를 생성할 수 없음
		
		PastaReceipt pr = new PastaReceipt("최연석");
		pr.info(); //자식객체를 통해 추상 클래스의 메서드를 호출할 수 있음
		pr.makeSource();
		
		StakeReceipt sr = new StakeReceipt("이현복");
		sr.info();
		sr.grillStake();
	}
}
```
- 추상클래스는 사실 일반 클래스와 크게 다를것은 없어보이지만, 직접 객체를 생성하지 못한다는 사실을 알 수 있다.

### 추상클래스에 추상메서드는 언제 구현해야 할까??
- 자식 클래스들이 반드시 구현해야 하는 메서드가 있다면, 우리는 추상 메서드로 해당 메서드를 부모 클래스(추상클래스)에 선언해 둘 수 있다.
```
추상 클래스를 상속받은 모든 자식 클래스는 반드시 추상 메서드를 오버라이딩 및 재정의하여 구현해야 한다.

그렇지 않으면 컴파일 에러가 발생한다.
```

### Phone 클래스
```java
package test2;

public abstract class Phone {
	abstract public void openingLogo();
	
	public void powerOn() {
		openingLogo();
		System.out.println("핸드폰이 켜집니다.");
	}
	
	public void powerOff() {
		System.out.println("핸드폰이 꺼집니다.");
	}
}
```

### PineapplePhone클래스
```java
package test2;

public class PineApplePhone extends Phone{

	@Override
	public void openingLogo() {
		System.out.println("@@@");
	}
}
```

### ThreeStarPhone클래스
```java
package test2;

public class ThreeStarPhone extends Phone{

	@Override
	public void openingLogo() {
		System.out.println("★★★");
	}
}
```

### PhoneMain클래스
```java
package test2;

public class PhoneMain {
	public static void main(String[] args) {
		PineApplePhone pp = new PineApplePhone();
		pp.powerOn();
		pp.powerOff();
		
		System.out.println();
		
		ThreeStarPhone tp = new ThreeStarPhone();
		
		tp.powerOn();
		tp.powerOff();
	}
}
```

## 추상 클래스와 추상 메서드의 용도
```
- 자식 클래스 간의 공통적인 필드와 메서드 이름을 통일할 수 있다.
- 반드시 구현해야 하는 메서드를 선언함으로써 공통 규격을 제공한다.
```
- 결과적으로 자식 클래스들의 규격과 내용을 통일하기 위함이며, 이는 곧 객체 지향 프로그래밍의 다형성을 구현하기 위한 탄탄한 기반이 된다.

# 인터페이스
- 모든 메서드가 추상 메서드인 일종의 추상 클래스를 '인터페이스'라고 부른다.
- 인터페이스는 <b>추상 메서드와 상수</b> 로만 이루어져 있으며, 추상클래스와 마찬가지로 스스로 객체를 생성할 수 없다.
- 언뜻 보면 인터페이스와 추상 클래스가 같은 역할을 하는 것처럼 느껴질 수 있지만, 취지는 완전히 다르다.
- 추상 클래스는 자식클래스들의 공통적인 특징을 추출하고 제공하는것이 주된 역할이었다면

![image](img/추상화.png)

![image](img/인터페이스.png)

- 인터페이스는 그뿐 아니라 다른 클래스 코드들과의 중간 매개 역할을 하는 것을 중점으로 생각할 수 있다.


## 인터페이스의 선언
- 인터페이스는 클래스가 아니다.
- 추상클래스는 스스로 객체를 생성할 수는 없지만, 자식 클래스의 생성자를 통해 객체를 생성해낼 수 있었다.
- 하지만 인터페이스는 어떤 형태로도 객체를 만들 수 없기 때문에 클래스라고 부를 수 없다.
- 인터페이스는 객체의 매개체, 즉, 객체를 사용하는 방법을 제공하는 새로운 블록이라고 할 수 있다.

```java
[접근제한자]interface 인터페이스명{
	//상수
	//추상메서드
}
```
- 인터페이스를 선언하는 방법은 클래스를 작성하는 방법과 동일하며 class키워드 대신 interface를 작성한다.
- 또한, 인터페이스의 추상 메서드는 다른 클래스들과의 매개체 역할을 하므로 누구나 접근할 수 있다.
- 따라서 항상 public으로 구현한다.
- 만약 접근자를 default로 구현했다면 자동으로 public으로 인식한다.

### Phone인터페이스
```java
package test3;

public interface Phone {
	
	public static final int MAX_BATTERY_CAPACITY = 100;
	
	abstract void powerOn();
	abstract void powerOff();
	abstract boolean isOn();
	abstract void watchUtube();
	abstract void charge();
}
```
- 추상 클래스는 추상 메서드가 비어있기 때문에 객체 생성을 스스로 할 수 없다.
- 대신 자식 클래스의 생성자의 힘을 빌려 객체 생성을 할 수 있었다.
- 인터페이스도 마찬가지로 추상 메서드가 비어있기 때문에 객체 생성을 스스로 할 수 없다.
- 따라서 인터페이스도 자신이 가지고 있는 추상 메서드를 구현해줄 클래스를 작성해야만 한다.
- 인터페이스를 구현해주는 클래스를 '구현 클래스'라고 한다.


### 상수의 선언
- 인터페이스에서는 필드 대신 상수를 선언할 수 있다.
- 단, 상수이기 때문에 인터페이스는 고정된 값만 선언할 수 있어 충분한 고민을 통해 선언해야 한다.
```java
[접근제한자] interface 인터페이스 이름{
	public static final 자료형 상수명 = 값;
}

public : 인터페이스는 다른 클래스들의 접근이 가능해야 하기 때문에 public으로 한다.
static : 객체가 생성되지 않는 인터페이스이기 때문에, 내부 상수에 접근하려면 클래스 변수처럼 static으로 선언되어 메모리에 올라가있어야 한다.
final : 상수를 뜻하는 키워드이다.
```

## 인터페이스 사용
- 추상클래스는 추상메서드가 비어있기 때문에 객체를 스스로 생성할 수 없다.
- 대신 자식 클래스의 생성자의 힘을 빌려 객체를 생성할 수 있었다.
- 인터페치스 역시 추상 메서드가 비어있기 때문에 객체 ㅅ애성을 스스로 할 수 없다.
- 인터페이스를 구현해주는 클래스를 '구현 클래스'라고 한다.

### implements
- 구현 클래스는 인터페이스를 사용해 구현하겠다는 선언을 해야 한다.
- 구현한다는 의미를 가지고 있는 implements키워드를 사용하여 명시할 수 있다.
```java
[접근제한자]class 클래스명 implements 인터페이스명{
	//필드
	//생성자
	//메서드(추상메서드 오버라이딩)
}
```


### PineApplePhone클래스
```java
package test3;

public class PineApplePhone implements Phone{
	int batteryCapacity = 40;
	boolean isOn = false;
	
	@Override
	public void powerOn() {
		if(batteryCapacity > 30) {
			System.out.println("@@@Power On!!@@@");
			isOn = true;
		} else {
			System.out.println("Low Battery...");
		}
		
	}
	
	@Override
	public void powerOff() {
		System.out.println("@@@Power Off!!@@@\n");
		isOn = false;
		
	}
	
	@Override
	public boolean isOn() {
		if(isOn) {
			return true;
		} else {
			return false;
		}
	}
	
	@Override
	public void watchUtube() {
		if(batteryCapacity > 10) {
			System.out.println("--- watching Utube ---");
			batteryCapacity -= 10;
			System.out.println("battery is..." + batteryCapacity + "%\n");
		} else {
			System.out.println("Low Battery...");
			powerOff();
		}
		
	}
	
	@Override
	public void charge() {
		if(batteryCapacity < Phone.MAX_BATTERY_CAPACITY - 20) {
			System.out.println("--- charging ---");
			batteryCapacity += 5;
			System.out.println("Charged..." + batteryCapacity + "%\n");
		} else {
			System.out.println("You don't have to charge...");
			System.out.println("It's enough... " + batteryCapacity + "%");
		}
		
	}
}
```

### ThreeStarPhone클래스
```java
package test3;

public class ThreeStarPhone implements Phone{
	int batteryCapacity = 40;
	boolean isOn = false;
	
	@Override
	public void powerOn() {
		if(batteryCapacity > 30) {
			System.out.println("★★★폰이켜졌습니다.★★★");
			isOn = true;
		} else {
			System.out.println("배터리가 부족합니다...");
		}
		
	}
	
	@Override
	public void powerOff() {
		System.out.println("★★★폰이 꺼졌습니다.★★★\n");
		isOn = false;
		
	}
	
	@Override
	public boolean isOn() {
		if(isOn) {
			return true;
		} else {
			return false;
		}
	}
	
	@Override
	public void watchUtube() {
		if(batteryCapacity > 10) {
			System.out.println("--- U튜브 시청 중 ---");
			batteryCapacity -= 10;
			System.out.println("잔여 배터리" + batteryCapacity + "%\n");
		} else {
			System.out.println("배터리가 부족합니다...");
			powerOff();
		}
		
	}
	
	@Override
	public void charge() {
		if(batteryCapacity < Phone.MAX_BATTERY_CAPACITY - 20) {
			System.out.println("--- 충전중 ---");
			batteryCapacity += 5;
			System.out.println("잔여 배터리" + batteryCapacity + "%\n");
		} else {
			System.out.println("충전할 필요가 없습니다.");
			System.out.println("잔여 배터리..." + batteryCapacity + "%");
		}
		
	}
}
```
### Person클래스
```java
package test3;

public class Person {
	Phone p;
	
	public Person(Phone p) {
		this.p = p;
	}
	
	public void buyNewPhone(Phone p) {
		this.p = p;
		System.out.println(" = = = = = = == =");
		System.out.println("새 폰을 샀습니다.");
	}
	
	public void turnOnPhone() {
		p.powerOn();
	}
	
	public void turnOffPhone() {
		p.powerOff();
	}
	
	public void watchUtube() {
		if(p.isOn()) {
			p.watchUtube();
		}else {
			System.out.println("폰이 꺼져 있기 대문에 U튜브를 볼 수 없습니다.");
		}
	}
	
	public void chargePhone() {
		p.charge();
	}
}
```

### PhoneMain클래스
```java
package test3;

public class PhoneMain {
	public static void main(String[] args) {
		Person jimin = new Person(new PineApplePhone());
		jimin.turnOnPhone();
		for(int i = 1; i < 6; i++) {
			jimin.watchUtube();
			
			if(i % 3 == 0) {
				jimin.chargePhone();
			}
		}
		
		jimin.buyNewPhone(new ThreeStarPhone());
		jimin.turnOnPhone();
		
		for(int i = 1; i < 5; i++) {
			jimin.watchUtube();
			
			if(i % 3 == 0) {
				jimin.chargePhone();
			}
		}
	}
}
```
### 인터페이스의 장점
- 정보은닉 : 실제 구현 클래스의 내용을 전혀 보지 않고도 개발 코드로 객체를 사용할 수 있다.
- 모듈화 : 구현 클래스들이 독립적으로 구현되고 사용될 수 있다. 개발 코드에서 객체 변경이 필요할 때, 개발코드의 수정을 최소화할 수 있다.

### 추상 클래스와 인터페이스의 공통점
- 정보은닉, 모듈화, 추상화 등은 추상클래스와 인터페이스가 공통적으로 가진 장점이다.
- 추상 클래스와 인터페이스 모두 다형성을 구현할 수 있는 기반을 제공하며, 추상 메서드 구현에 대한 강제성을 반영하고 있다.

## 다중 인터페이스 구현
- 우리는 하나의 클래스로 여러 개의 인터페이스를 구현할 수 있다.
- 선언한 모든 인터페이스에 대한 추상 메서드를 모두 구현해 줘야 한다.
```java
[접근제한자]class 클래스명 implements 인터페이스1,인터페이스2{
	//필드
	//생성자
	//인터페이스1에 대한 구현 메서드
	//인터페이스2에 대한 구현 메서드
}
```
### MicroPhone인터페이스 생성
```java
package inter;

public interface MicroPhone {
	abstract void sing();
}
```

### Speaker인터페이스 생성
```java
package inter;

public interface Speaker {
	abstract void music();
}
```

### BluetoothMIC클래스 생성
```java
package inter;

public class BluetoothMIC implements MicroPhone, Speaker{

	@Override
	public void music() {
		// TODO Auto-generated method stub
		
	}

	@Override
	public void sing() {
		// TODO Auto-generated method stub
		
	}

}
```

## 인터페이스 상속
- 인터페이스끼리 상속관계를 만들 수 있다.
- 클래스의 상속과 만찬가지로 extends키워드를 사용하며, 다중 상속이 가능하기 때문에 콤마(,)를 이용해서 다음과 같이 선언한다.
```java
[접근제한자] interface 인터페이스명 extends 인터페이스1, 인터페이스2,...{

}
```
- 인터페이스 상속을 선언하면, 하위 클래스는 상위 클래스의 모든 멤버를 상속받게 된다.
- 따라서 만약 하위 인터페이스를 구현하는 클래스가 있다면, 해당 클래스는 하위 인터페이스의 추상메서드를 포함하여 상위 인터페이스르의 추상 메서드까지 구현해야 한다.

### BluetoothMIC 인터페이스로 수정하기
```java
package inter;

public interface BluetoothMIC extends MicroPhone, Speaker{

	abstract void connect();
}
```

### TJmic클래스 생성하기
```java
package inter;

public class TJmic implements BluetoothMIC{

	@Override
	public void sing() {
		System.out.println("마이크에 대고 노래를 부른다.");
		
	}

	@Override
	public void music() {
		System.out.println("마이크에 장착된 스피커로 반주가 나온다.");
		
	}

	@Override
	public void connect() {
		System.out.println("핸드폰과 블루투스 연결이 되었습니다.");
	}
}
```

### MicMain클래스 수정하기
```java
package inter;

public class MicMain {
	public static void main(String[] args) {
		System.out.println("---TJmic 객체---");
		TJmic tj = new TJmic();
		tj.connect();
		tj.music();
		tj.sing();
		
		System.out.println("\n---TJmic 객체를 BluetoothMIC로 타입 변환---");
		BluetoothMIC bm = tj;
		bm.connect();
		bm.music();
		bm.sing();
		
		System.out.println("\n---TJmic 객체를 Microphone으로 타입 변환---");
		MicroPhone m = tj;
		//m.connect(); 호출불가능
		//m.music(); 호출불가능
		m.sing();
		
		System.out.println("\n--TJmic 객체를 Speaker로 타입 변환---");
		Speaker s = tj;
		//s.connect(); 호출불가능
		s.music();
		//s.sing(); 호출불가능
		
	}
}

결과
---TJmic 객체---
핸드폰과 블루투스 연결이 되었습니다.
마이크에 장착된 스피커로 반주가 나온다.
마이크에 대고 노래를 부른다.

---TJmic 객체를 BluetoothMIC로 타입 변환---
핸드폰과 블루투스 연결이 되었습니다.
마이크에 장착된 스피커로 반주가 나온다.
마이크에 대고 노래를 부른다.

---TJmic 객체를 Microphone으로 타입 변환---
마이크에 대고 노래를 부른다.

--TJmic 객체를 Speaker로 타입 변환---
마이크에 장착된 스피커로 반주가 나온다.
```

## 내부 클래스
- 내부 클래스는 클래스 안에 만들어진 또 다른 클래스로 중첩 클래스라고도 부른다.
- 클래스에 다른 클래스를 선언하는 이유는 두 개의 클래스가 서로 긴밀한 관계를 맺고 있기 때문이다.

### 내부 클래스의 장점
- 두 클래스 멤버들 간에 손쉽게 접근할 수 있다.
- 불필요한 클래스를 감춰서 코드의 복잡성을 줄일 수 있다.

```java
public class OuterClass{ //외부 클래스

	class InnerClass{ //내부 클래스

	}
}
```

### 내부 클래스의 종류
|메서드|설명|
|-----|-----|
|인스턴스 클래스|외부 클래스의 멤버 변수와 같은 위치에 선언<br>주로 외부 클래스의 멤버 변수와 관련된 작업에 사용될 목적으로 선언|
|정적 클래스|외부 클래스의 클래스 변수와 같이 static키워드 부여|
|지역 클래스|외부 클래스의 메서드 내부에서 선언하여 사용<br>메서드 영역에서 선언되기 때문에 메서드 내부에서만 사용 가능|

## 인스턴스 클래스
- 인스턴스 클래스는 외부 클래스 내부에서 생성하고, 선언되어 사용하는 클래스를 의미한다.
- 인스턴스 변수(필드)와 같은 위치에 선언하며, 외부 클래스의 인스턴스 멤버처럼 다루어진다.
- 주로 외부클래스의 멤버들과  관련된 작업에 사용될 목적으로 선언된다.

```java
public class Outer{
	private String name; //필드

	//인스턴스 클래스
	public class Inner{
		private String name;
	}

}
```
- 내부 클래스도 외부 클래스 안에 생성되는 것 외에는 별도의 클래스이기 때문에, 파일이 컴파일되면 별도로 생성된다.

### 인스턴스 클래스의 객체화
- 인스턴스 클래스는 기본적인 내부 클래스이다.
- 외부 클래스 안에 생성되기 때문에, 클래스를 사용하려면 외부 클래스객체가 생성된 상태에서 객체 생성을 할 수 있다.

```java
Outer outer = new Outer(); //외부 클래스 객체 생성
Outer.Inner in = Outer.new Inner(); //외부 클래스를 이용해 내부 클래스 객체 생성
```

### CalculatorExample클래스
```java
package test3;

class Calculator{
	private int val1;
	private int val2;
	
	public Calculator(int val1, int val2) {
		this.val1 = val1;
		this.val2 = val2;
	}
	
	public class Calc{
		public int add() {
			return val1 + val2;
		}
	}
}


public class CalculatorExample {
	public static void main(String[] args) {
		Calculator cal = new Calculator(10, 11);
		Calculator.Calc c = cal.new Calc();
		System.out.println("합 : " + c.add());
	}
}
```
- 하나의 소스파일에 둘 이상의 public class가 존재하면 안된다.
- 각 클래스를 별도의 소스파일에 나눠서 저장하던가 아니면 둘 중 한 클래스에만 public을 붙혀야 한다.

## 정적 내부 클래스(static class)
- 클래스 안에 정적 변수를 선언할 수 있는 것처럼 클래스도 정적 클래스를 만들 수 있다.
- 필드(멤버)와 마찬가지로 static키워드를 사용해 클래스를 선언한 후 정적 내부 클래스를 생성한다.
- 주로 외부 클래스의 static메서드에서 사용될 목적으로 만든다.

```java
public class Outer{
	private String name; -> 필드

	public static class Inner{
		private String name;
	}
}
```
- 외부 클래스의 필드 또는 메서드를 정적 내부 클래스 안에서는 사용할 수 없다.
```java
public class Outer{
	private int val1; //필드

	public static class Inner{
		public void add(){
			int result = val1 + 10; -> 에러
		}
		
	}
}
```
- 정적 내부 클래스는 정적 변수 또는 정적 메서드를 호출하는 것은 가능하다.
```java
public class Outer{
	private int val1; //필드
	private static int cnt = 1; //클래스 변수

	public static class Inner{
		public void displayOuterInfo(){
			System.out.println(val); -> 에러
			System.out.println(cnt);
		}
		
	}
}
```
## 정적 내부 클래스의 객체 생성
- 외부 클래스의 객체를 생성하지 않아도 선언할 수 있다.
```java
Outer.Inner in = new Outer.Inner();
```

## StaticClassExam클래스
```java
package test3;

class PrintOut{
	public static class Out{
		public void println(String str) {
			System.out.println(str);
		}
	}
}

public class StaticClassExample {
	public static void main(String[] args) {
		String str = "정적 내부 클래스 테스트";
		PrintOut.Out out = new PrintOut.Out();
		out.println(str);
	}
}
```

## 지역클래스(local class)
- 지역 클래스는 외부 클래스의 메서드 내에서 선언되어 사용하는 클래스이다.
- 메서드 내에서 선언되기 때문에 해당 클래스는 메서드 내에서만 사용할 수 있다.
- 메서드의 실행이 끝나면 해당 클래스도 사용이 종료된다.
```java
public class LocalClass{
	public void print(){
		///////////////////
		class A{
				지역 클래스 선언
		}

		A a = new A();	메서드 내에서 사용
		//////////////////

	}

}
```
## LocalClassExample클래스
```java
package test3;

public class LocalClassExample {
	private int speed = 10;
	
	public void getUnit(String unitName) {
		
		class Unit{
			public void move() {
				System.out.println(unitName + "이 " + speed + " 속도로 이동합니다.");
			}
		}
		
		Unit unit = new Unit();
		unit.move();
	}
	
	public static void main(String[] args) {
		LocalClassExample local = new LocalClassExample();
		local.getUnit("마린");
	}
}
```

## 내부 클래스의 접근 제한
- 내부 클래스도 클래스이기 때문에 접근 제한자를 붙여서 사용할 수 있다.

### PermitExample클래스
```java
package innerclass;

public class PermitExample {
	private class InClass{
		public void print() {
			System.out.println("접근을 private로 제한한다.");
		}
	}
	
	public InClass getInClass() {
		return new InClass();
	}
	
	public static void main(String[] args) {
		PermitExample permit = new PermitExample();
		permit.getInClass().print();
	}
}

접근을 private로 제한한다.
```

## 지역 클래스의 접근 제한
- 지역 클래스는 메서드 내에서 선언되어 사용한다.
- 보통 메서드가 종료되면 클래스도 함께 종료되지만 메서드와 실행되는 위치가 다르기 때문에 종료되지 않고 남아있을 수도 있다.
- 그래서 지역 클래스에서 메서드 내의 변수를 사용할 때는 변수를 복사해 사용한다.
- 이러한 이유로 지역 클래스에서 메서드의 변수를 사용할 때 해당 변수가 변경되면 오류가 발생한다.

### LoacalClassExample클래스 코드 추가하기
```java
package test3;

public class LocalClassExample {
	private int speed = 10;
	
	public void getUnit(String unitName) {
		unitName = unitName + " 님";
		
		class Unit{
			public void move() {
				//unitName에서 에러 발생
				System.out.println(unitName + "이 " + speed + " 속도로 이동합니다.");
			}
		}
		
		Unit unit = new Unit();
		unit.move();
	}
	
	public static void main(String[] args) {
		LocalClassExample local = new LocalClassExample();
		local.getUnit("마린");
	}
}

```
- 자바 7버전까지는 지역 클래스에서 메서드의 변수를 사용하려면 final키워드를 붙여서 사용하도록 했으나
- 자바 8버전부터는 해당 변수를 변경하지 않는다는 조건하에 effective final이라는 기능이 추가되어 키워드를 사용하지 않아도 final변수로 인정된다.

## 익명클래스(anonymous class)
- 다른 내부 클래스와는 달리 이름이 없는 클래스를 의미한다.
- 익명 클래스는 클래스의 선언과 객체의 생성을 동시에 하므로 한 번만 사용할 수 있다.
- 오직 하나의 객체만을 생성할 수 있는 일회용 클래스이다.
- 따라서 생성자를 선언할 수도 없으며, 둘 이상의 인터페이스를 구현할 수도 없다.

- Person클래스
```java
package test3;

public class Person {
	public void mySelf() {
		System.out.println("나는 인간입니다.");
	}
}
```
- Student클래스
```java
package test3;

public class Student extends Person{
	@Override
	public void mySelf() {
		System.out.println("I'm child");
	}
}
```
- PersonMain
```java
package test3;

public class PersonMain {
	public static void main(String[] args) {
		Student s = new Student();
		s.mySelf();
	}
}
```
- Person클래스를 확장하기 위해 자식 클래스를 만들어서 사용한다.
- 그런데 만약 Person을 상속받아 처리해야 하는 클래스가 또 필요하지만 한번만 사용할 거라면 굳이 상속할 필요가 없다.

### AnonymousExample클래스 생성하기
```java
package innerclass;

interface buttonClickListener{
	public void click();
}

public class AnonymousExample {

	public class Button{
		private buttonClickListener listener;
		
		public void setButtonListener(buttonClickListener listener) {
			this.listener = listener;
		}
		
		public void click() {
			if(listener != null) {
				this.listener.click();
			}
		}
		
	}
	
	public static void main(String[] args) {
		AnonymousExample exam = new AnonymousExample();
		AnonymousExample.Button button = exam.new Button();
		
		button.setButtonListener(new buttonClickListener() {
			
			@Override
			public void click() {
				System.out.println("버튼을 눌렀습니다.");
				
			}
		});
		
		button.click();
	}
}
버튼을 눌렀습니다.
```