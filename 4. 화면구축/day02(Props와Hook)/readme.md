# 프론트엔드 서비스 개발

## Todo 리스트
### Todo 컴포넌트 만들어보기
- 이 컴포넌트는 checkbox와 label을 렌더링하는 컴포넌트이다.
- src디렉터리 아래에 Todo.js 파일을 생성하고, 실습 코드를 작성한다.

```js
import React from "react";

const Todo = () => {
    return(
        <div className="Todo">
            <input type="checkbox" id="todo0" name="todo0" value="todo0"/>
            {/* 입력 필드나 체크박스 같은 거 옆에 텍스트를 붙이고 싶을 때 쓴다.
            label 태그는 <label for="inputId">텍스트</label> 이렇게 쓰고, for 속성은 이 레이블이 어떤 입력 요소와 연결될지를 지정한다. */}
            <label for="todo0">Todo 컴포넌트 만들기</label>
        </div>
    );
};

export default Todo;
```
- 현재 index.js는 App 컴포넌트가 렌더링 되고 있다.
- 따라서 Todo 컴포넌트를 화면에 출력하기 위해 App컴포넌트의 render함수에 Todo컴포넌트를 추가한다.

### App.js 코드 수정하기
```js
import logo from './logo.svg';
import Todo from './Todo' //Todo 컴포넌트를 사용하기 위해 import
import './App.css';

function App() {
  return (
    <div className="App">
      <Todo /> {/*Todo 컴포넌트 추가하기*/}
    </div>
  );
}

export default App;
```
- 바뀐 부분을 실행해보면 다음과 같이 나온다.

![image](img/실행화면.png)

- Todo를 2개 출력하려면 컴포넌트를 두개 쓰면 된다.
```js
import logo from './logo.svg';
import Todo from './Todo' //Todo 컴포넌트를 사용하기 위해 import
import './App.css';

function App() {
  return (
    <div className="App">
      <Todo /> 
      <Todo /> 
    </div>
  );
}

export default App;
```

## Props와 Hook
- 현재 프로젝트의 요구사항은 다양한 내용의 Todo를 추가하는 것이다.
- 하지만 지금은 타이틀이 정해진 똑같은 Todo를 반복해서 추가하고 있다.
- 이후에는 API에서 받아온 임의의 Todo를 출력할 수 있어야 한다.
- 임의의 Todo리스트는 각 Todo마다 다른 내용을 갖고 있어야 한다.
- 이 요구사항을 충족하기 위해 Todo 컴포넌트에 title을 매개변수로 넘겨야 한다.

## Hook
- 함수형 컴포넌트에서 상태와 생명주기 기능을 사용할 수 있게 해주는 기능이다.
- React 16.8에서 도입되었으며, 클래스 컴포넌트를 사용하는 대신 함수형 컴포넌트로도 상태 관리와 기타 기능을 구현할 수 있게 한다.


### useState
- 상태를 관리하는 Hook의 일종이다.
- 함수형 컴포넌트에서 상태 변수와 이를 업데이트할 수 있는 함수를 반환한다.

### 사용법
#### 1.상태 변수 선언
```js
const [state, setState] = useState(initialState);
```
- const [state, setState] : 배열의 구조분해 할당
  - 배열의 요소를 개별 변수에 할당하는 데 사용된다. 배열의 각 요소를 변수에 쉽게 분리할 수 있다.
```js
const numbers = [1, 2, 3, 4, 5];

// 배열을 구조 분해 할당하여 변수에 저장
const [first, second, third] = numbers;

console.log(first);  // 1
console.log(second); // 2
console.log(third);  // 3
```
- state: 현재 상태 값을 나타내는 변수.
- setState: 상태를 업데이트하는 함수.
- initialState: 상태의 초기값. 기본값을 설정하며, 숫자, 문자열, 배열, 객체 등 다양한 데이터 타입을 사용할 수 있다.

#### 2. 초기값의 설정
- useState의 초기값은 컴포넌트가 처음 렌더링될 때 한 번만 설정된다. 
- 이후에는 setState 함수를 통해 상태를 업데이트할 수 있다.
```js
import React, { useState } from 'react';

function Example() {
  const [message, setMessage] = useState('Hello, world!');

  return (
    <div>
      <p>{message}</p>
      <button onClick={() => setMessage('Hello, React!')}>Change Message</button>
    </div>
  );
}
```

