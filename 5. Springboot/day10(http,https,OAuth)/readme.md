## Route53 도메인 설정
- 인증과 인가를 구현할 때, JWT는 반드시 HTTPS와 사용해야 한다고 했다.
- HTTPS 인증서를 받기 위해 필요한 절차를 학습해보자.

### 도메인 구매
- AWS콘솔에서 Route53으로 들어간다.
- 도메인과 호스팅 관리를 도와주는 서비스이다.

![img](img/route53.png)

- 대시보드의 도메인 등록을 선택하고 시작하기를 누른다.

![img](img/도메인구매.png)

- 사용하고 싶은 도메인을기입한 후 검색을 누른다.
- 아래 사용하고 싶은 도메인을 선택하고 결제를 진행합니다.
- 본인의 연락처를 기입한 후 계속을 누른다.
- 다음으로 넘어가 연락처 정보를 확인한 후 결제한다.
- 도메인 이름에 따라 가격이 달라질 수 있음을 유의하자
- 도메인을 구매하면 입력한 이메일로 확인 메일이 전송된다.
- 확인 이메일의 링크를 눌러야 도메인이 활성화되니 반드시 활성화 링크를 누르자.

### 다른 사이트를 통한 구매
- https://www.gabia.com 에서도 원하는 도메인을 검색하고 구매할 수 있다.

![img](img/가비아.png)

- 원하는 도메인을 선택하고 신청하기를 누릅니다.

![img](img/도메인선택.png)

- 전화번호와 주소만 입력한 후 결제하기로 넘어갑니다.


### 호스팅 영역 생성
- 도메인을 생성했으면 이 도메인을 위한 호스팅 영역을 생성한다.
- 호스팅 영역에서는 서브 도메인을 생성한다.
- Route 53의 왼쪽 탭에서 호스팅 영역을 누른다.

![img](img/호스팅영역생성.png)

- 이전에 산 도메인 이름을 기입하고 호스팅 생성영역을 누른다.
- 생성된 호스트 영역으로 들어가면 두 개의 기본 레코드가 추가돼있다.

![img](img/기본레코드.png)


### Host Zone(호스트 영역)
- 호스트 영역은 DNS영역파일이다.
- DNS영역을 생성하는 이유는 여러 개의 레코드를 한 곳에서 관리하기 위함이다.

### 레코드(Record)
- 레코드는 쉽게 말하면 이름과 IP를 연결해 놓은 파일 또는 엔트리이다.
- 레모드에는 종류가 여러 개 있는데 호스트 영역을 생성하면 일단 SOA와 NS가 하나씩 생긴다.
#### SOA(Start Of Authority)레코드
- 이 영역을 관리하는 관리자의 정보를 가지고 있는 레코드

#### NS(Name Server)레코드
- 해당 도메인의 IP를 물어볼 서버들을 가지고 있다.

### A레코드
- 해당 도메인을 특정 IP 또는 다른 도메인으로 연결하는 레코드이다.

### 가비아 네임서버 설정하기
- 가비아에 로그인 한 후 My가비아탭으로 이동합니다.
- 가운데 도메인을 눌러 이동합니다.

![img](img/도메인관리.png)

- 구매한 도메인의 관리버튼을 누릅니다.

![img](img/관리설정.png)

- 네임서버의 설정 버튼을 누릅니다.

![img](img/네임서버설정.png)

- route 53에서 등록한 레코드에서 만들어진 트래픽 라우터 대상을 4개 모두 복사한다.

![img](img/라우팅대상.png)

- 가비아에서 네임서버 설정부분에 차례대로 넣되 마지막 .은 빼고 넣어야 한다.

![img](img/가비아네임설정.png)

- 모두 적은 뒤 적용 버튼을 누른다.

### 서브 도메인 만들기
- A레코드를 이용하여 백엔드와 프론트엔드에 서브 도메인을 만들어 연결해주자
- route 53 > 내가 만든 호스팅 영역으로 이동한다.
- 오른쪽 위 레코드 생성 버튼을 누른다.
- 서브도메인 앞에 붙이기 위한 레코드 이름을 설정합니다.
    - 여기서는 예시로 다음과 같이 작성합니다.(꼭 똑같이 작성해야 하는건 아니다.)
    - 프론트엔드에 app.자기도메인
    - 백엔드에서는 api.자기도메인

