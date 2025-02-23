# 이용자 화면 설계
## 헤더와 푸터

<center>
   <image src="img/header.png">
</center>

### 1. 헤더
- 헤더는 기본적으로 모든 화면의 상단에 적용된다.
- 하나의 헤더를 모든 화면에 적용하도록 설계할 수도 있지만 경우에 따라서 2개 또는 3개를 설계하여 각 화면에 알맞은 헤더를 설계해서 호출할 수 있다.
- [Header Type 1]은 메인, 검색 결과, 라라마켓 소개에 적용되는 타입으로, GNB영역 하단에는 오픈 숍과 스타일 숍의 진입경로를 두어 이용자에게 잘 노출되도록 설계했다.
- [Header Type 2]은 오픈 숍과 스타일 숍에 사용되는 타입으로, 쇼핑 시 자주 사용하는 장바구나, 주문조회 메뉴를 GNB 하단에 배치하여 이용자의 사용 시나리오를 고려해 설계했다.

### 2. GNB
- 헤더에서 가장 중요한 요소는 3라인의 GNB이다.
- 이용자의 시선이 먼저 향하는 왼쪽부터 중요한 순으로 배치한다.
- 따라서 상품 판매가 중요한 웹 쇼핑몰에서는 주로 상품 카테고리 메뉴를, 브랜드 중점적으로 알려야 하는 신생 브랜드 등은 브랜드 소개 메뉴를 가장 왼쪽에 배치한다.
- GNB는 구성하다보면 수정할 일이 많이 생기므로 처음부터 완벽하게 설계할 필요는 없다.
- 초안을 만들고, 사이트를 설계하며 수시로 보완해 완성도를 높일 수 있다.

### 3. 회원/비회원
- 회원 가입 기능이 있는 사이트는 로그인 전후 화면을 구분해 설계한다.
- 로그인 전 화면에는 웹 쇼핑몰의 특징을 강조해 회원 가입을 유도하는 것이 좋다.
- 비회원보다는 회원으로 구매했을 때 받을 수 있는 혜택이 많다는 점을 알리는 식이다.
- 반면, 로그인 후 화면에는 이용자의 맞춤 정보나 로그인 후 이용할 수 있는 메뉴를 설계한다.
- 1 쇼핑몰 이름 상단에 있는 홍보 메시지도 비회원과 회원에게 필요한 메시지를 따로 기획할 수 있다.
- 2. 유틸리티 메뉴는 GNB의 보조 메뉴역할을 한다.
- 로그인 전에는 [회원가입]과 [로그인] 메뉴를 반드시 배치하고, 로그인 후에는 이용자가 외원 정보와 주문정보를 확인할 수 있는 메뉴, 이용자가 자주 사용하는 메뉴 등으로 구성할 수 있다.

### 4. 서브메뉴
- GNB메뉴와 오픈숍, 스타일숍에 대한 정의는 다음 슬라이드에 할 것이므로 해당 기능을 설명하는 화면의 쪽 번호, 화면 아이디, 화면명 등을 디스크립션에 기입하여 작업자가 해당 화면을 쉽게 찾아갈 수 있도록 한다.

### 5. 검색어 입력
- 검색어를 입력하는 공간에 '검색어를 입력하세요!'라는 기본 문구가 있다.
- 이용자가 이 부분을 클릭하면 기본 문구는 사라지고 검색어를 입력할 수 있다.
- 이러한 기능을 플레이스홀더(Place holder)라고 하며, 이용자가 어떤 내용을 입력하면 되는지 아렬주는 가이드 역할을 한다.
- 검색 기능은 가장 마지막에 할 메인 화면 설계 시 다룰 것이다.
- 마찬가지로 이 기능을 설명한 화면의 위치 정보를 디스크립션에 남겨놓는다.

## 2. GNB 서브 메뉴 설계하기

<center>
   <image src="img/GNB.png">
</center>

 ### 1. 서브메뉴
 - 1,4,5,6에 마우스를 올리면 서브 메뉴가 펼쳐진다.
 - 이런 기능을 마우스 호버(hover)라고 한다.
 - 마우스 호버는 작은 영역에 핵심 정보 하나만 표시해 놓고 마우스 커서를 그 위로 가져가면 자세한 정보를 펼쳐서 보여준다.
 - 좁은 영역에 많은 정보 노출이 필요한 경우인 메인 메뉴에 속한 서브 메뉴를 출력할 때 자주 사용한다.
 - 2,3 메뉴는 서브 메뉴가 없으므로 별도의 기능을 설계하지 않아도 된다.

### 2. 상품메뉴
- 5,6번의 서브메뉴는 상품 카테고리로 구성한다.
- 이용자의 관심을 끌 수 있도록 마케팅 전략에 따라 최신 등록 상품, 시즌 추천 상품 등도 카테고리로 설계할 수 있다.

### 3. 오픈숍
- 이용자가 제품을 직접 등록하고 판매하는 중고거래 메뉴이다.
- 여기서는 최근 등록된 상품을 먼저 볼 수 있게 설계했다.
- 새로운 상품이 계속해서 업데이트되는 상황을 보여 주며, 사이트의 활성화 정도를 이용자에게 간접적으로 알려준다.
- 등록된 상품 더 많은 이용자에게 홍보해 판매 촉진 역할을 하기도 한다.
- 최근 등록된 상품이 효과가 없다면 이용자들이 등록한 상품 중 노출 가치가 높은 상품을 선정해 보여 주는 추천 상품을 기획하는 등 기획자의 아이디어에 따라 마음껏 설계할 수 있다.

### 4. 스타일숍
- 운영자가 직접 판매하는 상품을 진열한 메뉴이다.
- 서브 메뉴의 6.1 상품 미리 보기 영역은 시준 추천 상품, 많이 판매된 상품, MD추천 상품, 할인 중인 상품 등으로 다양하게 설계할 수 있다.
- 상품을 자동으로 호출해 표기하는 방식이라면 어떤 방법으로 호출할 것인지도 고민해야 한다.

<table border="1">
<tr>
    <td>
        이용자의 웹 사이트 이용 데이터를 활용하는 방법
    </td>
    <td>
        이용자가 웹 사이트를 이용하여 남기는 데이터를 기준으로 상품을 호출한다.<br>
        - BEST 상품은 이용자가 구매한 상품의 개수를 기준으로 가장 많이 판매되는 상품 1 ~ 5위 또는 1 ~ 10위 등 상황에 맞게 설계한다.<BR>
        - 최근 등록된 상품은 이용자(운양자)가 상품들 등록한 날짜를 기준으로 가장 최근에 등록한 상품 1 ~ 5개 또는 1 ~ 10개 등 상황에 맞게 설계할 수 있다.
    </td>
</tr>
<tr>
    <td>
        운영자가 직접 상품을 선택하는 방법
    </td>
    <td>
        시준 추천 상품, MD 추천 상품, 요즘 유행 상품 등은 프로그램이 강품을 구별할 수 있는 특정한 기준이 없으므로 운영자가 직접 상품음 선별한다. 운영자가 직접 관리자 화면에 접속해 제목을 정하고 해당 영역에 호출할 상품을 하나씩 지정한다. 따라서 이 기능을 구현할 때는 관리자 화면을 어떻게 구성하면 좋을지도 함께 고민해야 한다.
    </td>
</tr>
</table>

