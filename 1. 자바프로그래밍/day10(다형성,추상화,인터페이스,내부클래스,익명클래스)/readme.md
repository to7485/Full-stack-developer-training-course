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
- 프로그램의 컴파일 시점에 부모 클래스는 자신의 멤버함수밖에 접근할 수 없으나
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
## Bike클래스
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

## FourWheelBike클래스
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

## BikeMain클래스
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

# 다형성
- 다형성은 객체 지향 프로그래밍의 대표적인 특징 중 하나로, 하나의 타입으로 다양한 객체를 사용할 수 있다는것을 의미한다.
- 자바에서는 앞에서 학습한 타입 변환을 통해, 부모 클래스의 타입 하나로 여러 가지 자식 객체들을 참조하여 사용함으로써 다형성을 구현할 수 있다.
- 클래스의 타입 변환이 존재하는 이유는 다형성을 구현하기 위함이라고 할 수 있다.
- 완벽한 다형성을 구현하기 위해서는 상속 + 메서드 오버라이딩 + 클래스 타입변환 이 세가지 개념을 합쳐야 한다.
- 객체가 특정 클래스의 필드가 되면서, 하나의 부품처럼 사용될 수 있다.
- 이때, 부품을 교체할 일이 생긴다면 우리는 다형성을 구현함으로써 코드 수정을 최소화할 수 있다.

## Computer클래스
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

## Samsung클래스
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
## ComputerRoom클래스
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

## ComMain클래스
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

## LZ클래스
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

## ComputerRoom 클래스 수정하기
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

## ComMain클래스 수정하기
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
# 추상화
```java
//추상화
//공통성과 본질을 모아 추출하는것
//기존 클래스들의 공통적인 요소를 모아 상위 클래스를
//만들어내는 기술

//공통적인 속성과 행위를 모아 정의하면, 반복적인 코드를
//줄일수 있고, 보다 효과적인 클래스간의 관계를 설정하여
//유지보수가 용이해진다.
```

- 바로 전에 작성했던 FarmTest에서 메서드 오버라이딩을 이용하여 처리한 경우를 다시한번 살펴보자.
- Animal클래스의 cry()메서드가 텅 비어있는 것을 확인할 수 있다.
- Animal 객체를 통해 직접 cry()메서드를 호출할 일은 없지만,
- Animal클래스를 상속받은 자식 클래스들이 cry()메서드를 오버라이딩 하여 재정의 하고
- 타입변환을 통해서 그 메서드를 사용하기 위함이었다.

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
## 추상 클래스
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

## AbsParent클래스(abstract)
```java
abstract public class AbsParent {
	//추상메서드를 한갤라도 가지고 있는 클래스는
	//abstract키워드를 붙여 추상클래스로 정의해둬야 한다.

	int value = 100;

	//get space+cntl 누르면 완성 가능
	public int getValue(){ // 일반적인 메서드
		return value;
	}
	그동안 우리가 만들던 일반적인 메서드들과 가장 큰차이점이 뭘까요??
	// 추상 메서드는 body가 없기때문에 이를 "미완성적 개념"이라 한다.

	//추상 메서드는 body( { } )가 없다. - abstract로 시작한다.
	abstract public void setValue(int n);
	//public abstract void setValue(int n);
	
	// 그러므로 이 미완성적 개념을 자식이 물려
	// 받아서 완성 시켜야하는 것이 하나의 조건이 된다.
}
```

## AbsChild클래스 정의
```java
public class AbsChild extends AbsParent{
	
	//추상 클래스를 상속받은 자식 클래스는
	//부모가 가지고 있는 추상 메서드(미완성)를 무조건 받아두어야 한다.
	//재정의 할 필요는 없지만 오버라이딩 해서 가지고는 있어야 한다는 의미.

	//추상클래스에서 만든 메서드를 몸체까지 강제로 오버라이딩이 됨.
	//무조건 받아야 하고 자식클래스의 상황에 맞게 내용을 정의할 수 있다.

	@Override
	public void setValue(int n) {
		System.out.println("추상메서드 재정의함");
	}
```	
	
## AbsMain정의
```java
public class AbsMain {
	public static void main(String[] args) {
		//추상클래스는 인스턴스를 직접 가질 수 없다.
		//즉, 객체화 시킬 수 없다는 것.
		AbsParent ap = new AbsParent(); //오류확인 후 주석
			
		// 그러므로 추상클래스는 자신의 기능을 자식이 완성 시키도록 조건부 
		// 상속하여 자식클래스가 생성될 때 객체화된다.
		AbsChild a1 = new AbsChild();
		a1.setValue(20);
		System.out.println(a1.getValue());
	}
}
```

