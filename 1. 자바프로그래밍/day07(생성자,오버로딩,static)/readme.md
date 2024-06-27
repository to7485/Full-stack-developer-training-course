# 생성자
- 클래스를 구성하는 구성요소중 하나인 생성자는, 객체를 생성할 때 호출되어 객체의 초기화를 담당하는 특별한 메서드입니다.
- 객체를 생성하고 초기화하기 위해서는 반드시 생성자를 호출해야 한다.
- 따라서 객체를 생성해야 하는 참조용 클래스는 모두생성자를 가지고 있다.

## 생성자의 정의
- 생성자는 반환값이 없지만, 반환 타입을 아예 작성하지 않는다.(void로도 적지 않는다.)
- 생성자는 초기화를 위한 데이터를 인수로 전달받을 수 있다.
```java
접근제어자 클래스명 (파라미터1,파라미터2...){

}
```

## 생성자의 호출 위치
- 일반 메서드들과는 다르게, 생성자를 호출하는곳이 정해져있다.
- 생성자는 클래스를 기반으로 객체를 생성할 때, 객체의 초기화를 담당하는 역할을 하므로 객체를 생성할 때만 호출할 수 있다.

## 생성자 호출 방법
- 생성자를 호출할 때는 new 키워드를 함께 사용한다.
```java
클래스명 객체명 = new 클래스명();
```

## Ex1_Constructer패키지 생성하기
- ConTest 클래스 만들기
```java
public class ConTest {

	//생성자 : 객체가 생성될 때 메모리 할당을 위해 호출되는 영역
	//생성자는 객체가 생성될 때 처음 딱 한번만 자동으로 호출된다.

	//ConTest ct = new ConTest();

	//생성자의 특징
	//클래스와 이름이 완전히 동일하다.
	//반환형이 없다.
	public ConTest(){
		System.out.println("나는 생성자임 ㅋㅋ");
	} 	
}
```
- ConMain클래스 정의
```java
public class ConMain {
	public static void main(String[] args) {

	다른 클래스에 있는 메서드 혹은 멤버변수(ssd,cpu,ram) 쓰고싶을 때 클래스를 힙 메모리에
	할당을 받는다.
		
	ConTest ct = new ConTest(); //생성자를 호출한다는 뜻임
	//ct.ConTest(); --> 생성자를 . 찍어서 호출 불가능
	//new라고 하는 키워드는 힙이라고 하는 동네에 집을 지을 땅이 있는지 찾아보는 역할
	//실제로 집을 짓는 역할은 생성자가 함.
}
```

## 기본생성자
- 자바의 모든 클래스에는 하나 이상의 생성자가 정의되어야 있어야 한다.
- 클래스를 생성하면서 개발자가 직접 생성자를 선언하지 않았지만, 자바 컴파일러가 기본생성자를 자동으로 제공해주고 있다.
- 다만, 컴파일러의 눈에만 보일 뿐 우리가 보는 코드에는 생략되어 있다.

```java
public class ConTest {

	public ConTest(){ //기본생성자
		
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
- 메서드를 호출해서 파라미터에 값을 전달했던 것처럼, 생성자 역시 파라미터를 통해 값을 전달할 수 있다.

```java
public class ConTest {

