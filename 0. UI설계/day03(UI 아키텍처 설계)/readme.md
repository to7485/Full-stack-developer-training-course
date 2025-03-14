# UI 아키텍처 설계
- 이때 UI/UX 아키텍처 설계는 사용자가 편리하게 인터페이스를 사용할 수 있도록 구조를 설계하는 과정을 의미한다.

## :one: UI/UX 아키텍처 설계의 중요성
✅ 왜 UI/UX 아키텍처 설계가 필요할까?   
웹사이트나 앱을 개발할 때, 단순히 예쁜 디자인만 중요한 것이 아니다.   
사용자가 쉽게 탐색하고 원하는 정보를 빠르게 찾을 수 있도록 체계적인 설계가 필요하다.

💡 UI/UX 아키텍처 설계를 잘하면?   
✔ 사용자가 편리하게 웹사이트/앱을 사용할 수 있음   
✔ 불필요한 클릭을 줄이고, 원하는 정보를 쉽게 찾을 수 있음   
✔ 사용자 만족도가 높아지고, 이탈률(사이트를 떠나는 비율)이 낮아짐

📌 예를 들어 보자!

쇼핑몰에서 결제하기 버튼을 찾기 어렵다면? 🛑 UX 설계 실패!   
검색창이 너무 작아서 잘 보이지 않는다면? 🔴 UI 설계 실패!   
메뉴가 복잡해서 원하는 페이지를 찾기 어렵다면? 🟠 UI/UX 아키텍처 설계 부족!   
따라서, UI/UX 아키텍처 설계를 철저히 해야 사용자가 웹사이트를 쉽게 탐색하고 좋은 경험을 가질 수 있다. 🚀   

## :two: UI/UX 아키텍처 설계의 핵심 요소
UI/UX 아키텍처 설계를 할 때 고려해야 할 핵심 요소가 있다.

🔹 1. 정보 아키텍처 (Information Architecture, IA)   
웹사이트나 앱에서 정보를 체계적으로 정리하고, 사용자가 쉽게 찾을 수 있도록 구성하는 과정이다.   

✅ 정보 아키텍처의 주요 요소   

- 내비게이션(Navigation): 사용자가 원하는 페이지로 쉽게 이동할 수 있도록 설계   
- 카테고리 구조: 정보를 계층적으로 정리 (예: 쇼핑몰의 '의류 > 남성 > 상의' 구조)   
- 검색 기능: 사용자가 키워드를 입력하면 원하는 정보를 쉽게 찾을 수 있도록 설계
- 콘텐츠 매핑(Content Mapping)   
   - 사용자가 콘텐츠를 어떻게 탐색하고 연결할지 내비게이션 설계 및 사이트맵을 만드는 과정에서 활용된다.
   - 사용자 경험 중심으로 콘텐츠를 배치하는 과정이라 UX 구조 설계와도 밀접한 관련이 있다.<br>
- 콘텐츠 모델(Content Model)
   - 콘텐츠의 데이터 구조와 속성을 정의하는 작업이기 때문에 정보 아키텍처(IA) 및 데이터 모델링에 포함된다.
   - 개발과 UX 설계를 연결하는 중요한 역할을 한다.

🔹 2.레이블링 (Labeling)이란?   
레이블링(Labeling)은 정보를 쉽게 이해하고 찾을 수 있도록 명확한 이름(레이블, Label)을 붙이는 과정을 말한다.   
사용자가 웹사이트나 앱에서 길을 잃지 않고 원하는 정보를 쉽게 찾을 수 있도록 도와주는 역할을 한다.

✅ 레이블링을 적용하는 주요 요소

| 적용 요소 | 설명 | 예시 |
|----------|-----|------|
| **네비게이션 메뉴** | 웹사이트의 주요 카테고리 및 메뉴 이름 | "홈, 제품 소개, 고객센터" |
| **버튼(Label Button)** | 버튼이 수행하는 기능을 나타내는 이름 | "로그인, 회원가입, 다음 단계" |
| **입력 필드 (Input Field)** | 입력해야 할 정보를 명확하게 설명 | "이메일 주소 입력, 비밀번호 입력" |
| **링크(Link Text)** | 사용자가 클릭할 링크에 대한 설명 | "자세히 보기, 주문 내역 확인" |

✅ 좋은 레이블링을 위한 가이드라인  

**1. 명확하고 직관적인 단어 사용**  
- "확인" 대신 "결제 완료"  
- "정보" 대신 "계정 정보"  

**2. 일관성 유지**  
- 같은 기능은 항상 같은 이름으로 유지 (예: "장바구니" vs "쇼핑카트" 같은 혼란 방지)  

