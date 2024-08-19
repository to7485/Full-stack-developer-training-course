# 함수적 종속성
- 하나의 테이블에서 한 컬럼의값(X)가 다른 컬럼의 값(Y)을 결정하는 관계를 함수적 종속이라고 할 수 있다.
- 정규화가 잘된 테이블일수록 결정자 X는 PK한개이고 종속자가 여러개인 구조를 가진다.

![함수적종속성](https://github.com/to7485/Web1500/assets/54658614/e52cbdd2-8367-4e9b-8f5e-52d4348bd212)


위처럼 X가 다른 모든 컬럼의 값을 결정하는<br>
X -> Y1<br>
X -> Y2<br>
X -> Y3<br>
X -> Y4<br>
와 같은 관계를 갖는다.<br>
위와 같은 성격을 완전함수 종속이라고 한다.<br>

## 완전함수 종속
- 종속자가 기본키에만 종속되며, 기본키가 여러 속성으로 구성되어 있을 경우 기본키를 구성하는<br> 모든속성이 포함된 기본키의 부분집합에 종속된 경우를 완전함수종속이라고 한다.

![완전함수종속](https://github.com/to7485/Web1500/assets/54658614/cbb84915-ae98-4890-86ec-39071f212334)

- 주민번호를 알면 이름,성별,주소를 모두 식별할 수 있다.
- 하지만 이름만으로는 성별, 주소, 주민번호 어떤것도 식별할 수 없다.

위의 테이블은<br>
주민번호(X) -> 이름(Y1)<br>
주민번호(X) -> 성별(Y2)<br>
주민번호(X) -> 주소(Y3)<br>
와 같은 관계가 성립하는<br>
주민번호를 제외한 다른 속성들이 다른 속성에 종속되지 않는 완전 함수 종속이 이루어진 테이블이다. <br>

## 부분함수 종속
- 테이블에서 기본키가 복합키일 경우 기본키를 구성하는 속성 중 일부에게 종속된 경우를 부분함수 종속이라고 한다.

![부분함수종속](https://github.com/to7485/Web1500/assets/54658614/50777119-aa7f-40ad-b11d-90ef21ee85ef)


위의 테이블에서 기본키는(이름,성별)이다.<br>

(이름,성별) -> 주소<br>
(이름,성별) -> 지역번호<br>
관계가 성립하게 된다.

하지만<br>
(이름) -> 주소<br>
의 관계도 성립이 된다.<br>

이 경우 기본키가 여러 속성으로 구성되어있을 경우 기본키를 구성하는 속성 중 일부에게 종속된 경우이다.<br>

## 이행함수 종속
- 테이블에서 X,Y,Z라는 세개의 컬럼이 존재할 때 X->Y,Y->Z이란 종속관계가 있을 경우, X->Z가 성립되는것을 이행적 함수 종속이라고 한다.
- 위의 테이블에서 X(이름,성별) -> Y(주소), X(이름,성별) -> Z(지역번호)관계를 알았다.
- 그런데 Y(주소) -> Z(지역)의 관계도 성립이 된다.

## 정규화
- 테이블 만들때 모델링을 하면서 정확하게 만들었지만 불필요한 컬럼이라던지 불필요한 요소를 걸러내는 작업이 필요하다.
- 정규화 라는 규칙에 맞게끔 설계를 해야한다는 뜻이다.
- 논리 모델링시 정규화를 진행하게 된다.

정규화 : 삽입/수정/삭제의 이상현상을 제거, 데이터의 중복 최소화, 대부분 3차 정규화 까지만 진행<br>
1차,2차 진행하면서 5차까지 하는 경우가 있는데 정규화를 하다보면 하나의 테이브를 계속 분리를 해서 데이터를 가져오는 작업을 할 때 불편하다. 그래서 보통 3차 정규화 까지 진행을 한다.<br>

- 정규화의 이점
	- 불필요한 데이터 반복을 제거함으로써 저장공간을 최소화할 수 있으며, 데이터의 변경 시 데이터의 불일치성을 최소화하고, 연산작업을 최소화할 수 있다.

## 정규화 순서

- 정규화 전

![정규화전](https://github.com/to7485/Web1500/assets/54658614/4a8404ff-6ec8-4c19-a427-41e42a3b0f97)


- 1차 정규화(1NF) :  도메인이 원자값이어야 한다.
	- 하나의 컬럼에 값이 1개만 있어야 한다, 반복적인 컬럼값이 나타나는 경우<br>
	- 보통 취미를 체크할때 체크박스를 사용해서 여러개를 선택하게 할 수 있다.<br>

![1차정규화](https://github.com/to7485/Web1500/assets/54658614/efbe40bd-6279-4b4f-bdbb-20094cab0518)



- 2차 정규화(2NF) : 부분적 함수 종속 제거
	- 1차 정규화의 조건을 만족하며 테이블의 모든 컬럼이 서로 관계가 있어야 한다.

위의 데이터를 2차 정규화의 조건에 맞게 변형한 것이다.

![2차정규화1](https://github.com/to7485/Web1500/assets/54658614/e69c5bfb-b5b0-44c5-9965-d019c0b1ba22)


![2차정규화2](https://github.com/to7485/Web1500/assets/54658614/5743e716-5d15-4643-b52c-e083361a7820)


하지만 현재 회원의 활동 상태를 파악하지 못하는 단점이 있으므로 두 테이블의 관계를 정의하는 테이블이 필요하다.

![2차정규화3](https://github.com/to7485/Web1500/assets/54658614/b43788e9-af70-4b59-b72d-e5fec2022aaf)



- 3차 정규화(3NF) :  2차 정규화의 조건을 만족하면서 이행적 함수 종속 제거를 제거해야 한다.
	- 하나의 컬럼이 다른 컬럼을 대표할 수 없다.<br>

위의 회원상태 테이블에서<br>
X(회원ID) -> Y(지역코드) 의존성을 가지고,<br>
Y(지역코드) -> Z(거주지)에 의존성을 가지므로<br>
X(회원ID) -> Z(거주지) 의존성을 가진다.<br>
따라서 기본키가 아닌 데이터 컬럼이 다른 컬럼의 결정요소가 되므로 이것을 제거하기 위해 항목들을 분리해야 한다.

![3차정규화1](https://github.com/to7485/Web1500/assets/54658614/f439e403-78a7-4a22-82a4-89ea9560102e)


![3차정규화2](https://github.com/to7485/Web1500/assets/54658614/e9ef770a-9027-441d-b2fd-28498b02c8c2)


데이터베이스에서 정규화가 필요한 이유 : 데이터베이스를 잘못 설계하면 불필요한 데이터 중복으로인해 공간이 낭비된다. 이러한 현상을 (Anomaly)라고 한다.

## 이상현상(Anormally)

![이상현상](https://github.com/to7485/Web1500/assets/54658614/d1dd5141-b30a-4067-ab6b-56b43674ea27)


### 삽입이상
> 새 데이터를 삽입하기 위해 불필요한 데이터도 삽입해야 하는 문제
  EX)담당 프로젝트가 정해지지 않은 사원이 있다면, 프로젝트 코드에 NULL을 작성할 수 없으므로 이 사원은 테이블에 추가할 수 없다. 따라서 '미정'이라는 프로젝트 코드를 따로 만들어서 삽입해야한다.

### 갱신이상
 >중복 행 중 일부만 변경하여 데이터가 불일치하게 된는 모순의 문제
  한 명의 사원은 반드시 하나의 부서에만 속할 수 있다.만약 “이현준”이 보안팀으로 부서을 옮길 시 3개 모두 갱신해 주지 않는다면개발팀인지 보안팀인지 알 수 없다. 이러한 현상을 갱신이상이라고 한다.

### 삭제이상
>행을 삭제하면 꼭 필요한 데이터까지 함께 삭제되는 문제, 이순신이 담당한 프로젝트를 박살내서 드랍된다면 이순신행을 모두 삭제하게 된다. 따라서 프로젝트에서 드랍되면 정보를 모두 드랍하게 된다. 이러한 현상을 삭제 이상이라고 한다.

이러한 현상이 발생하는 이유는 테이블이 정규화가 되어있지 않기 때문이다.<br>
정규화를 진행하기 위해서는 각 컬럼간의 관련성을 파악해야 하고,<br>
이 관련성을 "함수적 종속성"(Functional Dependecy)이라고 한다.<br>
따라서 하나의 테이블에서는 하나의 함수적 종속성만 존재하도록 정규화를 한다.<br>

# SQL함수
- 사용자가 필요한 기능을 만드는 함수가 아닌, 오라클 자체적으로 제공하는 함수
- 상황에 맞는 적절한 함수를 사용하기 위해서는 어떤 기능을 하는 함수들이 존재하는지 정확하게 파악하고 있어야 한다.

## 내장함수의 종류
- 단일행 함수 : 1개의 행값이 함수에 적용되어 1개의 행을 반환한다.
- 집계 함수 : 1개 이상의 행의 값이 함수에 적용되어 1개의 값을 반환한다.

## 문자함수
|함수|기능|
|---|------|
|ASCII|지정된 문자의 ASCII값을 반환한다.|
|CHR|지정된 수치와 일치하는 ASCII코드를 반환한다.|
|RPAD|왼쪽 정렬 후 오른쪽에 생긴 빈공백에 특정 문자를 채워 반환한다.|
|LPAD|오른쪽 정렬 후 오른쪽에 생긴 빈공백에 특정 문자를 채워 반환한다.|
|TRIM|문자열 공백 문자들을 삭제한다.|
|RTRIM|문자열 오른쪽(뒤)의 공백 문자들을 삭제한다.|
|LTRIM|문자열 왼쪽(뒤)의 공백 문자들을 삭제한다.|
|LOWER|지정된 문자를 소문자로 반환한다.|
|UPPER|지정된 문자를 대문자로 반환한다.|
|INSTR|특정 문자의 위치를 반환한다.|
|INITCAP|지정된 문자열의 첫 단어를 대문자로 나머지는 소문자로 반환한다.|
|SUBSTR|시작 위치부터 선택 개수만큼 문자를 반환한다.|
|LENGTH|문자열의 길이를 반환한다.|
|REPLACE|첫 번째 파라미터로 지정한 문자를 두번째 파라미터로 지정한 문자로 바꿔준다.|
|CONCAT|입력되는 두 문자열을 연결하여 반환한다.

```SQL
-- 지정된 문자 ASCII값을 반환한다.
SELECT ASCII('A') FROM DUAL; --결과 : 65

-- 지정된 수치와 일치하는 ASCII코드를 반환한다.
SELECT CHR(65) FROM DUAL; --결과 A

-- 왼쪽 정렬 후 오른쪽에 생긴 빈 공백에 특정 문자를 채워 반환한다.
-- RPAD(데이터,고정길이,문자)
-- 고정길이 안에 데이터를 출력하고 남는 공간을 문자로 채운다.

SELECT RPAD(DEPT_NAME,10,'*') FROM DEPT;

-- 오른쪽 정렬 후 왼쪽에 생긴 빈 공백에 특정 문자를 채워 반환한다.
-- LPAD(데이터,고정길이,문자)
-- 고정길이 안에 데이터를 출력하고 남는 공간을 문자로 채운다.

SELECT LPAD(DEPT_NAME,10,'*') FROM DEPT;

-- 문자열 공백 문자들을 삭제한다
SELECT TRIM('  HELLOW  ') FROM DUAL;

-- 컬럼이나 대상 문자열에서 특정 문자가 첫 번째나 마지막 위치에 있으면, 해당 특정 문자를 잘라낸 후 남은 문자열만 반환한다.
SELECT TRIM('zzz' FROM 'zzzHELLOWzzz') FROM DUAL;

-- 문자열 오른쪽(뒤)의 공백 문자들을 제거한다.
SELECT RTRIM('HELLOW  ')FROM DUAL;

-- 문자열 왼쪽(앞)의 공백 문자들을 제거한다.
SELECT LTRIM('   HELLOW')FROM DUAL;

-- 특정문자의 위치를 반환한다.
SELECT INSTR('HELLOW','O') FROM DUAL;

- 문자열에서 1번째 자리부터 검색하여 두번째로 나오게 되는 글자가 위치하는 자리를 반환한다.
SELECT INSTR('HELLOW','L',1,2) FROM DUAL;

-- 찾는 문자열이 없으면 0을 반환한다.
SELECT INSTR('HELLOW','Z') FROM DUAL;

--첫 문자를 대문자로 변환하는 함수 공백이나 /를 구분자로 인식함
select initcap('good morning') from dual;
select initcap('good/morning') from dual;

-- 문자열의 길이를 반환한다.
select length('john') from dual;

-- 주어지는 두 문자열을 연결한다.
SELECT CONCAT('Republic of',' Korea') FROM dual;

-- 문자열의 시작 위치부터 길이만큼 자른 후 반환한다.
-- 길이는 생략 가능하며, 생략 시 문자열의 끝까지 반환한다.

SELECT SUBSTR('Hello Oracle', 2) AS CASE1,
    SUBSTR('Hello Oracle', 7, 5) AS CASE2
FROM dual;

-- LOWER : 문자열을 모두 소문자로 변환하여 반환한다.
-- UPPER : 문자열을 모두 대문자로 변환하여 반환한다.
SELECT LOWER('hello ORACLE!') AS LOWER,
    UPPER('hello ORACLE!') AS UPPER,
    INITCAP('hello ORACLE!') AS INITCAP
FROM dual;

-- 첫 번째 지정한 문자를 두번째 지정한 문자로 바꿔 반환한다.
문) 부서번호가 50번인 사원들의 이름을 출력하되 이름중 'el'을 모두 '**'로 대체하여 출력하시오
SELECT REPLACE(FIRST_NAME,'el','**') FROM EMPLOYEES WHERE DEPARTMENT_ID = 50;

-- 이름이 6글자 이상인 사원의 사번과 이름, 급여를 출력
SELECT employee_id, first_name, salary
FROM EMPLOYEES e 
WHERE length(first_name)>=6;


```

<hr>

## 숫자함수

|함수|기능|
|---|------|
|ABS|절대값을 반환한다.|
|ROUND|특정 자리수에서 반올림을 하여 반환한다.|
|FLOOR|주어진 숫자보다 작거나 같은 정수중 최대값을 반환한다.|
|TRUNC|특정 자리수에서 잘라내고 반환한다.|
|SIGN|주어진 값의 음수,정수,0 여부를 반환한다.|
|CEIL|주어진 숫자보다 크거나 같은 정수 중 최소값을 반환한다.|
|MOD|나누기 후 나머지를 반환한다.|
|POWER|주어진 숫자의 지정된 수 만큼의 제곱값을 반환한다.|

```SQL
-- 절대값을 반환한다.
SELECT -10,ABS(-10) FROM DUAL;

-- 특정 자리수에서 반올림하여 반환한다.
-- 지정한 숫자가 양수이면 소수점 아래, 음수이면 소수점 위를 의미한다. 생략되면 반올림해서 정수를 반환한다
SELECT ROUND(1234.567,1),ROUND(1234.567,-1),ROUND(1234.567) FROM DUAL;

-- 주어진 숫자보다 작거나 같은 정수 중 최대값을 반환한다.
SELECT FLOOR(2), FLOOR(2.1) FROM DUAL;

-- 특정 자리수를 버리고 반환한다.
SELECT TRUNC(1234.567,1),TRUNC(1234.567,-1),TRUNC(1234.567) FROM DUAL;

-- 주어진 값의 음수,정수,0 여부를 반환한다.
--음수는 -1, 0은 0, 양수는 1, NULL은 NULL을 반환한다.
SELECT SIGN(-10),SIGN(0),SIGN(10),SIGN(NULL) FROM DUAL;

-- 주어진 숫자보다 크거나 같은 정수 중 최소값을 반환한다.
SELECT CEIL(2),CEIL(2.1) FROM DUAL;

-- 나누기 후 나머지를 반환한다.
SELECT MOD(1,3),MOD(2,3),MOD(3,3),MOD(4,3),MOD(0,3) FROM DUAL;

-- 주어진 숫자의 지정된 수 만큼 제곱값을 반환한다.
SELECT POWER(2,1),POWER(2,2),POWER(2,3),POWER(2,0) FROM DUAL;

-- 사원번호가 홀수이면 1, 짝수이면 0을 출력하시오.
select employee_id, mod(employee_id, 2)
from employees;

-- 사원번호가 짝수인 사람들의 사원 번호와 이름을 출력하시오.
select first_name, employee_id
from emp
where mod(employee_id,2) = 0;

-- 사원테이블에서 이름, 급여, 급여 1000당 0의 개수를 채워 조회하세요
-- ex) 급여가 8,000이다. 00000000로 표현
SELECT first_name, salary, RPAD('■',ROUND(SALARY/1000),'■')
FROM EMPLOYEES;
```

## 날짜함수
|함수|기능|
|---|------|
|ADD_MONTHS|특정날짜에 개월수를 더해준다. |
|MONTHS_BETWEEN|주어진 두 개의 날짜 간격 개월을 반환한다.|
|NEXT_DAY|주어진 일자가 다음에 나타나는 지정요일(1:일요일 ~ 7:토요일)의 날짜를 반환한다.|
|LAST_DAY|주어진 일자가 포함된 월의 말일을 반환한다.|

※ 날짜 + 날짜 : 날짜끼리는 더하기가 안됩니다.

- SYSDATE : 현재 날짜

```SQL
-- 특정 날짜에 개월수를 더한다.

select sysdate, add_months(sysdate, 2)from dual;

문제) 사원테이블에서 모든 사원의 입사일로부터 6개월 뒤의 날짜를 이름, 입사일, 6개월뒤 날짜 순으로 출력
select first_name, hire_date,add_months(hire_date,6) new_date from employees;

문제) 사번이 120번인 사원이 입사후 3년 6개월째 되는날 진급예정이다. 진급 예정 날짜를 구하시오.
select fist_name, add_months(hire_date, 42) promotion from employees where employee_id = 120;

select trunc( months_between(sysdate, '01/01/2015'), 2)from dual;

2) MONTHS_BETWEEN : 두 날짜 사이의 개월수를 구한다

문제)모든 사원들이 입사일로부터 오늘가지 몇개월이 경과했는지 출력

SELECT sysdate, hire_date, MONTHS_BETWEEN(sysdate,hire_date) FROM EMPLOYEES;

문제) 사원들의 이름, 입사일, 입사후 오늘까지의 개월수를 조회하되 입사기간이 200개월 이상인 사람만 출력하고 입사개월수는
소수점 이하 한자리까지만 버림하시오.

SELECT FIRST_NAME, HIRE_DATD, TRUNC(MONTHS_BETWEEN(SYSDATDE,HIRE_DATE),1) MONTHS FROM EMPLOYEES
WHERE TRUNC(MONTHS_BETWEEN(SYSDATDE,HIRE_DATE),1) >= 200;

문제)입사기간이 160개월 이상인 사원들의 이름, 입사일, 입사후 개월수를 출력

select first_name, hire_date,mon from employees where trunc(months_between(sysdate, hire_date)>=200),0) mon

문제) 사번이 120번인 사원이 입사후 3년 6개월이 되는날 퇴사했다. 이 사원의 사번,이름,입사일,퇴사일을 출력

SELECT EMPLOYEE_ID, FIRST_NAME, HIRE_DATE, add_months(HIRE_DATE, 42) fired FROM EMPLOYEES WHERE EMPLOYEE_ID = 120;

SELECT SYSDATE,
	NEXT_DAY(SYSDATE-7,'일요일') prev_sunday, --이전 일요일 
	NEXT_DAY(SYSDATE,'일요일')   next_sunday --다음 일요일 
FROM DUAL;
  
SELECT NEXT_DAY(SYSDATE, 1)        FROM DUAL;
SELECT NEXT_DAY(SYSDATE, '일요일') FROM DUAL;
SELECT NEXT_DAY(SYSDATE, '일')     FROM DUAL;

-- 오라클 세팅이 한글이라서 영어로 작성하니 안된다
SELECT NEXT_DAY(SYSDATE, 'SUNDAY') FROM DUAL;
SELECT NEXT_DAY(SYSDATE, 'SUN')    FROM DUAL;
```
## 형변환 함수
|함수|기능|
|---|------|
|TO_CHAR|날짜를 형식에 맞춰 문자열로 변환|
|TO_DATE|문자열을 형식에 맞춰 날짜형으로 변환|
|TO_NUMBER|문자를 숫자로 변환(숫자만 있는 문자열은 묵시적으로 숫자로 취급하기에 잘 사용은 안한다.)|

### 날짜형식 FORMATTING 모델
|모델|기능|
|---|------|
|SCC, CC|세기|
|YYYY,YY|연도|
|MM|월|
|DD|일|
|DAY|요일|
|MON|월명(JAN)|
|MONTH|월이름이 다나온다(JANUARY)|
|HH,HH24|시간|
|MI|분|
|SS|초|

```SQL
--TO_CHAR(날짜,포맷)
SELECT TO_CHAR(sysdate,'yyyy-mm-dd'), 
 TO_CHAR(sysdate,'yyyy-mm-dd day'), 
 TO_CHAR(sysdate,'yyyy-mm-dd HH:MI:SS')
FROM dual;

--TO_CHAR(숫자,포맷)
/*
0 : 숫자, 공백시 0으로 채움
9 : 숫자
, : 쉼표 표기
L : local currency symbol
*/
SELECT TO_CHAR(1234567, '9,999,999'), -- '1,234,567' 
  TO_CHAR(1234567, 'L9,999,999.99'), -- '￦1,234,567.00'
  TO_CHAR(12, '0999') -- '0012'
FROM dual;

--TO_DATE
SELECT TO_DATE('2022.04.11'), -- 22/02/11(날짜형)
  TO_DATE('04.11.2022', 'MM,DD,YYYY'), --22/02/11(날짜형)
  TO_DATE('2022.04', 'YYYY.MM'), --22/04/01 : 일 입력 안하면 1일로 변환
  TO_DATE('11', 'DD') -- 22/04/11 : 년, 월 입력 안하면 해당년 해당월로 변환
FROM dual;
```
## NULL 처리 함수

### NULL 값을 다른 값으로 변경
|함수|기능|
|---|------|
|NVL| NULL값 대신 다른 값으로 변경 후 검색|
|NVL2| NULL일 때의 값, NULL이 아닐 때의 값을 각각 설정|
|NULLIF|두 인자 값을 비교, 같으면 NULL을 반환, 다르면 첫번째 인자 값을 반환|
```SQL
NVL(컬럼,치환할 값)
NVL2(컬럼,NULL이 아닐 때 치환할 값, NULL일 때 치환할 값)

-- 두 컬럼에 대해서 비교할 수 있다.
NULLIF(컬럼1,컬럼2);

-- 특정 컬럼에 특정 값과 비교할 수 있다.
NULLIF(컬럼1,특정값);

-- 함수의 인자는 동적으로 입력할 수 있다.
COALESCE(컬럼1,컬럼2,컬럼3...);

--PLAYER 테이블에서 POSITION이 NULL인 선수 검색
SELECT * FROM PLAYER WHERE "POSITION" IS NULL;
SELECT * FROM PLAYER WHERE "POSITION" IS NOT NULL;

--PLAYER 테이블에서 POSITION이 NULL이면 '미정'으로 결과 출력하기
SELECT NVL("POSITION",'미정') FROM PLAYER WHERE "POSITION" IS NULL;
SELECT PLAYER_NAME “선수 이름”, NVL("POSITION",'미정') 포지션 FROM PLAYER;
SELECT PLAYER_NAME “선수 이름”, NVL2("POSITION",'확정','미정') AS 포지션 FROM PLAYER;

--PLAYER 테이블에서 NATION이 NULL이 아니면 등록, NULL이면 미등록으로 변경
SELECT PLAYER_NAME "선수 이름", NVL(NATION, '등록','미등록') "국가 등록 여부" FROM PLAYER;
```
## 순위 함수
|함수|기능|
|----|-----|
|RANK|그룹 내 순위를 계산하여 NUMBER타입으로 순위를 반환<br>중복 순위 계산|
|DENSE_RANK|그룹 내 순위를 계산하여 NUMBER타입으로 순위를 반환<br>중복 순위 계산 안함|

```SQL
RANK() OVER(ORDER BY 컬럼)
DENSE_RANK() OVER(ORDER BY 컬럼)

SELECT RANK() OVER(ORDER BY SALARY DESC) AS "RANK", FIRST_NAME, SALARY FROM EMPLOYEES;
SELECT RANK() OVER(ORDER BY SALARY DESC,EMPLOYEE_ID ASC ) AS "RANK", FIRST_NAME, SALARY FROM EMPLOYEES;
```


<hr>

## 집계함수
- 여러 행들에 대한 연산의 결과를 하나의 행으로 반환한다.
- 집계 함수는 NULL을 체크하지 않는다. 단 COUNT(*)의 경우 NULL도 포함한 값을 반환한다.

|함수|기능|
|---|------|
|COUNT|행들의 개수를 반환|
|MIN|행들의 최소값을 반환|
|MAX|행들의 최대값을 반환|
|SUM|행들의 합계를 반환|
|AVG|행들의 평균을 반환한다.|
|STDDEV|행들의 표준편차를 반환한다.|
|VARIANCE|행들의 분산을 반환한다.|

```SQL
-- 일반적으로 그룹함수와 일반컬럼을 함께 쓸 수 없다.
select count(*), first_name from employees;

예) 사원테이블의 전체 사원수를 출력
select COUNT(*) FROM EMPLOYEES;

예) 사원테이블에서 보너스를 받는 사원의 수를 출력
select count(commIssion_pct) from employees;

-- COMMISSION_PCT 속성에 값이 있는 행의 개수만 센다.

문제) 사원테이블에서 직종이 SA_REP인 사원들의 평균급여, 급여최고액, 급여최저액, 급여의 총 합계를 출력하시오.
select AVG(salary) AVG,MAX(salary) MAX,MIN(salary) MIN,SUM(salary) SUM
from employees
WHERE JOB_ID = 'SA_REP';

예) 부서의 갯수를 출력
select count(DISTINCT department_id)from employees;

DISTINCT : 중복된 값은 세지 않는다.

문) 부서번호가 80번인 부서의 사원들의 급여의 평균을 출력

SELECT ROUND(AVG(SALARY), 1) AVG FROM EMPLOYEES WHERE DEPARTMENT_ID = 80;

예) 관리자의 수를 출력
distinct : 중복된 값을 제외
select count(distinct manager_id) from employees;


문제) 사원 테이블에 등록되어있는 모든 사원의 수, 보너스를 받는 인원수, 전체사원 급여의 평균, 등록되어있는 부서의 갯수를 화면에 출력
select count(employee_id),count(
				select count(employee_id),count(commission_pct),avg(salary),count(distinct department_id) 
				from employees; commission_pct),avg(salary),count(distinct department_id) 
				from employees;

문제) 사원테이블에서 80번 부서에 속하는 사원들의 연봉의 평균을 소수점 두자리까지 반올림하여 출력하시오
select round(AVG(salary), 2) from employees where department_id = 80;

문제) 사원테이블에서 50번에 속하는 사원들의 급여의 최대값과 최소값을 출력하세요
select Max(salary),MIN(SALARY), FROM EMPLOYEES WHERE DEAPRTMENT_ID = 50;
```
## GROUP BY(그룹화)
- 특정테이블에서 소그룹을 만들어 결과를 분산시켜 얻고자 할 때
- GROUP BY : ~별 (예 : 부서별 인원수)

```SQL
예) 각 부서별 급여의 평균과 총 합을 출력

SELECT DEPARTMENT_ID, COUNT(*), AVG(SALARY), SUM(SALARY) FROM EMPLOYEES GROUP BY DEPARTMENT_ID;

GROUP BY로 소그룹을 지정하고 싶은 컬럼이 있는데 이걸 SELECT에서도 사용하고 싶으면 GROUP BY에 작성해놓은 컬럼명만 SELECT에 추가할 수 있다.

예) 부서별, 직종별로 그룹을 나눠서 인원수를 출력 단, 부서번호가 낮은순으로 정렬하시오.

SELECT DEPARTMENT_ID, JOB_ID, COUNT(*) FROM EMPLOYEES GROUP BY DEPARTMENT_ID, JOB_ID ORDER BY DEPARTMENT_ID;

부서가 같아도 직종이 다른 경우가 있기 때문에 좀더 세부적인 결과물을 가져올수 있는게 GROUP BY다.

문) 각 직종별 인원수를 출력

SELECT JOB_ID, COUNT(*) FROM EMPLOYEES GROUP BY JOB_ID;

문) 각 직종별 급여의 합을 출력

SELECT JOB_ID, SUM(SALARY) FROM EMPLOYEES GROUP BY JOB_ID;
괄호안에 어떤걸 넣어야 하는지 알면 난이도가 많이 내려간다.

문) 부서별로 가장 높은 급여를 조회

SELECT DEPARTMENT_ID, MAX(SALARY) FROM EMPLOYEES GROUP BY DEPARTMENT_ID;

문) 부서별 급여의 합계를 내림차순으로 조회

SELECT DEPARTMENT_ID, SUM(SALARY) FROM EMPLOYEES GROUP BY DEPARTMENT_ID ORDER BY SUM(SALARY) DESC;
```
## 그룹함수

```SQL
CREATE TABLE 월별매출 (
    상품ID VARCHAR2(5),
    월 VARCHAR2(10),
    회사 VARCHAR2(10),
    매출액 INTEGER );
    
INSERT INTO  월별매출 VALUES ('P001', '2019.10', '삼성', 15000);
INSERT INTO  월별매출 VALUES ('P001', '2019.11', '삼성', 25000);
INSERT INTO  월별매출 VALUES ('P002', '2019.10', 'LG', 10000);
INSERT INTO  월별매출 VALUES ('P002', '2019.11', 'LG', 20000);
INSERT INTO  월별매출 VALUES ('P003', '2019.10', '애플', 15000);
INSERT INTO  월별매출 VALUES ('P003', '2019.11', '애플', 10000);

SELECT * FROM 월별매출;
```

- ROLLUP
    - ROLLUP(A) : A 그룹핑 -> 합계
    - ROLLUP(A,B) : A,B그룹핑 -> A소계/합계
    - ROLLUP(A,B,C) : A,B,C그룹핑 -> (A소계,B소계)/합계
 
```SQL
SELECT 상품ID, 월, SUM(매출액) AS 매출액
FROM 월별매출
GROUP BY ROLLUP(상품ID, 월);
```

![image](https://github.com/to7485/DBMS1900/assets/54658614/0cce5aea-3337-477c-94c6-f6e60754f04b)

- CUBE
    - CUBE(A) : A그룹핑 -> 합계
    - CUBE(A,B) : A,B그룹핑/A그룹핑/B그룹핑 -> A소계,B소계/합계
    - CUBE(A,B,C) : A,B,C그룹핑/A,B그룹핑/A,C그룹핑/B,C그룹핑/A그룹핑/B그룹핑/C그룹핑 -> (A소계,B소계),(A소계),(B소계)/합계

```SQL
SELECT 상품ID, 월, SUM(매출액) AS 매출액
FROM 월별매출
GROUP BY CUBE(상품ID, 월);
```

![image](https://github.com/to7485/DBMS1900/assets/54658614/bf9caa9e-af05-48f6-9c92-356542b60073)

- GROUPING SETS
    - GROUPING SETS(A,()) : A그룹핑 -> 합계
    - GROUPING SETS(A,B,()) : A그룹핑/B그룹핑 -> 합계
 
 ```SQL
SELECT 상품ID, 월, SUM(매출액) AS 매출액
FROM 월별매출
GROUP BY GROUPING SETS(상품ID, 월);
 ```
 
 ![image](https://github.com/to7485/DBMS1900/assets/54658614/0d56776f-7458-4702-894d-50627e57ee79)


## HAVING절
- Having 절은 Group by로 집계된 값 중 where 절 처럼 특정 조건을 추가한다고 생각 하시면 됩니다.

### WHERE절과 HAVING절의 차이점
- HAVING절은 GROUP BY절과 함께 사용해야 하며 집계 함수를 사용하여 조건절을 작성하거나 GROUP BY컬럼만 조건절에 사용할 수 있다.

```SQL
예) 각 부서의 급여의 최대값, 최소값, 인원수를 출력하자
     단, 급여의 최대값이 8000이상인 결과만 보여줄 것.
select department_id, MAX(salary),MIN(salary),COUNT(*)
from employees 
group by department_id
having MAX(salary)>=8000; -> 그룹함수가 사용된 조건이라면 WHERE 이 아닌 HAVING을 써야한다.
--WHERE MAX(SALARY) >= 8000;

문제) 각 부서별 인원수가 20명 이상인 부서의 정보를 부서번호, 급여의 합, 급여의 평균, 인원수 순으로 출력
단, 급여의 평균은 소수점 2자리 반올림
select department_id, SUM(salary), ROUND(AVG(salary),2) avg,COUNT(*)
from employees
having COUNT(*)>=20;

그룹함수만 having에 쓰고 일반 조건은 where에 써야 한다. 일반조건이 having절에 들어가려면 group by에 묶여야 한다.

문제) 부서별, 직종별로 그룹화 하여 결과를 부서번호, 직종, 인원수 순으로 출력, 단, 직종이 'MAN'으로 끝나는 경우만 출력
sleect department_id,job_id,count(*)
from employees
where job_id like '%MAN' -> HAVING으로 해도 값이 나오긴 하지만 일반컬럼이기 때문에 WHERE쓰는게 좋다.
group by department_id,job_id;

문제)각 부서별 평균 급여를 소수점 한자리까지 버림으로 출력 단, 평균 급여가 10000미만인 그룹만 조회해야 하며
 부서번호가 50이하인 부서만 조회 
select department_id, TRUNC(AVG(salary),1)
from employees 
where department_id<=50 
group by department_id
having AVG(salary)<10000;

문제) 각 부서별 부서번호, 급여의 합, 평균, 인원수 순으로 출력 단, 급여의 합이 30000이상인 경우만 출력해야 하며, 급여의 평균은 소수점 2자리에서 반올림 하시오.
select department_id, SUM(salary), ROUND(AVG(salary),2),COUNT(*) 
from employees 
group by department_id 
having SUM(salary)>=30000;
```

