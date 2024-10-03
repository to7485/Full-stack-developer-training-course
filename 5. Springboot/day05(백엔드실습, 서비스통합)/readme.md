# 서비스 통합
- 현재 독립적으로 동작하는 백엔드 애플리케이션과 독립적으로 동작하는 프론트엔드 애플리케이션이 하나씩 있다.
- 이제 두 애플리케이션을 통합해 하나의 기능을 하는 웹 애플리케이션을 완성할 차례이다.
- 프론트엔드에서 fetch또는 axios를 이용해 Todo아이템을 조회,추가,수정,삭제하는 백엔드 API를 호출하는 코드를 작성한다.

## App.js에서 fetch()로 백엔드 API 호출하기
- 첫 번째로 구현할 부분은 Todo 아이템을 조회하는 것이다.
- 브라우저에 http://localhost:3000을 치고 들어가면 Todo 아이템이 리스트에 보여야 한다.
- 이 부분을 구현하기전에 **우리의 백엔드 서버를 실행하자!**
```jsx
import axios from 'axios';
//axios 없으면 npm install axios 하기


function App() {
  const [items, setItems] = useState([])

  axios.get("http://localhost:9090/todo", {
    headers: {
        "Content-Type": "application/json"
    }
})
.then(response => {
    setItems(response.data); // response.data를 통해 서버에서 반환된 데이터를 처리
})
.catch(error => {
    console.error("There was an error!", error); // 에러 처리
});
```
- npm start를 한 후 localhost:3000으로 들어가 개발자도구의 콘솔 창을 켜보면 다음과 같은 에러를 확인할 수 있다.

![img](img/cors.png)

- 보안을 위해 CORS 헤더 Policy를 위반했기 때문이다.

## CORS(Cross-Origin Resource Sharing)
- 교차 출처 리소스 공유라는 의미다.
- 이 개념을 이해하려면 먼저 **출처(origin)**와 브라우저 보안 정책을 알아야 한다.

### 출처
- 출처는 프로토콜과 호스트주소 그리고 포트번호까지 모두 합친것을 의미한다.
- 즉, 서버의 위치를 찾아가기 위해 필요한 가장 기본적인 것들을 합쳐놓은 것이다.

![img](img/출처.png)

### 동일 출처 정책(Same-Origin Policy)
- 브라우저는 기본적으로 보안을 위해 동일 출처 정책이라는 규칙을 따른다.
- 같은 출처에서 로드된 웹사이트만 서로 데이터를 주고받을 수 있다는 내용이다.
- 즉, 웹페이지가 한 출처에서 로드되었을 때, 다른 출처에서 데이터를 요청하는 것을 제한하는 정책이다.
- https://www.example.com에서 로드된 웹페이지는 기본적으로 https://api.example.com 같은 다른 출처에 데이터를 요청할 수 없다.
- 이 정책은 보안을 위해 존재하는데, 악의적인 웹사이트가 사용자의 브라우저를 이용해 다른 출처에서 데이터를 가져오지 못하게 막는 역할을 한다.

