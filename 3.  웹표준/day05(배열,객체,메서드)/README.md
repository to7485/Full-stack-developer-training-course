# Array(배열)
```html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8">
		<title>배열</title>
		<script type="text/javascript"> /*type="text/javascript" 는 이전버전과의 호환 때문에 있는 코드, 없어도 상관 없다.*/
			var arr = new Array(3); /* 배열을 만드는 순간에는 어떤 자료형의 데이터를 담을지 알 수 없다. */
			arr[0] = 10;
			arr[1] = 20;
			arr[2] = "안녕" /* 자바에서는 상상도 할 수 없는 내용 */
			arr[3] = 3.14; /* 방이 모자라면 더 만들어버림 */
			
			/* 자바에서의 배열의 생성 및 초기화
			int[]arr = {1,2,3}*/
			
			/* 자바스크립트에서의 배열의 생성 및 초기화
			var arr = [10,20,'안녕',3.14]*/
			
			for(var i = 0; i<arr.length; i++) {
				//document.write(arr[i] +"<br>");
				document.write(`${arr[i]}<br>`);
			}
		</script>
		
	</head>
	
	<body>
	
	</body>
</html>
```
# 객체
- 실생활에서 우리가 신식할 수 있는 사물로 이해할 수 있다.
- 자바스크립트의 기본타입(data type)은 객체(object)이다.
- 객체란 키(key)와 값(value)로 구성된 프로퍼티(property)의 정렬되지 않은 집합이다.
- 프로퍼티의 값으로 함수가 올 수도 있는데, 이러한 프로퍼티를 메서드(method)라고 한다.

## 객체의 생성
- 자바스크립트에서 객체를 생성하는 방법은 세가지가 있습니다.
  
### 1.객체 리터럴
- 자바에서는 클래스를 만들고 클래스를 통해서 객체를 만들었지만 자바스크립트에서는 변수처럼 정의가 가능하다.
- 키(key) : 변수와 거의 비슷한 속성
  - 이름 짓는 규칙이 비슷하다.
- 값(value) : 원시타입(숫자,문자,null,undifined, false, true),객체(객체의 값으로 객체가 들어올 수 있다.)

```js
var 객체이름 = {
    프로퍼티1이름 : 프로퍼티1의값,
    프로퍼티2이름 : 프로퍼티2의값,
    ...
};

var kitty = {
	name: "나비",
	family: "코리안 숏 헤어",
	age: 1,
	weight: 0.1
};

document.write("우리 집 새끼 고양이의 이름은 " + kitty.name + "이고, 종은 " + kitty.family + "입니다.");
```
#### js_object.html 생성하기
```html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8">
		<title>Insert title here</title>
		<script type="text/javascript">
			var person = { name : "홍길동", age: 30};
			//객체를 출력하는법
			document.write('person.name : ',person.name+"<br>");
			document.write('person.age : ',person.age+"<br>");
			document.write("<hr>");
			
			document.write("person['name'] : ",person['name'],"<br>");
			document.write("person['age'] : ",person['age']+"<br>");
			document.write("<hr>");
			
			//없는 속성에 값만 넣으면 객체에 추가가 된다.
			person.bt = 'AB';
			document.write("person['bt'] : ",person['bt'],"<br>");
			document.write("<hr>");
			
			//객체에서 속성 삭제하기
			//delete 연산자를 사용하면 object의 property를 삭제할 수 있다.
			//이때 피연산자는 property의 key여야 한다.
			delete person.bt;
			document.write('bt : ' + person['bt']+"<br>");
			document.write("<hr>");
			
			//속성이 객체에 속해있는지 확인하는법 : in -> 결과는 true , false로 반환
			document.write('name in person : '+('name' in person));
			document.write("<hr>");


			//for-in문을 사용하면 객체(배열 포함)에 포함된 모든 프로퍼티에 대해 루프를 수행할 수 있다.
			//i에 객체의 프로퍼티 이름이 반환된다. 단, 순서는 보장되지 않는다.
			for(i in person){
				document.write(`${i} = ${person[i]}<br>`);
			}
			document.write("<hr>");
			
			//새로운 객체에 기존 객체를 참조 시킬수 있다. 주소값을 복사해오기 때문에 person의 속성값을 변경하면 같이 바뀐다.
			var person2 = person;
			
			person.age = 40;
			
			document.write('person2.age : ',person2.age); //결과 40

			//객체 안에 객체가 들어갈 수 있다.
			var circle = {
			  center : {x : 1.0, y: 2.0},
			radius : 2.5
					}
			document.write("<hr>");
			
			document.write('circle.center.x : ',circle.center.x,' circle.center.y : ',circle.center.y+"<br>");
			document.write('circle.radius : ',circle.radius+"<br>");
			document.write("<hr>");
				
				
			//객체 안에 함수가 들어갈 수 있다.
			var person = {
					name : "홍길동",
					age : 30,
					getInfo : function(){
						document.write('이름 : ',this.name,"<br>",'나이 : ',this.age,"<br>");
					}
			};
							
			//함수의 호출
			person.getInfo();
			
		</script>
	</head>
	<body>
	
	</body>
</html>
```
### 2.생성자를 이용한 객체의 생성
- 자바스크립트는 prototype 기반 객체지향 프로그래밍 언어이다.
- 따라서 자바스크립트의 동작 원리를 이해하기 위해서는 prototype의 개념을 이해해야 한다.
- prototype기반 객체지향 프로그래밍 언어는 클래스 없이(Class-less)도 객체를 생성할 수 있다.
- 메서드를 생성자 처럼 사용하여 새롭게 생성되는 객체를 초기화 하는 역할을 한다.

