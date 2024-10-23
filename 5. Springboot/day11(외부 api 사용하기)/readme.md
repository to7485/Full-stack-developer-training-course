# 외부 api 사용해보기
- 다양한 종류의 api를 사용해보자.
- api-react-app 만들기
- react-router-dom 설치하기
- src에 api 폴더 만들기

## App.js에 코드 작성하기
```js
import './App.css';
import { Routes, Route, BrowserRouter } from 'react-router-dom';
import Address from './api/Address'
import MultipleButtons from './MultipleButtons';

function App() {
  
  return (
    <div className='App'>
      <BrowserRouter>
        <Routes>
          <Route path="/" element={<MultipleButtons />} />
          <Route path="/address" element={<Address />} />
          <Route path="/about" element={<MultipleButtons />} />
          <Route path="/address" element={<MultipleButtons />} />
        </Routes>
      </BrowserRouter>
    </div>
  );
}
export default App;
```

## MultiButtons.js파일 만들기
```js
import { useNavigate } from 'react-router-dom';

function MultipleButtons() {
  const navigate = useNavigate();

  // 하나의 핸들러에서 버튼 구분하기
  const handleButtonClick = (event) => {
    const buttonId = event.target.id; // 버튼의 id 값으로 구분

    switch (buttonId) {
      case 'address':
        navigate('/address');
        break;
      case 'about':
        navigate('/about'); // about 페이지로 이동
        break;
      case 'contact':
        navigate('/contact'); // contact 페이지로 이동
        break;
      default:
        console.log('알 수 없는 버튼 클릭');
    }
  };

  return (
    <div>
      <button id="address" onClick={handleButtonClick}>
        주소찾기 api
      </button>
      <button id="about" onClick={handleButtonClick}>
        About
      </button>
      <button id="contact" onClick={handleButtonClick}>
        Contact
      </button>
    </div>
  );
}

export default MultipleButtons;
```

## 1. 주소 api 사용하기
### 공식 DAUM 주소 API 사용설명서
- https://postcode.map.daum.net/guide

### DAUM 주소 API 활용 특징
- API 키를 발급받을 필요가 없다.
- 사용량에 대한 제한이 없다.
- 기업용이든 상업적 용도이든 상관없이 무료로 사용 가능하다.
- 기초구역번호가 발급된 도로명 주소, 영문 주소를 확인할 수 있다.
- 행정안전부에서 제공하는 "도로명 주소"DB를 직업 업데이트 받고 있으므로 가장 최신의 데이터를 이용할 수 있다.

### 공식문서 사용 예시
```JS
<script src="//t1.daumcdn.net/mapjsapi/bundle/postcode/prod/postcode.v2.js"></script>
<script>
    new daum.Postcode({
        oncomplete: function(data) {
            // 팝업에서 검색결과 항목을 클릭했을때 실행할 코드를 작성하는 부분입니다.
            // 예제를 참고하여 다양한 활용법을 확인해 보세요.
        }
    }).open();
</script>
```

### 패키지 설치하기
- 우리는 REACT에서 사용을 할 것이므로 패키지를 설치한다.
- Daum 우편번호 검색 서비스를 React 환경에서 간편하게 이용할 수 있습니다.
```JS
npm install react-daum-postcode
```
※ 주의사항
- react-daum-postcode는 Daum 우편번호 서비스와 독립적으로 제작된 패키지다.

### 주요 속성
### oncomplete
- 우편번호 검색 결과 목록에서 특정 항목을 클릭한 경우, 해당 정보를 받아서 처리할 콜백 함수를 정의하는 부분이다.
- null값 또는 정의하지 않을 시에 검색은 가능하지만, 결과 항목을 클릭하면 아무 일도 일어나지 않는다.

```js
 oncomplete: function(data) {
        //data는 사용자가 선택한 주소 정보를 담고 있는 객체이며, 상세 설명은 아래 목록에서 확인하실 수 있습니다.
    }
```

