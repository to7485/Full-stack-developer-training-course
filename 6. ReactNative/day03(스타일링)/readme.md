# 스타일링
- 리액트 네이티브에서 스타일링은 웹 프로그래밍에서 사용하는 CSS와 약간 차이가 있다.
- 3장에서 JSX의 문법에 대해 알아보면서 간단하게 살펴봤듯이 background-color처럼 하이픈으로 된 CSS와 달리 backgroundColor처럼 카멜 표기법으로 작성해야 한다.
- 그 이외에도 리액트 네이티브에서 알아둬야 할 스타일링 방법에 대해 알아보자
### 실습을 위해 프로젝트 생성하기
```js
expo init react-native-style
```
- 프로젝트 생성이 완료되면 src폴더를 생성하고 App컴포넌트를 다음과 같이 작성한다.
```js
import React from 'react';
import { Text, View } from 'react-native';

export default function App() {
  return (
    <View>
      <Text>React Native Style</Text>
      
    </View>
  );
}
```
- App 컴포넌트의 작성이 완료되면 루트경로에 있는 App.js파일을 다음과 같이 변경한다.
```js
import App from './src/App';

export default App;
```
- 리액트 네이티브에서는 자바스크립트를 이용해 스타일링 할 수 있다.
- 컴포넌트에는 style 속성이 있고, 이 속성에 인라인 스타일을 적용하는 방법과 스타일시트에 정의된 스타일을 사용하는 방법이 있다.
### 인라인 스타일링
- HTML의 인라인 스타일링처럼 컴포넌트에 직접 스타일을 입력하는 방식이다.
- 다만 HTML에서는 문자열 형태로 스타일을 입력하지만, 리액트 네이티브에서는 객체 형태로 전달해야 한다는 차이점이 있다.
- App 컴포넌트에 인라인 스타일을 적용해서 다음과 같이 수정해보자
```js
import React from 'react';
import { View, Text } from 'react-native';

const App = () => {
  return (
    <View
      style={{
        flex: 1,
        backgroundColor: '#fff',
        alignItems: 'center',
        justifyContent: 'center',
      }}
    >
      <Text
        style={{
          padding: 10,
          fontSize: 26,
          fontWeight: '600',
          color: 'black',
        }}
      >
        Inline Styling - Text
      </Text>
      <Text
        style={{
          padding: 10,
          fontSize: 26,
          fontWeight: '400',
          color: 'red',
        }}
      >
        Inline Styling - Error
      </Text>
    </View>
  );
};

export default App;
```
- 인라인 스타일링은 어떤 스타일이 적용되는지 잘 보인다는 장점이 있다.
- 하지만 두 Text 컴포넌트처럼 비슷한 역할을 하는 컴포넌트에 동일한 코드가 반복된다는 점과, 어떤 이유로 해당 스타일이 적용되었는지 코드만으로는 명확하게 이해하기 어렵다는 단점이 있다

### 클래스 스타일링
- 컴포넌트의 태그에 직접 입력하는 방식이 아니라 스타일시트에 정의된 스타일을 사용하는 방법이다.
- 스타일시트에 스타일을 정의하고 컴포넌트에서는 정의된 스타일의 이름으로 적용하는 클래스 스타일링 방법은 웹 프로그래밍에서 CSS클래스를 이용하는 방법과 유사하다.
- 프로젝트를 생성하면 함께 생성되는 App.js파일에서 클래스 스타일링이 적용된 모습을 확인할 수 있다.
- 인라인 스타일을 클래스 스타일 방식으로 변경해보자

### StyleSheet
- React Native의 내장 객체로, 화면에 표시될 요소들의 디자인(예: 배경색, 글꼴 크기, 여백)을 지정하는 역할을 한다.

### StyleSheet의 사용 이유
- React Native 앱은 웹이 아닌 모바일 환경에서 동작하기 때문에, CSS처럼 스타일을 작성하는 방식은 비효율적일 수 있다.
- StyleSheet를 사용하면 코드의 성능이 개선되고, 스타일을 체계적으로 관리할 수 있게 된다.

### StyleSheet의 사용 방법
- StyleSheet.create 메서드를 호출해 스타일을 정의한다.
- 이 메서드를 통해 스타일을 객체 형태로 작성할 수 있다.

### StyleSheet의 장점
1. **성능 향상**: StyleSheet.create를 사용하면 React Native가 스타일을 최적화해 앱 성능이 좋아진다.
2. **재사용 가능성**: 한 번 정의한 스타일을 여러 곳에서 재사용할 수 있다.
3. **가독성**: 스타일 코드가 깔끔하게 관리돼, 코드 가독성이 높아진다.

