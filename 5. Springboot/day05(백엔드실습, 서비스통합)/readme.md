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

