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


### useState 사용하기
- components 폴더 안에 Counter.js 파일을 생성하고 useState를 사용해서 다음과 같이 작성하자
```js
import React, {useState} from "react";
import styled from "styled-components";
import Button from "./Button";

const StyledText = styled.Text`
    font-size : 24px;
    margin: 10px;
`

const Counter = () => {
    const[count, setCount] = useState(0);
    return(
        <>
            <StyledText>
                Count: {count}
            </StyledText>
            <Button
                title="+"
                onPress={() => {
                    setCount(count +1);
                }}
            />
            <Button
                title="-"
                onPress={() => {
                    setCount(count -1);
                }}
            />
        </>
    )
}
export default Counter;
```

### ※ 화살표함수로 호출하는 이유
#### 1. 즉시 호출 방지
- onPress={setCount(count - 1)}와 같이 함수 호출 문법으로 작성하면 컴포넌트가 렌더링될 때 setCount(count - 1)이 즉시 실행되어, onPress 이벤트가 발생할 때가 아닌 렌더링 시점에 setCount가 호출되게된다.

#### 2. this 바인딩 문제 해결
- 리액트 클래스 컴포넌트에서는 일반적으로 이벤트 핸들러에서 this가 현재 컴포넌트를 참조하도록 bind(this)를 사용해야 했다.
```js
class MyComponent extends React.Component {
  constructor() {
    super();
    this.state = { count: 0 };
  }

  handleClick = () => {
    this.setState({ count: this.state.count + 1 }); // this가 컴포넌트를 가리킴
  }

  render() {
    return <button onClick={this.handleClick}>Click me</button>;
  }
}
```
- 화살표 함수는 this를 호출한 컨텍스트에 바인딩하지 않고, 상위 스코프의 this를 그대로 사용하게 돼서 this 바인딩 문제를 피할 수 있다.
```js
function Person() {
  this.name = 'Alice';
  
  // setTimeout의 콜백 함수에서 일반 함수를 사용
  setTimeout(function() {
    console.log(this.name); // undefined가 출력됨
  }, 1000);
}

const person = new Person();
```
- 화살표함수 사용시
```js
function Person() {
  this.name = 'Alice';

  // setTimeout의 콜백 함수에서 화살표 함수 사용
  setTimeout(() => {
    console.log(this.name); // 'Alice'가 출력됨
  }, 1000);
}

const person = new Person();
```

#### 요약
- 화살표 함수는 함수형 컴포넌트에서 이벤트 발생 시점에만 함수를 실행하도록 돕는 깔끔한 패턴이다.

### Counter.js 사용하기
- App 컴포넌트에서 Counter컴포넌트 사용하기
```js
import React from 'react'
import styled from 'styled-components'
import Counter from './components/Counter'

const Container = styled.View`
    flex:1;
    background-color: #fff;
    justify-content : center;
    align-items: center;
`

const App = () => {
    return (
    <Container>
        <Counter />
    </Container>
    )
}

export default App;
```


### 세터 함수
- useState에서 반환된 세터 함수를 사용하는 방법은 두가지이다.
- 첫번재는 우리가 지금까지 사용했던 방법으로 세터 함수에 변경될 상태의 값을 전달하는 방법이다.
- 두번째는 세터 함수의 파라미터에 함수를 전달하는 방법이다.
```js
setState(prevState => {});
```
- 전달된 함수에는 변경되기 전의 상태 값이 파라미터로 전달되며 이 값을 어떻게 수정할지 정의하면 된다.
- 세터 함수는 비동기로 동작하기 때문에 상태 변경이 여러번 일어날 경우 상태가 변경되기 전에 또 다시 상태에 대한 업데이트가 실행되는 상황이 발생할 수 있다.