### 주요 스타일 속성
- **flex**: 요소가 공간을 차지하는 비율을 설정한다.
- **justifyContent**: 주축 방향(세로 또는 가로)으로 정렬 방식을 설정한다.
- **alignItems**: 교차축 방향(주축과 수직)으로 정렬 방식을 설정한다.
- **backgroundColor**: 배경색을 지정한다.
- **fontSize**: 글자 크기를 지정한다.
- **color**: 글자 색깔을 지정한다.

```js
import React from 'react';
import { StyleSheet, View, Text } from 'react-native';

const App = () => {
  return (
    <View style={styles.container}>
      <Text style={styles.text}>
        Inline Styling - Text
      </Text>
      <Text style={styles.error}>Inline Styling - Error</Text>
    </View>
  );
};

const styles = StyleSheet.create({
  container: {
    flex: 1,
    backgroundColor: '#fff',
    alignItems: 'center',
    justifyContent: 'center',
  },
  text: {
    padding: 10,
    fontSize: 26,
    fontWeight: '600',
    color: 'black',
  },
  error: {
   padding: 10,
    fontSize: 26,
    fontWeight: '400',
    color: 'red',
  },
});

export default App;
```
- 인라인 스타일을 적용했을 때보다 조금 더 깔끔해진 느낌을 받을 수 있다.
- 인라인 스타일 방식으로 작성했을 때는 왜 color: 'red'인지 코드만으로 명확하게 이해하기 어려웠었다.
- 지금은 error라는 이름으로 오류가 있는 상황에서 사용하기 위한 것이라는 의도를 파악하기 쉽다.
- 전체적인 스타일을 관리하는 데도 클래스 스타일링이 인라인 스타일링보다 더 쉽다.
- 만약 오류가 있는 상황에서 글자 색을 빨간색이 아니라 주황색으로 변경해야 한다면, 클래스 스타일 방식에서는 error 객체에서 color: 'orange'로만 변경하면 되지만, 인라인 방식에서는 모든 파일을 찾아다니며 변경해야 한다는 단점이 있다.

### 여러개 스타일 적용
- 우리가 작성한 App 컴포넌트 스타일 코드에서 text스타일과 error스타일은 중복된 스타일이 많으며, 두 스타일 모두 Text 컴포넌트에 적용되는 스타일이라는 공통접도 있다.
- 이렇게 중복된 코드를 제거하다 보면 스타일을 덮어쓰거나 하나의 컴포넌트에 여러 개의 스타일을 적용해야 할 때가 있다.
- 여러 개의 스타일을 적용해야 할 경우는 배열을 이용하여 style 속성에 여러 개의 스타일을 적용하면 된다.
```js
<View style={styles.container}>
    <Text style={[styles.text, { color: 'green' }]}>
    Inline Styling - Text
    </Text>
    <Text style={[styles.text, styles.error]}>Inline Styling - Error</Text>
</View>
...
error: {
fontWeight: '400',
color: 'red',
},
```
- 중복된 코드가 사라지면서 코드가 깔끔해지고 공통된 부분의 관리가 편해진다.
- 여러 개의 스타일을 적용할 때 주의할 점은 적용하는 스타일의 순서이다.
- 뒤에오는 스타일이 앞에 있는 스타일을 덮는다는 것을 기억해야 한다.
- 예를 들어 위의 코드에서 적용된 스타일의 순서를 [styles.error, styles.text]로 작성하면 글자의 색이 빨간색 대신 검은색으로 된다.
- 여러 개의 스타일을 적용할 때 반드시 클래스 스타일만 적용해야 하는 것은 아니다.
- 인라인 스타일과 클래스 스타일 방식을 혼용해서 사용할 수도 있다.

```js
const App = () => {
  return (
    <View style={styles.container}>
      <Text style={[styles.text, { color: 'green' }]}>
```