### 상속
- 자바스크립트에서는 현재 존재하고 있는 객체를 프로토타입으로 사용하여, 해당 객체를 복제하여 재사용하는 것을 상속이라고 한다.

### prototype
- 자바스크립트의 모든 객체는 자신의 부모 역할을 담당하는 객체와 연결되어 있다.
- 이것은 마치 객체 지향의 상속 개념과 같이 부모 객체의 property 또는 method를 상속받아 사용할 수 있게 한다.
- 이러한 부모 객체들을 Prototype객체 또는 줄여서 Prototype이라고 한다.

```js
var student = {
  name: 'Lee',
  score: 90
};

// student에는 hasOwnProperty 메소드가 없지만 아래 구문은 동작한다.
console.log(student.hasOwnProperty('name')); // true

//console.dir() : 요소를 트리구조로 출력
//js객체의 전체 구조를 보려고 할때 유용하다.
console.dir(student);
```

![image](image/printout_student_obj_from_chrome.png)

#### 2.1 Object 생성자 함수
- new 연산자와 Object생성자 함수를 호출하여 빈 객체를 생성할 수 있다.
- 빈 객체 생성 후 프로퍼티 또는 메서드를 추가하여 객체를 완성하는 방법이다.

```js
// 빈 객체의 생성
var person = new Object();
// 프로퍼티 추가
person.name = 'Lee';
person.gender = 'male';
person.sayHello = function () {
  console.log('Hi! My name is ' + this.name);
};

console.log(typeof person); // object
console.log(person); // {name: "Lee", gender: "male", sayHello: ƒ}

person.sayHello(); // Hi! My name is Lee
```

#### 2.2 생성자 함수
- 객체 리터럴과 Object 생성자 함수 방식으로 객체를 생성하는 것은 property 값만 다른 여러 개의 객체를 생성할 때 불편하다.
- 동일한 프로퍼티를 갖는 객체임에도 불구하고 매번 같은 프로퍼티를 기술해야 한다.
- 생성자 함수를 사용하면 마치 객체를 사용하기 위한 클래스 처럼 사용하여 프로퍼티가 동일한 여러 객체를 간편하게 생성할 수 있다.
```js
// 생성자 함수
function Person(name, gender) {
  this.name = name;
  this.gender = gender;
  this.sayHello = function(){
    console.log('Hi! My name is ' + this.name);
  };
}

// 인스턴스의 생성
var person1 = new Person('Lee', 'male');
var person2 = new Person('Kim', 'female');

console.log('person1: ', typeof person1);
console.log('person2: ', typeof person2);
console.log('person1: ', person1);
console.log('person2: ', person2);

person1.sayHello();
person2.sayHello();
```
- 생성자 함수의 이름은 일반적으로 대문자로 시작한다.(메서드 중에서 생성자라는것을 인식하는데 도움이 된다.)
- property 또는 methodName 앞에 쓴 this는 생성자 함수가 생성할 instance를 가리킨다.
- this에 binding되어있는 property와 method는 기본적으로 public 이므로 외부에서 참조 가능하다.
- constructorMethod 내에서 선언된 일반 변수는 private이 되어 외부에서 참조가 불가능하다.

```js
function Person(name, gender) {
  var married = true;         // private
  this.name = name;           // public
  this.gender = gender;       // public
  this.sayHello = function(){ // public
    console.log('Hi! My name is ' + this.name);
  };
}

var person = new Person('Lee', 'male');

console.log(typeof person); // object
console.log(person); // Person { name: 'Lee', gender: 'male', sayHello: [Function] }

console.log(person.gender);  // 'male'
console.log(person.married); // undefined
```

# 함수
- 일련의 처리를 하나로 모아 언제든 호출할 수 있도록 만들어 놓은것
- 수학 함수와 비슷
- 함수의 입력 값을 인수, 함수의 출력 값을 반환값
```javascript 
function 함수명 (인수) {   
	처리 로직 
 
   return 출력 반환값
}
```
## 함수 선언문으로 함수 정의하기
- 함수는 function 키워드를 사용해서 정의
```javascript
function square(x) {    
	var result = x * x; 
	
	return result; 
}  
``` 
- square - 함수 이름
- x - 인수
- var result = x \* x - 처리 로직 
- return result - 처리 후 반환값 
- 참조) 함수명 캐멀 표기법

## 함수 호출
함수를 호출하려면 함수 이름 뒤에 소괄호 인수를 묶어 입력
```javascript
square(3); // 9
```
## 인수
- 함수는 인수를 여러 개 받을 수 있음
- 인수가 여러 개라면 인수와 인수를 쉼표(,)로 구분
```javascript
function add(a, b) {   
	var c = a + b;
	return c;
}
```
- 인수를 받지 않는 함수도 정의할 수 있음
```javascript
function bark() {    
	alert("멍멍"); 
};
bark(); // 멍멍 
alert(bark()); // undefined - 반환값이 없으므로
```

