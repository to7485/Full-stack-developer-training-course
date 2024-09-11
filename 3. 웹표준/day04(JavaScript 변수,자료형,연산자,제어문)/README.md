# JavaScript
- html과 css로 만들어진 웹페이지를 동적으로 만들어주는 프로그래밍 언어

## html에서 JavaScript를 사용하는법
- \<script\> ~ \</script\> 를 사용한다.
- 

### HTML 요소의 생성
|메서드|설명|
|------|---|
|document.createElement(HTML요소)|지정된 HTML 요소를 생성함.|
|document.write(텍스트)|HTML 출력 스트림을 통해 텍스트를 출력함.|

```html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8">
		<title>자바스크립트</title>
		
		<script>
			//자바스크립트를 작성하기 위한 영역
			/**/ 한줄 주석과 여러줄 주석 다 사용이 가능하다.
			document.write("hello javascript");
			//document 객체는 웹 페이지 그 자체를 의미합니다.
			//document.write(텍스트) : HTML출력 스트림을 통해 body에 텍스트를 출력함
		</script>
		
	</head>
	
	<body>
	
	</body>
</html>
```
- \<script\> 태그를 \<head\> 태그와 \<body\> 태그에 각각 넣는 것은 각각 다른 동작을 수행하며 웹 페이지의 동작에 영향을 미친다.

### \<head\> 태그에 \<script\> 넣기
- \<head\> 태그에 위치한 \<script\>는 HTML 문서가 파싱되는 동안에 로드되며, 이는 페이지의 렌더링을 차단할 수 있다.<br>스크립트가 로드되기 전까지는 다른 리소스들이 로딩되지 않는다.
- 자원 초기화 및 설정: 보통 이곳에는 웹 페이지의 초기화 및 설정과 관련된 스크립트를 넣는다.

### \<body\> 태그에 \<script\> 넣기
- \<body\> 태그에 위치한 \<script\>는 페이지의 렌더링이 진행되는 중에 로드되기 때문에, 페이지의 다른 내용들은 먼저 로드되고 렌더링된다.
- 동적 작업 및 이벤트 처리: 보통 이곳에는 동적으로 생성되는 컨텐츠나 이벤트 처리와 관련된 스크립트를 위치시킵니다.
- 일반적으로는 초기화 스크립트를 \<head\>에, 나머지는 \<body\>에 위치시키는 것이 일반적인 방법입니다.

## variable(변수)와 ValueType(자료형)
- JavaScript에서 변수를 만들 때 앞에다가 따로 명시하지 않습니다.
```html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8">
		<title>자바스크립트의 자료형</title>
		<script type="text/javascript">
		//자바스크립트의 자료형
		//var,let,const
		//var : 같은 이름의 변수가 만들어졌을 때를 감지하지 못한다.
		//let : 같은 이름의 변수가 만들어졌을때를 감지한다(mutable) 값을 새롭게 대입은 가능
		//const : 일종의 상수와 같은 자료형(immutable) 값 다시 대입 불가능
				
		//각각의 자료형을 나타내는 키워드가 따로 존재하지 않는다.	
		let i1 = 10;
		let i2 = 20;
	    

	        var num1 = 100;
	        var num2 = 200;
	        var num3 = "100 + 200 : " + (num1 + num2); //문자열
     
		document.write(num3+"<br>");
		
		num3 = 50; //다시 정수로 바뀜
			
		document.write(num3+100);
		
		num3 = 10 / 3;
		
		document.write("10 / 3 : " + num3 + "<br>");
		
		//자바스크립트는 문자열과 문자의 구별이 없다.
		document.write("안녕하세요<br>");
		document.write('안녕하세요<br>');

	      </script>
	</head>
	<body>
	
	</body>
</html>
```
### var, let, const의 차이
- 차이에 앞서 스코프와 호이스팅에 대해 알아야 한다.

