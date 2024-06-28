# 기타제어문
- 일반적으로 조건식의 검사를 통해서 반복문에 진입하게 되면, 다음 조건식을 검사하기 전까지 반복문에 안에 있는 모든 명령을 실행한다.
- 기타제어문을 통해 반복문 자체의 흐름을 개발자가 직접 제어할 수 있다.
- 기타제어문에는 break와 continue가 있다.
## break
- 반복문 내에서 break를 만나게 되면 가장 가까운 반복문을 종료하고 다음 코드를 실행하게 된다.
```java
for(int i = 1; i <= 2; i++){ 
	             for(int j = 1; j <= 5; j++){ 
	
         if(j % 2 == 0){//j 를 2으로 나눈 나머지가 0일때
          break;// 가장 가까운 반복문 탈출!
         }
	          System.out.print(" " + j);
    }//안쪽 for문의 끝
	System.out.println();//줄 바꿈!
}//바깥쪽 for문의 끝
```
- while문과 break
```java
int n = 1;
	
while (true) {//무한반복. !true나 false는 불허
	System.out.println(n);
n++;
	
//n이 10보다 클 때 break로 while문을 빠져나오는 구문을 만들어보자	

if(n > 5){
	break;
  }
}
```
## continue
- 반복문 내에서 continue를 만나게 되면 가장 가까운 반복문의 증감식으로 돌아간다.(증감식이 없을 때 조건식으로 돌아간다)

```java
public class Ex1_continue {
	public static void main(String[] args) {
		
		//continue문 : 반복문 내에서 특정 문장을 건너뛰고자 할 때 사용
		
		for( int i = 1; i <= 2; i++) {
			
			for(int j = 1; j <=5;) {
				
				if(j % 2 == 0) {
				//가장 가까운 반복문의 증감식으로 이동, 증감식이 없다면 조건식으로 이동
					continue;
				}
				j++;
				
				System.out.print(j + " ");
			}//inner
			System.out.println();
		}//outer
		
	}//main
}
```
- continue와 while문
```java
public class Ex2_continue {
	public static void main(String[] args) {
		
		int n = 0;
		
		while(n < 10) {
			n++;
			
			if( n % 2 != 0) {
				//while문에서 continue를 만나면 조건식으로 이동
				continue;
			}
			
			System.out.println(n);
		}//while
		
```
## label
- 일반적인 기타제어문은 단 하나의 반복문만을 이동하게 해줍니다.
- break,continue에 라벨을 달아서 가장 가까이 있는 반복문이 아닌 내가 원하는 반복문을 빠져나오거나,이동할 수 있게 한다.

```java
Ex3_label_break 클래스 생성
	//label: 특정 반복문에 이름표를 붙여 두 개 이상의 반복문을
	//       제어할 수 있도록 하는 키워드
	
	//label은 항상 쌍으로 존재한다.
	//label의 이름은 자기가 원하는대로 사용이 가능하다.
	
	//label은 자신을 포함하고 있는 상위 개념에게만 달 수 있다.
	
	happy: for (int i = 1; i <= 3; i++) {
	
		for (int k = 1; k <= 10; k++) {
			System.out.println(k + " ");
		}
	
		for (int j = 1; j <= 10; j++) {
	
			if (j % 2 == 0) {
				break happy;
			}
			System.out.print(j + " ");
		} // inner
		System.out.println();
	} // outer
}

--------------------------------------------------------------------예제1
continue 패키지에 클래스 만들기
Ex3_label_continue 클래스 생성
int n = 0;
		
outer : while(true){
	
if( n >= 10) //이 부분은 무한반복 되는거 확인후 가장 마지막에 추가.	
		break;
	while(true){
	
n++;		
if(n % 3 == 0){
	System.out.println("continue를 만남");
	continue outer;	System.out.println(n);
	
}
--------------------------------------------------------------------------------
switch속의 break
n = 0;
		
w : while( n < 10) {
	
	n++;
	
	switch( n ) {
	case 1:
		System.out.println("switch문 1번 거쳐감");
		//switch문에서 break는 반복문을 나가는게 아닌 switch문만 나가게 된다.
		break w;
		
	case 2:
		System.out.println("switch문 2번 거쳐감");
		//switch문만 단독으로 사용을 할 때는 continue를 사용할 수 없다.
		continue;
	
	}//switch
	System.out.println(n);
	
}//while

```