```js
<Button
    title="+"
    onPress={() => {
        setCount(count +1);
        setCount(count +1);
        console.log(`count: ${count}`)
    }}
/>
```
- Counter 컴포넌트에서 증가 버튼을 클릭했을 때, 세터 함수를 두 번 호출하도록 수정을 했다.
- 증가 버튼을 클릭해도 1씩 증가하는 모습을 볼 수 있다.
- 세터 함수가 비동기로 동작하기 때문에 세터 함수를 호출해도 바로 상태가 변경되지 않는다는 점에서 발생하는 문제다.
- 이렇게 상태에 대해 여러 업데이트가 함께 발생할 경우, 세터 함수에 함수를 인자로 전달하여 이전 상태값을 이용하면 문제를 해결할 수 있다.
```js
<Button
    title="+"
    onPress={() => {
        setCount(prevCount => prevCount +1);
        setCount(prevCount => prevCount +1);
        console.log(`count: ${count}`)
    }}
/>
```
- 이전 상태의 값에 의존하여 상태를 변경할 경우, 세터 함수에 함수를 인자로 전달하여 이전 값을 이용하도록 작성해야 문제가 생기지 않는다.

## useEffect
- 컴포넌트가 렌더링 될 때마다 원하는 작업이 실행되도록 설정할 수 있는 기능이다.
```js
useEffect(() => {}, []);
```
- 첫번째 파라미터로 전달된 함수는 조건을 만족할 때마다 호출된다.
- 두번째 파라미터로 전달되는 배열을 이용해 함수가 호출되는 조건을 설정할 수 있다.

### useEffect 사용하기
- 두번째 파라미터에 어떤 값도 전달하지 않으면 useEffect의 첫 번째 파라미터로 전달된 함수는 컴포넌트가 렌더링 될 때마다 호출된다.
- components에 Form.js파일을 생성하고 이메일과 이름을 입력받는 컴포넌트를 작성해보자.
```js
import React, {useState, useEffect} from "react";
import styled from "styled-components";

const StyledTextInput = styled.TextInput.attrs({
    autoCapitalize: 'none',
    autoCorrect : false
})`
    border : 1px solid #757575;
    padding : 10px;
    margin : 10px 0;
    width : 200px;
    font-size : 20px;
`;

const StyledText = styled.Text`
    font-size : 24px;
    margin : 10px;
`

const Form = () => {
    const[name,setName] = useState('');
    const[email,setEmail] = useState('');

    useEffect(() => {
        console.log(`name: ${name}, email: ${email}\n`);
    })

    return(
        <>
            <StyledText> Name : {name} </StyledText>
            <StyledText> Email : {email} </StyledText>
            <StyledTextInput
                value={name}
                onChangeText={text => setName(text)}
                placeholder="name"
            />
            <StyledTextInput
                value={email}
                onChangeText={text => setEmail(text)}
                placeholder="email"
            />
        </>
    )
}

export default Form;
```
- TextInput 컴포넌트를 이용해서 이메일과 이름을 입력받는 컴포넌트를 만들고, useEffect를 사용해서 컴포넌트가 다시 렌더링될 때마다 name과 email을 출력한다.
- App컴포넌트에서 작성한 Form 컴포넌트를 사용해보자.

```js
import Form from './components/Form'

...

const App = () => {
    return (
    <Container>
        <Form />
    </Container>
    )
}
```

### 특정 조건에서 실행하기
- useEffect에 설정한 함수를 특정 상태가 변경될 때만 호출하고 싶은 경우, useEffect의 두 번째 파라미터에 해당 상태를 관리하는 변수를 배열로 전달하면 된다.
- 상태의 값을 변경하는 세터 함수가 비동기로 동작하므로 상태의 값이 변경되면 실행할 함수를 useEffect를 이용해서 정의해야 한다.
- email이 변경될 때만 useEffect가 동작하도록 Form 컴포넌트를 수정하자.

```js
const Form = () => {
    ...
    useEffect(() => {
        console.log(`name : ${name}, email : ${email}\n`);
    },[email])
}
```
- name이 변경될 때는 실행되지 않지만 email이 변경될 대는 함수가 잘 실행되는 것을 확인할 수 있다.

