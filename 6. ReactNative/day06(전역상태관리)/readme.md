# Context API
- 만약 컴포넌트가 아니라 전역적으로 상태를 관리하려면 어떻게 해야할까?
- Context API는 데이터를 전역적으로 관리하고 사용할 수 있도록 하는 기능이다.

### 프로젝트 생성하기
```js
expo init react-native-context
```
- styled-components 설치하기
```js
npm install styled-components --force
```
- src폴더를 생성하고 App컴포넌트를 작성한다.
```js
import React from 'react'
import styled from 'styled-components'

const Container = styled.View`
    flex : 1;
    background-color : #ffffff;
    justify-content : center;
    align-items : center;
`;

const App = () => {
    return <Container></Container>
}

export default App;
```
- 루트 디렉터리에 있는 App.js파일에서 src폴더의 App.js컴포넌트를 사용하도록 수정한다.
```js
import App from "./src/App";

export default App;
```

## 전역 상태 관리
- 일반적인 리액트 네이티브 애플리케이션의 경우 데이터는 부모 컴포넌트에서 자식 컴포넌트로 전달된다.
- 만약 데이터를 사용하는 컴포넌트가 많다면, 최상위 컴포넌트인 App 컴포넌트에서 상태를 관리하여 하위 컴포넌트 어디서 필요로 하든 전달할 수 있게 해야한다.
- 예를 들어, 어떤 데이터를 App 컴포넌트에서 관리하고 하위 컴포넌트 중 몇 개의 컴포넌트에서 데이터를 사용한다면, App 컴포넌트로부터 데이터를 필요로 하는 컴포넌트까지 props를 통해 값을 전달해서 사용할 수 있다.
- 하지만 props를 이용하여 데이터를 전달하는 방법은 상당히 번거롭다.

### 1. Props Drilling 문제
- `개념`: Props Drilling은 데이터를 최하위 자식 컴포넌트에 전달하기 위해 여러 단계의 중간 컴포넌트들을 거쳐야 하는 상황을 의미한다.
- `문제점`: 계층이 깊어지면, 특정 데이터를 사용하지 않는 중간 컴포넌트들도 props를 받아야 하고, 이를 다시 자식 컴포넌트로 전달해야 한다. 이로 인해 코드가 복잡해지고 가독성이 떨어지며, 유지보수가 어려워진다.
- `예시`: 최상위 컴포넌트에서 깊숙이 위치한 자식 컴포넌트로 데이터를 전달하려면 모든 중간 컴포넌트가 해당 props를 받아 전달해야 한다. 이는 코드를 장황하게 만들고, 중간 컴포넌트들이 불필요하게 props를 다루게 한다.

### 2. 재사용성과 독립성이 떨어짐
- `개념`: 컴포넌트가 특정 데이터와 강하게 결합되면, 해당 컴포넌트를 다른 곳에서 재사용하기가 어려워진다.
- `문제점`: 계층이 깊어질수록 특정 데이터와 의존 관계가 강해지는 경향이 있어, 개별 컴포넌트를 독립적으로 사용하거나 테스트하는 것이 어려워질 수 있다.
- `결과`: 데이터 전달에 의존적인 컴포넌트는 다른 컨텍스트에서 재사용할 때 데이터 구조를 맞추어야 하는 번거로움이 생기며, 이는 코드의 유연성을 저해한다.

### 3. 상태 관리와 동기화의 어려움
- `개념`: 상태가 상위 컴포넌트에 위치한 경우, 자식 컴포넌트에서 상태를 변경하려면 최상위 컴포넌트로 다시 값을 전달해 상태를 변경해야 한다.
- `문제점`: 컴포넌트 계층이 깊을수록 상태 업데이트 과정이 복잡해진다. 상위 컴포넌트에서 상태를 관리하고 이를 여러 단계의 자식 컴포넌트로 전달하는 과정에서 버그가 발생할 가능성이 높아진다.
- `예시`: 자식 컴포넌트에서 이벤트가 발생하여 상태를 변경해야 할 때, 상위 컴포넌트로 이벤트를 전달하고, 상태가 변경된 후 다시 자식 컴포넌트로 전달되어야 하므로 코드가 복잡하고 비효율적이 된다.