![img](img/레코드생성.png)

#### 값 설정하기
- 레코드를 생성할 때 값에는 로드밸런서나 IP주소를 넣어줘야 한다.
- EC2 > 인스턴스로 이동해 인스턴스ID를 클릭한다.
- IPv4 주소를 복사해 붙혀넣자

![img](img/ec2퍼블릭ip.png)

```
이렇게 프론트엔드와 백엔드를 연결하는 두 개의 서브 도메인을 만든다.
하지만 연결이 되고 적용되기 까지 24 ~ 48시간이 걸릴 수 있다.
```

![img](img/서브도메인생성.png)

### 백엔드에 요청하는 코드 수정하기
- React에서 스프링부트에 요청하는 주소를 우리가 연결한 서브 도메인 주소로 바꾸자.
- 주소가 담겨있는 api-config.js를 수정하가
```js
let backendHost;

const hostname = window && window.location && window.location.hostname;

if (hostname === "localhost") {
  backendHost = "http://localhost:8080";
} else {
  backendHost = "http://api.<설정한도메인>";
}

export const API_BASE_URL = `${backendHost}`; 
```
- npm run build를 하여 eb에 다시 배포를 진행합니다.

### CORS 문제 수정하기
- WebSecurityConfig클래스에 프론트에서 들어오는 요청 허가하기

```java
configuration.setAllowedOrigins(Arrays.asList(
          "http://localhost:3000",
    		  "http://app.hens-lab.com",
    		  "https://app.hens-lab.com"));
```
- 브라우저에 http://app.본인도메인을 입력하면 접속할 수 있다.

![img](img/결과.png)

## 로드밸런서 설정하기
### 로드밸런서란?
- 서버에 대한 네트워크 트래픽을 효율적으로 분산시켜 여러 서버로 나누어 처리하는 장치 또는 소프트웨어다.
- 로드밸런서를 사용하면 트래픽 부하를 분산시켜 각 서버에 가해지는 부담을 줄이고, 서버가 과부하로 인해 다운되는 것을 방지하여 애플리케이션의 성능과 가용성을 높일 수 있다.
### AWS Elastic Load Balancer(ELB)
- AWS에서 제공하는 로드밸런싱 서비스로, EC2 인스턴스 간 트래픽을 자동으로 분산시킨다.
- AWS ELB는 여러 유형의 로드밸런서를 제공한다.
#### ELB의 종류
- Application Load Balancer(ALB) : L7 로드밸런서로, HTTP 및 HTTPS 트래픽을 처리하며, 애플리케이션 기반 라우팅을 지원한다.
- Network Load Balancer(LAB) : L4 로드밸런서로, TCP 트래픽을 처리하며 대량의 트래픽을 빠르게 분산할 수 있다.
- Classic Load Balancer (CLB): L4 및 L7 로드밸런싱 기능을 제공하지만, 새로운 기능 지원이 제한된다.
```
※ OSI 7계층
- 네트워크 통신 과정을 7개의 계층으로 나눈 모델로, 컴퓨터 네트워크에서 통신이 이루어지는 방식과 각 단계의 역할을 명확히 하기 위해서 설계되었다.
- 각 계층은 독립적이면서도 상호 작용하며, 데이터가 한 계층에서 다른 계층으로 이동하면서 구체적인 통신 기능을 수행한다.
- 각 계층을 L1, L2, L3 이런 식으로 줄여서 부르기도 한다.
- L1: 물리 계층(Physical Layer) 물리적 매체를 통해 비트 전송
- L2: 데이터 링크 계층(Data Link Layer) 프레임 단위의 데이터 전송
- L3: 네트워크 계층(Network Layer) IP 주소 기반 경로 설정 및 라우팅
- L4: 전송 계층(Transport Layer) 신뢰성 있는 전송, 오류 검출, 포트 기반 통신
- L5: 세션 계층(Session Layer) 세션 관리, 대화 제어, 데이터 동기화
- L6: 프레젠테이션 계층(Presentation Layer) 데이터 암호화/복호화, 데이터 형식 변환
- L7: 응용 계층(Application Layer) 사용자와 네트워크 간 인터페이스 제공
```
### Target Group
- 로드밸런서가 트래픽을 분산시킬 대상을 정의하는 그룹이다.
- 로드밸런서에 연결된 인스턴스, 컨테이너, IP 주소 등의 리소스를 그룹으로 묶어 관리하며, 이를 통해 로드밸런서는 트래픽을 효율적으로 분배할 수 있다.