**3. 너무 길거나 짧지 않게 작성**  
- "더 보기" → **짧아서 의미가 모호함** ❌  
- "더 많은 제품 보기" → **구체적인 설명으로 이해하기 쉬움**

**4. 사용자 입장에서 생각하기**  
- 개발자가 아니라 사용자가 쉽게 이해할 수 있는 단어 사용 


🔹 3. 와이어프레임 (Wireframe) & 프로토타입 (Prototype)   
UI/UX 아키텍처를 설계할 때는 먼저 화면의 기본 구조를 그려보는 과정이 필요하다.   
이때 사용하는 것이 **와이어프레임(Wireframe)과 프로토타입(Prototype)**이다.

✅ 와이어프레임 (Wireframe)

와이어프레임은 웹사이트나 앱의 화면 설계를 단순한 개요 형태로 표현한 것이다.   
✔ 종이에 손으로 그리거나, Figma, Adobe XD, Balsamiq 같은 도구로 제작   
✔ 버튼, 입력 창, 메뉴 등의 배치를 설계

✅ 프로토타입 (Prototype)

프로토타입은 와이어프레임을 실제로 작동하는 것처럼 구현한 것   
✔ 사용자가 실제로 클릭해보면서 테스트할 수 있음

📢 쉽게 말해!

와이어프레임 → 화면의 기본 틀을 그린 스케치   
프로토타입 → 실제로 작동하는 샘플

🔹 4. 사용자 플로우 (User Flow) & 사용자 여정 맵 (User Journey Map)   
**사용자 플로우(User Flow)**는 사용자가 특정 목표(예: 회원가입, 결제 등)를 달성하기 위해 어떤 경로를 거치는지를 정리하는 과정이다.   

✅ 사용자 플로우를 만들 때 고려할 요소

사용자가 어디서 시작하는가? (홈페이지? 광고 클릭?)   
사용자가 목표를 달성하기까지 몇 단계가 필요한가?   
어떤 단계에서 사용자가 어려움을 겪을 수 있는가?   
📌 예시: 온라인 쇼핑몰에서 구매까지의 사용자 플로우   
1️⃣ 사용자가 홈페이지 방문   
2️⃣ 상품 검색   
3️⃣ 상품 상세 페이지 확인   
4️⃣ 장바구니 추가   
5️⃣ 결제 진행   
6️⃣ 주문 완료   

✔ 사용자 플로우를 잘 설계하면, 사용자가 원하는 정보를 쉽게 찾고 목표를 달성하는 과정이 더 쉬워진다!

## :three: 정보 레이블링 설계란?  

**정보 레이블링(Information Labeling) 설계**는 데이터를 사용자가 쉽게 찾을 수 있도록 체계적으로 정리하는 과정이다.  
웹사이트나 애플리케이션에서 메뉴, 버튼, 링크 등의 구조를 설계할 때 중요한 역할을 한다.  

📢 **쉽게 말해!**  
> "정보를 체계적으로 분류해서 사용자들이 원하는 데이터를 쉽게 찾을 수 있도록 돕는 과정!"

### 🔹 정보 조직화 설계의 종류  

웹사이트나 애플리케이션을 만들 때 정보를 어떻게 구성할지 정하는 방식이 여러 가지가 있다. 대표적인 4가지 구조를 살펴보자.  

| 구조 유형 | 설명 | 예시 |
|----------|-----|------|
| **1. 선형 구조 (Linear Structure)** | 한 페이지씩 한 방향으로 이동하는 구조 | 쇼핑몰에서 "홈 → 카테고리 → 제품 목록 → 상세 페이지" |
| **2. 계층 구조 (트리 구조, Hierarchical Structure)** | 상위 메뉴에서 하위 메뉴로 Top-Down 방식으로 이동하는 구조 | 회사 조직도, 대학교 학과 구조, 네비게이션 메뉴 |
| **3. 격자 구조 (그리드 구조, Grid Structure)** | 바둑판식으로 수평과 수직 형태로 연결된 구조 | 갤러리 페이지, 게시판 목록, 온라인 도서관 |
| **4. 네트워크 구조 (웹 구조, Network Structure)** | 비선형적으로 배열되어 특정 페이지로 이동이 자유로운 구조 | 위키(Wikipedia), 포털 사이트 |


---

## :four: 와이어프레임(Wireframe)이란?  

웹사이트나 애플리케이션을 만들 때, 전체적인 **구조와 레이아웃을 설계하는 과정**을 와이어프레임(Wireframe)이라고 한다.  
이것은 마치 건물을 짓기 전에 설계도를 그리는 것과 비슷하다.

### 🔹 와이어프레임의 역할  

