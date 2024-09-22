# Context API
## 개념
- React에서 컴포넌트 간의 전역 상태를 관리하고 데이터를 공유하기 위한 내장 기능이다. 
- 컴포넌트 트리의 최상위에서 데이터를 제공(Provider)하고, 하위 컴포넌트에서 해당 데이터를 소비(Consumer)할 수 있다.
- 컴포넌트 트리의 여러 단계에 걸쳐 데이터를 전달해야 할 때, 즉 Props Drilling(프롭스 드릴링) 문제를 해결하는 데 유용하다.

## Props Drilling(프롭스 드릴링)
- 상위 컴포넌트에서 하위 컴포넌트로 데이터를 전달할 때, 여러 단계의 컴포넌트를 거쳐야 하는 문제를 말한다. 
- 이는 코드의 가독성을 떨어뜨리고, 유지보수를 어렵게 만들 수 있다.

### 예제
- App.js
```js
// App.js
import React from 'react';
import Parent from './Parent';

function App() {
  const user = { name: 'John Doe', age: 30 };

  return <Parent user={user} />;
}

export default App;
```
- Parent.js
```js
// Parent.js
import React from 'react';
import Child from './Child';

function Parent({ user }) {
  return <Child user={user} />;
}

export default Parent;
```
- Child.js
```js
import React from 'react';
import GrandChild from './GrandChild';

function Child({ user }) {
  return <GrandChild user={user} />;
}

export default Child;
```
- GrandChild.js
```js
import React from 'react';

function GrandChild({ user }) {
  return (
    <div>
      <h1>{user.name}</h1>
      <p>Age: {user.age}</p>
    </div>
  );
}

export default GrandChild;
```
- user 데이터를 App 컴포넌트에서 GrandChild 컴포넌트로 전달하기 위해 Parent와 Child 컴포넌트를 거쳐야 한다.
- 이처럼 데이터 전달을 위해 여러 단계의 컴포넌트를 거쳐야 하는 상황을 Props Drilling이라고 한다.

## 왜 Context API를 사용해야 하는가
### 전역 상태 관리
- 애플리케이션에서 전역으로 사용되는 상태를 관리할 수 있다. 
- 예를 들어, 사용자 인증 정보, 테마 설정, 언어 설정 등을 전역 상태로 관리할 수 있다.
### Props Drilling 문제 해결
- 상위 컴포넌트에서 하위 컴포넌트로 데이터를 전달할 때, 여러 중간 컴포넌트를 거쳐야 하는 문제를 해결할 수 있다.

## Context API로 전역 상태 관리하기
### ConText API 사용 방법
1. Context 생성하기
    - React.createContext를 사용하여 Context를 생성한다.
```js
import { createContext } from 'react';

const MyContext = createContext();
```
2. Provider 설정하기
    - Context의 Provider를 사용하여 하위 컴포넌트에 데이터를 제공한다.
```js
import React, { useState } from 'react';

const MyProvider = ({ children }) => {
    const [value, setValue] = useState('Hello, Context!');

    return (
        <MyContext.Provider value={{ value, setValue }}>
            {children}
        </MyContext.Provider>
    );
};

```
3. Consumer 사용하기
    - Context의 Consumer 또는 useContext 훅을 사용하여 하위 컴포넌트에서 데이터를 소비한다.
```js
import { useContext } from 'react';

const MyComponent = () => {
    const { value, setValue } = useContext(MyContext);

    return (
        <div>
            <p>{value}</p>
            <button onClick={() => setValue('Updated Context!')}>Update</button>
        </div>
    );
};

```

### 예제
- Context API를 사용하여 전역 상태를 관리하고, Props Drilling 문제를 해결해보자.