### 5. 고객센터
- 웹 쇼핑몰 이용에 보조적인 역할을 하는 메뉴이다.
- 따라서 오픈 초기에는 이용자의 불편이 직접적으로 접수되지 않을 시기이므로 기능을 간소화하는 것이 좋다.
- [고객센터]에 등록된 게시글도 최근 등록된 상품, 시즌 추천 상품 영역과 같이 최근 등록글, 중요 공지글 등을 호출하도록 구현할 수 있지만, 오픈 초기에는 개발 대비 효율성이 낮으므로 간단히 메뉴명만 제공한다.
- 이용자가 늘어나고 고객 문의가 많아지면 그 때 효과적인 방법으로 개선하는 것이 바람직하다.

### 6. 문자호출
- 상품명 등의 문자를 호출할 때는 문자의 길이를 디스크립션에 정의한다.
- 그렇지 않으면 글자가 넘쳐 다른 내용을 가리거나 퍼블리싱이 어긋나 화면 정렬이 흐트러질 수 있다.
- 문자의 길이는 표기 줄 수로 작성하면 좋다.
- 바이트(byte)또는 글자 수로 작성하는 것이 가장 정확하지만, 파워포인트에서 작성한 문서와 포토샵 또는 HTML웹 문서에서 출력하는 화면 사이즈에 차이가 있기 때문에 기획 단계에서는 노출되는 정확한 글자 수를 파악하기 어렵다.
- 그러므로 노출되는 줄 수를 디스크립션에 정의한 후 디자이너나 퍼블리싱 작업이 완료됐을 때 결과물을 검토하며 값을 보완해야한다.

## 3. 푸터 설계하기
<center>
   <image src="img/Footer.png">
</center>

### 1. 푸터
- 웹 사이트의 모든 화면 아래쪽에는 푸터가 있다.
- 푸터는 화면의 가장 하단에 위치하므로 상단 영역에서 제공하지 않는 서비스 중 이용 빈도나 중요도가 낮은 메뉴를 주로 배치한다.
- 이용자에게 추가로 알리고 싶은 정보, 웹 쇼핑몰과 관련된 다른 웹 사이트 정보, 이용자의 궁금증을 해소할 수 있는 정보, 웹 쇼핑몰 관련 법률 표기 사항 등이 있다.
- 대분의 웹 사이트는 회사 소개, 이용 약관, 개인정보 처리방침, 인재 채용, 제휴/제안 등을 푸터의 메뉴로 구성한다.
- 이용자들도 위와 같은 메뉴들은 하단에 있다는 것을 학습으로 알고있다.
- 만약 푸터로 구성할 메뉴가 없다면 억지로 설계하지 않아도 된다.

### 2. 법적 표기 의무 사항
- 전자상거래 등에서 소비자 보호에 관한 법률 제 10조(사이버몰의 운영)와 전자상거래 등에서의 소비자 보호에 관한 법률 시행 규칙 제 7조(사이버몰 운영자의 표시 방법)에 의해 아래와 관련된 사업자 정보를 첫 화면에 모두 표시하고, 이용 약관은 링크로 연결해야 한다.

<table border="1">
<tr>
    <td>
        법적 표기 의무 사항
    </td>
    <td>
        상호 및 대표자 성명, 영업소가 있는 곳의 주소, 전화번호, 전자 우편 주소, 사업자 등록 번호, 사이버몰의 이용 약관
    </td>
</tr>
</table>

### 3. 저작권
- 가장 아랫줄에는 저작권(Copyright...)을 표기한다.
- 저작권은 저작물을 창작한 순간에 자동으로 발생하기 때문에 저작권 표시가 없어도 저작권법에 따라 보호를 받을 수 있지만, 방문자의 무단카피 예방을 위해 예시와 같이 설계한다.

### 4. 링크설계
- 1~ 11각 메뉴에 링크 주소와 방식(blank, self)을 디스크립션에 작성한다.
- 그 중 11[사업자 번호 확인]메뉴는 단순한 링크로는 연결할 수 없다.
- 공정거래위원화에서 사업자 번호를 이용해 링크를 연결해야 하기 때문이다.
- 그러므로 연결할 수 있는 가이드가 있는 화면 경로나 링크를 디스크립션에 작성해두면 개발자가 정보를 찾는 시간을 절약할 수 있다.

<hr>
<br>

# 회원가입
- 회원가입 프로세스를 설계하기 위해 가장 먼저 확인할 사항은 구현하려는 사이트에 회원가입이 필요한지 검토하는 것이다.
- 웹 쇼핑몰, 플랫폼, 포털 등과 같이 이용자 개인별로 제공되는 서비스나 정보가 있다면 이용자마다 구분이 필요하므로 회원 가입 프로세스 설계가 필요하다.
- 반면 회사 홈페이지나 마이크로사이트(한 기업에서 여러 브랜드를 운영할 때 특정 브랜드만 소개하는 사이트), 국가 기관의 정보 제공 사이트 등 누구에게나 제한 없이 정보를 제공하거나 이용자 개인별로 제공되는 서비스가 없는 경우, 이용자가 사이트에서 정보를 남기는 상황이 없다면 회원 가입 프로세스는 설계하지 않는다.
- 회원 가입 프로세스를 설계할 때는 사이트를 효과적으로 이용하기 위해 이용자로부터 어떤 항목을 수집할 것인지를 먼저 분석한다.
- 그러기 위해서는 사이트 내에서 제공하는 서비스를 살펴봐야 한다.
- 아직 사이트 화면을 눈으로 볼 수 있는 단계가 아니므로 서비스 기획서, 기능 정의서, 정책 정의서 등을 참고하여 사이트에서 제공할 기능과 이용자의 이용 형태를 최대한 유추해 이용자의 유형을 분류(개인/사업자, 학생/교수, 일반/프리미엄 등)하고 필요한 항목을 최대한 수집한다.
- 그리고 취합한 내용을 바탕으로 회원 가입 프로세스를 설계한다.

## 1. 회원가입 프로세스 설계하기
- 회원 가입 프로세스를 설계한다는 것은 어떤 순서로 회원 가입을 진행할 것인지 순서를 정 하는 것이다.
- 먼저 회원 가입 단계에서 회원에게 알려야 하는 사항과 회원으로부터 받아 야 하는 정보 등을 모두 모은 다음 어떻게 단계를 나누어 효과적으로 설계할지 고민해야 한다.
-  회원에게 알려야 할 사항도 많고 수집해야 할 항목도 많다면 아래의 큰 기본 프로 세스를 먼저 설계한 후 그 외 단계는 이를 기준으로 앞 또는 사이사이에 넣어 프로세스를 완성하면 쉽다.
### 1. 먼저 약관 동의, 정보 입력, 가입 완료의 3단계를 기본 프로세스로 설계합니다.
- 회원 정보를 수집하려면 먼저 개인정보 수집을 위한 동의와 사이트를 이용하기 위한 조건 에 대한 동의가 먼저 이루어진 다음에 진행하는 것이 기본 원칙이다.
-  회원 정보를 먼저 수집하고 나서 약관 동의를 받는 것은 계약서에 서명부터 하고 세부 내용을 읽어보는 것과 같은 행위이므로 이용자가 사이트 약관에 동의하는지 의사를 먼저 묻는 것이 기본이다.
- 가입 완료 단계는 항상 가입 프로세스를 모두 마친 마지막 단계로 설계합니다.