#### 스코프
- 식별자(변수명,함수명,클래스명등)의 유효범위를 말한다.
- 전역에 선언된 전역변수는 하위 모든곳에서 참조가 가능하다.
- 지역에 선언된 지역변수는 해당 지역과 하위 지역에서만 참조가 가능하다.
- var은 함수에서만 지역변수가 되는 함수레벨 스코프를 갖고있다.
```js
function a() {
  var variable = 1;
}
console.log(variable) // ReferenceError: variable is not defined

if (true) {
  var variable = 1;
}
console.log(variable) // 1
```
- let과 const는 블록레벨 스코프를 가져 모든 코드블록에서 지역스코프를 가진다.
```js
function a() {
  const constance = 1;
}
console.log(constance) // ReferenceError: constance is not defined

if (true) {
  let string = '';
}
console.log(string) // ReferenceError: string is not defined
```

#### 호이스팅
- 자바스크립트 엔진은 소스코드를 한 줄씩 읽으며 순차적으로 실행하기 전에 변수 선언을 포함한 모든 선언문을 찾아내어 먼저 실행한다.
- 마치 함수안의 선언들을 모두 끌어올려 해당 함수 유효 범위 최상단에 선언된 것과 같은 특징을 <b>호이스팅</b>이라고 한다.
- 모든 식별자(변수, 함수, 클래스등)는 호이스팅이 되어 먼저 선언된다.

##### 변수의 호이스팅
- 변수는 크게 '변수 선언'과 '값 할당'으로 이루어진다.
```js
let a; //변수 선언
a = 1; //값 할당
```
- <b>선언단계</b> : 변수 이름을 등록해서 자바스크립트가 엔진에 의해 변수의 존재를 알린다.
- <b>초기화 단계</b> : 값을 저장하기 위한 메모리 공간을 확보하고 암묵적으로 undifined를 할당해 초기화한다.

- <b>var</b>로 선언한 변수의 경우 호이스팅 시 undifined로 변수를 초기화까지 해준다.
```js
console.log(a); //undifined
var a;
```
- <b>let</b>은 선언단계와 초기화 단계가 분리되어 진행된다.
- 선언 단계는 런타임 이전에 변수 선언문에서 이루어진다.
- 초기화 단계는 런타임 이후에 변수 선언문에서 이루어진다.
```js
console.log(b); //ReferenceError: Cannot access 'b' before initialization
let b; //여기서 초기화 단계 실행, b에 undefined를 암묵적으로 할당
console.lob(b); //undifined
```
- <b>const</b>는 선언과 동시에 초기화해야한다.
- 그렇지 않으면 다른 에러가 출력된다.
```js
const c; // SyntaxError: Missing initializer in const declaration
console.log(c);

//ReferenceError가 아닌 SyntaxError이다. 문법적으로 옳지 않다는 뜻이다.

console.log(c); //ReferenceError: Cannot access 'c' before initialization
const c = 1;
```
- 문법을 지켜서 c가 자바스크립트 엔진에 등록은 됐지만
- 초기화 단계는 런타임 이후 변수 선언문에서 이루어지기 때문이다.
- 그러므로 let과 const는 Scope의 시작 위치에서 선언하는게 좋다.


### 변수에 저장할 수 있는 자료형
- <b>문자형(String)</b> : var 변수 = "사용할 문자나 숫자"; 
- <b>숫자형(Number)</b> : var 변수 = 숫자; 또는 Number(”문자와 숫자”);
- <b>논리형(Boolean)</b>
	- var 변수 = true 또는 false; Boolean(데이터);
	- false - false, 0, null, '', undefined
- <b>null</b> : 변수의 값이 비어 있다는 것을 표시할 경우 
- <b>undefined</b> : 
	- 변수가 선언되었을때 값이 지정되지 않았을 경우
	- 변수를 선언하면 기본값은 undefined 입니다.