### 1. Context 생성
- UserContext.js
```js
//createContext import하기
import React, { createContext, useState } from 'react';

//새로운 Context를 생성한다.
export const UserContext = createContext();

// Context Provider 컴포넌트
//사용자 정보를 관리하고 하위 컴포넌트에 제공하는 Provider 컴포넌트이다.
export const UserProvider = ({ children }) => {
  //사용자 정보(이름과 나이)를 관리한다.
  const [user, setUser] = useState({ name: 'John Doe', age: 30 });

  return (
    //UserContext.Provider : Context에서 제공하는 특수한 컴포넌트
    <UserContext.Provider value={{ user, setUser }}>
      {children}
    </UserContext.Provider>
  );
};

```
#### createContext()
- 데이터를 공유할 Context를 생성한다.
- Context는 React 컴포넌트를 하위로 전달할 수 있는 수단이다.
#### UserContext
- createContext()로 생성된 Context 객체를 저장하는 변수다.
- 이 객체는 데이터를 제공(Provider)하거나, 데이터를 소비(Consumer)할 수 있는 기능을 제공한다.
  - UserContext.Provider: 데이터를 제공하는 컴포넌트로 사용된다.
  - UserContext.Consumer 또는 useContext(UserContext): 데이터를 소비하는 컴포넌트에서 사용한다.

#### UserProvider
- Context의 Provider 역할을 한다. 
- 즉, 이 컴포넌트를 사용하면 하위 컴포넌트에서 UserContext의 데이터를 사용할 수 있다.

#### \<UserContext.Provider />
- **Provider**는 Context에서 제공하는 특수한 컴포넌트로, 하위 컴포넌트들에게 전역 상태를 전달하는 역할을 한다.

#### value
- Provider가 하위 컴포넌트들에게 제공할 데이터를 정의한다.
- 여기서는 { user, setUser }라는 객체를 제공하여, 사용자 정보를 가져오거나 변경할 수 있게 한다.

#### {children}
- UserProvider 컴포넌트가 감싸고 있는 모든 하위 컴포넌트들을 의미한다.
- 이 children들은 UserContext.Provider로부터 전달된 데이터를 사용할 수 있다.

### 2. Provider 설정
- App.js
```js
import React from 'react';
import { UserProvider } from './UserContext';
import Parent from './Parent';

function App() {
  return (
    <UserProvider>
      <Parent />
    </UserProvider>
  );
}

export default App;
```
- Parent.js
```js
// Parent.js
import React from 'react';
import Child from './Child';

function Parent() {
  return <Child />;
}

export default Parent;
```
- Child.js
```js
import React from 'react';
import GrandChild from './GrandChild';

function Child() {
  return <GrandChild />;
}

export default Child;
```
- GrandChild.js
```js
// ChildComponent.js
import React, { useContext } from 'react';
import { UserContext } from './UserContext';

function ChildComponent() {
  //UserContext로부터 데이터를 가져온다. 
  //user 상태와 setUser 함수를 가져와서 컴포넌트 내에서 사용할 수 있다.
  const { user, setUser } = useContext(UserContext);

  //user의 이름과 나이를 화면에 표시하고, 버튼을 클릭하면 setUser를 호출하여 사용자 정보를 업데이트할 수 있다.
  return (
    <div>
      <h1>{user.name}</h1>
      <p>Age: {user.age}</p>
      <button onClick={() => setUser({ name: 'Jane Doe', age: 28 })}>
        Change User
      </button>
    </div>
  );
}

export default ChildComponent;
```

# 비동기 데이터 처리
- 작업이 시작된 후 즉시 결과를 기다리지 않고, 다른 작업을 계속할 수 있는 프로그래밍 방식이다.
- 주로 네트워크 요청(API 호출), 파일 읽기, 타이머 등 시간이 오래 걸릴 수 있는 작업을 처리할 때 사용된다.
- 이 방식은 작업이 완료될 때까지 애플리케이션이 멈추지 않고, 다른 코드나 작업을 계속해서 실행할 수 있게 해준다.

## 동기처리(Synchronous)
- 한 번에 하나의 작업만 처리되며, 작업이 완료될 때까지 다음 작업을 진행할 수 없다.
```js
console.log('첫 번째 작업 시작');
const result = performHeavyTask(); // 무거운 작업 실행 (예: API 호출)
console.log('첫 번째 작업 완료:', result);
console.log('다음 작업 진행');
```
- 여기서 **performHeavyTask()**가 완료될 때까지 프로그램은 멈춰서 기다린다.
- 그다음 작업은 무거운 작업이 완료된 후에야 실행된다.

