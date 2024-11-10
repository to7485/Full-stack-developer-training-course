# 채팅프로그램 만들기
- 지금까지 공부한 내용을 바탕으로 간단한 채팅 어플리케이션을 만들어보자.

## 구현할 기능 
- 로그인/회원가입 : 이메일과 비밀번호를 이용한 로그인과 회원가입
- 프로필 : 나의 정보 확인 및 변경
- 채널 생성 : 채널 생성 기능
- 채널 목록 : 생성된 채널들의 목록 조회
- 채널 : 실시간으로 메시지를 송수신하는 공간

## 프로젝트 생성하기
```js
expo init react-native-simple-chat
```

## 네비게이션
- 채팅 어플리케이션은 크게 세 부분으로 나눌것이다.
- 로그인 등 인증하는 화면
- 채팅방의 목록 등을 확인할 수 있는 화면
- 메시지를 주고받는 화면
- 화면은 유기적으로 연결되어 있으며 화면 간 이동이 잦다.

### 라이브러리 설치

#### @react-navigation/native
- 앱에서 화면간 네비게이션을 관리해줄 수있는 라이브러리
```
npm install @react-navigation/native@6.1.18
```
#### 주요기능
- NavigationContainer 제공
- 네비게이션 상태 관리
  - 앱의 현재 위치나 화면 전환과 같은 네비게이션 상태를 관리한다.
  - 이를 통해 사용자가 특정 화면에서 나가더라도 다시 돌아왔을 때 동일한 상태를 유지할 수 있게 하며, 히스토리 기반으로 백스택을 관리할 수 있다.
- 네비게이터와의 통합
  -  Stack, Tab, Drawer와 같은 네비게이터와 결합해 네비게이션 구조를 형성할 수 있다.

#### 기능관련 라이브러리 다운로드
```
expo install react-native-gesture-handler react-native-reanimated react-native-screens react-native-safe-area-context @react-native-community/masked-view
```

#### react-native-gesture-handler 
- 더 향상된 제스처 처리를 가능하게 해주는 라이브러리다.
- 기본적으로 React Native는 터치 이벤트를 제공하지만, 제스처를 복잡하게 사용할 때는 성능이나 일관성에서 제한이 있을 수 있다.
- 이 라이브러리는 그러한 한계를 극복하고 부드럽고 효율적인 제스처 인식을 제공한다.

#### 주요 기능
1. 복잡한 제스처 지원
     - 기본 제스처뿐 아니라 스와이프, 드래그, 핀치 줌 등 고급 제스처를 쉽게 인식하고 사용할 수 있다.
     - 여러 제스처를 동시에 인식하거나, 특정 제스처가 끝난 후 다른 제스처를 인식하는 방식으로 제스처 간의 우선순위와 조합을 설정할 수 있다.
2. 성능 개선
     - 네이티브에서 제스처를 처리하여 JS와 네이티브 간의 통신을 줄이기 때문에, React Native의 기본 터치 이벤트 시스템보다 부드럽고 빠르게 작동한다.
     - 네이티브에서 직접 제스처를 처리하므로, 스크롤 리스트나 드래그 앤 드롭과 같은 복잡한 UI에서도 성능이 뛰어나다.
3. react-navigation과의 통합
     - react-navigation과 완벽하게 호환되어 화면 전환, Drawer 네비게이션, 스택 네비게이션 등의 제스처 기반 네비게이션 동작을 구현하는 데 적합하다.
     - DrawerNavigation이나 StackNavigation에서 화면 전환을 제스처로 구현하는 경우, 이 라이브러리가 있어야 원활한 사용이 가능하다.

#### eact-native-screens
- 화면 전환 성능을 최적화하기 위한 라이브러리다. 
- 이 라이브러리는 iOS와 Android의 네이티브 화면 관리 기능을 활용하여 화면 간 전환을 더 부드럽게 하고, 메모리 사용을 줄여 성능을 향상시킨다. 
- 특히 `react-navigation`과 함께 사용할 때 효과적이다.

#### 주요 기능
1. **네이티브 스크린 관리**
   - `react-native-screens`는 네이티브 화면 관리 기능을 사용해 각 화면의 라이프사이클을 더 효과적으로 관리한다.
   - 각 화면이 메모리에 완전히 남아있지 않고, 비활성화되거나 숨겨진 화면은 메모리에서 제거하여 앱의 메모리 사용량을 줄인다.

2. **react-navigation과의 통합**
   - `react-native-screens`는 `react-navigation`의 Stack Navigator와 함께 사용할 때 성능 향상 효과가 크다.
   - Stack Navigator의 화면 전환이 네이티브 방식으로 처리되어, 화면 간 전환이 부드럽고 빠르게 동작한다.

3. **메모리 사용 최적화**
   - `react-native-screens`는 비활성 상태의 화면을 메모리에서 제거하거나, 네이티브 레벨에서 관리하여 전체적인 메모리 사용량을 줄인다.
   - 이를 통해 더 복잡한 네비게이션 구조에서도 성능 저하 없이 화면을 전환할 수 있다.

