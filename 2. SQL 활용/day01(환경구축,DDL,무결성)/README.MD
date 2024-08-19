## DB(DataBase) 
- 구조화된 정보, 데이터의 조직화된 모음, 일반적으로 컴퓨터에 전자적으로 저장이 되고 데이터베이스관리시스템에 의해 제어된다.

## DBMS(DataBaseManagementSystem)
- 데이터베이스와 사용자 또는 프로그램 간의 매개체 역할을 하여 사용자가 정보의 구성,검색,수정,삭제와 같은 관리를 할 수 있게 해줍니다.

## DBMS의 종류
1. 계층형 데이터베이스(HDBMS)
    - 폴더와 파일 등의 계층 구조로 데이터를 저장하는 방식
    - 데이터의 관계를 트리 구조로 정의, 부모-자식 형태를 가짐
    - 하드디스크,DVD파일 시스템 등
    - 데이터 액세스 속도가 빠름
    - 데이터의 사용량 쉽게 예측
    - 상하 종속적인 관계로 구성되어 초기 세팅 후 프로세스 수용이 어려움
2. 네트워크형 데이터베이스(NDBMS)
    - 데이터 구조를 네트워크상의 노드 형태로 논리적이게 표현한 데이터 모델, 각각의 노드를 서로 대등한 관계로 구성한 시스템
    - 계층형 데이터베이스의 데이터 중복 문제 해결, 상하 종속적 관계 해결
    - 추후 변경시 복잡한 구조로 인해 변경이 어려움
    - 데이터 종속성을 해결하지 못함
3. 관계형 데이터베이스(RDBMS)
    - 행(Column)과 열(Rows)을 가지는 표 형식 데이터를 저장하는 형태의 데이터베이스
  