## 비동기처리(Asynchronous)
- 작업이 완료되기를 기다리지 않고, 다른 작업을 동시에 진행할 수 있다.
- 결과가 준비되면, 그 시점에 맞춰 특정 작업을 처리할 수 있도록 한다.
- 비동기 처리는 콜백 함수, Promise, async/await 같은 구조로 처리된다.
```js
console.log('첫 번째 작업 시작');
setTimeout(() => {
  console.log('첫 번째 작업 완료');
}, 2000); // 2초 후에 실행
console.log('다음 작업 진행');
```
- 위 코드에서 **setTimeout**은 비동기적으로 실행되며, 2초가 지나야 실행된다.
- 그러나 **'다음 작업 진행'**은 즉시 실행된다.
- 즉, 프로그램은 멈추지 않고, 타이머가 끝나는 동안 다른 작업을 처리한다.

## 비동기 처리가 중요한 이유
- 주로 시간이 오래 걸리는 작업(예: 네트워크 요청, 파일 읽기/쓰기, 타이머 등)을 처리할 때 유용하다.
- 만약 이런 작업을 동기 방식으로 처리한다면, 작업이 완료될 때까지 애플리케이션이 멈추게 되어 사용자 경험이 매우 나빠질 수 있다.
- 비동기 처리를 사용하면, 작업이 완료될 때까지 기다리는 동안에도 UI가 반응하고 다른 작업이 실행될 수 있다.

## 비동기 처리의 주요 패턴
### 1. 콜백함수(Callback Function)
- 콜백 함수는 특정 작업이 완료된 후에 호출되는 함수이다.
- 예를 들어, API 요청이 완료되었을 때 실행될 함수를 전달하여, 해당 작업이 끝난 후 처리하게 할 수 있다.
```js
function fetchData(callback) {
  setTimeout(() => {
    const data = '서버에서 받은 데이터';
    callback(data); // 작업이 끝난 후 콜백 실행
  }, 2000); // 2초 뒤에 실행
}

console.log('API 요청 시작');
fetchData((result) => {
  console.log('API 응답:', result);
});
console.log('다음 작업 진행');

```
- fetchData 함수는 2초 후에 데이터를 반환하고, 데이터를 받은 후 콜백 함수가 실행된다.
- 그러나 2초를 기다리는 동안 다음 작업은 즉시 실행된다.

### 2. Promise
- Promise는 비동기 작업이 완료되었을 때 성공 또는 실패 결과를 반환하는 객체이다.
- then과 catch를 통해 작업의 성공 또는 실패를 처리할 수 있다.

```js
const fetchData = () => {
  //Promise객체를 반환
  return new Promise((resolve, reject) => {

    //2초 후에 비동기적으로 실행될 작업을 지연시킨다.
    setTimeout(() => {
      const success = true; // 성공 여부
      if (success) {
        //success가 true일 때 
        resolve('데이터 받아옴');
      } else {
        reject('에러 발생');
      }
    }, 2000); // 2초 후 실행
  });
};

console.log('API 요청 시작');
fetchData()  //결과에 따라 then과 catch 블록이 실행됩니다.
  .then(data => { //then() : Promise가 성공(즉, resolve 호출)하면 실행되는 콜백 함수입니다. 콘솔에 응답 데이터('데이터 받아옴')를 출력합니다.
    console.log('API 응답:', data);
  })
  .catch(error => {// Promise가 실패(즉, reject 호출)하면 실행되는 콜백 함수입니다. 여기서는 에러 메시지를 콘솔에 출력합니다.
    console.error('에러:', error);
  });
console.log('다음 작업 진행');
```

### 3. async/await
- Promise를 기반으로 한 비동기 처리 방식으로, 동기 처리처럼 보이지만 비동기 작업을 수행할 수 있게 해준다.
- await 키워드는 Promise가 해결될 때까지 기다린다.