### 2. 약관 동의, 정보 입력, 가입 완료 이외의 단계가 있다면 가장 앞 또는 단계 사이사이에 넣어 정보 수집의 흐름을 구상합니다.
- 이용자의 선택에 따라 약관 동의 내용이 변경되거나 정보 입력 항목이 변경되는 등의 영향 이 있는 경우라면 약관 동의 앞 단계로 설계한다. 
- 가장 흔한 예가 바로 이용자 분류이다. 
- 가입하는 이용자가 개인회원인지 기업회원인지에 따라 약관 내용과 수집되는 정보가 달라질 수 있다.
- 따라서 이용자에게 알맞은 회원 정보 양식을 제공하기 위해 약관 동 의 앞 단계에 설계한다.
- 정보 입력 단계에서 수집된 정보 외의 추가 정보를 수집하거나 결제하는 등의 단계가 필요 하다면 정보 입력 단계와 가입 완료 단계 사이에 해당 정보를 수집할 수 있도록 설계한다. 
- 회원 가입 절차를 간단히 하는 것이 이용자 확보에 도움이 되지만, 서비스의 특성상 어쩔 수 없이 특정 조건을 만족해야만 가입이 가능할 수도 있다.
- 특정한 자격 조건을 확 인하기 위해 서류를 업로드하거나, 유료로 정보를 제공하는 사이트에서 가입비를 결제해 야하는 경우가 예이다.
- 물론 정보 입력 단계에서 이 정보를 한 번에 모두 받을 수도 있다.
- 그러나 굳이 단계를 나누어 설계하는 이유는 최초 정보 입력 항목을 간소화하여 이용자의 사이트 이탈률을 줄 이고, 각 단계마다 임시 저장 기능을 두어 중간에 화면을 이탈해도 회원 가입을 이어서 할 수 있도록 편의성을 높이기 위해서이.
- 따라서 회원 가입 시 정보 입력 단계는 최대한 간소화하고, 추가로 갖춰야 하는 요건이 많다면 각 단계에 임시 저장 기능을 두어 기존에 작성된 내용을 불러올 수 있도록 이용자 편의를 돕는 편이 효과적이다.

## 2. 약관 동의화면 설계하기

<center>
   <image src="img/회원가입프로세스1.png">
</center>

### 1.약관 동의
- 이용자와 정보 제공자 간 서로 지켜야 하는 약속을 명시한 내용을 이용자가 동의하는 것을 말한다. 
- 또한 사이트 이용 중 작성되는 개인정보를 사이트에서 수집하는 것에 동의하고 운영자는 이를 철저히 관리하겠다는 개인정보 수집 및 이용 동의가 있다. 
- 그 밖에도 이용자의 개인정보가 사이트 이용 목적 외에 사용될 경우, 마케팅 용도로 사 용될 경우 등에는 별도의 항목을 구성하여 이용자의 동의를 받아야한다.
### 2. 경고창
- 본 약관 동의 화면은 서비스 이용 약관에 대한 동의를 받을 때 개인정보 수집 및 이용 동 의와 개인정보 제3자 제공 동의, 마케팅 정보 제공도 함께 진행한다.
-  각 항목은 필수 동 의와 선택 동의로 나뉜다.
-  필수 동의 항목에 동의하지 않으면 더 이상 회원 가입 프로세 스를 진행할 수 없으므로 적절한 경고창을 띄워야한다.
### 3. 개인정보 수집 및 이용도 필수 동의 항목입니다. 
- 이용자가 개인정보 수집 및 이용에 대 한 내용을 모두 인지하고 동의한 후에 회원 정보를 받는 것이 순서이기 때문에 약관 동의 화면과 회원 정보 작성 화면의 순서를 바꾸거나 이 두 가지를 한 페이지 내에서 일괄 진행 하지 않도록 주의해야 한다.

### 4. 레이아웃
- 여기서는 레이아웃을 2단으로 구성하여 왼쪽 레이아웃에 회원 가입 절차를 스텝퍼(stepper) 로 표기했다. 
- 회원 가입 절차는 이용자가 회원 가입의 복잡성을 판단하는 척도가 되며, 가입 절차 단계 중 현재 어느 단계를 진행하고 있는지 알려 준다.
- 설계 시 이용자가 현재 어느 단계에 있는지 알 수 있도록 해당하는 단계에 하이라이팅(highighting)으로 표시해 주면 좋습니다.

### 5. 스크롤창
- 1 ~ 4 약관의 내용을 한 화면에서 모두 볼 수 있게 스크롤 창으로 설계한다.
-  스크롤은 특정 영역 안에 그보다 많은 내용이 담기면 자동으로 생기는 HTML 기능으로, 설계에 필수 요소는 아니지만 화면 설계 리뷰 시 이해를 돕기 위해 넣어 두는 것이 좋다.

### 6. 필수/선택동의
- 상품 거래가 성립하기 위해 이용자와 관리자가 서로 지켜야 할 중요한 항목은 필수 동의 로 구분하고, 서비스 이용이나 상품 거래와 직접적인 관련이 없는 항목은 선택 동의로 구분합니다. 
- 이용자 편의를 위해 [모두 동의] 체크 박스도 설계한다.

### 7. 관리자 화면
- 약관 내용은 관리자 화면에서 등록한 약관 내용이 호출되도록 설계한다.
- 만약 관리자 화면에 약관 등쪽 기능을 설계하지 않는다면, 퍼블리셔는 HTML 파일 안에 전체 약관 내 용을 직접 삽입해야 한다. 
- 약관 내용은 별도의 파일로 준비해서 화면 정의서와 함께 전 달하고 화면 정의서에는 작업자가 쉽게 이해할 수 있도록 약관 파일명만 기입한다.
### 8. 요소의 배치
- PC 화면의 경우(마우스 환경) 긍정적인 요소의 버튼(확인, 전송, 완료, 다음 등)을 왼쪽에 배치한다.
- 글을 읽는 방향을 기준으로 부정적인 요소의 버튼(취소, 삭제, 뒤로 등)보다 먼저 눈에 띄게 하기 위해서이다.
- 반대로 모바일 화면의 경우(터치 환경) 부정적인 요소가 왼쪽, 긍 정적인 요소가 오른쪽에 위치하도록 설계한다.
- 화면이 작은 모바일 화면에서는 이용자 의 시선보다 쉬운 터치를 우선시하므로 오른손 엄지 손가락이 터치하기 쉬운 자리에 설계 하는 것이다.
- 따라서 회원 정보 입력 화면으로 이동하는 [다음] 버튼은 왼쪽에, 가입을 원하지 않는 이용자가 누를 수 있는 [취소] 버튼은 오른쪽에 설계한다. 
- 현재 화면은 GNB 메뉴가 생략된 상태이지만 GNB 메뉴를 눌러도 화면이 이동하므로 [취소] 버튼은 생락할 수 있습니다.

### 9. 다음단계
- 이용자는 필수 동의 항목을 모두 체크해야만 다음 단계로 넘어갈 수 있다.
- 만약 필 수 등의 항목에 제크하지 않고 다음 버튼을 눌렀다면 상황에 맞는 경고 창(alert)이 표 시되어야 하고, 이용자가 [취소] 버튼을 눌렀다면 실행 여부를 다시 묻는 확인 창(confim)
이 표시되어야한다.

