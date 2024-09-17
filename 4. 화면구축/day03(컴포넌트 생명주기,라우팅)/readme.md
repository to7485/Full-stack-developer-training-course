## 리액트 컴포넌트 생명주기
- 리액트 컴포넌트는 **생성, 업데이트, 제거**라는 세 가지 주요 단계에서 작동하며, 각 단계에서 특정한 메서드들이 실행된다.
-  생명주기 메서드를 통해 컴포넌트가 언제 생성되었고, 언제 상태나 props가 변경되었으며, 언제 제거될지 제어할 수 있다.
-  컴포넌트 생명주기는 클래스형 컴포넌트에서 주로 사용되었으며, 함수형 컴포넌트에서는 useEffect 훅을 사용해 비슷한 동작을 구현할 수 있다.

## 컴포넌트 생명주기 메서드

### 1. 생성(Mount)
#### constructor()
- 컴포넌트가 생성될 때 가장 먼저 호출되며, 초기 상태(state)를 설정할 수 있다.
#### render()
- UI를 렌더링하는 메서드로, JSX를 반환한다.
#### componentDidMount()
- 컴포넌트가 처음 렌더링된 후 호출된다. 
- 주로 API 호출 등 초기 데이터를 가져오는 작업을 수행한다.

### 2 업데이트(Updating)
- 컴포넌트가 업데이트될 때, 즉 props나 state가 변경될 때 호출되는 메서드들이다.

#### shouldComponentUpdate()
- 컴포넌트가 업데이트될지 여부를 결정한다. 
- 성능 최적화를 위해 사용된다. 
- true를 반환하면 업데이트가 진행되고, false를 반환하면 업데이트가 중단된다.
#### componentDidUpdate()
- 컴포넌트가 업데이트된 후 호출된다. 
- 업데이트 직후에 추가 작업을 수행할 때 사용된다.

### 3. 제거(Unmounting)
- 컴포넌트가 DOM에서 제거될 때 호출되는 메서드다.
#### componentWillUnmount()
- 컴포넌트가 제거되기 직전에 호출되며, 타이머 정리, 구독 해제 등 정리 작업(clean-up)을 수행한다.


## 클래스형 컴포넌트에서 생명주기 사용하기
```js
import React from 'react';

class LifecycleExample extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      count: 0,
    };
    console.log('constructor: 컴포넌트가 생성됨');
  }

  componentDidMount() {
    console.log('componentDidMount: 컴포넌트가 화면에 렌더링됨');
    // 예시: API 요청을 통해 데이터 가져오기
  }

  shouldComponentUpdate(nextProps, nextState) {
    console.log('shouldComponentUpdate: 컴포넌트가 업데이트될지 결정됨');
    // true를 반환하면 컴포넌트가 업데이트됨
    return true;
  }

  componentDidUpdate(prevProps, prevState) {
    console.log('componentDidUpdate: 컴포넌트가 업데이트됨');
    // 예시: 상태가 변경된 후 추가 작업 수행
  }

  componentWillUnmount() {
    console.log('componentWillUnmount: 컴포넌트가 제거됨');
    // 예시: 타이머나 구독 해제
  }

  handleIncrement = () => {
    this.setState((prevState) => ({
      count: prevState.count + 1,
    }));
  };

  render() {
    console.log('render: UI 렌더링됨');
    return (
      <div>
        <h1>Count: {this.state.count}</h1>
        <button onClick={this.handleIncrement}>Increment</button>
      </div>
    );
  }
}

export default LifecycleExample;

```

## 함수형 컴포넌트에서 생명주기와 유사한 동작 구현
- 함수형 컴포넌트에서는 생명주기 대신 useEffect훅을 사용해 비슷한 효과를 구현할 수 있다.

## useEffect 훅
- React의 함수형 컴포넌트에서 사이드 이펙트를 처리하는 데 사용된다.
- 사이드 이펙트는 컴포넌트의 렌더링과는 직접적으로 관련이 없는 작업들을 말한다.
- 예를 들어 데이터 fetching, 구독 설정, 타이머 설정 등이 있습니다.
- useEffect 훅은 컴포넌트가 렌더링된 후에 특정 작업을 수행하거나 컴포넌트가 업데이트되었을 때 실행되는 코드를 작성할 수 있게 해준다.

