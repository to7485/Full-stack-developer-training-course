# 제어문
- 일반적으로 프로그램에 포함된 실행문은 순차적으로 실행이 된다.
- 하지만 순차적으로만 실행한다면 프로그램이 매우 길어지거나 표현하기 어려운 상황이 발생할 수 있다.
- 예를 들어, 어떤 변수에 10을 더하는 명령을 1,000번 수행해야 하는 경우, 순차적으로만 실행하면 실행문을 1,000번 적어야 한다.
- 또한 선택의 개념을 구현하기가 힘듭니다.
## 조건문
- 조건식에 따라서 프로그램의 흐름을 제어할 수 있는 문법이다.
- 삼항연산자에서 미리 살펴봤듯이, 조건식의 true 또는 false라는 결과에 따라서 어떤 구문을 실행할지 결정한다.

### 조건문의 종류
- 조건문에는 크게 if문과 switch문이 있다.
- 고려해야 하는 조건이 적으면 if, 많으면 switch를 사용하는것이 효율적이다.
- 하지만 특정 개수에 따라 반드시 둘 중 하나를 선택해야 하는 것인 아니다.

## 단순 if문
- 조건문 중에서도 가장 기본이 되는 명령문이다.

```java
// 조건식에는 논리형으로 결과를 확인할 수 있는 모든 식을 넣을 수 있다.
// 조건식의 값이 true라면 {}안에 있는 코드를 실행한다.
기본형
if(조건식){
  조건식이 참일 때 실행할 문장.
}

//만약 실행해야 하는 명령이 하나라면 중괄호를 생략할 수 있다.
if(조건식)
  조건식이 참일 때 실행할 문장.

if(조건식)조건식이 참일 때 실행할 문장;

```

### 자바에서 간결하고 가독성이 좋은 코드를 만드는 중괄호와 들여쓰기
- 중괄호({})블록은 여러 개의 수행문을 하나로 묶기위해 작성한다.
- 수행문이 하나일경우 생략할 수 있지만 중괄호를 사용하면 가독성이 좋을 뿐 아니라 코드의 해석이 용이하고 버그를 찾아 수정하는데 도움이 되므로 중괄호를 사용하는 습관을 길러두는것이 좋다.
- 중괄호를 사용할 때는 들여쓰기를 하는 것이 좋다. 들여쓰기는 공백이나 탭을 이용하는데 혼용하여 사용하지 않고 한가지 방법으로 일관되게 사용하는 것이 좋다.

## ex01_if패키지 생성하기

### if01클래스 생성하기
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
- if문을 사용하면 조건이 참(true)일때만 흐름을 제어할 수 있다.
- 조건이 거짓일때도 흐름을 제어하고 싶다면 if-else문을 사용한다.
- "만약 ~라면 A하고 아니면 B하겠다"라는 의미를 코드로 작성한 것으로 보면 된다.

### 기본 구조
```java
기본형
if(조건식){
  조건식이 참일 때 실행할 문장.
} else {
  조건식이 거짓일 때 실행할 문장.
}
```

### if02클래스 생성하기
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
```
- 우리는 if-else문을 활용해 다양한 문제를 해결할 수 있다.
- 예를 들어, 정수 2개를 비교하여 더 큰 수를 찾아내는 코드를 보다 간단하게 해결할 수 있다.
```java
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