### 외부 스타일 시트 이용하기
- 우리가 만든 스타일을 다양한 곳에서 사용하고 싶은 경우 어떻게 해야 할까?
- 상황에 따라 외부 파일에 스타일을 정의하고 여러 개의 파일에서 스타일을 공통으로 사용하는 경우가 있다.
- 외부 파일에 스타일을 작성하고 컴포넌트에서 외부 파일에 정의된 스타일을 이용하는 방법에 대해 알아보자.
- src폴더 밑에 styles.js파일을 생성하고 다음과 같이 작성한다.
```js
import { StyleSheet } from 'react-native';

export const viewStyles = StyleSheet.create({
  container: {
    flex: 1,
    backgroundColor: '#fff',
    alignItems: 'center',
    justifyContent: 'center',
  },
});

export const textStyles = StyleSheet.create({
  text: {
    padding: 10,
    fontSize: 26,
    fontWeight: '600',
    color: 'black',
  },
  error: {
    fontWeight: '400',
    color: 'red',
  },
});
```
- 이제 App 컴포넌트에서 styles.js파일에 정의된 스타일을 이용하도록 수정하자
```js
import React from 'react';
import { View, Text } from 'react-native';
import { viewStyles, textStyles } from './styles';

const App = () => {
  return (
    <View style={viewStyles.container}>
      <Text style={[textStyles.text, { color: 'green' }]}>
        Inline Styling - Text
      </Text>
      <Text style={[textStyles.text, textStyles.error]}>
        Inline Styling - Error
      </Text>
    </View>
  );
};

export default App;
```

## 리액트 네이티브 스타일
- 리액트 네이티브에는 많은 종류의 스타일 속성들이 있다.
- 그중에는 특정 플랫폼에서만 적용되는 스타일도 있고 웹 프로그래밍에서 사용해본 익숙한 속성들도 있다.
- 자주 사용되는 중요한 스타일 속성들에 대해 알아보자

### flex와 범위
- 화면의 범위를 정하는 속성에는 폭과 높이를 나타내는 width와 height가 있다.
- 리액트 네이티브에서도 width와 height를 설정할 수 있다.
- Header와 Footer컴포넌트의 높이를 80으로 하고 Contents 컴포넌트가 나머지 영역을 차지하도록 구성하려면 높이값을 어떻게 설정해야 할까?
- src에 components 폴더를 생성하고 Layout.js파일을 생성한다.
- Layout.js 파일에는 Header 컴포넌트, Contents 컴포넌트, Footer 컴포넌트를 정의해서 화면에 나타나도록 정의한다.
```js
import React from 'react';
import { StyleSheet, View, Text } from 'react-native';

export const Header = () => {
  return (
    <View style={[styles.container, styles.header]}>
      <Text style={styles.text}>Header</Text>
    </View>
  );
};

export const Contents = () => {
  return (
    <View style={[styles.container, styles.contents]}>
      <Text style={styles.text}>Contents</Text>
    </View>
  );
};

export const Footer = () => {
  return (
    <View style={[styles.container, styles.footer]}>
      <Text style={styles.text}>Footer</Text>
    </View>
  );
};

const styles = StyleSheet.create({
  container: {
    width: '100%',
    alignItems: 'center',
    justifyContent: 'center',
    height: 80,
  },
  header: {
    backgroundColor: '#f1c40f',
  },
  contents: {
    backgroundColor: '#1abc9c',
    height: 640,
  },
  footer: {
    backgroundColor: '#3498db',
  },
  text: {
    fontSize: 26,
  },
});
```
- 작성이 완료되면 App 컴포넌트에서 정의된 세 개의 컴포넌트를 사용하도록 수정하자
```js
import React from 'react';
import { View } from 'react-native';
import { viewStyles } from './styles';
import { Header, Contents, Footer } from './components/Layout';

const App = () => {
  return (
    <View style={viewStyles.container}>
      <Header />
      <Contents />
      <Footer />
    </View>
  );
};

export default App;
```
- Header 컴포넌트와 Footer 컴포넌트의 높이를 80으로 고정하고, Contents 컴포넌트가 나머지 영역을 차지하도록 640이라는 값으로 설정했다.
- 하지만 고정값을 이용하면 기기마다 화면 크기의 차이 때문에 서로 다른 모습으로 나타나고 이런 다양한 크기의 기기에 대응하기 어렵다.
- 이때 flext를 이용하면 문제를 해결할 수 있다.
- flex는 width나 height와 달리 항상 비율로 크기가 설정된다.
- flex는 값으로 숫자를 받으며 값이 0일때는 설정된 width와 height값에 따라 크기가 결정되고, 양수인 경우 flex값에 비례하여 크기가 조절된다.
- 우리가 만든 컴포넌트가 화면을 1:2:1 비율로 나눠 채우게 하려면 어떻게 해야할까?
```js
  header: {
    flex: 1
    backgroundColor: '#f1c40f',
  },
  contents: {
    flex: 2
    backgroundColor: '#1abc9c',
    height: 640,
  },
  footer: {
    flex: 1
    backgroundColor: '#3498db',
  },
```
- 결과를 보면 영역을 1:2:1 비율로 나눠 차지하고 있는 모습을 확인할 수 있다.
- 원래 목적으로 돌아가서, 다양한 크기의 기기에 항상 동일하게 화면이 구성되도록 하려면 Header 컴포넌트와 Footer컴포넌트의 높이를 80으로 고정하고 Contents 컴포넌트가 나머지 부분을 차지하도록 설정하면 된다.
```js
  header: {
    backgroundColor: '#f1c40f',
  },
  contents: {
    flex: 1
    backgroundColor: '#1abc9c',
    height: 640,
  },
  footer: {
    backgroundColor: '#3498db',
  },
```

