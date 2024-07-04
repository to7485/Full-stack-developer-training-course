# 제어문
- 일반적으로 프로그램에 포함된 실행문은 순차적으로 실행이 된다.
- 하지만 순차적으로만 실행한다면 프로그램이 매우 길어지거나 표현하기 어려운 상황이 발생할 수 있다.
- 예를 들어, 어떤 변수에 10을 더하는 명령을 1,000번 수행해야 하는 경우, 순차적으로만 실행하면 실행문을 1,000번 적어야 한다.
- 또한 선택의 개념을 구현하기가 힘듭니다.
- 제어문은 실행문의 순서를 변경하는 것으로 조건문과 반복문이 존재합니다.
  - 조건문 : if,switch
  - 반복문 : for,while, do-while

## 조건문
- 조건식에 따라서 프로그램의 흐름을 제어할 수 있는 문법이다.
- 삼항연산자에서 미리 살펴봤듯이, 조건식의 true 또는 false라는 결과에 따라서 어떤 구문을 실행할지 결정한다.

## 단순 if문
- 기본형

```java
기본형
if(조건식){
  조건식이 참일 때 실행할 문장.
}

//만약 실행해야 하는 명령이 하나라면 중괄호를 생략할 수 있다.
if(조건식)
  조건식이 참일 때 실행할 문장.

if(조건식)조건식이 참일 때 실행할 문장;

```

- 조건식에는 논리형으로 결과를 확인할 수 있는 모든 식을 넣을 수 있다.
- 조건식의 값이 true라면 {}안에 있는 코드를 실행한다.

```java
int result = 0;
if(3 > 2) {
	result = 3;
}
System.out.println(result);
```

```java
Scanner sc = new Scanner(System.in);

int age = sc.nextInt();
if(age > 19) {
	System.out.println("성인입니다.");
}
System.out.println("프로그램을 종료합니다.");
```

## if - else문
```java
기본형
if(조건식){
  조건식이 참일 때 실행할 문장.
} else {
  조건식이 거짓일 때 실행할 문장.
}
```
```java
int num = 5;

if(num > 4) {
	System.out.println(num+"은 4보다 큽니다.");
} else {
	System.out.println(num+"은 4보다 작습니다.");
}
---------------------------------------------------------
int a = 4;
int b = 10;

if(a > b) {
	System.out.println("a가 b보다 큽니다.");
} else {
	System.out.println("a가 b보다 작거나 같습니다.");
}
---------------------------------------------------------
int x = 10;
int y = 7;
int max = 0;
if(x > y) {
	max = x;
} else {
	max = y;
}

System.out.printf("%d 와 %d 중에 큰 수는 %d 입니다.",x,y,max);
```

### 문제
- 키보드에서 나이를 입력받아 age라는 변수에 저장한다.
- 나이가 20살 이상이면 성인입니다.
- 나이가 20살 보다 어리면 미성년자 입니다. 출력하기.

```java
Scanner sc = new Scanner(System.in);
System.out.print("나이를 입력하세요 : ");
int age = sc.nextInt();

if(age > 19) {
	System.out.println("성인입니다.");
}else {
	System.out.println("미성년자입니다.");
}
```

### 문제2
- 삼항연산자로 만들었던 X개의 농구공을 담기 위한 박스의 개수 구하기
- 키보드에서 값을 입력받아 ball 변수에 저장하기
- 입력받은 공의 개수에 따라 보관에 필요한 박스의 개수를 구하기

```java
Scanner sc = new Scanner(System.in);
System.out.print("공의 개수를 입력하세요 : ");
int ball = sc.nextInt();
int box = 0;
if(ball % 5 == 0) {
	box = ball /5;
	System.out.printf("필요한 박스의 개수는 %d개 입니다.",box);
}else {
	box = ball /5+1;
	System.out.printf("필요한 박스의 개수는 %d개 입니다.",box);
}
```