### useEffect 사용법
```js
import React, { useEffect, useState } from 'react';

function MyComponent() {
  const [count, setCount] = useState(0);

  useEffect(() => {
    // 이 부분이 사이드 이펙트 코드입니다.
    document.title = `You clicked ${count} times`;

    // 클린업 함수 (선택적)
    return () => {
      // 컴포넌트가 언마운트되거나 의존성 배열의 값이 변경되기 전에 실행됩니다.
    };
  }, [count]); // 의존성 배열

  return (
    <div>
      <p>You clicked {count} times</p>
      <button onClick={() => setCount(count + 1)}>Click me</button>
    </div>
  );
}
```
### 주요 개념
1. 첫 번째 인자 : 사이드 이펙트 함수
    - useEffect의 첫 번째 인자는 사이드 이펙트 로직을 포함한 함수다.
    - 이 함수는 컴포넌트가 렌더링된 후에 실행된다.

2. 두 번째 인자: 의존성 배열
    - 이 배열에 포함된 값들이 변경될 때만 사이드 이펙트 함수가 다시 실행된다.
    - 배열을 생략하면 사이드 이펙트 함수는 매 렌더링마다 실행된다.
    - 배열이 빈 경우, 사이드 이펙트 함수는 컴포넌트가 처음 마운트될 때만 실행됩니다.

3. 클린업 함수 (선택적)
    - 사이드 이펙트 함수는 선택적으로 클린업 함수를 반환할 수 있다.
    - 이 클린업 함수는 컴포넌트가 언마운트되거나 의존성 배열의 값이 변경되기 전에 실행된다.
    - 예를 들어, 타이머를 설정한 경우 클린업 함수에서 타이머를 정리할 수 있다.
  
### 사용 예시
- 데이터 fetching
    - 컴포넌트가 마운트될 때 데이터를 가져오고, 컴포넌트가 언마운트될 때 요청을 취소하거나 클린업 작업을 수행할 수 있다.
```js
useEffect(() => {
  const fetchData = async () => {
    const response = await fetch('https://api.example.com/data');
    const data = await response.json();
    // 데이터 상태를 설정
  };

  fetchData();

  // 클린업 함수 (선택적)
  return () => {
    // 예를 들어, 요청 취소 로직
  };
}, []); // 빈 배열: 컴포넌트가 처음 마운트될 때만 실행
```
### 의존성 배열의 종류
1. 의존성 배열이 비어 있는 경우 ([])
- 이 경우, useEffect는 컴포넌트가 처음 마운트될 때만 실행된다.
- 이후에는 사이드 이펙트가 다시 실행되지 않습니다.
```js
useEffect(() => {
  // 이 사이드 이펙트는 컴포넌트가 처음 마운트될 때만 실행됩니다.
  console.log('Component mounted');

  // 클린업 함수 (선택적)
  return () => {
    console.log('Component will unmount');
  };
}, []); // 빈 배열
```
2. 의존성 배열에 상태나 프로퍼티를 포함하는 경우
- 이 경우, 의존성 배열에 포함된 값들이 변경될 때마다 useEffect의 사이드 이펙트 함수가 실행된다.
```js
const [count, setCount] = useState(0);

useEffect(() => {
  console.log(`Count has changed to ${count}`);

  // 클린업 함수 (선택적)
  return () => {
    console.log('Cleanup before the next effect or unmount');
  };
}, [count]); // count가 변경될 때마다 실행

```
3. 의존성 배열이 없는 경우
- 사이드 이펙트 함수는 컴포넌트가 렌더링될 때마다 실행된다.
- 이는 의존성 배열을 생략한 경우의 기본 동작입니다.

## useEffect를 활용한 생명주기 예시
```js
import React, { useState, useEffect } from 'react';

const TimerFunction = () => {
  const [time, setTime] = useState(0);

  useEffect(() => {
    const timer = setInterval(() => {
      setTime((prevTime) => prevTime + 1);
    }, 1000);

    return () => {
      clearInterval(timer);
    };
  }, []);

  return (
    <div>
      <h1>Timer: {time} seconds</h1>
    </div>
  );
};

export default TimerFunction;
```