### 마운트 될 때 실행하기
- 컴포넌트가 마운트 될 때 useEffect에 전달된 함수를 실행시켜보자.
- useEffect의 두 번째 파라미터에 빈 배열을 전달하면 컴포넌트가 처음 렌더링 될 때만 함수가 호출되도록 작성할 수 있습니다.

```js
  useEffect(() => {
    console.log('\n===== Form Component Mount =====\n');
  }, []);
```
- 컴포넌트가 처음 렌더링 될 때 함수가 호출되고, 이후에는 상태가 변해 컴포넌트가 다시 렌더링 되어도 함수가 실행되지 않는다는 것을 확인할 수 있다.

### 언마운트 될 때 실행하기
- 컴포넌트가 언마운트될 때 useEffect의 함수가 실행되게 해보자
```js
useEffect(() => {
console.log('\n===== Form Component Mount =====\n');
refName.current.focus();
return () => console.log('\n===== Form Component Unmount =====\n');
}, []);
```
### 클린업 함수
- 클린업(clean-up) 함수는 컴포넌트가 언마운트되거나, useEffect가 다시 실행되기 전에 실행되는 함수다.
- 주로 리소스를 정리하거나, 이벤트 리스너를 제거하거나, 타이머를 정리하는 등 필요한 뒷처리를 수행하기 위해 사용한다.

#### 클린업 함수 사용 방법
- useEffect는 첫 번째 인자로 함수를 받는데, 이 함수는 다시 함수를 반환할 수 있다. 
- 반환된 이 함수가 바로 클린업 함수로, 컴포넌트가 언마운트될 때 실행되거나, useEffect의 의존성이 변경될 때 실행된다.

- Form 컴포넌트가 언마운트 되는 상황을 테스트하기 위해 App 컴포넌트를 다음과 같이 수정하자
```js
import React, { useState } from 'react';
import styled from 'styled-components/native';
import Counter from './components/Counter';
import Form from './components/Form';
import Button from './components/Button';


const App = () => {
    const [isVisible, setIsVisible] = useState(true);
  
    return (
      <Container>
        <Button
          title={isVisible ? 'Hide' : 'Show'}
          onPress={() => setIsVisible(prev => !prev)}
        />
        {isVisible && <Form />}
      </Container>
    );
  };
```
- useState를 이용해 Form 컴포넌트의 렌더링 상태를 관리할 isVisible을 생성하고, 버튼을 클릭할 때마다 상태를 변경해서 Form 컴포넌트의 렌더링 상태를 관리하도록 수정했다.


## useRef
- 특정 DOM 요소나 값의 변화를 추적하거나 유지할 때 사용되는 객체를 반환해 주는 역할을 한다.
- DOM 요소에 접근하기 위해 사용하거나, 리렌더링 없이 상태를 유지할 때 사용하는 경우다.

### 주요 특징
- `초기 값 유지`: useRef의 초기 값은 컴포넌트가 마운트될 때 한 번만 설정되며 이후에는 유지된다.
- `리렌더링 없이 값 유지`: useRef의 값이 바뀌어도 컴포넌트는 리렌더링되지 않으므로, 값의 변경이 UI에 즉각적인 영향을 주지 않아야 할 때 유용하다.
- `DOM 접근`: useRef는 컴포넌트의 특정 DOM 요소에 접근할 때 사용할 수 있다. 
  - 주로 input, button 등 특정 DOM 요소에 직접 접근해 포커스를 설정하거나, 요소의 값을 직접 조작할 때 사용된다.

useRef를 이용해 지금까지 작성한 Form 컴포넌트를 수정해보자.

```js
import React, { useState, useEffect, useRef } from 'react';
import styled from 'styled-components/native';

const StyledTextInput = styled.TextInput.attrs({
  autoCapitalize: 'none',
  autoCorrect: false,
})`
  border: 1px solid #757575;
  padding: 10px;
  margin: 10px 0;
  width: 200px;
  font-size: 20px;