![image](https://github.com/to7485/Web1500/assets/54658614/bd4f8174-f439-4002-b5fb-588008c9ab94)

    - SQL을 이용하여 관리 및 접근
    - 관계 대수에서 착안하여 만들어짐
    - 다양한 용도로 사용 가능(범용성), 높은 성능
    - 데이터 무결성 보장, 높은 신뢰성
    - 명확한(= 엄격한) 스키마 정의
    - 정규화에 따른 갱신 비용 최소화
    - 데이터의 분류, 정렬, 탐색 속도가 빠름
    - 관계를 통해 각 데이터를 중복없이 한 번만 저장
    - 대량의 데이터 입력 처리
    - 갱신이 발생한 테이블의 인덱스 생성 및 스키마 변경
    - 컬럼 확장 어려움 ▶️ 유연성 부족
    - 데이터베이스 부하 분석이 어려움
    - 수평 확장의 어려움 ▶️ 데이터베이스 저장 방식으로 인해 수직 확장만 지원


### 인기있는 RDBMS 소프트웨어
- MySQL : 오픈소스 커뮤니티에서 개발
- Microsoft SQL Server : 마이크로소프트에서 개발, 윈도우 플랫폼에서만 동작
- PostgreSQL : 오픈소스 커뮤니티에서 개발
- Oracle Database : 오라클에서 개발, 가장 많이 사용하는 DBMS
- DB2 : IBM이 개발, 한동한 IBM 컴퓨터에서만 구동이 가능했다.
등등

```
회사에 가서 다른 DBMS를 사용할 수 도 있지만 프로그래밍언어 처럼 한가지를 배워놓으면 다른 DBMS도 금방 습득할 수 있다.
```

## 오라클 DBMS 설치
https://www.oracle.com/database/technologies/xe-prior-release-downloads.html

- 돋보기 버튼 누르고  XE Prior Release Archive 입력하고 검색하기
- XE Prior Release Archive 클릭하기

![20230406_134017](https://user-images.githubusercontent.com/54658614/230273656-8c50ea22-68c2-49e7-8f39-fdc8de10be0a.png)

- 운영체제에 맞는 버전 다운로드 하기

![image](https://user-images.githubusercontent.com/54658614/230274134-c09aeefb-0b7d-4241-90c9-7a709fa389b7.png)

- 압축 풀고 폴더 안에 있는 setup.exe 실행하기

![image](https://user-images.githubusercontent.com/54658614/230274775-60330aba-0bed-4f43-a7f2-aaa557ec13c6.png)

- 동의 눌러주고 next 진행한다.

![image](https://user-images.githubusercontent.com/54658614/230274935-47d28b33-9579-414b-ad1d-e12f8aec893a.png)

- 설치할 경로를 정해줄 수 있는데 따로 바꿔줄 필요는 없다.(항상 필요한 용량은 확보해두자)

![image](https://user-images.githubusercontent.com/54658614/230275196-3d0c701d-3d0c-4084-a4c0-bc6ebc85310e.png)

- 혹시 DBMS를 지웠다가 다시 까는 경우 이러한 문구가 뜰 수 있다. 

![image](https://user-images.githubusercontent.com/54658614/230275283-67444bb5-02db-4007-b56c-d202bbd3026b.png)

- 설치했던 곳에 있는 폴더를 제거 하고 진행해주자

![image](https://user-images.githubusercontent.com/54658614/230275348-6f5ea512-ad8b-47dc-8e15-074a42e51cca.png)

- DB에 접속할 계정의 비밀번호를 설정해야 한다. 까먹지 않을 비밀번호로 설정하자.

![image](https://user-images.githubusercontent.com/54658614/230275461-9b9e5730-b1e6-44b9-8f82-1060c12a32d0.png)

- 그리고 쭉 진행해준다.

- 설치를 모두 마치면 다음과 아이콘을 더블클릭하여 실행할 수 있다.

![image](https://user-images.githubusercontent.com/54658614/230275813-e86781f6-4251-4534-b196-2e2750e2221e.png)

- 실행을 하면 다음과 같은 화면이 나오는데 실행이 안될 수 도 있다.

![image](https://user-images.githubusercontent.com/54658614/230275882-c3a1fbe5-f768-4eae-bc7e-86ae8cd550f0.png)

- 이러한 오류가 발생할 수 있다.

![image](https://user-images.githubusercontent.com/54658614/230276206-104cb7ae-9bf5-40b9-97d1-9281b08cbac7.png)


![image](https://user-images.githubusercontent.com/54658614/230276002-0da8350c-ec68-429f-8cf1-8afd45647ba2.png)

![image](https://user-images.githubusercontent.com/54658614/230276054-7835d3f8-dc93-435f-a0a1-5231886b99a0.png)

- 이렇게 바꿔주자

![image](https://user-images.githubusercontent.com/54658614/230276265-885421ae-af8b-4092-ab5d-d793754b2657.png)

## DBeaver IDE 설치하기
- IDE : 통합 개발 환경(IDE)이란 프로그래머가 소프트웨어 코드를 효율적으로 개발하도록 돕는 소프트웨어 애플리케이션입니다.
- 이는 소프트웨어 편집, 빌드, 테스트, 패키징과 같은 기능을 사용하기 쉬운 하나의 애플리케이션에 통합하여 개발자 생산성을 높입니다.

※ DBeaver는 JDK 가 설치되어있지 않으면 작동을 하지 않는다.

DBeaver 홈페이지 : https://dbeaver.io/

![image](https://user-images.githubusercontent.com/54658614/230538837-c45cd02a-6a1c-40f6-aea6-8a4963a98544.png)


- 스크롤을 아래로 내려서 이전버전을 받을 수 있는 아카이브로 들어가기

![image](https://user-images.githubusercontent.com/54658614/230538904-603b27c8-c8ba-45f7-b5c6-67375a0f96de.png)

- 다운로드 받고싶은 버전을 찾아서 들어간다.

![image](https://user-images.githubusercontent.com/54658614/230538950-2bc68b34-8342-4dc5-b197-14cef9b19079.png)

- 본인의 운영체제에 맞게 다운로드를 해준다.

![image](https://user-images.githubusercontent.com/54658614/230539001-37599182-a5e1-483a-8f0e-b366df1c94d0.png)

- util 폴더에 압축을 풀고 사용하면 된다.

![image](https://user-images.githubusercontent.com/54658614/230539081-19ddf391-5326-49f7-9cb9-79ef62a6b9c3.png)

- 처음 DBeaver를 켜면 다음과 같은 창이 뜬다.

![image](https://user-images.githubusercontent.com/54658614/230539138-9f00132d-1b55-4ece-a541-5a06cbd79309.png)

- 뜨지 않는다면 왼쪽 위에 플러그 모양 버튼을 눌러주자

![image](https://user-images.githubusercontent.com/54658614/230539187-6d7a4044-4694-4153-a7d6-a0e90affa78c.png)

- 빈칸을 다음과 같이 채워넣어주면 된다.
    - Host : Ip주소
    - Database : Service Name을 설정해야 하는데 xe라고 적는다.
        - Service Name : 데이터베이스에 원격으로 접속할 때 사용하는 TNS alias
        - 클라이언트의 tnsnames.ora파일에 기록된다.
    - User name : hr
    - Password : hr
#### 익스프레스 에디션(XE)
- 무료로 사용할 수 있는 버전으로 상용으로 사용하려면 기능상 제한이 있음

![image](https://user-images.githubusercontent.com/54658614/230539317-eb33e20e-c975-4591-b1c8-9e2c092d87e3.png)

- 아마 처음 Oracle을 설치했다면 hr 계정이 잠겨있을 것이다.

## 데이터베이스 사용자 계정
- 데이터베이스의 생성 및 관리, 데이터의 삽입, 수정, 변경 및 삭제를 수행하는 데이터베이스 계정을 의미한다.

### 관리자 계정(Administrator)
- 데이터베이스의 생성과 관리를 담당하는 슈퍼유저(Super User)계정이며, 정의, 생성, 삭제 등의 작업이 가능하다.
- 오라클 데이터베이스 생성시 관리자 계정인 SYS와 SYSTEM 계정이 자동으로 생성되어 있다.
- 데이터베이스에 대한 모든 권한과 책임을 가지는 계정이다.

### 일반계정
- 데이터베이스에 대하여 명령(Query), 갱신, 보고서 작성 등의 작업을 수행할 수 있는 계정
- 일반 계정은 업무에 필요한 최소한의 권한만 가지는 것을 원칙으로 한다.
		
### hr 계정 잠금 풀기

win + r 키를 눌러 실행을 켜고 cmd를 입력하여 프롬포트를 연다. 

![image](https://user-images.githubusercontent.com/54658614/230539594-b6527235-5bf4-4639-b569-c856d5eb2ece.png)

- sqlplus : db접속하기
	- system 계정으로 로그인을 하자
	
![image](https://user-images.githubusercontent.com/54658614/230539678-2fd407ff-d9cc-4062-8d11-86f2a838d1d9.png)

- 계정 잠금 풀기 : Alter user 계정명 account unlock;
- 계정 비밀번호 설정하기 : alter user 계정명 identified by 비밀번호;

![image](https://user-images.githubusercontent.com/54658614/230539865-a33af57e-0cd6-4419-8e1b-e195be2d5d54.png)

- 디비버로 돌아와서 TestConnetion을 누르면 드라이버를 요구한다.
- 오라클 설치된 곳 안에 라이브러리가 있기 때문에 경로만 잡아주자.

![image](https://user-images.githubusercontent.com/54658614/230539995-5daa712a-9c47-415a-8c71-69f1af30fa0b.png)

![image](https://user-images.githubusercontent.com/54658614/230540093-c5bf48ed-4662-4a82-8164-4f261564c4bc.png)

### ojdbc
- 데이터베이스와의 통신을 담당하는 인터페이스
- Oracle Java DataBase Connectivity의 약자
- Oracle 전용의 jdbc 라이브러리이다.
- Oracle에서 제공하는 오라클DB를 관리할 수 있도록 해주는 JDBC
- MS SQL, MySQL등과 같은 데이터베이스에 알맞은 JDBC 드라이버를 구현하여 제공
- JDBC 드라이버의 구현체를 이용해서 특정 벤더의 데이터베이스에 접근할 수 있다.

### JDBC
- JDBC(Java Database Connectivity)는 Java 기반 애플리케이션의 데이터를 데이터베이스에 저장 및 업데이트하거나,
- 데이터베이스에 저장된 데이터를 Java에서 사용할 수 있도록 하는 자바 API이다.
- Java 애플리케이션에서 데이터베이스에 접근하기 위해 JDBC API를 사용하여 데이터베이스에 연동할 수 있으며,
- 데이터베이스에서 자료를 쿼리(Query)하거나 업데이트하는 방법을 제공한다.
- JDBC API는 java.sql.\* 패키지에 의해 구현됩니다.
<br>
ok를 누르면 오라클과 DBeaver의 연결이 완료된다.

연결된 오라클을 펼쳐보면 여러가지 샘플 테이블들을 볼 수 있다.

![image](https://user-images.githubusercontent.com/54658614/230540232-2a4e0e59-3486-4d1f-a91b-aa27ac508ea2.png)

스크립트를 생성하여 여러가지 쿼리문들을 작성할 수 있다.

![image](https://user-images.githubusercontent.com/54658614/230540303-417e24ee-0ef6-4d32-bdca-57061b2bf603.png)

- Select Data Source 창이 뜸 오라클 선택 F2 눌러서 이름 day00로 수업 날짜에 맞춰 변경
- 글자가 잘안보인다면 windows > Preferences > font 검색 > Colors and Fonts > Basic > Text Font 더블클릭 > 글꼴과 크기 변경 가능

## 스키마
- 스키마란?
1. 스키마는 데이터베이스의 구조와 제약 조건에 관한 전반적인 명세를 기술한 메타데이터의 집합이다.
2. 스키마는 데이터베이스를 구성하는 데이터 개체(Entity), 속성(Attribute), 관계(Relationship) 및 데이터 조작 시 데이터 값들이 갖는 제약 조건 등에 관해 전반적으로 정의한다.
3. 스키마는 사용자의 관점에 따라 외부 스키마, 개념 스키마, 내부 스키마로 나눠진다.

![image](https://github.com/to7485/DBMS1900/assets/54658614/ace7ecdc-7205-4dd6-af09-b51108f5d130)

- 스키마의 특징
1. 스키마는 데이터 사전(Data Dictionary)에 저장되며, 다른 이름으로 메타데이터라고도 한다.
2. 스키마는 현실 세계의 특정한 한 부분의 표현으로서 특정 데이터 모델을 이용해서 만들어진다.
3. 스키마는 시간에 따라 불변인 특성을 갖는다.
4. 스키마는 데이터의 구조적 특성을 의미하며, 인스턴스에 의해 규정된다.

### 스키마의 종류
- 스키마는 사용자의 관점에 따라서 외부, 개념, 내부 스키마로 구분하게 됩니다.

1. 개념스키마 : 전체적인 뷰
	- 조직체 전체를 관장하는 입장에서 DB를 정의한 것
	- 관계, 제약조건, 접근권한, 보안정책, 무결성 규칙에 관한 사항을 포함하고 있다.
	- 따라서 개념스키마를 '스키마'라고 칭하기도 하며, DB전체를 기술한것이기 때문에 한 개밖에 존재할 수 없다.

2. 내부스키마 : 물리적인 저장장치 입장에서 DB가 저장되는 방법을 기술한 것
	- 구체적인 개념으로 스키마를 디스크 기억장치에 물리적으로 구현하기 위한 방법을 기술한 것
	- 데이터베이스의 물리적 저장구조를 정의
	- 디스크에 어떤 구조로 저장할 것인가
	- 데이터의 실제 저장방법을 기술
	- 물리적인 저장장치와 밀접한 계층
	- 시스템 프로그래머나 시스템 설계자가 보는 관점의 스키마

3. 외부스키마 : 사용자 뷰
	- 사용자나 응용 프로그래머가 개인의 입장에서 필요한 데이터베이스의 논리적 구조를 정의
	- 실세계에 존재하는 데이터들을 어떤 형식, 구조, 배치 화면을 통해 사용자에게 보여줄 것인가
	- 전체 데이터베이스의 한 논리적 부분 -> 서브 스키마
	- 하나의 데이터베이스에는 여러 개의 외부 스키마가 존재할 수 있다.
	- 예를들어 '운전면허시험'에 대한 전반적인 정보를 얻고자 할 때, 누구는 '운전면허시험'이라고 검색하고, 누구는 '운전면허증', 누군가는 '운전면허필기시험'이라고 검색할 것이다.
	- 이것이 외부 스키마는 여러개 존재할 수 있다는 의미이다.
	- 응용 프로그래머는 C,JAVA등의 언어를 이용해서 DB에 접근한다.

## SQL문
- 구조화된 질의언어(Structured Query Language)의 약자로 DBMS 상에서 데이터를 읽고 쓰고 삭제하는 등 데이터를 관리하기 위한 일종의 프로그램 언어이다.
- C나 Java같은 일반 프로그래밍 언어는 절차적 언어라고 할 수 있는데 반해 SQL은 집합적 언어이다.
- 집합적 언어는 데이터를 특정 집합 단위로 분류해 이 단위별로 한 번에 처리하는 언어이다.
- RDBMS의 표준 언어로 SQL을 채택했고, 표준 SQL문만 학습하면 오라클은 물론 MSSQL, DB2등 여러 DBMS에서 동일하게 사용할 수 있다는 뜻이다. 물론 DBMS별로 독특한 기능이 있지만, 다른 프로그래밍 언어에 비해 그 차이는 미미하다.
- SQL문장은 대소문자를 구별하지 않는다.
- 한줄 또는 여러줄에 걸쳐 입력하는 것이 가능
- SQL문장의 끝은 세미콜론(;)으로 맺어야 한다. 

## SQL문장의 종류
1. DDL(Data Definition Language) : 데이터 정의어
    - 데이터베이스 객체를 관리하는 언어이다.
2. DML(Data Manipulation Language) : 데이터 조작어
    - 데이터 삽입, 조회,삭제, 갱신 등 실제로 데이터를 조작하는 언어이다.
    - 개발자 입장에서 가장 많이 사용하는 SQL이다.
3. DCL(Data Controll Language) : 데이터 제어어
    - grant, revoke등의 키워드를 가지는 문장
4. TCL(Transaction Controll Language) : 트랜잭션 제어어
    - commit, rollback, savepoint
    
## DDL(Data Definition Language) : 데이터 정의어
- 데이터베이스 객체를 생성, 삭제, 변경하는 언어이다.
  1. CREATE : 테이블이나 인덱스, 뷰 등 데이터베이스 객체를 생성한다.
  2. DROP : 생성된 데이터베이스 객체를 영구히 삭제
  3. ALTER : 이미 생성된 데이터 베이스 객체를 수정
  4. TRUNCATE : 테이블의 데이터를 통째로 삭제

### 개발 현장에서의 DDL의 사용
```
실제 일을 하면 DDL을 사용하는 일은 그리 많지 않다.
보통 데이터베이스 객체의 관리는 DBA(데이터베이스 관리자)나 별도 관리 인원이 담당한다.
각 개발자가 공통으로 사용하고 있는 테이블을 마음대로 삭제하고 생성하게 되면 프로젝트를 원활이 진행할 수 없을것이다.

프로젝트의 규모에 따라 다르긴 하지만, 일반적인 SI나 SM 프로젝트들은 개발 DB와 운영DB를 별도로 분리한 후, 개발자들에게는 개발DB만 접속할 수 있는 권한을 주고, 데이터베이스 객체의 관리는 별도 인원이 한다.

프로젝트마다 다르겠지만 일반적인 개발자들은 DDL명령어를 실행할 수 없게 할 때가 많다^^
```

## 테이블
- 행과 열로 이루어진 데이터의 집합을 테이블이라고 한다. 엑셀을 켜고 보는 모양과 매우 흡사하다.
- 일반적인 데이터베이스에서는 행과 열만 있으면 테이블이라고 하지만, 관계형데이터베이스에서는 특별한 제약을 추가해서 릴레이션(relation)이라고 부른다.

![image](https://user-images.githubusercontent.com/54658614/230540594-e2065530-0123-4a00-8b96-c3cc29efc3ce.png)

## 행(row)
- 테이블을 구성하는 데이터들 중 가로로 묶은 데이터셋을 의미한다. 일반적으로 한 명에 대한 정보를 가지고 있다.
- 이 또한 관계형 데이터베이스에서는 튜플(tuple), 또는 레코드(record)라는 이름으로 불린다.
- 행의 수를 기수(Cardinality) 라고 한다.

## 열(column)
- 테이블을 구성하는 데이터들 중 세로로 묶은 데이터넷을 의미한다. 일반적으로 열은 그 테이블의 속성을 의미한다.
- 열을 구성하는 값들은 같은 도메인(domain)으로 되어있다. 이 또한 관계형 데이터베이스에서는 속성(attribute)라는 이름으로 불린다.
- 열의 수를 차수(Degree)라고 한다.

## 도메인(domain) 
- 하나의 속성이 취할 수 있는 동일한 유형의 데이터 집합을 의미한다.
- 예를들어 성별을 저장하기로 했으면 남,여에 대한 데이터만 들어올 수 있다.

## 자료형(데이터타입)
- 데이터 타입이란 컬럼이 저장되는 데이터의 유형을 말하며, 오라클에서는 기본으로 제공되는 기본 데이터 타입이 있다.

### 문자 데이터 타입
- 문자나 문자열 데이터는 문자형 데이터에 속하며, 오라클에서 제공하는 문자형은 다음과 같다.
<table>
<tr>
	 <th>데이터타입</th>	
	 <th>특징</th>
</tr>
<tr>
	<td>CHAR(n)</td>
	<td>고정길이 문자 / 최대 2000byte / 디폴트 값은 1byte </td>
</tr>
<tr>
	<td> VARCHAR2(n)</td>
	<td>가변길이 문자 / 최대 4000BYTE / 디폴트 값은 1byte </td>
</tr>
<tr>
	<td>NCHAR(n)</td>
	<td>고정길이 유니코드 문자(다국어 입력가능) / 최대 2000byte / 디폴트 값은 1byte </td>
</tr>
<tr>
	<td> NVARCHAR(n)</td>
	<td>가변길이 유니코드 문자(다국어 입력가능) / 최대 2000byte / 디폴트 값은 1byte</td>
</tr>
</table>

- 가변길이라 함은 실제 입력된 데이터 길이에 따라 크기가 변해 정해지는 것을 말한다.
- 예를들어 VARCHAR2(10)으로 선언하면, 10byte까지 데이터를 입력할 수 있지만, 'bac'라는 세글자만 들어왔을 때 실제 길이는 3byte가 된다.
- 공간효율적인 측면에서 VARCHAR2를 사용하는 것이 좋다.
- 영어는 글자당 1byte, 한글은 2byte이다.

### 숫자 데이터 타입
- 대부분 NUMBER형을 사용한다.
<table>
<tr>
	 <th>데이터타입</th>	
	 <th>특징</th>
</tr>
<tr>
	<td>NUMBER(P,S)</td>
	<td>가변숫자 / P (1 ~ 38, 디폴트 : 38) / S (-84 ~ 127, 디폴트 값 : 0)  / 최대 22byte </td>
</tr>
<tr>
	<td>FLOAT(P)</td>
	<td>NUMBER의 하위타입 / P (1~128 .디폴트 : 128) / 이진수 기준 / 최대 22byte </td>
</tr>
<tr>
	<td>BINARY_FLOAT</td>
	<td>32비트 부동소수점 수 / 최대 4byte </td>
</tr>
<tr>
	<td> BINARY_DOUBLE</td>
	<td> 64비트 부동소수점 수 / 최대 8byte </td>
</tr>	
</table>

- 숫자타입은 4가지가 있긴 하지만 NUMBER형만 사용할 때가 많다.
- NUMBER(5)는 12345를 나타낼수 있다.
- NUMBER(5,2)는 123.45를 나타낼 수 있다.
- 다른 DBMS는 INTEGER와 같은 정수형, DECIMAL과 같은 실수형을 제공한다.
- 오라클도 이런 타입으로 작성하는 것이 가능하지만 내부에서는 모두 NUMBER로 변환되어 생성된다.

### 날짜 데이터 타입
<table>
<tr>
	 <th>데이터타입</th>	
	 <th>특징</th>
</tr>
<tr>
	<td> DATE</td>
	<td>BC 4712년 1월 1일부터 9999년 12월 31일, 연, 월, 일, 시, 분, 초 까지 입력 가능</td>
</tr>
<tr>
	<td>TIMESTAMP</td>
	<td>연도, 월, 일, 시, 분, 초 + 밀리초까지 입력가능</td>
</tr>
</table>

- 가장 일반적이고 많이 사용하는 날짜 데이터 타입은 DATE이며 연,월,일과 시,분,초까지 입력 가능하다.
- TIMESTAMP는 초 단위를 더 세부적으로 입력할 수 있다.

### LOB데이터 타입
- LOB은 'Large OBject'의 약자로 대용량 데이터를 저장할 수 있는 데이터 타입이다.

|데이터 타입|설명|
|------|-----|
|CLOB|문자형 대용량 객체, 고정길이와 가변길이 문자 집합 지원, 최대 크기는 (4GB)|
|NCLOB|유니코드(다국어)를 포함한 문자형 대용량 객체, 최대 크기는 (4GB)|
|BLOB|이진형 대용량 객체, 최대 크기는(4GB)|
|BFILE|대용량 이진 파일에 대한 로케이터(위치,이름)저장 최대 크기는(4GB)|

## 제약조건
- 제약조건이란, 테이블에 문제가 되는 결함이 있는 데이터가 입력되지 않도록 미리 지정해둔 조건입니다.
- 제약조건은 테이블을 생성할 때 함께 설정할 수 있고, 추후에 생성하거나 변경할 수 도 있습니다.
```
※ 이미 데이터가 포함되어 있는 상황에서 제약조건을 함부로 바꾸기 어려우므로 사전에 테이블 설계를 잘 해두는 편이 좋다.
```

### NOT NULL
```sql
컬럼명 데이터타입 NOT NULL;
```
- 컬럼을 정의할 때 NOT NULL 제약조건을 명시하면 해당 컬럼에는 반드시 데이터를 입력해야 한다.
- 즉 반드시 값이 들어 잉ㅆ어야 하는 컬럼에는 NOT NULL제약조건을 만들어 사용한다.

### UNIQE
```sql
컬럼명 데이터타입 UNIQUE;
또는
CONSTRAINTS 제약조건명 UNIQUE(컬럼명,...);
```
- 해당 컬럼에 들어가는 값이 유일해야 한다는 의미이다.
- 즉, 중복되는 값을 허용하지 않는다.
- NOT NULL을 같이 명시하면 해당 컬럼에 들어오는 값은 유일함은 물론 반드시 입력해야 한다.

### PRIMARY KEY(기본키)
- 보통 테이블에 키를 생성했다라고 할 때, 이는 기본키를 의미한다.
- 기본키는 UNIQUE와 NOT NULL 속성을 동시에 가진 제약조건으로, 테이블 당 1개의 기본키만 생성할 수 있다.
```sql
컬럼명 데이터타입 PRIMARY KEY;
또는
CONSTRAINTS 제약조건명 PRIMARY KEY(컬럼명,...);
```
### FOREIGN KEY(외래키)
```sql
CONSTRAINT 외래키명 FOREIGN KEY(컬럼명, ...)
REFERENCES 참조 테이블(참조 테이블 컬럼명, ...);
```
- 부서의 정보는 부서테이블에 저장이 되어있고, 사원 테이블에는 부서번호만 저장을 했을때 신입사원이 입사했을 때 잘못된 부서번호를 입력하는 오류를 범할 수 있다.
- 외래키를 설정해놓으면 부서정보에 없는 부서번호를 입력하려고 할 때 오라클은 오류를 발생시켜 잘못된 데이터가 입력되는 것을 방지한다.
- 삭제에서도 마찬가지이다. 사원이 있는 부서가 있을 때는 부서의 정보를 삭제할 수 없다.

#### 외래키 제약사항
```
- 반드시 참조하는 테이블이 먼저 생성되어야 하며, 참조키가 참조 테이블의 기본키로 만들어져 있어야 한다.
- 외래키에 사용할 수 있는 컬럼 개수는 최대 32개이다.
- 여러 컬럼을 외래키로 만들려면, 참조하는 컬럼과 외래키 컬럼의 순서와 개수는 같아야 한다.
```

#### 현장에서의 외래키 생성 시점
```
개발 현장에서 초창기에는 외래키를 생성하지 않는다. 개발 중에는 수시로 데이터를 입력하고 삭제하는 경우가 빈번한데, 외래키를 생성하면 여러 모로 불편한 것이 사실이다.
그래서 개발 후 테스트 기간을 거쳐 어느 정도 시스템이 안정화된 후 외래키를 생성할 때가 많다.
```

### CHECK
- 컬럼에 입력되는 데이터를 체크해 특정 조건에 맞는 데이터만 입력받고 그렇지 않으면 오류를 낸다.
```sql
CONSTRAINT 체크명 CHECK(체크조건);
```

### DEFAULT
- 아무것도 입력하지 않으면 설정한 기본값이 입력됨
- 값이 입력되면 기본값은 무시된다.

## TBL_MEMBER 테이블 생성해보기
```
CREATE TABLE TBL_MEMBER(
	NAME VARCHAR2(500),
	AGE NUMBER
);
```

## CAR 테이블 생성
- 테이블을 생성하며 제약조건을 같이 줘보자.
- CONSTRAINT [제약조건이름] [제약조건 종류] (컬럼명)
```
CREATE TABLE TBL_CAR(
	ID NUMBER,
	BRAND VARCHAR2(100),
	COLOR VARCHAR2(100),
	PRICE NUMBER,
	CONSTRAINT CAR_PK PRIMARY KEY(ID)
);
```

## 테이블 삭제
- DROP TABLE 테이블명;
```SQL
DROP TABLE TBL_CAR;
DROP TABLE TBL_MEMBER;
```

## 테이블 변경
- CREATE문으로 테이블을 생성한 후 불가피하게 수정해야 할 상황이 발생할 때가 많다.
- 최초설계를 잘못한 원인도 있고 요구사항이 변경되기 때문이기도 하다.
- 여러 원인으로 기존에 생성했던 컬럼의 데이터 타입을 수정하거나 삭제, 새로운 컬럼을 넣어야 하는 경우가 발생하는데, 이때마다 테이블을 삭제하고 다시 생성하는 것은 여러 문제를 만들 수 있다.
- 이럴때 ALTER TABLE문을 사용해 테이블을 수정할 수 있다.

### ex2_10테이블 생성
```sql
CREATE TABLE ex2_10(
	Col1 VARCHAR2(10) NOT NULL,
	Col2 VARCHAR2(10) NULL,
	Create_date DATE DEFAULT SYSDATE
);
```
### 컬럼명 변경
```sql
ALTER TABLE [테이블명] RENAME COLUMN [생성된 컬럼명] TO [새로운 컬럼명];
ALTER TABLE ex2_10 RENAME COLUMN Col1 TO Col11;
```

### 컬럼타입 변경
```sql
ALTER TABLE 테이블명 MODIFY 컬럼명 데이터타입;
ALTER TABLE ex2_10 MODIFY Col2 VARCHAR2(30);
```

### 컬럼추가
```sql
ALTER TABLE 테이블명 ADD 컬럼명 데이터타입;
ALTER TABLE ex2_10 ADD Col3 NUMBER;
```

### 컬럼삭제
```sql
ALTER TABLE 테이블명 DROP COLUMN 컬럼명;
ALTER TABLE ex2_10 DROP COLUMN Col3;
```
## 제약 조건 추가
- 테이블이 이미 생성된 뒤 제약조건 추가를 해보자
```SQL
ALTER TABLE 테이블명 ADD CONSTRAINT [제약조건명] [제약조건 종류](컬럼명);
ALTER TABLE ex2_10 ADD CONSTRAINT pk_ex2_10 PRIMARY KEY(Col11);
```

## 제약 조건 삭제
- ALTER TABLE 테이블명 DROP CONSTRAINT 제약조건명;
```SQL
ALTER TABLE TBL_CAR DROP CONSTRAINT CAR_PK;
```



## TBL_ANIMAL 테이블 생성
```SQL
CREATE TABLE TBL_ANIMAL(
	ID NUMBER PRIMARY KEY, 
	--제약조건을 만들어서 PK를 설정하는 법이 있고 이와 같이 간단하게 만드는법도 있다.
	"TYPE" VARCHAR2(100), 
	--오라클에서는 TYPE은 명령어 이기 때문에 명령어를 컬럼으로 사용하고 싶다면 쌍따옴표 안에 넣어야 한다.
	AGE NUMBER(3),
	FEED VARCHAR2(100)
);

--기존 제약조건 삭제(PK)
-- properties > constrains 탭으로 들어가면 제약조건에 이름이 정해져 있다.
ALTER TABLE TBL_ANIMAL DROP CONSTRAINT Name
--제약조건 추가(PK)
ALTER TABLE TBL_ANIMAL ADD CONSTRAINT ANIMAL_PK PRIMARY KEY(ID);
DROP TABLE TBL_ANIMAL;
만들었으면 확인을 하고 싶은데요 DML이라는걸 쓰는데 아직 안배웠지만 한번 써보도록 할게요.
SELECT * FROM TBL_ANIMAL;
```

## 학생 테이블 생성
- DEFAULT와 CHECK제약조건에 대해서 알아보자
```SQL
CREATE TABLE TBL_STUDENT(
	ID NUMBER,
	NAME VARCHAR2(100),
	MAJOR VARCHAR2(100),
	GENDER CHAR(1) DEFAULT 'W' NOT NULL CONSTRAINT BAN_CHAR CHECK(GENDER = 'M' OR GENDER ='W'),
	BIRTH DATE CONSTRAINT BAN_DATE CHECK(BIRTH >= TO_DATE('1980-01-01','YYYY-MM-DD')),
	CONSTRAINT STD_PK PRIMARY KEY(ID)
);
```
- DEFAULT 제약조건은 값을 넣지 않으면 'W'를 기본값으로 설정하겠다는 제약조건이다.
- NOT NULL은 해당 속성의 값은 NULL이 될 수 없다는 것이다.
- 그러면 DEFAULT를 지정하면 굳이 NOT NULL을 쓰지 않아도 되는것이 아닌가??

### NOT NULL과 DEFAULT의 차이점
```SQL
ex) GENDER CHAR(1) DEFAULT 'W'
/* QUERY 1*/
INSERT INTO TBL_STUDENT GENDER VALUES (NULL);

/* QUERY 2*/
INSERT INTO TBL_STUDENT GENDER VALUES ();
```
- 쿼리1은 'NULL'이라는 특정한 값을 받았다고 생각하기 때문에 아무일도 일어나지 않는다.
- 쿼리2는 아무런 입력도 받지 않았다고 생각하기 때문에 DEFAULT값은 'W'으로 설정된다.

### 1. NOT NULL만 선언한 경우
a. 해당 컬럼에 아무값도 넣지 않고 INSERT했을 때 : NOT NULL 동작<br>
b. 해당 컬럼에 NULL값을 넣어 INSERT했을 때 : NOT NULL 동작<br>

### 2. DEFAULT만 선언한 경우
a. 해당 컬럼에 아무값도 넣지 않고 INSERT했을 때 : DEFAULT 동작<br>
b. 해당 컬럼에 NULL값을 넣어 INSERT했을 때 : DEFAULT 동작하지 않음<br>
    - NULL이라는 값이 들어간 것으로 취급하여, DEFAULT값이 들어가지 않는다.

### 3. NOT NULL과 DEFAULT 둘 다 선언한 경우
a. 해당 컬럼에 아무값도 넣지 않고 INSERT했을 때 : DEFAULT 동작하여 기본값 들어감<br>
b. 해당 컬럼에 NULL값을 넣어 INSERT했을 때 : NOT NULL 동작<br>

## 무결성
- 데이터베이스에 저장된 데이터 값과 그것이 표현하는 현실 세계의 실제값이 일치하는지 정확성을 의미한다.
- 무결성 제약조건은 DB에 들어있는 데이터의 정확성을 보장하기 위해 부정확한 자료가 DB내에 저장되는 것을 방지하기 위한 제약조건을 말한다.
- 데이터의 정확성, 일관성, 유효성이 유지되는 것, 일관된 데이터베이스 상태를 정의하는 규칙을 묵시적으로 또는 명시적으로 정의함
	- 정확성 : 중복이나 누락이 없는 형태
	- 일관성 : 원인과 결과의 의미가 연속적으로 보장되어 변하지 않는 상태
	- 유효성 : 사용자로부터 값을 입력받을 때 정확한 값만 입력되도록 할 때 유효한 기능이다.

### 1. 개체 무결성
- PK로 선택된 컬럼은 고유한 값을 가져야 하며, 빈 값, NULL값은 허용하지 않는다.

### 2. 참조 무결성
- 외래키 값은 Null 이거나 참조 테이블의 기본키 값과 동일해야 한다.
- 즉, 테이블은 참조할 수 없는 외래키 값을 가질 수 없다는 규정이다.
    - <수강> 테이블의 '학번' 속성에는 <학생> 테이블의 '학번'속성에 없는 값은 입력할 수 없다.
  
![image](https://github.com/to7485/Web1500/assets/54658614/eeb63389-8366-4e0d-9fff-86fb074527e2)


### 3. 도메인 무결성
- 주어진 속성의 값들이 도메인에 속한 값이어야 한다는 규정이다.
    - <수강> 이라는 테이블에 '과목명'이라는 속성에 영어,수학, 국어 세 가지만 입력되도록 유효한 값을 가지는 경우
    - 반드시 해당 값만 입력을 해야 한다.

![image](https://github.com/to7485/Web1500/assets/54658614/49b10fd9-68c2-476c-8efa-68fbbe9454de)


### 4. 사용자 정의 무결성
- 속성 값들이 사용자가 정의한 제약 조건에 만족해야 한다는 규정이다.