#### @react-native-community/masked-view
- 특정 영역을 가리거나 마스크 효과를 줄 때 사용하는 라이브러리다. 
- 이 라이브러리는 주로 화면 전환 애니메이션에서 화면이 겹쳐 보이지 않도록 마스크 처리를 하거나 특정 부분만 보이게 할 때 활용된다.

#### 주요 기능
1. **화면 마스킹**
   - 화면의 특정 영역만 보이도록 제한하여, 원하는 부분에만 마스크 효과를 줄 수 있다.
   - 예를 들어, 둥근 모서리를 가진 이미지나 특정 영역만 표시되는 UI를 구현할 때 유용하다.

2. **react-navigation과의 통합**
   - `@react-native-community/masked-view`는 `react-navigation`의 Stack Navigator와 함께 자주 사용된다.
   - Stack Navigator의 화면 전환 애니메이션을 사용할 때, 이전 화면이 겹쳐 보이지 않도록 마스킹 효과를 적용하여 깔끔한 화면 전환을 구현할 수 있다.

### 바텀탭바 라이브러리 설치
```
npm install @react-navigation/bottom-tabs@6.5.20
```

### styled components와 props-types 설치
```js
npm install styled-components prop-types
```
#### prop-types
- `prop-types`는 React 컴포넌트에서 전달받는 `props`의 타입을 검증해주는 라이브러리다. 
- 컴포넌트에 전달되는 `props`의 타입과 값이 예상한 형태인지 확인할 수 있으며, 개발 중 잘못된 `props`가 전달될 경우 경고 메시지를 출력해 디버깅에 도움을 준다.

#### 주요기능
1. **타입 검증**
   - `prop-types`를 사용하여 `props`의 데이터 타입을 미리 정의할 수 있다. 
   - 잘못된 타입의 `props`가 전달되면 콘솔에 경고 메시지가 출력된다.
   
2. **기본값 설정**
   - 컴포넌트에 `defaultProps`를 설정해 `props`가 전달되지 않았을 때 기본값을 사용할 수 있다.

3. **유연한 타입 설정**
   - 다양한 데이터 타입을 검증할 수 있으며, 특정 조건을 만족하는 타입도 정의할 수 있다. `number`, `string`, `array`, `object` 등 다양한 타입 검증을 지원한다.

### 추가적인 라이브러리
- 위의 라이브러리 외에도 프로젝트를 진행하면서 다음과 같은 라이브러리를 사용할 예정이다.
- 추가적인 라이브러리는 사용되는 곳을 명확하게 알기 위해 필요한 상황이 오면 설치하고 사용하자.
- expo-image-picker
  - 기기의 사진이나 영상을 가져올 수 있도록 시스템 UI에 접근할 수 있는 기능을 제공한다.
  - 이번 프로젝트에서 기기의 사진을 선택해 사용자의 사진을 설정 혹은 변경하기 위해 사용할 예정이다.
- moment
  - 시간을 다양한 형태로 변경하는 등 시간과 관련된 많은 기능을 제공하는 라이브러리로, 날짜와 관련된 라이브러리 중 가장 널리 알려져 있고 많이 사용되고 있다.
  - 여기서는 타밍스탬프를 사용자가 보기 편한 형태로 변경하기 위해 사용할 예정이다.
- react-native-keyboard-aware-scroll-view
  - 키보드가 화면을 가리면서 생기는 불편한 점을 해결하기 위해 사용되는 라이브러리이다.
- react-native-gifted-chat
  - 메시지를 주고받는 채팅 화면을 쉽게 구현할 수 있도록 돕는 라이브러리이다.

### 프로젝트 파일 구조
- 모든 소스 파일을 관리할 src폴더를 생성한 후 theme.js파일을 생성하고 다음과 같이 작성하자.
```js
const colors = {
    white : '#ffffff',
    black : '#000000',
    grey_0 : '#d5d5d5',
    grey_1 : '#a6a6a6',
    red : '#e84118',
    blue : '#3679fe',
};

export const theme = {
    background : colors.white,
    text : colors.black,
}
```
- 공통으로 사용할 색을 적의하고 배경색과 글자의 색을 미리 정했다.
- 이번에는 최상위 컴포넌트가 사용될 App 컴포넌트를 src폴더 안에 작성해보자.
```js
import React from 'react'
import {StatusBar} from 'react-native'
import {ThemeProvider} from 'styled-components'
import {theme} from './theme'

const App = () => {
    return(
        <ThemeProvider theme={theme}>
            <StatusBar barStyle='dark-content' />
        </ThemeProvider>
    )
}

export default App;
```
- 스타일드 컴포넌트의 ThemeProvider 컴포넌트를 사용해 스타일드 컴포넌트에서 정의된 theme을 사용할 수 있도록 작성했다.
- 이번에는 루트 디렉터리에 있는 App.js파일을 수정해서 우리가 만든 App 컴포넌트가 메인 파일이 되도록 수정해보자.
```js
import App from "./src/App";

export default App;
```

#### 그 외 폴더
- src폴더 밑에 각 역할에 맞는 파일을 관리할 폴더를 다음과 같이 생성하자
- components : 컴포넌트 파일 관리
- contexts : Context API 파일 관리
- navigations : 네비게이션 파일 관리
- screens : 화면 파일 관리
- utils : 프로젝트에서 이용할 기타 기능 관리