### 정렬
- flex를 이용하면 컴포넌트가 원하는 영역을 차지하게 할 수 있다.
- 이번에는 컴포넌트를 정렬하는 방법에 대해 알아보자

### flexDirection
- 지금까지 실습을 하면서 컴포넌트가 항상 위에서 아래로 쌓인다는 것을 살펴봤다.
- 화면을 구성하다보면 컴포넌트가 쌓이는 방향을 변경하고 싶을 때가 있는데 이때 flexDirection을 이용하면 컴포넌트가 쌓이는 방향을 변경할 수 있다.
- `flexDirection`은 요소들이 정렬되는 **주축의 방향**을 결정하는 속성이다. `row`와 `column`을 사용하여 가로 또는 세로 방향으로 정렬할 수 있다.

### flexDirection의 속성값
- **column** : 세로 방향으로 정렬
- **column-reverse**: 자식 요소들을 세로 방향으로 정렬하되, 역방향으로 배치한다.
- **row**: 자식 요소들을 **가로 방향**으로 정렬한다.
- **row-reverse**: 자식 요소들을 가로 방향으로 정렬하되, 역방향으로 배치한다.

![img](img/flex-direction.png)

- components폴더에 flexDirectionTest.js 만들기
```js
import React from 'react';
import { View, Text, Button } from 'react-native';
import { box_styles } from '../styles';

const FlexDirectionTest = () => {
    const [direction, setDirection] = React.useState('row');

    return (
        <View style={box_styles.container}>
            <Text style={box_styles.title}>flexDirection: {direction}</Text>
            <View style={[box_styles.boxContainer, { flexDirection: direction }]}>
                <View style={box_styles.box}><Text style={box_styles.boxText}>1</Text></View>
                <View style={box_styles.box}><Text style={box_styles.boxText}>2</Text></View>
                <View style={box_styles.box}><Text style={box_styles.boxText}>3</Text></View>
            </View>

            <View style={box_styles.buttons}>
                <Button title="Row" onPress={() => setDirection('row')} />
                <Button title="Column" onPress={() => setDirection('column')} />
                <Button title="Row Reverse" onPress={() => setDirection('row-reverse')} />
                <Button title="Column Reverse" onPress={() => setDirection('column-reverse')} />
            </View>
        </View>
    );
};

export default FlexDirectionTest;
```
- styles.js에 코드 추가하기
```js
export const box_styles = StyleSheet.create({
    container: {
        flex: 1,
        justifyContent: 'center',
        alignItems: 'center',
        padding: 20,
        backgroundColor: '#f5f5f5',
    },
    title: {
        fontSize: 18,
        marginBottom: 20,
    },
    boxContainer: {
        width: 200,
        height: 200,
        backgroundColor: '#ddd',
        justifyContent: 'center',
        alignItems: 'center',
        marginBottom: 20,
    },
    box: {
        width: 50,
        height: 50,
        backgroundColor: '#3498db',
        justifyContent: 'center',
        alignItems: 'center',
        margin: 5,
    },
    boxText: {
        color: '#fff',
        fontSize: 18,
    },
    buttons: {
        flexDirection: 'row',
        justifyContent: 'space-between',
        width: '100%',
    },
});
```

### justifyContent
- 컴포넌트 내부의 자식 요소들이 주축(main axis)을 따라 정렬되는 방식을 설정하는 스타일 속성이다.
- flexDirection 속성에 따라 주축의 방향이 바뀌는데, 기본적으로 flexDirection: 'column'일 경우 세로 방향이 주축이 되고, flexDirection: 'row'일 경우 가로 방향이 주축이 된다.