## 함수의 실행흐름
- 호출된 코드에 있는 인수가 함수 정의문에 대입된다. 
- 함수 정의문의 중괄호 안에 작성된 플그램이 순차적으로 실행된다.
- return 문이 실행되면 호출된 코드로 돌아간다. return 문의 값은 함수의 반환값이 된다.
- return 문이 실행되지 않은 상태로 마지막 문장이 실행되면, 호출한 코드로 돌아간 후에 
- undefined가 함수의 반환값이 된다.

### 함수 선언문의 호이스팅
- 자바스크립트 엔진은 변수 선언문과 마찬가지로 함수 선언문을 프로그램의 첫머리로 끌어올림
- 따라서 함수 선언문은 프로그램 어떤 위치에서도 작성할 수 있다.

```javascript
alert(square(5)); // 25 
function square(x) {  return x * x; }
``` 
## 미리 정의된 전역함수
- 자바스크립트는 사용자의 편의를 위해 다양한 기능의 여러 전역 함수를 미리 정의하여 제공한다.
- 이러한 전역 함수는 자바스크립트의 어떤 타입의 객체에서도 바로 사용할 수 있다.

### eval()
- eval()함수는 문자열로 표현된 자바스크립트 코드를 실행하는 함수이다.
```js
var x = 10, y = 20;
var a = eval("x+y"); //30
var b = eval("y*3"); //60
document.write(`${a} <br> ${b}`);
```

### isFinite()
- isFinite()함수는 전달된 값이 유한한 수인지를 검사하여 그 결과를 반환한다.
- 만약 인수로 전달된 값이 숫자가 아니라면, 숫자로 변환하여 검사한다.
```html

isFinite(123)
isFinite(123e100)
isFinite(0)
isFinite(true)
isFinite(false)
isFinite(null)
isFinite("123")
isFinite("")
isFinite("문자열")
isFinite(undefined)
isFinite(NaN)

```

### isNaN()
- isNaN() 함수는 전달된 값이 NaN인지를 검사하여 그 결과를 반환합니다.
- 만약 인수로 전달된 값이 숫자가 아니라면, 숫자로 강제 변환하여 검사합니다.
```js
isNaN(123);       // false
isNaN(123e100);   // false
isNaN(0);         // false
isNaN(true);      // false
isNaN(false);     // false
isNaN(null);      // false
isNaN("123");     // false
isNaN("");        // false

isNaN("문자열");  // true
isNaN(undefined); // true
isNaN(NaN);       // true
```
### parseFloat(), parseInt()
- arseFloat() 함수는 문자열을 파싱하여 부동 소수점 수(floating point number)로 반환합니다.
- parseInt() 함수는 문자열을 파싱하여 정수로 반환합니다.
```js
parseFloat("123");        // 123
parseFloat("123.000");    // 123
parseFloat("123.456");    // 123.456
parseFloat("12 34 56");   // 12
parseFloat(" 123 ");      // 123
parseFloat("123 초콜릿"); // 123
parseFloat("초콜릿 123"); // NaN

-----------------------------------------------------------
parseInt("123");        // 123
parseInt("123.000");    // 123
parseInt("123.456");    // 123
parseInt("12 34 56");   // 12
parseInt(" 123 ");      // 123
parseInt("123 초콜릿"); // 123
parseInt("초콜릿 123"); // NaN

//두번째 인수로 특정 진법을 전달하면, 해당 진법에 맞는 정수로 반환한다.
//전달받은 문자열의 시작이 "0x"로 시작하면, parseInt()함수는 해당 문자열을 16진수로 인식한다.
parseInt("10", 10);     // 10
parseInt("10", 8);      // 8
parseInt("10", 16);     // 16
parseInt("0x10");       // 16
```

### encodeURI(),encodeURIComponent()
- encodeURI() 함수는 URI에서 주소를 표시하는 특수문자를 제외하고, 모든 문자를 이스케이프 시퀀스(escape sequences) 처리하여 부호화한다.
- encodeURIComponent() 함수는 URI에서 encodeURI() 함수에서 부호화하지 않은 모든 문자까지 포함하여 이스케이프 시퀀스 처리한다.

```js
var uri = "http://google.com/search.php?name=홍길동&city=서울";
var enc1 = encodeURI(uri);
var enc2 = encodeURIComponent(uri);
document.write(enc1 + "<br>" + enc2);
```

### Number()
- Number() 함수는 전달받은 객체의 값을 숫자로 반환합니다.
```js
Number("123");        // 123
Number("123.000");    // 123
Number("123.456");    // 123.456
Number("12 34 56");   // NaN
Number("123 초콜릿"); // NaN

Number(true);         // 1
Number(false);        // 0
Number(new Date());   // 현재 날짜에 해당하는 숫자를 반환함.
Number(null);         // 0
```

