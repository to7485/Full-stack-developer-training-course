# 형변환
- 자료형을 다른 자료형으로 변환하는 것을 말한다.
- 모든 연산은 기본적으로 같은 자료형들끼리만 수행할 수 있다.
- 따라서 서로 다른 자료형의 연산을 수행하기 위해서는 같은 자료형으로 변환해야 한다.
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