### 주요 속성값
- flex-start: 자식 요소들을 주축의 시작 부분에 배치한다. (기본값)
- center: 자식 요소들을 주축의 중앙에 배치한다.
- flex-end: 자식 요소들을 주축의 끝 부분에 배치한다.
- space-between: 첫 번째 자식 요소는 주축의 시작 부분에, 마지막 자식 요소는 주축의 끝 부분에 배치하며, 각 자식 요소 간에 동일한 간격을 둔다.
- space-around: 자식 요소들 사이에 동일한 간격을 배치하되, 주축의 양 끝에도 반 간격만큼의 여백을 둔다.
- space-evenly: 모든 자식 요소들 사이에 동일한 간격을 두며, 주축의 양 끝에도 동일한 간격을 둔다.
```js
import React, { useState } from "react";
import { View, Text, Button } from 'react-native';
import { box_styles } from '../styles';

const JustifyContentTest = () => {
    const [justifyContent, setJustifyContent] = useState('flex-start');

    return (
        <View style={box_styles.container}>
            <Text style={box_styles.title}>JustifyContent: {justifyContent}</Text>
            
            {/* 아래의 View에 감싸진 요소들을 justifyContent로 수평 정렬을 설정 */}
            <View style={[box_styles.boxContainer, { justifyContent: justifyContent }]}>
                <View style={box_styles.box}><Text>1</Text></View>
                <View style={box_styles.box}><Text>2</Text></View>
                <View style={box_styles.box}><Text>3</Text></View>
            </View>
            
            <View style={box_styles.buttons}>
                <Button title="Flex Start" onPress={() => setJustifyContent('flex-start')} />
                <Button title="Center" onPress={() => setJustifyContent('center')} />
                <Button title="Flex End" onPress={() => setJustifyContent('flex-end')} />
                <Button title="Space Between" onPress={() => setJustifyContent('space-between')} />
                <Button title="Space Around" onPress={() => setJustifyContent('space-around')} />
                <Button title="Space Evenly" onPress={() => setJustifyContent('space-evenly')} />
            </View>
        </View>
    );
}

export default JustifyContentTest;
```

![img](img/justifyContent.jfif)

### alignItems
- flexDirection에서 정한 방향과 수직이 되는 방향으로 정렬할 때 사용하는 속성이다.

### 주요 속성값
- flex-start : 시작점에서부터 정렬(기본값)
- flex-end : 끝에서부터 정렬
- center : 중앙 정렬
- stretch: alignItems의 방향으로 확대
- baseline : 컴포넌트 내부의 텍스트 베이스라인을 기준으로 정렬

```js
import React, { useState } from "react";
import { View, Text, Button } from 'react-native';
import { box_styles } from '../styles';

const AlignItemsTest = () => {
    const [alignment, setAlignment] = useState('flex-start');

    return (
        <View style={box_styles.container}>
            <Text style={box_styles.title}>AlignItems: {alignment}</Text>
            
            {/* 아래의 View에 감싸진 요소들을 alignItems로 수직 정렬을 설정 */}
            <View style={[box_styles.boxContainer, { alignItems: alignment }]}>
                <View style={box_styles.box}><Text>1</Text></View>
                <View style={box_styles.box}><Text>2</Text></View>
                <View style={box_styles.box}><Text>3</Text></View>
            </View>
            
            <View style={box_styles.buttons}>
                <Button title="Flex Start" onPress={() => setAlignment('flex-start')} />
                <Button title="Center" onPress={() => setAlignment('center')} />
                <Button title="Flex End" onPress={() => setAlignment('flex-end')} />
                <Button title="Stretch" onPress={() => setAlignment('stretch')} />
            </View>
        </View>
    );
}

export default AlignItemsTest;
```

### 그림자
- 그림자는 리액트 네이티브에서 플랫폼마다 다르게 적용되는 스타일 속성이다.
- 이 경우 리액트 네이티브에서 제공하는 Platform 모듈을 이용해 각 플랫폼마다 다른 코드가 적용되도록 코드를 작성할 수 있다.
- 문서 : https://bit.ly/react-native-platform

## Platform 모듈
- 앱이 실행되는 **운영 체제에 따라 다른 코드를 실행**할 수 있게 도와주는 도구다. 
- React Native로 앱을 개발하면 같은 코드로 iOS와 Android에서 동시에 실행할 수 있지만, **일부 기능이나 스타일은 플랫폼에 따라 다르게** 적용해야 할 때가 있다. 
- 이때 `Platform` 모듈을 사용하면 앱이 실행 중인 플랫폼에 맞춰 필요한 코드를 쉽게 추가할 수 있다.

### `Platform` 모듈 사용법
#### 1. `Platform.OS` 사용하기
- `Platform.OS`는 현재 앱이 실행 중인 플랫폼을 알려주는 값이다. 
- iOS에서는 `"ios"`, Android에서는 `"android"` 값을 반환한다.
```js
import { Platform, Text, View } from 'react-native';

const App = () => {
  return (
    <View>
      {Platform.OS === 'ios' ? (
        <Text>iOS에서 실행 중</Text>
      ) : (
        <Text>Android에서 실행 중</Text>
      )}
    </View>
  );
};

export default App;
```