#### 항목
| 항목                      | 설명                                                                                                                                                                                      |
| ------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `zonecode`                | 국가기초구역번호. 2015년 8월 1일부터 시행될 새 우편번호.                                                                                                                                  |
| `address`                 | 기본 주소 (검색 결과에서 첫줄에 나오는 주소, 검색어의 타입(지번/도로명)에 따라 달라진다.)                                                                                                 |
| `addressEnglish`          | 기본 영문 주소                                                                                                                                                                            |
| `addressType`             | 검색된 기본 주소 타입: R(도로명), J(지번)                                                                                                                                                 |
| `userSelectedType`        | 검색 결과에서 사용자가 선택한 주소의 타입                                                                                                                                                 |
| `noSelected`              | 연관 주소에서 "선택 안함" 부분을 선택했을때를 구분할 수 있는 상태변수                                                                                                                     |
| `userLanguageType`        | 검색 결과에서 사용자가 선택한 주소의 언어 타입: K(한글주소), E(영문주소)                                                                                                                  |
| `roadAddress`             | 영문 도로명 주소                                                                                                                                                                          |
| `jibunAddress`            | 지번 주소                                                                                                                                                                                 |
| `jibunAddressEnglish`     | 영문 지번 주소                                                                                                                                                                            |
| `autoRoadAddress`         | '지번주소'에 매핑된 '도로명주소'가 여러개인 경우, 사용자가 '선택안함' 또는 '지번주소'를 클릭했을 때 연관된 도로명 주소 중 임의로 첫번째 매핑 주소를 넣어서 반환합니다.                    |
| `autoRoadAddressEnglish`  | autoRoadAddress의 영문 도로명 주소                                                                                                                                                        |
| `autoJibunAddress`        | '도로명주소'에 매핑된 '지번주소'가 여러 개인 경우, 사용자가 '선택안함' 또는 '도로명주소'를 클릭했을 때 첫 번째 매핑 주소가 반환됨. (autoMapping을 false로 설정한 경우 값이 채워지지 않음) |
| `autoJibunAddressEnglish` | `autoJibunAddress`의 영문 지번 주소                                                                                                                                                       |
| `buildingCode`            | 건물관리번호                                                                                                                                                                              |
| `buildingName`            | 건물명                                                                                                                                                                                    |
| `apartment`               | 공동주택 여부 (아파트, 연립주택, 다세대주택 등)                                                                                                                                           |
| `sido`                    | 도/시 이름                                                                                                                                                                                |
| `sidoEnglish`             | 도/시 이름의 영문                                                                                                                                                                         |
| `sigungu`                 | 시/군/구 이름                                                                                                                                                                             |
| `sigunguEnglish`          | 시/군/구 이름의 영문                                                                                                                                                                      |
| `sigunguCode`             | 시/군/구 코드 (5자리 구성된 시/군/구 코드)                                                                                                                                                |
| `roadnameCode`            | 도로명 코드, 7자리로 구성된 도로명 코드. 추후 7자리 이상으로 늘어날 수 있음.                                                                                                              |
| `bcode`                   | 법정동/법정리 코드                                                                                                                                                                        |
| `roadname`                | 도로명 값, 검색 결과 중 선택한 도로명주소의 "도로명" 값이 들어감 (건물번호 제외)                                                                                                          |
| `roadnameEnglish`         | 도로명 값, 검색 결과 중 선택한 도로명의 "영문" 값이 들어감 (건물번호 제외)                                                                                                                |
| `bname`                   | 법정동/법정리 이름                                                                                                                                                                        |
| `bnameEnglish`            | 법정동/법정리 이름의 영문                                                                                                                                                                 |
| `bname1`                  | 법정리의 읍/면 이름 ("동" 지역일 경우에는 공백, "리" 지역일 경우에는 "읍" 또는 "면" 정보가 들어감)                                                                                        |
| `bname1English`           | 법정리의 읍/면 이름의 영문 ("동" 지역일 경우에는 공백, "리" 지역일 경우에는 "읍" 또는 "면" 정보가 들어감)                                                                                 |
| `bname2`                  | 법정동/법정리 이름                                                                                                                                                                        |
| `bname2English`           | 법정동/법정리 이름의 영문                                                                                                                                                                 |
| `hname`                   | 행정동 이름, 검색어를 행정동으로 검색하고, 검색결과의 법정동과 검색어에 입력한 행정동이 다른 경우에 표시됨.                                                                               |
| `query`                   | 사용자가 입력한 검색어                                                                                                                                                                    |
| `postcode`                | 구 우편번호 (2020년 3월 9일 이후로는 데이터가 내려가지 않음)                                                                                                                              |
| `postcode1`               | 구 우편번호 앞 3자리 (2020년 3월 9일 이후로는 데이터가 내려가지 않음)                                                                                                                     |
| `postcode2`               | 구 우편번호 뒤 3자리 (2020년 3월 9일 이후로는 데이터가 내려가지 않음)                                                                                                                     |
| `postcodeSeq`             | 구 우편번호 일련번호 (2020년 3월 9일 이후로는 데이터가 내려가지 않음)                                                                                                                     |

