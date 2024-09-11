# 프론트엔드개발
- 사용자의 바로 앞에서 사용자와 상호작용하며 애플리케이션 로직을 수행하고 백엔드 서버로 요청을 전달하는 역할을 한다.
- 웹 서비스에서 클라이언트 또는 프론트엔드란 웹 브라우저를 뜻한다.
- 사용자는 자신의 컴퓨터로 브라우저를 실행하고, 브라우저는 인터넷을 이용해 서버에 있는 자원(HTML,JS,CSS)을 사용자의 컴퓨터로 다운로드 후, 브라우저에서 실행시킨다.

## 프론트엔드 개발 환경 설정
### 학습 내용
- 브라우저의 작동 원리
- Node.js
- SPA와 React.js

### 실습 내용
- 브라우저의 개발자 툴
- 프론트엔드 개발 환경 설정(VS Code)
- Node.js 설치
- Npm 실습
- 리액트 애플리케이션 생성 및 실행

## Node.js와 NPM 설치
### Node.js
- Node.js 전까지 자바스크립트는 브라우저 내에서만 실행이 가능했다.
- 자바스크립트를 실행하기 위해서는 브라우저상에서 HTML 렌더링의 일부로 실행하거나, 개발자 창의 자바스크립트 콘솔을 이용해 실행해야 했다.
- Node.js는 자바스크립트를 내 컴퓨터에서 실행할 수 있게 해주는 프로그램이다.

### 자바스크립트를 브라우저 밖에서 사용함으로서 얻는점
- 자바스크립트를 클라이언트 언어뿐만 아니라 서버 언어로도 사용할 수 있다는 뜻이다.
- 우리는 이 자바스크립트로 된 node 서버를 이용해 프론트엔드 서버를 개발한다.
- 우리의 프론트엔드 서버는 요청이 왔을 때, HTML,JS,CSS를 리턴한다.

### NPM(Node Package Manager)
- npm은 nodejs의 패키지 관리 시스템이다.
- 우리는 npm을 이용해 npmjs(https://www.npmjs.com)에서 node.js라이브러리를 설치한다.
- npm은 nodejs를 설치하면 함께 설치된다.
- https://nodejs.org/en/에서 nodejs를 다운로드 후 설치한다.
- 이 책에서 16.14.2 LTS를 다운로드 하여 사용한다.
- 되도록이면 같은 버전을 설치하는 것을 추천한다.

### npm version
- 설치 후 커맨트라인에서 npm version 명령어로 버전 정보를 확인한다.
- 각 버전 정보는 Node.js 버전에 따라 다를 수 있다.
```js
C:\Users\lis74>npm version
{
  npm: '10.5.0',
  node: '20.12.2',
  acorn: '8.11.3',
  ada: '2.7.6',
  ares: '1.27.0',
  base64: '0.5.2',
  brotli: '1.1.0',
  cjs_module_lexer: '1.2.2',
  cldr: '44.1',
  icu: '74.2',
  llhttp: '8.1.2',
  modules: '115',
  napi: '9',
  nghttp2: '1.60.0',
  nghttp3: '0.7.0',
  ngtcp2: '0.8.1',
  openssl: '3.0.13+quic',
  simdutf: '4.0.8',
  tz: '2024a',
  undici: '5.28.4',
  unicode: '15.1',
  uv: '1.46.0',
  uvwasi: '0.0.20',
  v8: '11.3.244.8-node.19',
  zlib: '1.3.0.1-motley-40e35a7'
}
```

### 프로젝트 초기화하기
- Node.js 프로젝트를 초기화 하기 위해서는 npm init을 사용한다.
- 우리는 npm이 아닌 npx라는 툴로 리액트 애플리케이션을 초기화 할것이다.
- npm으로 설치를 하면 설정을 해줘야 할 부분이 많다.

```js
leehj4206@DESKTOP-QBTAA2C MINGW64 /d/develop
$ mkdir test-project

leehj4206@DESKTOP-QBTAA2C MINGW64 /d/develop
$ cd test-project

leehj4206@DESKTOP-QBTAA2C MINGW64 /d/develop/test-project
$ npm init
This utility will walk you through creating a package.json file.
It only covers the most common items, and tries to guess sensible defaults.

See `npm help init` for definitive documentation on these fields
and exactly what they do.

Use `npm install <pkg>` afterwards to install a package and
save it as a dependency in the package.json file.

Press ^C at any time to quit.
package name: (test-project) //프로젝트 이름
version: (1.0.0) //프로젝트 버전
description: test-project //프로젝트 설명
entry point: (index.js) //시작파일
test command:
git repository:
keywords:
author:
license: (ISC)
About to write to D:\develop\test-project\package.json:

{
  "name": "test-project",
  "version": "1.0.0",
  "description": "test-project",
  "main": "index.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "author": "",
  "license": "ISC"
}


Is this OK? (yes) yes
```
- Node 프로젝트를 초기화하면 패키지 이름이나, 버전 등 기본적인 정보를 입력해야 한다.
- 모든 정보를 입력하면 마지막에 package.json이라는 파일을 만들어준다.
- package.json에 프로젝트의 메타데이터가 들어간다.

### npm install react
- npm을 이용하여 react를 설치한다.
```js
npm install react
```
- 그러면 해당 패키지는 node_modules 디렉토리 아래에 인스톨된다.
- package.json의 dependencies에 추가된 라이브러리는 이후 프로덕션의 배포에 사용된다.

### 비주얼 스튜디오 코드 설치
- 비주얼 스튜디오 코드를 자바스크립트 IDE로 사용한다.
- https://code.visualstudio.com/download에서 다운로드 받는다.

### 프론트엔드 애플리케이션 생성
- 원하는 디렉토리에 워크스페이스 디렉토리를 생성한다.

```js
mkdir react-workspace
```
- 생성한 디렉토리로 이동한다.
```js
cd react-workspace
```
- npx를 이용하여 리액트앱 생성하기
```js
npx create-react-app todo-react-app
```
- 오류 발생시 아래의 코드를 작성하고 다시 시도해보자
```js
npm uninstall -g create-react-app
npm install -g create-react-app
```