### 4. 불필요한 리렌더링
- 개념: 상위 컴포넌트의 상태가 변경되면, 해당 상태를 전달받는 모든 하위 컴포넌트가 리렌더링된다.
- 문제점: 계층이 깊어지면, 상태를 직접적으로 사용하지 않는 중간 컴포넌트까지 리렌더링될 수 있다. 이로 인해 성능이 저하되고, 애플리케이션이 느려질 수 있다.
- 결과: 최적화가 어려워지고, 불필요한 리렌더링을 줄이기 위해 코드에 여러 가지 조치가 필요해진다. 특히 큰 트리 구조의 컴포넌트에서 이 문제는 성능에 큰 영향을 줄 수 있다.

### 5. 유지보수와 코드 가독성 저하
- `개념`: 복잡한 계층 구조에서 props 전달 경로가 길어지면, 데이터가 어디에서 시작되고, 어떻게 흐르는지 추적하기 어려워진다.
- `문제점`: 데이터 흐름이 복잡해지면서 코드 가독성이 떨어지고, 유지보수하기 어려워진다. 특히 새로운 개발자가 프로젝트에 참여하거나 시간이 지나 코드의 컨텍스트를 잊게 되었을 때, 이 데이터 흐름을 이해하고 수정하는 데 많은 시간이 소요된다.
- `결과`: 데이터 전달 구조가 복잡할수록 예기치 않은 버그가 발생할 가능성이 높아지고, 코드가 복잡해지며 유지보수가 어려워진다.

## Context API
- Context API는 React.createContext 함수를 이용해 생성되며, Provider와 Consumer로 구성되어 있다.
  - Provider: 데이터를 제공하는 역할을 한다. Provider는 value라는 속성을 가지며, 이 속성을 통해 Context에서 공유할 데이터를 전달한다.
  - Consumer: 데이터를 소비하는 역할을 하며, Provider가 제공하는 데이터를 직접 사용할 수 있다. 

### 사용방법
#### 1. context의 생성
```js
import React, { createContext } from 'react';

const MyContext = createContext(null);
```
- createContext 함수를 호출해 새로운 Context를 생성한다. 
- MyContext가 생성되면, Provider와 Consumer를 사용할 수 있다.

#### 2. Provider로 제공하기
- Provider를 통해 상위 컴포넌트에서 데이터를 하위 컴포넌트들에게 제공할 수 있다.
```js
import React from 'react';
import { MyContext } from './MyContext';

const MyProvider = ({ children }) => {
  const sharedValue = 'Hello, Context!';

  return (
    <MyContext.Provider value={sharedValue}>
      {children}
    </MyContext.Provider>
  );
};

export default MyProvider;
```
- 위와 같이 Provider는 value 속성을 통해 데이터를 전달한다. 
- 이 value 속성은 Context를 통해 모든 하위 컴포넌트에서 접근할 수 있는 값이 된다.

#### 3. Consumer 사용하기
- Context의 데이터를 하위 컴포넌트에서 사용할 수 있다.
```js
import React from 'react';
import { MyContext } from './MyContext';

const MyComponent = () => (
  <MyContext.Consumer>
    {value => <div>{value}</div>}
  </MyContext.Consumer>
);
```

### User.js파일 만들기
- src폴더에 contexts폴더를 만들고 안에 User.js파일을 만든다.
```js
import { createContext } from 'react';

const UserContext = createContext({ name: 'Beomjun Kim' });

export default UserContext;
```

### Consumer
- Consumer 컴포넌트는 상위 컴포넌트 중 가장 가까운 곳에 있는 Provider 컴포넌트가 전달하는 데이터를 이용한다.
- 만약 상위 컴포넌트 중 Provider 컴포넌트가 없다면 createContext 함수의 파라미터로 전달된 기본값을 사용한다.
- src폴더 안에 components폴더를 생성하고 Consumer컴포넌트를 이용해서 createContext 함수의 파라미터로 전달된 기본값을 출력하는 User 컴포넌트를 작성해보자.

#### 사용법
```js
const MyContext = createContext(null);

<MyContext.Consumer>
```

