# 열거형
- 열거형은 상수를 가지고 생성되는 객체들을 한곳에 모아둔 하나의 묶음이다.
- 상수를 사용자가 지정한 이름으로부터 0부터 순차적으로 증가시켜준다.(index값을 가진다)
- 클래스처럼 보이게 하는 상수
- 서로 관련있는 상수들끼리 모아 상수들을 정의하는것

※상수만 들어갈 수 있다.

ex1_Enum 패키지 생성

### Item enum 생성
![image](https://user-images.githubusercontent.com/54658614/221763228-0f755180-bb54-4e30-853a-acb27ede920e.png)
![image](https://user-images.githubusercontent.com/54658614/221763289-9b65b891-2087-4bb3-a2cc-c9a13d6144a2.png)

```java
package test;

public enum Item {START,STOP,EXIT}
```
### Enum클래스가 컴파일 될 때 자동 추가되는 메서드
- getDeclaringClass()
- name() : 열거형 상수의 이름을 문자열로 반환
- ordinal() : 열거형 상수가 정의된 순서를 반환
- valueof("상수명") : String값을 enum에서 가져온다 값이 없으면 Exception을 살생시킨다.
- valueof(Item.class, "START); : 넘겨받은 class에서 String을 찾아, enum에서 가져온다.
- values() : 열거형 상수안에 들어있는 내용들을 enum타입의 배열로 반환

### 열거형 데이터 비교 특징
- 열거형 상수간의 비교에는 ==을 사용할 수 있다.(상수의 주소를 비교)
- '<','>'와 같은 비교연산자는 사용할 수 없고 compareTo()는 사용이 가능하다.

#### Ex1_Enum 클래스 생성
```java
public class Ex1_Enum {

	public static void main(String[] args) {
		Item[] items = Item.values();
		System.out.println(Arrays.toString(items)); //Arrays 클래스 import
    
    //열거형 순서 반환해보기
		for(Item item : items) {
			System.out.println("name="+item.name()+",ordinal = "+item.ordinal());
		}
    
    Item i1 = Item.START;
		Item i2 = Item.valueOf("START");
		Item i3 = Item.valueOf(Item.class,"START");
		Item i4 = Item.STOP;
		System.out.println(i1 == i2);
		
    System.out.println(d1 > d4);//오류남
    
	switch(i1) {
	case START://Item.START라고 쓸 수 없다.
		System.out.println("게임시작!");
	break;
	case STOP:
		System.out.println("게임멈춤!");
	break;
	case EXIT:
		System.out.println("게임종료!");
	break;
	}

    }
}

```
열거형 클래스 안에 있는 상수에 직접 값을 입력할 수 있다.

#### Item enum클래스에 코드 추가하기
```java
public enum Item {
	START("시작",">"),STOP("멈춤","<"),EXIT("종료","V");//값을 직접 대입하면 생성자를 만들어줘야 한다.
	
	protected String itemStr;
	protected String Symbol;
	하지만 다른 클래스에서 생성자를 호출할 수 없다.
	Item(String str){ //private
	    this.itemStr = str;
	}
	
	public String getItemStr(){
		return itemStr;
	}
}


```

#### Ex2_Enum 클래스 생성하기
```java
package test;

public class Ex2_Enum {
	public static void main(String[] args) {
		
		/*
		 * Item item = new Item(); -> 생성자를 외부에서 호출하는것이 불가능하다.
		 * Item start = Item.START; 
		 * String str = start.getItemStr(); //하나만 출력하기
		 * System.out.println(str);
		 */
		
		//향상된 for문을 이용하여 열거형의 전체내용 출력하기
		Item[] items = Item.values();
		for(Item item : items) {
			System.out.println(item.getItemStr());
		}
	}
}

```

#### Item enum클래스에 코드 추가하기
```java
package test;

public enum Item {
	START("시작","s"),STOP("멈춤","p"),EXIT("종료","e");//값을 직접 대입하면 생성자를 만들어줘야 한다.
	
	protected String itemStr;
	protected String symbol;
	
	Item(String str,String sysmbol){//private
	    this.itemStr = str;
	    this.symbol = symbol;
	}
	
	public String getItemStr(){
		return itemStr;
	}
	
	public String getSymbol(){
		return symbol;
	}
}

```
#### Ex2_Enum 클래스 코드 수정하기
```java
package test;

public class Ex2_Enum {
	public static void main(String[] args) {
		
		/*하나의 상수만 출력하기
		 * Item start = Item.START; 
		 * String str = start.getItemStr();
		 * System.out.println(str);
		 */
		
		Item[] items = Item.values();
		for(Item item : items) {
			System.out.printf("메뉴 : %s, 기호 : %s\n",item.getItemStr(),item.getSymbol());
		}
	}
}
```
사실은 열거형 상수 하나하나가 객체이다.<br>
열거형을 일반적인 클래스로 만들고 상수로 정의를 한다면... 아래와 같은 결과가 된다.<br>

```java
public enum Item {
	START("시작","s"),STOP("멈춤","p"),EXIT("종료","e");
	↓↓↓↓↓↓		
public class Item {
	public static final Item START =  new ITEM("시작","s");
	public static final Item STOP =  new ITEM("멈춤","p");
	public static final Item EXIT =  new ITEM("종료","e");
		
	정적 상수로 만들어지는 정적 객체이기 때문에 메모리에 한번만 올라간다.
```

### 열거형에 추상메서드 추가하기
- 열거형에 추상 메서들르 선언하면 각 열거형 상수가 이 추상 메서드를 반드시 구현해야 한다.
- 추상클래스나 인터페이스를 가지고 추상 메서드를 구현함으로써 익명 클래스를 작성하는 것과 유사하다.

#### Transportaion 열거형 생성하기
```java
package test;

public enum Transportaion {
	BUS(100),
	TRAIN(150),
	SHIP(200),
	AIRPLANE(250);
	
	protected final int fare;
	
	Transportaion(int fare){
		this.fare = fare;
	}
	abstract int totalFare(int distance); //추상메서드를 적으면 구현을 해야 한다며 오류가 난다.
}

```
![image](https://user-images.githubusercontent.com/54658614/222339460-a50b9493-3eb5-4282-abd7-8b9588a81b96.png)

구현을 해주자

#### Transportaion 열거형 코드 추가하기
```java
package test;

public enum Transportaion {
	BUS(100){
		int totalFare(int distance){
			return distance*fare;
	}	
   },
	TRAIN(150){
	   int totalFare(int distance){
			return distance*fare;
	}	
   },
	SHIP(200){
	   int totalFare(int distance){
			return distance*fare;
	}	
   },
	AIRPLANE(250){
	   int totalFare(int distance){
			return distance*fare;
	}	
   };
	
	protected final int fare;
	
	Transportaion(int fare){
		this.fare = fare;
	}
	
	abstract int totalFare(int distance);
	//사실 추상클래스로 정의할 필요는 없긴하지만 추상클래스가 있을 때 어떻게 작성해야 하는지 보여주기 위한 예제
	//추상클래스가 들어갈 수 있다는 것은 enum도 추상클래스이다.
}

```
#### Ex3_Transportaion클래스 생성
```java
package test;

public class Ex3_Transportaion {
	public static void main(String[] args) {
		Transportaion[] trans = Transportaion.values();
		
		for(Transportaion tran : trans) {
			System.out.printf("name : %s, 100km - fare : %d\n",tran.name(),tran.totalFare(100));
		}
	}
}
```

열거형은 상수가 정적객체로 만들어진다고 보면된다.

### 어노테이션
- 프로그램의 소스코드 안에 다른 프로그램을 위한 정보를 미리 약속된 형식으로 포함시킨 것
- 어노테이션은 주석(comment)처럼 프로그래밍 언어에 영향을 미치지 않으면서도 다른 프로그램에게 유용한 정보를 제공할 수 있다는 장접이 있다.
- 어노테이션의 뜻은 주석,주해,메모이다.

```java
@Test   // 이 메서드가 테스트 대상임을 테스트 프로그램에게 알린다.
public void method() {
	....
}

'@Test'는 이 메서드를 테스트해야 한다는 것을 테스트 프로그램에게 알리는 역할을 하며, 
메서드가 포함된 프로그램 자체에는 아무런 영향을 미치지 않는다. 주석처럼 존재하지 않는 것이나 다름없다.
```

### 표준 어노테이션

|어노테이션|설명|용도|
|------|---|---|
|@Override|컴파일러에게 재정의 하는 메서드라는 것을 알린다.| 메서드명,반환값이 일치하는지 판단해서 오류를 발생시킨다.
|@Deprecated|앞으로 사용되지 않을 것을 권장하는 대상에게 붙인다.|
|@SuppressWarnings|컴파일러의 특정 경고메세지가 나타나지 않게 해준다.| 경고를 무시해준다.
|@SafeVarargs|지네릭스 타입의 가변인자에 사용한다.(JDK1.7)| (매개변수에 가변 인수를 쓸 때 발생하는 예외를 억제할 때)경고를 무시해준다.
|@FunctionalInterface|함수형 인터페이스라는 것을 알린다.(JDK1.8)| 람다식(인터페이스 - 추상메서드가 1개만 정의된 인터페이스)
|@Native|native메서드에서 참조되는 상수 앞에 붙인다.(JDK1.8)| 다른 언어로 구현된것을 자바에서 사용하려고 할 때 사용한다.
|@Target*|어노테이션이 적용 가능한 대상을 지정하는데 사용한다.|
|@Documented*|어노테이션 정보가 @javadoc으로 작성된 문서에 포함되게 한다.|
|@Inherited*|어노테이션이 하위 클래스에 상속되도록 한다.|
|@Retention*|어노테이션이 유지되는 범위를 지정하는데 사용한다.|
|@Repeatable*|어노테이션을 반복해서 적용할 수 있게 한다.(JDK1.8)|

ex1_annotaion 패키지 생성

#### Ex1_annotaion 클래스 생성

```java
//1. 표준 어노테이션
// JDK 제공
// 컴파일시에 컴파일러에게 정보제공
//@Override 컴파일러에게 재정의 하는 메서드라는 것을 알린다.
//@Deprecated 앞으로 사용되지 않을 것을 권장하는 대상에게 붙인다.
//@SuppressWarnings 경고를 무시해준다.
//@SafeVarargs (매개변수에 가변 인수를 쓸 때 발생하는 예외를 억제할 때)경고를 무시해준다.
//@FunctionalInterface 람다식(인터페이스 - 추상메서드가 1개만 정의된 인터페이스)


@FunctionalInterface -이 어노테이션을 사용하면 인터페이스에 추상메서드를 하나만 정의할 수 있다.
interface testInter{
	void method1();
	void method2();
}


public class Ex1_annotaion {
	
	public static void main(String[] args) {
		Integer num1 = new Integer(9);
	}
	
}
```

### 메타 어노테이션
- 어노테이션을 만들기 위한 어노테이션
- 스프링에서는 어노테이션으로 많이 통제한다.
- java.lang.annotaion 패키지에 정의되어 있다.

### @Target

어노테이션이 적용 가능한 대상(범위)을 지정하는데 사용된다.<br>
말 그대로 어노테이션을 붙일 수 있는 대상을 지정하는 것<br>

|어노테이션|설명|
|------|---|
|@Target(ElementType.TYPE)|클래스의 어떤 요소에나 적용 가능, 기본값|
|@Target(ElementType.FIELD)|클래스의 특정 필드|
|@Target(ElementType.METHOD)|클래스의 메서드|
|@Target(ElementType.PARAMETER)|메서드의 파라미터|
|@Target(ElementType.CONSTRUCTOR)|생성자|
|@Target(ElementType.ANNOTATION_TYPE)|어노테이션 타입|

- @Target({TYPE,FIELD, TYPE_USE,METHOD})로 여러개 사용 가능

### @Retention
어노테이션이 유지되는 기간을 지정하는데 사용된다.

|어노테이션|설명|
|------|---|
|@Retention(SOURCE)|어노테이션이 소스 코드에만 이용 가능하며 컴파일 후에는 사라짐|
|@Retention(CLASS)|어노테이션이 .class파일에 존재하지만 런타임에는 사라짐(실행시 사용 불가)|
|@Retention(RUMTIME)|어노테이션이 컴파일러와 런타임에 사용 가능(실행시에 정보 제공)|

### 어노테이션 타입 정의하기
- "@"기호를 붙이는 것을 제외하면 인터페이스를 정의하는 것과 동일하다.
- "@Override"는 어노테이션이고 'Override'는 어노테이션의 '타입'이다.

만드는방법
```java
@interface 어노테이션{

}
```
### 어노테이션 요소의 규칙
어노테이션 요소를 선언할 때 반드시 지켜야 하는 규칙
- 요소의 타입은 기본자료형,String,Enum,어노테이션,Class만 허용된다.
- ()안에 매개변수를 선언할 수 없다.
- 예외를 선언할 수 없다.
- 요소를 타입 매개변수로 정의할 수 없다.

![image](https://user-images.githubusercontent.com/54658614/223021389-e148a551-90ef-4649-a29f-2f7896ce5f69.png)

#### TestInfo 어노테이션 생성하기
```java
//2. 메타 어노테이션
// 어노테이션을 만들기 위한 어노테이션
// @Target - @Target(TYPE), @Target({TYPE, FIELD, TYPE_USE, METHOD})
// @Documented
// @Inherited
// @Retention
// @Repeatable

package test;

import static java.lang.annotation.ElementType.*;//ElementType은 열거형 -> 들어있는 것은 전부 상수
import java.lang.annotation.*;
import static java.lang.annotation.RetentionPolicy.*;//RetentionPolicy은 열거형 -> 들어있는 것은 전부 상수


@Target({TYPE,FIELD,TYPE_USE,METHOD})
@Retention(RUNTIME)
public @interface TestInfo {//앞으로 다른곳에서 @TestInfo로 어노테이션을 사용할 수 있다.
	String value();//추상메서드
}
```
#### Ex2_annotaion 클래스 생성하기
```java
package test;

import java.lang.annotation.Annotation;

@TestInfo(value="테스트 정보")//value=를 통해서 TestInfo의 value()메서드에 정보가 저장된다.
						   //value= 는 생략 가능하다.
public class Ex2_annotaion {
	public static void main(String[] args) {
		Annotation[] annos = Ex2_annotaion.class.getAnnotations();
		
		for(Annotation anno : annos) {
			System.out.println(anno);
		}
		
		TestInfo testInfo = (TestInfo)Ex2_annotaion.class.getAnnotation(TestInfo.class);
		System.out.println(testInfo.value()); //테스트 정보 출력
	}
}

```
#### TestInfo 어노테이션 수정하기
```java
package test;

import static java.lang.annotation.ElementType.*;//ElementType은 열거형 -> 들어있는 것은 전부 상수
import java.lang.annotation.*;
import static java.lang.annotation.RetentionPolicy.*;//RetentionPolicy은 열거형 -> 들어있는 것은 전부 상수

@Target({TYPE,FIELD,TYPE_USE,METHOD})
@Retention(RUNTIME)
public @interface TestInfo {
	String[] value();//배열형태로 저장이 가능하다.
}

```
#### Ex2_annotaion 클래스 코드 수정하기
```java
package test;

import java.lang.annotation.Annotation;
import java.util.Arrays;

@TestInfo({"테스트 정보","정보2","정보3"})//여러개를 쓸 때는 중괄호를 사용해야 한다.
public class Ex2_annotaion {
	public static void main(String[] args) {
		Annotation[] annos = Ex2_annotaion.class.getAnnotations();
		
		for(Annotation anno : annos) {
			System.out.println(anno);
		}
		
		TestInfo testInfo = (TestInfo)Ex2_annotaion.class.getAnnotation(TestInfo.class);
		String[] value = testInfo.value();
		System.out.println(Arrays.toString(value));
	}
}

```
#### TestInfo 어노테이션 수정하기
```java
package test;

import static java.lang.annotation.ElementType.*;//ElementType은 열거형 -> 들어있는 것은 전부 상수
import java.lang.annotation.*;
import static java.lang.annotation.RetentionPolicy.*;//RetentionPolicy은 열거형 -> 들어있는 것은 전부 상수



@Target({TYPE,FIELD,TYPE_USE,METHOD})
@Retention(RUNTIME)
public @interface TestInfo {
	String[] value()default"정보1";//아무것도 입력하지 않으면 기본값으로 "정보1"이 나오게 할 수 있다.
}
```
#### Ex2_annotaion 클래스 코드 수정하기
```java
package test;

import java.lang.annotation.Annotation;
import java.util.Arrays;

@TestInfo()//여러개를 쓸 때는 중괄호를 사용해야 한다.
public class Ex2_annotaion {
	public static void main(String[] args) {
		Annotation[] annos = Ex2_annotaion.class.getAnnotations();
		
		for(Annotation anno : annos) {
			System.out.println(anno);
		}
		
		TestInfo testInfo = (TestInfo)Ex2_annotaion.class.getAnnotation(TestInfo.class);
		String[] value = testInfo.value();
		System.out.println(Arrays.toString(value));
	}
}

```
일반적인 추상메서드 외에도 다른 타입에 대해서 알아보자.

#### TestInfo 어노테이션 수정하기
```java
package test;

import static java.lang.annotation.ElementType.*;//ElementType은 열거형 -> 들어있는 것은 전부 상수
import java.lang.annotation.*;
import static java.lang.annotation.RetentionPolicy.*;//RetentionPolicy은 열거형 -> 들어있는 것은 전부 상수



@Target({TYPE,FIELD,TYPE_USE,METHOD})
@Retention(RUNTIME)
public @interface TestInfo {
	String[] value()default"정보1";//아무것도 입력하지 않으면 기본값으로 "정보1"이 나오게 할 수 있다.
	String[] testTool()default"INFO1"; 
	String tester();
	DateTime datetime();
}
```
#### DateTime 어노테이션 생성하기
```java
package test;

import static java.lang.annotation.ElementType.*;//ElementType은 열거형 -> 들어있는 것은 전부 상수
import java.lang.annotation.*;
import static java.lang.annotation.RetentionPolicy.*;//RetentionPolicy은 열거형 -> 들어있는 것은 전부 상수

@Target(METHOD)//범위를 메서드로 제한한다.
@Retention(RUNTIME)
public @interface DateTime {
	//날짜와 시간을 저장하도록 하는 메서드 
	String date();
	String time();
}

```
#### Ex2_annotaion 코드 추가하기
```java
package test;

import java.lang.annotation.Annotation;
import java.util.Arrays;

@TestInfo(tester="이현준", datetime=@DateTime(date="20230306",time="150008"))
public class Ex2_annotaion {
	public static void main(String[] args) {
		Annotation[] annos = Ex2_annotaion.class.getAnnotations();
		
		for(Annotation anno : annos) {
			System.out.println(anno);
		}
		
		TestInfo testInfo = (TestInfo)Ex2_annotaion.class.getAnnotation(TestInfo.class);
		String[] value = testInfo.value();
		System.out.println(Arrays.toString(value));
		
		String[] tools = testInfo.testTool();
		System.out.println(Arrays.toString(tools));
		
		String tester = testInfo.tester();
		System.out.println(tester);
		
		String date = testInfo.datetime().date();
		String time = testInfo.datetime().time();
		System.out.printf("date=%s, time=%s \n",date,time);
	}
}

```
