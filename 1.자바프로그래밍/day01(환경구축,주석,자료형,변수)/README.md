# 실습 환경 구축하기

## 내 PC에 실습을 위한 폴더 만들기
내 PC -> D드라이브 진입 -> JAVA1900_이니셜 -> 안에 util,work 폴더만들기

![image](https://user-images.githubusercontent.com/54658614/211975967-b510f6c6-1f98-4372-b52c-65c6ed39bb6e.png)


## 자바란?
- 썬 마이크로시스템즈 소속 제임스고슬링 등의 일부 연구진들은 '그린프로젝트'라는 이름으로 '오크(Oak)'라는 언어를 개발하고 있었다.
- 오크는 오디오,tv,세탁기 등 각각의 가전제품을 제어하는 통합된 언어로써 개발중이었지만 결국 목적을 달성하지 못하고 실패로 돌아간다.
- 그 무렵 웹(www)이 급속도로 발전하게 되고, 이에 발맞추고자 썬에서는 오크의 명칭을 Java로 바꾼뒤 서로 다른 컴퓨터(OS - 운영체제)사이에서 호환성과 이식률을 높인 언어로 발전시켰다.


## 자바 설치하기
- 자바로 프로그램을 개발하고 실행하려면 자바가상머신(JVM)이 필요하다.
- 자바가상머신은 자바 개발 키트(Java Development Kit) 또는 자바 실행 환경(Java Runtime Environment)을 설치하면 자동으로 설치된다.

https://www.oracle.com/java/technologies/downloads

### JVM
- 자바 가상 머신(Java Virtual Machine)은 자바 프로그램 실행환경을 만들어주는 소프트웨어입니다.
- 자바 코드를 컴파일 하여 바이트 코드로 만들면 이 코드가 자바 가상 머신 환경에서 실행됩니다.
- JVM은 자바 실행 환경 JRE(Java Runtime Environment)에 포함되어 있습니다.
- 현재 사용하는 컴퓨터의 운영체제에 맞는 자바 실행환경(JRE)가 설치되어 있다면 자바 가상 머신이 설치되어 있다는 뜻입니다.

### JRE(Java Runtime Environment)
- JVM과 자바 프로그램을 실행시킬 때 필요한 라이브러리 API를 함께 묶어서 배포되는 패키지이다.
- JRE는 기본적으로 JDK에 포함되어 있기 때문에 JDK를 설치하면 함께 설치된다.

## 환경 변수 설정
- 환경 변수 : 프로그램이 컴퓨터에서 동작하는 방식에 영향을 미치는 동적인 값들의 모임
- [내PC] - [속성]을 선택하고 [시스템] - [고급 시스템 설정]을 클릭한다. 이어서[시스템 속성] 창에서 [환경 변수]를 클릭한다.

![image](img/환경변수1.png)

![image](img/환경변수2.png)

- [시스템 변수]에서 [새로 만들기]를 클릭한다. 변수 이름에 'JAVA_HOME', 변수값에는 자바를 설치한 경로를 찾아주고 확인 버튼을 클릭한다.

![image](img/환경변수3.png)

- [시스템 변수]에서 [Path] 환경 변수를 선택하고 [편집]을 클릭한다. 이어서 [새로 만들기]를 클릭한 후 '%JAVA_HOME%\bin'을 입력하고 [확인]버튼을 누른다.

![image](img/환경변수4.png)

![image](img/환경변수5.png)

## 자바가 잘 설치되어있는지 확인하는법

win + r -> 실행창에 cmd -> java -verion 입력

![image](https://user-images.githubusercontent.com/54658614/211975334-e2287139-5269-4218-8dd0-1167fd62eea4.png)


### 자바의 버전을 보면 많다 어떤 버전을 사용하는것이 좋은가??
- 기업에서 이미 운영하고 있는 프로젝트들이 있을 것이다. 
- 이미 만들어진 프로젝트의 경우 Java8버전이 많을 수 있다.
- 프로젝트를 새로 시작하는 경우 Java11, Java17을 사용할 수 있다.

### LTS(LongTimeService)
- 장기간 안정적인 지원을 받을 수 있는 버전
- 실무에서는 LTS버전을 선호하는 경향이 있다.
- 보안 패치와 성능 개선을 지속적으로 받을 수 있다는 장점이 있기 때문이다.

### 특정 자바 버전을 학습 해야 할까???
- 12,17과 같은 특정 Java버전만을 "학습"할 필요는 없다.
- 자바는 하위호환성이 매우 높기 때문이다.

## 자바의 특징
### 객체 지향 언어
- 하나의 기능을 객체로 만들고, 이러한 객체들을 결합해서 하나의 프로그램을 완성하는 기법을 말한다.
- 자바는 대표적인 객체 지향 언어로 상속, 캡슐화, 다형성이 잘 나타난다.

### 단순성
- C/C++을 기반으로 개발되었지만, C/C++에서 제공하는 문법인 포인터 등 혼란을 일으키는 불필요한 기능들을 제거했다.

### 이식성
- 한번만 작성해놓으면 운영체제의 종류와 상관없이 실행할 수 있다.

![image](https://user-images.githubusercontent.com/54658614/211973993-8e9d86f8-5251-48b8-9e10-4567dde3ef49.png)

### 메모리 자동 정리
- 자바는 자동으로 가비지 컬렉터(GC: Garbage Collector)가 사용하지 않는 메모리를 주기적으로 수거하고 관리한다.

### 풍부한 오픈소스 라이브러리
- 자바는 무료로 제공하는 라이브러리가 많이 개발되어 있어 프로그램 개발 기간을 단축할 수 있으며 안전성 높은 프로그램을 개발할 수 있다.

## 통합 개발환경
통합 개발 환경(統合開發環境, Integrated Development Environment, IDE)은 코딩, 디버그, 컴파일, 배포 등 프로그램 개발에 관련된 모든 작업을 하나의 프로그램 안에서 처리하는 환경을 제공하는 소프트웨어이다.

### 대중적인 IDE
- 이클립스(Eclipse) : 웹, Java, C, C++
- Visual Studio : C, C++, C#, Python
- Intellij : Java, C/C++
등등 많은 IDE가 있다.

## 이클립스 설치하기
- 이클립스 홈페이지 : https://www.eclipse.org/

- 홈페이지에 접속하여 다운로드 버튼을 누른다.
![image](img/이클립스설치1.png)

- 다운로드 버튼 아래 Download Packages를 누른다.
![image](img/이클립스설치2.png)

- 오른쪽에서 다른 버전을 고를 수 있다.
- 버전을 골랐다면 Eclipse IDE for Java and Web Developers버전을 다운로드받아야 한다.
- 본인이 사용하고 있는 컴퓨터의 운영체제와 맞는 버전을 다운로드 한다.
![image](img/이클립스설치3.png)

- 다운로드 받은 압축 파일을 util폴더로 옮기고 압축을 푼다.


## 이클립스 실행해보기
```diff
- ※ jdk를 먼저 설치하지 않으면 이클립스가 실행되지 않습니다!!
```
- 이클립스를 켜고 Browse를 눌러 우리가 만들어 놓은 work 폴더로 경로를 잡아주자.
- 앞으로 우리가 작업하는 프로젝트들은 work폴더에 저장될 것이다.

![image](https://user-images.githubusercontent.com/54658614/211976280-0159d649-c5d5-47c3-840a-09f4e37d4e24.png)

## 이클립스 프로그램 구성

![image](https://user-images.githubusercontent.com/54658614/212237771-1da23aee-2b7b-4d49-9692-e1b87980a835.png)

## 자바 프로젝트 생성하기
![image](https://user-images.githubusercontent.com/54658614/212238723-e89acb35-1605-4a1b-8e9f-716fd097cc81.png)

![image](https://user-images.githubusercontent.com/54658614/212238789-2ef70972-6e66-432e-9380-159f46f01526.png)

![image](https://user-images.githubusercontent.com/54658614/212238858-e61b8d78-c9a4-45ee-9480-ad523f1589ad.png)

![image](https://user-images.githubusercontent.com/54658614/212238952-7869b3bd-a2ea-4eeb-a94a-5081bedc8ecc.png)

## 폴더에 해당하는 패키지 생성하기

![image](https://user-images.githubusercontent.com/54658614/212239071-7dea18ab-2129-470a-b383-ae8a81c6a9d6.png)

### 패키지 이름을 적고 finish를 누릅니다.
- section01 이라는 이름으로 패키지를 만들어보자

![image](https://user-images.githubusercontent.com/54658614/212239347-bc640c8d-266a-4e4a-b1cf-6ca13aad557b.png)

### 그러면 비어있는 패키지가 생성되게 됩니다.

![image](https://user-images.githubusercontent.com/54658614/212239455-3f18af92-83b4-4f2f-8c43-276e56506204.png)

## 코드를 작성하는 공간인 클래스 생성하기

![image](https://user-images.githubusercontent.com/54658614/212239571-0380fc1a-b15c-4f17-aacd-036e5e6d9b05.png)

### 클래스명 작성하기
- 클래스를 작성할 때 클래스의 이름의 첫번째 글자는 반드시 대문자로 작성해야 합니다.
- Hello라는 이름으로 클래스를 생성해보자.

![image](https://user-images.githubusercontent.com/54658614/212239611-d741c393-40b5-430b-8b43-3b8e62956724.png)

![image](https://user-images.githubusercontent.com/54658614/212239789-91e1818d-fb55-4fba-83b5-c727a4cbae4c.png)

### 클래스 내용 작성하기
- 클래스를 작성하면 항상 main이라고 하는걸 작성해주자 지금 당장은 뭔지 모르겠지만 자바가 실행될 때 main 영역 안에 있는 코드가 실행된다.

```java
public class Test {
	public static void main(String[] args) {
		
	}
}
```
### System.out.println("hello world"); 작성해보기
- main의 영역 안에 System.out.println("hello world");라고 적어보자
- 항상 명령이 끝난 뒤에는 세미콜론(;)를 붙혀야 한다.
- 세미콜론(;)이 나올 때 까지 한 문장의 실행문으로 인식하기 때문이다.
- 실행을 하기 전에는 ctrl + s를 눌러 꼭 저장을 해주도록 합시다!

```java
public class Test {
	public static void main(String[] args) {
		System.out.println("hello world");
	}
}
```

- 실행단추 Run을 클릭하거나 Ctrl + f11을 누르면 작성한 프로그램을 실행할 수 있다.

![image](https://user-images.githubusercontent.com/54658614/212241733-b89dbf5a-ae42-4ebd-b28c-53d89afbc2af.png)

### 디버깅(오류 수정하기)
- 프로그래밍 도중 오류가 발생하면 소스 코드 아래 빨간 밑줄이 나타난다.
- 빨간 밑줄이 표시된 부분에 마우스를 가져가면 오류 원인을 확인할 수 있다.

![image](img/디버깅1.png)

# 자바 프로그램의 실행 프로세스
- 자바 언어로 만들어진 파일을 컴파일 하면서 기계어 파일인 바이트코드(.class)파일이 생성된다.
- 이후 바이트코드를 JVM이 읽고 실행하게 된다.

![image](img/자바프로세스1.png)

## 자바 바이트코드
- 우리가 프로그래밍 언어로 명령을 한다고 해서 컴퓨터가 알아들을수는 없다.
- 프로그래밍 언어를 1과0으로 이루어진 바이트코드로 변환을 해주는 작업을 거쳐야 한다.
- 코드의 명령어 크기가 1바이트라서 자바 바이트 코드라고 불리고 있습니다.
- 이러한 자바 바이트 코드의 확장자는 .class입니다.
- JVM만 설치되어 있으면, 어떤 운영체제에서라도 실행될 수 있습니다.

## 컴파일(Compile)
- 프로그래머가 작성한 .java 코드(자바코드)를 .class 코드(바이트 코드)로 바꾸는 일련의 과정
### 자바 컴파일러(Java Compiler)
- 자바 소스 파일을 JVM이  해석할 수 있는 자바 바이트코드(.class)파일로 번역한다.

## 자바 프로그램의 기본 구조
```JAVA
//class : 클래스를 정의하는 키워드
//Hello : 클래스 이름
public class Hello{
	//main : 메서드 이름
	public static void main(String[] args){
		System.out.println("Hello JAVA!!"); //실행문
	}
}
```

### 클래스
- 자바에서 프로그램을 개발하는 단위이다.
- 하나 이상의 클래스가 있어야 하며 소스 파일의 이름이 클래스의 이름과 동일해야 한다.

### 메서드
- 수행할 작업을 나열한 코드의 모음
- 자바 프로그램의 시작 위치인 main()메서드를 포함하는 클래스가 반드시 있어야 한다.

### 실행문
- 작업을 지시하는 것으로 변수나 상수의 선언, 값 저장, 메서드 호출 등 다양한 명령어와 연산자로 구성된다.

## 주석
- 프로그램의 소스코드에 프로그래머의 의견이나 설명을 적을 수 있는데 이런 것을 주석(Comment)라고 합니다.
- 주석은 프로그램 소스에 삽입하더라도 프로그램의 수행에 전혀 영향을 끼치지 않습니다.
- 컴퓨터(JVM)에서 컴파일을 할 시 인식하지 못하는 코드이기 때문입니다.
- 주석으로 코드를 잘 설명해놓으면 오류를 찾거나 복잡한 코드를 이해하기 쉽고 다른 개발자가 코드를 해석하는데 도움이 된다.

### 주석의 종류
#### // (행주석)
- //부터 그 줄의 끝까지 주석으로 처리, 주석 내용이 한줄일 때 사용
#### /* \*/ (범위 주석)
-  /* 와 */ 사이의 내용을 모두 주석으로 처리, 여러 줄의 주석이 필요할 때 사용

```java
public class Test {
	public static void main(String[] args) {
	    //한줄 주석 : //
	    /*
	    여
	    러
	    줄
	    주
	    석
	    */
	    //주석을 사용하는 이유 : 코드에 설명을 달아주기 위해
	    //sysout 적고 ctrl + spacebar 자동완성
		System.out.println("hello world");
	}
}
```

#### // TODO
- 아직 해결되지 않은 작업이나 구현해야할 부분을 나타내는 주석 태그
```java
// TODO : 추후에 하드코딩을 개선해야 합니다.
```

#### //FIXME
- 수정이 필요한 버그, 오류, 또는 잘못된 동작을 나타내는 주석 태그
- FIXME 주석 태그를 포함하고 어떤 문제가 있는지 설명하고 이를 해결해야 하는 이유를 기록한다.
- 코드나 문서를 검토할 때 빠른 수정이 필요한 부분을 강조하는데 사용된다.
```java
// FIXME : 해당 코드에서는 런타임 오류가 발생합니다. 수정해야 합니다.!
```

#### //XXX
- 다른 개발자가 알아봐야 할 중요한 이슈 또는 경고를 나타내는 주석 태그를 의미
- XXX와 함께 어떤 문제가 있는지 설명하고 이를 처리해야 하는 이유를 기록한다.
- 코드나 문서를 검토할 때 주의해야 할 부분을 강조하는데 사용되며 주로 버그 또는 잠재적인 문제를 가리키는 데 사용되며 개선이 필요한 부분을 의미한다.
```java
// XXX : 해당 부분이 하드코딩 된 것 같습니다. 수정해야 합니다.
```

![image](img/주석1.png)

#### /** 주석문 */
- 줄 수 와 상관없이 /** 시작과 */ 사이의 내용을 모두 주석으로 간주한다. 이 주석은 소스를 라이브러리로 만들 때 공식 문서용으로 뽑아 사용할 수 있다. javadoc 시스템을 사용하여 API 문서나 도움말 등에 이용된다.

# 프로그램의 구성
- 컴퓨터 프로그램은 데이터(data)와 명령어(instruction)의 결합으로 구성된다.

## 데이터
- 실제적인 값을 의미한다.
- 숫자,문자와 같은 단순한 데이터부터 사진,영상등의 복합적인 데이터가 있다.
- 데이터는 언제든지 수정할 수 있어야 하며, 사용목적에 따라 다른 형태로 가공할 수 있어야 한다.
- 이러한 데이터는 컴퓨터의 메모리에 저장된다.

## 데이터의 출력
```java
System.out.print() : 괄호안의 내용을 출력한다.
System.out.println() : 괄호안의 내용을 출력하고 줄을 바꿔준다(개행)
```
- System.out.print(),System.out.println() 출력문은 모든 데이터를 문자열로 인식하여 있는 그대로 출력하는 메서드이다.

### System.out.print()
```java
package test;

public class Test{
	public static void main(String[] args) {
		//괄호()안의 데이터를 콘솔창에 출력
		System.out.print("Welcome");
		//"Welcome"문자열 옆에 "Java World"문자열 출력
		System.out.print("Java World");
	}
}
```
### System.out.println()
```java
package test;

public class Test{
	public static void main(String[] args) {
		//괄호()안의 데이터를 콘솔창에 출력
		System.out.println("Welcome");
		//"Welcome"문자열 아래 "Java World"문자열 출력
		System.out.println("Java World");
	}
}
```

### System.out.printf() 
```java
System.out.printf()
```
- System.out.printf() 출력문은 값의 자료형에 따라 서식문자를 이용해 문자열속에서 데이터를 출력할 수 있다.

|서식문자|출력형태|
|-----|------|
|%d|정수(10진수)|
|%o|정수(8진수)|
|%x|정수(16진수)|
|%f|실수|
|%s|문자열|
|%c|문자형|
|%b|논리형|

### Printf01 클래스 생성하기
```java
package test;

public class Printf01{
	public static void main(String[] args) {
		System.out.printf("저는 대학교 %d학년에 재학중입니다.",3);
		
		//서식문자를 한번에 여러개를 넣을 수 있다.
		System.out.printf("%d은 첫 번째, %f은 두 번째, %s은 세 번째.",1,2.0,"셋");
	}
}
```
### 출력값의 정렬
- 정수의 정렬
```java
%3d, %5d //주어진 숫자 칸 만큼 확보한후, 오른쪽 정렬하여 출력
예) (%5d,1) -> XXXX1

System.out.printf("%5d",1);
System.out.println();
System.out.printf("%5d",12);
System.out.println();
System.out.printf("%5d",123);
System.out.println();
System.out.printf("%5d",1234);
System.out.println();
System.out.printf("%5d",12345);
System.out.println();
```
- 실수의 정렬

```java
%.2f //소수점 아래 정수번째 자리까지 출력(반올림)

System.out.printf("%.1f",1.1234567);
System.out.println();
System.out.printf("%.2f",1.1234567);
System.out.println();
System.out.printf("%.3f",1.1234567);
System.out.println();
System.out.printf("%.4f",1.1234567);
System.out.println();
System.out.printf("%.5f",1.1234567);
```
# 자료형(기본자료형)
- 현실에서는 물을 종이컵에다 마시든, 플라스틱 컵에다 마시든, 유리컵에다 마시든 전혀 문제가 되지 않습니다.
- 하지만 프로그래밍에서는 '물은 종이컵에 담아먹겠다' 라고 약속을 했으면 무조건 지켜야 합니다.
- 프로그래밍에서 자료형이라고 하는거는 데이터를 담을 컵의 크기와 재질이라고 비유를 들 수 있습니다.
- 자료형(data type)은 자바가 처리할 수 있는 데이터의 종류를 의미한다.

## 기본자료형
- 실제 데이터 값을 저장할 수 있게 해줍니다. 정수,실수,문자,논리 타입으로 분류된 8개의 자료형이 존재한다.
- 각 타입에 저장되는 값의 허용 범위를 모두 외울 필요는 없지만 메모리 할당 크기는 알고있는것이 좋다.

|자료형|키워드|메모리 크기|표현 범위|
|------|------|----------|-----------|
|논리형|boolean|1bit|true, false(기본값 false)|
|문자형|char|2byte|기본값 \u0000 or 0|
|정수형|byte<br>short<br>int<br>long<br> |1byte<br>2byte<br>4byte<br>8byte |-128 ~ 127<br>-32,768 ~ 32,767<br>-21,4748,3648 ~ 21,4748,3647<br>-9,223,372,036,854,775,808 ~ (900경)|
|실수형|float<br>double<br>|4byte<br>8byte<br>|기본값 0.0|

### 주의점
- 정수의 경우 해당 자료형이 표현할 수 있는 범위를 벗어난 데이터를 저장하면, 오버플로우(overflow)가 발생해 전혀 다른 값이 저장될 수 있다.

#### 오버플로우 / 언더플로우
- 오버플로우는 해당 자료형이 표현할 수 있는 최대 범위보다 큰 수를 저장할 때 발생하는 현상으로 잘못된 결과를 얻을 수 있다.
- 언더플로우는 해당 자료형이 표현할 수 있는 최소 범위보다 작은 수를 저장할 때 발생하는 현상이다.

## 참조자료형
- 하나의 기본 자료형으로는 표현할 수 없는 것들을 표현할 때 사용하는 자료형
- 개발자가 직접 추가하여 사용할 수 도 있기 때문에 개수가 정해져 있지 않다.
- 대표적으로는 String이라는 문자열을 저장할 수 있는 참조 자료형이 있다.
- char는 문자 하나를 저장하는 기본 자료형이고, 우리는 문자들의 조합을 문장 즉, 문자열이라고 표현한다.

|자료형|키워드|
|------|------|
|문자열|String|

## 여러가지 형태의 데이터 출력해보기

```java
public class Test {
	public static void main(String[] args) {
		    //한줄 주석 : //
		    /*
		    여
		    러
		    줄
		    주
		    석
		    */
		    //주석을 사용하는 이유 : 코드에 설명을 달아주기 위해
		    //sysout 적고 ctrl + spacebar 자동완성
		System.out.println("hello world");
		System.out.println(100);
		System.out.println(100+50);
		
		//문장뒤에 숫자를 더하면 문장 뒤에 붙는구나
		System.out.println("안녕하세요"+10);
		
		//코드는 항상 위에서 아래로, 좌에서 우로 진행이 되기 때문에 15:15가 나옵니다.
		System.out.println(5+10+":"+(5+10));
		
		// "2 + 2 = "가 숫자 처럼 보이지만 ""안에 묶여있으면 문장 취급을 받고
		//문장에 숫자를 더했기 때문에 22가 됩니다.
		System.out.println("2 + 2 = " + 2 + 2);
		System.out.println("2 + 2 = " + (2 + 2));	 
	}
}
```

# 변수
- 자료형이 데이터를 담기 위한 컵의 재질과 크기라면
- 변수는 데이터를 실제로 담기 위한 컵을 만드는 과정 이라고 생각하시면 됩니다.

## 변수의 선언

1. 변수를 선언하고 값을 대입하는 법 (컵을 만든 후 물을 따르는법)
```java
자료형 변수명; -> 변수의 선언
변수명 = 값; -> 변수의 대입
대입을 할 때는 앞에 자료형을 명시할 필요가 없다.
```
2. 변수를 만듦과 동시에 값을 넣는법
```java
자료형 변수명 = 값;
변수의 초기화(초기화 라고 함은 reset의 개념이 아닌 초기값을 지정한다는 의미)
```

## 변수명 명명 규칙
1. 숫자가 먼저 들어가면 안된다.
2. 영어 대소문자를 구분한다(Name과 name은 다른 변수라고 인식한다)
3. 일반적으로 영어소문자로 시작한다.
4. _를 제외하고 특수기호가 포함될 수 없다.
5. 예약어 금지(switch, while 등)
6. 한글은 사용하지 말 것.

## 표기법
- 변수명은 문자 수의 제한 이 없으므로 최대한 변수의 의미를 쉽게 파악할 수 있도록 구체적으로 명명하는 것이 좋다.

### 카멜 표기법(camel case)
- 두번째 단어부터 첫글자를 대문자료 표기하는 방법
- 마치 낙타의 등처럼 올라갔다 내려갔다 하는 모양이라 붙혀진 이름
```java
userName
phoneNumber
```

### 스네이크 표기법(snake case)
- 모든 단어가 소문자로 시작하고, 단어와 단어 사이는( _ ) 로 연결하는 방식
```java
user_name
phone_number
```
## 변수로 데이터 불러오기
- 개발자가 데이터 값이 필요할 때 데이터의 값을 직접 쓰는 대신
- 데이터를 변수에 저장해두고 변수의 이름을 불러서 그 값을 사용할 수 있게 해준다.


### 변수 만들기 실습
```java
-------------------------------------------------------------------------------
논리형
논리형은 true, false 즉, 사실이다와 사실이 아니다의 두 가지 값만을 가진다.
boolean b = true;
System.out.println("b의 값 : " + b); //+기호는 더한다는 의미가 아닌 이어붙인다의 의미.
//단, 숫자 사이의 + 기호는 더하기를 의미.
boolean b = 1;//자료형의 값이 올바르지 않아 오류
-------------------------------------------------------------------------------

문자형
char ch = 'A'; //문자형은 홑따옴표 안에 넣어야 하며 한글자이상 넣을 수 없다.
System.out.println("ch = " + ch); //결과 : A

char ch3 = 65 + 1; //아스키코드 65에 + 1
System.out.println("ch3 = " + ch3); //결과 : B


-------------------------------------------------------------------------------

정수형
//byte b = 128; byte자료형의 표현범위를 벗어나므로 오류가 난다.

byte b1 = 127;
short s = 32767;
int n = 550;

System.out.println("b1 = " + b1); //결과 127
System.out.println("s = " + s); //결과 32767
System.out.println("n = " + n); //결과 550
-------------------------------------------------------------------------------
실수형(소수)
//float f = 3.14;
//java에서 실수는 기본적으로 double형으로 인식하기 때문에 float자료형을 사용한다는 것을 명시해줘야 한다. (3.14f)

float f1, f2;
f1 = 3.14f;

System.out.println("f1 = " + f1); //결과 3.14 
System.out.println("f2 = " + f2); //결과 150.0
-------------------------------------------------------------------------------
int myAge = 20; //myAge에 20을 저장
int yourAge = myAge; //myAge에 저장된 20이 복사되어 yourAge에 저장된다.

-------------------------------------------------------------------------------
//두 변수에 들어있는 값을 바꾸려면 어떻게 해야할까??
int su1 = 20;
int su2 = 30;

System.out.println("변경전");
System.out.println("su1 : " + su1);
System.out.println("su2 : " + su2);

//컵 두개에 들어있는 내용물을 서로 교환한다고 생각을 해보자.
//컵 두개로는 서로 바꾸는게 불가능하다.
//내용물을 임시로 담아놓을 컵이 하나 필요하다.
int temp;
temp = su1;
su1 = su2;
su2 = temp;

System.out.println("변경후");
System.out.println("su1 : " + su1);
System.out.println("su2 : " + su2);

```
# 형변환
- 자료형을 다른 자료형으로 변환하는 것을 말한다.
- 모든 연산은 기본적으로 같은 자료형들끼리만 수행할 수 있다.
- 따라서 서로 다른 자료형의 연산을 수행하기 위해서는 같은 자료형으로 변환해야 한다.

### Casting01 클래스 생성하기
```java
public class Casting01{
	public static void main(String[] args){
		int num = 11;
		double num2 = 3.14;
		double num1Change = (double)num1;

		System.out.println("num1 : " + num1);
		System.out.println("num1Change : " + num1Change);
		System.out.println((int)1.23);
	}
}
```

## Promotion(자동형변환)
- 작은 자료형에서 큰 자료형으로 변환할 때
    - byte -> short -> int -> long
- 정수형이 실수형으로 변환 될 때

```java
   double d = 100.5; //8byte
   int n = 200; //4byte
   d = n;
   System.out.println("d = " + d); //결과 : 200.0

   char c = 'A'; //2byte
   long l = 100;//8byte
   l = c;
   System.out.println("l = " + l); //결과 65
```

## Demotion(강제형변환)
- 큰 컵의 물을 작은 컵에 옮겨 담는것과 같다.
- 물의 양에 따라서 보존될 수도 있지만 넘칠수도 있다.
- 큰 자료형에서 작은 자료형으로 옮길 때 데이터의 손실이 발생할 수도 있고 아닐 수도 있다.

### 형변환 방법
```java
(원하는 자료형) 데이터or 변수;
```

```java
   char c = 'B'; //2byte
   int n = c + 1; //여기까지는 프로모션 캐스팅
   c = n; //c는 2byte, n은 4byte이므로 오류 발생   
   c = (char)n; //이렇게 수정
   System.out.println("c = " + c);

   float f = 5.5f;
   int n = 0;
   n = (int)f; //같은 4byte여도 자료형이 일치하지 않으면 대입되지 않음. 고로 캐스팅
   System.out.println("n = " + n);
   //결과는 5 인데, float에서 int로 캐스팅되면서 소수점 이하 자리를 상실함
```

## 자바의 특징
```java
짚고 넘어갈 자바의 장점(신기함)
byte b1 = 100;
byte b2 = 20;
byte b3 = b1 + b2; //오류남.

int b3 = b1 + b2; //이렇게 수정
```
byte의 표현 범위가 127까지 밖에 되지 않다보니, byte끼리의 연산은 127을 넘어가버릴 가능성이 높다.<br>
이런 상황을 대비하여 java개발자들은 byte끼리의 연산이 수행될 때, int형 변수로 값을 받도록 만듦.<br>

# 데이터의 입력
- 키보드를 통해 다양한 데이터를 자유롭게 입력하는 방법이 있다.
- 키보드를 통해 입력하는 데이터를 문자열로 얻기 위해서는 'java.util'패키지에 있는 Scanner클래스를 이용해야 한다.
```java
import java.util.Scanner;
Scanner 객체명 = new Scanner(System.in);
```
<table>
<tr>
	<th>자료형</th>
	<th>메서드</th>
	<th>설명</th>
</tr>
<tr>
	<td rowspan = "4">정수형</td>
	<td>byte nextByte()</td>
	<td>입력받은 값을 byte형으로 반환</td>
</tr>
<tr>
	<td>short nextShort()</td>
	<td>입력받은 값을 short형으로 반환</td>
</tr>
<tr>
	<td>int nextInt()</td>
	<td>입력받은 값을 int형으로 반환</td>
</tr>
<tr>
	<td>long nextLong()</td>
	<td>입력받은 값을 long형으로 반환</td>
</tr>
<tr>
	<td rowspan = "2">실수형</td>
	<td>float nextFloat()</td>
	<td>입력받은 값을 float형으로 반환</td>
</tr>
<tr>
	<td>double nextDouble()</td>
	<td>입력받은 값을 double형으로 반환</td>
</tr>
<tr>
	<td rowspan="2">문자형</td>
	<td> String nextLine()</td>
	<td>입력받은 라인 전체를 문자열 타입으로 반환.enter키로 구분</td>
</tr>
<tr>
	<td>String next()</td>
	<td>입력받은 값을 문자열 타입으로 반환. 띄어쓰기로 구분</td>
</tr>
 
</table>

## 데이터 입력받기
```java
//Scanner 객체명 = new Scanner(System.in);
Scanner sc = new Scanner(System.in);
System.out.print("나이를 입력해주세요");

//자료형 변수명 = 객체명.Scanner함수();
int age = sc.nextInt();

System.out.printf("제 나이는 %d세 입니다.",age);
```
```java
//Scanner 객체명 = new Scanner(System.in);
Scanner sc = new Scanner(System.in);
String name,address;
int age;
double weight;
System.out.print("이름 : ");
name = sc.next();
System.out.print("나이 : ");
age = sc.nextInt();
System.out.print("주소 : ");
address = sc.next();
System.out.print("체중 : ");
weight = sc.nextDouble();

System.out.printf("당신의 이름은 %s입니다.\n",name);
System.out.printf("당신의 나이는 %d입니다.\n",age);
System.out.printf("당신의 주소는 %s입니다.\n",address);
System.out.printf("당신의 체중은 %.1fkg입니다.\n",weight);
```

# 연산자(Operator)
- 연산이란 데이터를 처리하고 결과를 산출하는 작업을 말한다.
- 연산은 항(피연산자)과 연산자로 이루어진다.
- 항은 연산에 사용되는 값을 의미하며, 연산자는 기호를 의미한다.
- 항과 연산자를 이용해 연산 과정을 나열한 것을 연산식(expression)이라고 합니다.

![image](https://github.com/to7485/Java1900/assets/54658614/5eb76465-0954-489f-b644-ab02045f7af3)

## 기본 연산자의 종류
- 자바는 사칙연산을 비롯해 다양한 연산자를 제공하고 있다.
- 피연산자의 개수에 따라 단항,이항,삼항 연산자로 분류할 수 있다.
- 사용 목적에 따라 산술,증감,대입,비교,논리, 비트,증감등으로 분류할 수 있다.

## ex1_operator 패키지 생성
|종류|연산자|기능|
|----|------|-----|
|최고연산자연산자|. , ()| 괄호 연산 먼저 계산|
|증감연산자연산자| ++, --| 1씩 증감|
|산술연산자연산자|+,-,*,/,%|사칙연산,나머지계산|
|시프트연산자|>>,<<| 비트의 이동|
|비교연산자| >, <, >=,<=,==,!= | 두 값의 비교|
|논리연산자| &&,\|\|\,!|논리의 연산|
|비트연산자|&,\|,~,^ |비트단위의 논리연산|
|대입연산자|=, +=,-=,/=,*=,%=|우변의 값을 좌변에 대입|
|삼항연산자|조건식? A : B| 조건식의 결과에 따라 A와 B선택|

## 산술연산자
- 산술연산자는 4칙연산(+,-,*,/)과 나머지 값을 구하는 연산자로 나뉜다.
- 프로그래밍에서 곱셈은 x가 아닌 *, 나눗셈은 / 기호를 사용한다.

```java
int n1, n2, n3;
n1 = 20; //n1에20을대입
n2 = 7; //n2에7을대입
n3 = n1 + n2; //n1 + n2의값을n3에대입
System.out.println("n3 = " + n3); //결과27

n3 = n1 - n2;
System.out.println("n3 = " + n3); //결과 13

n3 = n1 / n2;
System.out.println("n3 = " + n3); //결과 2 - 몫 출력

n3 = n1 % n2;
System.out.println("n3 = " + n3) //결과 6 - 나머지 출력
```

### 산술변환
- 기본적으로 이항 연산자의 연산은 두 피연산자의 타입이 일치해야 연산이 가능하다.
- 컴퓨터는 서로 다른 타입을 계산하지 못하므로 값의 손실이 적은쪽으로 타입을 맞춰준다.

```java
long + int -> long + long -> long
float + int -> float + float -> float
double + float -> double + double -> double

```

## 대입연산자
- 우변의 값을 좌변에 대입을 한다 라고 생각하자!

```java
int n1 = 10; //n1이라는 int형 변수에 10이라는 정수를 대입함.
int n2 = 7;
System.out.println("=연산자: n1 = " + n1 + ", n2 = " + n2);
```
### 복합대입연산자 
- 산술연산자와 대입연산자가 합쳐진 형태, +=,-=,*=,/=,%=
- A = A +,-,*,/,% B 와 같은 의미이다.
```java
package test;

public class Test{
	public static void main(String[] args) {
		int x = 10;
		int y = 1;
		
		y += x; // y = y + x; -> y = 1 + 10;
		System.out.println(y); //11
		
		y *= x; // y = y * x -> y = 11 * 10;
		System.out.println(y); //110
		
		y %= x; //y = y % x; -> y = 110 % 10;
		System.out.println(y); //0
	}
}
```

## 관계(비교)연산자
- 변수나 상수의 값을 비교하여 참과 거짓을 판단하는 연산자.
- 결과가 항상 true나 false로 반환된다. (반환을 받는다는건 연산식 자체가 반환값 데이터로 바뀌게 된다)

```java
int x = 10;
int y = 20;
boolean result;
result = x < y;
//한줄로하면boolean result = x < y;
System.out.println("x < y : " + result);

result = x == y;
System.out.println("x == y : " + result);

result = x != y;
System.out.println("x != y : " + result);
```
## 논리연산자
- 피연산자를 두개 필요로 하는 연산자이다.
- 피연산자로 boolean형 데이터만 사용가능하다.

|연산자|논리식|연산내용|
|-----|-----|--------|
|&&|논리곱(AND)|두 항이 모두 참이면 true, 아니면 false)|
|\|\||논리합(OR)|두 항 중 하나라도 참이면 true, 아니면 false|
| ! | 부정(not) | 참을 거짓으로, 거짓을 참으로 연산|

### &&은 And의 의미를 가지고 있다. 앞 뒤의 연산이 모두 True여야 True를 반환한다.
```java
int myAge = 30;
int limit = 35;

//&&은 앞쪽의 연산이 false일때 뒤쪽연산을 수행하지 않고 넘어간다.
//&&는and의 뜻. '~하고'라는 의미로 이해하면 도움이 된다.
//참 && 참 = 참
//참 && 거짓 = 거짓
//거짓 && 참 = 거짓
//거짓 && 거짓 = 거짓
//둘 다 참일때만 참
boolean result = (limit - myAge) >= 5 && myAge > 30;
System.out.println("&&연산결과: " + result);
```
### ||는 Or의 의미를 가지고 있다. 앞 뒤의 연산중 하나만 True이어도 True를 반환한다.

```java
int n1 = 10;
int n2 = 20;
//||은앞쪽의연산이false여도 뒤쪽연산을수행한다.
//||는or의 뜻. '~거나'라는의미로이해하면도움이된다.
//참 || 참 = 참
//참 || 거짓 = 참
//거짓 || 참 = 참
//거짓 || 거짓 = 거짓

//한쪽만 참이어도 참
boolean result2 = (n1 += 10) > 20 || n2 - 10 == 11;
System.out.println("||연산결과: " + result2);
```

### !는 not의 의미를 가지고 있다. True를 False로 False를 True로 바꿔준다.
```java
System.out.println("true의 부정 : " + !true);
System.out.println("false의 부정 : " + !false);

Scanner sc = new Scanner(System.in);

System.out.print("정수 하나 입력 : ");
int num = sc.nextInt();

System.out.println("입력한 정수가 짝수인가? " + !(!(num % 2 == 0)));
System.out.println("입력한 정수가 짝수인가? " + !(num % 2 != 0));

//위에서 입력 받은 수가 3의 배수인지 확인하여 출력하세요
System.out.println("입력한 정수가 3의 배수인가? " + !(!(num % 3 == 0)));
System.err.println("입력한 정수가 3의 배수인가? " + !(num % 3 != 0));

System.out.println("입력한 정수가 양수인가? " + (num > 0));
System.out.println("입력한 정수가 양수인가? " + !(num <= 0));
```

## 비트연산자.
- 논리 연산자와 유사하지만 bit단위(2진수)의 연산만 가능하다.
- 일반적으로 다음에 배울 시프트 연산자와 더불어 암호화, 복호화 작업에 사용된다.

|연산자|논리식|연산내용|
|-----|-----|--------|
|&|논리곱(AND)|두 항이 모두 참이면 true, 아니면 false)|
|\||논리합(OR)|두 항 중 하나라도 참이면 true, 아니면 false|
|^|배타적논리합(XOR)|두 항이 다르면 true, 같으면 false|
| ~ | 부정(not) | 참을 거짓으로, 거짓을 참으로 연산|

```java
int a = 10; //1010
int b = 7; //0111
int c = a & b; //논리곱(and) - 2진수로바꿨을 때 두값이모두1 일때만결과가1. 나머지는0
System.out.println("c : " + c);

int a2 = 12;
int b2 = 8;
int c2 = a2 | b2; //논리합(or) - 2진수로바꿨을 때 두값이모두0일때만결과가0. 나머지는1
System.out.println("c2 : " + c2);

int a3 = 9;
int b3 = 11;
int c3 = a3 ^ b3; //배타적or(xor) - 2진수로바꿨을때 두값이 서로같을때는0.서로다를때는1
System.out.println("c3 : " + c3);  
```

### ~ (not연산)
- 2진수로는 음수를 표현할 수 없다.
- 그래서 비트의 맨 앞자리는 수의 표현이 아닌 부호의 표현으로 쓰기로 약속을 했다.
- 1이면 음수, 0이면 양수이다.
```c
int x = 7;
System.out.println("~x : " + ~x); //-8

왜 -8이 나오는가

1. 7의 2진수 표현 :  0111
2. 비트의 반전 : 1000
3. 가장 낮은 비트에 1 더하기 : 1001

편하게 그냥 -(x+1) 를 하자.
```

## 증감연산자.
- 1씩 증가시키거나 1씩 감소시키는 연산자.
- ++, --
### 선행증감
- 변수의 앞에서 사용된다.
```java
int a = 10;
System.out.println("a : " + ++a); //결과 11
```

### 후행증감
- 변수의 뒤에서 사용된다.
```java
int b = 10;
System.out.println("b : " + b++); //결과 10
//여기까지 일단 결과 보여주고 아래쪽 System.out.println()써서 확인시켜주자.
		
//여기서는 값이 증가되어 있다.
//b++연산을 수행 한뒤 대기하다가 다시 b를 만났을때 증가된 값을 출력했기 때문.
System.out.println("b++ : " + b); //결과 11

//이렇게 보면 쓸모 없어보이는 것 같아도 정말 많이 쓰이는 연산자 중 하나.
//반복문 들어가면 쓸 일 많아진다.
```

### 오버플로우와 언더플로우
- 오버플로우(overflow)란 타입이 허용하는 최대값을 벗어나는것을 말한다.
- 언더플로으(underflow)는 타입이 허용하는 최소값을 벗어나는것을 말한다.
- 정수 타입 연산에서 오버플로우 또는 언더플로우가 발생하면 실행에러가 발생할 것 같지만 해당 정수 타입의 최소값 또는 최대값으로 되돌아간다.

```java
byte value = 127;
value++;
System.out.println(value);

byte value2 = -128;
value2--;
System.out.println(value2);
```

- 연산 과정 중 발생하는 오버플로우와 언더플로우는 우리가 기대하는 값이 아니므로
- 항상 해당 타입의 범위 내에서 연산이 수행되도록 코딩에 신경써야 한다.
- 만약 연산 과정에서 int타입에서 오버플로우 또는 언더플로우가 발생할 가능성이 있다면 long타입으로 연산을 하도록 해야한다.

## 삼항연산자.
- 하나의 조건을 정의하여 조건식이 참일 때 반환할 명령, 거짓일때 반환할 명령을 얻어내기 위한 연산자.

```java
int a = 10;
int b = 15;
boolean result;		
result = ++a >= b ? true : false;
System.out.println("result :" + result);
		
int n1 = 10;
int n2 = 20;
char result2;
result2 = (n1 += n1) == n2 ? 'O' : 'X';
System.out.println("result2 : " + result2);
//삼항연산의 값을 받을 변수의 자료형과 ?뒤의 결과값의 타입이 같아야 한다.
```

## 연산의 방향과 우선순위
- 산술연산에서 덧셈과 뺄셈보다는 곱셈과 나눗셈이 우선 처리된다는것을 이미 알고 있다.

## 연산자 문제
```java

int x = 10;
int y = 20;
int z = (++x) + (y--);
System.out.println(z); // 31

-----------------------------------------------------------------------------------------------------
int a = 10;
int b = 12;
//++a >= b || 2 + 7 <= b && 13 - b >= 0 && (a += b) - (a % b) > 10;
오류나므로 주석처리 하고 코드 작성없이 결과 도출해 보라 하자

//풀이
int a = 10;
int b = 12;
boolean result;
result = ++a >= b || 2 + 7 <= b && 13 - b >= 0 && (a += b) - (b % a) > 10;
System.out.println(result); 

결과 = true
-----------------------------------------------------------------------------------------------------
/*
* 과수원이 있다.
* 
* 배, 사과, 오렌지를 키우고 있는데 하루에 생산되는 양은 각각
* 5,  7,   5개.
* 
* 과수원에서 하루에 생산되는 총 개수를 출력하고, 시간당 
* 전체 과일의 평균 생산 갯수를 출력.
* 평균값을 담는 변수는 float으로 할 것.
*/
	
//풀이	
int pear = 5; //배
int apple = 7; //사과
int orange = 5; //오렌지
		
int fruitTotal = pear + apple + orange; //하루생산량
System.out.println("하루에 생산되는 과일 수 : " + fruitTotal + "개");
		
float average = fruitTotal / 24f; //시간당 평균
System.out.println("시간당 평균 생산 갯수 : " + average + "개");
-----------------------------------------------------------------------------------------------------
//농구공을 담기 위해 필요한 상자의 개수를 구하세요
//상자 하나에는 농구공이 5개가 들어갈 수 있다.
//만일 농구공이 23개라면 몇개의 상자가 필요한가?

int ball = 23;
int box = ball % 5 == 0 ? ball/5 : ball/5 + 1;
System.out.println("필요한 상자의 수 : " + box);
-------------------------------------------------------------------------------------------------------
//국어,영어,수학에 대한 점수를 키보드를 이용해 정수로 입력받고
//1. 세 과목에 대한 합계 출력하기
//2. 평균 출력하기 (합계/3.0)

//세 과목의 점수와 평균을 가지고 합격 여부를 처리하는데
//세 과목의 점수가 각각 40점 이상이면서 평균이 60점 이상일때 합격
//아니면 불합격

Scanner sc = new Scanner(System.in);
		
System.out.print("국어 : ");
int kor = sc.nextInt();
System.out.print("영어 : ");
int eng = sc.nextInt();
System.out.print("수학 : ");
int math = sc.nextInt();

int total = kor + eng + math;
double avg = ((total) / 3.0);

System.out.println(total);
System.out.println(avg);

String result = (kor >= 40 && eng >= 40 && math >= 40 && avg >= 40) ? "합격" : "불합격"; 
System.out.println(result);
```