## 3. 회원 정보 입력 화면 설계하기

<center>
   <image src="img/회원가입정보입력.png">
</center>

### 1. 입력공간 나누기
- 이용자가 입력해야 할 정보를 표와 도형을 사용하여 공간을 적절하게 구분하여 설계한다.
- 회원 정보 입력 화면에서는 수집 항목 및 입력 조건을 설계하는 것이 중요합니다. 여기 서는 이름, 아이디, 비밀번호, 이메일 4가지 항목을 수집한다.
- 이름을 짓는 규칙에 관한 벌출에 의거 이름은 성을 포함해 최대 6자까지 입력받을 수 있도록 설계한다.
- 단, 외국인도 회원 가입을 받는다면 최대 30자까지 입력할 수 있도록 하는 것이 좋다.
- 아이디, 비밀번호, 이메일도 최대 글자 수, 한글/영문 사용 여부, 띄어쓰기/특수문자 사용 여부 등과 같은 입력 조건이 필요하다. 
- 정책 정의서를 보고 각각의 입력 조건을 확인한 후 이용자가 알 수 있도록 안내 문구를 삽입합니다.
### 2. 정보의 입력
- 회원 정보에 이름을 입력할 때는 이용자가 직접 입력하는 방법과 본인 인증 서비스를 사 용하여 확인된 이름을 그대로 가져오는 방법이 있다. 
- 은행, 공공 기관, 대학교, 카드 회 사와 같이 보안이 중요한 웹 사이트의 경우 입력된 회원 정보가 실제 이용하는 사람의 정 보라는 것을 확인하기 위해 본인 인증 서비스를 이용하는 것이 좋다.
- 이는 본인 명의 휴대폰을 가지고 있다는 전제하에 통신사에 가입된 정보를 토대로 본인임을 인증하는 서비스이다.

### 3.중복확인
- 아이디는 웹 사이트에서 이용자를 식별할 수 있는 유일한 값이다.
- 이용자 간 같은 아이디는 사용할 수 없으므로 반드시 아이디 중복 확인 기능을 설계한다.
- 웹 사이트 가 입시 자신이 사용하려는 아이디를 입력하고 (중복 확인] 버튼을 누르면 내가 설정한 아이 디를 다른 이용자가 사용하고 있는지 확인한다. 
- 이때 같은 아이디가 있는 경우와 없는 경우 모두를 고려해 이용자에게 노출할 메시지를 정한다.
### 4. 비밀번호
- 비밀번호는 특수 문자로 표기되도록 설계한다. 
- 이를 마스킹(masking) 처리 또는 패스워드(password) 처리라고 한다. 
- 비밀번호는 아이디와 달리 보안이 중요하 므로 무엇을 입력했는지 알 수 없도록 해야한다. - 그래서 원하는 비밀번호로 정확하게 입력했는지 확인하기 위해 비밀번호 확인란도 함께 두어 두 개의 비밀번호가 동일한 경우 에만 가입에 성공하게 합니다.
### 5. 이메일 입력
- @ 앞에는 영문과 숫자만, 뒤에는 이메일 형식만 입력 할 수 있도록 한다. 
- 모든 이메일 도메인을 드롭다운 목록에 담을 수 없으므로 이용자가 직접 입력할 수 있는 기능도 함께 설계한다. 
- 드롭다운 목록에 들어갈 이메일 형식의 종 류는 디스크립션에 기입합니다.
### 6. 회원가입 종류
- 이 웹 쇼핑몰은 회원 유형에 따라 [회원가입] 버튼이 2개이다. 
- 첫 번째 버튼은 상품만 구매할 수 있는 계정이고, 두 번째 버튼은 상품을 구매할 뿐만 아니라 자신의 상품을 직접 등록하여 판매할 수 있는 계정이다. 
### 7. 툴팁
- 회원 가입 유형을 안내하는 6 ~ 7 문구는 말풍선(tooltip)으로 표기한다. 
- 매번 내용을 보아야 사이트를 이용할 수 있는 사항은 별도 클릭이 없어도 내용을 볼 수 있도록 화면에 직접 안내 문구를 작성한다. 
- 하지만 이용자 대부분이 알고 있거나 쉽게 유추할 수 있는 내용, 한 번만 알면 쉽게 할 수 있는 안내는 말풍선을 사용하는 것이 좋다.
### 8. 회원 정보 필수 작성 항목
- 이용자가 반드시 입력해야 사이트를 이용할 수 있는 정보들이다. 
- 이용자가 쉽게 구분할 수 있도록 1,2,4,5에 눈표(*)를 삽입합니다. 
- [취소]버튼처럼 이용자가 입력한 내용을 무효화할 때는 확인 창을 한 번 더 띄운다.
### 9. 안내문구
- 화면 위와 아래에는 안내 문구를 배치한다. 
- 이용자가 반드시 알아야 하는 내용은 시선 이 집중되는 위쪽에 배치하는 것이 좋다. 
- 하지만 이용자는 회원 가입 화면의 안내 문 구를 잘 읽지 않는 경향이 있다. 
- 따라서 중요한 안내 사항은 아래쪽에 중복으로 배치 하는 것이 좋다.

## 4. 회원 가입 타당성 검증 화면 설계하기
<center>
   <image src="img/타당성검증.png">
</center>

1. 회원 가입 정보를 모두 입력했다면 이제 [가입하기] 버튼을 누르면 끝입니다. 하지만 입 력 조건에 맞는지, 필수 항목을 작성했는지 등 이용자가 작성한 정보가 정책에 맞게 작성 되었는지 검증해야 합니다. 이러한 과정을 타당성 검증(valication check)이라고 한다.

2. 타당성 검증은 이용자가 모든 정보를 입력하고 다음 단계로 넘어가는 가장 마지막 시점 인 [가입 완료] 버튼을 클릭했을 때 체크되도록 설계한다(본 예시에서는 [스타일 숍 회원 가입], [오픈 숍 회원가입] 버튼이 가입 완료와 같은 역할을 한다.) 간단한 타당성 검증은 디스크립션에 작성해도 좋지만, 회원 정보 입력 화면처럼 작성해야 할 항목이 많다면 표로 이해하기 쉽게 정리하는 것이 좋다. 회원 가입 정보 입력 화면 다음에 슬라이드를 새로 만들어 정리한다.

3. 웹 기획자는 가입 정책으로 정해 놓은 항목 외에도 이용자가 행할 수 있는 모든 변칙 상황을 예상하여 그에 맞는 대처 방안을 설계해야 한다. 가장 첫 번째 항목인 이름 항목을 예로 들면, 이용자가 이름을 입력하지 않고 바로 [가입 완료] 버튼을 눌렀을 경우부터 작성해 나가면 됩니다.

4. 타당성 검증은 보통 개발자들이 가장 첫 번째 항목부터 순차적으로 검사할 수 있도록 개발한다. 따라서 회원 가입 항목의 여러 곳이 잘못 작성되어도 동시에 경고 창이 노출되는 것은 아니다. 검사 과정 중 가장 첫 번째로 잘못된 항목을 체크하여 경고 창을 노출하고 이용자가 내용을 수정할 수 있도록 한다. 첫 번째로 항목이 다시 올바르게 작성되었다면 다음 항목의 잘못된 사항을 체크하여 경고 창을 노출하게된다.