### onclose
- 우편번호 찾기 화면을 팝업으로 띄운 후, 검색 결과를 선택하거나, 브라우저의 닫기버튼을 통해 닫았을 때 발생하는 콜백 함수를 정의하는 부분이다.
- 검색결과를 선택한 경우에는 onComplete콜백함수가 완료된 후에 실행되게 된다.

```js
    onclose: function(state) {
        //state는 우편번호 찾기 화면이 어떻게 닫혔는지에 대한 상태 변수 이며, 상세 설명은 아래 목록에서 확인하실 수 있습니다.
        if(state === 'FORCE_CLOSE'){
            //사용자가 브라우저 닫기 버튼을 통해 팝업창을 닫았을 경우, 실행될 코드를 작성하는 부분입니다.

        } else if(state === 'COMPLETE_CLOSE'){
            //사용자가 검색결과를 선택하여 팝업창이 닫혔을 경우, 실행될 코드를 작성하는 부분입니다.
            //oncomplete 콜백 함수가 실행 완료된 후에 실행됩니다.
        }
    }
```

#### 항목
<table border="1">
  <tr>
    <th>항목</th>
    <th>값</th>
    <th>설명</th>
  </tr>
  <tr>
    <td rowspan="2">state</td>
    <td>FORCE_CLOSE</td>
    <td>브라우저의 닫기 버튼을 통해 화면이 닫혔을 경우 (레이어 모드에서는 발생하지 않음).</td>
  </tr>
  <tr>
    <td>COMPLETE_CLOSE</td>
    <td>검색결과를 선택하여 화면이 닫혔을 경우 (팝업/레이어 모드의 기본 동작).</td>
  </tr>
</table>


### AddressFinder.js 만들기
```js
import React, { useState, useEffect } from 'react';
import {useDaumPostcodePopup} from 'react-daum-postcode';
import '../address.css'

const PostcodeComponent = () => {
  const [postcode, setPostcode] = useState(''); // 우편번호를 저장할 state
  const [address, setAddress] = useState(''); // 주소를 저장할 state
  const [detailAddress, setDetailAddress] = useState(''); // 상세주소를 저장할 state
  const [extraAddress, setExtraAddress] = useState(''); // 참고항목을 저장할 state

    // Daum 우편번호 API 스크립트 URL
    let scriptUrl = 'https://t1.daumcdn.net/mapjsapi/bundle/postcode/prod/postcode.v2.js'

    // react-daum-postcode의 useDaumPostcodePopup 훅을 사용하여 API를 팝업으로 실행할 준비
    const open = useDaumPostcodePopup(scriptUrl);

  
    // Daum Postcode API에서 주소 선택 완료 후 실행되는 함수
    const handleComplete = (data) => {
        let addr = ''; // 주소 변수
        let extraAddr = ''; // 참고항목 변수

        // 사용자가 선택한 주소 타입에 따라 주소 설정
        // 도로명 주소(R) 또는 지번 주소(J)를 선택했는지 확인

        if (data.userSelectedType === 'R') {
            addr = data.roadAddress; // 도로명 주소 선택 시 도로명 주소 할당
        } else {
            addr = data.jibunAddress; // 지번 주소 선택 시 지번 주소 할당
        }

        // 참고항목 처리 (도로명 주소인 경우)
        if (data.userSelectedType === 'R') {
            // 법정동명이 있는지 확인하고 추가 (법정동, 법정리가 있을 때만)
            if (data.bname !== '' && /[동|로|가]$/g.test(data.bname)) {
            extraAddr += data.bname;
            }
            // 건물명이 있고 공동주택일 경우 추가
            if (data.buildingName !== '' && data.apartment === 'Y') {
            extraAddr += extraAddr !== '' ? ', ' + data.buildingName : data.buildingName;
            }
            // 참고항목이 있다면 괄호로 감싸서 추가
            if (extraAddr !== '') {
            extraAddr = ` (${extraAddr})`;
            }
            // 참고항목 state 업데이트
            setExtraAddress(extraAddr);
        } else {
            // 지번 주소인 경우 참고항목을 빈 문자열로 설정
            setExtraAddress('');
        }

        setPostcode(data.zonecode); // 우편번호 설정
        setAddress(addr);// 주소 설정

        // 상세주소 입력 필드로 포커스를 이동
        document.getElementById('sample6_detailAddress').focus();
        }

        // 팝업을 열고 완료 시 handleComplete 함수 실행
        const handleClick = () => {
        open({ onComplete: handleComplete });
        };

  return (
    <div className="form-group">
    <div className="form-row">
      <input
        type="text"
        id="sample6_postcode"
        placeholder="우편번호"
        value={postcode}
        readOnly
      />
      <input
        type="button"
        onClick={handleClick}
        value="우편번호 찾기"
      />
      </div>
      <input
        type="text"
        id="sample6_address"
        placeholder="주소"
        value={address}
        readOnly
      />
      <div className="form-row split">
      <input
        type="text"
        id="sample6_detailAddress"
        placeholder="상세주소"
        value={detailAddress}
        onChange={(e) => setDetailAddress(e.target.value)}
      />
      <input
        type="text"
        id="sample6_extraAddress"
        placeholder="참고항목"
        value={extraAddress}
        readOnly
      />
    </div>
    </div>
  );
};

export default PostcodeComponent;
```