## useRef 훅
- React에서 DOM 요소나 컴포넌트 인스턴스에 대한 레퍼런스를 유지할 때 사용된다.
- useState와 달리 렌더링 사이에서 값을 저장할 수 있으며, 컴포넌트가 다시 렌더링되더라도 값이 유지된다.
- 컴포넌트 렌더링과 관련이 없는 값을 저장하거나, DOM 요소에 직접 접근할 때 유용합니다.

### 생성
```js
const 변수명 = useRef(초기값)

함수의 실행 결과로 {current : 초기값}을 지닌 객체가 반환된다.
```

### 주요 기능
1. DOM 요소에 접근하기
    - 컴포넌트가 렌더링된 후 DOM 요소에 접근할 수 있다.
    - 이 기능은 폼 요소에 포커스를 설정하거나, 스크롤 위치를 조정하는 등의 작업에 유용하다.
    - 바닐라 자바스크립트의 getElementById, querySelector와 비슷하다.
```js
const App = () => {

const countVar = 0;

const increaseVar = () => {
countVar = countVar +1;
}

return (
<div>
<p>Var: {countVar} </p>
{/*버튼을 누르고 렌더링을 해주면 var는 몇이 나올까?
정답은 0이다. 렌더링을 해준다는 것은 함수를 처음부터 다시 실행한다는 것을 의미한다.
렌더링을 할때마다 App컴포넌트를 나타내는 함수가 다시 불린다. 그러면 함수가 불릴때마다 이 함수 내부에 있는 변수들이 다시 초기화가 된다.
따라서 렌더링이 될때마다 const countVar = 0; 를 통해서 countVar라는 변수에는 계속해서 0으로 초기화가 된다.
*/}
<button onClick={increaseVar}> Var올려 </button>
</div>
)
```
```JS
import React, { useRef } from 'react';

function FocusInput() {
  // useRef를 사용하여 input 요소에 대한 레퍼런스 생성
  const inputRef = useRef(null);

  const handleClick = () => {
    // input 요소에 포커스를 설정
    inputRef.current.focus();
  };

  return (
    <div>
      <input ref={inputRef} type="text" />
      <button onClick={handleClick}>Focus the input</button>
    </div>
  );
}

export default FocusInput;
```
- 실습
```js
import React, { useState, useRef } from "react";

const InputSample = () => {
  const [inputs, setInputs] = useState({
    이름: "",
    nickname: "",
  });

  const nameFocus = useRef();

  const { 이름, nickname } = inputs;

  const onChange = (e) => {
    const { value, name } = e.target;
    setInputs({
      ...inputs,
      [name]: value,
    });
  };

  const onReset = () => {
    setInputs({
      이름: "",
      nickname: "",
    });
    nameFocus.current.focus();
  };
  return (
    <div>
      <input
        name="이름"
        placeholder="이름쓰세요"
        onChange={onChange}
        value={이름}
        ref={nameFocus}
      />
      <input
        name="nickname"
        placeholder="닉네임쓰세요"
        onChange={onChange}
        value={nickname}
      />
      <button onClick={onReset}>초기화</button>
      <div>
        <b>값:</b>
        {이름}({nickname})
      </div>
    </div>
  );
};

export default InputSample;
```
2. 렌더링 간 값 유지하기
    - 렌더링 간에 값을 저장할 수 있다.
    - 이 값은 컴포넌트의 렌더링 사이에서 변경될 수 있지만, 상태 업데이트로 인해 렌더링을 트리거하지 않습니다.
3. 구독 객체나 타이머 ID를 저장하고, 클린업 함수에서 이러한 값을 활용할 수 있습니다.
```js
import React from "react";
import { useState } from "react";
import { useRef } from "react";

function AppRef(){
    const refNum = useRef(0);
    const [stateNum, setStateNum] = useState(0);

    console.log("렌더링 발생");

    const increaseStateNum = ()=>{
        setStateNum((stateNum)=>(stateNum+1));
    }
    
    const increaseRefNum = ()=>{
        refNum.current = refNum.current+1;
        console.log(`refNum : ${refNum.current}`);
    }
    return(
        <>
            <h1>refNum:{refNum.current}</h1>
            <h1>stateNum:{stateNum}</h1>
            <button onClick={increaseRefNum}>refNum + 1 </button>
            <button onClick={increaseStateNum}>stateNum + 1 </button>
        </>
    )
}

export default AppRef;
```