# 데이터 타입의 분류
- 기본타입과 참조타입으로 분류한다.
- 참조 타입이란 객체의 주소를 참조하는 타입으로 배열, 열거형, 클래스, 인터페이스가 있다.

## 자바 메모리 영역
### 메서드 영역
- 바이트코드 파일을 읽은 내용이 저장되는 영역으로 클래스별로 상수, static, 메서드코드, 생성자 코드 등이 저장된다.

### 힙영역
- 객체가 생성되는 영역이다. 객체의 주소는 메서드 영역과 스택 영역의 상수와 변수에서 참조할 수 있다.

### 스택영역
- 지역변수와 메서드의 매개변수가 만들어지는 영역이다.
- 

# 배열(Array)
- 같은 자료형의 변수를 지정하여 여러 데이터를 저장할 수 있는 저장공간을 의미한다.
- 이렇게 여러 데이터를 담을 수 있는 구조를 자료구조(data structure)라고 한다.
- 배열을 사용하면 같은 자료형의 데이터를 효율적으로 다룰 수 있다.

## 배열의 선언
![image](https://user-images.githubusercontent.com/54658614/215389995-4398cf1e-78c8-4969-8478-1a3fb9a741a1.png)

- 대괄호[]는 배열의 연산자를 의미한다.
- 자료형 뒤에 붙이거나 변수명 뒤에 붙이면 해당 자료형은 배열이라는 의미로 선언된다.
- 자료형 뒤에 붙이는것이 가독성이 좋아 자주 사용된다.

## null
```java
int num;
```
- 해당 변수는 어떤 값을 가질지 알 수 없다.
- 만약 변수를 만들 때 값을 부여하지 않으면 시스템이 타입에 맞는 불특정 값을 부여하게 된다.
- 따라서 변수를 만들 때, 어떤 값이 부여되는지 쉽게 알기 위해 다음과 같이 초기값을 부여하면서 선언하도록 했다
```java
int num = 0;
```

- 배열의 경우는 여러 개의 데이터를 저장하기 위한 별도의 공간이 필요하다.
- 배열을 선언만 하고 생성하지 않을 경우, 시스템은 배열을 만들 때 null 이라는 키워드를 부여한다.
- null의 의미는 "없다"라는 의미를 가진다.
- 배열 변수는 만들어졌지만 그 안에 값을 담을 공간들이 생성되지 않았다는 뜻이다.
- 신차를 만들 때 이름은 정해서 발표했지만, 실제로 자동차는 아직 생산되지 않은 상태이다.

## 배열의 생성
![image](https://user-images.githubusercontent.com/54658614/215390064-8eaa5306-29c6-4aa4-9acb-86f377d1f8d2.png)

## 선언과 생성을 동시에 하는것도 가능하다.
![image](https://user-images.githubusercontent.com/54658614/215390219-ebbe71be-fd12-46b5-8d31-a12f98307c21.png)

- 배열에 저장될 값을 미리 부여해 선언하는 방법이 있다.
```java
int[] arr = {1,2,3,4,5}
```
- 위와 같이 배열을 선언할 때 값을 지정할 수 있다.
- 5개의 값을 대입했기 때문에, 배열의 크기는 5가 되며 각 순서에 맞게 데이터가 삽입된다.
- 해당 방법은 배열을 최초 선언할 때만 가능하다.

```java
int[] arr; //배열선언
arr = {1,2,3,4,5} //오류
```
- 배열을 선언한 후 다시 값을 대입해야할 경우에는 이미 선언된 배열을 다시 정의하여 값을 대입하면 가능하다.
```java
int [] arr;
arr = new int[]{1,2,3,4,5};
```
- 위와 같은 방법들을 통해서 배열을 선언하면 실제 시스템 메모리에는 선언된 크기와 값 만큼 각각의 독립적인 저장 공간이 연속적으로 배치되어 생성된다.

![image](https://user-images.githubusercontent.com/54658614/215388446-0a8c33c5-5e62-4798-b98b-d445511574a6.png)

- 메모리에 지정한 크기만큼의 저장 공간을 생성하고 그 저장 공간이 있는 위치 값을 arr 변수에 대입한다.
- 배열의 변수는 그 주소 값을 통해서 배열에 접근하는 데이터를 가져오게 된다.

## Ex1_Array 클래스
```java
package test;

public class Test{
	public static void main(String[] args) {
		
		int[] arr = new int[4];
		
		System.out.println(arr);
				
	}
}

[I@7d6f77cc
```
- [X@xxx...과 같은형태로 출력이 될것이다.
- 이 값은 배열이 위치한 주소값이다.
- 이처럼 값을 직접 변수에 저장하는것이 아니라 주소값이 저장되어 해당 주소를 통해 실제 주소에 접근한다.
- 이를 참조변수라고 한다.

## 배열의 특징
- 배열 선언 시 크기를 지정한다.
- 배열 선언 후 공간의 크기를 늘리거나 삭제할 수 없다.
- 지정된 자료형의 값만 저장할 수 있다.

## 배열의 구조
1. 인덱스(index)
    - 배열을 만든 후에는 값을 넣거나 꺼내야 한다.
    - 배열은 각 공간마다 위치를 알려주는 위치 값이 존재한다.
    - 우리는 배열이 지니는 값들의 위치를 인덱스(index)라고 부른다.
    - 인덱스(index)는 배열의 공간마다 붙여진 번호로 0부터 시작하여 순차적으로 증가한다.

```java
// 1) 배열선언
int[] ar;

// 2) 배열생성
//배열의 index수의 갯수는 처음 지정해둔 갯수에서 강제로 늘리거나 줄일 수 없다.
//스택과 힙에 대한 설명  기본자료형 변수와 데이터는 스택에 만들어진다.
//클래스 구조와 배열구조는 스택에 일단 만들어진다. new 라는 키워드를 통해서 힙 메모리 영역에 집을 지어주는 키워드이다.
ar = new int[4];

//생성 후에는 값을 넣어 초기화가 필요하다.
//아무런 값도 넣지않으면 기본자료형은 각 자료형의 초기값,
//스트링형은 null이 들어간다.
//int[] ar = {100, 200, 300, 400};//초기화 방법1

// 3) 초기화 방법2
ar[0] = 100;
ar[1] = 200;
ar[2] = 300;
ar[3] = 400;
//배열의 출력		
System.out.println(arr[0]);
System.out.println(arr[1]);
System.out.println(arr[2]);
System.out.println(arr[3]);
```
2. 배열의 길이
    - 배열을 생성할 때 대괄호[]안에 배열의 길이를 작성했다.
    - 배열을 사용하면서 종종 배열의 길이가 필요할 때가 있다.
    - 배열은 내부적으로 length라는 변수를 지니는데, 해당 변수는 배열의 길이 값을 가지고 있다.
    - 배열의 길이를 알고싶을 때는 '배열명.length'를 하면 된다.
    - 이 변수의 값은 배열이 생성될 때 지정되며 변경할 수 없다.

```java
//배열의 출력2
//ar.length : 배열의 방의 개수
for(int I = 0; I < ar.length; I++){
	System.out.println(ar[i]);
}
```
3. 배열의 초기값
    - 배열은 생성과 동시에 데이터 자료형 별로 기본값이 주어진다.
    - 배열을 선언했을 때 저장되는 초기값을 자료형 별로 정리하면 다음과 같다.

|자료형|초기값|
|------|------|
|정수형|0|
|실수형|0.0|
|문자형|''|
|객체형|null|

```java
package test;

public class Test{
	public static void main(String[] args) {
		
		//5개의 공간을 가지는 배열선언
		int [] intArray = new int[5];
		String[] strArray = new String[5];
		
		//5개의 값을 가지는 배열 선언
		int [] varArray = {1,2,3,4,5};
		
		//intArray의 첫번째 값 출력
		System.out.println("intArray[0] : "+intArray[0]);
		//intArray의 두번째 값 출력		
		System.out.println("intArray[1] : "+intArray[1]);
		//strArray의 첫번째 값 출력
		System.out.println("strArray[0] : "+strArray[0]);
		//strArray의 두번째 값 출력		
		System.out.println("strArray[1] : "+strArray[1]);
		//varArray의 첫번째 값 출력
		System.out.println("varArray[0] : "+varArray[0]);
		//varArray의 두번째 값 출력		
		System.out.println("varArray[1] : "+varArray[1]);		
	}
}
```

## 배열 사용하기
- Ex3_Array 클래스 생성하기
```java
public class ArrayEx3 {
	public static void main(String[] args) {
		char[] ch;
		ch = new char[4];
		//char[] ch = new char[4];
		
		//배열 초기화
		ch[0] = 'J';
		ch[1] = 'A';
		ch[2] = 'V';
		ch[3] = 'A';
		
		//배열 내용 출력
		for(int i = 0; i < ch.length; i++){
			System.out.printf("ch[%d] : %c",i,ch[i]);
		}


		String[] str = new String[3];
		str[0] = "hello";
		
		for(int i = 0; i < ch.length; i++) {
			System.out.print(ch[i]);
		}
		System.out.println();
    
    		System.out.println(ch); //문자형 배열은 배열의 이름만으로도 전체 내용을 출력할 수 있다.
		
		System.out.println("----------------------------");
		
		System.out.println(str); //문자열 배열은 이상하게 나온다.

		//개선된 루프.
		//편리하지만, 배열의 각 요소에 대한 값의 수정과 삭제가 불가
		//for(char ch2 : ch)
			//System.out.println(ch2);
	}
}
```
```java
public class Ex2_array {
	public static void main(String[] args) {
		
		int [] iArr = new int[4];
		
		for(int i = 0; i < iArr.length; i++) {
			//초기화를 할 때 값을 반복문을 통하여 한번에 할당을 할 수 도 있다.
			iArr[i] = (i + 1)*100;
			System.out.println(iArr[i]);
		}
		
	}//main
}
```
```java
package test;

public class Test{
	public static void main(String[] args) {
		
		//단일 문자 배열에 단어와 숫자를 섞어 넣는다.
		char[] cards = {'1','L','O','2','V','3','E'};
		String myWord = "";
		
		//배열의 전체 순회
		for(int i = 0; i < cards.length; i++) {
			
			//i가 대괄호로 들어가며 index가 된다.
			//값을 word변수에 대입한다.
			int word = cards[i];
			
			//아스키 코드를 이용한다.
			//65 ~ 90 는 대문자 A ~ Z
			//97 ~ 122는 소문자 a ~ z
			if((word >= 65 && word <= 90) || (word >= 97 && word <= 122)) {
				
				//문자를 문자열에 연결한다.
				myWord += (char)word;
			}
		}
		
		System.out.println("단어 : " + myWord);
	}
}
```
## 실습문제
- 문제1
```java
//배열 arr에 담겨있는 모든 값의 합을 출력하시오
//결과 : 150

int[] arr = {10,20,30,40,50};

int total = 0;
for(int I = 0; I <arr.length; I++){
	total += arr[i];
}
System.out.printf("배열의 총 합 : %d\n",total);
```
- 문제2
```java
프로그램이 실행되면 배열의 길이를 몇으로 할 것인지 물어본다.
예를들어 키보드에서 5를 입력받으면...

결과 : 
배열의 길이는 몇으로? : 5
ABCDE

public class Work_Ex1 {
	public static void main(String[] args) {
		
		System.out.print("배열의 길이는 몇으로? : ");
		Scanner scan = new Scanner(System.in);
		int n = scan.nextInt();
		
		char c[] = new char[n];
		char c2 = 'A';
		
		for(int i = 0; i < c.length; i++){
			System.out.print(c[i] = c2++);
		}
		
		// char ch[] = new char[n];
		// for(int i = 0; i < ch.length; i++){

		 // ch[i] = (char)('A' + i);
		 // System.out.print(ch[i]);
		// }		
	}
}
```
- 문제3
```java
변수 money에 10 ~ 5000사이의 난수를 발생시켜 넣는다.
단 3450,2100,60과 같이 1의자리 숫자는 반드시 0이 되도록 한다.

발생된 난수 money를 동전으로 바꾸면 각 동전이 몇 개씩 필요한지를 판단하는 코드 작성,

가능한한 적은 수의 동전을 사용하도록 한다.

//4170
//500원 : 8
//100원 : 1
//50원 : 1
//10원 : 2

int[] coin = {500,100,50,10};
int money = new Random().nextInt( 500 )+1
money *= 10;
System.out.println(“금액: ” + money);

for(int I = 0; I < coin.length; I++) {
     int res = money / coin[i];
     System.out.println( coin[i] + “원 : ” + res);
     money %= coin[i];
}//for
```
- 문제4
```java
1 ~ 45의 난수를 발생시켜 로또번호를 생성하는 프로그램 만들기.
public class MyLotto {
	public static void main(String[] args) {
		
		//로또번호 6개를 담을 배열 준비
		int[] lotto = new int[6];
		outer : for(int i = 0; i < lotto.length;){//나중을 위해 i++을 생략
			lotto[i] = new Random().nextInt(45) + 1;
			//중복값을 비교하는 반복문
			for(int j = 0; j < i; j++){
				if(lotto[i] == lotto[j]){
					continue outer;
				}					
			}//inner For
			System.out.print(lotto[i] + " ");
			i++;						
		}//outer For
	}
}
```

## Arrays
- Arrays 클래스는 배열의 복사, 항목 정렬, 항목 검색 등 배열을 다루기 위한 다양한 메서드를 제공한다.
- 지금 당장은 배열의 도우미 기능을 지닌것으로만 생각하자.
- Arrays클래스를 이용하면 배열의 기능을 더욱 쉽게 사용할 수 있다.
- Arrays에 속해있는 기능을 사용할 때는 'Arrays.함수명()'로 작성하여 기능을 호출한다.

### 배열의 출력
- toString()은 반복문의 도움 없이 배열을 출력할 수 있도록 도와준다.
- 배열에 정의된 값을 문자열(String)형태로 변환하여 출력해준다.
```java
public class Test{
	public static void main(String[] args) {
		
		int[] arr = {1,6,2,3,10,7,4,5,8,9};
		
		System.out.println(Arrays.toString(arr));
	}
}
```

### 배열의 정렬
- sort()는 배열을 정렬해주는 기능이 있다.
- 기본적으로 오름차순으로 정렬이 된다.
```java
public class Test{
	public static void main(String[] args) {
		
		int[] arr = {1,6,2,3,10,7,4,5,8,9};
		
		//정렬전
		System.out.println(Arrays.toString(arr));
		
		//정렬후
		Arrays.sort(arr);
		System.out.println(Arrays.toString(arr));
	}
}
```
- Comparator.reverseOrder()를 통해서 내림차순으로 정렬이 가능하다.
- 하지만 기본자료형 배열로는 불가능하다.
- 기본자료형의 클래스타입이 필요한데 이를 Wrapper클래스 라고 한다.

```java
public class Test{
	public static void main(String[] args) {
		
		Integer[] arr = {1,6,2,3,10,7,4,5,8,9};
		
		//정렬후
		Arrays.sort(arr, Comparator.reverseOrder());
		System.out.println(Arrays.toString(arr));
	}
}
```

### 배열의 복사
- 자바에서 배열은 한 번 생성하면 그 길이를 변경할 수 없다.
- 따라서 더 많은 데이터를 저장하거나 기존의 배열과 똑같은 배열을 새로 만드려면 배열을 복사해야 한다.
- 배열을 복사하는 방법에는 얕은 복사와 깊은 복사 두가지가 있다.
    - 얕은 복사(Shallow Copy) : 복사된 배열이나 원본 배열이 변경될 때 서로 간의 값이 함께 변경된다.
    - 깊은 복사(Deep Copy) : 복사된 배열이나 원본 배열이 변경될 때 서로 간의 값은 바뀌지 않는다.
 
```java
//얕은복사
public class Test{
	public static void main(String[] args) {
		
		int[] arr01 = {1,2,3};
		
		//배열의 얕은 복사
		int[] arr02 = arr01;
		
		System.out.println("arr01 배열 : " + Arrays.toString(arr01));
		
		//배열 arr02의 값 변경
		arr02[1] = 10;
		
		//arr01변경 후 배열 출력
		System.out.println("arr01 배열 : " + Arrays.toString(arr01));
		System.out.println("arr02 배열 : " + Arrays.toString(arr02));
	}
}
```

```java
//깊은 복사
//배열의 깊은 복사는 반복문을 이용해 새로운 배열에 값을 직접 넣어주거나
//Arrays클래스 또는 System 클래스가 가진 기능을 이용한다.
public class Test{
	public static void main(String[] args) {
		
		int [] cards = {1,6,4,5,3,2};
		int [] newCards = new int[cards.length];
		
		//Arrays클래스를 이용한 깊은 복사
		int [] newCards2 = Arrays.copyOf(cards, cards.length);
		
		//반복문을 이용한 깊은 복사
		for(int i =0; i < cards.length; i++) {
			newCards[i] = cards[i];
		}


		//System클래스를 이용한 깊은 복사
		int[] newCards3 = new int[5];

		System.arraycopy(cards, 0, newCards3, 0, cards.length);
		
		newCards[1] = 100;
		
		System.out.println("cards 배열 : " + Arrays.toString(cards));
		System.out.println("newCards 배열 : " + Arrays.toString(newCards));
		System.out.println("newCards2 배열 : " + Arrays.toString(newCards2));
		System.out.println("newCards3 배열 : " + Arrays.toString(newCards3));
	}
}
```

# 다차원배열
- 다차원 배열이란 2차원 이상의 배열을 의미하며, 배열의 요소로 또 다른 배열을 가지는것을 의미합니다.
- 2차원 배열은 배열의 요소로 1차원 배열을 가지고,
- 3차원 배열은 배열의 요소로 2차원 배열을 가지게 됩니다.

## 2차원 배열의 선언
- 2차원 배열을 선언하는 방법은 1차원방법과 근본적으로는 동일합니다.
- 다만 대괄호[]가 하나 더 추가됩니다.

![image](https://user-images.githubusercontent.com/54658614/215390509-ba91a4f5-ca52-41e0-bd32-04be2d2e08d8.png)

```java
int test[][] = new int[2][3];
test[0][0] = 100;
test[0][1] = 200;
test[0][2] = 300;
		
test[1][0] = 400;
test[1][1] = 500;
test[1][2] = 600;
System.out.println(test[0][1]);//숫자 바꿔가며 확인
```
![image](https://user-images.githubusercontent.com/54658614/215390509-ba91a4f5-ca52-41e0-bd32-04be2d2e08d8.png)

- 2차원 배열은 다양한 방식으로 선언할 수 있는데, 다음과 같이 열을 지정하지 않고 선언할 수 있다.
```java
int[][] arr = new int[크기][];
```
- 열의 크기를 지정하지 않고 선언한 뒤, 각 행의 열을 각각 선언하여 사용할 수 있다.
```java
int[][] arr = new int[3][];
arr[0] = new int[2];
arr[1] = new int[3];
arr[2] = new int[1];
```
```java
↓↓↓이렇게 각 방 사이즈 지정해줘도 됨
int num[][] = new int[2][];
num[0] = new int[3];
num[1] = new int[2];
int n = 0;
		
for(int i = 0; i < num.length; i++){
			
	for(int j = 0; j < num[i].length; j++){
				
		System.out.print((num[i][j] = n += 100) + " ");
				
	}
	System.out.println();		
}
```
## 실습문제
```java
public class FileEx {
	public static void main(String[] args) throws Exception{

		int arr[][] = {{1, 2, 3, 4, 5},
				{6, 7, 8, 9, 10},
				{11, 12, 13, 14, 15},
				{16, 17, 18, 19, 20}};
		
		//int arr[][] = new int[4][5];
		//int count = 0;
		int total = 0;
		float average = 0;
		int count = 0;

		for(int i = 0; i < arr.length; i++){

			for(int j = 0; j < arr[i].length; j++){
				//arr[i][j] = ++count;
				total += arr[i][j];
				count++;
			}
		}
		System.out.println("total : " + total);
		average = (float)total / count;
		System.out.println("평균 : " + average);
	
	}
}
```
- 문제2
```java
학생들의 수학과 영어성적을 등록하는 프로그램이 있다.
프로그램을 실행하면 몇 명의 정보를 저장 할 것인지를 입력받은 후,
입력받은 수 만큼 학생들의 이름과 수학성적, 영어성적을 입력받는 프로그램 작성 

결과 :
등록할 인원수 : 2
이름 : 홍길동
수학 : 90
영어 : 87
-------------------------
이름 : 독고길동
수학 : 70
영어 : 100
-------------------------
2명 등록 완료!!
홍길동 90 87
독고길동 70 100


풀이 : 
public class Work_Ex2 {
	public static void main(String[] args) {

		System.out.print("등록할 인원수 : ");
		Scanner scan = new Scanner(System.in);
		int n = scan.nextInt();

		String str[][] = new String[n][3];

		for(int i = 0; i < str.length; i++){

			System.out.print("이름 : ");
			str[i][0] = scan.next();

			System.out.print("수학 : ");
			str[i][1] = "수학 : " + scan.next();

			System.out.print("영어 : ");
			str[i][2] = "영어 : " + scan.next();
			System.out.println("-------------------------");
		}		
		
		System.out.println(str.length + "명 등록 완료!!");
		for(int i = 0; i < str.length; i++){
			
			for(int j = 0; j < str[i].length; j++){
				System.out.print(str[i][j] + “ ”);
			}
			System.out.println();
		}
	}
}
```

## 향상된 for문
- 향상된 for문은 JDK 1.5부터 새롭게 추가된 기능으로 배열과 컬렉션의 모든 요소를 참조하기 위한 반복문이다.

```java
for(변수 : 배열){
    실행코드
}
```
- for문을 실행할 반복 대상이 있으면 변수는 반복대상이 지닌 자료형과 같은 타입으로 지정해야 한다.
- 반복 대상의 요소를 하나씩 꺼내서 변수에 대입하면서 진행하고, 반복 대상의 길이만큼 꺼내어 반복한다.

```java
public class Test{
	public static void main(String[] args) {
		
		int[] score = {90,92,93};
		
		int sum = 0;
		double avg = 0;
		
		for(int val : score) {
			sum += val;
		}
		
		avg = (double)sum/3;
		System.out.println("총점 : " + sum + ", 평균 : " + avg);
	}
}
```
