# 반복문
## 특정 수행문을 여러번 반복할 수 있도록 해주는 제어문
- 반복문: 특정수행문을 원하는만큼 반복하여 실행하는 제어문
- 반복문의 종류 : for, while

## for문
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

```java
문제 : 1부터 10까지 반복하는 for문을 작성해보자.
for(int i = 1; i <= 10; i++){
	System.out.println(i);
}

문제 : 10부터 1까지 감소하는 for문을 작성해보자.
for(int i = 10; i >= 1; I--){
	System.out.println(i);
}

문제 - 1부터 10까지 반복하는 문장에서 3의 배수만 출력하는 제어력을 갖추어 보자!	
for(int i=1; i<=10 ; i++){
	if(i%3 == 0){
	    System.out.println(i + “은(는) 3의 배수입니다.”);
	}
}//for의 끝!


문제 - 1부터 20까지 홀수를 차례대로 출력해보자.
for(int i=1; i<=19; i++) {
        if(i%2!=0) {
             System.out.print(i+" ");
        } //if
     } //for

 
문제 - 1부터 10까지 총 합을 구해보자.
int total = 0;
for(int i = 1; i<=10; i++){
 	total += i;
}
System.out.println("1~10까지의 총합 : " + total);
 
정수형 변수를 하나 초기화 하고 해당 정수에 해당하는 구구단 출력하기
int dan = 2;
for(int i = 1; i <= 9; i++){
	System.out.println(dan + " X " + i + " = " + (dan * i));
}
```
```java
자바 1주차(2) 문제 - 1
Scanner를 통해 정수 n을 입력받는다.
그리고 1부터 입력받은 정수 n까지의 합을 계산하여 그 결과를 출력하는 프로그램을 작성.
예를들어 정수 5를 입력받으면, 1 + 2 + 3 + 4 + 5의 연산결과인 15를 출력해야 한다.

public class Work_Ex1 {
	public static void main(String[] args) {
		
int result = 0;
System.out.print("숫자입력 : ");
Scanner scan = new Scanner(System.in);	
int n = scan.nextInt();
	for(int i = 1; i <= n; i++){
		result += i;
		System.out.println("결과 : " + result);
  	}
}//main

//10개의 정수를 입력받아 그 수들 중 짝수가 몇개인지 출력하는 프로그램
int count = 0;
for(int i = 0; i < 10; i++) {
	System.out.print("정수 입력 : ");
	int a = sc.nextInt();
	
	if( a % 2 == 0) {
		count++;
	}
}

System.out.println("입력받은 짝수는 "+count+"개입니다.");


자바 1주차(2) 문제 - 2
Scanner를 통해 정수 n1, n2를 입력받는다.
그리고 n1부터 n2까지의 합을 계산하여 그 결과를 출력하는 프로그램을 작성.
예를들어 2와 5를 입력받으면, 2 + 3 + 4 + 5의 연산결과인 14를 출력해야 한다.

public class Work_Ex2 {	
	public static void main(String[] args) {
		
	int n1 = 0, n2 = 0;
	int result = 0;
		
	System.out.print("첫번째 숫자입력 : ");	
	Scanner scan = new Scanner(System.in);	
	n1 = scan.nextInt();
	System.out.print("두번째 숫자입력 : ");
	n2 = scan.nextInt();
		
	//혹시 스왑을 사용하고 싶다면...	
	if(n1 > n2){
	    int n3 = n1;
	    n1 = n2;
	    n2 = n3;
	}

	for(int i = n1; i <= n2; i++){	
		result += i;
	}
	System.out.println("결과 : " + result);
    }
}

자바 1주차(2) 문제 - 3
키보드에서 숫자를 두 개 입력 받아, 입력받은 두 수의 최소공배수 구하기.
예를들어 2와 5를 입력받았다면 10을, 
         3과 3을 입력받았다면 3이 출력되어야 한다.

public class Work_Ex3 {
	public static void main(String[] args) {
		
		int n1 = 0, n2 = 0;
		
		System.out.print("첫번째 숫자입력 : ");
		Scanner scan = new Scanner(System.in);
		n1 = scan.nextInt();
		
		System.out.print("두번째 숫자입력 : ");
		n2 = scan.nextInt();
		
		int i = 0;
		for(i = 1; i <= n1 * n2; i++){
			
			if(i % n1 == 0 && i % n2 == 0)
				break;						
		}
		//while(true){
			//i++;
			//if(i % n1 == 0 && i % n2 == 0)
				//break;
		//}

		//int i = 1;	
		//while(!(i % n1 == 0 && i % n2 == 0)){
			//i++;
		//}
		System.out.println("최소공배수는 " + i);
	}
}


자바 1주차(2) 문제 - 4
키보드에서 숫자를 두 개 입력 받아, 입력받은 두 수의 최대공약수 구하기.
예를들어 10과 4를 입력받았다면 2가,3과 7을 입력받았다면 “최대공약수가 없습니다”라는 문자열이 출력 되어야 한다.

public class Work_Ex4 {
	public static void main(String[] args) {

int n1 = 0, n2 = 0;
int check = 0;
	System.out.print("첫번째 숫자입력 : ");	Scanner scan = new Scanner(System.in);
n1 = scan.nextInt();

		System.out.print("두번째 숫자입력 : ");
		n2 = scan.nextInt();

		if(n1 >= n2)
			check = n2;
		else
			check = n1;

		int i;
		for (i = check; i >= 1; i--) {
			if ((n1 % i == 0) && (n2 % i == 0)) {
				break;
			}
		}
		
		if (i == 1) {//두 숫자에는 1이외의 공통된 약수가 없다는 의미.
			System.out.print("최대공약수가 없습니다.");	
		}else {
			System.out.print("최대공약수 : " + i);
		}
	}
}

자바 1주차(2) 문제 – 5
키보드에서 숫자를 입력받으면 그 숫자가 소수인지 아닌지를 판별해주는 코드 작성.

public class Work_Ex5 {
	public static void main(String[] args) {

		int n = 0;
		
		System.out.println("숫자를 입력하세요 : ");
		Scanner scan = new Scanner(System.in);
		
		n = scan.nextInt();
		
		int i = 0;
		for(i = 2; i <= n; i++){
			
			if(n % i == 0){
				break;
			}
		}
		
		if(i == n)
			System.out.println(n + "은(는) 소수입니다.");
		else{
			System.out.println(n + "은(는) 소수가 아닙니다.");
		}
	}
}
```
## 다중 for문
- for문 안에 for문이 있는 경우
```java
for(초기식;조건식;증감식){
	for(초기식;조건식;증감식){
		
	}
}
```
### 다중 for문이 작동하는 원리
```java
for(int i = 1;i<=3;i++){
	for(int j = 1;j<=3;j++){
		System.out.println(i+" " + j);
	}
	System.out.println();
}
```

