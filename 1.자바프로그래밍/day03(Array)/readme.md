# 배열(Array)
- 같은 자료형의 변수를 지정하여 여러 데이터를 저장할 수 있는 저장공간을 의미한다.
- 이렇게 여러 데이터를 담을 수 있는 구조를 자료구조(data structure)라고 한다.
- 배열을 사용하면 같은 자료형의 데이터를 효율적으로 다룰 수 있다.

## 배열이 필요한 이유
- 10개의 데이터를 저장하려면 해당 자료형의 변수를 10개 만들어서 저장해야 했다.
- 물론 이런방법으로 데이터를 저장할 수 있지만 데이터가 많아질수록 관리를 하기 힘들어진다.

## 배열의 선언
- 배열을 사용하려면 변수와 마찬가지로 선언을 먼저 해야 한다.
```
자료형[] 배열명;
자료형 배열명[];
```
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
- 배열을 선언한 후에는 배열을 생성해야 한다.
- 배열을 선언한 것은 집을 짓는것과 같다. 안에 방을 만들어야 입주가 가능하듯이, 배열에 데이터를 넣어줄 수 있는 공간을 생성해줘야 한다.
- 프로그래밍에서는 뭔가를 기억할 때 메모리를 사용한다.
- 배열은 데이터를 저장하기 위한 공간이 필요하므로 메모리에 필요한 만큼 공간을 만들도록 선언해야 한다.
- 배열을 생성하기 위해서는 'new'라는 연산자와 함께 자료형의 길이를 지정한다.
```
new int[4]
```
- 메모리에 배열의 데이터를 저장하기 위한 4개의 공간을 만들어라 라는 명령이다.

## 선언과 생성을 동시에 하는것도 가능하다.
```
int [] arr = new int [4];
```

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
int [] arr; //배열선언
arr = new int[]{1,2,3,4,5}; //배열 재정의
```
- 위와 같은 방법들을 통해서 배열을 선언하면 실제 시스템 메모리에는 선언된 크기와 값 만큼 각각의 독립적인 저장 공간이 연속적으로 배치되어 생성된다.

![image](https://user-images.githubusercontent.com/54658614/215388446-0a8c33c5-5e62-4798-b98b-d445511574a6.png)

- 메모리에 지정한 크기만큼의 저장 공간을 생성하고 그 저장 공간이 있는 위치 값을 arr 변수에 대입한다.
- 배열의 변수는 그 주소 값을 통해서 배열에 접근하는 데이터를 가져오게 된다.

###  Array01 클래스생성
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
### 1. 인덱스(index)
- 배열을 만든 후에는 값을 넣거나 꺼내야 한다.
- 배열은 각 공간마다 위치를 알려주는 위치 값이 존재한다.
- 우리는 배열이 지니는 값들의 위치를 인덱스(index)라고 부른다.
- 인덱스(index)는 배열의 공간마다 붙여진 번호로 0부터 시작하여 순차적으로 증가한다.

![image](img/인덱스.png)

- 배열의 값을 저장하고 가져오는 방법은 변수와 같다.
- 단지 변수명 대신 인덱스(index)를 사용한다는점이 다르다.

### Array02클래스 생성하기
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
### 2. 배열의 길이
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
### 3. 배열의 초기값
- 배열은 생성과 동시에 데이터 자료형 별로 기본값이 주어진다.
- 배열을 선언했을 때 저장되는 초기값을 자료형 별로 정리하면 다음과 같다.

|자료형|초기값|
|------|------|
|정수형|0|
|실수형|0.0|
|문자형|''|
|객체형|null|

### Array03클래스 생성하기
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
### Array04 클래스 생성하기
```java
package array;

public class Array03 {
	public static void main(String[] args) {
		//10개의 배열을 생성
		int [] numbers = new int[10];
		
		//배열에 랜덤 함수를 이용해 값을 넣는다.
		for(int i = 0 ; i < numbers.length; i++) {
			numbers[i] = (int)(Math.random()*30)+1;
		}
		
		//배열 안에서 짝수의 합 구하기
		int sum = 0;
		for(int i = 0; i<numbers.length; i++) {
			sum += numbers[i];
		}
		
		//출력해보기
		for(int i = 0 ; i < numbers.length; i++) {
			//numbers배열의 랜덤값 출력
			System.out.print(numbers[i] + " ");
		}
		
		//줄 바꾸기
		System.out.println();
		System.out.println("배열의 짝수들의 합 : " + sum);
	}
}

```
## 배열의 정렬
- 배열의 값이 순서 없이 저장되는 경우, 배열의 값을 오름차순, 내림차순으로 정렬해야 할 때가 있다.
- 정렬 방법에는 다양한 알고리즘이 있다.

### Array05클래스 생성하기
```java
package array;

public class Array04 {
	public static void main(String[] args) {
		int [] arr = {1,6,2,3,10,7,4,8,5,9};
		
		int temp = 0;
		
		for(int i = arr.length - 1; i > 0; i--) {
			for(int j = 0; j < i; j++) {
				//앞의 값이 뒤의 값보다 크다면 정렬
				if(arr[j] > arr[j+1]) {
					//뒤의 값을 임시 변수에 저장
					temp = arr[j+1];
					arr[j+1] = arr[j];
					arr[j] = temp;
				}
			}
		}
		
		System.out.println("정렬 후 출력 : ");
		for(int i = 0 ; i < arr.length; i++) {
			System.out.print(arr[i] + " ");
		}
	}
}