```js
import React from 'react';
import styled from 'styled-components/native';
import UserContext from '../contexts/User';

const StyledText = styled.Text`
  font-size: 24px;
  margin: 10px;
`;

const User = () => {
    return (
        <UserContext.Consumer>
          {value => <StyledText>Name: {value.name}</StyledText>}
        </UserContext.Consumer>
      
    );
};

export default User;
```
- Consumer 컴포넌트의 자식은 반드시 리액트 컴포넌트를 반환하는 함수여야 하고, 이 함수는 Context의 현재값을 파라미터로 전달받아 데이터를 사용할 수 있다.
- 작성된 User 컴포넌트를 App 컴포넌트에서 사용해보자.

```js
import React from 'react'
import styled from 'styled-components'
import User from './components/User';
const Container = styled.View`
    flex : 1;
    background-color : #ffffff;
    justify-content : center;
    align-items : center;
`;

const App = () => {
    return( 
    <Container>
        <User />
    </Container>
    )
}

export default App;
```
- 입력한 이름이 잘 나오는것을 확인할 수 있다.

### Provider
- Context에 있는 Provider 컴포넌트는 하위 컴포넌트에 Context 변화를 알리는 역할을 한다.
- Provider컴포넌트는 value를 받아서 모든 하위 컴포넌트에 전달하고, 하위 컴포넌트는 provider컴포넌트의 value가 변경될 때마다 다시 렌더링된다.
- 우리가 사용한 styled 컴포넌트를 생각하면 쉽게 이해할 수 있다.
- ThemeProvider 컴포넌트를 최상위 컴포넌트로 사용하여 theme에 우리가 정의한 색을 지정하면 모든 하위 컴포넌트에서 theme을 받아서 사용할 수 있었다.
- theme로 지정한 색을 변경하면 모든 컴포넌트에서 변경된 색이 반영되었다.
- App컴포넌트에서 Provider 컴포넌트를 사용해보자.

```js
import UserContext from './contexts/User';

...

const App = () => {
    return( 
     <UserContext.Provider>
    <Container>
        <User />
    </Container>
     </UserContext.Provider>
    )
}

export default App;
```
- App 컴포넌트를 Provider컴포넌트로 감쌌기 때문에 User 컴포넌트에서 사용된 Consumer 컴포넌트는 더 이상 Context의 기본값을 사용하지 않고 상위 컴포넌트인 Provider 컴포넌트가 전달하는 데이터를 사용하도록 변경되었다.
- 하지만 provider컴포넌트에서는 어떤 값도 전달되지 않고 Consumer컴포넌트의 자식으로 지정된 함수의 파라미터로 undefined가 전달되면서 오류 메시지가 나타난다.
- 이 문제는 Provider 컴포넌트의 value에 값을 전달하여 해결할 수 있다.
```js
<UserContext.Provider value={{name:'Gildong'}}>
<Container>
    <User />
</Container>
</UserContext.Provider>
```
- Context를 생성할 때 전달한 기본값이 아닌 provider 컴포넌트의 value로 지정된 값이 잘 나타나는걸 확인할 수 있다.
- Provider 컴포넌트로부터 value를 전달하는 하위 컴포넌트의 수에는 제한이 없다.
- 하지만 Consumer 컴포넌트는 가장 가까운 Provider 컴포넌트에서 값을 받으므로, 자식 컴포넌트 중 Provider 컴포넌트가 있다면 그 이후의 자식 컴포넌트 중간에 있는 Provider 컴포넌트가 전달하는 값을 사용한다.
- components의 User.js 코드 추가하기
```js
const User = () => {
    return (
        <UserContext.Provider value={{name:'React Native'}}>
        <UserContext.Consumer>
          {value => <StyledText>Name: {value.name}</StyledText>}
        </UserContext.Consumer>
        </UserContext.Provider>
      
    );
};
```
- User 컴포넌트에서 사용된 Provider 컴포넌트의 데이터로 나타난다.
- Provider 컴포넌트를 사용할 때 반드시 value를 지정해야 한다는 점과 Consumer 컴포넌트는 가장 가까운 Provider가 전달하는 값을 이용한다는 점을 꼭 기억해두자.