5. 굳이 경고 창을 노출하 지 않아도 된다. 타당성 검증 과정에서 잘못 입력된 항목이 있다면 해당 항목으로 커서를 위치시켜 이용자가 알 수 있도록 설계할 수도 있다.(본 도서에서는 학습을 위해 경고창으로 설계하였습니다).

6. [스타일 숍 회원가입] 버튼을 클릭한 후 가입이 완료되면 이용자에게 가입 완료 메일을 발송하도록 정의한다.

7. 가입 완료 메일, 구매 완료 메일 등 특정 시점에 발송되는 메일은 별도 슬라이드나 별도 문서로 정리하면 좋다. 개발자들이 대부분 가장 마지막에 일괄 작업하기 때문이다.
발송되는 메일을 정리할 때는 발송 시점, 메일 제목, 메일 내용, 수신자(이용자, 관리자)의 항 목을 구성하여 정리하면된다.

## 5. 본인 인증 화면 설계하기

<center>
   <image src="img/본인인증화면.png">
</center>

1. 오픈 숍은 이용자가 제품을 등록하고 판매할 수 있는 메뉴도 제공하므로 거래 사고를 예 방하기 위해 본인 인증을 진행해야한다. 스타일숍 회원가입을 선택하면 본인 인증 없 이 정보 일력 화면으로 이동하고,[오픈숍 회원가입]을 선택하면 본인 인증을 진행한 후 정보 입력 화면의 이름 항목과 본인 인중에서 확인된 이름을 비교해 작성된 정보가 올바른지 확인할 수 있도록 한다.

2. 본인 인증은 타 업체에서 제작이 완료된 모듈을 연결하여 진행하는 방식이므로 디스크립션에 작동 원리까지 상세히 작성하지 않아도 된다. 다만 본인 인증 완료 후 해당 모듈 에서 보내온 결괏값을 어떻게 사이트에서 활용할 것인지를 정의해야 한다. 본인 인증 성공시 웹 사이트로 국적, 생년월일, 성별, 이름, 휴대폰 번호 등의 이용자 정보를 알려 준다. 여기서 우리는 이름 항목으로 정보의 정확도를 체크할 것이다.

3. 체크 로직을 넣어 본인 인증 완료 후 회원 가입 정보에서 작성한 이름과 일치할 때만 가입이 완료되도록 설계한다. 이름이 일치할 경우와 일치하지 않을 경우 모두 경고창으로 안내한다. 보안이 중요한 웹 사이트라면 본인 인증 실패 횟수를 계산하여 일정 횟수 이상 일치하지 않으면 더 이상 같은 정보로 회원 가입이 진행되지 않도록 설계할 수도 있다.

# 회사 소개
- 우리가 채소, 과일 등 신선 식품을 구매할 때는 생산지를 유심히 살펴본다. - 겉은 신선해 보이지만 건강하게 자란 상품인지 궁금하기 때문이다. 
- 회사 소개 화면은 소비자의 이러한 궁금 증을 해결하는 역할을 한다.
- 회사에 대한 기본 정보를 소개하여 이용자에게 제품에 대한 신뢰도를 높이는 것이다.
- 따라서 웹 기획자는 회사의 인지도를 높이고, 제품이나 서비스의 우수성을 잘 알릴 수 있도록 회사 소개 화면을 기획해야한다.

## 1. 소개화면 설계하기

<center>
   <image src="img/본인인증화면.png">
</center>

### 1. 회사 소개
- 회사 소개 화면은 보통 클라이언트에게 요청하여 받은 자료를 바탕으로 구성한다. 
- 하지만 이를 그대로 반영하기는 어렵다. 
- 클라이언트는 회사 소개를 어떤 방식으로 구성 해야 하는지는 모르는 경우가 많기 때문이다. 
- 웹 기획자는 제품의 성격, 회사의 규모, 브랜드 인지도 등을 파악하여 무엇을 어떻게 소개할 것인가를 고민해야한다. 
- 여기서는 제품의 우수성을 강조함과 동시에 하나의 웹 사이트에서 두 가지 쇼핑몰을 즐길 수 있다는 점을 강조했다.

<table border="1">
<tr>
    <td>
        회사의 규모가 작거나 1인 쇼핑몰의 경우
    </td>
    <td>
        쇼핑몰 운영 마인드, 창업 스토리, 의류를 제작하는 기준 관점, 독특한 스타일, 품질에 대한 자신감을 강조
    </td>
</tr>
<tr>
    <td>
        아이디어 상품인 경우
    </td>
    <td>
        제품이 현실화되는 과정과 대표의 열정을 강조
    </td>
</tr>
<tr>
    <td>
        브랜드 인지도가 높은 제품인 경우
    </td>
    <td>
        제품의 우수성을 증명할 수 있는 점유율, 회원 수를 강조
    </td>
</tr>
</table>

### 2. 링크
- 오픈숍과 스타일 숍 소개 정보 아래 1,2 링크 버튼을 설계하여 자연스럽게 상품소개 화면으로 유도한다.
- 링크 주소와 링크 방식은 디스크립션에 작성한다.

### 3. 쇼핑몰에서 판매하는 제품의 종류에 따라 회사 소개를 디자인하는 방식도 달라진다.
- 보통 저가 상품을 판매하거나 외식 프랜차이즈 기업은 사람들의 흥미를 끌기 위해 유머 코 드나 웹툰, 유명 모델 등을 주로 활용한다.
- 반면 감성적인 요소가 구매 요인으로 작용하 는 화장품과 향수, 그리고 자부심과 전통을 중시하는 악기나 고급 자동차는 무겁고 진지한 분위기를 연출하여 이용자에게 신뢰를 주는 것이 중요하다.

### 4. 회사 소개의 서브 메뉴
- 대표 인사말, 찾아오시는 길, 연혁, 브랜드 소개 등으로 다양하 게 구성할 수 있다.
- 이 내용 역시 기본적인 자료는 클라이언트 측에서 제공받는다.
- 회사 소개 화면에는 특별한 기능을 구현할 일은 없으며 대부분 텍스트로 이루어져 있다. 
- 따라서 이 텍스트를 어떻게 잘 구성해 표현하느냐가 중요하다. 
- 이용자에게 전달할 내용을 알차게 구성하기 위해 다른 회사 소개 화면들을 벤치마킹하는 것도 도움이 된다.

# 스타일숍 상품 소개
- 웹 쇼핑몰의 상품 소개 화면은 이용자에게 상품을 소개하고 구매를 유도하는 등의 핵심 역할을 한다.
- 고객은 온라인으로 쇼핑하면서 상품의 디자인, 가격, 리뷰 등을 살펴보며 구매 를 결정하기 때문이다. 
- 따라서 상품 소개 화면을 어떻게 구성하느냐에 따라 매출에도 상 당한 영향을 줄 수 있다.
- 이번 실습에서는 판매하는 상품에 따라 화면을 어떻게 구성하는지 이해하고, 상품 소개 화 면에 필요한 필수 기능과 설계 방법을 배워 보자.

## 1. 상품 목록 화면 설계하기

<center>
   <image src="img/스타일숍.png">
</center>