`;
const StyledText = styled.Text`
  font-size: 24px;
  margin: 10px;
`;

const Form = () => {
    ...

  const refName = useRef(null);
  const refEmail = useRef(null);

  useEffect(() => {
    console.log('\n===== Form Component Mount =====\n');
    refName.current.focus();
    return () => console.log('\n===== Form Component Unmount =====\n');
  }, []);

  return (
    <>
      <StyledText>Name: {name}</StyledText>
      <StyledText>Email: {email}</StyledText>
      <StyledTextInput
        value={name}
        onChangeText={text => setName(text)}
        placeholder="name"
        ref={refName}
        returnKeyType="next"
        onSubmitEditing={() => refEmail.current.focus()}
      />
      <StyledTextInput
        value={email}
        onChangeText={text => setEmail(text)}
        placeholder="email"
        ref={refEmail}
        returnKeyType="done"
      />
    </>
  );
};

export default Form;
```
- useRef 함수를 이용하여 refName과 refEmail를 생성해 각각 이름과 이메일을 입력받는 TextInput 컴포넌트의 ref로 설정했고, 키보드의 완료 버튼을 각각 next와 done으로 변경했다.
- 또한 이름을 받는 컴포넌트의 확인(next)버튼을 클릭하면 이메일을 입력받는 컴포넌트로 포커스가 이동하도록 작성했으며, Form 컴포넌트가 마운트될 때 포커스가 이름을 입력받는 컴포넌트에 있도록 수정했다.

## useMemo
- useMemo는 React에서 제공하는 훅으로, 메모이제이션을 활용해 특정 연산의 결과를 저장해두고, 불필요한 반복 계산을 피하도록 도와준다.
- 이 훅은 복잡한 계산이 매번 다시 이루어지지 않도록 최적화하는 역할을 하며, 의존성 배열에 따라 값이 바뀔 때만 연산이 다시 수행되도록 설정할 수 있다.

### 메모제이션와 useMemo
- 메모이제이션이란 같은 계산을 반복해야 할 때 그 결과를 저장해두고, 다시 필요할 때 저장된 값을 꺼내 사용하는 기법이다.
- 반복적으로 동일한 연산을 수행하지 않아도 되어, 성능이 크게 향상된다.
- useMemo는 이 메모이제이션을 React 컴포넌트에서 사용할 수 있도록 지원하는 훅이다.

### useMemo의 동작 방식
- useMemo는 특정 계산의 결과를 기억하고 있다가, 다음에 해당 계산이 필요할 때 의존하는 값이 바뀌지 않았으면 이전 결과를 그대로 반환한다.
- 만약 의존하는 값이 바뀌었다면, 새로운 결과를 계산해 반환하고, 그 결과를 다시 기억한다.

```js
useMemo(()=>{},[]);
```

- 첫 번째 파라미터에는 함수를 전달하고, 두 번째 파라미터에는 함수 실행 조건을 배열로 전달하면 지정된 값에 변화가 있는 경우에만 함수가 호출된다.

- components폴더에 Length.js파일을 생성하고 문자열의 길이를 계산하는 컴포넌트를 만들자
```js
import React, { useState, useMemo } from 'react';
import styled from 'styled-components/native';
import Button from './Button';

const StyledText = styled.Text`
  font-size: 24px;
`;

const getLength = text => {
  console.log(`Target Text: ${text}`);
  return text.length;
};

const list = ['JavaScript', 'Expo', 'Expo', 'React Native'];

let idx = 0;
const Length = () => {
  const [text, setText] = useState(list[0]);
  const [length,setLength] = useState('');

  const _onPress = () => {
    setLength(getLength(text));
    ++idx;
    if (idx < list.length) setText(list[idx]);
  };

  return (
    <>
      <StyledText>Text: {text}</StyledText>
      <StyledText>Length: {length}</StyledText>
      <Button title="Get Length" onPress={_onPress} />
    </>
  );
};

export default Length;
```
- 4칸짜리 배열을 생성하고, 버튼을 클릭할 때마다 배열을 순환하면서 문자열의 길이를 구하는 컴포넌트를 작성했다.
- 이제 Length 컴포넌트를 App 컴포넌트에서 사용하도록 수정하자