### String()
- String() 함수는 전달받은 객체의 값을 문자열로 반환합니다.
```js
String(123);        // 123
String(123.456);    // 123.456
String("123");      // 123
String(new Date()); // 현재 날짜에 해당하는 문자열을 반환함.
String(null);       // null

String(true);       // true
String(false);      // false
String(Boolean(1)); // true
String(Boolean(0)); // false
```



# HTML 요소의 선택
- 자바스크립트로 HTML 요소를 제어하려면 그 전에 제어하고자 하는 요소 객체를 먼저 가져와야 합니다.
- 물론 Document 객체의 DOM 트리를 타고 올라가 요소 객체를 가져오는 방법도 있지만 Document 객체는 이보다 편리하게 요소 객체를 가져올 수 있는 메서드가 마련되어 있습니다.


|메서드|설명|
|------|---|
|document.getElementsByTagName(태그이름)|해당 태그 이름의 요소를 모두 선택함.|
|document.getElementById(아이디)|해당 아이디의 요소를 선택함.|
|document.getElementsByClassName(클래스이름)|해당 클래스에 속한 요소를 모두 선택함.|
|document.getElementsByName(name속성값)|해당 name 속성값을 가지는 요소를 모두 선택함.|
|document.querySelectorAll(선택자)|해당 선택자로 선택되는 요소를 모두 선택함.|

### id 속성으로 노드 가져오기
- HTML 문서의 요소에는 id 속성을 지정할 수 있습니다.
- id 속성 값은 문서에서 유일한 값이어야 합니다. 따라서 id 속성 값으로 요소 하나를 가리킬 수 있습니다.

```javascript
document.getElementById(id 값);
```

### 태그이름으로 노드 가져오기
- 인수로 넘긴 문자열과 같은 이름을 가진 태그 목록을 가져올 수 있습니다. 인수로는 태그 이름을 넘깁니다.
- 태그 이름은 대소문자를 구별하지 않습니다.
- getElementsByTagName 메서드는 반환값이 복수개의 요소 입니다. 이것은 일반적인 HTML 문서에는 이름이 같은 태그가 많이 사용되기 때문입니다. 
- getElementsByTagName 메서드는 NodeList 객체를 반환합니다. NodeList 객체는 유사 배열 객체이며 읽기 전용입니다. 
- 요소 이름 대신 와일드카드(\*)를 지정할 수도 있습니다. 이 경우에는 NodeList에 HTML 문서 안의 모든 요소를 담아서 반환합니다.

```javascript
document.getElementsByTagName(요소의 태그 이름)[index];
```

### class 속성 값으로 노드 가져오기
- class 속성 값은 0개 이상의 식별자(클래스 이름)를 CSS에서 사용하는 공백 문자(공백, 탭 등)로 연결한 문자열로 표기합니다.
- 이 class 속성으로 class 속성 값을 갖는 요소의 집합이 정의됩니다.
- 즉, 똑같은 식별자 class 속성 값으로 포함된 요소들이 모인 집합 하나가 정의됩니다.
- getElementsByClassName 메서드를 사용하면 특정 class  속성 값을 class 속성 값으로 가지는 요소 객체 목록(NodeList)을 가져올 수 있습니다.

```javascript
document.getElementsByClassName(class의 이름)[index];
```

### CSS선택자로 노드 가져오기
```js
document.querySelector("#태그아이디값");
document.querySelector(".태그클래스값");

```

## DOM요소 속성 조정
|메서드|설명|
|------|---|
|hasAttribute(속성)|지정한 속성을 가지고 있는지 검사한다.|
|getAttribute(속성)|속성의 값을 가져온다.|
|setAttribute(속성명,값)|속성과 속성값을 설정한다.|
|removeAttribute(속성)|지정한 속성을 제거한다.|
|hasAttribute(속성)|지정한 속성을 가지고 있는지 검사한다.|
|.attributes|속성들을 모아서 배열로 반환|

### js_dom.html 생성하기
```html
<!DOCTYPE html>
<html>
  <body>
  <input type="text">
  <script>
     const input = document.querySelector('input[type=text]');
     console.log(input);

     if (!input.hasAttribute('value')) {  // value 어트리뷰트가 존재하지 않으면
       // value 어트리뷰트를 추가하고 값으로 'hello!'를 설정
       input.setAttribute('value', 'hello!');
     }

     // value 어트리뷰트 값을 취득
     console.log(input.getAttribute('value')); // hello!

     // value 어트리뷰트를 제거
     input.removeAttribute('value');

  </script>
  </body>
</html>
```