### 예제
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
### if_elseif01클래스 생성하기
```java
int favorite = 7;

if(favorite < 5) {//1번 조건문
	System.out.println("좋아하는 숫자가 5보다 작습니다.");
}else if(favorite > 5) {//2번 조건문
	System.out.println("좋아하는 숫자는 5보다 큽니다.");
}else {
	System.out.println("좋아하는 숫자는 5입니다.");
}
```
- 1번 조건식이 true라면 2번 조건식이 아무리 true여도, 실행되지 않고 프로그램은 바로 if-else if문을 빠져나간다.
- 코드를 아래와 같이 수정하고 실행을 해보겠습니다.
### if_elseif02클래스 생성하기
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
- 효율적인 흐름으로 제어하기 위해 if문과 elseif문의 조건문의 위치를 바꿔야 한다.
- 이러한 구조적 흐름때문에 if-else if문을 작성할 때 조건식의 순서를 어떻게 결정하느냐에 따라서 프로그램의 흐름이 완전히 달라질 수 있도, 오류가 발생할수도 있다.
- 개발자들은 흐름을 정확히 판단해 조건식의 구문과 위치를 결정해야 한다.

### if_elseif03클래스 생성하기
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
### if_elseif04클래스 생성하기
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
### multi_if01클래스 생성하기
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
- switch문에 조건으로 사용될 수 있는 연산자는 '==' 밖에 없다.
- 즉, 두 개의 피연산자 값이 같을때만 조건으로 활용할 수 있다.
- 따라서 하나의 변수 안에 저장되어 있는 값을 다수의 값과 비교해야 할때 주로 사용한다.

```java
기본형
switch(비교값){
case 조건값1 :
    비교값과 조건값이 일치할 때 실행할 문장.
    break;
case 조건값2 :
    비교값과 조건값이 일치할 때 실행할 문장.
    break;
case 조건값3 :
    비교값과 조건값이 일치할 때 실행할 문장.
    break;
default ://비교값과 일치하는 조건값이 없을 때 실행된다. 
	코드;
}
```
## ex02_switch 패키지 만들기

### Switch01클래스 만들기
```java
//1) 비교값과 조건값의 타입은 반드시 일치해야 한다.
//2) 중복되는 조건값을 가질 수 없다.
int n = 1;
	
package test2;

public class Test {
	public static void main(String[] args) {
		int num = 7;
		
		switch(num) {
		case 1:
			System.out.println("num은 1입니다.");
			break;
		case 7:
			System.out.println("num은 7입니다.");
			break;
		default:
			System.out.println("num은 1도 7도 아닙니다.");
		}
	}
}

}
```
## if vs switch
- 둘 다 조건에 따라서 명령을 실행을 하는 문법이다.
- if문은 범위에 따라서 조건을 비교하는데 효과적이고
- switch문은 하나의 값에 따라서 조건을 비교하는데 효과적이다.

### Switch02클래스 생성하기
```java
//switch문의 비교값으로 사용 가능한 자료형
//1) 정수(byte,short,int)
//2) 문자형(char)
//3) 문자열(String)

String str = "홍";
String result;
	
switch (str) { //인자로 비교할 값이 들어와야 한다.

case "박"://인자와 비교할 조건값이 들어온다.	
result = "박길동";	
break;
	
case "이"://콜론이다. 세미콜론 아니다.	
result = "이길동";	
break;
	
case "독고":	
result = "독고길동";	
break;
	
case "홍":	
result = "홍길동";	
break;
	
default:	
result = "제대로 입력하시지";	
break;
}
	
System.out.println(result);
```
## switch문에 break가 없다면 어떻게 될까?
- break키워드는 뒤에오는 모든 조건이 실행되지 않도록 switch문을 빠져나가는 역할을 한다.
- break키워드가 없으면 어떻게 될까?

### Switch03클래스 생성하기
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
- 조건에 맞는 case를 시작으로 뒤따라오는 모든 case구문이 실행된다.
- 따라서 개발자는 break; 키워드를 적절하게 이용할 수 있어야 합니다.

# java 12 이상의 switch문
- 조건절에 복수개의 값을 사용하는것이 가능해졌다.
- 화살표 표현식을 이용하는게 가능하다.
- 기존 switch문과 달리 case에 해당하는 절만 실행되고, 그 이후 case들은 실행되지 않는다.