#### 2. `Platform.select` 사용하기
- 운영 체제별로 서로 다른 값을 쉽게 설정할 수 있게 해준다.
- iOS와 Android에서 각각 다르게 설정해야 할 스타일이나 속성을 지정할 때 유용하다.
```js
import { Platform, StyleSheet, Text, View } from 'react-native';

const styles = StyleSheet.create({
  container: {
    paddingTop: Platform.select({
      ios: 50,      // iOS에서 paddingTop 50 적용
      android: 20,  // Android에서 paddingTop 20 적용
    }),
  },
});

const App = () => {
  return (
    <View style={styles.container}>
      <Text>플랫폼별 스타일 적용하기</Text>
    </View>
  );
};

export default App;
```

#### 3. `Platform.Version` 사용하기
- 운영 체제의 버전 번호를 가져오는 속성이다. 
- 이 값을 사용하면 iOS나 Android 버전에 따라 다른 코드를 실행할 수 있다.
```js
import { Platform, Text, View } from 'react-native';

const App = () => {
  return (
    <View>
      <Text>현재 플랫폼 버전: {Platform.Version}</Text>
      {Platform.OS === 'android' && Platform.Version < 30 ? (
        <Text>이 기능은 Android 30 이상에서만 지원됩니다.</Text>
      ) : (
        <Text>현재 플랫폼에서 지원되는 기능입니다.</Text>
      )}
    </View>
  );
};

export default App;
```
### 그림자 만들기
- Platform을 이용하여 iOS와 안드로이드 두 플랫폼에서 그림자를 만들어보자.
- components 폴더 밑에 ShadowBox.js 파일을 생성하고 platform을 이용하여 그림자가 있는 박스를 만들자
```js
import React from 'react';
import { StyleSheet, View, Platform } from 'react-native';

export default () => {
  return <View style={styles.shadow}></View>;
};

const styles = StyleSheet.create({
  shadow: {
    backgroundColor: '#fff',
    width: 200,
    height: 200,
    ...Platform.select({
      ios: {
        shadowColor: '#000',
        shadowOffset: {
          width: 10,
          height: 10,
        },
        shadowOpacity: 0.5,
        shadowRadius: 10,
      },
      android: {
        elevation: 20,
      },
    }),
  },
});
```
- 완성된 ShadowBox 컴포넌트를 App 컴포넌트에서 사용해보자
```js
import React from 'react';
import { View } from 'react-native';
import { viewStyles } from './styles';
import ShadowBox from './components/ShadowBox';

const App = () => {
  return (
    <View style={viewStyles.container}>
      <ShadowBox />
    </View>
  );
};

export default App;
```
- Platform을 사용하지 않고 스타일 코드를 작성해도 각 속성들이 적용되는 플랫폼에서만 동작한다.
- 하지만 어떤 코드가 어떤 플랫폼에 적용되는지, 코드의 역할은 무엇인지 알기 어려우므로 Platform을 이용해서 명확하게 작성하는 것을 추천한다.

## Styled-component
- 스타일드 컴포넌트는 자바스크립트 파일 안에 스타일을 작성하는 CSS-in-JS 라이브러리이며, 스타일이 적용된 컴포넌트라고 생각하면 이해하기 쉽다.
  
` ※ react-router-dom 과 충돌나는거 같다 최신버전으로는 설치가 안된다.`
```
npm install styled-components@5.3 --legacy-peer-deps
```

