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
2. Provider 설정하기
    - Context의 Provider를 사용하여 하위 컴포넌트에 데이터를 제공한다.
3. Consumer 사용하기
    - Context의 Consumer 또는 useContext 훅을 사용하여 하위 컴포넌트에서 데이터를 소비한다.

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