### Context 수정하기
- 지금까지 Provider 컴포넌트를 이용해 데이터를 전달하고 Consumer 컴포넌트를 이용해 내용을 출력하는 방법에 대해서 알아봤다.
- 이번에는 Context의 값을 수정해 Context를 사용하는 컴포넌트에 변경된 내용을 반영하는 방법을 살펴보자.
- contexts의 User.js 수정하기
```js
import React, { createContext, useState } from 'react';

// 1. Context 생성 및 기본 값 설정
// `UserContext`를 생성하고, 기본 값으로 `user` 객체와 `dispatch` 함수를 설정함.
// `user`는 사용자 정보 (여기서는 이름)이고, `dispatch`는 이름을 업데이트하는 함수로 사용될 예정임.
const UserContext = createContext({
  user: { name: '' },  // 기본 사용자 이름을 빈 문자열로 설정
  dispatch: () => {},  // 기본 `dispatch`는 빈 함수로 설정
});

// 2. UserProvider 컴포넌트 정의
// `UserProvider`는 `UserContext`의 값을 제공하는 역할을 함.
// 하위 컴포넌트들이 `UserContext`에 접근할 수 있게 해줌.
const UserProvider = ({ children }) => {
  // `name` 상태를 "Beomjun Kim"으로 초기화하고, `setName`을 통해 상태를 업데이트할 수 있게 함.
  const [name, setName] = useState('Beomjun Kim');

  // `value` 객체에는 현재 `user` 상태와 상태를 업데이트할 함수 `dispatch`를 포함함.
  // `dispatch`로 `setName` 함수를 전달하여 하위 컴포넌트들이 이름을 업데이트할 수 있게 함.
  const value = { user: { name }, dispatch: setName };

  // `UserContext.Provider`를 사용해 하위 컴포넌트에게 `value` 객체를 전달.
  return <UserContext.Provider value={value}>{children}</UserContext.Provider>;
};

// 3. Consumer 컴포넌트 정의
// `UserConsumer`는 `UserContext.Consumer`를 의미함.
// 하위 컴포넌트에서 `UserConsumer`를 사용하여 `UserContext`의 값에 접근할 수 있음.
const UserConsumer = UserContext.Consumer;

// `UserProvider`와 `UserConsumer`, `UserContext` 자체를 export하여 다른 파일에서 사용할 수 있게 함.
export { UserProvider, UserConsumer };
export default UserContext;

```
- Provider컴포넌트의 value에 전역적으로 관리할 상태 변수와 상태를 변경하는 함수를 함께 전달하는 UserProvider 컴포넌트를 생성했다.
- UserProvider 컴포넌트는 기존의 Provider 컴포넌트와 사용법이 동일하지만 하위에 있는 Consumer컴포넌트의 자식 함수의 파라미터로 데이터뿐만 아니라 데이터를 변경할 수 있는 함수도 함께 전달한다.
- createContext의 기본값도 userProvider 컴포넌트의 value로 전달하는 형태와 동일한 형태를 갖도록 작성했다.
- Consumer 컴포넌트의 상위 컴포넌트에 Provider 컴포넌트가 없더라도 동작에 문제가 생기지 않도록 형태를 동일하게 맞추는 것이 좋다.
- 마지막으로 Consumer 컴포넌트와 동일한 UserConsumer컴포넌트를 생성했다.
- 수정이 완료되면 App컴포넌트에서 Provider컴포넌트 대신 UserProvider컴포넌트를 사용하도록 수정하자.
```js
...
import { UserProvider } from './contexts/User';
...
const App = () => {
    return( 
     <UserProvider>
    <Container>
        <User />
    </Container>
     </UserProvider>
    )
}

export default App;
```
- UserProvider 컴포넌트는 내부에서 provider 컴포넌트를 이용해 value를 전달하므로 따로 value를 전달하지 않아도 괜찮다.
- 이제 User컴포넌트에서 전달된 새로운 value를 사용하도록 수정하자.
```js
...

import { UserConsumer } from '../contexts/User';

...

const User = () => {
    return (
        <UserConsumer>
          {({user}) => <StyledText>Name: {user.name}</StyledText>}
        </UserConsumer>
    );
};

export default User;
```
- Consumer 컴포넌트 대신에 UserConsumer컴포넌트를 사용했다.
- Provider 컴포넌트에서 전달되는 value의 형태가 변경되었기 때문에 함수 형태도 전달되는 값에 맞게 수정되었다.
- 이번에는 UserProvider 컴포넌트의 value로 전달되는 세너 함수를 이용해 입력되는 값으로 Context의 값을 변경하는 Input컴포넌트를 만들어보자.
- components폴더에 Input.js파일 만들기
```js
import React, { useState, useContext } from 'react';
import styled from 'styled-components/native';
import { UserConsumer } from '../contexts/User';

const StyledInput = styled.TextInput`
  border: 1px solid #606060;
  width: 250px;
  padding: 10px 15px;
  margin: 10px;
  font-size: 24px;