# 리액트 라우터

## 1. 리액트 라우터의 개념
- 리액트는 SPA(Single Page Application)로, 하나의 HTML 페이지에서 여러 컴포넌트를 교체하며 동작한다.
- 그러나 여러 페이지를 가진 웹사이트처럼 URL에 따라 다른 화면을 보여주고 싶을 때가 있다. 
- 사용자가 URL을 변경하거나 네비게이션을 할 때 페이지를 새로고침하지 않고도 URL에 맞는 컴포넌트를 렌더링할 수 있도록 해준다.


## 2. 리액트 라우터의 필요성
### 1. SPA의 특성 유지
- 리액트 애플리케이션은 기본적으로 하나의 HTML 페이지에서 여러 컴포넌트를 전환하면서 동작한다. 
- 리액트 라우터를 사용하면 브라우저의 새로고침 없이도 URL을 변경하고 해당 URL에 맞는 컴포넌트를 렌더링할 수 있다.

### 2. 페이지 전환 시 깜빡임 방지
- 전통적인 멀티 페이지 애플리케이션에서는 사용자가 페이지를 이동할 때마다 전체 페이지를 다시 로드하게 되어 깜빡임 현상이 발생한다. 
- 리액트 라우터는 클라이언트 사이드 라우팅을 통해 페이지 전환 시 깜빡임 현상을 없애고, 보다 매끄럽고 빠른 사용자 경험을 제공한다.

### 3. 브라우저 히스토리 관리
- 리액트 라우터는 브라우저의 히스토리 API를 사용하여 뒤로 가기, 앞으로 가기 등의 네비게이션 기능을 정상적으로 동작하게 한다. 
- 사용자가 페이지를 탐색할 때 히스토리가 관리되므로, 이전 페이지로 쉽게 돌아갈 수 있다.

#### 히스토리 API(History API)
- 브라우저에서 사용자의 탐색 기록(히스토리)을 조작하고 관리할 수 있는 기능을 제공하는 웹 API이다.
- 이 API를 사용하면 JavaScript를 통해 브라우저의 주소(URL)를 변경하거나, 사용자의 브라우저 히스토리를 업데이트할 수 있다. 

### 4. 복잡한 애플리케이션 구조 관리
- 대규모 애플리케이션에서는 여러 개의 페이지와 다양한 경로를 관리해야 한다. 
- 리액트 라우터는 이러한 복잡한 경로 구조를 컴포넌트 형태로 쉽게 관리할 수 있게 해준다.

### 설치
```JS
npm install react-router-dom
```

## 라우팅 예제
### index.js
```js
import React from 'react';
import ReactDOM from 'react-dom';
import { BrowserRouter } from 'react-router-dom';
import App from './App';

ReactDOM.render(
  <BrowserRouter>
    <App />
  </BrowserRouter>,
  document.getElementById('root')
);
```
- BrowserRouter 
  - 브라우저 환경에서 HTML5 히스토리 API를 사용하여 클라이언트 사이드 라우팅을 관리한다.

### App.js에 라우트 정의
- Route 컴포넌트를 사용하여 경로와 렌더링할 컴포넌트를 지정한다.
```js


import React from 'react';
import { Routes, Route } from 'react-router-dom';
import Home from './Home';
import About from './About';

function App() {
  return (
    <div>
      <Routes>
        <Route path="/home" element={<Home />} />
        <Route path="/about" element={<About />} />
      </Routes>
    </div>
  );
}

export default App;
```
### Routes
- 모든 라우트를 그룹화하며, URL 경로에 따라 적절한 라우트를 렌더링한다.
### Route
- URL 경로와 컴포넌트를 매핑하여 특정 경로에 맞는 컴포넌트를 렌더링하는 역할을 한다.

#### Route 컴포넌트의 주요 속성(Props)
1. path
    - URL 경로를 정의한다. 
    - 사용자가 특정 경로에 접근할 때 어떤 컴포넌트를 렌더링할지를 결정하는 데 사용된다.
    - ex) path="/about"는 /about 경로에 접근할 때 렌더링할 컴포넌트를 지정한다.