#### 3. 상태 변수의 여러 개 사용하기
- 컴포넌트에서 여러 개의 상태 변수를 사용할 수 있다. 
- 각 useState 호출은 독립적인 상태 변수를 반환한다.
```js
import React, { useState } from 'react';

function MultiState() {
  const [count, setCount] = useState(0);
  const [name, setName] = useState('Alice');

  return (
    <div>
      <p>Count: {count}</p>
      <button onClick={() => setCount(count + 1)}>Increase Count</button>
      
      <p>Name: {name}</p>
      <button onClick={() => setName('Bob')}>Change Name</button>
    </div>
  );
}
```
```js
import { useState } from 'react';

function Counter() {
  const [count, setCount] = useState(0);

  return (
    <div>
      <p>Count: {count}</p>
      <button onClick={() => setCount(count + 1)}>Increase</button>
    </div>
  );
}
```
### 변수의 값이 변했을 때 새로고침을 안하고 어떻게 렌더링이 되는가?
- 상태를 변경하는 함수(setState, setCount 등)를 호출하면, 새로운 상태 값 또는 상태 업데이트 요청이 React의 상태 큐에 추가된다.
- React는 상태 큐를 처리하여 상태 변경 요청을 실제 상태에 반영한다. 이 과정에서 React는 비동기적으로 상태를 업데이트하므로, 여러 상태 변경 요청이 있을 때 효율적으로 처리할 수 있다.
- 상태가 변경되면 React는 해당 상태를 사용하는 컴포넌트를 다시 렌더링할 필요가 있다고 판단한다. 이 과정은 다음 단계로 진행된다:

## Props
- 컴포넌트에 데이터를 전달하는 방식이다.
- "properties"의 줄임말로, 부모 컴포넌트가 자식 컴포넌트에 정보를 전달할 때 사용된다. 
- 컴포넌트는 외부로부터 값을 받아서 렌더링하거나 동작할 수 있다.

### 기본 사용법
1. 부모 컴포넌트에서 props 전달하기
   - 부모 컴포넌트는 자식 컴포넌트에 props를 전달할 수 있다.
```js
function ParentComponent() {
  return (
    <ChildComponent name="Alice" age={30} />
  );
}
```
2. 자식 컴포넌트에서 props 사용하기
    - 자식 컴포넌트는 props를 매개변수로 받아서 사용할 수 있다.
```js
function ChildComponent(props) {
  return (
    <div>
      <p>Name: {props.name}</p>
      <p>Age: {props.age}</p>
    </div>
  );
}
```
- props.name과 props.age를 통해 부모 컴포넌트에서 전달한 name과 age 값을 사용할 수 있다.

### props의 특성
1. 읽기 전용
   - props는 자식 컴포넌트에서 읽기 전용이다. 
   - 즉, 자식 컴포넌트는 props를 수정할 수 없으며, 부모 컴포넌트에서 변경할 수 있다. 
   - 상태를 관리해야 하는 경우에는 state를 사용해야 한다.
2. 기본값 설정
   - props에 기본값을 설정할 수 있다. 
   - 이를 위해 defaultProps를 사용할 수 있다
```js
function MyComponent({ name }) {
  return <div>Hello, {name}</div>;
}

MyComponent.defaultProps = {
  name: 'Guest'
};

```
- 위 코드에서는 name prop이 전달되지 않으면 기본값 'Guest'를 사용한다.

3. 컴포넌트 재사용
    - props를 사용하면 컴포넌트를 재사용할 수 있다. 
    - 여러 개의 부모 컴포넌트가 같은 자식 컴포넌트를 사용하면서 각기 다른 props를 전달할 수 있다.
```js
function Greeting({ name }) {
  return <div>Hello, {name}!</div>;
}

function App() {
  return (
    <div>
      <Greeting name="Alice" />
      <Greeting name="Bob" />
    </div>
  );
}
```

4. 구조 분해 할당을 이용한 props 사용
   - 구조 분해 할당을 사용하여 props를 더 간편하게 사용할 수 있다
```js
function ChildComponent({ name, age }) {
  return (
    <div>
      <p>Name: {name}</p>
      <p>Age: {age}</p>
    </div>
  );
}
```
- 위 코드에서는 props 객체에서 name과 age를 직접 추출하여 사용할 수 있다.

### App.js에서 Todo컴포넌트에 item 매개변수 넘기기

```js
import Todo from './Todo'
import './App.css';
import React, {useState} from "react";

function App() {
  const [item,setItem] = useState({
    id : "0",
    title : "Hello World 1",
    done : true
  })
  return (
    <div className="App">
      <Todo item={item} />
    </div>
  );
}

export default App;
```

### App.js에서 넘어온 props값 넣기
```js
import React, {useState} from "react";

const Todo = (props) => {
    const [item, setItem] = useState(props.item);
    return(
        <div className="Todo">
            <input type="checkbox" 
                    id={item.id} 
                    name={item.id} 
                    checked={item.done}/>
            <label for={item.id}>{item.title} </label>
        </div>
    );
};

export default Todo;
```

## 연습
- App.js에 다음의 조건에 맞게 코드 작성하기
1. Todo를 하나 더 만들어 item을 하나 더 넘겨보자.
   - id는 "1"이다.
   - title은 "Hello World2"이다.
   - done은 false이다.
2. Todo를 두 개 연속으로 늘어 놓는 대신, 배열과 반복문을 이용해보자.
   - 반복문으로 생성된 Todo컴포넌트들을 어떻게 넘길것인가?