## if - else if
- 비교해야할 조건이 여러개 있는 경우 사용하는 문법
- 물론 if문안에 두 개 이상의 조건식과 논리연산자를 사용할 수도 있지만
- 더욱 코드를 간결하게 하고 가독성을 높이기 위한 방법으로 if - else if문을 구현합니다.
```java
기본형
if(조건식1){
  조건식1이 참일 때 실행할 문장.
} else if(조건식2) {
  조건식1이 거짓이고 조건식2가 참일 때 실행할 문장.
} else if(조건식3){
  조건식1,2가 거짓이고 조건식3이 참일 때 실행할 문장.
} else {
  위의 조건이 모두 거짓일 때 실행할 문장
}
```
- else - if문의 개수에는 제한이 없습니다.
- 하지만 너무 많은 else - if문을 사용한다면 프로그램의 실행 속도가 현저히 느려질 수 있기 때문에 다른 방법을 함께 고려해야 한다.
- if - else if문의 가장 마지막에 작성하는 else블록은 필요없다면 생략이 가능하다.

```java
int favorite = 7;

if(favorite < 5) {
	System.out.println("좋아하는 숫자가 5보다 작습니다.");
}else if(favorite > 5) {
	System.out.println("좋아하는 숫자는 5보다 큽니다.");
}else {
	System.out.println("좋아하는 숫자는 5입니다.");
}
```
```java
int favorite = 7;

if(favorite > 5) {
	System.out.println("좋아하는 숫자가 5보다 큽니다.");
}else if(favorite == 7) {
	System.out.println("좋아하는 숫자는 7입니다.");
}
```
- elseif에 있는 조건문이 더 정확함에도 불구하고 if문에 있는 조건식이 true가 되버리기 때문에
- elseif에 있는 조건식은 실행되지 못하고 if-else if문을 빠져나간다.
- 보다 효율적인 흐름으로 제어하기 위해 if문과 elseif문의 조건문의 위치를 바꿔야 한다.

```java
Scanner sc = new Scanner(System.in);
System.out.print("나이를 입력하세요 : ");
int age = sc.nextInt();
if(age > 19) {
	System.out.println("성인입니다.");
} else if(age > 13) {
	System.out.println("청소년입니다.");
} else if(age > 6) {
	System.out.println("어린이입니다.");
} else {
	System.out.println("유아입니다.");
}
```

```java
int num = 75;
	
if(num >= 90)
System.out.println("성적은 A입니다.");

else if(num >= 80)	
System.out.println("성적은 B입니다.");

else if(num >= 70)
System.out.println("성적은 C입니다.");

else if(num >= 60)	
System.out.println("성적은 D입니다.");

else
System.out.println("성적은 F입니다.");		
```

### if문의 중첩
- 제어문은 자유롭게 중첩해서 사용할 수 있습니다.
- if문 안에 if문이 있는 경우

```java
if(조건식1){
  if(조건식2){
      조건식1,2가 모두 참일 때 실행할 문장 
  }
}
```

```java
int num = 5;
if(num <=10){
  if(num % 2 == 1){
    System.out.println(num + "은 홀수입니다."); 
  }
}
```

## switch문
- if문과 비슷하지만 if문은 괄호안에 인자값이 true, 혹은 false로 결정되는 조건식이 들어가야 한다.
- Switch문은 인자값으로 조건이 아닌 비교할 값이 들어가야 한다.
- 특정 값을 바로 찾아 들어가기 때문에 if문에 비해 처리속도가 빠르다.

