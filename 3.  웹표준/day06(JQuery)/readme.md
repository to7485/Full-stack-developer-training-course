# JQuery란?
- 자바스크립트로 만들어진 라이브러리이다. 자바스크립트의 DOM(Document Object Model)작업을 좀 더 쉽게 할 수 있는 기능을 갖고 있다.

## JQuery 변수
- $기호가 붙는다.
```js
var $변수명
```
- jQuery 내장함수 (= 메서드) 사용 가능.

※ css(), hide(), how() 등.<br>
$hz.css('background-color', 'red') (O)

## JQuery Selectors
- Query 선택기는 이름, ID, 클래스, 유형, 속성, 속성 값 등을 기반으로 HTML 요소를 "찾기"(또는 선택)하는 데 사용됩니다.
- jQuery의 모든 선택자는 달러 기호와 괄호 $()로 시작합니다.

### 태그의 선택
- 요소 이름을 기반으로 요소를 선택합니다.
- 다음 <p>과 같이 페이지의 모든 요소를 선택할 수 있습니다 .
```js
$("p")
```

### \#id 선택기
- HTML 태그의 id 속성을 사용하여 특정 요소를 찾습니다.
```js
$("#test")
```

### .class 선택기
- .class선택기는 특정 클래스의 요소를 찾습니다.
```js
$(".test")
```

### 속성 선택기
- 태그의 속성을 기반으로 클래스의 요소를 찾는다.
```js
$(input[name='value']) name속성이 value인 input태그를 선택
```

## JQuery Events
- 웹 페이지가 응답할 수 있는 모든 다양한 방문자의 작업을 이벤트라고 합니다.

<table>
  <tr>
    <th>Mouse Events</th>
    <th>Keyboard Events</th>
    <th>Form Events</th>
    <th>Document/Window Events</th>
  </tr>
  <tr>
    <td>click</td>
    <td>keypress</td>
    <td>submit</td>
    <td>load</td>
  </tr>
  <tr>
    <td>mouseenter</td>
    <td>keyup</td>
    <td>focus</td>
    <td>scroll</td>
  </tr>
  <tr>
    <td>mouseleave</td>
    <td></td>
    <td>blur</td>
    <td>unload</td>
  </tr>
</table>

### 일반적으로 사용되는 jQuery 이벤트 메서드
- <b>$(document).ready()</b> 메서드를 사용하면 문서가 완전히 로드되었을 때 함수를 실행할 수 있습니다.

```js
$(document).ready()
```
- **click()** 사용자가 HTML 요소를 클릭하면 함수가 실행됩니다.

```js
$("p").click(function(){
$(this).hide();
});

이벤트에 의해 실행되는 함수 영역 안에서 특수 키워드 this를 사용할 수 있다.
$(this)는 일종의 변수, 선택자인데, this 키워드를 $()함수에 전달하면, 이벤트가 발생한 자기 자신을 감지할 수 있게 된다.

```

```js
<div>
  <button id="single" type="button"> 클릭하세요 </button>
</div>

let cnt = 0;

$('#single').click(function(){
	$(this).text((++cnt) +'번 클릭하셨습니다.');
});
```