### Target
- 로드밸런서가 트래픽을 보내는 대상이다.
- AWS에서는 여러 종류의 리소스를 타겟으로 사용할 수 있다.
- EC2 인스턴스, Lambda 함수, 컨테이너, IP 주소 등이 타겟이 될 수 있다.

### 타겟그룹 만들기
- [EC2]로 이동하여 왼쪽 아래 [대상그룹]을 클릭한다.

![img](img/로드밸런서연결1.png)

- 대상 유형 선택은 [인스턴스]를 선택한다.
- 대상 그룹 이름을 작성하고 다음으로 넘어간다.

![img](img/로드밸런서연결2.png)

- 라우팅 하려고 하는 인스턴스를 선택한 후 포트를 설정하고 아래에 보류 중인 것으로 포함을 누른다.

![img](img/로드밸런서연결3.png)

- 대상그룹 생성을 누른다.

### Health Check
- Target Group은 각 타겟의 상태를 모니터링할 수 있는 헬스 체크 기능을 제공한다.
- 헬스 체크를 통해 타겟이 정상인지 여부를 판단하고, 트래픽을 정상적인 타겟에만 전달한다.
- 헬스 체크는 주로 HTTP(S) 요청을 통해 진행되며, 설정된 기준에 따라 헬스 체크에 통과하지 못한 타겟은 트래픽 분배에서 제외된다.


### 2. 인스턴스에 요청이 들어오도록 설정
- EC2 > 보안그룹 > 타겟의 보안그룹 ID로 이동한다.
- 인바운드 규칙 편집을 누른다.
- HTTP와 HTTPS에 대한 인바운드 규칙을 추가해준다.
- 소스는 Anywhere-Ipv4로 한다.
- 그리고 규칙 저장을 누른다.

![img](img/로드밸런서연결4.png)

#### 인바운드 규칙
- 네트워크 보안에서 특정 인프라나 시스템으로 들어오는 트래픽을 제어하는 규칙을 말한다.
- 주로 방화벽이나 보안 그룹 설정에서 사용되며, 허용 또는 차단할 트래픽을 정의하는데 활용한다.
- AWS EC2 인스턴스나 네트워크 장비에서 인바운드 규칙을 설정할 때 고려하는 항목
  - 소스(Source) : 어떤 IP 주소 또는 IP 범위에서 오는 트래픽을 허용할지 결정한다.
  - 프로토콜(Protocol) : 허용할 트래픽의 프로토콜을 설정한다. 일반적으로 많이 사용하는 프로토콜로는 TCP, UDP, ICMP등이 있다.
  - 포트(Port) : 특정 애플리케이션이 사용하는 포트를 지정하여 해당 포트로 접근하는 트래픽을 허용하거나 차단할 수 있다. HTTP는 80, HTTPS는 433을 사용한다.


### 3. 로드밸런서 생성하기
- [EC2]의 왼쪽 아래 [로드밸런서]탭으로 이동한다.
- 오른쪽 위에 로드 밸런서 생성 버튼을 누른다.

![img](img/로드밸런서연결5.png)

- Application Load Balancer를 생성한다.

![img](img/로드밸런서연결6.png)

- 로드밸런서의 이름을 설정한다.
- 본인이 알아보기 쉽게 정하면 된다
- 예시
  - frontend-lb
  - backend-lb

![img](img/로드밸런서연결7.png)

- VPC는 기본값을 사용한다.
- 가용영역은 인스턴스가 만들어진 영역을 보고 고르면 된다.
- 2개를 고르라고 하기 때문에 2개를 골라준다.