## AbsClass정의
```java
public abstract class AbsClass {
	int value = 100;

	public int getValue(){
		return value;
	}

	public abstract int changeValue(); // 추상메서드
}
```

## Phone 클래스
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

## PineapplePhone클래스
```java
package test2;

public class PineApplePhone extends Phone{

	@Override
	public void openingLogo() {
		System.out.println("@@@");
	}
}
```

## ThreeStarPhone클래스
```java
package test2;

public class ThreeStarPhone extends Phone{

	@Override
	public void openingLogo() {
		System.out.println("★★★");
	}
}
```

## PhoneMain클래스
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

# 인터페이스
- 모든 메서드가 추상 메서드인 일종의 추상 클래스를 '인터페이스'라고 부른다.
- 인터페이스는 추상 메서드와 상수로만 이루어져 있으며, 추상클래스와 마찬가지로 스스로 객체를 생성할 수 없다.
- 언뜻 보면 인터페이스와 추상 클래스가 같은 역할을 하는 것처럼 느껴질 수 있지만, 취지는 완전히 다르다.
- 추상 클래스는 자식클래스들의 공통적인 특징을 추출하고 제공하는것이 주된 역할이었다면
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

## Phone클래스
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

## PineApplePhone클래스
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

## ThreeStarPhone클래스
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

## Person클래스
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

## PhoneMain클래스
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
## Menu1 인터페이스 정의
```java
public interface Menu1 {
	abstract String jajang();

	//abstract는 생략되어도 interface안에서는 자동으로 추상으로 인식.
	String jjambbong();
}
```

## Menu2 인터페이스 정의
```java
public interface Menu2 {
	abstract String tangsuyuck();//탕수육 철자 모르겠다;;ㅋ
}
```

## Menu3 인터페이스 정의
```java
public interface Menu3 extends Menu1, Menu2{
	//인터페이스는 일반클래스 상속이 불가능하고 인터페이스만 상속이 가능하다.
	//인터페이스는 구현능력이 없기 때문에 다중상속이 가능하다
	abstract String boggembab();//보끔밥....
}
```

## Kitchen 클래스 생성
```java
public class Kitchen implements Menu1, /*Menu2, Menu3*/ {
	@Override
	public String jajang() {
		// TODO Auto-generated method stub
		return "중면 + 춘장 + 완두콩";
	}

	@Override
	public String jjambbong() {
		// TODO Auto-generated method stub
		return "중면 + 홍합 + 야채;
	}

	@Override
	public String tangsuyuck() {
		// TODO Auto-generated method stub
		return "돼지고기 + 당근 + 갖은양념";
	}

	@Override
	public String boggembab() {
		// TODO Auto-generated method stub
		return "춘장 + 달걀 + 쌀";
	}

}
```

## InterMain 클래스 정의
```java
package test3;

public class KitchenMain {

	public static void main(String[] args) {
		Kitchen k = new Kitchen();
		
		Menu1 im1 = k;
		Menu2 im2 = k;
		Menu3 im3 = k;
		
		//타입 변환된 각 인터페이스 내에 정의된 메서드들로 국한된다.
		
		//im1 객체에서는 jjambbong()과 jajang()만 호출할 수 있다.
		System.out.println(im1.jajang());
		System.out.println(im1.jjambbong());
		
		//im2 객체에서는 tangsuyuck()만 호출할 수 있다.
		System.out.println(im2.tangsuyuck());
		
		//im3객체에서는 boggembab()만 호출할 수 있다.
		System.out.println(im3.boggembab());

	}

}
```

# 내부 클래스
- 내부 클래스는 클래스 안에 만들어진 또 다른 클래스로 중첩 클래스라고도 부른다.
- 클래스에 다른 클래스를 선언하는 이유는 두 개의 클래스가 서로 긴밀한 관계를 맺고 있기 때문이다.

## 내부 클래스의 장점
- 두 클래스 멤버들 간에 손쉽게 접근할 수 있다.
- 불필요한 클래스를 감춰서 코드의 복잡성을 줄일 수 있다.

```java
public class OuterClass{ //외부 클래스

	class InnerClass{ //내부 클래스

	}
}
```

## 내부 클래스의 종류
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

## 인스턴스 클래스의 객체화
- 인스턴스 클래스는 기본적인 내부 클래스이다.
- 외부 클래스 안에 생성되기 때문에, 클래스를 사용하려면 외부 클래스객체가 생성된 상태에서 객체 생성을 할 수 있다.
```java
Outer outer = new Outer(); //외부 클래스 객체 생성
Outer.Inner in = Outer.new Inner(); //외부 클래스를 이용해 내부 클래스 객체 생성
```