![image](https://github.com/to7485/Web1500/assets/54658614/5bc0d5d1-1099-4911-8267-6afa517b5f0a)

- index() 함수와 this를 이용한 중복클래스 제어
```
<div>
  <button class="multi" type="button">button0 (0번 클릭됨)</button>
  <button class="multi" type="button">button1 (0번 클릭됨)</button>
  <button class="multi" type="button">button2 (0번 클릭됨)</button>
</div>

let multicnt = { multi : [0, 0, 0] };
// 버튼 별로 횟수를 담아줄 객체를 만든다.
// 값을 배열형식으로 설정했다.

$('multi').click(function(){
// 버튼을 클릭할 때 발생하는 이벤트

    let idx = $(this).index();
    multicnt.multi.[idx]++;
// 버튼을 클릭할 때 해당 버튼이 몇 번째 요소인지 idx에 저장
// 아까 만든 객체 배열에 버튼이 눌릴 때 마다 
// 해당 배열에 숫자를 한 개씩 증가시켜서 넣어줌

    $(this).html('button' + idx + 
    '(' + multicnt.multi[idx] + '번 클릭됨)');
});
```

![image (1)](https://github.com/to7485/Web1500/assets/54658614/4768d77d-c2a6-4955-b45e-fc8a11c6f780)

- **dblclick()** 사용자가 HTML 요소를 두 번 클릭하면 함수가 실행됩니다.

- **mouseenter()** 마우스 포인터가 HTML 요소에 들어갈 때 실행됩니다.
```js
$("#p1").mouseenter(function(){
alert("You entered p1!");
});
```
- **mouseleave()** 마우스 포인터가 HTML 요소를 떠날 때 실행됩니다.

- **mousedown()** HTML 요소 위에 마우스가 있는 동안 왼쪽, 가운데 또는 오른쪽 마우스 버튼을 누르면 함수가 실행됩니다.

- **mouseup()** HTML 요소 위에 마우스가 있는 동안 왼쪽, 가운데 또는 오른쪽 마우스 버튼을 놓으면 함수가 실행됩니다.

- **hover()**

```js
$("#p1").hover(function(){
alert("You entered p1!");
},
function(){
alert("Bye! You now leave p1!");
});
```

- **focus()** 양식 필드에 포커스가 있을 때 실행됩니다.

```js
  $("input").focus(function(){
  $(this).css("background-color", "#cccccc");
});
```
- **blur()** 양식 필드가 포커스를 잃을 때 실행됩니다.

- **on()** on()메서드는 선택한 요소에 대해 하나 이상의 이벤트 핸들러를 연결합니다.

```js
<p> 요소에 여러 이벤트 핸들러를 연결합니다.

$("p").on({
mouseenter: function(){
  $(this).css("background-color", "lightgray");
},
mouseleave: function(){
  $(this).css("background-color", "lightblue");
},
click: function(){
  $(this).css("background-color", "yellow");
}
});
```

## JQuery Effects
- JQuery 숨기기 및 표시
  - jQuery를 사용하면 **hide()**및 **show()**메서드를 사용하여 HTML 요소를 숨기거나 표시할 수 있습니다.
```js
$("#hide").click(function(){
  $("p").hide();
});
$("#show").click(function(){
  $("p").show();
});
```

- jQuery 토글
  - **toggle()**메서드 를 사용하여 요소를 숨기거나 표시하는 사이를 전환할 수도 있습니다 .
  - 표시된 요소는 숨겨지고 숨겨진 요소는 표시됩니다.
```js
$("button").click(function(){
  $("p").toggle();
});
```

## JQuery HTML

### JQuery Get
- jQuery에는 HTML 요소와 속성을 변경하고 조작하는 강력한 방법이 포함되어 있습니다.

### 콘텐츠 가져오기
- DOM 조작을 위한 간단하지만 유용한 세 가지 jQuery 메서드가 있다.

1. **text()** - 선택한 요소의 텍스트 내용을 설정하거나 반환합니다.
2. **html()** - 선택한 요소(HTML 마크업 포함)의 내용을 설정하거나 반환합니다.
3. **val()** - 양식 필드의 값을 설정하거나 반환합니다.

```js
$("#btn1").click(function(){
  alert("Text: " + $("#test").text());
});
$("#btn2").click(function(){
  alert("HTML: " + $("#test").html());
});
```

4. **attr()** - 속성값을 가져올때 사용할 수 있다.

```js
$("button").click(function(){
  alert($("#w3s").attr("href"));
});
```

### JQuery Add
- 새 HTML 콘텐츠를 추가하는 데 사용되는 4가지 jQuery 메서드

1. append() - 선택한 요소의 끝에 내용을 삽입합니다.
2. prepend() - 선택한 요소의 시작 부분에 내용을 삽입합니다.
3. after() - 선택한 요소 뒤에 내용 삽입
4. before() - 선택한 요소 앞에 내용 삽입

### JQuery Remove
- 요소와 콘텐츠를 제거하기 위해 주로 두 가지 jQuery 메서드

1. remove() - 선택한 요소(및 해당 하위 요소)를 제거합니다.
2. empty() - 선택한 요소에서 자식 요소를 제거합니다.

## JQuery AJAX

### JQuery load()메서드
- jQuery load()메서드는 간단하지만 강력한 AJAX 메서드입니다.
- load()메서드는 서버에서 데이터를 로드하고 반환된 데이터를 선택한 요소에 넣습니다.

```js
$(selector).load(URL,data,callback);
```

- 필수 URL 매개변수는 로드하려는 URL을 지정합니다.
- 선택적 data 매개변수는 요청과 함께 보낼 쿼리 문자열 키/값 쌍 세트를 지정합니다.
- 선택적 callback 매개변수는 load()메소드가 완료된 후 실행할 함수의 이름입니다

### jQuery를 이용한 Ajax 기본 사용방법
```js
$.ajax({
    url: "",
    type: "",
    cache: ,
    dataType: "",
    data: "",
    success: function(data){
  
    },
    error: function (request, status, error){        

    }
});
```
- url : 요청 url을 의미한다.
- type : 데이터 전송방식. GET 또는 POST
- cache : 요청 페이지의 캐시 여부. false 또는 true
- datatype : 서버에서 받아올 데이터를 어떤 형태로 해석할 것인지. xml, json, html, script를 선택할 수 있다.
- data : 서버로 데이터를 전송할 때 사용한다. "name="+name 이런 형태로
- success : Ajax 통신에 성공했을 때 실행되는 이벤트.
- error : Ajax 통신에 실패했을 때 실행되는 이벤트. request, status, error로 에러 정보를 확인할 수 있다.