![img](img/로드밸런서연결8.png)

- 리스너 및 라우팅
- 타겟으로 80번 포트로 전달할 것이다.

![img](img/로드밸런서연결9.png)

- 로드밸런서 생성 버튼을 누른다.

### 도메인에 로드밸런서를 연결한다.
- [Route53] > 호스팅영역으로 가서 본인이 설정한 도메인으로 들어간다.
- A레코드를 누르고 레코드 편집을 누른다.
- 별칭을 활성화 하고 엔드포인트에 [Application/Classic Load Balancer]에 대한 별칭을 선택한다.
- 리전은 로드밸런서를 만든 리전을 선택한다.
- 우리가 만든 로드밸런서를 선택한다.

![img](img/로드밸런서연결10.png)



## HTTPS사용하기

### HTTPS
- HTTP에 SSL(Secure Sockets Layer)를 추가한 프로토콜로, 데이터를 암호화하여 안전하게 통신을 할 수 있도록 만든다.
- HTTPS를 사용하려면 서버가 SSL/TLS 인증서를 설치해야 한다.
- 인증서는 신뢰할 수 있는 인증 기관(CA, Certificate Authority)이 발급하며, 해당 서버가 실제로 그 주체가 맞는지 증명해준다.
- 인증서를 통해 클라이언트는 서버가 신뢰할 수 있는 대상인지 확인한 후 통신을 시작할 수 있다.

### SSL
- HTTPS에서 보안을 제공하는 초기 기술로, 웹 서버와 브라우저 간의 통신을 암호화한다.

### 리액트 api-config.js 수정하기
```js
let backendHost;

const hostname = window && window.location && window.location.hostname;

if(hostname === "localhost"){
    backendHost = "http://localhost:5000";
}else {
    backendHost = "https://api.hens-lab.com";
  }

export const API_BASE_URL = `${backendHost}`
```

### 백엔드/프론트엔드 AWS Certificate Manager를 이용한 https설정
- 콘솔에 certificate manager를 입력하고 이동한다.
- 인증서 요청 버튼을 누른다.

![img](img/ssl인증서발급1.png)

- 퍼블릭 인증서 요청을 통해 요청을 시도한다.


![img](img/ssl인증서발급2.png)


- 도메인 이름에 가비아에서 구매한 도메인을 입력해준다.
- 프론트와 백엔드에 할당한 서브 도메인에 모두 적용을 시켜주기위해 [*.도메인] 형식으로 적는다.
- 나머지는 수정할 것이 없고 요청 버튼을 누른다.

![img](img/ssl인증서발급3.png)

- 검증 대기중 / 아니요/ 부적격이 뜨면 정상이다.

![img](img/ssl인증서발급4.png)

### 백엔드 애플리케이션 HTTPS 설정
- [EC2] > [로드밸런서]로 이동하여 백엔드에서 사용하는 로드밸런서를 클릭하고 리스너 추가를 누른다.
  
![img](img/ssl인증서발급5.png)

- 프로토콜 : https
- 포트 : 443
- 대상그룹 : 본인의 백엔드 타겟
- 추가를 누릅니다.

![img](img/ssl인증서발급6.png)

### 프론트엔드 애플리케이션 HTTPS 설정
- [EC2] > [로드밸런서]로 이동하여 프론트엔드에서 사용하는 로드밸런서를 클릭하고 리스너 추가를 누른다.

- 프로토콜 : https
- 포트 : 443
- 대상그룹 : 본인의 프론트엔드 타겟
- 추가를 누릅니다.

### VPC의 보안그룹 설정하기
- 로드밸런서에 443포트가 접속할수 있도록 하자
- [EC2] >[보안그룹]으로 들어가 VPC보안그룹 ID를 누른다.

![img](img/보안그룹ID.png)

- 인바운드 규칙 편집을 누르고 HTTPS를 추가해준다.
- 규칙저장을 한다.

![img](img/HTTPS.png)

### 브라우저에서 확인하기
- 브라우저에 https://app.도메인 을 입력하고 잘 출력되는지 확인해보자.

![img](img/결과2.png)