#### async 함수
- async 키워드는 함수 앞에 붙여서 그 함수가 비동기 함수임을 나타낸다.
- 비동기 함수는 항상 Promise를 반환한다.
- 함수 내부에서 return 값은 자동으로 **resolve**로 처리됩니다.
```js
async function fetchData() {
  return '데이터';
}

// fetchData()는 Promise를 반환함
fetchData().then(data => console.log(data)); // "데이터"
```

#### await
- await 키워드는 비동기 함수에서만 사용할 수 있으며, Promise가 처리될 때까지 함수 실행을 일시적으로 중지한다.
- Promise가 **resolve**되면, 그 값을 반환받아 동기적으로 코드가 실행되는 것처럼 이어진다.

```js
async function fetchData() {
  const response = await fetch('https://jsonplaceholder.typicode.com/posts'); // 데이터를 기다림
  const data = await response.json(); // JSON으로 변환 완료될 때까지 기다림
  return data;
}

fetchData().then(posts => console.log(posts)); // Promise가 resolve되면 posts 출력

```

```js
const fetchData = () => {
  return new Promise((resolve) => {
    setTimeout(() => {
      resolve('데이터 받아옴');
    }, 2000); // 2초 후 실행
  });
};

async function getData() {
  console.log('API 요청 시작');
  const data = await fetchData(); // 2초 후에 데이터를 받음
  console.log('API 응답:', data);
  console.log('다음 작업 진행');
}

getData();

```

- async 함수 내부에서 **await**를 사용하여 비동기 작업이 완료될 때까지 기다립니다.
**await**는 해당 비동기 작업이 완료될 때까지 코드 실행을 일시 중지하고, 완료되면 다시 실행합니다.


## 비동기 처리의 장점
### UI 반응성 유지
- 무거운 작업을 수행할 때도 애플리케이션이 멈추지 않고 계속해서 동작한다.
### 성능 최적화
- 네트워크 요청, 파일 읽기 등 시간이 오래 걸리는 작업이 완료될 때까지 기다리지 않고, 다른 작업을 동시에 수행할 수 있다.
### 사용자 경험 향상
- 데이터를 처리하거나 로딩하는 동안도 애플리케이션이 반응하며, 사용자에게 즉각적인 피드백을 제공할 수 있다.

## API와 통신하는 방법
- React에서 API와 통신하는 가장 일반적인 방법은 fetch API와 Axios 라이브러리를 사용하는 것이다.

## Fetch API
- 브라우저에서 제공하는 비동기 네트워크 요청을 수행하는 기본 API이다.
- **Promise**를 반환하며, 네트워크 요청의 성공 여부에 따라 성공 또는 실패 상태로 처리된다.

```js
// Fetch API 사용 예시
fetch('https://jsonplaceholder.typicode.com/posts')
  .then(response => response.json()) // JSON 형식으로 응답을 변환
  .then(data => console.log(data))   // 데이터 출력
  .catch(error => console.error('Error:', error)); // 에러 처리
```

## Axios
- Promise 기반 HTTP 클라이언트로, Fetch API보다 기능이 더 풍부하고 편리하다.
- 자동으로 JSON 변환을 수행하고, 에러 처리가 더 간편하게 구현된다.

### Axios 설치 및 사용 예시
```js
npm install axios
```
```js
// Axios 사용 예시
import axios from 'axios';

axios.get('https://jsonplaceholder.typicode.com/posts')
  .then(response => console.log(response.data))  // 데이터 출력
  .catch(error => console.error('Error:', error)); // 에러 처리
```

## 리액트에서 데이터 비동기 처리하기
- useEffect 훅을 사용하여 컴포넌트가 렌더링될 때 비동기 API 요청을 수행하고, 그 결과를 화면에 표시해보자.

### Fetch API로 데이터 가져오기
- JSONPlaceholder의 게시글 데이터를 가져오는 예제입니다. 
- 데이터가 로딩 중일 때는 "로딩 중..."이라는 메시지를 보여주고, 데이터가 도착하면 목록으로 표시한다.