`;

const Input = () => {
  const [name, setName] = useState('');
  return (
    <UserConsumer>
        {({dispatch}) => {
            return(
                <StyledInput
                value={name}
                onChangeText={text => setName(text)}
                onSubmitEditing={() => {
                  dispatch(name);
                  setName('');
                }}
                placeholder="Enter a name..."
                autoCapitalize="none"
                autoCorrect={false}
                returnKeyType="done"
              />
            );
        }}
    </UserConsumer>
    );
};

export default Input;
```
- useState함수를 이용해서 name 상태 변수를 생성하고 TextInpu 컴포넌트에 값이 변경될 때마다 name에 반영되도록 작성했다.
- UserConsumer 컴포넌트의 자식 함수에 전달되는 value에는 Context의 값을 변경할 수 있는 dispatch함수가 함께 전달된다.
- dispatch함수를 이용해 키보드의 확인 버튼을 누르면 TextInput 컴포넌트에 입력된 값으로 Context의 값을 변경하도록 작성했다.
- App.js에 반영하기
```js
     <UserProvider>
    <Container>
        <User />
        <Input />
    </Container>
     </UserProvider>
```
- App 컴포넌트에서 Input컴포넌트를 사용했다.
- Input 컴포넌트에 다양한 값을 입력하고 확인 버튼을 눌렀을 때 입력한 값으로 Context의 값이 바뀔 것이다.

## useContext
- useContext함수는 Consumer 컴포넌트의 자식 함수로 전달되던 값과 동일한 데이터를 반환하므로 Consumer컴포넌트를 사용하지 않고 Context의 내용을 사용할 수 있게 해준다.
- components의 User.js 수정하기
```js
import React,{useContext} from 'react';
import styled from 'styled-components/native';
import UserContext from '../contexts/User';

...
const User = () => {
    const {user} = useContext(UserContext);
    return <StyledText>Name: {user.name}</StyledText>
};

export default User;
```
- Consumer컴포넌트를 사용할 때는 Consumer 컴포넌트의 자식으로 반드시 리액트 컴포넌트를 반환하는 함수를 넣어야한다.
- 하지만, useContext를 이용하면 Consumer 컴포넌트를 사용했을 때보다 사용법이 훨씬 간편하고 코드의 가독성도 좋아지는 것을 볼 수 있다.
- 이제 Input 컴포넌트도 useContext를 이용하여 수정해보자.
```js
import React, { useState, useContext } from 'react';
import styled from 'styled-components/native';
import UserContext, { UserConsumer } from '../contexts/User';

const StyledInput = styled.TextInput`
  border: 1px solid #606060;
  width: 250px;
  padding: 10px 15px;
  margin: 10px;
  font-size: 24px;
`;

const Input = () => {
  const [name, setName] = useState('');
  const { dispatch } = useContext(UserContext);

  return (
    <StyledInput
      value={name}
      onChangeText={text => setName(text)}
      onSubmitEditing={() => {
        dispatch(name);
        setName('');
      }}
      placeholder="Enter a name..."
      autoCapitalize="none"
      autoCorrect={false}
      returnKeyType="done"
    />
  );
};

export default Input;
```
- useContext를 사용한 코드도 문제 없이 잘 동작하는 것을 확인할 수 있다.
  