## CalculatorExample클래스
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

## Permit클래스
```java
package test3;

public class Permit {
	private class InClass{
		public void print() {
			System.out.println("접근을 private로 제한합니다.");
		}
	}
	
	public void getInClass() {
		InClass inClass = new InClass();
		inClass.print();
	}
}
```

## PermitMain클래스
```java
package test3;

public class PermitMain {

	public static void main(String[] args) {
		Permit permit = new Permit();
		
		permit.getInClass();

	}
}
```

## 지역 클래스의 접근 제한
- 지역 클래스는 메서드 내에서 선언되어 사용한다.
- 보통 메서드가 종료되면 클래스도 함께 종료되지만 메서드와 실행되는 위치가 다르기 때문에 종료되지 않고 남아있을 수도 있다.
- 그래서 지역 클래스에서 메서드 내의 변수를 사용할 때는 변수를 복사해 사용한다.
- 이러한 이유로 지역 클래스에서 메서드의 변수를 사용할 때 해당 변수가 변경되면 오류가 발생한다.

## LoacalClassExample클래스 코드 추가하기
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

## 보통의 상속관계 처리
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

```java
package test3;

public class PersonMain {
	public static void main(String[] args) {
		Student s = new Student();
		s.mySelf();
		
		Person p2 = new Person() {
			@Override
			public void mySelf() {
				System.out.println("저는 직장인입니다.");
			}
		};
		
		p2.mySelf();
	}
}
```
- 생성자 뒤에 코드 블록{}이 추가되고, 해당 클래스가 가진 메서드들을 override하여 구현하는 방법이다.
- 해당 클래스 자체를 재정의하여 구현한다.
- 구현된 문법 마지막에는 세미콜론(;)을 붙힌다.
- 익명 클래스는 보통 인터페이스의 기능을 구현할 때 사용한다.
- 인터페이스를 상속하여 하위 클래스를 통해 구현하는 것이 아니라 인터페이스를 익명 클래스로 선언하여 기능을 직접 구현한다.

## 내부 클래스의 접근 제한
- 멤버 클래스 내부에서 외부 클래스의 필드와 메서드에 접근할 때는 제한이 따른다.
- 또한 내부 클래스의 선언 위치에 따라 생기는 제약들도 존재한다.
### 1. 접근제한자
- 내부클래스도 클래스이기 때문에 접근 제한자를 붙여서 사용할 수 있다.
- 우리가 앞에서 배웠던 접근 제한자들을 사용해 외부에서 접근을 제한할 수 있다.
```java
package test2;

public class Test {
	private class InClass{
		public void print() {
			System.out.println("접근을 private로 제한한다.");
		}
	}
	
	public InClass getInClass() {
		return new InClass();
	}

	public static void main(String[] args) {
		Test test = new Test();
		test.getInClass().print();
	}
}
//결과
//접근을 private로 제한한다.
```
- 인스턴스 클래스를 private로 선언하여 getter를 통해 클래스를 얻도록 제한을 했다.

### 2. 지역 클래스의 접근 제한
- 지역 클래스는 메서드 내에서 선언되어 사용한다.
- 보통 메서드가 종료되면 클래스도 함께 종료되지만 메서드와 실행되는 위치가 다르기 때문에 종료되지 않고 남아있을 수 있다.
- 그래서 지역 클래스에서 메서드 내의 변수를 사용할 때는 변수를 복사해사용한다.
- 이러한 이유로 지역 클래스에서 메서드의 변수를 사용할 때 해당 변수가 변경되면 오류가 발생한다.
```java
```

## AnonymousExample클래스
- 익명클래스는 다른 내부클래스와는 달리 이름이 없는 클래스를 의미한다.
- 익명클래스는 클래스의 선언과 객체의 생성을 동시에 하므로 한 번만 사용할 수 있으며 오직 하나의 객체만을 생성할 수 있는 일회용 클래스이다.
- 따라서, 생성자를 선언할 수도 없으며, 둘 이상의 인터페이스를 구현할 수도 없다.
- 오직 단 하나의 클래스를 상속받거나 단 하나의 인터페이스를 구현해야 한다.
```java
package test;

interface buttonClickListener{
	public void click();
}

public class AnonymousExample {
	
	public class Button{
		private buttonClickListener listener;
		
		public void setButtonListener(buttonClickListener listener) {
			this.listener = listener;
		}
		
		//버튼 클릭 기능
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
	}
}
```