```js
import Length from './components/Length'

const App = () => {
  return (
    <Container>
      <Length />
    </Container>
  );
};
```
- 화면에서 버튼을 클릭하면 현재 문자열의 길이를 구하는 것을 확인할 수 있다.
- 마지막 문자열 이후에는 더 이상 문자열의 변화가 없기 때문에 같은 문자열의 길이를 반복해서 구한다.
- 특별한 문제 없이 잘 동작하지만 두 번째와 세 번째는 Expo라는 동일한 문자열의 길이를 계산했고, 배열의 마지막 값 이후에는 문자열의 변화가 없는데도 계속해서 getLength 함수가 호출된다.
- 이런 상황에서 useMemo를 이용하면 계산하는 값에 변화가 있는 경우에만 함수가 호출되므로 중복되는 불필요한 연산을 제거할 수 있다.
- Length 컴포넌트에 useMemo를 사용해서 계산할 값에는 변화가 없는 경우 getLength 함수가 호출되지 않도록 수정하자
```js
const Length = () => {
  const [text, setText] = useState(list[0]);

  const _onPress = () => {
    ++idx;
    if (idx < list.length) setText(list[idx]);
  };
  const length = useMemo(() => getLength(text), [text]);

  ...

```
- useMemo를 사용해 text의 값이 변경되었을 때만 text 길이를 구하도록 수정했다.
- 결과를 보면 동일한 문자열인 Expo를 다시 계산하지 않고, 배열의 마지막 값이 이후에는 문자열의 변화가 없기 때문에 더 이상 getLength 함수를 호출하지 않는다는 것을 확인할 수 있다.

### 언제 useMemo를 사용해야 할까?
### `비용이 큰 계산이나 반복 작업이 있을 때`
- 복잡한 배열 연산이나 필터링, 정렬 등의 작업을 useMemo로 최적화할 수 있다.
```js
import React, { useState, useMemo } from 'react';
import { View, Text, TextInput, ScrollView } from 'react-native';

function ExpensiveFilter() {
    const [query, setQuery] = useState('');
    const items = Array.from({ length: 1000 }, (_, i) => `Item ${i + 1}`); // 큰 배열 예시

    // query가 변경될 때만 필터링 작업을 수행
    const filteredItems = useMemo(() => {
        console.log("Filtering items...");
        return items.filter(item => item.toLowerCase().includes(query.toLowerCase()));
    }, [query]);

    return (
        <View style={{ padding: 20 }}>
            <TextInput
                style={{ height: 40, borderColor: 'gray', borderWidth: 1, marginBottom: 10 }}
                placeholder="Search..."
                value={query}
                onChangeText={setQuery}
            />
            <ScrollView>
                {filteredItems.map((item, index) => (
                    <Text key={index} style={{ fontSize: 16 }}>{item}</Text>
                ))}
            </ScrollView>
        </View>
    );
}

export default ExpensiveFilter;
```
- 여기서는 query가 변경될 때만 필터링 작업이 다시 수행되며, items 배열이 커도 불필요한 연산을 줄여 성능을 높일 수 있다.

