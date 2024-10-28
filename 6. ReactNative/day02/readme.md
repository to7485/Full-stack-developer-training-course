# 컴포넌트
- 컴포넌트는 재사용할 수 있는 조립 블록으로 화면에 나타나는 UI 요소라고 생각하면된다.

## 프로젝트 생성하기
- 실습을 위해 다음의 명령어를 사용하여 react-native-component라는 이름의 프로젝트를 생성한다.
```
expo init react-native-component
```

## JSX
- react-native-component 프로젝트의 App.js파일을 확인해보면 다음과 같은 코드를 확인할 수 있다. 

```js
import { StatusBar } from 'expo-status-bar';
import { StyleSheet, Text, View } from 'react-native';

export default function App() {
  return (
    <View style={styles.container}>
      <Text>Open up App.js to start working on your app!</Text>
      <StatusBar style="auto" />
    </View>
  );
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
    backgroundColor: '#fff',
    alignItems: 'center',
    justifyContent: 'center',
  },
});
```
- 자바스크립트 파일임에도 불구하고 HTML을 작성한것같은 코드들이 보인다.

### JSX의 기본 개념
- JSX는 리액트와 리액트 네이티브에서 화면을 만들 때 사용하는 문법인데, 쉽게 말해서 JavaScript와 HTML을 합친 형태라고 보면 된다.
- 객체 생성과 함수 호출을 위한 문법적 편의를 제공하기 위해 만들어진 확장 기능으로 리액트 프로젝트에서 사용된다.
- JSX는 가독성이 높고 작성하기도 쉬울 뿐만 아니라, XML과 유사하다는 점에서 중첩된 구조를 잘 나타낼 수 있다는 장점이 있다.
- 리액트 네이티브는 JSX문법을 사용하여 코드가 작성되므로 꼭 필요한 JSX 문법에 대해 알아보자

### 하나의 부모
- JSX에서는 여러 개의 요소를 표현할 경우 반드시 하나의 부모로 감싸야 한다.
- App.js파일을 수정해보자
```jsx
export default function App() {
  return (
      <Text>Open up App.js to start working on your app!</Text>
      <StatusBar style="auto" />
  );
}
```
- 에러가 나타나는것을 확인할 수 있다.
- JSX에서는 앞의 코드처럼 여러 개의 요소를 반환하는 경우에도 반드시 하나의 부모로 나머지 요소들을 감싸서 반환해야 한다.
```JSX
export default function App() {
  return (
    <View style={styles.container}>
      <Text>Open up App.js to start working on your app!</Text>
      <StatusBar style="auto" />
    </View>
  );
}
```
- View는 UI를 구성하는 가장 기본적인 요소로 웹 프로그래밍에서 \<div>와 비슷한 역할을 하는 컴포넌트이다.
- 컴포넌트를 반환할 때 View 컴포넌트처럼 특정 역할을 하는 컴포넌트로 감싸지 않고 여러 개의 컴포넌트를 반환하고 싶은 경우 Fragment 컴포넌트를 사용한다.

```jsx
import { Fragment } from 'react';

export default function App() {
  return (
    <Fragment>
      <Text>Open up App.js to start working on your app!</Text>
      <StatusBar style="auto" />
    </Fragment>
  );
}
```
- Fragment 컴포넌트를 사용하기 위해 import를 이용하여 불러오고 View 컴포넌트 대신 Fragment컴포넌트를 사용했다.
- 결과를 보면 기존의 View 컴포넌트에 적용된 스타일이 없어졌기 때문에 모습은 조금 바뀌었지만 오류 없이 정상적으로 동작하는 것을 확인할 수 있다.
- Fragment 컴포넌트는 단축 문법을 제공한다.
```jsx
import { Fragment } from 'react';

export default function App() {
  return (
    <>
      <Text>Open up App.js to start working on your app!</Text>
      <StatusBar style="auto" />
    </>
  );
}
```

