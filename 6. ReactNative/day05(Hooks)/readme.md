## Hooks
- 이전에는 컴포넌트의 상태를 관리하거나 생명 주기에 따라 특정 작업을 수행하려면 클래스형 컴포넌트를 사용해야 했다.
- 하지만 Hooks를 이용할 수 있게 되면서 함수형 컴포넌트에서도 상태를 관리할 수 있게 되었고 컴포넌트의 생명 주기에 맞춰 특정 작업을 수행할 수 있게 되었다.

### 프로젝트 생성하기
```js
expo init react-native-hooks
```
- styled-components 설치하기
```js
npm install styled-components --force
```
- src 폴더를 생성하고 App 컴포넌트를 만든다.
```js
import React from 'react'
import styled from 'styled-components'

const Container = styled.View`
    flex:1;
    background-color: #fff;
    justify-content : center;
    align-items: center;
`

const App = () => {
    return <Container></Container>
}

export default App;
```
- 루트 경로에 있는 App.js 파일을 다음과 같이 변경한다.
```js
import App from "./src/App";
export default App;
```
- src아래 components폴더를 생성하고 실습에서 사용할 간단한 Button 컴포넌트를 만들어보자.
- Button.js 만들기
```js
import React from 'react';
import styled from 'styled-components';

const Container = styled.Pressable`
    background-color : #3498db;
    border-radius : 15px;
    padding : 15px 30px;
    margin : 10px 0px;
    justify-content: center;
`;

const Title = styled.Text`
    font-size : 24px;
    font-weight : 600;
    color : #ffffff;
`

const Button = ({title, onPress}) =>{
    return(
        <Container onPress={onPress}>
            <Title>{title}</Title>
        </Container>
    )
}

export default Button;
```

## useState
```js
const[state, setState] = useState(initialState);
```
- useState 함수를 호출하면 파라미터로 전달한 값을 초기값으로 갖는 상태 변수와 그 변수를 수정할 수 있는 세터함수 배열로 반환한다.
- useState 함수는 관리해야 하는 상태의 수만큼 여러 번 사용할 수 있다.
- 상태를 관리하는 반드시 세터 함수를 이용해 값을 변경해야 하고, 상태가 변경되면 컴포넌트가 변경된 내용을 반영하여 다시 렌더링 된다.

### 변수를 만들면 안되나?
1. 변수로 직접 만드는 경우
- 컴포넌트가 리렌더링되면 변수는 초기화된다.
- 즉, 렌더링이 다시 이루어질 때마다 변수에 새 값을 할당해도 이전 값이 사라지고 초기값으로 돌아가게 된다.
- 변수 값의 변화가 컴포넌트 리렌더링을 트리거하지 않아서, 변수 값이 바뀌어도 화면이 갱신되지 않는다.

2. useState로 만드는 경우
- useState로 만든 상태는 컴포넌트가 리렌더링되더라도 값이 유지된다.
- 상태가 업데이트되면 리액트가 이를 감지해 자동으로 컴포넌트를 다시 렌더링하여 최신 상태가 화면에 반영된다.
- 즉, 상태 값의 변화를 반영하려면 useState가 필요하다.

```js
import React, { useState } from 'react';

const Counter = () => {
  let count = 0; // 변수로 선언
  const [stateCount, setStateCount] = useState(0); // useState로 선언

  const increaseCount = () => {
    count += 1; // 변수로 값 증가
    setStateCount(stateCount + 1); // 상태로 값 증가
  };

  return (
    <div>
      <p>변수 count: {count}</p>
      <p>useState로 만든 count: {stateCount}</p>
      <button onClick={increaseCount}>증가</button>
    </div>
  );
};

export default Counter;
```
- 리액트 컴포넌트는 props를 통해 다른 컴포넌트와 데이터를 주고받는다.
- useState로 관리하는 값은 props로 하위 컴포넌트에 전달할 수 있어 부모와 자식 컴포넌트 간에 상태를 공유하거나 데이터를 전달할 수 있게 된다. 
- 변수를 통해 만든 값은 상태가 아니기 때문에 다른 컴포넌트에 props로 전달해도 리렌더링에 따라 값이 초기화될 수 있어 예기치 않은 동작을 초래할 수 있다.