### `렌더링 성능이 중요한 경우`
- 불필요한 재계산이 자주 발생하는 경우, 이를 방지해 렌더링 성능을 높일 수 있다.
```js
import React, { useState, useMemo } from 'react';
import { View, Text, Button } from 'react-native';

function RenderOptimizedComponent() {
    const [count, setCount] = useState(0);
    const [expensiveValue, setExpensiveValue] = useState(100);

    // expensiveValue가 변경될 때만 복잡한 계산을 수행
    const computedValue = useMemo(() => {
        console.log("Calculating expensive value...");
        let result = expensiveValue;
        for (let i = 0; i < 1000000; i++) {
            result += i;
        }
        return result;
    }, [expensiveValue]);

    return (
        <View style={{ padding: 20 }}>
            <Text style={{ fontSize: 18 }}>Expensive Calculation Result: {computedValue}</Text>
            <Button title="Increment Count" onPress={() => setCount(count + 1)} />
            <Text style={{ fontSize: 18, marginTop: 10 }}>Count: {count}</Text>
            <Button title="Increase Expensive Value" onPress={() => setExpensiveValue(expensiveValue + 10)} />
        </View>
    );
}

export default RenderOptimizedComponent;
```
- 여기서 count가 변경될 때는 computedValue가 다시 계산되지 않으므로, 렌더링 성능을 높일 수 있다. 
- expensiveValue가 변경될 때만 복잡한 계산을 다시 수행하게 된다.

### `상태 값이 변경되지 않는 한 같은 계산 결과를 사용하고 싶을 때`
- 특정 상태 값이 변하지 않는다면, 이전에 계산한 값을 재사용하여 성능을 개선할 수 있다. 
```js
import React, { useState, useMemo } from 'react';
import { View, Text, Button } from 'react-native';

function AverageCalculator() {
    const [numbers, setNumbers] = useState([10, 20, 30, 40, 50]);
    const [extra, setExtra] = useState(0);

    // numbers 배열이 변경될 때만 평균을 재계산
    const average = useMemo(() => {
        console.log("Calculating average...");
        const sum = numbers.reduce((acc, curr) => acc + curr, 0);
        return sum / numbers.length;
    }, [numbers]);

    return (
        <View style={{ padding: 20 }}>
            <Text style={{ fontSize: 18 }}>Average: {average}</Text>
            <Button title="Add Number" onPress={() => setNumbers([...numbers, Math.floor(Math.random() * 100)])} />
            <Button title="Change Extra State" onPress={() => setExtra(extra + 1)} />
            <Text style={{ fontSize: 18, marginTop: 10 }}>Extra Value (unrelated): {extra}</Text>
        </View>
    );
}

export default AverageCalculator;
```
- 여기서는 numbers 배열이 변경될 때만 average가 다시 계산된다. 
- extra 상태는 average 계산에 영향을 주지 않기 때문에, 불필요한 재계산을 방지하고 성능을 높일 수 있다.

## 커스텀 Hooks 만들기
- 우리만의 hook를 만들 수 있다.
- 우리가 만들 hook 함수는 특정 API에 GET요청을 보내고 응답을 받는 함수이다.
- 리액트 네이티브에서는 네트워크 통신을 위해 Fetch와 XMLHttpRequest를 제공하고, 추가적으로 WebSocket도 지원한다.
- 이번에는 Fecth를 이용하여 useFetch라는 이름의 hook을 만들어보자
- src안에 hooks라는 폴더를 만들고 안에 useFetch.js파일을 만들자

```js
import { useState,useEffect } from "react";

export const useFetch = url => {
    const [data, setData] = useState(null);
    const [error, setError] = useState(null);

    useEffect(async() => {
        try {
            const res = await fetch(url);
            const result = await res.json();
            if (res.ok){
                setData(result);
                setError(null);
            } else {
                throw result;
            }
        } catch (error) {
            setError(error);
        }
    },[]);
    return {data, error};
}
```
- 전달받은 API의 주소로 요청을 보내고 그 결과를 성공 여부에 따라 data 혹은 error에 담아서 반환하는 useFetch를 만들었다.
- 이제 만들어진 useFetch를 이용해 API 요청하는 Dog 컴포넌트를 작성해보자.
- components 폴더에 Dog.js 파일 만들기
```js
import React from "react";
import styled from "styled-components";
import { useFetch } from "../hooks/useFetch";

const StyledImage = styled.Image`
    background-color : #7f8c8d;
    width : 300px;
    height : 300px;
`;

const ErrorMessage = styled.Text`
    font-size : 18px;
    color : #e74c3c;
