# 인증프론트엔드통합
- 백엔드 서비스에 인증과 인가를 구현하고 나서 프론트앤드 애플리케이션을 다시 시작해보면 동작하지 않을 것이다.
- 백엔드가 인증을 하기 시작했기 때문이다.
- 애플리케이션을 정상적으로 사용하기 위해선 프론트엔드에도 인증을 구현해줘야 한다.

## 로그인, 회원가입
- 프론트엔드 애플리케이션은 이제부터 백엔드에 HTTP요청을 보냈을 때, 403이 날아오면 토큰을 어딘가에 저장해놓고 로그인 페이지로 리다이렉트 해야 한다.
- 저장해놓은 토큰을 Http요청을 보낼 때마다 헤더에 Bearer 토큰으로 지정해줘야 한다.
 
### 라우팅
- 우리가 리액트에서 사용하는 라우팅은 서버-사이드 라우팅이 아닌 클라이언트-사이드 라우팅이다.
- 클라이언트-사이드 라우팅은 서버로 어떠한 요청도 날리지 않는다.

### 우리 프로그램에 적용시키기
1. http://localhost:3000에 접속하면 프론트엔드 서버가 리액트 애플리케이션을 반환한다.
   1. 이 애플리케이션은 앞으로 브라우저에서 필요한 모든 리소스(html,css,js)를 갖고있다.
2. http://localhost:3000/login을 주소창에 치면 리액트 라우터가 가로챈다.
3. 리액트 라우터의 로직은 URL을 해석해 Login 컴포넌트를 렌더링한다.
4. Login 페이지를 가져오는 두 번째 요청은 클라이언트-사이드이기 때문에 인터넷이 끊기더라도 실행된다.

### 로그인 컴포넌트
- 라우팅을 테스팅 하기 위해 src폴더에 기능이 없는 Login.js를 추가한다.
```js
import React from "react";

const Login = () => {
    return(
        <p> 로그인 페이지</p>
    )
}
export default Login;
```

### AppRouter 컴포넌트
- AppRouter.js에 모든 라우팅 규칙을 작성한다.
```js
import React from "react";
import "./index.css";
import App from "./App";
import Login from "./Login";
import {BrowerRouter, Routes, Route} from "react-router-dom";
import {Typography,Box} from "@mui/material";

function Copyright(){
    return(
        <Typography variant="body2" color="textSecondary" align="center">
            {"Copyright "}
            fsoftwareengineer, {new Date().getFullYear()}
            {"."}
        </Typography>
    );
}

function AppRouter(){
    return(
        <div>
            <BrowerRouter>
                <Routes>
                    <Route path="/" element={<App />}>
                    <Route path="login" element={<Login />}>
                </Routes>
            </BrowerRouter>
            <Box mt={5}>
                <Copyright />
            </Box>
        </div>
    )
}
```

### \<BrowerRouter\>
- 브라우저가 관리하는 히스토리를 사용해 브라우저와 리액트 사이의 URL을 동기화 하므로 뒤로가기가 잘 작동한다.

### \<Routes\>와 \<Route\>
- \<Route\>는 실제 경로를 지정해주기 위한 컴포넌트이다.
  - 예를 들어 http://localhost:3000/login 경로는 Login컴포넌트를 렌더링하기 위해 \<Route path="login" element={\<Login />}같이 선언했다.
- \<Routes\>는 \<Route\>를 관리하고 실제로 가장 적합한 \<Route\>를 찾아주는 컴포넌트다.
- URL경로가 바뀌는 경우, \<Routes\>컴포넌트가 자신에게 등록된 모든 \<Route\>컴포넌트를 검토하고 가장 적합한 \<Route\>를 찾는다.

### index.js 수정하기
- 기존에는 ReactDOM에 App 컴포넌트를 넘겨줬다. 
- 하지만 이제는 경로에 따라 실행되는 컴포넌트가 다르므로 그 정보를 갖고 있는 AppRouter를 가장 먼저 렌더링해야한다.
- index.js로 가서 가장 처음 렌더링되는 컴포넌트가 AppRouter컴포넌트가 되도록 수정한다.
```js
import React from 'react';
import './index.css';
import AppRouter from './AppRouter';
import reportWebVitals from './reportWebVitals';

const root = ReactDOM.createRoot(document.getElementById('root'));
root.render(
  <React.StrictMode>
    <AppRouter tab="home"/>
  </React.StrictMode>
);

// If you want to start measuring performance in your app, pass a function
// to log results (for example: reportWebVitals(console.log))
// or send to an analytics endpoint. Learn more: https://bit.ly/CRA-vitals
reportWebVitals();
```
- 프론트엔드를 재시작 한 후 http://localhost:3000/login페이지로 들어가보자
- 로그인 페이지 하고 문구가 뜬다면 라우팅이 제대로 동작하는 것이다.

### 접근 거부시 로그인 페이지로 라우팅하기
- 접근 거부를 받는 경우 /login으로 라우팅 하는 코드를 작성해보자.
- 우리는 http://localhost:9090/todo에게 요청을 했을 때 거부를 받을 수 있다.
- App.js의 useEffect 또는 add,delete,update를 확인해보면 API콜을 위해 ApiService의 call메서드를 사용하는 것을 알 수 있다.
- 또한 HTTP메서드의 종류에 상관 없이 로그인 하지 않은 경우 로그인 페이지로 리다이렉트 해야한다.
- 따라서 리다이렉트하는 로직을 ApiService의 어딘가에 추가해야 한다.

### ApiService.js 수정하기
- call메서드는 결국 axios메서드를 호출한다.
- axios를 이용하면 API콜을 한 후 .then을 이용해 HTTP응답을 받아올 수 있다.
- 받아온 응답의 Status가 200이면 요청이 잘 수행된 것이다.
- Status값이 403이라면 인증에 실패해 접근이 거부된 것이다.
- 따라서 Status가 403인경우 login화면으로 리다이렉트해주는 로직을 작성해야 한다.