### 상태를 직접 변경하면 안되는 이유
- 리액트는 상태가 변경될 때 컴포넌트를 다시 렌더링하는데, 리액트가 상태 변화를 감지하기 위해서는 상태가 리액트의 방식대로 업데이트돼야한다.

### 리액트가 상태를 추적하는 원리
- 리액트가 상태를 추적하는 원리는 **불변성(immutability)과 참조 비교(reference comparison)**를 활용하는 것에 기반을 두고 있다.

### 1. 불변성(Immutability)을 통한 상태 관리
- 리액트는 상태가 불변하다고 가정하고, 상태 변경 시 항상 새로운 상태 객체를 생성한다.
- 이 불변성 덕분에 리액트는 참조만으로 상태가 변했는지 쉽게 감지할 수 있다.
- 상태를 직접 변경하지 않고 새로운 객체를 만들어야 리액트가 이를 "변경된 상태"로 인식한다.
- 만약 기존 상태를 직접 변경하면 기존 참조와 새로운 참조가 동일해 리액트가 이를 변경으로 감지하지 못한다.

#### 1. 불변성을 유지하지 않는 경우
- 불변성을 지키지 않고 객체를 수정할 수는 있다.
- 리액트에서 이런 식으로 상태를 변경하면 문제가 발생할 수 있다.
```js
const person = { name: 'Alice', age: 25 };

// 나이를 변경하는 함수
const updateAgeDirectly = (obj, newAge) => {
  obj.age = newAge; // 직접 변경 (불변성을 위반)
  return obj;
};

const updatedPerson = updateAgeDirectly(person, 30);

console.log(person); // { name: 'Alice', age: 30 }
console.log(updatedPerson === person); // true (같은 객체를 참조)
```
- 위 코드에서 person객체를 직접 수정해 age를 변경했다.
- 이 경우 person과 updatePerson이 같은 객체로 남아 있게 되고, 리액트는 변경된 객체가 새 객체가 아니라고 판단해 상태가 바뀐것을 인식하지 못할 수 있다.

#### 2. 불변성을 유지하는 경우
```js
const person = { name: 'Alice', age: 25 };

// 나이를 변경하는 함수 (불변성 유지)
const updateAgeImmutably = (obj, newAge) => {
  return { ...obj, age: newAge }; // 새로운 객체 생성
};

const updatedPerson = updateAgeImmutably(person, 30);

console.log(person); // { name: 'Alice', age: 25 } (원본이 변경되지 않음)
console.log(updatedPerson); // { name: 'Alice', age: 30 } (새 객체)
console.log(updatedPerson === person); // false (다른 객체를 참조)
```
- 여기서는 불변성을 유지하기 위해 스프레드연산자를 사용하여 기존 객체의 값을 복사하고, age 속성만 새 값으로 변경한 새로운 객체를 반환했다.
- 이렇게 하면 updatePerson과 person이 서로 다른 객체이므로, 리액트는 상태가 변경되었다고 인식해 컴포넌트를 다시 렌더링하게 된다.



### 2. 참조 비교(reference comparison)를 이용한 변경 감지
- 리액트는 **얕은 비교(shallow comparison)**를 사용해 이전 상태와 새로운 상태를 비교한다.
- 얕은 비교는 객체의 참조를 비교하는 방식으로, 성능이 뛰어나고 불필요한 렌더링을 줄이는 데 효과적이다.

```js
// 두 개의 객체가 동일한 키와 값을 가진 경우
const object1 = { name: 'Alice' };
const object2 = { name: 'Alice' };

// 얕은 비교 - 객체의 참조만 비교
console.log(object1 === object2); // false

// 이유: object1과 object2는 내용이 같지만 다른 메모리 위치에 저장된 별도의 객체임

// 두 객체가 동일한 참조를 가리키도록 설정한 경우
const object3 = object1;
console.log(object1 === object3); // true

// 이유: object1과 object3은 같은 객체를 참조하고 있기 때문에 true가 됨

// 깊은 비교 예시 - 내용이 같은지 확인 (일반적인 깊은 비교 구현 예제)
const deepEqual = (obj1, obj2) => {
  return JSON.stringify(obj1) === JSON.stringify(obj2);
};

console.log(deepEqual(object1, object2)); // true

// 이유: object1과 object2의 내부 구조와 값이 같기 때문에 깊은 비교에서는 true가 됨
```