### 자바스크립트 변수
- JSX는 내부에서 자바스크립트의 변수를 전달하여 이용할 수 있다.
- App.js 파일을 수정해보자
```jsx
export default function App() {
  const name = "Gil-Dong";
  return (
    <View style={styles.container}>
      <Text style={styles.text}>My name is {name}</Text>
      <StatusBar style="auto" />
    </View>
  );
}
```

![img](img/결과3.png)

### 자바스크립트 조건문
- 개발을 하다보면 자바스크립트의 변수를 이용해서 화면을 나타내는 것뿐만 아니라, 특정 조건에 따라 나타나는 요소를 다르게 하고싶은 경우가 있다.
- JSX에서도 자바스크립트의 조건문을 이용하여 상황에 따른 요소를 출력할 수 있다.
- 다만 제약이 약간 있으므로 복잡한 조건인 경우 JSX 밖에서 조건에 따른 값을 설정하고 JSX내에서 사용하는 조건문에서는 최대한 간단하게 작성하는 것이 코드를 조금 더 깔끔하게 작성할 수 있다.

#### if 조건문
- JSX 내부에서는 if문을 사용할 수 있기는 하지만, if문을 즉시실행함수 형태로 작성해야 한다.
```jsx
export default function App() {
  const name = "Mal-Dong";
  return (
    <View style={styles.container}>
      <Text style={styles.text}>
        {(()=>{
          if(name ==='Hanbit') return 'My name is Hanbit';
          else if(name === 'Gil-Dong') return 'My name is Gil-Dong';
          else return 'My name is React Native';
        })()}
        </Text>
      <StatusBar style="auto" />
    </View>
  );
}
```
- name 변수의 값에 따라 출력되는 내용이 달라진다.

### 삼항연산자
- JSX는 내부에서 if 조건문 외에도 삼항 연산자를 사용할 수 있다.
- App.js파일을 수정해보자
```jsx
export default function App() {
  const name = "Gil-Dong";
  return (
    <View style={styles.container}>
      <Text style={styles.text}>
        My name is {name === 'Gil-Dong' ? 'Gil-Dong Hong' : 'React-native'}
        </Text>
      <StatusBar style="auto" />
    </View>
  );
}
```
- name 변수의 값을 변경하면서 결과를 확인하면 삼항연산자 규칙에 따라 값이 바뀌는걸 볼 수 있다.

### AND 연산자와 OR연산자
- AND연산자와 OR 연산자를 잘 이용하면 특정 조건에 따라 컴포넌트의 렌더링 여부를 결정하도록 코드를 구성할 수 있다.
```JSX
import { StatusBar } from 'expo-status-bar';
import { StyleSheet, Text, View } from 'react-native';

export default function App() {
  const name = "Gil-Dong";
  return (
    <View style={styles.container}>
      {name === 'Gil-Dong' &&(
        <Text style={styles.text}> My name is Gil-Dong</Text>
      )}
      {name !== 'Gil-Dong' &&(
        <Text style={styles.text}> My name is not Gil-Dong</Text>
      )}
      <StatusBar style="auto" />
    </View>
  );
}
```
- AND 연산자 앞의 조건이 참일 때 뒤의 내용이 렌더링 되고, 거짓인 경우 나타나지 않는다.
- OR연산자는 AND연산자와 반대로 앞의 조건이 거짓인 경우 내용이 나타나고, 조건이 참인 경우 나타나지 않는다.

### null과 undefined
- 조건에 따라 출력하는 값을 변경하다 보면 컴포넌트가 null이나 undefined를 반환하는 경우가 있다.
- JSX의 경우 null은 허용하지만 undefined는 오류가 발생하는데 주의해야 한다.
- App.js파일을 수정해보자
```jsx
export default function App() {
  return null;
}
```
- 하지만 undefined를 반환하는 코드는 오류 메시지가 나타난다.
```jsx
export default function App() {
  return undefined;
}
```