## 타 애플리케이션과 어떻게 통합할까??
- 우리의 Todo 애플리케이션을 깃허브의 이슈 기능을 연결한다고 가정해보자.
- 타 애플리케이션을 통합하는 기능은 어떻게 구현해야 할까?
- 가장 간단한 방법은 사용자에게서 깃허브의 아이디와 비밀번호를 받는것이다.
- 사용자가 공유 기능을 최초로 사용할 때, 사용자의 깃허브 아이디와 비밀번호를 입력받고 이를 데이터베이스에 저장한다.
- 이후 사용자가 공유 기능을 사용할 때마다 데이터베이스에 저장된 아이디와 비밀번호로 깃허브에 로그인해 이슈를 가져오는 것이다.
- 하지만 이 방법은 정보가 애플리케이션에 안전하게 저장되는지, 계정 정보를 이용해 다른 정보를 빼가지 않을지  신뢰하기 힘들다.
- 만약 100개의 애플리케이션에 아이디와 비밀번호를 제공했다고 가정했을 때, 한 애플리케이션을 더 이상 사용하고 싶지 않고 이 애플리케이션이 더 이상 내 깃허브에 접근하지 않았으면 좋겠다.
- 비밀번호를 바꿔버리게 되면 나머지 99개의 애플리케이션에서도 사용을 못하게 될 것이다.

## OAuth 2.0
- OAuth 2.0은 다양한 서비스와 애플리케이션 간에 안전하게 자원을 공유할 수 있도록 만들어진 인증 및 권한 부여 프로토콜이다.
- 서드파티 어플리케이션이 자기 자신 또는 리소스 오너를 대신해 HTTP 서비스에 제한된 액세스를 제공하도록 해주는 인가 프레임워크이다.
- 주로 클라이언트 애플리케이션이 사용자 데이터를 요청할 때 사용되며, 사용자가 직접 자격 증명을 제공하지 않아도 타사 서비스에 안전하게 접근할 수 있게 해준다.
- 많은 소셜미디어 플랫폼이 OAuth 2.0 프레임워크를 구현하고 있고, 우리는 비밀번호 대신 OAuth 2.0를 사용해 사용자의 정보에 액세스한다.

### 서드파티 어플리케이션
- 다른 회사나 개발자가 만든 애플리케이션
- 서비스에 대해 사용자가 자신의 계정 정보나 데이터를 공유하거나 통합할 수 있도록 만든 애플리케이션을 의미한다.
- OAuth2에서는 우리의 Todo어플리케이션이 서드파티 어플리케이션이다.

### 리소스
- Todo 어플리케이션은 사용자의 계정 정보를 사용하고자 한다.
- '사용자 정보'가 리소스가 된다.

### 리소스 오너
- 리소스를 가지고 있는 사람 즉, 사용자를 의미한다.

### 제한된 액세스
- '비밀번호'를 이용한 접근과 완전 반대되는 개념이다.
- 서드파티 어플리케이션이 리소스 오너가 허락한 리소스에만 접근할 수 있도록 하겠다는 것이다.
- 예를 들어 사용자는 우리 어플리케이션이 사용자 아이디와 이름만 접근하도록 허락할 수 있다.
- 이 경우 우리 어플리케이션은 사용자의 깃허브 소스 코드나 다른 개인정보에는 접근할 수 없다.

## OAuth 2.0의 주요 개념
1. **리소스 소유자(Resource Owner)**: 자신의 자원에 대한 접근 권한을 가지고 있는 주체, 보통 사용자입니다.
   
2. **클라이언트(Client)**: 리소스 소유자의 데이터를 사용하고자 하는 애플리케이션입니다. 이 클라이언트는 리소스 서버에 직접 접근하지 않고, OAuth 2.0을 통해 인증 및 권한 부여 과정을 거친 후 데이터를 얻습니다.

3. **인증 서버(Authorization Server)**: 리소스 소유자의 동의를 얻고, 액세스 토큰을 발급하는 서버입니다. OAuth 인증 서버는 클라이언트가 적절한 권한을 가졌는지 확인한 뒤 토큰을 발급합니다.