```

## Arrays
- Arrays 클래스는 배열의 복사, 항목 정렬, 항목 검색 등 배열을 다루기 위한 다양한 메서드를 제공한다.
- 지금 당장은 배열의 도우미 기능을 지닌것으로만 생각하자.
- Arrays클래스를 이용하면 배열의 기능을 더욱 쉽게 사용할 수 있다.
- Arrays에 속해있는 기능을 사용할 때는 'Arrays.함수명()'로 작성하여 기능을 호출한다.

### Arrays01클래스 생성하기

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

### Arrays02클래스 생성
 
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
```
int [][] arr = new int [크기][크기];
```

### 2차원 배열은 다양한 방식으로 선언할 수 있는데, 다음과 같이 열을 지정하지 않고 선언할 수 있다.
```java
int[][] arr = new int[크기][];
```
### 열의 크기를 지정하지 않고 선언한 뒤, 각 행의 열을 각각 선언하여 사용할 수 있다.
```java
int[][] arr = new int[3][];
arr[0] = new int[2];
arr[1] = new int[3];
arr[2] = new int[1];
```
```java
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
### 이차원 배열의 초기값 지정
```
int [][] arr = { {1,2},{3,4},{5,6}};
```
- 이와 같은 방법은 배열을 최초 선언할 때만 가능하다.

## 2차원 배열의 구조
- 2차원 배열의 행은 독립된 공간으로 분리되어 있고, 그 행들이 각각 독립된 열을 가지고 있다.

![image](https://user-images.githubusercontent.com/54658614/215390509-ba91a4f5-ca52-41e0-bd32-04be2d2e08d8.png)

### multi_Array01클래스 생성
```java
package array;

public class Multi_Array01 {
	public static void main(String[] args) {
		
		int[][]arr = new int[2][3];
		
		arr[0][0] = 1;
		arr[0][1] = 2;
		arr[0][2] = 3;
		
		arr[1][0] = 11;
		arr[1][1] = 12;
		arr[1][2] = 13;
		
		//행의 주소 출력
		System.out.println("2차원 배열 : " + arr);
		
		//1행이 가진 열에 대한 주소 출력
		System.out.println("2차원 배열 1행 : " + arr[0]);
		
		//행의 크기 출력
		System.out.println("행의 크기 : " + arr.length);
		
		//각 행의 열 크기 출력
		System.out.println("1 행의 열 크기 : " + arr[0].length);
		System.out.println("2 행의 열 크기 : " + arr[1].length);
		
		//1행 1열의 값 출력
		System.out.println("arr[0][0] : " + arr[0][0]);
		
		
		
	}
}

//결과
2차원 배열 : [[I@58ceff1
2차원 배열 1행 : [I@7c30a502
행의 크기 : 2
1 행의 열 크기 : 3
2 행의 열 크기 : 3
arr[0][0] : 1
```
## 2차원 배열의 활용
### Multi_Array02클래스 생성
```java
package array;

public class Multi_Array02 {
	public static void main(String[] args) {
		
		int[][]arr = new int[5][5];
		
		int count = 1;
		
		//1부터 25까지 차례로 배열에 넣는다.
		for(int i = 0; i < 5; i++) {
			for(int j = 0; j < 5; j++) {
				arr[i][j] = count++;
			}
		}
		
		for(int i = 0 ; i < 5; i++) {
			for(int j = 0 ; j < 5; j++) {
				System.out.print(arr[i][j]+" ");
			}
			System.out.println();
		}
	}
}
//결과
1 2 3 4 5 
6 7 8 9 10 
11 12 13 14 15 
16 17 18 19 20 
21 22 23 24 25 
```

### Multi_Array03클래스 생성
- 2차원 배열을 활용한 로또
```java
package array;

import java.util.Scanner;

public class Multi_Array03 {
	public static void main(String[] args) {
		
		//당첨번호 리스트
		int[][] lotto = {{2,6,11,33,42,44},{1,6,17,22,24,33},{7,16,24,33,42,44},{11,27,32,34,43,46},{6,17,22,24,33,41}};
		
		Scanner scan = new Scanner(System.in);
		
		String myNum = "";
		
		boolean isWin = false;
		
		System.out.println("당첨 숫자를 6개 연속으로 입력해주세요 >>> ");
		myNum = scan.next();
		
		for(int i = 0 ; i< lotto.length; i++) {
			String lottoNumber = "";
			//한 행의 번호를 더해서 하나의 숫자로 만든다.
			for(int j = 0 ; j < lotto[i].length; j++) {
				lottoNumber += lotto[i][j];
			}
			if(myNum.equals(lottoNumber)) {
				isWin = true;
				break;
			}
		}
		
		if(isWin) {
			System.out.println(myNum+"번호 당첨");
		} else {
			System.out.println(myNum + "번호는 당점되지 못했습니다.");
		}
		scan.close();
	}
}
//결과
당첨 숫자를 6개 연속으로 입력해주세요 >>> 
2611334244
2611334244번호 당첨
```

## 향상된 for문
- 향상된 for문은 JDK 1.5부터 새롭게 추가된 기능으로 배열과 컬렉션의 모든 요소를 참조하기 위한 반복문이다.

```java
for(자료형 변수 : 배열){
    실행코드
}
```
- for문을 실행할 반복 대상이 있으면 변수는 반복대상이 지닌 자료형과 같은 타입으로 지정해야 한다.
- 반복 대상의 요소를 하나씩 꺼내서 변수에 대입하면서 진행하고, 반복 대상의 길이만큼 꺼내어 반복한다.

### For01클래스 생성하기
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