```java
기본형
switch(비교값){
case 조건값 :
    비교값과 조건값이 일치할 때 실행할 문장.
    break;
case 조건값 :
    비교값과 조건값이 일치할 때 실행할 문장.
    break;
case 조건값 :
    비교값과 조건값이 일치할 때 실행할 문장.
    break;
}
```
```java
//1) 비교값과 조건값의 타입은 반드시 일치해야 한다.
//2) 중복되는 조건값을 가질 수 없다.
int n = 1;
	
switch (n) {//인자로 비교할 값이 들어와야 한다.
case 1://인자와 비교할 조건값이 들어온다.
	System.out.println("1. 게임하기");	
	break;//현재 switch문을 빠져나오는 키워드.

case 2:	
	System.out.println("2. 게임소개");	
	break;	
case 3:	
	System.out.println("3. 종료");	
	break;
	
default://비교값과 조건값이 일치하는 것이 하나도 없는 경우 반드시 실행되는 영역			
    System.out.println("메뉴선택이 올바르지 않습니다.");	
	break;
}
```
## if vs switch
둘 다 조건에 따라서 명령을 실행하는 것은 맞지만<br>
if문은 범위에 따라서 조건을 비교하는데 효과적이고<br>
switch문은 하나의 값에 따라서 조건을 비교하는데 효과적이다.<br>

```java
char c = 'A';

switch (c) { //인자로 비교할 값이 들어와야 한다.

case A://인자와 비교할 조건값이 들어온다.	
	result = "90 ~ 100점";	
	break;
	
case B://콜론이다. 세미콜론 아니다.	
	result = "80 ~ 89점";	
	break;
	
case C:	
	result = "70 ~ 79점";	
	break;
	
case D:	
	result = "60 ~ 69점";	
	break;
	
case F:	
	result = "59점 이하";	
	break;
	
default:	
	result = "제대로 입력하시지";	
	break;
}
```
```java
//switch문의 비교값으로 사용 가능한 자료형
//1) 정수(byte,short,int)
//2) 문자형(char)
//3) 문자열(String)

String str = "홍";
String result;
	
switch (str) { //인자로 비교할 값이 들어와야 한다.

case "박“://인자와 비교할 조건값이 들어온다.	
result = "박길동";	
break;
	
case "이"://콜론이다. 세미콜론 아니다.	
result = "이길동";	
break;
	
case ”독고":	
result = "독고길동";	
break;
	
case “홍":	
result = "홍길동";	
break;
	
default:	
result = "제대로 입력하시지";	
break;
}
	
System.out.println(result);
```
## 만약 switch문에 break가 없다면 어떻게 될까?
```java
int num = 1;

switch(num) {
case 1:
	System.out.println("num은 1입니다.");
case 7:
	System.out.println("num은 7입니다.");
default:
	System.out.println("num은 1도 7도 아닙니다.");	
}
```
- 조건에 맞는 case를 시작으로 뒤따라오는 모든 case구문이 실행됩니다.
- 따라서 개발자는 break; 키워드를 적절하게 이용할 수 있어야 합니다.

### 문제1
- 정수형 변수를 하나 만들고 해당 달이 몇일까지 있는지 switch문을 이용해서 작성하시오.
```java
int month = 4
switch(month) {
case1: case3: case5:
case7: case8: case10:
case12:
  System.out.println( month + “월은 31일 까지 있습니다.”);
  break;
case4: case6:
case9: case11:
  System.out.println( month + “월은 30일 까지 있습니다.”);
  break;
case2:
  System.out.println( month + “월은 28일 까지 있습니다.”);
}
```
### 문제2
- 두개의 정수형 변수를 초기화 한다 (값은 자유)
- 그리고 연산자를 담아줄 문자열 변수를 만든다.
- switch문을 이용하여 정수의 연산을 수행하는 코드를 작성해보자.
```java

실행결과 :
10 * 7 = 70
풀이 :
int su1 = 10;
int su2; = 7;
String op = "*";
	
switch (op) {

case "+":
	System.out.println(num1 + " + " + num2 + " = " + (num1 + num2));
//(num1 + num2)괄호로 안묶으면 결과값이 더해지지 않고 문자열로 붙어서 나온다.	
    break;

case "-":
	System.out.println(num1 + " - " + num2 + " = " + (num1 – num2));	
    break;
	
case "*":
	System.out.println(num1 + " * " + num2 + " = " + (num1 * num2));	
    break;
	
case "/":
	System.out.println(num1 + " / " + num2 + " = " + (num1 / num2));	
    break;
	
default:
	System.out.println("올바른 연산자가 아닙니다.");
    break;
}	
```