### App.js에 코드 추가하기
```js
import Todo from './Todo'
import './App.css';
import React, {useState} from "react";

function App() {
  const [items,setItems] = useState([
    {
    id : "0",
    title : "Hello World 1",
    done : true
    },
    {
      id : "1",
      title : "Hello World 2",
      done : false
    }
]);
//map()
//배열의 각 요소에 대해 지정된 함수를 호출하고, 그 결과로 새로운 배열을 생성한다.

//key
//React에서 리스트를 렌더링할 때 각 요소를 고유하게 식별하기 위해 사용하는 특별한 프로퍼티이다.
//key는 React가 요소를 식별하고, 업데이트를 효율적으로 처리하는 데 도움을 준다.
//key의 역할
//리스트 렌더링 최적화: React는 key를 사용하여 리스트의 요소가 변경된 경우, 어떤 요소가 변경되었는지 빠르게 파악할 수 있다.
//key의 사용법
//리스트를 렌더링할 때, 각 리스트 항목에 대해 고유한 key를 제공해야 한다.
const todoItems = items.length > 0 && items.map(item => <Todo item={item} key={item.id}/>);

  return (
    <div className="App">
      {todoItems}
    </div>
  );
}

export default App;
```

![image](img/실행화면2.png)


## material-ui를 이용한 디자인
- 우리가 Todo컴포넌트를 만들었듯이, material-ui는 UI를 위한 다양한 컴포넌트를 제공한다.
- 그 중 우리는 ListItem, ListItemText, InputBase, CheckBox 등의 컴포넌트를 이용해 복잡한 CSS를 사용하지 않고도 UI를 개선할 수 있다.

### Todo.js에 코드 추가하기
```js
import React, {useState} from "react";
import {ListItem,ListItemText,InputBase,CheckBox} from '@mui/material';

const Todo = (props) => {
    const [item, setItem] = useState(props.item);
    return(
        <ListItem>
        <Checkbox checked={item.done}/>
        <ListItemText>
            <InputBase 
                inputProps={{"aria-label" : "naked"}}
                type="text"
                id={item.id}
                name={item.id}
                value={item.title}
                multiline={true}
                fullWidth = {true}
            />
        </ListItemText>
    </ListItem>
    );
};

export default Todo;
```

### App.js에 코드 추가하기
```js
import Todo from './Todo'
import './App.css';
import React, {useState} from "react";
import {List, Paper } from "@mui/material";

function App() {
  const [items,setItems] = useState([
    {
    id : "0",
    title : "Hello World 1",
    done : true
    },
    {
      id : "1",
      title : "Hello World 2",
      done : false
      }
]);
///////////////////////////////////////////////////////////////
let todoItems = items.length > 0 && (
  <Paper style={{ margin: 16 }}>
    <List>
      {items.map((item) => (
        <Todo item={item} key={item.id} deleteItem={deleteItem}/>
      ))}
    </List>
  </Paper>
);
///////////////////////////////////////////////////////////////
  return (
    <div className="App">{todoItems}</div>
  );
}

export default App;

```
![image](img/결과.png)

## Todo추가
- Todo를 추가하기 위한 UI와 백엔드 콜을 대신할 가짜 함수를 만들어보자.
- Todo리스트를 추가하기 위한 이벤트를 구현하고 연결하는법을 알아보자

### AppTodo.js 생성하기
```js
import React, {useState} from "react";
import {Button, Grid2, TextField} from "@mui/material"

const AddTodo = (props) =>{
    const [item,setItem] = useState({title : ""});

    return(
        <Grid2 container style={{marginTop : 20}}>
            <Grid2 xs={11} md={11} item style={{paddingRight : 16}}>
                <TextField placeholder="Add Todo here" fullWidth/>
            </Grid2>
            <Grid2 xs={1} md={1} item>
                <Button fullWidth style={{height : '100%'}} color="secondary" variant="outlined">
                    +
                </Button>
            </Grid2>
        </Grid2>
    )
}

export default AddTodo;
```

### App.js에 AddTodo 컴포넌트 추가하기
```js
import Todo from './Todo'
import AddTodo from './AddTodo'
import './App.css';
import React, {useState} from "react";
///////////////////////////////////////////////////////////////
import {Container, List, Paper } from "@mui/material";
///////////////////////////////////////////////////////////////

function App() {
  const [items,setItems] = useState([
    {
    id : "0",
    title : "Hello World 1",
    done : true
    },
    {
      id : "1",
      title : "Hello World 2",
      done : false
      }
]);

let todoItems = items.length > 0 && (
  <Paper style={{ margin: 16 }}>
    <List>
      {items.map((item) => (
        <Todo item={item} key={item.id}/>
      ))}
    </List>
  </Paper>
);
///////////////////////////////////////////////////////////////
  return (
    <div className="App">
      <Container maxWidth="md">
        <AddTodo />
        <div className="TodoList">
          {todoItems}
        </div>
      </Container>
    </div>
  );
}
///////////////////////////////////////////////////////////////
export default App;
```