### 결과
![image](https://user-images.githubusercontent.com/54658614/215011017-deb1c912-68c8-416b-b3c9-9e4a7b965e25.png)

- Outer for문이 1번 반복할 때 Inner for문은 완전히 작동한다.
- Inner for문의 동작을 마치고 아래에 명령이 있다면 명령을 수행하고 Outer for문의 증감식으로 올라간다.

```java
//    1 2 3 4
//    1 2 3 4
//    1 2 3 4

for(int i = 1; i <= 3; i++){ //y축	         
	for(int j = 1; j < 5; j++){ //x축
		System.out.print(" " + j);	
     }//안쪽 for문의 끝
	System.out.println();//줄바꿈

}// 바깥쪽 for문의 끝

----------------------------------------------------------------예제 1

// 01 02 03 04
// 05 06 07 08
// 09 10 11 12

int count = 0;
	
for(int i = 1; i <= 3; i++){ //y축
     for(int j = 1; j < 5; j++){ //x축	              
	System.out.printf("%02d ",++count);// 정수3자리에 j값 출력!
     }//안쪽 for문의 끝	           
     System.out.println();//줄바꿈
}// 바깥쪽 for문의 끝
----------------------------------------------------------------예제ex

// A B C D
// E F G H
// I J K  L
char ch = 'A';

for(int i = 1; i <= 3; i++){	          
	for(int j = 1; j <= 4 ; j++){
    System.out.print(" " + ch++);
     }//System.out.printf("%2c", ch++);
    System.out.println();//줄바꿈
}
------------------------------------------------------------------ 예제 2


//* 
//* * 
//* * * 
//* * * * 
//* * * * *

for(int i = 1; i <= 5; i++){	          
	for(int j = 0; j < i; j++){
	    System.out.print("* ");
    	}	
	System.out.println();
     }         
}


------------------------------------------------------------------ 예제 3

//        * 
//      * *
//    * * *
//  * * * *
//* * * * *

for(int I = 0; i< 5; I++) {
   for(int j = 0; j< 5 - (i+1); j++){
       System.out.print(“ ”);
   }//inner for1
    for(int k = 1; k <= I+1; k++) {
        System.out.print(“*”);
   }//inner for2
   System.out.println();
}//outer for

------------------------------------------------------------------ 예제 5
다중for문을 이용하여 아래와 같은 결과를 도출하는 로직을 구현하자.

결과)
1 2 3 4 5 6 7 8 9 10 
2 3 4 5 6 7 8 9 10 1 
3 4 5 6 7 8 9 10 1 2 
4 5 6 7 8 9 10 1 2 3 
5 6 7 8 9 10 1 2 3 4 
6 7 8 9 10 1 2 3 4 5 
7 8 9 10 1 2 3 4 5 6 
8 9 10 1 2 3 4 5 6 7 
9 10 1 2 3 4 5 6 7 8 
10 1 2 3 4 5 6 7 8 9

풀이)
public class Work {
	public static void main(String[] args) {
	for(int i = 1; i <= 10; i++){	          
		for(int j = 0; j < 10; j++){

		     int num = i + j;
	             if(num > 10){
		            num -= 10;
            
	             }//if문
        	System.out.print(num + " ");		          
		}//안쪽 for문
	 System.out.println();
	 }//바깥쪽 for문
    }//main
}
```
# while문
- 간편한 구성을 가진 반복문(선비교 후처리)
- 반복 횟수가 정해져 있지 않고 조건식이 true일 경우 계속해서 반복하는 문법.
- for문보다 구조가 간단하기는 하지만 주의해서 사용하지 않으면 무한 루프 같은 오류에 빠지기 쉽다.

```java
while(조건식){
    조건식이 참일때 반복할 명령
}
```
- while문은 for문처럼 시작값과 증감값을 가지고 있지 않기 때문에 값을 변화시켜주지 않으면 무한반복이 일어나게된다.

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
- while문은 선비교 후처리를 하지만
- do-while문은 선처리 후비교를 하기 때문에 조건에 맞지않아도 무조건 한번은 실행을 하게 된다.
- 제어문 중 유일하게 뒤에 세미콜론(;)을 붙혀야 한다.

```java	
int i = 11;
do{
    System.out.println(i);

}while(i <= 10); //결과 : 11
```
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