### Switch04클래스 생성하기
```java
package test2;

public class Test {
	public static void main(String[] args) {
		String day = "SUNDAY";
		
		//기존의 switch문
		//불필요하게 장황하다
		//에러 발생시 디버깅이 어렵다
		
		switch(day) {
		case "MONDAY":
		case "TUESDAY":
		case "WENDSDAY":
		case "THURSDAY":
		case "FRIDAY":
			System.out.println("평일");
			break;
		case "SATURDAY":
		case "SUNDAY":
			System.out.println("주말");
			break;
		default:
			System.out.println("잘못된 입력입니다.");
		}
		//자바 12이상에서의 switch문
		switch(day) {
		case "MONDAY", "TUESDAY", "WENDSDAY", "THURSDAY", "FRIDAY" -> System.out.println("평일");
		case "SATURDAY","SUNDAY" ->System.out.println("주말");
		default -> System.out.println("잘못된 입력입니다.");
		}
	}
}
```

### Switch05클래스 생성하기
- 기존의 방식에서는 다음과 같이 변수에 값을 대입할 수 있다.
- 하지만 중복되는 코드가 많이 만들어지게 된다.
```java
package test2;

public class Test {
	public static void main(String[] args) {
		int number = 3;
		
		String result = "";
		
		switch(number) {
		case 1:
		case 3:
		case 5:
			result = "홀수";
			break;
		case 2:
		case 4:
		case 6:
			result = "홀수";
			break;
		default:
			result = "6이하의 정수만 입력하세요";
			break;
		}
		System.out.println(result);
			
	}

	//자바 12이상
	String result2 = switch(number) {
		case 1,3,5 -> "홀수";
		case 2,4,6 -> "짝수";
		default -> "6이하의 정수만 입력하세요"; // 값을 리턴할 경우 default 문장이 반드시 있어야 한다.
		};
		
		System.out.println(result2);
}

```

# 반복문
- 특정수행문을 원하는만큼 반복하여 실행하는 제어문
### 반복문의 종류
- for, while

## for문
- 주로 반복 횟수가 정해져 있을 때 사용하는 문법
```java
for(초기식; 조건식; 증감식){
	조건식에 해당할때 반복할 명령
}
```
- 초기식 : 반복을 하기 위한 시작값으로 변수를 하나 초기화 한다.
- 조건식 : 반복을 하기 위한 종료값으로 비교연산자를 많이 사용한다.
- 증감식 : 변수의 값을 증감시켜주는 역할을 한다 증감연산자를 많이 사용한다.

※후행증감이나 선행증감이나 영향은 없지만 개발자들이 다들 후행증감을 사용하므로 후행증감으로 사용하도록 하자.<br>

```java
for(int i = 0; i <= 3; i++){
	System.out.println(i);
}//for문 돌아가는 구조 설명해주기.
```

![image](https://user-images.githubusercontent.com/54658614/215010183-dceb4e66-811e-46ba-a8b6-e3e902446b3d.png)

## 다중 for문
- for문안에 또 다른 for문을 사용하는 경우를 말한다.
- for문을 중첩하여 사용하기 때문에 코드가 어려워 보일 수 있으나 반복문의 원리는 같다.
```java
for(초기식;조건식;증감식){
	for(초기식;조건식;증감식){
		
	}
}
```

# while문
- for무ㄴ은 정해진 횟수만큼 반복하는 문법이다.
- 반면 while문은 반복 횟수가 정해져 있지 않고, 조건식이 true일 경우 계속해서 반복하는 문법이다.
- 부여된 조건식이 true이면 반복문이 실행되고 false면 종료된다.
- **주의하지 않으면 무한루프에 빠질수 있다.**

```java
while(조건식){
    조건식이 참일때 반복할 명령
}
```
- while문은 for문처럼 시작값과 증감값을 가지고 있지 않기 때문에 값을 변화시켜주지 않으면 무한반복이 일어나게된다.

### While01클래스 생성하기

```java
int num = 1;
		
while(num <= 10){ 
	System.out.println(num);
}//while문의 끝
```

```java
int num = 1;
		
while(num <= 10){ 
	System.out.println(num);
	num++;
}//while문의 끝
```

## do-while문
- while문과 같이 조건을 만족할 때까지 반복한다.
- 다만, while문과 다른 점은 먼저 루프를 한 번 실행한 후 조건식을 검사한다는 점이다.
- 즉, 조건식의 결과와 상관없이 무조건 한 번은 실행을 한다.

### Do_while01클래스 생성하기

```java
do{
	반복하고자 하는 명령;
}while(조건식);
```
```java	
int i = 11;
do{
    System.out.println(i);

}while(i <= 10); //결과 : 11
```
- 1부터 10까지의 합 출력하기
```java
int sum = 0;
int i = 1;

do {
	sum += i;
	i++;
} while(i <= 10);

System.out.println("합  : " + sum);
```

### 상황에 따라 반복문 사용하기
- 반복횟수가 지정되는 경우 -> 횟수를 만족할 때 까지 반복
    - ex) 물통에 물을 10번 채워라 -> for문