## 2. 네이버 검색 api
- 네이버 개발자 센터로 이동한다.
- 다양한 api를 제공하는데 도서를 검색하는 api를 사용해보자.

![img](img/어플등록.png)

- API를 사용하기 위헤 어플리케이션을 등록한다.

![img](img/이용신청.png)

- Client ID와 Client Secret을 발급받는다.
- 어딘가에 잘 복사해놓자.
![img](img/키.png)


### 요청 URL
|요청 URL|결과값 반환 형식|
|https://openapi.naver.com/v1/search/book.xml|XML|
|https://openapi.naver.com/v1/search/book.json|JSON|

### 프로토콜
- HTTPS

### HTTP메서드
- GET

### 파라미터
- 파라미터를 쿼리스트링 형식으로 전달한다.

<table border="1" cellspacing="0" cellpadding="10">
  <tr>
    <th>파라미터</th>
    <th>타입</th>
    <th>필수 여부</th>
    <th>설명</th>
  </tr>
  <tr>
    <td>query</td>
    <td>String</td>
    <td>Y</td>
    <td>검색어. UTF-8로 인코딩되어야 합니다.</td>
  </tr>
  <tr>
    <td>display</td>
    <td>Integer</td>
    <td>N</td>
    <td>한 번에 표시할 검색 결과 개수 (기본값: 10, 최댓값: 100)</td>
  </tr>
  <tr>
    <td>start</td>
    <td>Integer</td>
    <td>N</td>
    <td>검색 시작 위치 (기본값: 1, 최댓값: 1000)</td>
  </tr>
  <tr>
    <td rowspan="2">sort</td>
    <td rowspan="2">String</td>
    <td rowspan="2">N</td>
    <td>- sim: 정확도순으로 내림차순 정렬 (기본값)</td>
  </tr>
  <tr>
    <td>- date: 출간일순으로 내림차순 정렬</td>
  </tr>
</table>

### 참고사항
- API를 요청할 때 다음 예와 같이 HTTP 요청 헤더에 클라이언트 아이디와 클라이언트 시크릿을 추가해야 한다.
```
GET /v1/search/book.xml?query=%EC%A3%BC%EC%8B%9D&display=10&start=1 HTTP/1.1
Host: openapi.naver.com
User-Agent: curl/7.49.1
Accept: */*
X-Naver-Client-Id: {애플리케이션 등록 시 발급받은 클라이언트 아이디 값}
X-Naver-Client-Secret: {애플리케이션 등록 시 발급받은 클라이언트 시크릿 값}
```

### 응답
- 응답에 성공하면 XML 또는 JSON 형식으로 반환한다.

| 항목                   | 타입     | 설명                                                   |
|------------------------|----------|--------------------------------------------------------|
| `lastBuildDate` | dateTime | 검색 결과를 생성한 시간                                   |
| `total`        | Integer  | 총 검색 결과 개수                                        |
| `start`        | Integer  | 검색 시작 위치                                           |
| `display`      | Integer  | 한 번에 표시할 검색 결과 개수                             |
| `title`   | String   | 책 제목                                                  |
| `link`    | String   | 네이버 도서 정보 URL                                      |
| `image`   | String   | 섬네일 이미지의 URL                                       |
| `author`  | String   | 저자 이름                                                |
| `discount`| Integer  | 판매 가격. 절판 등의 이유로 가격이 없으면 값을 반환하지 않음  |
| `publisher`| String  | 출판사                                                   |
| `isbn`    | Integer  | ISBN                                                    |
| `description`| String| 네이버 도서의 책 소개                                    |
| `pubdate` | dateTime | 출간일     