✅ **화면 설계:** 각 페이지와 기능 간의 관계를 정리한다.   
✅ **기획 단계:** 개발자가 보기 전에 어떻게 만들지 정리한다.  
✅ **디자인 가이드:** UI/UX 디자이너, 개발자가 참고할 기본 틀을 제공한다.

### 🔹 와이어프레임 구성 요소  

| 구성 요소 | 설명 |
|----------|-----|
| **레이아웃(Layout)** | 화면의 전체적인 구조 |
| **내비게이션(Navigation)** | 메뉴, 버튼 등 사용자가 이동할 수 있는 요소 |
| **콘텐츠 배치(Content Placement)** | 텍스트, 이미지, 버튼 등이 어디에 위치할지 결정 |
| **기능 정의(Functionality Definition)** | 버튼을 누르면 어떤 일이 일어날지 정의 |



## :five: 콘텐츠 매핑과 콘텐츠 모델이란?  

### 1. 콘텐츠 매핑(Content Mapping)
- 웹사이트나 애플리케이션에서 콘텐츠가 어떻게 배치되고 연결될지 정의하는 과정이다.  
- 사용자가 원하는 정보를 효율적으로 찾을 수 있도록 콘텐츠를 구조화하고, 탐색 경로를 최적화하는 데 중점을 둔다.

### 📌 **주요 특징**
- 정보 구조(Information Architecture, IA)와 관련된다.
- 콘텐츠 간의 관계를 시각화하고, 내비게이션과 탐색 경로를 최적화한다.
- 사용자 경험(UX) 개선을 위해 콘텐츠의 흐름을 설계한다.
- 사이트맵, 사용자 여정(User Journey), 내비게이션 구조 등을 포함한다.

#### ✅ 예시
- 홈페이지에서 "자주 묻는 질문(FAQ)"으로 쉽게 이동할 수 있도록 메뉴를 배치하는 과정
- 블로그 게시글에서 관련 기사 목록을 자동으로 표시하도록 설정하는 과정

### 2. 콘텐츠 모델(Content Model)
- 콘텐츠의 구조와 속성을 정의하여 콘텐츠를 체계적으로 관리할 수 있도록 하는 설계 방식이다.  
- 콘텐츠 유형, 속성, 관계 등을 정의하여 새로운 콘텐츠를 추가할 때 일관성을 유지하고, 검색과 필터링 기능을 향상할 수 있다.

### 📌 **주요 특징**
- 데이터 모델링과 관련되며, 콘텐츠의 구조를 정의한다.
- 콘텐츠의 유형(Content Type), 속성(Properties), 관계(Relationships)을 포함한다.
- 일관된 용어 사용을 통해 자동화된 콘텐츠 연결을 가능하게 한다.
- 새로운 콘텐츠를 쉽게 추가할 수 있도록 유연성을 제공한다.

#### ✅ **예시**
- 뉴스 웹사이트에서 "기사(Article)" 유형을 만들고, 속성으로 "제목", "본문", "작성자", "작성일"을 정의하는 과정
- 전자상거래 사이트에서 "상품(Product)" 유형을 정의하고, "카테고리(Category)", "리뷰(Review)"와 관계를 설정하는 과정

## :six: 태스크 플로우(Task Flow)란?  

- 사용자가 웹사이트나 애플리케이션을 사용할 때, 어떤 순서로 행동하는지(경로)를 정리하는 과정이다.


### 🔹 태스크 플로우 작성 시 사용되는 기법  

| 기법 | 설명 |
|------|-----|
| **사이트맵(Sitemap)** | 웹사이트의 특정 영역을 대표하는 페이지들을 시각적으로 보여주는 구조도 (회사 조직도처럼 계층적으로 표현) |
| **사용자 플로우(User Flow)** | 사용자가 웹사이트에서 취하는 경로나 과정을 보여주는 지도 (어떤 버튼을 클릭하면 어디로 이동하는지 정리) |
---

## 🔥 실습: 간단한 와이어프레임 그려보기!  

### ✏️ 실습 목표  
아래의 화면을 기준으로 간단한 와이어프레임을 그려보자!  

#### 🖼️ 예제 화면 구성
1. **홈 화면**
   - 상단에 "메뉴 버튼"
   - 중앙에 "로고"  
   - 하단에 "로그인 버튼, 회원가입 버튼"  

2. **로그인 화면**
   - 이메일 입력 창  
   - 비밀번호 입력 창  
   - 로그인 버튼  

3. **회원가입 화면**
   - 이름 입력 창  
   - 이메일 입력 창  
   - 비밀번호 입력 창  
   - 회원가입 버튼  

### 📌 예제 와이어프레임 작성 방법  
📝 **1단계:** 연습장에 손으로 스케치해보기  
📝 **2단계:** Figma, Adobe XD, Balsamiq 같은 도구로 디지털 와이어프레임 제작  