1. 상품 목록은 상품 상세의 요약된 정보만으로 원하는 상품을 쉽게 찾아볼 수 있도록 구성 한 것이다. 상세 화면에 진입하기 전 이용자가 찾는 상품임을 감지할 수 있는 요소, 클릭 을 유도하는 마케팅 요소 등 다양하게 구성할 수 있다.

2. 상품 목록은 상품을 그룹별로 정리해 놓은 카테고리를 어디에 위치시키느냐에 따라 레이 아웃이 결정된다. 일반적으로 GNB 영역을 상품 카테고리로 사용하는 형태와 상품 카테 고리를 LNB로 사용하는 두 가지 형태가 있다.

3. GNB 영역에 상품 카테고리가 노출되도록 설계하였으면 상품 목록 화면에 @와 같은 INB 는 필요하지 않다. 하지만 GNB를 다른 메뉴로 설계하였다면 카테고리를 클릭하며 상 품을 열람할 수 있도록 와 같은 LNB가 필요하다. 본 도서에서는 LNB가 있는 레이아웃 으로 설계한다.

3. 인지도, 신뢰도가 낮은 쇼핑몰에서는 GNB에 상품 카테고리를 노출하는 것보다 서비스 개요나 브랜드를 인지시킬 수 있는 요소로 구성하는 것이 이용자의 구매를 유도하는 데 더욱 효과적입니다. 사이트에 신뢰가 생기기 전까지 구매를 망설이기 때문입니다. 반면 인 지도와 신뢰도가 높은 쇼핑몰은 이용자가 사이트에 대해 이미 긍정적인 경험이 있으므로 GNB에 카테고리가 노출되도록 설계해도 좋습니다.

4. 웹 사이트에 검색 기능이 있는데 A 카테고리 목록이 필요한 이유는 무엇일까요? 바로 이 용자들의 소비 스타일이 다양하기 때문입니다.
• 무엇을 살 것인지 정하고 쇼핑몰에 접속하는 이용자: 검색 기능 활용
• 구매 제품은 정하지 않았지만 제품을 둘러보고 싶은 이용자: 카테고리 활용

5. 스타일 숍과 오픈 숍을 쉽게 오갈 수 있도록 각각의 서브 메뉴도 함께 설계합니다. 이용자가 보고 있는 사이트 화면의 위치는 1처럼 표시합니다. 카테고리의 깊이가 깊지 않다면 생략해도 좋습니다. 이용자들은 이미 많은 웹 사이트 이용 경험이 있으므로 정보를 찾다가 길을 잃는 경우는 없습니다.

6. 2와 같이 상품을 홍보하는 배너를 만들면 이용자에게 상품이 더 많이 노출될 수 있습니 다. 만약, 상품 목록에 등록된 상품의 수가 20개 미만이라면 배너 영역을 제외하고 이용자의 관심을 상품 리스트에 집중시키는 것이 좋습니다.

7. 3 쇼핑 안내 기능은 일반 쇼핑몰에서는 볼 수 없는 기능입니다. 이 실습에서는 각종 쇼핑 정보나 알아두면 좋을 패션 정보를 공유하며 이용자에게 더욱 친근하게 다가갈 수 있도록 설계했습니다. 필수 기능은 아니므로 운영 상황을 고려해 설계합니다.

8. 4 상품 목록 영역에 몇 개의 상품을 열과 행으로 배치할지 결정합니다. 카테고리에 등 록된 상품이 없는 경우에 보여 줄 내용도 빠뜨리지 않고 설계합니다. 이 실습에서는 간단히 '등록된 상품이 없습니다.라는 안내 문구가 나타나도록 정의했습니다.

9. 8 상품 요약 정보에는 이미지, 가격, 상품 특징 등 이용자가 자주 찾고 다른 상품과 구별 되는 정보를 간략히 담습니다. 이용자가 상품을 일일이 클릭하지 않아도 상품의 특징을 바 로 파악할 수 있어야 합니다.

10. 이용자가 소비 스타일에 맞추어 상품 목록을 직접 조정할 수 있도록 6 상품 필터 기능과 7 상품 목록 정렬 기능을 설계합니다. 상품 필터 기능은 이용자가 보고 싶은 상품만 노출하는 기능입니다. 예를 들어 관리자 화면에서 특정 상품에 추천상품, BEST, 할인 등의 꼬리표를 추가하면 6의 목록에서 선택 시 해당 상품만 노출하도록 합니다. 상품 목록 정렬 기 능은 상품을 원하는 순서로 재배열하는 기능입니다. 일반 가전, 의류, 화장품 등은 최신순 정렬이 이용자의 구매에 도움이 되지만 농수산물, 가공식품, 생필품 등은 큰 의미가 없으므 로 대신 구매순이나 가격순 또는 리뷰순으로 구성하는 것이 이용에 도움이 됩니다.

11. 9는 페이지 내비게이션입니다. 많은 제품을 한 화면에 모두 보여 줄 수 없으므로 페이 지별로 나누어 보여 주기 위한 기능입니다. 최신순, 인기순과 같이 앞 페이지에 있는 상품의 중요도가 높다면 지금 예시와 같이 설계합니다. 하지만 서적, 자동차 부품, 중고 상품 목록 처럼 앞 페이지에 있는 상품과 마지막 페이지에 있는 상품의 중요도에 차이가 없다면 원하는 페이지로 바로 이동하는 기능을 추가할 수 있습니다. 요즘에는 상품 목록의 마지막을 프 로그램이 인지하여 스크롤이 끝에 도달하면 추가로 상품을 소팅하는
무한 스크롤(infinity scrol) 기능을 사용하기도 합니다.

## 2. 상품 소개화면 설계하기

<center>
   <image src="img/상품소개화면2.png">
</center>

### 1. 상품 상세 화면은 A 상품 요약 영역과 B 상품 상세 및 부가 정보 영역으로 나뉩니다.
- A 상품 요약 영역은 상품 상세를 보지 않아도 상품의 대략적인 정보를 파악하고 구매 여부 를 빠르게 결정할 수 있도록 구매에 필요한 정보 및 기능을 중심으로 구성합니다. 
- 만약 금액 정보나 [구매하기] 버튼이 상품 상세 정보 하단에 있다면 상품 상세 정보를 보지 않고 도 구매할 의사가 있는 이용자에게 매우 불편합니다. 
- B 상품 상세 및 부가 정보 영역은 구매와 관련된 이용자의 각종 문의 사항을 해소하는 역할을 합니다.

• 이용자 입장에서는 상품 소개, 운영자 입장에서는 상품 상세라는 단어를 사용합니다.

### 2. 상품 대표 이미지를 1개, 섬네일을 4개로 설계합니다. 
- 디스크립션 역시 최대 등록 가 능한 이미지 수를 4개로 정합니다. 
- 이미지를 1~2개만 등록한 경우 나머지 섬네일에 일명 엑스 박스(웹에서 이미지가 뜨지 않을 때 나타나는 표기)가 나타나지 않도록, 등록된 수만큼만 섬네 일 영역이 활성화될 수 있도록 정의합니다. 
- 섬네일 이미지가 4개 이상일 경우에는 전체 섬네일 좌우 영역에 이동 버튼을 추가로 설계하세요.