### JSONPlaceholder
- 테스트 및 프로토타입을 위한 샘플 데이터를 제공하는 무료 온라인 REST API서비스이다.
- 게시글, 댓글, 앨법, 사진 등 실제 백엔드를 설정하지 않고도 애플리케이션을 테스트하는 데 사용할 수 있는 Fake 데이터를 제공한다.
- 실제 데이터를 생성하거나 라이브 API에 의존할 필요 없이 응용 프로그램의 기능을 테스트하고자 하는 사람에게 매우 유용한 서비스이다.

### 공식문서
https://jsonplaceholder.typicode.com/guide/


```js
fetch('https://jsonplaceholder.typicode.com/posts/1')
  .then((response) => response.json())
  .then((json) => console.log(json));

결과
{
  id: 1,
  title: '...',
  body: '...',
  userId: 1
}
```

```js
fetch('https://jsonplaceholder.typicode.com/posts')
  .then((response) => response.json())
  .then((json) => console.log(json));

결과
[
  { id: 1, title: '...' /* ... */ },
  { id: 2, title: '...' /* ... */ },
  { id: 3, title: '...' /* ... */ },
  /* ... */
  { id: 100, title: '...' /* ... */ },
];

```

### FetchExam.js 만들기
```js
import React, { useState, useEffect } from 'react';

function FetchExam() {
  const [posts, setPosts] = useState([]);        // 데이터를 저장할 상태
  const [loading, setLoading] = useState(true);  // 로딩 상태 관리
  const [error, setError] = useState(null);      // 에러 상태 관리

  useEffect(() => {
    // 비동기적으로 데이터 호출
    const fetchData = async () => {
      try {
        const response = await fetch('https://jsonplaceholder.typicode.com/posts');
        if (!response.ok) {
          throw new Error('데이터를 불러오는데 실패했습니다.');
        }
        const data = await response.json();
        setPosts(data);  // 상태에 데이터를 저장
      } catch (err) {
        setError(err.message);  // 에러 처리
      } finally {
        setLoading(false);  // 로딩 상태를 완료로 설정
      }
    };

    fetchData();  // 함수 호출
  }, []);  // 컴포넌트가 처음 렌더링될 때 한 번만 실행

  // 로딩 중일 때 보여줄 내용
  if (loading) {
    return <p>로딩 중...</p>;
  }

  // 에러 발생 시 보여줄 내용
  if (error) {
    return <p>에러 발생: {error}</p>;
  }

  // 데이터를 성공적으로 불러왔을 때 보여줄 내용
  return (
    <div>
      <h1>게시글 목록</h1>
      <ul>
      {/*posts.slice(0, 10)는 posts 배열에서 인덱스 0부터 9까지의 첫 10개의 게시글을 잘라내서 새로운 배열을 반환합니다.*/}
        {posts.slice(0, 10).map((post) => (  // 첫 10개의 게시글만 출력
          <li key={post.id}>{post.title}</li>
        ))}
      </ul>
    </div>
  );
}

export default FetchExam;
```
### useState로 상태 관리
- posts: 불러온 게시글 데이터를 저장한다.
- loading: 데이터를 불러오는 중일 때 로딩 상태를 관리한다.
- error: 데이터를 불러오지 못했을 때 발생하는 에러를 관리한다.

### useEffect로 API 요청
- **useEffect**는 컴포넌트가 렌더링될 때 실행된다.
- 이 훅에서 비동기 함수를 호출하여 데이터를 가져온다.
**fetch**로 데이터를 불러와서 성공 시 posts 상태에 데이터를 저장하고, 에러가 발생하면 error 상태에 에러 메시지를 저장한다.

### 로딩 상태와 에러 처리
- **loading이 true**일 때는 "로딩 중..."이라는 메시지를 표시한다.
- error가 발생하면 에러 메시지를 표시합니다.
- 데이터가 정상적으로 불러와지면, 게시글 목록을 화면에 출력합니다.