`;

const URL = 'https://dog.ceo/api/breeds/image/random';
const Dog = () => {
    const {data, error} = useFetch(URL);

    return(
        <>
            <StyledImage source={data?.message ? { uri : data.message} : nul} />
            <ErrorMessage>{error ?.message} </ErrorMessage>
        </>
    )
}

export default Dog;
```

## 옵셔널 체이닝
- JavaScript에서 객체의 속성에 안전하게 접근하기 위한 문법이다.
- 이 문법을 사용하면, 중첩된 객체 속성에 접근할 때 객체나 속성이 존재하지 않아도 에러를 발생시키지 않고 undefined를 반환하도록 한다.
- 옵셔널 체이닝을 통해 코드가 중단되지 않고 안전하게 실행될 수 있다.

### 옵셔널 체이닝 문법
- 셔널 체이닝은 ?.를 사용하여 작성한다. 
- 이 문법은 다음과 같은 상황에서 유용하게 쓰인다

#### 1. 객체 속성에 접근하기
- 중첩된 객체의 속성에 접근할 때 객체가 null 또는 undefined이면 에러가 발생할 수 있다. 
```js
const user = {
    profile: {
        name: "Alice"
    }
};

// 중첩된 객체 속성에 접근할 때 매번 null 체크가 필요함
let age;
if (user && user.profile && user.profile.age) {
    age = user.profile.age;
} else {
    age = undefined;
}

console.log(age); // undefined
-------------------------------------------------
const user = {
    profile: {
        name: "Alice"
    }
};

// 옵셔널 체이닝을 통해 더 간단하게 안전하게 접근 가능
const age = user.profile?.age;
console.log(age); // undefined

```

#### 2. 배열 요소에 접근하기
- 옵셔널 체이닝을 사용하면 배열이 존재하지 않거나, 해당 인덱스의 요소가 없어도 안전하게 접근할 수 있다.
```js
const users = [{ name: "Alice" }, null, { name: "Bob" }];

// 배열의 요소가 null인지 확인하는 코드가 필요함
let userName;
if (users[1] && users[1].name) {
    userName = users[1].name;
} else {
    userName = undefined;
}

console.log(userName); // undefined
---------------------------------------------
const users = [{ name: "Alice" }, null, { name: "Bob" }];

// 옵셔널 체이닝으로 더 간결하게 배열 요소에 접근 가능
const userName = users[1]?.name;
console.log(userName); // undefined
```

#### 3. 함수 호출하기
- 객체에 함수가 있을 때만 안전하게 호출할 수 있다.
- 함수가 undefined일 경우 호출하려고 하면 에러가 발생하지만, 옵셔널 체이닝을 사용하면 안전하게 함수가 있는 경우에만 호출할 수 있다.
```js
const apiResponse = {
    data: {
        user: {
            profile: {
                email: "alice@example.com"
            }
        }
    }
};

// 중첩된 데이터에 접근할 때 null 확인이 필요함
let email;
if (apiResponse && apiResponse.data && apiResponse.data.user && apiResponse.data.user.profile) {
    email = apiResponse.data.user.profile.email;
} else {
    email = undefined;
}

console.log(email); // "alice@example.com"

------------------------------------------------
const apiResponse = {
    data: {
        user: {
            profile: {
                email: "alice@example.com"
            }
        }
    }
};

// 옵셔널 체이닝으로 중첩된 데이터에 간단하게 접근 가능
const email = apiResponse.data?.user?.profile?.email;
console.log(email); // "alice@example.com"
```

### 옵셔널 체이닝의 장점
- 안정성 : null 또는 undefined인 값에 접근할 때 발생하는 오류를 방지한다.
- 가독성 : 여러 중첩된 속성에 접근할 때 코드를 짧고 명확하게 작성할 수 있다.
- 간편한 에러 처리 : 값이 없을 경우 undefined를 반환하기 때문에 별도의 if문이나 try-catch문 없이도 에러 처리가 가능하다.