- 특정 조건이 부여되는 경우 -> 조건이 만족할 때까지 반복(물이 다 차기 전까지)
    - ex) 물통에 물이 가득 찰 때까지 채워라 -> while문
- 특정 조건과 옵션이 부여되는 경우 -> 한 번 실행한 후 반복 여부 판단
    - ex) 물통에 물을 따라보고 새지 않으면 끝까지 채워라 -> do - while문

# 기타제어문
- 반복문(for,while,do-while)은 각각 정해진 횟수 또는 조건에 의해 반복을 진행한다.
- 하지만 숫자가 표시된 100개의 공에서 특정 숫자가 적힌 공을 찾는데, 10번만에 찾았다면 더이상 반복을 할 필요가 없을 것이다.
- 기타제어문은 반복문을 좀 더 개발자의 입맞에 맞게 다룰 수 있게 해준다.

## 1. continue
- 반복문 안에서 continue를 만나게 되면 이후의 실행 코드는 수행되지 않고, 반복문의 처음으로 돌아가 반복문을 진행하게 된다.
- for문의 증감식으로 이동하며, while문과 do-while의 경우 조건식으로 이동한다.

### Continue01클래스 생성하기
```java
package test2;

public class Continue01 {
	public static void main(String[] args) {
		int sum = 0;
		for(int i = 1; i <= 100; i++) {
			if(i % 2 == 0) {
				continue;
			}
			sum += i;
		}
		System.out.println("짝수 합 : " + sum);
	}
}
```

## 2. break
- break문은 이전에 switch문을 학습할 때 나왔던 구문으로 case문을 종료할 때 사용되었다.
- break라는 단어의 의미와 동일하게 반복문을 미리 종료할 때 사용한다.
- 반복문이 진행되는 도중, 특정 조건을 만족해 더이상 반복문을 실행할 필요 없이 종료하려고 할 때 사용한다.

### Break01클래스 생성하기
```java
package control_stat;

import java.util.Scanner;

public class Break01 {
	public static void main(String[] args) {
		int magicNumber = (int)(Math.random() * 50) + 1;
		Scanner scan = new Scanner(System.in);
		boolean isMatched = false;
		
		for(int i = 0 ; i < 10; i++) {
			System.out.print("찾는 숫자를 입력 >>  ");
			int guess = scan.nextInt();
			
			if(guess == magicNumber) {
				System.out.println((i+1) + "번째에 맞췄습니다!");
				isMatched = true;
				break;
			} else if(guess > magicNumber) {
				System.out.println("맞춰야할 숫자가 더 작습니다.");
			} else if(guess < magicNumber) {
				System.out.println("맞춰야할 숫자가 더 큽니다.");
			}
		}
		
		if(!isMatched) {
			System.out.println("정답을 맞추지 못했습니다.");
		}
	}
}
```