2. element
    - 경로와 일치할 때 렌더링할 컴포넌트를 지정한다. \<Route> 컴포넌트가 URL 경로와 일치할 경우, element로 지정된 컴포넌트를 렌더링한다.
    - 예: element={\<Home />}는 / 경로에 접근할 때 \<Home> 컴포넌트를 렌더링한다.

### 네비게이션 구현
- Link 컴포넌트를 사용하여 페이지간 이동할 수 있는 링크를 만든다.

### Navbar.js
```js
import React from 'react';
import { Link } from 'react-router-dom';

function Navbar() {
  return (
    <nav>
      <Link to="/home">홈</Link>
      <br/>
      <Link to="/about">소개</Link>
    </nav>
  );
}

export default Navbar;
```
- Link: 사용자가 클릭할 때 해당 경로로 이동시키는 링크를 생성한다.
  - SPA에서 페이지 전환을 처리하기 위해 사용한다.
  - 일반적인 HTML의 \<a>태그와 유사하지만, 페이지 전체를 다시 로드하지 않고도 URL을 변경하고 해당 경로에 맞는 컴포넌트를 렌더링한다.


### Link 컴포넌트의 주요 속성
- to속성 : 이동할 경로를 지정한다. 문자열 또는 객체를 전달할 수 있다.
#### 문자열 형태
```js
<Link to="/경로">
```
#### 객체 형태
```js
<Link
  to={{
    pathname: '/search',
    search: '?query=react',
    hash: '#top',
  }}
>
  검색
</Link>
```
- replace : true로 설정하면 현재 히스토리 엔트리를 대체한다.
```js
<Link to="/login" replace>
  로그인
</Link>

```
- state : 링크를 통해 전달할 추가 상태 정보를 담는다.
```js
<Link
  to={{
    pathname: '/profile',
    state: { fromDashboard: true },
  }}
>
  프로필
</Link>

```

### Link 컴포넌트의 동작 원리
#### 히스토리 API 활용
- Link 컴포넌트를 클릭하면 React Router는 브라우저의 히스토리 스택에 새로운 엔트리를 추가한다.
#### 라우트 매칭
- URL이 변경되면 React Router는 새로운 경로에 매칭되는 컴포넌트를 찾아서 렌더링한다.
#### 페이지 리로드 방지
- 이벤트의 기본 동작을 방지하여 페이지 전체가 다시 로드되는 것을 막는다. 


## 동적 라우트

### 동적 라우트의 개념
- 동적 라우트는 URL의 일부를 변수처럼 사용하여 다양한 경로를 처리할 수 있는 기능이다. 
- 이를 통해 하나의 라우트 설정으로 여러 유사한 경로를 처리할 수 있다.
- 예를 들어, 블로그 애플리케이션에서 각 게시글마다 고유한 ID나 슬러그를 사용하여 상세 페이지를 보여줄 때 동적 라우트를 사용한다.

```
- 정적 라우트 예시: /about, /contact
- 동적 라우트 예시: /posts/1, /posts/2, /users/username
```

### 동적 라우트 설정 방법
- 동적 라우트를 설정하려면 Route 컴포넌트의 path 속성에 콜론(:)을 사용하여 파라미터를 정의한다.
```js
<Route path="/posts/:postId" element={<PostDetail />} />
```

### URL 파라미터 접근 방법
- 동적 라우트로 설정된 경로에서 컴포넌트는 useParams 훅을 사용하여 URL 파라미터에 접근할 수 있다.
```js
import { useParams } from 'react-router-dom';

function PostDetail() {
  const { postId } = useParams();

  // postId를 사용하여 데이터 가져오기 등 작업 수행
  return (
    <div>
      <h2>게시글 상세 페이지</h2>
      <p>게시글 ID: {postId}</p>
    </div>
  );
}
```

## useParam
- React Router에서 제공하는 훅으로, 동적 라우트에서 URL에 포함된 파라미터 값을 가져오는 데 사용한다. 
- 이를 통해 URL 경로의 변수 부분을 컴포넌트 내부에서 활용할 수 있다.
- 예를 들어, URL이 /users/1인 경우 :id에 해당하는 값 1을 가져올 수 있다.