### CORS
- Cross-Origin Resource Sharing의 약자로, 출처가 다른 두 웹사이트 간의 데이터 요청을 허용하는 방식을 말한다.
- 예시
  - A라는 웹사이트(https://www.siteA.com)에서 B라는 서버(https://www.siteB.com)에 데이터를 요청하려고 할 때, 
  - B 서버가 A 사이트의 요청을 허용하는지 확인해야 한다.
  - B 서버가 A 사이트의 요청을 허용하면, CORS를 통해 데이터 요청이 가능해진다.

### CORS가 필요한 이유
- 오늘날의 웹 애플리케이션은 여러 도메인에서 데이터를 주고받는 경우가 많다.
- 프론트엔드는 한 도메인에서 실행되고, 백엔드 서버는 다른 도메인에서 실행되는 경우가 많다.
- 동일 출처 정책은 보안을 위해 데이터를 차단하지만, CORS는 허용된 출처에서 데이터를 요청할 수 있도록 한다.

### CORS의 동작 방식
1. 클라이언트(브라우저)
   - 사용자가 웹사이트를 방문하면 브라우저는 다른 출처로 데이터 요청을 보낸다.
2. 서버
   - 데이터를 요청받은 서버는 해당 요청이 허용된 출처에서 온 것인지 확인한다.
3. 응답
   - 서버가 CORS 설정을 통해 요청을 허용하면, 브라우저는 데이터를 받을 수 있다. 
   - 허용되지 않은 출처에서 요청이 왔다면, 브라우저는 데이터를 차단한다.

## CORS를 가능하게 하기 위해 백엔드에서 설정하기
- com.example.demo.config 패키지 만들기
  - WebMvcConfig클래스 생성하기
```java
package com.example.demo.config;

import org.springframework.context.annotation.Configuration;
import org.springframework.web.servlet.config.annotation.CorsRegistry;
import org.springframework.web.servlet.config.annotation.WebMvcConfigurer;

@Configuration // 스프링에서 해당 클래스를 설정 클래스로 인식하고 빈으로 등록함
public class WebMvcConfig implements WebMvcConfigurer { // WebMvcConfigurer 인터페이스를 구현하여 CORS 설정을 포함한 MVC 설정을 커스터마이징할 수 있음

    private final long MAX_AGE_SECS = 3600; // 브라우저가 CORS 요청 결과를 캐싱하는 최대 시간(초) 설정

    @Override
    public void addCorsMappings(CorsRegistry registry) {
        // addMapping("/**"): 모든 경로에 대해 CORS 설정을 적용
        registry.addMapping("/**")
            // allowedOrigins("http://localhost:3000"): React 애플리케이션이 실행되는 도메인(출처)에서 오는 요청을 허용
            .allowedOrigins("http://localhost:3000")
            // allowedMethods("GET", "POST", "PUT", "DELETE"): HTTP 메서드(GET, POST, PUT, DELETE)를 허용
            .allowedMethods("GET", "POST", "PUT", "DELETE")
            // allowedHeaders("*"): 모든 헤더를 허용
            .allowedHeaders("*")
            // allowCredentials(true): 쿠키나 인증 정보를 포함한 요청을 허용
            .allowCredentials(true)
            // maxAge(MAX_AGE_SECS): 브라우저가 서버로부터 받은 응답을 일정 시간 동안 저장해 두고, 그 시간 내에 동일한 요청이 있을 경우 서버에 다시 요청하지 않고 저장된 응답을 재사용한다는 의미다.
            .maxAge(MAX_AGE_SECS);
    }
}
```
### WebMvcConfigurer
- Spring MVC에서 제공하는 인터페이스로, 스프링 MVC의 동작을 커스터마이징할 때 사용된다.
- 스프링은 기본적으로 MVC 동작을 자동으로 설정해주지만, 때로는 프로젝트 요구사항에 맞게 특정 기능을 추가하거나 수정해야 할 때 WebMvcConfigurer를 구현하여 원하는 설정을 적용할 수 있다.

### 주요 기능
- CORS 설정(Custom CORS Configuration)
  - addCorsMappings 메서드를 오버라이드하여 CORS(Cross-Origin Resource Sharing) 규칙을 설정할 수 있다.
  - 이를 통해 특정 도메인에서 오는 요청을 허용하거나, 전체 도메인에서 오는 요청을 제어할 수 있다.
- 인터셉터(Interceptors) 추가
  - 인터셉터는 HTTP 요청이 컨트롤러에 도달하기 전후에 실행되며, 요청을 가로채어 로깅, 인증, 권한 확인 등의 작업을 수행할 수 있다.
<br>

코드를 작성한 후 백엔드 애플리케이션을 수정한 후 재시작 한다.<br>
이후 브라우저를 새로고침하면 더 이상 CORS에러가 나지 않는것을 확인할 수 있다.


## UseEffect를 이용한 Todo 리스트 초기화
- CORS로 인한 에러 미시지는 사라졌지만 네트워크 탭을 열어보면 todo가 끝없이 나열된 것을 확인할 수 있다.

![img](img/network.png)

### 리액트의 렌더링
- 리액트는 브라우저에 보이는 HTML DOM 트리의 다른 버전인 ReactDOM을 가지고 있다.
- 어떤 이유에서 컴포넌트의 상태가 변하면 ReactDOM은 이를 감지하고 컴포넌트 함수를 다시 호출함으로써 변경된 부분의 HTML을 바꿔준다.
- HTML이 업데이트되면 우리는 변경된 결과를 눈으로 확인할 수 있다.
- 즉, 화면에 보여주는 것을 렌더링이라고 한다.

### 무한루프에 빠진 리액트
- 렌더링이 가장 처음 일어나는 순간, 리액트는 ReactDOM트리가 존재하지 않는 상태에서 처음으로 각 컴포넌트 함수를 호출해 자신의 DOM트리를 구성한다.
- 애플리케이션에서 가장 처음으로 호출하는 함수는 바로 APP()이다.
- App() 함수를 호출할 때, 함수 내에서 axios를 이용해 Todo API를 호출한다.
- axios를 사용한 API 호출은 비동기 호출이기 때문에 API 호출 후 응답이 올 때까지 기다리지 않는다.
- 기다리지 않고 함수를 반환했으니 Add Todo Here과 같은 입력필드나 + 버튼을 볼 수 있는 것이다.
- Todo API 호출이 완료돼 리스트가 반환되면 then()으로 이어진 함수가 차례로 실행된다.
- Todo API 호출이 성공하는 경우 then 함수 체인은 결국 setItem(..)을 부른다.
- setItem을 부르면 Item의 상태가 새로 초기화 된다.
- 상태가 바뀌었음으로 리액트는 재렌더링을 위해 다시 App()을 호출한다. 
- API함수를 호출할 때, 함수 내에서 axios를 다시 호출하게 된다.
- 이렇게 리액트는 무한루프에 빠지게 된다.

```jsx
import React, { useEffect,useState } from 'react';
import axios from 'axios';

function App() {
  const [items, setItems] = useState([])


  useEffect(() => {
    axios.get("http://localhost:9090/todo", {
      headers: {
          "Content-Type": "application/json"
      }
    })
    .then(response => {
        setItems(response.data); // response.data를 통해 서버에서 반환된 데이터를 처리
    })
    .catch(error => {
        console.error("There was an error!", error); // 에러 처리
    });
  },[])
  ... 중략
```
- useEffect를 사용하여 처음 렌더링 될 때 1번만 실행하게 만들 수 있다.

## 확장성을 염두한 코드 작성하기
- API를 호출하는 주소를 하드코딩 할 수 있지만 실제 도메인을 사용하는 것을 염두에 두면 좋은 방법이 아니다.
- 설정파일에서 애플리케이션이 사용할 백엔드 URI를 동적으로 가져오도록 구현해 이후 도메인이 바뀌는 경우를 대비하자.

### api-config.js 파일 생성하기
```js
let backendHost;
//window 객체 : 브라우저에서 실행되는 모든 코드에 접근할 수 있는 최상위 객체이다.
//웹 페이지에서 실행되는 모든 JavaScript는 window 객체를 기반으로 동작한다.

//window.location 객체는 현재 웹 페이지의 URL 정보를 다루는 객체이다.

//window.location.hostname: 현재 페이지의 호스트 이름(도메인)을 반환한다.
//호스트 이름은 도메인의 이름 부분으로, 프로토콜(http:// 또는 https://), 경로, 쿼리 문자열을 제외한 부분이다.

//왼쪽부터 차례대로 평가하며, false나 null, undefined가 나오면 바로 평가를 중단하고 그 값을 반환한다.
const hostname = window && window.location &&window.location.hostname;

if(hostname == "localhost"){
    backendHost = "http://localhost:9090";
}

export const API_BASE_URL = `${backendHost}`
```

### service폴더 생성하기
- ApiService.js 파일 생성하기
```js
import axios from 'axios';
import { API_BASE_URL } from "../api-config";

//api : 호출할 API의 경로 (예: /todos, /users)
//method: HTTP 메서드 (예: GET, POST, PUT, DELETE)
//request: 요청에 담을 데이터(주로 POST, PUT 요청에서 사용)
export function call(api, method, request) {
    // 기본 옵션 설정
    let options = {
        url: API_BASE_URL + api,
        method: method,
        headers: {//요청 헤더를 설정.
            "Content-Type": "application/json"
        }
    };

    // request가 존재하는 경우: POST, PUT, DELETE와 같은 GET 이외의 요청일 때, 요청 본문에 데이터를 담아 보낸다.
    if (request) {
        options.data = JSON.stringify(request); // 객체 형태로 전달된 데이터를 JSON 문자열로 변환하여 서버에 전송한다.
    }

    // axios(options): 앞서 설정한 options 객체를 사용하여 Axios로 HTTP 요청을 보낸다.
    return axios(options)
        //요청이 성공적으로 처리된 경우 실행되는 코드이다.
        .then(response => {
            //서버에서 반환된 실제 데이터를 반환하여, 이 데이터를 호출한 쪽에서 사용할 수 있도록 한다.
            console.log(response.data);
            return response.data;
        })
        //요청 중에 오류가 발생한 경우 실행되는 코드.
        .catch(error => {
            //에러가 발생하면, 이를 console.log로 출력하여 디버깅하거나 문제를 파악할 수 있도록 한다.
            const m_error = error;
            return m_error;
        });
}
```
- 위 함수가 없다면 요청을 할 때마다 매번 작성해야 한다.

### App.js의 기존 함수들을 ApiService를 이용해 수정하자
```js
import logo from './logo.svg';
import Todo from './Todo';
import React, { useEffect, useState } from 'react';
import { Container, List, Paper } from "@mui/material";
import './App.css';
import AddTodo from './AddTodo'
import { call } from "./service/ApiService"



function App() {
  const [items, setItems] = useState([])


  useEffect(() => {
    /////////////////call메서드 호출///////////////////
    call("/todo", "GET")
      .then(result => setItems(result.data))
    /////////////////call메서드 호출///////////////////
  }, [])

  const addItem = (item) => {
    /////////////////call메서드 호출///////////////////
    call("/todo", "POST", item)
      .then(result => setItems(result.data))
    /////////////////call메서드 호출///////////////////
  }

  //내용 수정
  const editItem = () => {
    setItems([...items])
  }

  //삭제
  const deleteItem = (item) => {
    /////////////////call메서드 호출///////////////////
    call("/todo", "DELETE", item)
      .then(result => setItems(result.data))
    /////////////////call메서드 호출///////////////////
  }


  let todoItems = items.length > 0 && (
    <Paper style={{ margin: 16 }}>
      <List>
        {items.map((item) => (
          <Todo item={item} key={item.id} deleteItem={deleteItem} editItem={editItem} />
        ))}
      </List>
    </Paper>
  );

  return (
    <div className="App">
      <Container maxWidth="md">
        <AddTodo addItem={addItem} />
        {/* props를 컴포넌트에 전달하기
      이름={useState값} */}
        <div className="TodoList">
          {todoItems}
        </div>
      </Container>
    </div>
  );
}

export default App;
```
- 브라우저를 새로고침 한 후 Todo 아이템을 추가해보자
- 그리고 다시 새로고침을 해보자.
- 백엔드의 데이터베이스에서 Todo 리스트를 가져오므로 새로고침을 해도 사라지지 않는다.
- 또는 프론트엔드 애플리케이션을 완전히 종료했다가 다시 켜도, 당연히 사라지지 않는다.

## Todo Update 수정
- 사용자가 키보드 키를 입력하면 item 객체를 수정했기 때문에 우리가 할 일은 App.js의 editItem() 함수 내에서 items 리스트를 새 배열로 옮김으로써 재렌더링 하는 작업을 했다.
- 따로 수정한 item을 editItem()으로 넘기지 않아도 잘 동작했다.
- 하지만 API를 이용해 item을 수정하기 위해서는 몇가지를 수정해야 한다.

### 1. Service API를 이용해 서버 데이터를 업데이트 한다.
### 2. 변경된 내용을 화면에 다시 출력해야 한다.

### App.js코드 수정하기
```js
//내용 수정
const editItem = (item) => {
   call("/todo","PUT",item)
   .then(result => setItems(result.data))
}
```
- 우리가 수정한 editItem() 함수는 매개변수를 받는다.
- 따라서 Todo.js에서 editItem()함수를 호출할 때 매개변수에 값을 전달해줘야한다.

### 주의사항
- 타이틀 변경을 위해 input의 필드에서 사용자의 입력을 받아올 때 editEventHandler()에서 item을 바로 넘겨버리면 한 글자 한 글자 입력할 때마다 HTTP요청을 보내게 된다.
- 이는 매우 낭비기 때문에 수정을 완료한 시점에서 HTTP 요청을 보내고 싶다.
- 수정을 완료한 시점은 입력이 끝나 수정이 불가능한 상태로 바뀌는 시점이다.

### Todo.js코드 수정하기
```js
const editEventHandler = (e) => {
   setItem({...item,title:e.target.value});//변경만 해서는 렌더링이 안된다.
}

//turnOnReadOnly함수
const turnOnReadOnly = (e) =>{
   if(e.key === 'Enter' && readOnly === false){
      setReadOnly(true);
      editItem(item);
   }
}
```

## 체크박스 수정
- 체크 상태가 업데이트 될 때마다 editItem()을 호출해 백엔드 HTTP요청을 보내면 된다.
### Todo.js코드 수정하기
```js
//체크박스변경
const checkboxEventHandler = (e) =>{
   item.done = e.target.checked;
   editItem(item);//App.js의 editItem의 매개변수에 전달된다.
}
```
- 브라우저를 새로고침 한 후 업데이트 부분을 테스트해보자.
- 리액트 애플리케이션을 재시작하거나 이미 실행중인 경우 브라우저를 새로고침한다.

# REST API 인증기법
- 지금까지는 모든 것이 로컬에서 돌아가는 것이었고 나만 사용하는 애플리케이션이었다.
- 우리의 목표는 이 애플리케이션을 많은 사람이 사용할 수 있도록 배포하는 것이다.
- 많은 사람이 사용할 수 있도록 하려면 어떤 형태로든 인증 매커니즘을 구현해야 한다.
## 인증
### 개념
- 사용자가 누구인지 확인하는 과정이다.

### 동작 과정
- 사용자가 제공한 정보(사용자 이름과 비밀번호)를 바탕으로, 시스템이 해당 사용자가 실제로 누구인지 확인하는 단계이다.

### 방법
- 사용자명과 비밀번호
  - 가장 전통적인 인증 방식으로, 사용자가 입력한 비밀번호와 저장된 비밀번호를 비교하여 신원을 확인한다.
- 다중 요소 인증(MFA)
  - 비밀번호 외에도 추가적인 인증 수단(예: SMS 코드, 이메일 확인 등)을 사용하여 보안을 강화한다.
- 생체 인증
  - 지문, 안면 인식 등 사용자의 고유한 생체 정보를 이용한 인증 방식이다.
- OAuth 2.0 소셜 로그인
  - 사용자가 페이스북, 구글과 같은 외부 서비스의 계정을 이용해 로그인하는 방식.

## 인가
### 개념
- 사용자가 인증된 후에, 그 사용자가 무엇을 할 수 있는지를 결정하는 과정이다.
- 특정 자원이나 기능에 접근할 수 있는 권한을 부여하는 절차다.

### 동작 과정
- 사용자가 인증된 후, 시스템은 사용자의 역할, 권한 등을 바탕으로 사용자가 어떤 자원에 접근할 수 있고, 어떤 작업을 수행할 수 있는지를 결정한다.

### 방법
- 역할 기반 인가(RBAC, Role-Based Access Control)
  - 사용자는 특정 역할(예: 관리자, 사용자, 게스트 등)에 속하며, 각 역할에 따라 다른 권한이 부여된다.
- 정책 기반 인가(PBAC, Policy-Based Access Control)
  - 미리 설정된 정책에 따라 사용자의 권한이 결정된다. 예를 들어, 특정 시간대에만 자원에 접근할 수 있게 하는 정책.
- 권한 기반 인가
  - 특정 권한(예: 읽기, 쓰기, 삭제 등)에 따라 자원 접근 여부를 결정한다.

<hr>

```
- 인증과 인가의 구현은 아키텍처 디자인과 밀접한 관계를 갖는다.
- 우리의 서비스가 확장성이 높더라도 인증과 인가의 확장이 어렵다면 우리의 서비스는 인증과 인가 서비스의 확장성에 제약을 받게 된다.
```

## Basic 인증
- 우리가 구현한 Todo 애플리케이션은 로그인을 제외하면 특별히 상태를 유지해야 할 이유가 없다.
- 그래서 REST 아키텍처를 사용하는 것이기도 하다.
- 상태가 없는 웹 애플리케이션에서 인증을 구현하는 가장 간단한 방법은 모든 HTTP 요청에 아이디와 비밀번호를 같이 보내는 것이다.
- 이런 방법을 Basic 인증이라고 한다.

### Basic 인증의 동작 방식
1. 클라이언트가 요청을 보냄
   - 클라이언트(브라우저 또는 애플리케이션)가 서버에 자원에 대한 요청을 보낸다.
2. 서버가 인증 요구
   - 서버는 요청된 자원이 인증이 필요하다고 판단되면, 401 Unauthorized 상태 코드와 함께 인증이 필요하다는 메시지를 반환한다.
3. 클라이언트가 자격 증명을 전송
   - 클라이언트는 아이디와 비밀번호를 Base64 인코딩하여 HTTP 요청 헤더에 포함한 뒤 다시 요청을 보낸다.
4. 서버가 인증 확인
   - 서버는 전송된 자격 증명을 디코딩하여 사용자가 인증할 수 있는지 확인하고, 자격이 유효하면 요청한 자원에 접근을 허용한다.

![img](img/베이직.png)

### Baisc 인증 요청 예시
```
GET /protected-resource HTTP/1.1
Host: example.com
Authorization: Basic dXNlcm5hbWU6cGFzc3dvcmQ=
```
- 이 HTTP 요청을 수신한 서버는 인코딩된 문자열을 디코딩해 아이디와 비밀번호를 찾아낸 후, 유저 정보가 저장된 데이터베이스 또는 인증 서버의 레코드와 비교한다.
- 데이터베이스의 레코드가 아이디와 비밀번호와 일치하면 요청 받은 일을 수행하고 아니라면 거부한다.

### 장점
1. 단순하고 구현이 쉬움
      - Basic 인증은 다른 복잡한 인증 방식과 비교해 매우 간단하며, 설정과 구현이 쉬운 편이다.
2. HTTP 표준
   - HTTP 프로토콜의 표준에 포함되어 있어 모든 HTTP 클라이언트에서 쉽게 지원된다.

### 단점
1. 보안 취약점
   - Base64는 인코딩일 뿐이지 암호화가 아니기 때문에 사용자 이름과 비밀번호를 쉽게 디코딩할 수 있다. 
   - 즉, 네트워크 상에서 데이터를 가로챈다면 자격 증명이 쉽게 노출될 수 있다.
2. HTTPS가 필수
   - Basic 인증을 사용하려면 반드시 **HTTPS(SSL/TLS 암호화)**를 사용해야 한다. 
   - 그렇지 않으면, 네트워크 상에서 자격 증명이 평문으로 전송되어 탈취 위험이 크다.
3. 세션 관리가 어려움
   - Basic 인증은 상태를 유지하지 않기 때문에, 매 요청마다 인증 정보를 함께 전송해야 한다.
4. 유저를 로그아웃시킬 수 없다.
   - 모든 요청이 일종의 로그인 요청이기 때문이다.
   - 여러 디바이스에서 로그인이 가능한 경우 한꺼번에 로그아웃 하거나 디바이스별로 로그아웃 할 수 있는 기능이 있다.
5. 사용자의 계정 정보가 있는 저장 장소의 경우 인증 서버와 인증 DB에 과부하가 걸릴 확률이 높다.


## 토큰 기반 인증
- 사용자가 인증에 성공한 후 토큰을 발급받아, 이를 사용해 서버와의 통신에서 인증을 처리하는 방식이다.
- 이 방식은 세션 기반 인증과 달리, 서버에 사용자의 상태를 저장하지 않고, 토큰을 통해 인증을 관리하기 때문에 무상태(Stateless) 방식으로 작동한다. 
- 이는 RESTful API와 같은 분산 시스템에서 많이 사용된다.
### 토큰
- 사용자를 구별할 수 있는 문자열이다.
- 서버가 자기만의 노하우로 토큰을 만들어준다.

### 동작 방식
1. 사용자가 로그인
   - 사용자가 로그인 요청을 서버에 보낸다. 
   - 이때 사용자는 일반적으로 사용자명과 비밀번호를 전송한다.
2. 서버가 사용자 인증
   - 서버는 사용자명과 비밀번호를 확인하여 사용자가 올바른 자격을 가지고 있는지 확인한다.
3. 토큰 발급
   - 인증에 성공하면, 서버는 사용자의 정보 또는 권한을 포함한 토큰을 생성하여 클라이언트에게 반환한다. 
   - 이 토큰은 주로 JWT(JSON Web Token) 형식을 사용한다.
4. 클라이언트가 토큰 저장
   - 클라이언트는 이 토큰을 브라우저의 로컬 스토리지(Local Storage) 또는 세션 스토리지(Session Storage) 등에 저장한다.
   - 쿠키에 저장하는 경우도 있다.
5. 토큰을 포함한 요청
   - 이후 클라이언트는 서버에 요청을 보낼 때마다 이 토큰을 HTTP 요청 헤더에 포함시켜 인증을 처리한다.
   - 일반적으로 Authorization 헤더에 Bearer <토큰> 형식으로 토큰을 포함한다.
6. 서버가 토큰 검증
   - 서버는 클라이언트로부터 전달받은 토큰이 유효한지 확인한다.
   - 토큰이 유효하다면, 서버는 요청을 처리하고 필요한 자원에 접근을 허용한다.
7. 응답 반환
   - 서버는 클라이언트에게 요청된 데이터를 반환하거나, 필요한 처리를 수행한다.

```
Authorization: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9
```

![img](img/토큰%20기반.png)

- Basic 인증과 다른 점은 아이디와 비밀번호를 매번 네트워크를 통해 전송해야 할 필요가 없어 보안 측면에서 조금 더 안전하다.
- 또 토큰은 서버가 마음대로 생성할 수 있으므로 사용자의 인가 정보(일반유저, 관리자) 또는 유효기간을 다르게 정하거나 임의로 로그아웃 할 수도 있다.

## JSON 웹 토큰(JWT, JSON WEB TOKEN)
- SON 형식으로 사용자 정보를 저장하고 **서명(Signature)**을 통해 토큰의 무결성을 검증하는 토큰 기반 인증 방식이다.
- JWT는 무상태(Stateless) 방식으로, 서버가 사용자 정보를 별도로 저장하지 않고도 클라이언트를 인증할 수 있기 때문에 분산 시스템이나 RESTful API에서 많이 사용된다.

```
※ 전자서명이란?
서명하고 싶은 메시지를 해시함수를 이용해 축약한 후 개인키로 암호화 했을 때 나오는 결과값을 의미한다.

해시 함수(Hash Function)는 임의의 크기를 가진 데이터를 고정된 크기의 값으로 변환하는 함수이다.
개인 키는 주로 데이터의 암호화 해제 또는 디지털 서명을 만드는 데 사용되며, 오직 소유자만이 알고 있어야 한다.
```

### JWT구조
- JWT는 세 부분으로 나뉜다.
1. 헤더(Header)
2. 페이로드(Payload)
3. 서명(Signature)
- 이 세 부분을 Base64 URL 인코딩으로 인코딩 한 후 마침표로 구분해 하나의 문자열로 합친것이 JWT이다.

```
Authorization: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOiIxMjM0NTY3ODkwIiwibmFtZSI6IkpvaG4gRG9lIiwiaWF0IjoxNTE2MjM5MDIyfQ.SflKxwRJSMeKKF2QT4fwpMeJf36POk6yJV_adQssw5c
```
- 인코딩된 토큰을 Base64로 디코딩하면 헤더,페이로드,서명을 분리할 수 있다.

```json
{
  "alg": "HS256",
  "typ": "JWT"
}.
{
  "sub": "1234567890",
  "iss": "demo app",
  "exp": 1596597657,
  "iat": 1516239022
}.
SflKxwRJSMeKKF2QT4fwpMeJf36POk6yJV_adQssw5c
```
### Header
- alg: 사용할 해싱 알고리즘. 예를 들어 HS256(HMAC-SHA256).
- typ: 토큰의 타입, 여기서는 JWT

### 페이로드(Payload)
- 페이로드는 토큰에 담을 **클레임(Claims)**을 포함한다. 
- 클레임은 JWT에서 사용자 또는 시스템과 관련된 정보를 전달하기 위한 데이터이다. 
- 페이로드에는 여러 유형의 클레임이 포함될 수 있다

- sub : 사용자 ID 또는 주제(subject). 토큰의 주인을 의미한다.
- iss : Issuer를 줄인말. 이 토큰을 발행한 주체를 의미한다.
- iat : issued at를 줄인말. 토큰이 발행된 날짜와 시간을 의미한다.
- exp : expiration을 의미한다. 토큰이 만료되는 시간을 의미한다.

### Signature
- 토큰을 발행한 주체 Isuuer가 발행한 서명
- 토큰의 헤더와 페이로드를 각각 Base64로 인코딩한 뒤, 비밀키(Secret Key)와 함께 선택한 알고리즘(HMAC, RSA 등)을 사용하여 해싱한 값이다.
- 시그니처(Signature)는 토큰이 위변조되지 않았는지 검증하는 역할을 한다.
- 시그니처가 중요한 이유는, 클라이언트가 JWT 토큰을 서버에 보낼 때 서버는 시그니처를 다시 계산하고, 클라이언트가 보낸 시그니처와 비교해서 토큰이 변조되었는지 확인할 수 있기 때문이다.

## User 레이어 구현
- 사용자를 관리하기 위해서는 유저에 관려된 모델,서비스,레포지토리,컨트롤러가 필요하다

## UserEntity
- com.example.demo.model패키지에 UserEntity클래스 만들기
```java
@Data // Lombok을 사용하여 getter, setter, toString, equals, hashCode 등을 자동 생성해준다.
@Entity // JPA에서 엔티티 클래스임을 나타낸다. 이 클래스는 데이터베이스 테이블과 매핑된다.
@Builder // Lombok의 Builder 패턴을 사용하여 객체를 생성할 수 있도록 한다.
@NoArgsConstructor // 기본 생성자를 자동으로 생성해준다.
@AllArgsConstructor // 모든 필드를 인자로 받는 생성자를 자동으로 생성해준다.
@Table(uniqueConstraints = {@UniqueConstraint(columnNames="username")}) 
// 테이블에서 username 컬럼이 유니크하도록 설정한다. 즉, 동일한 username을 가진 유저는 중복으로 생성될 수 없다.
public class UserEntity {

    @Id // JPA에서 이 필드가 테이블의 Primary Key임을 나타낸다.
    @GeneratedValue(generator="system-uuid") // id 필드는 자동으로 생성된다. 여기서는 UUID 전략을 사용한다.
    @GenericGenerator(name="system-uuid", strategy="uuid") 
    // Hibernate에서 제공하는 UUID를 생성하는 커스텀 전략을 사용한다. system-uuid라는 이름으로 UUID를 생성하는 방식이다.
    private String id; // 유저에게 고유하게 부여되는 ID. UUID로 생성되며 고유한 값이다.

    @Column(nullable=false) // username 컬럼은 null 값을 허용하지 않는다.
    private String username; // 아이디로 사용할 유저네임. 이메일일 수도 있고, 그냥 문자열일 수도 있다.

    private String password; // 유저의 패스워드.

    private String role; // 유저의 권한. 예를 들어 "관리자", "일반사용자"와 같은 값이 들어갈 수 있다.

    private String authProvider; // 이후 OAuth에서 사용할 유저 정보 제공자 : github
}
```
- 보통의 경우는 무조건 값이 들어가야 하는게 맞지만 password에 null값이 허용이 된다.
- sso을 이용해 로그인 하는 경우에는 비밀번호가 필요 없기 때문이다.
- 반드시 비밀번호를 입력하도록 규제하면 SSO 구현시 문제가 생기므로 처음부터 null을 입력할 수 있도록 했다.
- 대신 회원가입을 구현하는 컨트롤러에서 password를 반드시 입력하도록 하는 방법이 있다.

# SSO(Single Sign-On)란?

SSO(Single Sign-On)는 **한 번의 로그인**으로 여러 개의 애플리케이션이나 시스템에 접근할 수 있게 해주는 인증 방식이다. 즉, 사용자가 한 번 로그인하면 이후 다른 시스템이나 서비스에도 추가로 로그인할 필요 없이 자동으로 접근할 수 있다.

## SSO의 주요 개념

1. **중앙 인증 시스템**
   - SSO는 사용자의 인증 정보를 중앙에서 관리하는 시스템이 있어야 한다. 이 중앙 인증 시스템에서 사용자가 인증되면, 그 정보가 다른 시스템에 전달되어 사용자는 추가 로그인을 요구받지 않는다.

2. **토큰 기반 인증**
   - SSO는 보통 인증이 완료된 후 사용자에게 **토큰**을 발급한다. 이 토큰을 가지고 사용자는 다양한 서비스에 접근할 수 있게 된다. 일반적으로 SAML(Security Assertion Markup Language), OAuth, JWT(JSON Web Token) 같은 기술이 사용된다.

3. **편리성**
   - 사용자는 여러 번 로그인할 필요가 없기 때문에 사용자 경험이 크게 향상된다. 특히 대규모 시스템에서는 다양한 애플리케이션에 접속할 때마다 로그인하는 번거로움이 없어지기 때문에 매우 유용하다.

4. **보안**
   - SSO는 보안 관점에서 유리하다. 사용자 비밀번호를 여러 시스템에 저장하지 않고 중앙에서만 관리하므로, 보안 위험이 줄어든다. 또한 SSO 시스템에서 강력한 인증 방식을 적용하면, 여러 시스템에 걸쳐 강화된 보안이 적용된다.

## SSO의 작동 방식
1. **사용자 로그인 요청**: 사용자가 애플리케이션 A에 접근하려고 하면, 로그인 화면으로 리디렉션된다. 이 로그인 화면은 SSO 서버로부터 제공된다.
   
2. **인증 요청**: SSO 서버는 사용자에게 인증을 요구하고, 사용자는 ID와 비밀번호를 입력한다.

3. **토큰 발급**: 인증이 성공하면 SSO 서버는 사용자에게 인증 토큰(예: SAML, JWT)을 발급해준다.

4. **접근 허용**: 애플리케이션 A는 SSO 서버로부터 받은 토큰을 확인하고, 해당 사용자가 인증되었음을 확인한 후 애플리케이션에 접근을 허용한다.

5. **다른 애플리케이션에 접근**: 이후 사용자가 애플리케이션 B에 접근하려고 할 때, SSO 서버는 사용자가 이미 인증된 상태임을 인식하고 자동으로 접근을 허용한다. 사용자는 다시 로그인할 필요가 없다.

## SSO의 장점

- **사용자 편의성**: 한 번 로그인으로 여러 시스템에 접근할 수 있어, 사용자 입장에서 매우 편리하다.
- **보안 관리 강화**: 비밀번호를 여러 시스템에 저장할 필요가 없고, 중앙에서 일관된 보안 정책을 적용할 수 있다.
- **효율성**: 사용자가 여러 번 로그인을 할 필요가 없어 로그인 절차에서 오는 중복된 작업을 제거할 수 있다.

## SSO의 단점

- **단일 실패 지점**: 만약 SSO 시스템에 문제가 발생하거나 해킹당하면, 모든 서비스에 대한 접근이 차단되거나 보안이 취약해질 수 있다.
- **복잡한 설정**: 여러 시스템과의 통합 및 보안 관리가 복잡할 수 있다. 또한 각 서비스와의 연동을 신중하게 설정해야 한다.

## SSO를 사용하는 대표적인 예시

- **Google 계정으로 로그인**: 한 번 구글 계정에 로그인하면, Gmail, Google Drive, YouTube 등 여러 구글 서비스에 자동으로 로그인된다.
- **기업 내 SSO**: 대기업에서는 직원들이 한 번의 로그인을 통해 사내 여러 시스템(메일, 문서 관리, 인사 시스템 등)에 접근할 수 있도록 SSO를 활용하는 경우가 많다.

SSO는 사용자 경험을 개선하고, 보안 및 관리 측면에서 큰 장점을 제공하는 인증 방식이다.

## UserRepository
- com.eaxmple.demo.persistence에 UserRepository인터페이스 만들기
```java
package com.example.demo.persistence;
@Repository
public interface UserRepository extends JpaRepository<UserEntity, String>{
    UserEntity findByUsername(String username);// username 값으로 UserEntity를 찾아 반환한다.
    Boolean existsByUsername(String username);//해당 username이 존재하면 true, 존재하지 않으면 false를 반환한다.
    UserEntity findByUsernameAndPassword(String username, String password);//username과 password를 기준으로 UserEntity를 조회하는 메서드다.
    //And가 사용되었으므로, 두 필드를 모두 만족하는 데이터를 찾는 조건으로 쿼리가 자동 생성된다.
}
```

## UserService
- com.example.demo.service패키지에 UserService클래스 만들기
- UserService는 TodoService처럼 유저 데이터베이스에 저장된 윶를 가져올 때 사용한다.
- UserRepository를 이용해 사용자를 생성하고, 로그인 시 인증에 사용할 메서드를 작성한다.
```java
package com.example.demo.service;

import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.stereotype.Service;

import com.example.demo.model.UserEntity;
import com.example.demo.persistence.UserRepository;

import lombok.extern.slf4j.Slf4j;

@Service // 이 클래스가 스프링의 서비스 계층에 속하는 빈(Bean)임을 나타낸다.
@Slf4j // Lombok을 사용하여 로깅 기능을 자동으로 추가한다. log 객체를 통해 로그를 기록할 수 있다.
public class UserService {

    @Autowired // 스프링이 UserRepository 타입의 빈을 자동으로 주입해준다.
    private UserRepository repository; // UserRepository를 통해 데이터베이스에 접근하는 역할을 한다.

    public UserEntity create(UserEntity userEntity) {
        // 주어진 UserEntity가 null이거나 username이 null인 경우, 예외를 던진다.
        if(userEntity == null || userEntity.getUsername() == null) {
            throw new RuntimeException("Invalid arguments"); // 유효하지 않은 인자에 대해 예외를 발생시킨다.
        }

        final String username = userEntity.getUsername(); // UserEntity에서 username을 가져온다.
        
        // 주어진 username이 이미 존재하는 경우, 경고 로그를 남기고 예외를 던진다.
        if(repository.existsByUsername(username)) {
            log.warn("Username already exists {}", username); // 이미 존재하는 username에 대해 로그를 기록한다.
            throw new RuntimeException("Username already exists"); // 중복된 username인 경우 예외를 던진다.
        }
        
        // username이 중복되지 않았다면 UserEntity를 데이터베이스에 저장하고 반환한다.
        return repository.save(userEntity); // UserRepository의 save 메서드를 통해 userEntity를 저장한다.
    }

    // 주어진 username과 password로 UserEntity를 조회한다.
    public UserEntity getByCredentials(String username, String password) {
        // UserRepository의 findByUsernameAndPassword 메서드를 사용하여 유저 정보를 조회한다.
        return repository.findByusernameAndPassword(username, password);
    }
}
```
## UserDTO
- com.example.demo.dto에 UserDTO 클래스 만들기
```java
@Data
@Builder
@NoArgsConstructor
@AllArgsConstructor
public class UserDTO {

	private String token;
	private String username;
	private String password;
	private String id;
}
```

## UserController
- com.example.demo.controller패키지에 UserController클래스 생성하기
- 유저 서비를 이용해 현재 유저를 가져오는 기능과 회원가입 기능을 구현한다.
```java
package com.example.demo.controller;

import com.example.demo.dto.ResponseDTO;
import com.example.demo.dto.UserDTO;
import com.example.demo.model.UserEntity;
import com.example.demo.service.UserService;
import lombok.extern.slf4j.Slf4j;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.http.ResponseEntity;
import org.springframework.web.bind.annotation.PostMapping;
import org.springframework.web.bind.annotation.RequestBody;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.RestController;

@Slf4j // Lombok을 사용하여 로그를 남길 수 있는 log 객체를 자동으로 생성한다.
@RestController // 이 클래스가 RESTful 웹서비스의 컨트롤러 역할을 한다는 것을 나타낸다.
@RequestMapping("/auth") // 이 컨트롤러의 기본 URI 경로가 "/auth"로 설정된다.
public class UserController {

    @Autowired // UserService 타입의 빈을 자동으로 주입받는다.
    private UserService userService; // 사용자 관련 비즈니스 로직을 처리하는 서비스 클래스.

    @PostMapping("/signup") // POST 요청을 처리하는 메서드로, 경로는 "/auth/signup"이다.
    public ResponseEntity<?> registerUser(@RequestBody UserDTO userDTO) { 
        // 요청 본문에 포함된 UserDTO 객체를 수신하여 처리한다.
        try {
            // UserDTO를 기반으로 UserEntity 객체를 생성한다.
            UserEntity user = UserEntity.builder()
                            .username(userDTO.getUsername()) // UserDTO에서 username 값을 가져온다.
                            .password(userDTO.getPassword()) // UserDTO에서 password 값을 가져온다.
                            .build(); // UserEntity 객체를 빌드한다.

            // UserService를 이용해 새로 만든 UserEntity를 데이터베이스에 저장한다.
            UserEntity registeredUser = userService.create(user);

            // 등록된 UserEntity 정보를 UserDTO로 변환하여 응답에 사용한다.
            UserDTO responseUserDTO = UserDTO.builder()
                            .id(registeredUser.getId()) // 등록된 유저의 ID를 가져온다.
                            .username(registeredUser.getUsername()) // 등록된 유저의 username을 가져온다.
                            .build(); // UserDTO 객체를 빌드한다.

            // 성공적으로 저장된 유저 정보를 포함한 HTTP 200 응답을 반환한다.
            return ResponseEntity.ok(responseUserDTO);
        } catch (Exception e) {
            // 예외가 발생한 경우, 에러 메시지를 포함한 ResponseDTO 객체를 만들어서 응답한다.
            ResponseDTO responseDTO = ResponseDTO.builder().error(e.getMessage()).build();

            // HTTP 400 상태 코드를 반환하고, 에러 메시지를 응답 본문에 포함시킨다.
            return ResponseEntity
                            .badRequest() // HTTP 400 응답을 생성한다.
                            .body(responseDTO); // 에러 메시지를 포함한 응답 본문을 반환한다.
        }
    }

    @PostMapping("/signin") // POST 요청을 처리하는 메서드로, 경로는 "/auth/signin"이다.
    public ResponseEntity<?> authenticate(@RequestBody UserDTO userDTO) {
        // 요청 본문으로 전달된 UserDTO의 username과 password를 기반으로 유저를 조회한다.
        UserEntity user = userService.getByCredentials(
                        userDTO.getUsername(), // UserDTO에서 username 값을 가져온다.
                        userDTO.getPassword()); // UserDTO에서 password 값을 가져온다.

        // 사용자가 존재하면
        if (user != null) {
            // 인증에 성공한 경우 유저 정보를 UserDTO로 변환하여 응답에 사용한다.
            final UserDTO responseUserDTO = UserDTO.builder()
                            .id(user.getId()) // 유저의 ID를 UserDTO에 설정한다.
                            .username(user.getUsername())
                            .build(); // UserDTO 객체를 빌드한다.

            // 성공적으로 인증된 유저 정보를 포함한 HTTP 200 응답을 반환한다.
            return ResponseEntity.ok().body(responseUserDTO);
        } else {
            // 유저가 존재하지 않거나 인증 실패 시 에러 메시지를 포함한 ResponseDTO를 반환한다.
            ResponseDTO responseDTO = ResponseDTO.builder()
                            .error("Login failed.") // 에러 메시지를 설정한다.
                            .build(); // ResponseDTO 객체를 빌드한다.

            // HTTP 400 상태 코드를 반환하고, 에러 메시지를 응답 본문에 포함시킨다.
            return ResponseEntity
                            .badRequest() // HTTP 400 응답을 생성한다.
                            .body(responseDTO); // 에러 메시지를 포함한 응답 본문을 반환한다.
        }
    }
}
```
- 포스트맨을 열고 post로 요청을 해본다.
- request에 아이디와 비밀번호를 실어서 보낸다.
- 응답에는 비밀번호를 보낼 이유가 없어서 뺐다.
- 하지만 추가할 때 비밀번호가 잘 들어왔는지 검증은 해야 한다.
![img](img/회원추가.png)

- 추가가 잘되었다면 로그인 요청도 해보자

![img](img/로그인.png)

### 주의점
- 회원가입과 로그인이 잘 작동하는 것을 알 수 있다.
- 하지만 이렇게 구성했을 때의 문제점은 무엇일까?

1. 로그인만 되고 로그인 상태가 유지되지 않는다.
    - 로그인을 구현했지만 이 다른 API는 이 유저가 로그인 했는지 아닌지 모른다.
    - 우리의 REST API는 상태가 없으므로 로그인 상태를 기억하지 않기 때문이다.
2. 우리가 지금까지 작성한 API는 유저의 로그인 여부 자체를 확인하지 않는다.
     - createTodo API에서는 임의로 유저 아이디를 정해줬다.
     - 따라서 현재 로그인 기능이 있어도, 내가 로그인하든 여러분이 로그인 하든 같은 Todo 리스트를 보게 되는 셈이다.
3. 패스워드를 암호화 하지 않는다.
     - 이것은 보안 규정에 위배되는 사항이다.

### 정리
- 사용자를 관리하는 데 필요한 API를 구성해봤다.
- 근본적으로는 Todo기능을 구현할 때 했던 작업과 같은 작업이고, 스프링 시큐리티와는 상관없는, 즉 우리 애플리케이션이 유저를 관리하기 위해 자체 개발한 서비스이다.
- 우리는 User관련 레이어를 구현한 후 현재 구현의 문제점을 알아봤다.
- 기본적으로 로그인 상태가 유지되지 않는다는 점이 가장 큰 문제였다.