## DOM 객체의 스타일 변경하기
- element.style 객체로 태그의 css를 변경할수도 있다.
1. 요소의 배경색 변경
```js
var element = document.getElementById('myElement');
element.style.backgroundColor = 'lightblue';
```
2. 폰트 색상 변경
```js
var element = document.getElementById('myElement');
element.style.color = 'red';
```
3. 폰트 크기 변경
```js
var element = document.getElementById('myElement');
element.style.fontSize = '20px';
```
4. 테두리 추가:
```js
var element = document.getElementById('myElement');
element.style.border = '2px solid black';
```
5. 요소의 가시성 변경
```js
var element = document.getElementById('myElement');
element.style.display = 'none'; // 숨기기
// 또는
element.style.display = 'block'; // 보이기
```
6. 요소의 위치 변경
```js
var element = document.getElementById('myElement');
element.style.position = 'relative';
element.style.left = '50px';
element.style.top = '20px';
```
7. 클래스의 추가/제거
```js
var element = document.getElementById('myElement');
element.classList.add('newClass'); // 클래스 추가
// 또는
element.classList.remove('oldClass'); // 클래스 제거
```
8. 다중 속성 변경
```js
var element = document.getElementById('myElement');
element.style.cssText = 'color: blue; font-size: 18px;'; // 여러 속성을 동시에 변경
```
### js_style.html
```html
<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>Insert title here</title>

</head>
<body>
	<p id="p_id"> 자바스크립트로 css 바꾸기 연습</p>
	
	<script type="text/javascript">
		var element = document.getElementById("p_id"); 
		element.style.backgroundColor='lightblue';
		element.style.color='red';
		element.style.fontSize = '30px';
		element.style.border='2px solid black';
		element.classList.add('newClass');
		console.log(element.getAttribute('class'))

</script>
</body>
</html>
```

## JavaScript의 이벤트 처리
### 이벤트(event)란?
- 이벤트란 웹 브라우저가 알려주는 HTML요소에 대한 사건의 발생을 의미한다.
- 웹 페이지에 사용된 자바스크립트는 이렇게 발생한 이벤트에 반응하여 특정 동작을 수행할 수 있다.
- 따라서 클라이언트 측 자바스크립트를 비동기식 이벤트 중심의 프로그래밍 모델이라고 한다.

### 마우스 이벤트
|이벤트|설명|
|----|----|
|click|요소에 마우스 클릭했을 때 이벤트가 발생|
|dbclick|요소에 마우스를 더블클릭했을 때 이벤트가 발생|
|mouseover|요소에 마우스를 오버했을 때 이벤트가 발생|
|mouseout|요소에 마우스를 아웃했을 때 이벤트가 발생|
|mousedown|요소에 마우스를 눌렀을 때 이벤트가 발생|
|mouseup|요소에 마우스를 떼었을 때 이벤트가 발생|
|mousemove|요소에 마우스를 움직였을 때 이벤트가 발생|
|contextmenu|context menu(마우스 오른쪽 버튼을 눌렀을 때 나오는 메뉴)가 나오기 번에 이벤트 발생|

### 키 이벤트
|이벤트|설명|
|----|----|
|keydown|키를 눌렀을 때 이벤트가 발생|
|keyup|키를 떼었을 때 이벤트가 발생|
|keypress|키를 누른 상태에서 이벤트가 발생|

### 폼 이벤트
|이벤트|설명|
|----|----|
|focus|요소에 포커스가 이동되었을 때 이벤트 발생|
|blur|요소에 포커스가 벗어났을 때 이벤트 발생|
|change|요소에 값이 변경되었을 때 이벤트 발생|
|submit|submit 버튼을 눌렀을 때 이벤트 발생|
|reset|reset 버튼을 눌렀을 때 이벤트 발생|
|select|input이나 textarea 요소 안의 텍스트를 드래그하여 선택했을 때 이벤트 발생|

### 로드 및 기타 이벤트
|이벤트|설명|
|----|----|
|load|페이지의 로딩이 완료되었을 때 이벤트 발생|
|abort|이미지의 로딩이 중단되었을 때 이벤트 발생|
|unload|페이지가 다른 곳으로 이동될 때 이벤트 발생|
|resize|요소의 사이즈가 변경되었을 때 이벤트 발생|
|scroll|스크롤바가 움직였을 때 이벤트 발생|



### 1. HTML 속성을 이용한 이벤트 처리
- 이벤트를 HTML요소에 직접 추가하는 방식이다.
- 예를들어 'onclick' 속성을 사용하여 클릭 이벤트를 처리할 수 있다.
```html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8">
		<title>Insert title here</title>
		<script>
		  function myFunction() {
		    alert("버튼이 클릭되었습니다!");
		  }
		</script>
	</head>
	<body>
		<button onclick="myFunction()">클릭</button>
	</body>
</html>

```

### 2. 프로퍼티 방식
- 프로퍼티 리스너 방식은 이벤트 대상에 해당하는 객체의 프로퍼티로 이벤트를 등록하는 방식이다.
- 1번 방식에 비해 HTML과 JavaScript를 분리할 수 있다는 점에서 선호되는 방식이지만 추천하지는 않는다.
- 프로퍼티 방식은 이벤트에 오직 하나의 이벤트 핸들러만을 바인딩할 수 있다.
```html
<button class="btn">Click me</button>
<script>
    const btn = document.querySelector('.btn');

    // 이벤트 핸들러 프로퍼티 방식은 이벤트에 하나의 이벤트 핸들러만을 바인딩할 수 있다
    // 첫번째 바인딩된 이벤트 핸들러 => 실행되지 않는다.
    btn.onclick = function() {
        alert('① Button clicked 1');
    };

    // 두번째 바인딩된 이벤트 핸들러
    btn.onclick = function() {
        alert('① Button clicked 2'); // << 실행결과 
    };
</script>
```