### 사용법
- react-router-dom 패키지에서 import하여 사용한다.
```js
import { useParams } from 'react-router-dom';
```
- 이 훅을 호출하면 URL 파라미터의 키-값 쌍을 가진 객체를 반환한다.

### UserProfile.js
- 유저의 프로필이 보여질 컴포넌트 작성하기
```js
import React from 'react';
import { useParams } from 'react-router-dom';

function UserProfile() {
  const { id } = useParams();

  // 실제로는 id를 사용하여 서버에서 데이터를 가져온다
  const user = {
    id,
    name: id === '1' ? '홍길동' : id === '2' ? '이순신' : '김유신',
    age: id === '1' ? 30 : id === '2' ? 45 : 38,
  };

  return (
    <div>
      <h2>{user.name}님의 프로필</h2>
      <p>사용자 ID: {user.id}</p>
      <p>나이: {user.age}</p>
    </div>
  );
}

export default UserProfile;
```

### Home.js 생성하기
- 실제는 서버에서 데이터를 가져오겠지만 임의로 만들어본다.
- 각 유저의 프로필을 보러갈 수 있는 메뉴를 생성하는 컴포넌트이다.
```js
import React from 'react';
import { Link } from 'react-router-dom';

function Home() {
  const users = [
    { id: 1, name: '홍길동' },
    { id: 2, name: '이순신' },
    { id: 3, name: '김유신' },
  ];

  return (
    <div>
      <h1>홈 페이지</h1>
      <ul>
        {users.map(user => (
          <li key={user.id}>
            <Link to={`/users/${user.id}`}>{user.name}의 프로필 보기</Link>
          </li>
        ))}
      </ul>
    </div>
  );
}

export default Home;
```

### App.js에 컴포넌트 추가하기
```js
import React from 'react';
import { Routes, Route } from 'react-router-dom';
import UserProfile from './UserProfile';
import Home from './Home';

function App() {
  return (
    <Routes>
      <Route path="/" element={<Home />} />
      <Route path="/users/:id" element={<UserProfile />} />
    </Routes>
  );
}

export default App;

```

## 중첩 라우트
- 우트 내에 또 다른 라우트를 정의하여 계층 구조를 형성하는 방식이다. 
- 페이지나 컴포넌트의 중첩된 구조를 반영하고, 하나의 라우트 아래에서 다른 라우트를 렌더링하는 경우에 사용된다.

### 라우트 중첩 실습
### App.js
```js
// App.js

import React from 'react';
import { Routes, Route } from 'react-router-dom';
import Dashboard from './Dashboard';

function App() {
  return (
    <Routes>
      <Route path="/dashboard/*" element={<Dashboard />} />
    </Routes>
  );
}

export default App;
```

### Dashboard.js
```js
import React from 'react';
import { Routes, Route, Link } from 'react-router-dom';
import Overview from './Overview';
import Settings from './Settings';

function Dashboard() {
  return (
    <div>
      <h1>대시보드</h1>
      <nav>
        <ul>
          <li><Link to="overview">개요</Link></li>
          <li><Link to="settings">설정</Link></li>
        </ul>
      </nav>
      <Routes>
        <Route path="overview" element={<Overview />} />
        <Route path="settings" element={<Settings />} />
      </Routes>
    </div>
  );
}

export default Dashboard;
```

### Overview.js
```js
import React from 'react';

function Overview() {
  return <h2>대시보드 개요 페이지</h2>;
}

export default Overview;
```

### Settings.js
```js
import React from 'react';

function Settings() {
  return <h2>대시보드 설정 페이지</h2>;
}

export default Settings;
```

## 리다이렉션
- 특정 조건에 따라 사용자를 다른 페이지로 자동 이동시키는 기능이다.
- 로그인 후 홈 페이지로 리다이렉트하거나, 사용자가 존재하지 않는 페이지에 접근할 때 404 페이지로 리다이렉트할 수 있다.

### App.js
```js
import React from 'react';
import { Routes, Route } from 'react-router-dom';
import Home from './Home';
import NotFound from './NotFound';

function App() {
  return (
    <Routes>
      <Route path="/" element={<Home />} />
      <Route path="*" element={<NotFound />} />
    </Routes>
  );
}

export default App;
```