4. **리소스 서버(Resource Server)**: 보호된 리소스를 제공하는 서버입니다. 예를 들어, 사용자의 개인 정보를 저장하고 있는 서버가 해당됩니다. 클라이언트는 액세스 토큰을 통해 이 서버에 접근할 수 있습니다.

5. **액세스 토큰(Access Token)**: 인증 서버에서 발급하는 토큰으로, 클라이언트가 리소스 서버에 요청할 때 이를 사용해 인증을 받습니다. 이 토큰은 유효 기간이 있으며, 권한 범위(scope)를 나타냅니다.

## OAuth 2.0의 흐름

![img](img/OAuth2-1.jpg)

1. 사용자는 Todo 어플리케이션의 브라우저 화면상에서 '깃허브로 로그인하기'같은 버튼을 클릭한다.
2. 이 버튼은 Todo백엔드에게 소셜 로그인 요청을 보낸다.
3. 백엔드는 지정한 소셜 로그인 리소스 서버에 해당하는 인가 페이지로 브라우저를 리다이렉트한다. 이 시점에서 사용자는 더이상 우리 어플리케이션의 화면이 아닌 소셜 로그인의 리소스의 인가 페이지를 보게된다. 이 예제에서는 깃허브의 로그인 페이지가 이에 해당한다.
4. 소셜 로그인의 로그인 화면에서 리소스 오너가 로그인한다.
5. 소셜 로그인의 인가 서버로 로그인 요청이 된다.

![img](img/OAuth2-2.jpg)

6. 5에서 리소스 오너의 로그인 요청을 처리한 인가 서버는 'Todo 어플리케이션을 인가하겠습니까?'와 같이 Todo 어플리케이션에게 접근 권한을 부여하는 페이지로 브라우저를 리다이렉트한다.
7. 리소스 오너는 브라우저상에서 접근을 인가하는 버튼을 클릭한다.
8. 리소스 오너의 인가 요청을 받은 인가 서버는 브라우저를 다시 Todo어플리케이션 페이지로 리다이렉트한다. 이때, 인가 서버는 어떤 URL로 리다이렉트해야 하는지 미리 알고 있다.
9. 클라이언트인 Todo 애플리케이션은 인가 서버에서 받은 요청을 이용해 액세스 토큰을 받을 준비를 한다.

![img](img/OAuth2-3.jpg)

10. 인가 서버에서 받은 요청에는 인증을 위한 여러가지 매개변수가 들어있다. 이런 매개변수를 이용해 클라이언트는 인가 서버에 리소스 오너의 액세스 토큰을 요청한다. 이 액세스 토큰은 Bearer토큰과 같다.
11. 리소스 오너가 클라이언트에게 접근 권한을 이미 부여했으므로, 인가 서버는 클라이언트가 리소스 오너의 리소스를 접근할 수 있도록 액세스 토큰을 반환한다.
12. 액세스 토큰을 받은 클라이언트는 이제 토큰을 이용해 리소스 오너의 리소스에 접근할 수 있다.

※ 주의
- 리소스 서버 또는 리소스 인가 서버는 클라이언트 어플리케이션을 미리 알고있어야 한다. 다시말해, 클라이언트 어플리케이션은 이미 리소스 서버 또는 인가 서버에 등록된 어플리케이션이다.
- 그렇지 않으면 리소스 서버 및 인가 서버의 어떤 API요청도 할 수 없다.
- 클라이언트 어플리케이션이 리소스/인가 서버에 등록 당시 콜백URL을 지정한다.

## 소셜 로그인 백엔드 구현
- 깃허브를 이용해 소셜 로그인을 구현해보자
- 소셜 로그인이란 SSO(Single-Sign-On)의 일종으로 소셜 네트워크의 계정을 이용해 다른 어플리케이션의 계정을 생성하는 기능이다.
- SSO란 하나의 아이디를 이용해 여러개의 독립된 어플리케이션에 로그인할 수 있는 인증 메커니즘을 의미한다.
- 예를 들어 깃허브 아이디로 여러 다른 어플리케이션에 로그인 할 수 있다는 점에서 소셜 로그인은 SSO의 일종이다.
- 그리고 이 소셜 로그인을 구현하는 방법 중 하나가 바로 OAuth2다.