### 3. DOM 요소에 이벤트 리스너 추가
- JavaScript를 사용하여 DOM 요소에 이벤트 리스너를 동적으로 추가하는 방식이다.
- addEventListener 함수를 사용한다.
```html
<button id="myButton">클릭</button>

<script>
  // 요소를 선택하고 이벤트 리스너를 추가
  document.getElementById("myButton").addEventListener("click", function() {
    alert("버튼이 클릭되었습니다!");
  });
</script>
```

```html
<input type="button" id="target1" value="button1" />
<input type="button" id="target2" value="button2" />

<script>
    var t1 = document.getElementById('target1');
    var t2 = document.getElementById('target2');
    function btn_listener(event){
        switch(event.target.id){
            case 'target1':
                alert(1);
                break;
            case 'target2':
                alert(2);
                break;
        }
    }
    t1.addEventListener('click', btn_listener); // btn_listener()가 아니다.
    t2.addEventListener('click', "btn_listener()"); // btn_listener()를 쓰려면 문자열로 감싼다.
</script>
```

## 이제 body영역에서 작성한 내용을 Script영역까지 가져와보자.
- a 태그는 클릭해서 이동하는것은 가능하지만 내용을 가져오는데는 한계가 있다.
- 자바스크립트와 밀접한 관련이 있는 input 태그는 사용자가 데이터를 입력할 수 있는 입력필드를 정의할 때 사용합니다.
- input태그의 type속성을 달리함으로써 여러 가지 모양을 나타낼 수 있습니다.


|속성명|속성값|설명|
|------|---|---|
|type|button<br>chcekbox<br>color<br>date<br>datetime-local<br>
email<br>file<br>hidden<br>image<br>month<br>number<br>password<br>radio<br>range<br>reset<br>search<br>submit<br>tel<br>text<br>time<br>url<br>week<br>|input 요소가 나타낼 타입을 명시함.|