- <b>자료형 체크</b> : typeof 변수 또는 데이터
- <b>객체(Object)</b>
- **원시값** : 객체 이외의 값(숫자, 문자, 논리값, null, undefined, ""(빈값)

## Operator(연산자)
- 산술연산자 
	- 더하기(+), 빼기(-), 곱하기(\*), 나누기(/), 나머지(%)
- 문자 결합 연산자
	- 여러개의 문자를 하나의 문자형 데이터로 결합할 때 사용
	- 더하기에 피연산자로 문자형 데이터가 한 개라도 포함되어 있으면 다른 피연산자의 데이터는 자동으로 문자형 데이터로 형 변환되고 문자 결합이 이루어져 하나의 문자형 데이터로 반환
	```javascript
	"Text1 " + "Text2" = "Text1 Text2";
	"100" + 200 = 100200;
	100 + "200" = 100200;
	```
- 대입연산자
	- 연산된 데이터를 변수에 저장할 때 사용
	```javascript
	A = B
	A = 1 + 2
	```
	
	- 복합대입연산자 : 산술연산자 + 대입연산자
	<table>
		<tbody>
			<tr>
				<td>A += B</td>
				<td>A = A + B</td>
			</tr>
			<tr>
				<td>A *= B</td>
				<td>A = A * B</td>
			<tr>
			<tr>
				<td>A /= B</td>
				<td>A = A / B</td>
			</tr>
			<tr>
				<td>A %= B</td>
				<td>A = A % B</td>
			</tr>
		</tbody>
	</table>
	
	- 문자형 데이터 결합
	```javascript
	  var str = "<table border='1'>";
	  str += "<tr>";
	  str += "<td>1</td><td>2</td><td>3</td>";
	  str += "</tr>";
	  str += "</table>";
			
	  document.body.innerHTML = str;
	```
- 증감연산자
	- 증가연산자(++) - 숫자형 데이터를 1씩 증가
	```
	변수++; 또는 ++변수;
	```
	- 감소연산자(--) - 숫자형 데이터를 1씩 감소
	```
    변수--; 또는 --변수; 
	```
	- var a = ++b;   b를 1 증가 시킨 후 a에 대입
	- var a = b++;   a에 대입 후 b를 1 증가 
	
- 비교연산자 
	- 두 데이터를 '크다', '작다', '같다'와 같이 비교할때 사용
	- 연산된 결과는 논리형데이터(true - 참, false - 거짓)
	
|종류|설명||
|----|------|----------|
|A > B|||
|A < B|||
|A >= B|||
|A <= B|||
|A == B|A와 B는 같다|데이터 일치 여부만 체크( 10 == "10" -> true)|
|A != B|A와 B는 다르다|데이터 불일치 여부만 체크( 10 != "10" ->  false)|
|A === B|A와 B는 같다|데이터 일치 + 데이터 종류 일치 여부 체크(10 === "10" --> false)|
|A !== B|A와 B는 다르다|데이터 불일치 + 데이터 종류 불일치 여부 체크(10 !== "10" --> true)|

- 논리연산자

|종류|설명|
|-----|--------|
|\|\||OR 연산자, 비교하는 대상 중 하나라도 true면 true가 됨|
|&&|AND 연산자, 비교하는 대상 모두 true일때 true, 그렇지 않다면 false|
|!|not 연산자, 피 연산자의 값을 반대로 바꿈, true -> false, false -> true|

- 연산자 우선순위
	- 아래에서 위로 우선순위가 높아짐
	- 1. () 
	- 2. 단항 연산자(--, ++, !)
	- 3. 산술 연산자(\*, /, %, +, -)
	- 4. 비교 연산자(>, >=, <, <=, ==, ===, !=, !==)
	- 5. 논리 연산자(&&, ||)
	- 6. 대입(복합 대입)연산자(=, +=, -=, \*=, /=, %=)
	```
	  예) ++A * B <= C
		 단항 연산자 ++A
		 * B 
	  C와 비교(<=)
	```
- 삼항 조건 연산자
	- 조건식? 조건식이 true일때 : 조건식이 false 일때
	- var a = (b > 2)?”2 보다 크다”:”2보다 작거나 같다”;
```
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8">
		<title>자바스크립트 산술연산자</title>
		<script type="text/javascript">
		var a = 10;
		var b = 3;
		var result = 0;
		
		
		//비교연산자
		result = a > b; //결과 : true
		//자바에서 다룰수 있는 타입은 자바스크립트에서도 다 다룰 수 있다.
		document.write("a > b : " , result , "<br>");
		
		result = a == b;
		document.write("a == b : " , result , "<br>");
		
		result = a != b;
		document.write("a != b : " , result , "<br>");
		
		result = 5;
		result += a; //+=, -=,*=, /=, %=
		document.write("+= : " + result,'<br>');
		
		document.write("<hr>");
		
    var num1 = 10;
		var num2 = 20;
		
		document.write(++num1,'<br>');
		document.write(num2++,'<br>');
    
    document.write("<hr>");
		
		var age = 20;
		result = age > 20 && age < 30;
		alert(result);
		
		document.write("<hr>");
		
		var kor = 100;
		var eng = 77;
		var math = 65;
		
		result = (kor + eng + math) / 3;
		
		alert(result.toFiexed(2));
		
		
		</script>
	</head>
	<body>
	
	</body>
</html>
```
## 조건문

### if
- 조건식의 값이 참(true), 거짓(false)인지에 따라 제어
```javascript
   if (조건식) {
     // 처리할 내용
 } 
```
```javascript
	if (조건식) {
   
	} else { // 조건식이 false 일때 
		// 처리할 내용
	}
```
```javascript
	if (조건식1) {
	} else if (조건식2) { // 조건식1이 false일때 
	
	} else if (조건식3) { // 조건식1, 조건식2가 false 일때
 
	} else { // 조건식1, 조건식2, 조건식3이 false 일때 
	}
```   
- 조건식에서 false가 되는 기타 데이터<br>
   **0, null, ""(빈문자), null, undefined는 false로 인식**을 하고 **그 이외의 값은 true로 인식**
   
- 조건식을 여러개 사용할 경우 논리연산자 사용
	- **조건식1|| 조건식2** : 조건식1이 참이거나 조건식2가 참일때
  
	- **조건식1 && 조건식2** : 조건식1과 조건식2가 모두 참일때
    
- if문 안에 if 문을 중첩해서 사용할 수 있다.

### switch문
- 여러개(case) 중에서 하나를 선택
```javascript
var 변수 = 초기값;
switch (변수) {
	case 값1 : 코드1;
		break;
	case 값2 : 코드2;
		break;
	case 값3 : 코드3;
		break;
	case 값4 : 코드4;
		break;
	default : 코드5;	
}
```     
- 변수에 할당된 값이 case의 각 값에 매칭되면 매칭된 코드가 실행 됩니다.
- 최종적으로 매칭되는 값이 없는 경우는 default 부분의 코드5가 실행됩니다.
- 각 case에서 break가 없다면 다음 case로 넘어값니다. 
```     
	case 값1: 코드1; 
	case 값2: 코드2;
		break     
```     
- 값1로 매칭이 되면 코드1, 코드2가 실행이 됩니다.

## 반복문

### for문
```
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8">
		<title>for문</title>
		
		<script type="text/javascript">
			var dan = 8;
			
			for(var i = 1; i < 10; i++){//초기식에 int로 쓰지 않게 주의하기
				document.write(dan,"X",i,"=",dan*i,"<br>");
			}
			
			document.write("<hr>");
			
			for(var i = 6; i >= 1; i--){ // 태그를 만드는것도 가능하다.
				document.write('<h',i,'>','자바스크립트','</h',i,'>');
			}
			
			document.write("<hr>");
			
			document.write("<ul>");
			for(var i = 0; i < 3; i++){
				document.write("<li>안녕</li>");
			}
			document.write("</ul>");
			
		</script>
	</head>
	
	<body>
	</body>
</html>
```
![image](https://user-images.githubusercontent.com/54658614/228737008-4b4db81b-5fc0-47fa-8d4b-da3bec385ebd.png)

### while문
```javascript
while (조건식) {
	// 조건식이 true일때 반복 실행되는 부분 
}
```
- while구분에서는 반복 구간을 탈출할 수 있는 조건을 반드시 구현해야 합니다.(없을 경우 무한 loop) 
- 탈출 키워드 (while, do~while, for)
	- **break** : 반복을 종료
	- **continue** : 현재 반복 실행을 종료 하고 다음 반복 실행으로 넘어감
	```javascript
	var num = 0;     
	while (num < 1000) { 
		if (num >= 100) break;  // 반복횟수가 100이상이면 멈춤     
		num++;
	}
	```
### do ~ while 문
do {  }로 정의된 반복 실행을 적어도 1번은 실행하고 while 조건식에 따라 반복
```javascript
var 변수 = 초기값; 
do {
	// 최소 한번 이상 실행되는 반복 처리
} while(조건식);
```
```javascript
var num = 10;
do {
	console.log(num); // 10
    num++;
} while (num < 10);
```
* * * 
# ECMAScript 6 부터 추가된 데이터 타입
## 심벌
심벌은 ECMAScript6 부터 추가된 원시 값입니다. 심벌은 자기 자신을 제외한 그 어떤 값과도 다른 유일무의한 값입니다.

### 심벌의 생성
심벌은 Symbol()을 사용해서 생성합니다.
```javascript
var sym1 = Symbol();
```
Symbol()은 호출할 때마다 새로운 값을 만듭니다. 이를 확인하기 위해 또 다른 심벌을 생성해 보겠습니다.
```javascript
var sym2 = Symbol();
```
다음처럼 sym1 값과 sym2 값이 다르다는 사실을 확인할 수 있습니다.
```javascript
console.log(sym1 == sym2); // false
```
또한 Symbol()에 인수를 전달하면 생성된 심벌의 설명을 덧붙일 수 있습니다.
```javascript
var HEART = Symbol("하트");
``` 
심벌의 설명은 toString() 메서드를 사용해서도 확인할 수 있습니다.
```javascript
console.log(HEART.toString()); // Symbol(하트)
```
예를 들어 오셀로 케임을 만들 때 칸의 상태를 값으로 표현하는 코드를 작성한다고 가정해 보면 다음과 같이 칸의 상태를 숫자와 같은 값으로 표현할 수 있습니다.
```javascript
var NONE = 0; 
var BLACK = -1;
var WHITE = 1;
```

이 코드에서 숫자 자체의 특별한 의미가 없습니다. 칸의 상태를 cell 변수에 저장한다고 가정했을 때, cell 값을 확인하려면 cell == WHITE라고 작성해야 프로그램이 읽기 쉬워질 것입니다. 게다다 cell == 1이라고 작성해도 아무런 문제없이 동작합니다. 그러나 이러한 행위는 프로그램을 읽기 어렵게 만들므로 바람직하지 않습니다. **심벌을 활용하면 앞의 코드를 다음처럼 고칠 수 있습니다.**
```javascript
var NON = Symbol("none");
var BLACK = Symbol("black");
var WHITE = Symbol("white");
```
**심벌은 유일무이한 값입니다.** 따라서 이렇게 수정하면 변수 cell 값을 확인할 때 NONE, BLACK, WHITE만 사용하도록 제한할 수 있습니다.

### 심벌과 문자열 연결하기
Symbol.for()를 활용하면 문자열과 연결된 심벌을 생성할 수 있습니다.
```javascript
var sym1 = Symbol.for("club");
```
그러면 전역 레지스트리에 심벌이 만들어집니다. 또한 전역 레지스트리에서 그 심벌을 위에 지정한 문자열로 불러올 수 있습니다.
```javascript
var sym2 = Symbol.for("club");
console.log(sym1 == sym2); // true
```
이 기능을 활용하면 코드의 어느 부분에서도 같은 심벌을 공유할 수 있습니다. 심벌과 연결된 문자열은 Symbol.keyFor()로 구현할 수 있습니다.
```javascript
var sym1 = Symbol.for("club");
var sym2 = Symbol("club");
console.log(Symbol.keyFor(sym1)); // club
console.log(Symbol.keyFor(sym2)); // undefined
```

## 템플릿 리터럴
- 템플릿 리터럴은 ECMAScript6 부터 추가된 문자열 표현 구문입니다. 
- 템플릿이란 이부만 변경해서 반복하거나 재사용할 수 있는 틀을 말합니다. 템플릿 리터럴을 사용하면 표현식의 값을 문자열에 추가하거나 여러 줄의 문자열을 표현할 수 있습니다. 

### 기본적인 사용법
템플릿 리터럴은 역따옴표(\`)로 묶은 문자열입니다. 간단한 템플릿 리터럴은 큰 따옴표 또는 작은 따옴표로 묶은 문자열과 모습이 같습니다.
```javascript
`I'm going to learn Javascript.`
```
문자열 리터럴에서 줄 바꿈 문자를 표현할 때는 이스케이프 시퀀스(\n)를 사용했지만, 템플릿 리터를을 사용하면 일반적인 줄 바꿈 문자를 사용할 수 있습니다.
```javascript
var t =`Main errs as long as 
he strives.`;
```
이 문자열을 문자열 리터럴로 표현하면 다음과 같은 모습이 됩니다.
```javascript
var t ="Main errs as long as\nhe strives.";
```
물론 템플릿 리터럴에서도 이스케이스 시퀀스를 사용할 수 있습니다.
```javascript
var t =`Main errs as long as\nhe strives.`;
```
이스케이프 시퀀스 문자를 그대로 출력하려면 템플릿 리터럴 앞에 String.raw를 붙입니다.
```javascript
var t =String.raw`Main errs as long as\nhe strives.`;
```
이 문자열을 문자열 리터럴로 표현하면 다음과 같은 모습이 됩니다.
```javascript
var t ="Main errs as long as\\nhe strives.";
```
> 템플릿 리터럴 앞에 붙은 String.raw는 태그 함수라고 부릅니다.
### 보간 표현식
- 템플릿 리터럴 안에는 플레이스 홀더를 넣을 수 있습니다. 플레이스 홀더는 ${...}로 표기합니다.
- 자바스크립트 엔진은 플레이스 홀더 안에 든 ... 부분을 표현식으로 간주하여 평가(evaluation)합니다. 이를 활용하여 문자열 안에 변수나 표현식의 결과값을 삽입할 수 있습니다.
```javascript
var a = 2, b = 3;
console.log(`${a} + ${b} = ${a+b}`);
var now = new Date();
console.log(`오늘은 ${now.getMonth() + 1}월 ${now.getDate()}일 입니다.`);
```
- 모든 코드에서 ${} 안에 든 표현식이 평가되어 문자열로 바뀌었다는 사실을 확인할 수 있습니다.
- ECMAScript5 까지는 문자열에 변수 값을 삽입할 때 더하기(+) 연산자로 문자열을 연결하는 방법을 사용했지만 보간 표현식을 활용하면 좀 더 알아보기 쉽게 작성할 수 있습니다.

>**플레스이 홀더**<br>플레이스 홀더는 실제 내용물을 나중에 삽입할 수 있도록 확보한 장소라는 뜻으로 쓰입니다. 프로그래밍 언어에서 플레이스 홀더는 사용자의 입력 값처럼 실행 시점에 외부에서 주어지는 값을 표현식에 반영하고자 할 때 그것이 들어갈 수 있도록 마련한 장소를 뜻합니다.