	public ConTest(String name) {
		System.out.println("name이 " + name + "으로 초기화 됨");
	} 
	
	
}
```

```java
public class ConMain {
	public static void main(String[] args) {
		
	ConTest ct = new ConTest("홍길동");

}
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
	pbulic Person() {
		age = 40;
		name = "노태문";
	}

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

# 오버로딩
- 오버로딩(Overloading)이라는 뜻은 사전적으로 '과적하다.'라는 뜻이다.
- 자바에서는 하나의 메소드 이름으로 여러 기능을 구현하기 때문에 '과적하다.'라는 뜻의 이름을 붙여준 것으로 보인다.
- 자바의 한 클래스 내에 이미 사용하려는 이름과 같은 이름을 가진 메소드가 있더라도 매개변수의 개수 또는 타입이 다르면, 같은 이름을 사용해서 메소드를 정의할 수 있다.

## 오버로딩의 조건
1. 메서드의 이름이 같아야 한다.
2. 파라미터의 개수가 달라야 한다.
3. 파라미터의 개수가 같아도 타입이 달라야 한다
4. 파라미터의 개수가 같아도 순서가 달라야 한다

## 생성자에 전달할 파라미터가 부족하면 어떤일이 일어날까?
- Phone 클래스
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
- PhoneMain클래스
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

- Phone클래스에 color가 없는 생성자 만들기
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
- Book 클래스
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
- BookMain클래스
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
public class Ex1_Overload {
  
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
public class Ex2_OverloadingMain {
	public static void main(String[] args) {

	Ex1_Overload ov = new Ex1_Overload();
	ov.result();
	ov.result(10);
	ov.result('A'); //인자를 char로 받으면 65를 넣어도 'A'가 출력되긴함.
	ov.result("hi",10);
	ov.result(10,"hi");

	여러분들이 지금까지 수업을 듣는동안 알게모르게 오버로드메서드가 있다.

	System.out.printString("안녕하세요");
	System.out.printInt(10 + 15);

	오버로드의 장점 메서드를 상황에 따라서 구분할 필요가 없음 예를들어서 그냥 print를 쓰면됨
  }
}
```

## 메서드 오버로드 문제
```java
Method클래스를 만들어 각기 다른 기능을 하는 makeBread()메서드를 세 개만드는데,
메인클래스에서 각각의 메서드를 호출했을때의 결과를 보고 로직을 구현해 보자.

//빵을 만들었습니다 <-------------- method 1을 호출해서 나온 결과
//------------------
		
//빵을 만들었습니다 <-------------- method 2을 호출해서 나온 결과
//빵을 만들었습니다.
//요청하신 n개의 빵을 만들었습니다.
//---------------------

//크림빵을 만들었습니다 <-------------- method 3을 호출해서 나온 결과
//크림빵을 만들었습니다.
//요청하신 n개의 빵을 만들었습니다.

Method클래스 생성. 오버로드 메서드 정의
public class Method {
	
	void makeBread()
	{
		System.out.println("빵을 만들었습니다.");
	}

	void makeBread(int count)
	{
		for(int i = 0; i < count; i++)
			System.out.println("빵을 만들었습니다.");
		System.out.println("요청하신 " + count + "개의 빵을 완성했습니다.");
	}

	void makeBread(int count, String name)
	{
		for(int i = 0; i < count; i++)
			System.out.println(name + "을 만들었습니다.");
		System.out.println("요청하신 " + count + "개의 " + name + "을 완성했습니다.");
	}
}
```

- 오버로드을 위한 메인클래스 생성

```java
public class MethodMain {
	public static void main(String[] args) {

		Method mh = new Method();
		Scanner sc = new Scanner(System.in);
		
		mh.makeBread(); //예제1
		System.out.println("-------------------------------");
		
		System.out.print("만들고 싶은 빵의 개수: ");
		int num = sc.nextInt();
		mh.makeBread(num); //예제2
		System.out.println("-------------------------------");
		
		System.out.print("만들고 싶은 빵의 개수: ");
		int num = sc.nextInt();
		System.out.print("만들고 싶은 빵의 종류: ");
		String b = sc.next();
		mh.makeBread(num, b);//예제3
	}
}
	
```

# static변수
- 변수가 static으로 선언되면 객체를 생성하지 않고도 사용할 수 있다.
- static변수를 가지는 객체를 아무리 많이 생성한다고 해도 static변수는 오직 하나만 만들어 진다.

## static변수를 사용해서 은행 이자율을 관리해보자.
- Bank클래스 정의
```java
public class Bank {
	//static : 객체가 아무리 많이 생성되어도
	//메모리상에 딱 한 개만 만들어지는 변수나 메서드
	private String name = "우리은행";
	private String point; //은행 위치
	private String tel; //은행 전번
	static float interest = 10f; //은행이자
	
	//생성자 써먹어보자(생성자를 setter처럼 사용)
	public Bank(String point, String tel) {
		this.point = point;
		this.tel = tel;
	}
	
	//결과를 출력할 메서드
	public void printBank(){
		System.out.println("이름 : " + name);
		System.out.println("위치 : " + point);
		System.out.println("전화번호 : " + tel);  
		System.out.println("이자율 : " + interest + "%");
		System.out.println("-----------------------");
	}
}
```
- BackMain 클래스 정의

```java
public class BankMain {
	public static void main(String[] args) {
		
		Bank bk1 = new Bank("강남", "02-111-2222");
		Bank bk2 = new Bank("분당", "031-333-4444");
		Bank bk3 = new Bank("대전", "042-333-3333");

		//static 변수 클래스 이름으로 접근하는게 보통의 방식이다.
		//객체 생성 없이도 언제든 가져다가 사용할 수 있다.
		Bank.interest = 0.1f;
	
		bk1.printBank();
		bk2.printBank();
		bk3.printBank();	
					
	}
}
```