### 3. 요약정보 설계
- 이용자가 상품의 특징을 파악하고 구매로 이어질 수 있도록 꼭 필요한 3~9 상품 요약 정보를 설계합니다. 
- 상품 요약 정보는 미리 정의할 수 있는 항목과 그렇지 않은 항목으로 구분됩니다. 
- 상품을 구매할 때 꼭 확인해야 하는 필수 항목은 미리 정의할 수 있지만, 상품마다 필요한 정보가 다른 경우도 있기 때문입니다.

|미리 정의할 수 있는 항목(3, 4, 5, 9)| 미리 정의할 수 없는 항목(6, 7)|
|--------|--------|
|상품을 구매할 때 꼭 필요한 정보는 사전에 정의할 수 있습니다. 이러한 항목은 화면 정의서를 작성할 때부 터 항목명을 정확히 설정합니다.<br>예) 판매 가격, 적립 포인트, 수량, 배송비, 합계 금액|상품마다 필요한 정보가 다를 수 있습니다. 미리 정의 할 수 없는 항목은 관리자가 상품을 등록할 때 항목명 을 직접 작성하여 등록할 수 있도록 설계합니다.<br>예) 색상, 크기, 옵션 상품 등|

### 4. 상품 내용 호출
- 상품 상세 화면 내용 대부분은 관리자 화면에서 등록한 상품 정보를 호출하는 방식으로 구현됩니다. 
- 따라서 호출할 정보를 항목에 맞게 디스크립션에 정의합니다.

### 5. 배송비 적용
- 관리자 화면에서 상품을 등록할 때는 배송비를 일괄 적용할지, 상품의 크기 등을 고려해 상품별로 따로 적용할지를 선택하도록 설계합니다. 
- 5 배송비 영역에는 관리자 화면에서 설정한 배송비 적용 방식에 따라 배송 비용이 표기되도록 설계하면 됩니다.

### 6. 수량 설계
- 특히 8 수량을 설계할 때는 상품의 구매 단위를 고려해야 합니다. 
- 10개 미만으로 구매할 확률이 높은 경우에는 예시와 같이 스피너(spinner)를 쓰면 편리하지만, 답례품이나 청 첩장처럼 십 단위 또는 백 단위로 구매하는 상품에는 적용하기 어렵습니다. 
- 이런 경우에는 스피너의 수량 단위를 높이거나 수량을 직접 입력할 수 있는 기능을 추가합니다.

### 7. 재고 수
- 관리자는 상품을 등록할 때 상품별로 재고 수를 입력합니다. 
- 판매할 수 있는 상품이 모두 소진되면 이용자가 구매할 수 없도록 막기 위해서입니다. 
- 따라서 이용자가 제품을 구매 할 때마다 시스템에서는 현재 재고 수를 계산합니다. 
- 이용자가 재고 수 이상으로 수량을 입력하면 시스템에서는 현 상품의 재고 수와 이용자가 입력한 구매 수를 비교하여 이용자 에게 구매 가능 여부를 알려줄 수 있습니다. 
- 이때 경고 창으로 실제 구매 가능한 수량을 안 내하도록 정의합니다.

### 8. 결제 금액
- 9 총 결제 금액은 배송료를 제외한 상품 가격만을 표기할지, 배송료를 포함한 총 결제 금액을 표기할지를 정한 후 디스크립션에 총 결제 금액의 계산 방식을 정의합니다. 
- 간단한 수학 공식으로 정의하면 개발자들이 쉽게 이해할 것입니다.

## 3. 상품 상세 - 상품 구매 버튼 및 탭 메뉴 설계하기

<center>
   <image src="img/상품소개화면3.png">
</center>

### 1. 디스크립션 영역 부족
- 화면 내용을 정의할 때 디스크립션 작성 공간이 부족하다면 해당 슬라이드를 복제한 후 추가로 항목을 정의하면 됩니다. 
- 예를 들어 상품 상세 화면에 프로그램으로 호출되는 영역을 (상품명 호출)과 같이 작성하고, 복제된 슬라이드에는 A와 같이 실제 표기되는 문구의
예를 작성해 두면 웹 디자이너 및 개발자들이 이해하기 쉽습니다.

### 2. 장바구니
- 장바구니는 구매할 상품을 기록해 놓는 기능과 같습니다. 
- [장바구니 담기] 버튼을 클릭하면 이용자가 상품이 장바구니에 담겼다는 사항을 인지할 수 있도록 토스트 메시지를 설계합니다. 
- 토스트 메시지(toast message)란 이용자에게 안내할 메시지가 잠시 보였다 스스로 닫히는 기능을 말합니다. 
- 이용자가 내용을 꼭 인지하지 않아도 될 정도로 가볍게 전달 하는 경우나 눈에 보이지 않는 시스템 처리 과정을 알리는 경우 사용합니다.

### 3. 구매하기
- [구매하기]는 이용자가 상품을 구매하겠다는 의사를 표시하는 버튼이다.
- 버튼을 클릭하면 주문 정보 중 빠뜨린 사항은 없는지 확인하고, 누락된 항목이 있다면 Alert 2-1과 같이 안내한다.
- 모든 주문 정보 확인이 완료되면 주문 및 결제 화면으로 이동하도록 설계한다.

### 4. 메뉴 순서
- 3 ~ 7 탭 메뉴의 순서도 중요합니다. 
- 탭 메뉴는 이용자가 상품을 인지하고 구매로 이어지는 순서에 따라 배치하는 것이 좋습니다. 이용자 구매 패턴은 다양하지만, 가장 일반 적인 순서는 아래와 같습니다.

|순서|이용자 구매 판단 순서|설계 시 관리자가 제공해야 할 정보|
|---|------------|---------------|
|1|상품 인지|상품 기본(요약) 정보 제공|
|2|상품 정보 수집| 상품 상세 정보 제공|
|3|구매에 따른 불안, 위험 요인 해소 방안 탐색|다른 구매자의 경험을 참고할 수 있도록 상품 리뷰 제공|
|4|상품에 대한 질문 발생|상품 문의 기능 제공|
|5|배송에 대한 궁금증 발생|배송 안내 제공|
|6|잘못된 선택했을 경우 해결 방안|교환 및 반품 방법 안내 제공|

### 5. 정보의 이동
- 각 탭 메뉴는 한 화면 안에서 모두 표시되며, 정보가 구분되는 곳마다 앵커(anchor)를 놓고 탭 메뉴를 클릭해 해당 영역으로 이동하는 방식으로 작동합니다. 
- 정보가 많으므로 실제 화면에서는 세로로 매우 긴 형태입니다. 
- 따라서 탭을 클릭하면 어느 곳에 스크롤이 위치하는지도 알 수 있도록 정의합니다.

### 6. 상품 상세 정보 호출
- 3 상품 상세 정보는 [관리자 > 상품관리 > 상품등록]에서 등록한 내용을 호출하도록 설계한다.

## 4. 상품 상세 - 상품 리뷰 탭 화면 설계하기

<center>
   <image src="img/상품리뷰화면.png">
</center>

### 1. 상품 리뷰
- 상품리뷰는 해당 상품을 먼저 구매한 이용자의 사용 후기를 확인하며 이용자가 상품 구매 여부를 결정하는 데 중요한 역할을 합니다. 
- 상품 상세 정보에는 소개되지 않는 정보를 알 수도 있고, 구매를 망설이는 불안함을 다른 사람의 후기를 통해 해소할 수도 있습니다.
- 상품 리뷰는 제2의 광고로 불릴 만큼 구매에 많은 영향을 미칩니다.
### 2. 리뷰 로직 설계
- 상품 리뷰는 모든 상품 리뷰를 모으는 하나의 큰 저장소(DB)가 있으며, 여기에서 상품에 해당하는 리뷰만 호출해 보여 주는 방식입니다. 
- 여기서는 가장 기본적인 형태인 상품 후기 내용, 이미지, 만족도를 토대로 상품 리뷰를 설계해 보겠습니다.