### Home.js
```js
import React from 'react';

function Home() {
  return <h1>홈 페이지</h1>;
}

export default Home;
```

### NotFound.js
```js
import React from 'react';
import { Navigate } from 'react-router-dom';

function NotFound() {
  // 사용자를 홈 페이지로 리다이렉트
  return <Navigate to="/" />;
}

export default NotFound;
```
### \<Navigate /> 컴포넌트
- React Router에서 제공하는 컴포넌트로, 사용자를 특정 경로로 리다이렉트하기 위해 사용된다. 
- 이 컴포넌트는 페이지를 새로고침하지 않고도 현재 경로를 변경할 수 있다.
### Navigate 컴포넌트의 주요 기능
1. 즉시 리다이렉션
   - 사용자가 특정 경로에 접근할 때 즉시 다른 경로로 이동시킬 수 있다. 
   - 예를 들어, 인증되지 않은 사용자가 보호된 페이지에 접근하려 할 때 로그인 페이지로 리다이렉트할 수 있다.
2. 브라우저 히스토리 관리
   - 브라우저의 히스토리에 새 항목을 추가하거나(push), 현재 항목을 교체(replace)하여 브라우저의 뒤로 가기/앞으로 가기 버튼이 예상대로 작동하도록 관리할 수 있다.

### Navigate 컴포넌트의 주요 속성(props)
1. to
   - 사용자를 이동시키려는 경로를 지정한다.
   - ex) to="/login"은 사용자를 /login 경로로 이동시킨다.
2. replace
   - 리다이렉션할 때 현재 히스토리 항목을 새 항목으로 대체할지 여부를 결정한다.
   - replace={true}로 설정하면 브라우저의 히스토리 스택에서 현재 항목을 새로운 항목으로 교체한다. 
   - 즉, "뒤로 가기" 버튼을 눌렀을 때 리다이렉트된 경로로 다시 돌아가지 않는다.
   - 기본값은 false다. 즉, 히스토리 스택에 새로운 항목이 추가된다.

- NotFound 컴포넌트는 사용자가 잘못된 경로에 접근할 때 렌더링되며, 즉시 홈 페이지로 리다이렉트한다.

## 라우트 보호
- 특정 조건을 만족하는 사용자만 특정 라우트에 접근할 수 있도록 제한하는 기능이다.
- 주로 인증된 사용자만 접근 가능한 페이지를 만들 때 사용한다.
- 로그인하지 않은 사용자는 "대시보드" 페이지에 접근할 수 없게 하거나, 관리자 권한이 있는 사용자만 "관리자 페이지"에 접근할 수 있도록 할 수 있다.

### 라우트 보호 실습

### PrivateRoute.js
- 인증 여부를 확인한 후 접근을 허용하거나 로그인 페이지로 리다이렉트한다.
```js
import React from 'react';
import { Navigate } from 'react-router-dom';

function PrivateRoute({ element, isAuthenticated }) {
  return isAuthenticated ? element : <Navigate to="/login" />;
}

export default PrivateRoute;
```

### App.js
```js
import React from 'react';
import { Routes, Route } from 'react-router-dom';
import Dashboard from './Dashboard';
import Login from './Login';
import PrivateRoute from './PrivateRoute';

function App() {
  const isAuthenticated = false; // 실제로는 사용자 인증 상태를 확인해야 한다.

  return (
    <Routes>
      <Route path="/login" element={<Login />} />
      <Route
        path="/dashboard"
        element={<PrivateRoute element={<Dashboard />} isAuthenticated={isAuthenticated} />}
      />
    </Routes>
  );
}

export default App;
```
- PrivateRoute 컴포넌트는 isAuthenticated가 true일 때는 자식 컴포넌트를 렌더링하고, 그렇지 않으면 로그인 페이지로 리다이렉트한다.

### Login.js
```js
import React from 'react';

function Login() {
  return <h2>로그인 페이지</h2>;
}

export default Login;
```

### Dashboard.js
```js
import React from 'react';

function Dashboard() {
  return <h2>대시보드 페이지 (로그인 필요)</h2>;
}

export default Dashboard;
```


