# 상속
- 상속이란 우리가 일반적으로 알고있는 의미와 비슷하다.
- 부모가 자식에게 무언가를 물려주는 것을 상속이라고 부르는 것처럼, 자바에서도 부모 역할을 하는 클래스가
- 자식 역할을 하는 클래스에게 클래스 멤버와 메서드를 물려주는것을 상속이라고 한다
- 상속은 클래스를 재사용하기 때문에 중복을 줄여주고 수정을 최소화하는 특징을 가지고 있다.
- 상속해주는 클래스를 부모클래스, 상위클래스, 기반클래스 라고한다.
- 상속받는 클래스를 자식클래스, 하위클래스, 파생클래스 라고한다.

## ex_inheritance 패키지 생성하기
- 자바에서 상속을 구현하는 방법은 자식 클래스를 선언할 때, extends라는 키워드를 사용해 상속받을 클래스를 지명한다.
- 자식 클래스에서 선택받은 클래스는 부모 클래스 역할을 하게 된다.

### Parent 클래스 정의
```java
public class Parent {
	private int money = 2000000000; //부모의 재산
	String str = "신촌"; //부모의 부동산

변수를 private으로 만들면 자식이 사용할 수 없다.
	
}
```

### Child클래스 정의(Parent를 상속받는다)

```java
//public class Child{ 현재는 그냥 클래스 이름만 부모 자식인거지 진짜 부모자식은 아님
public class Child extends Parent{
//Child는 Parent클래스의 자식임을 명시하는 extends키워드를 사용한다.

//자바는 단일상속체제로써 하나의 자식이 여러부모를 동시에 상속(extends)받는 것은 불가능

	String car = "아반떼";	
}
```
### ExtendsMain클래스 정의