### 3. 필수/선택 요소
- 상품 리뷰에 상품 후기와 만족도 선택이 필수 항목이지만 이미지 등록은 필수가 아니기 때문에 이미지 유무를 모두 고려하여 UI를 설계해야 합니다. 
- 상품 리뷰는 GNB에 설계한 상품 리뷰 메뉴에서 작성할 수 있습니다. 
- 상품을 실제 구매한 이용자에게만 작성 권한이 있으며, 리뷰를 작성하려면 상품 구매 후 쇼핑몰에 다시 진입해야 합니다. 
- 따라서 상품 리뷰를 작성하려고 접속한 이용자가 메뉴를 쉽게 찾을 수 있도록 GNB에 상품 리뷰 메뉴를 설계합니다. 
- 마이 페이지에서도 상품 리뷰를 작성하는 기능을 구현합니다.
### 4. 리뷰화면 구성
- 상품 리뷰의 목록은 이미지, 작성일시, 작성자 ID, 만족도, [보기]/[닫기] 버튼으로 구성 합니다. 
- 작성일시는 얼마나 최근에 작성된 리뷰인지를 알 수 있고, 작성자 ID는 실 구매자가 작성한 리뷰라는 것을 증명하는 역할을 합니다. 
- 그리고 [보기]와 [닫기] 버튼을 구성한 이유는 리뷰가 긴 경우 협소한 화면에 모든 내용을 보여 줄 수 없기 때문입니다. 
- 따라서 리뷰의 일부 내용으로 목록을 구성하고, 이용자가 원하는 리뷰만 펼쳐 볼 수 있도록 구성합니다.
### 5. 리뷰 댓글
- 각 상품 리뷰에 달린 댓글은 [보기] 버튼을 눌러 상품 리뷰가 펼침 화면으로 나타날 때 볼 수 있습니다. 
- 댓글은 정책 정의에 따라 다르지만 상품 리뷰 작성자와 운영자만 작성 할 수 있도록 설계합니다. 
- 이는 칭찬 리뷰에 운영자가 감사의 인사를 남기거나, 불만 리뷰에 개선이나 구매자의 오해를 해소하기 위한 안내를 전달하는 기능을 합니다.

### 4.모든 리뷰
- [모두 보기]는 GNB에 있는 상품 리뷰 메뉴로 이동하는 버튼으로, 다른 상품들의 리뷰도 보고 싶은 이용자를 위해 설계합니다. 
- 클릭 시 이동되는 화면 정의서의 쪽수나 화면 ID를 디스크립션에 작성합니다.

## 상품상세 - 상품 문의 탭 화면 설계하기

<center>
   <image src="img/상품문의화면.png">
</center>

### 1. 상품문의
- 이용자는 상품에 대한 궁금증이 해소되지 않으면 구매를 꺼리는데, 이를 해소해 주는 기 능이 바로 상품 문의입니다. 
- 운영 원리는 상품 리뷰와 정반대로 지금 보고 있는 상품 상세 화면을 벗어나지 않고 바로 질문할 수 있도록 구성해야 합니다. 
- 모든 상품의 문의 내용은 [고객센터 > 상품 문의] 메뉴에서 한꺼번에 볼 수 있습니다.

### 2. 질문과 답변은 제목을 입력하지 않도록 설계했습니다. 
- 이용자의 입장에서는 제목을 정하기 모호하기도 하고, 제목이 특별한 의미가 되지 못하기 때문입니다. 
- 여기서는 2 문의 내용 앞부분을 제목과 같이 보일 수 있도록 설계했습니다. 제목으로 사용할 텍스트의 길이 는 디스크립션에 정의합니다.
### 3. 상품 문의 게시판의 UI 구성 요소
- 기본적으로 상품 리뷰와 비슷하지만, 상품 리뷰와 달리 질문 글과 답변 글의 내용을 함께 보여 주어야 합니다. 
- 그런데 이용자가 질문 글을 작성했더라도 운영자가 바로바로 답변을 달기는 어렵습니다. 
- 그렇다고 답변란을 빈 공간으로 오랫동안 남겨 둘 수도 없습니다. 
- 이러한 경우에는 3처럼 답변 글이 올라오기 전까지 안내 문구를 자동으로 노출하는 방법도 있습니다.
### 4. 이용자가 웹 쇼핑몰에 질문을 남기면 답변을 확인하기 위해 다시 방문할 가능성이 높습니다. 
- 재방문 시 상품 문의에 대한 답변이 상품 구매로 이어질 가능성도 높습니다. 
- 그러므로 이용자가 불편이나 부담 없이 운영자에게 질문할 수 있도록 절차를 간소화하는 것이 좋습니다. 
- 여기에는 이용자가 쉽고 빠르게 질문을 남길 수 있도록 5와 같이 댓글 형태로 설 계했습니다. 
- 그러면 이용자는 메뉴 이동 없이 그 자리에서 바로 질문을 남길 수 있습니다.

## 상품상세 - 배송안내/교환 및 반품 탭 화면 설계하기

<center>
   <image src="img/배송안내화면.png">
</center>

### 1. 정책 결정
- 1 배송 안내, 2 교환 및 반품도 어떤 기준, 어떤 정책으로 기획했느냐가 중요합니다.
- 특히 교환, 반품 서비스는 매출, 비용과 직접 연결되기 때문에 이 부분에 대한 기획이 잘못 되면 많은 시간과 인력을 손해볼 수 있으므로 정확한 판단이 필요합니다.
- 1 배송 안내, 2 교환 및 반품을 설계하기 위해서는 상품마다 배송 기준과 교환 및 반품 기준을 똑같이 적용할지, 아니면 상품마다 서로 다른 기준을 적용할지 정책을 먼저 정해야 합니다. 
- 상품마다 똑같은 기준을 적용한다면 관리자 화면에서 필요한 정보를 공통으로 한 번만 입력하고 다른 상품에 일괄 적용하면 됩니다. 
- 다른 기준으로 적용한다면 상품 등록 시 해당 상품에만 적용되는 배송 안내, 교환 및 반품 안내를 직접 입력하여 등록합니다.

|장점|장점|단점|
|---|---|---|
|공통적용|파일 하나만 변경하면 모든 상품에 동시 적용가능| 제품별로 서로 다른 정보를 제공할 수 없다|
|개별 적용| 각 상품에 맞는 정확한 정보를 제공할 수 있다.|모든 상황에 똑같이 적용할 내용이라도 일일이 하나씩 수정해 적용해야한다|

### 3. 배송 안내에는 배송 비용과 기간을 명확하게 안내합니다. 
- 이용자가 주의 깊게 봐야 할 부분은 글자의 크기, 색상 등을 이용해 강조합니다. 
- 교환 및 반품을 위해 이용자가 상품을 재포장할 때 상품이 손상되지 않도록 그림으로 포장 방법을 소개하는 등 다양한 방법으로 기획할 수 있습니다.