### 사용법
- 리액트 네이티브의 컴포넌트 이름을 styled 뒤에 붙여 스타일링된 컴포넌트를 만든다.
- 이때 styled 뒤에 작성하는 컴포넌트이름은 반드시 존재하는 컴포넌트여야 한다.
- 백틱(\` \`)안에 CSS 스타일을 작성하며, 이 스타일은 해당 컴포넌트에서만 적용된다.

```js
const 컴포넌트명 = styled.View`
  CSS코드
`

- 사용시
<컴포넌트명 />
```

### 스타일 적용하기
- components폴더에 Buttons.js파일을 생성하고 스타일드 컴포넌트를 이용해 다음과 같이 작성한다.
```js
import React from 'react';
import { StyleSheet, Pressable, Text } from 'react-native';

const styles = StyleSheet.create({
  container: {
    backgroundColor: '#9b59b6',
    borderRadius: 15,
    paddingVertical: 15,
    paddingHorizontal: 40,
    marginVertical: 10,
    justifyContent: 'center',
  },
  title: {
    fontSize: 20,
    fontWeight: '600',
    color: '#fff',
  },
});

const Button = props => {
  return (
    <ButtonContainer>
    <Title>{props.title}</Title>
  </ButtonContainer>
  );
};

export default Button;
```
- Pressable 컴포넌트에 스타일이 적용된 ButtonContainer라는 이름의 컴포넌트를 만들고 Text컴포넌트에 스타일이 적용된 Title 컴포넌트를 만들었다.
- 미자막으로 스타일드 컴포넌트로 만들어진 컴포넌트를 이용해 Button 컴포넌트를 만들었다.
- 스타일드 컴포넌트를 사용하면 이렇게 역할에 맞는 이름을 지정할 수 있다는 장점이 있다.
- 이제 완성된 Button 컴포넌트를 App 컴포넌트에 사용해보자.

```js
...
import Button from './components/Button';
import styled from 'styled-components';

const Container = styled.View`
  flex: 1;
  background-color: #ffffff
  align-items: center;
  justify-content: center;
`;

const App = () => {
  return (
    <Container>
      <Button title="Hanbit" />
      <Button title="React Native" />
  </Container>
  );
};

export default App;
```

![img](img/결과1.png);

### props 사용하기
- Button 컴포넌트에서 props로 전달되는 title의 값이 Hanbit인 경우 바탕색을 다르게 표현해보자
```js
import React from 'react';
import styled from 'styled-components';

const ButtonContainer = styled.Pressable`
 background-color: ${props =>
    props.title === 'Hanbit' ? '#3498db' : '#9b59b6'};
  border-radius: 15px;
  padding: 15px 40px;
  margin: 10px 0px;
  justify-content: center;
`;
...

const Button = props => {
  return (
    <ButtonContainer title={props.title}>
      <Title>{props.title}</Title>
    </ButtonContainer>
  );
};

export default Button;
```

- ButtonContainer 컴포넌트에 props로 title을 전달하여 배경색을 설정하는곳에서 title의 값에 따라 다른 색이 지정되도록 수정했다.
- 스타일드 컴포넌트를 이용하면 이 코드 처럼스타일이 작성되는 부분과 컴포넌트가 사용되는 부분을 구분하여 코드를 조금 더 깔끔하게 관리할 수 있다.


![img](img/결과2.png)

### attrs 사용하기
- 스타일드 컴포넌트를 사용하면 스타일을 작성하는 곳에서 컴포넌트의 속성도 설정할 수 있다.
- 그리고 속성을 설정할 때고 전달된 props를 이용할 수 있으므로 props의 값에 따라 속성을 변경할 수 있다.
- components 폴더 안에 Inputs.js파일을 생성한다.
```js
import React from 'react';
import styled from 'styled-components/native';

const StyledInput = styled.TextInput`
  width: 200px;
  height: 60px;
  margin: 5px;
  padding: 10px;
  border-radius: 10px;
  border: 2px;
  border-color: #3498db;
  font-size: 24px;
`;

const Input = props => {
  return <StyledInput placeholder="Enter a text..." placeholderTextColor="3498db" />;
};

export default Input;
```
- App.js
```js
<Button title="Hanbit" />
<Button title="React Native" />
<Input />
```
![img](img/결과3.png)

- 스타일드 컴포넌트의 attrs를 이용해서 props로 전달된 borderColor값에 따라 Input 컴포넌트의 디자인이 변경되도록 수정해보자.
```js
import React from 'react';
import styled from 'styled-components';

const StyledInput = styled.TextInput.attrs(props => ({
  placeholder: 'Enter a text...',
  placeholderTextColor: props.borderColor,
}))`
  width: 200px;
  height: 60px;
  margin: 5px;
  padding: 10px;
  border-radius: 10px;
  border: 2px;
  border-color: ${props => props.borderColor};
  font-size: 24px;
`;

const Input = props => {
  return <StyledInput borderColor={props.borderColor} />;
};

export default Input;
```
- 코드 수정이 완료되면 App 컴포넌트에서 Input 컴포넌트를 사용하면서 borderColor값을 전달하도록 수정하자

```js
<Button title="Hanbit" />
<Button title="React Native" />
<Input borderColor="#3498db" />
<Input borderColor="#9b59b6" />
```
- 이렇게 attrs를 이용하면 스타일을 설정하는 곳에서 props의 값에 따라 컴포넌트의 속성을 다르게 적용할 수도 있고 항상 일정한 속성을 미리 정의해놓을 수도 있다.
- 하지만 attrs를 이용하여 속성을 설정하는 것이 항상 좋은 것만은 아니다.
- 컴포넌트가 어떻게 사용되는가에 따라 attrs를 이용하지 않고 컴포넌트에 직접 속성을 전달하는 것이 코드를 이해하는 데 더 도움이 되는 경우도 있다.

### ThemeProvider
- ThemeProvider는 Context API를 활용해 어플리케이션 전체에서 스타일드 컴포넌트를 이용할 때 미리 정의한 값을 사용할 수 있도록 props로 전달한다.
- ThemeProvider를 이용하여 스타일을 정의할 때 미리 정의한 색을 사용해보자
- src에 Theme.js파일을 생성하고 Button 컴포넌트에서 사용했던 색을 정의해놓자
```js
export const theme = {
  purple: '#9b59b6',
  blue: '#3498db',
};
```
- 이제 모든 컴포넌트를 감싸는 최상위 컴포넌트로 ThemeProvider 컴포넌트를 사용하며, 앞에서 정의한 색을 ThemeProvider 컴포넌트의 theme 속성에 설정하자.
- 그러면 ThemeProvider 컴포넌트의 자식 컴포넌트에서는 스타일드 컴포넌트를 이용할 때 props로 theme을 전달받아 미리 정의된 색을 이용할 수 있다.

```js
import styled, { ThemeProvider } from 'styled-components';
import { theme } from './theme';
<ThemeProvider theme={theme}>
  <Container>
    <Button title="Hanbit" />
    <Button title="React Native" />
    <Input borderColor="#3498db" />
    <Input borderColor="#9b59b6" />
  </Container>
</ThemeProvider>

```
- 이제 Button 컴포넌트에서 스타일을 정의할 때 props로 전달되는 theme을 이용하여 수정해보자.
```js
background-color: ${props => props.title === 'Hanbit' ? props.theme.blue : props.theme.purple};
```
- 기존 화면과 동일하게 나오는 모습을 확인할 수 있다.
- 스타일드 컴포넌트를 사용할 때 ThemeProvider를 활용하여 theme를 지정하면, 하나의 파일에서 미리 정의해둔 색을 하위 컴포넌트에서 사용할 수 있다.
- 하나의 파일에서 모든 색을 관리하면 색의 사용이나 변경 등 유지보수에서 많은 이점을 얻을 수 있다.
- ThemeProvider를 이용하여 두 개의 색을 정의해두고 사용자의 선택에 따라 theme에 알맞은 값을 설정하는 것만으로 애플리케이션의 색 테마를 쉽게 변경할 수 있다.
```js
export const lightTheme = {
    background: '#ffffff',
    text: '#ffffff',
    purple: '#9b59b6',
    blue: '#3498db',
  };
  
  export const darkTheme = {
    background: '#34495e',
    text: '#34495e',
    purple: '#9b59b6',
    blue: '#3498db',
  };
```
- theme.js 파일에 테마에 따라 사용할 색을 정의했다.
- 이제 App 컴포넌트에서 테마를 변경할 수 있는 스위치를 추가하고, 테마에 따라 다른 색이 사용되도록 수정해보자
```js
import React, { useState } from 'react';
import { Switch } from 'react-native';
...
import { lightTheme, darkTheme } from './theme';

const Container = styled.View`
  flex: 1;
  background-color: ${props => props.theme.background};
  align-items: center;
  justify-content: center;
`;

const App = () => {
  const [isDark, setIsDark] = useState(false);
  const _toggleSwitch = () => setIsDark(!isDark);

  return (
    <ThemeProvider theme={isDark ? darkTheme : lightTheme}>
      <Container>
        <Switch value={isDark} onValueChange={_toggleSwitch} />
        <Button title="Hanbit" />
        <Button title="React Native" />
        <Input borderColor="#3498db" />
        <Input borderColor="#9b59b6" />
      </Container>
    </ThemeProvider>
  );
};

export default App;
```
- useState를 이용해 테마의 상태를 관리할 isDark와 상태를 변경할 setIsDark함수를 만들었다.
- 그리고 리액트 네이티브의 Switch 컴포넌트를 활용해 isDark의 상태를 변경할 수 있도록 화면을 구성했다.
- ThemeProvider 컴포넌트의 theme속성에는 isDark 상태에 따라 theme.js파일에 정의된 darkTheme또는 lightTheme이 적용되도록 수정되었고, App 컴포넌트에서 사용되는 Container컴포넌트의 스타일을 정의하는 곳에서 props로 전달된 theme을 이용하여 배경색을 설정했다.
- Button 컴포넌트에서도 theme의 변화에 따라 값이 잘 바뀌는지 확인하기 위해 Title 컴포넌트의 스타일을 다음과 같이 수정하자.
```js
const Title = styled.Text`
  font-size: 20px;
  font-weight: 600;
  color: ${props => props.theme.text};
`;
```