```java
public class ExtendsMain {
	public static void main(String[] args) {

		//Child클래스는 Parent클래스를 상속받은 상태이므로
		//부모로부터 상속받은 money, str등의 변수를 마음대로 가져다가
		//사용할 수 있다.
		Child c1 = new Child();
		
		System.out.println(c1.car); 
		System.out.println(c1.money); 
		System.out.println(c1.str);
    
    		//상속관계라고 할지라도 부모클래스는 자식의 재산을 마음대로 가져다가 		
		//사용할 수 없다.
		Parent p1 = new Parent();
		System.out.println(p1.money);
		System.out.println(p1.str);
   
		//c1이 Parent와 상속관계라면
		//instanceof 키워드를 통해서 true값을 얻을 수 있다.

		//c1과 Parent 클래스의 주소가 같습니까?
		if( c1 instancdof Parent) {
			System.out.println(“c1은 Parent의 자식!!”);
		}
		
}

```
부모자식 관계 객체는 자식객체가 메모리 할당이 되면 힙 영역에 놀랍게도 부모 영역이 먼저 만들어진다. 주소: 인스턴스
![image](https://user-images.githubusercontent.com/54658614/220524280-abf49bce-03d4-464c-9953-332e29942db6.png)



자식은 부모의 재산을 쓸수 있지만 부모는 자식의 재산에 손을 대는 것이 불가능하다
![image](https://user-images.githubusercontent.com/54658614/220524449-a00bc57e-8cec-43df-80eb-d126a4807b0b.png)



### 단일 상속 체제
1. 한명의 자녀가 두명의 부모를 갖는게 불가능 하다.
2. 언제 어떤 상황이 됐는 상속관계의 꼭대기에는 오브젝트가 있다.
3. 오브젝트는 모든 타입을 받아들일 수 있는 최상위 객체다.

## Animal클래스 정의
```java
public class Animal {

	private int eye = 2; //일반적인 동물들의 눈 갯수라고 가정
	private int leg = 4; //일반적인 동물들의 다리 개수라고 가정
	
	public int getEye() {
		return eye;
	}
	public int getLeg() {
		return leg;
	}
	
}
```
## Cat클래스 정의(Animal상속)
```java
public class Cat extends Animal{
	//고양이은 눈이 2개, 다리가 4개 이므로
	//eye, leg는 부모의 것을 가져다 쓰면 된다
	String balance = "균형감각이 좋다.";
}
```
## Lion클래스 정의(Animal상속)
```java
public class Lion extends Animal{
	//사자도 눈이 2개, 다리가 4개 이므로
	//eye, leg는 부모의 것을 가져다 쓰면 된다
	String galgi = "탈모걱정 ㄴㄴ";
}
```
## Snake클래스 정의(Animal상속)
```java
public class Snake extends Animal{

	String sensor = "감각이 발달";
	//오버로드는 메서드의 중복정의
	//메서드 오버라이딩: '메서드의 재정의'의 의미를 가진다.
	//상속관계의 객체에서 부모의 메서드를 자식이 가져와 사용하되
	//이름은 그대로 두고, 내용한 현재 자식클래스의 사정에 맞도록 재정의 하는 것.
	//오버라이딩 메서드는 내용을 제외하고는 부모의것과 완전히 동일해야 한다.
	//(접근제한은 부모것 보다 넓은 범위에서 변경 가능)
	@Override
	public int getLeg() {
		return 0;
	}
	
}
```
## AnimalMain클래스 정의
```java
public class AnimalMain {
	public static void main(String[] args) {
		
		Cat cat = new Cat();
		System.out.println( "---고양이---" );
		System.out.println( "눈 : " + cat.getEye() );
		System.out.println( "다리 : " + cat.getLeg() );
		System.out.println(“특징 : ” + cat.balance());
		
		Lion lion = new Lion();
		System.out.println("---사자---");
		System.out.println("눈 : " + lion.getEye());
		System.out.println("다리 : " + lion.getLeg());
		System.out.println(“특징 : ” + lion.balance());
		
		Snake snake = new Snake();
		System.out.println("---뱀---");
		System.out.println("눈 : " + snake.getEye());
		System.out.println("다리 : " + snake.getLeg());
		
	}//main
```

## 오버라이딩 예제
```java

//아주 간단한 오버라이딩 예제를 만들어 봅시다.
	
//Calculator클래스를 만들고
//getResult()함수를 정의하세요. 반환형은 정수.
//인자 두개(n1, n2)를 받고 -1로 리턴하게 만듭니다.
	
//CalPlus클래스를 만들어 Calculator클래스를 상속받으세요.
//오버라이딩을 이용하여 Calculator의 getResult()함수를
//인자로 받은 n1과 n2를 더해주는 함수로 만듭니다.
//물론 리턴값도 -1이면 안되겠죠??
	
//CalMinus클래스를 만들어 Calculator클래스를 상속받으세요.
//오버라이딩을 이용하여 Calculator의 getResult()함수를
//인자로 받은 n1과 n2를 빼주는 함수로 만듭니다.
	
//Main에서 실행하여 아래와 같은 결과가 나오면 성공
//CalPlus : 30
//CalMinus : 15

풀이
Calculator클래스 정의
public class Calculator {
	public int getResult(int n1, int n2){
		return -1;
	}
}

CalPlus클래스 정의
public class CalPlus extends Calculator{
	@Override
	public int getResult(int n1, int n2) {
		// TODO Auto-generated method stub
		return n1 + n2;
	}
}

CalMinus클래스 정의
public class CalMinus extends Calculator{
	@Override
	public int getResult(int n1, int n2) {
		// TODO Auto-generated method stub
		return n1 - n2;
	}
}

CalMain클래스 정의
public class CalMain {
	public static void main(String[] args) {
		CalPlus cp = new CalPlus();
		System.out.println("CalPlus : " + cp.getResult(10, 20));
		
		CalMinus cm = new CalMinus();
		System.out.println("CalMinus : " + cm.getResult(30, 15));
	}
}
```
# 상속에서의 생성자
- 모든 클래스는 생성자를 가진다.
- 그렇다면, 상속 관계에서 부모 클래스의 생성자와 자식 클래스의 생성자는 어떻게 사용해야 할까?

## super
- super 키워드는 부모 클래스로부터 상속받은 필드나 메소드를 자식 클래스에서 참조하는 데 사용하는 참조 변수이다.
- 부모 클래스의 멤버와 자식 클래스의 멤버 이름이 같을 경우 super 키워드를 사용하여 구별할 수 있다.

### super()
- this()가 같은 클래스의 다른 생성자를 호출할 때 사용된다면, super()메서드는 부모 클래스의 생성자를 호출할 때 사용한다.

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
## 상속과 super()를 이용한 문제
Car 클래스는 gasGauge변수를 갖고 있고, 가스잔여량을 출력하는 함수인 showCurrentGauge()를 갖고 있다.<br>

HybridCar 클래스는 electricGauge변수를 갖고 있고, Car 클래스를 상속하고 생성자를 생성할 때 gasGauge,electricGauge를 파라미터로 받는다.<br>
메서드는 오버라이딩을 이용하여 잔여 가스와 잔여 전기량을 출력<br>
	
HybridWaterCar 클래스는 waterGauge변수를 갖고 있고, HybridCar 클래스를 상속받는다.<br>
생성자 생성할 때는 gasGauge,electricGauge,waterGauge를 파라미터로 받는다.<br>
메서드 오버라이딩을 이용하여 잔여 가스와 잔여 전기량, 잔여 물량 출력<br>
	
main에서 HybridWaterCar 객체를 생성하여 다음과 같은 결과를 출력하시오.<br>

잔여 가스량 : 15<br>
잔여 전기량 : 30<br>
잔여 물량 : 25<br>

### Car 클래스 생성
```java
class Car {
	private int gasolineGauge; // 변수에 private가 붙어 다른 메소드에서 접근X
	Car(int gasolineGauge) { //생성자 오버로딩으로 파라미터를 받는다.
		this.gasolineGauge = gasolineGauge; 
	}
	// 변수 출력을 위해 해당 출력 메소드를 통해 접근
	public void showCurrentGauge() {
		System.out.println("잔여 가솔린 : " + gasolineGauge);
	
	}
}
```
### HybridCar 클래스 생성
```java
class HybridCar extends Car	{
	private int electricGauge;
	HybridCar(int gasolineGauge, int electricGauge) {
		super(gasolineGauge);
// 상위 클래스의 변수는 상위 클래스 생성자에서 초기화할 수 있도록 매개변수 전달
		this.electricGauge = electricGauge;	
	}

	public void showCurrentGauge() {
		super.showCurrentGauge();// Car 출력문 호출
		System.out.println("잔여 전기량 : " + electricGauge);
	}
}
```
### HybridWaterCar 클래스 생성
```java
class HybridWaterCar extends HybridCar {
	private int waterGauge;
	HybridWaterCar(int gasolineGauge, int electricGauge, int waterGauge) {
		super(waterGauge, electricGauge);
		this.waterGauge = waterGauge;
	}
	public void showCurrentGauge() {
		super.showCurrentGauge();
// HybridCar을 호출함으로써 상위 클래스 출력문까지 함께 출력
		System.out.println("잔여 워터량 : " + waterGauge);
	}
}
```
### CarMain 클래스 생성
```java
class Main {
	public static void main(String[] args) {
		HybridWaterCar hwc = new HybridWaterCar(15, 25, 35);
		hwc.showCurrentGauge();
	}
} 
```
[출처] [JAVA/자바] 상속 오버라이딩 예제|작성자 하늘달<br>

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