### js_function.html 생성하기
```html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8">
		<title>자바스크립트의 메서드(함수)</title>
		<script type="text/javascript">
			function fun01(){
				alert("메서드 정상 호출됨");
			}
			
			function fun02(n) {//파라미터에 자료형을 적어줄 필요가 없다.
				//script영역에서 body로 접근하여 특정 객체를 검색
				var res = document.getElementById("result");
				
				res.value = n; //입력상자의 값이 홍길동으로 바뀐다.
			}
			
			function fun03() {
				//name이라는 아이디를 가진 태그를 찾아서
				//해당 태그에 쓰여있는 value를 alert()으로 출력하기
				var res = document.getElementById("name");
				var value = res.value;
				alert(value);	
				
			}
			
			function fun04(){
				var res = document.getElementById("res").value;
				var m_div = document.getElementById("m_div");
				m_div.innerHTML = res;
				//document.write();를 쓰게 되면 페이지가 아예 새로써진다.
			}
		</script>
	</head>
	
	<body>
		<input type="button" value="버튼1" onclick="fun01();"><!-- onclick : 마우스로 클릭했을 때 실행-->
		<input type="button" value="파라미터 버튼" onclick="fun02('홍길동');"><br><!-- 문자로 보내고 싶을 때는 홑따옴표라도 묶어서 보내야 한다. -->
		
		<hr>
		<input type="text" value="연습" id="name">
		<input type="button" value="버튼3" onclick="fun03();"> <!-- 버튼을 눌렀을 때 입력상자에 쓰여있는 값을 호출해보고싶다.  -->
		
		<hr>
		<input id="res">
		<input type="button" value="버튼3" onclick="fun04();">
		<div id="m_div">
		
		</div>
		
		<hr>
		<input type="password" id="pwd"><br>
		
	</body>
</html>
```
![image](https://user-images.githubusercontent.com/54658614/229685111-1c71bc5c-c716-4de4-ad0e-c35beafb3da6.png)

## 구구단 만들기
```html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8">
		<title>Insert title here</title>
		
		<style type="text/css">
			#disp{width:300px; height:300px; background: black; color:white; }
		</style>
		
		<script type="text/javascript">
		
		function gugu() {
			var m_dan = document.getElementById("dan").value;
			
			//유효성체크
			if( m_dan.trim() == '' ){
				alert("값을 입력해야 합니다.")
				return; //더이상 진행하지 않고 끝내라
			}
			
			if( m_dan<2 || m_dan>9 ){
				alert("2~9 만 입력해 주세요")
				return; //더이상 진행하지 않고 끝내라
			}
			
			//구구단 생성
			var str = "";
			
			for(var i = 1; i<10; i++) {
				str = str + m_dan + 'X' + i + '=' + (m_dan * i) + "<br>";
			}
			var gugudan = document.getElementById("disp");
			gugudan.innerHTML = str;
			 
		}//gugu()
		var b_show = true;
		function show() {
			
			b_show = !b_show;
			document.getElementById("bt_show").value = b_show ? "숨기기":"보이기";
			document.getElementById("disp").style.display = b_show ? 'block' : 'none';
		}
		</script>
	</head>
	
	<body>
		<p>
			단:
			<input id="dan">
			<input type="button" value="계산시작" onclick="gugu();">
			<input type="button" id="bt_show"  value="숨기기" onclick="show();">
		</p>
		
		<hr>
		
		<div id="disp">
			여기에 구구단
		</div>
	</body>
</html>
```
![image](https://user-images.githubusercontent.com/54658614/229685861-d2e09053-76fc-44e9-94a6-28ed1ac7dbbc.png)

## 계산기 만들기
```html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8">
		<title>Insert title here</title>
		<style type="text/css">
		li{list-style: none;
			float:left;
			margin-left:10px;}
		ul{overflow:hidden;}
		input{border-style:none;}
		</style>
		<script type="text/javascript">
		function cal(n) {
			var num1 = Number(document.getElementById("su1").value);
			var num2 = Number(document.getElementById("su2").value);
			var num3 = document.getElementById("result");
			if(n == '+') {
				num3.value = num1+num2;
			}
			else if(n == '-') {
				num3.value = num1-num2;
			}
			else if(n == '*') {
				num3.value = num1*num2;
			}
			else if(n == '/') {
				num3.value = num1/num2;
			}
			
		}
		
		
		</script>
	</head>
	
	<body>
		<table border = "1">
			<tr>
				<th class="su">수1</th>
				<td><input id="su1" placeholder="정수만 입력하세요"></td>
			</tr>
			
			<tr>
				<th class="su">수2</th>
				<td><input id="su2" placeholder="정수만 입력하세요"></td>
			</tr>
			
			<tr>
				<td colspan="2">
					<ul>
						<li>
							<input type="button" value="+" onclick="cal('+');">
						</li>
						<li>
							<input type="button" value="-" onclick="cal('-');">
						</li>
						<li>
							<input type="button" value="*" onclick="cal('*');">
						</li>
						<li>
							<input type="button" value="/" onclick="cal('/');">
						</li>
					</ul>
				</td>
			</tr>
					<tr>
						<th>결과</th>
						<td><input id="result"></td>
					</tr>
		</table>
	</body>
</html>
```

![image](https://user-images.githubusercontent.com/54658614/229686187-0676b0aa-53ac-4486-90ca-7e4015f3756f.png)


## 갤러리 만들어보기
```html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8">
		<title>이미지 슬라이드</title>
		<style type="text/css">
			a{text-decoration:none;}
		</style>
		
		<script type="text/javascript">
			var num = 1;
			var path="image/img";
			
			
			function prev() {
				num--;
				
				if(num<1) {
					num = 7;
				}
				//gallery라는 아이디를 가진 태그를 검색
				var my_a = document.getElementById("gallery"); //my_a가 image1.jpg를 갖고 있는 a태그가 된다.
				my_a.src= path + num + ".jpg";
				
			}//prev
			
			function next() {
				num++;
				
				if(num>7) {
					num = 1;
				}
				var my_b = document.getElementById("gallery");
				my_b.src = path + num + ".jpg";
			}
			
			setInterval("next()",1000); // 1초 간격으로 자동으로 next() 메서드를 호출
		</script>
	</head>
	
	<body>
	
		<div id="galleryWrap">
		
			<p>
				<a href="#" onclick="prev();">
					<img alt="이전" src="image/left_btn.png">
				</a>
				
				<img alt="갤려리" id="gallery" src="image/img1.jpg" width="300" height="200">
				
				<a href="#" onclick="next();">
					<img alt="다음" src="image/right_btn.png">
				</a>
			</p>
		
		</div>
		
	</body>
</html>
```
![image](https://user-images.githubusercontent.com/54658614/229685278-97f71f02-dad3-4958-b43a-e4f2bdcab247.png)

## form태그를 통한 값 전달

### HTML 폼
- 폼에 입력한 데이터를 웹 서버로 보내고 웹 서버는 그 데이터를 처리한다. 그 결과를 사용자에게 반환하거나 데이터베이스에 저장한다.
- 클라이언트 측 자바스크립트로 웹 애플리케이션을 만들 때 사용자 입력을 받는 사용자 인터페이스로 사용한다. 이때 데이터 처리는 클라이언트 측 자바스크립트 프로그램이 담당한다.

### 폼 요소와 폼 컨트롤 요소
- 웹 서버에 데이터를 보낼 때는 다음과 같은 과정을 거칩니다. 우선 form 요소를 작성하고 method와 action 속성을 지정합니다.
	- <b>method 속성</b> : 데이터 전송 방법("POST" 또는 "GET")
	- <b>action 속성</b> : 데이터를 처리하는 CGI 프로그램의 URL
- 그 다음 form 요소 안에 사용자로부터 입력을 받는 input 요소 등의 폼 컨트롤 요소를 배치합니다.
- 마지막으로 form 요소 안에 데이터를 전송하기 위한 submit 버튼과 데이터 입력을 취소하는 reset 버튼을 배치합니다. 

```html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8">
		<title>form 태그를 통한 데이터 전달1</title>
		<script type="text/javascript">
		function check(){
			//forms : 현재 html문서내의 form들을 순차적으로 배열로 정의해둔 형태
			//body에서 form태그가 여러개 존재할 경우 foms배열에 0,1,2,등의 인덱스로 form태그를 구별한다.
			var f = document.forms[0]; 
			
			//form태그에서 m_id라는  name속성을 가지고 있는 입력상자
			//document객체가 필요하지 않다 정말 편하다.
			var myId = f.m_id.value;
			
			//아이디를 입력하지 않았을 때 경고를 띄워주는 유효성 검사
			//클라이언트 단에서 해주는것이 좋다.
			if(myId == '') {
				alert("아이디는 필수 사항입니다.");
				return;
			}
			
			var myPwd = f.m_pwd.value;
			if(myPwd == ''){
				alert("비밀번호는 필수 사항입니다.");
				return;
			}
			
			var myAge = f.m_age.value;
			if(myAge == ''){
				alert("나이는 필수 사항입니다.");
				return;
			}
			
			//form태그에서 서버로 값을 전달하고자 한다면 알아야 하는 것
			
			//전송방식(GET,POST)
			//GET: 파라미터가 URL에 노출, 속도가 빠르지만 보안성이 취약
			//POST: 파라미터가 URL에 노출되지 않는다. 속도가 빠르지 않지만 보안성이 높고 바이너리 타입의 데이터를 전달하는것이 가능하다
			f.method="get";
			
			//파라미터를 전달할 페이지(처리객체 지정)
			f.action = "login.jsp";
			

			
			//입력된 데이터를 전송
			//f가 가진 name속성이 action으로 지정해둔 페이지에 파라미터로 전달(주소창을 보면 login.jsp?m_id=aaa&m_pwd=1234로 ? 뒤에 파라미터로 전달이 된다.)
			f.submit();

		}
		</script>
	</head>
	
	<body>
		서버로 전달하고 싶은 모든 데이터는 form 태그 안에 있어야 한다.
		그렇지 않으면 다른 jsp,java클래스로 전달할수 없다. 매우 중요!
		<!--<form></form>-->
		<form>
			<!--<form>태그의 공식적인 자식태그의 형태는 거의 <input> 태그형태로 이루어져 있다고 생각하면된다.
			<TextArea>는 name 속성을 붙힐 수 있다. 그 외 태그들 <div><a>이런 태그들에는 name을 붙혀도 파라미터로 넘어오지 않는다.-->
			
			<table border = "1"> 
				<tr>
					<th>ID : </th>
					<!--name 속성은 form안에서 특정 input을 찾아낼 수 있도록 해주는 식별자
					id와 역할은 비슷하지만 id로 지정을 해놓으면 다른 페이지로 값을 전달할 수 없다.-->
					
					<!--placeholder : 입력창에 가이드라인을 준다.-->
					
					<td><input name="m_id" placeholder="아이디를 입력해주세요"></td> 
					<!-- login.jsp에게 name으로 설정되 있는 id와 pwd를 파라미터로 써 날아간다. -->
				</tr>
				
				<tr>
					<th>AGE : </th>
					<td><input name="m_age"></td>
				</tr>
				
				<tr>
					<th>PWD : </th>
					<td><input type="password" name="m_pwd"></td>
				</tr>
				
				<tr >
					<td colspan="2" align="center">
						<input type="button" value="전송" onclick="check();">
						<!--type="submit"으로 보내면 무조건 서버로 날리기 때문에 유효성 체크가 안되므로 일반적으로 쓰이지 않는다. -->
					</td>
				</tr>
			</table>
		</form>
	</body>
</html>
```

![image](https://user-images.githubusercontent.com/54658614/229689463-0f9ad6de-7430-41b7-b729-4620a403f99c.png)

### form 태그를 검색하는 방법-2
```html
!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8">
		<title>form 태그를 통한 데이터 전달1</title>
		<script type="text/javascript">
		function check(){
			//form태그에 준 이름을 가지고 바로 검색할 수 있다.
			var f = document.ff;
			
			var myId = f.m_id.value; //유효성 체크를 하기 위해 id의 값을 가져오는것이지 하지 않을거라면 안써도 무방하다
			
	
			//f.method="get";
			
			//f.action = "login.jsp";
			
			f.submit();

		}
		</script>
	</head>
	
	<body>
	<!-- form 태그에 이름을 준다!-->
		<form name="ff" action="login.jsp" method="GET">

			<table border = "1"> 
				<tr>
					<th>ID : </th>
					<td><input name="m_id" placeholder="아이디를 입력해주세요"></td> 

				</tr>
				
				<tr>
					<th>AGE : </th>
					<td><input name="m_age"></td>
				</tr>
				
				<tr>
					<th>PWD : </th>
					<td><input type="password" name="m_pwd"></td>
				</tr>
				
				<tr >
					<td colspan="2" align="center">
						<input type="button" value="전송" onclick="check();">
					</td>
				</tr>
			</table>
		</form>
	</body>
</html>
```

### form 태그를 검색하는 방법-3
```html
		<script type="text/javascript">
		function check(f){
			
			f.submit();

		}
		</script>
	</head>
	
	<body>
		<form action="login.jsp" method="GET">
			<table border = "1">
				<tr >
				<!--this는 form에만 사용할 수 있다. this.form은 버튼을 포장하고 있는 현재 form 태그를 의미한다.-->
					<td colspan="2" align="center">
						<input type="button" value="전송" onclick="check(this.form);">
					</td>
				</tr>
			</table>
		</form>
	</body>
</html>
```