## 소셜 로그인 사이트에서 클라이언트 어플리케이션 생성하기.
- 깃허브에 로그인 한후 오른쪽 위 아이콘을 누른다.
- [Setting] > [Developer Setting]을 클릭해서 들어간다.
- [OAuth Apps] > [New OAuth app]을 선택한다.
- 우리의 어플리케이션을 등록하기 위한 작업이다.

![img](img/OAuth2-4.png)

![img](img/OAuth2-5.png)

### Homepage URL
- Todo 백엔드 어플리케이션

### Authorization callback URL
- 백엔드 어플리케이션에 존재할 콜백 포인트이다.
- 콜백 포인트를 http://localhost:5000/oauth2/callback으로 설정하자.

**작성 후 Register application을 클릭하자.**

![img](img/OAuth2-6.png)

- Client ID를 반드시 메모해놓자.
- Generate a new client secret를 클릭해 시크릿을 발행한 후 메모해놓자.
- 리소스 오너의 액세스 토큰을 요청할 때, 리소스 오너의 리소스를 요청할 때 우리 어플리케이션은 Client ID와 Secret을 이용해야 한다.

## OAuth2.0 라이브러리 추가
```groovy
// https://mvnrepository.com/artifact/org.springframework.security/spring-security-oauth2-client
	implementation group: 'org.springframework.security', name: 'spring-security-oauth2-client', version: '6.3.1'
```

## application-dev.yml에 OAuth2.0설정
```yml
spring:
  security:
    oauth2:
      client:
        registration:
          github:
            clientId: <CLIENT_ID>
            clientSecret: <CLIENT_SECRET>
            redirectUri: "{baseUrl}/oauth2/callback/{registrationId}"
            scope:
              - user:email
              - read:user
    provider:
      github:
        authorization-uri: https://github.com/login/oauth/authorize
```

## Todo 백엔드 OAuth 2.0 엔드포인트 설정
- 백엔드에서 소셜 로그인 요청을 받기 위한 엔드포인트를 설정해야한다.
- 이 설정은 WebSecurityConfig에서 스프링 시큐리티가 제공하는 메서드를 이용하면된다.

```java
package com.example.demo.config;

import com.example.demo.security.JwtAuthenticationFilter;

@Configuration
@EnableWebSecurity
public class WebSecurityConfig {
   
   @Autowired
   private JwtAuthenticationFilter jwtAuthenticationFilter;
   
   @Bean
   protected DefaultSecurityFilterChain securityFilterChain(
         HttpSecurity http) throws Exception {

      http
         .cors(corsConfigurer -> corsConfigurer.configurationSource(corsConfigurationSource()))
         .csrf(csrfConfigurer -> csrfConfigurer.disable())
         .httpBasic(httpBasicConfigurer -> httpBasicConfigurer.disable())
         .sessionManagement(sessionManagementConfigurer ->
               sessionManagementConfigurer.sessionCreationPolicy(SessionCreationPolicy.STATELESS)
           )
         
         .authorizeHttpRequests(authorizeRequestsConfigurer -> 
            authorizeRequestsConfigurer
            /////////////추가//////////////////
            .requestMatchers("/", "/auth/**","/oauth2/**").permitAll()// /oauth2경로도 인증없이 허용
            /////////////추가//////////////////
            .anyRequest().authenticated()
         )
         /////////////추가//////////////////
         .oauth2Login();//oauth2 로그인 설정
         /////////////추가//////////////////

      http.addFilterBefore(jwtAuthenticationFilter, UsernamePasswordAuthenticationFilter.class);

      return http.build();
   }

   @Bean
   public CorsConfigurationSource corsConfigurationSource() {
      CorsConfiguration configuration = new CorsConfiguration();
      //React 애플리케이션이 실행되는 출처에서 오는 요청을 허용
      configuration.setAllowedOrigins(Arrays.asList("http://localhost:3000",
    		  "http://app.hens-lab.com",
    		  "https://app.hens-lab.com"));
      //HTTP메서드 허용
      configuration.setAllowedMethods(Arrays.asList("GET", "POST", "PUT", "DELETE", "OPTIONS"));
      //모든 헤더를 허용
      configuration.setAllowedHeaders(Arrays.asList("*"));
      //쿠키나 인증 정보를 포함한 요청을 허용
      configuration.setAllowCredentials(true);
      
      //모든 경로에 대해 CORS설정을 적용
      UrlBasedCorsConfigurationSource source = new UrlBasedCorsConfigurationSource();
      source.registerCorsConfiguration("/**", configuration);
      return source;
   }
}
```
### 어플리케이션 실행
- gradle을 이용하여 어플리케이션을 실행할 수 있다.
```groovy
./gradlew bootRun --args='--spring.profiles.active=dev --server.port=5000'
```
- 브라우저상에서 http://localhost:5000/oauth2/authorization/github 를 치고 들어가보면 깃허브의 로그인 화면으로 리다이렉트되는 것을 확인할 수 있다.

![img](img/OAuth2-7.png)

- 개발자도구를 확인해보면 리다이렉트가 여러 번 일어났다는 것을 확인할 수 있다.
- 첫번째로 http://localhost:5000/oauth2/authorization/github로 들어갔을 때 백엔드는 브라우저를 https://github.com/login/oauth/authorize로 리다이렉트한다.
- 사용자가 로그인하지 않은 상태이므로 깃허브는 이를 다시 https://github.com/login로 리다이렉트한다.

- 현재 소셜로그인 요청과 리다이렉트 부분을 구현한셈이다.
- 어느 엔드포인트를 사용할 것인지, 어디로 콜백할 건지만 알려주면 나머지는 스프링 시큐리티 OAuth 2.0라이브러리가 해결해준다.
- authorize 요청을 클릭하면 백엔드가 리다이렉트 당시 어떤 쿼리를 매개변수에 추가했는지 알 수 있다.
- client_id,scope,redirect_uri를 확인해보자.
- 이 매개변수의 값들은 우리가 설정한 application-dev.yml파일에서 온것이다.
- 이처럼 클라이언트 어플리케이션은 쿼리 매개변수를 이용해 깃허브의 인가 서버에게 자신이 어떤 클라이언트인지 어디로 리다이렉트 해야 하는지 어떤 리소스에 접근이 필요한 것인지 알려주는것이다.

### 로그인해보기
- 로그인을 하고 나서 Authorize를 누르면 인가가 된다.
- http://localhost:5000/oauth2/callback/github로 리다이렉트하려고 했으나 페이지가 존재하지 않아 HTTP 404를 반환한다.

### WebSecurityConfig 코드 추가하기
```java
.oauth2Login()
.redirectionEndpoint()
.baseUri("/oauth2/callback/*");
```
- http://localhost:5000/oauth2/callback/*으로 들어오는 요청을 redirectionEndpoint에 설정된 곳으로 리다이렉트하라는 뜻이다.
- redirectionEndpoint에 아무 주소도 넣지 않았다면 베이스 URL인 http://localhost:5000으로 리다이렉트한다.

## 소셜 로그인 후 자동으로 회원가입
- 사용자가 깃허브로 로그인을 하면 백엔드가 액세스 토큰을 요청해 사용자의 액세스 토큰을 발행하고, 액세스 토큰을 이용해 사용자의 게정 정보를 가져오는 것이다.
- 깃허브가 콜백 엔드포인트 요청을 보낼 때, 해당 사용자의 계정이 이미 있는지 확인하고 없다면 새로 생성해주는 부분을 구현해보자.

### application-dev.yml에 코드 추가하기
```yml
provider:
  github:
    authorization-uri: https://github.com/login/oauth/authorize
    token-uri: https://github.com/login/oauth/access_token
    user-info-uri: https://api.github.com/user
```

### token-uri
- 깃허브에 액세스 가능한 액세스 토큰을 받아오기위한 주소

### user-info-uri
- 유저의 정보를 가져오기 위한 주소이다.


- 유저의 정보를 가져오기 위해서는 액세스 토큰이 필요하므로 우리는 token-uri를 이용해 먼저 액세스 토큰을 받은 후, user-info-uri로 사용자의 정보를 요청할 때 토큰을 함께 보낸다.
