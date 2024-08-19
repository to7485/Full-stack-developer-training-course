# 모델링
- 데이터 모델링이란 정보시스템 구축의 대상이 되는 업무 내용을 분석하여 이해하고 약속된 표기법에 의해 표현하는걸 의미한다.
- 분석된 모델을 가지고 실제 데이터베이스를 생성하여 개발 및 데이터 관리에 사용된다.
- 특히 데이터를 추상화한 데이터 모델은 데이터베이스의 골격을 이해하고 그 이해를 바탕으로 SQL문장을 기능과 성능적인 측면에서 효율적으로 작성할 수 있기 때문에,
- 데이터 모델링은 데이터베이스 설계의 핵심 과정이기도 하다.

## 데이터 모델링의 특징
- 추상화 : 현실세계를 일정한 형식에 맞춰 간략하게 표현해야 합니다.
- 단순화 : 누구나 쉽게 이해할 수 있도록 제한된 표기법이나 언어를 사용해야 합니다.
- 명확화 : 명확하게 의미가 해석되어야 하고, 한 가지 의미만을 가져야 합니다.

### 1. 요구사항 분석
- 업무 파악은 어떠한 업무를 시작하기 전에 해당하는 업무에 대해서 파악하는 단계 이다.
- 고객과의 의사소통을 통해 고객의 업무 프로세스를 완벽하게 이해하고, 그들의 요구사항을 구체적으로 뽑아내는 과정

### 2. 개념적 데이터 모델링
- 내가 하고자 하는 일의 데이터 간의 관계를 구상하는 단계 이다.
- 각 개체들과 그들간의 관계를 발견하고 표현하기 위해 ERD 다이어그램을 생성한다.
-  피터 첸 표기법(Peter Chen Notation)으로 ERD 다이어그램을 구성한 그림이다.
-  그리는 방법은 어렵지 않다. 도형이 의미하는 바를 알고 화살표를 통해 관계를 표현하기만 하면 된다.
-  - 회원, 주문, 상품 3가지를 관리하고자 한다.

![image](https://github.com/to7485/Web1500/assets/54658614/45e36a20-8065-4456-b943-91b3ba185838)


### 3. 논리적 데이터 모델링
- 개념적인 데이터 모델이 완성되면, 구체화된 업무 중심의 데이터 모델을 만들어 내야한다.
- 업무에 대한 Key, 속성, 관계등을 표시하며, 정규화 활동을 수행한다.
- 정규화는 데이터 모델의 일관성을 확보하고 중복을 제거하여 신뢰성있는 데이터 구조를 얻는데 목적이 있다.

![image](https://user-images.githubusercontent.com/54658614/215704561-7a220819-60e8-44ad-9f1b-cd4e41ecb862.png)

### 4. 물리적 데이터 모델링
- 최종적으로 데이터를 관리할 데이터 베이스를 선택하고, 선택한 데이터 베이스에 실제 테이블을 만드는 작업을 말한다.
- 시각적인 구조를 만들었으면 그것을 실제로 SQL 코딩을 통해 완성하는 단계라고 보면 된다


```SQL
USER		
USER_ID:VARCHAR2(100)		
--------------------------		
USER_PW:VHARCHAR2(100)		
USER_NAME:VHARCHAR2(200)		
USER_ADDRESS:VHARCHAR2(300)		
USER_EMAIL:VHARCHAR2(300)		
USER_BIRTH:DATE

PRODUCT	
PRODUCT_NUM:NUMBER		
--------------------------		
PRODUCT_NAME:VHARCHAR2(300)		
PRODUCT_PRICE:NUMBER	
PRODUCT_COUNT:	NUMBER
	
ORDER
ORDER_NUM:NUMBER		
--------------------------
ORDER_DATE:DATE
USER_ID:VARCHAR2(100)
PRODUCT_NUM:NUMBER
```
모델링을 먼저하고 코드를 작성해야 오류를 줄일 수 있다.

```SQL
CREATE TABLE "USER"(
	USER_ID VARCHAR2(100) PRIMARY KEY,
	USER_PW VARCHAR2(100),
	USER_ADDRESS VARCHAR2(300),
	USER_EMAIL VARCHAR2(300),
	USER_BIRTH DATE
);

CREATE TABLE PRODUCT(
	PRODUCT_NUM NUMBER PRIMARY KEY,
	PRODUCT_NAME VARCHAR2(300),
	PRODUCT_PRICE NUMBER,
	PRODUCT_COUNT NUMBER
);

CREATE TABLE "ORDER"(
	ORDER_NUM NUMBER PRIMARY KEY,
	ORDER_DATE DATE,
	USER_ID VARCHAR2(100), --외래키로 참조할 컬럼의 데이터타입과 길이를 반드시 맞춰줘야 합니다.
	PRODUCT_NUM NUMBER,
	CONSTRAINT USER_FK FOREIGN KEY(USER_ID) REFERENCES "USER"(USER_ID),
	CONSTRAINT PRODUCT_FK FOREIGN KEY(PRODUCT_NUM) REFERENCES PRODUCT(PRODUCT_NUM)
);
```

## 데이터 모델링 실습

1. 요구사항
	- 꽃 테이블과 화분 테이블 2개가 필요하고, 꽃을 구매할 때 화분도 같이 구매한다.
	- 꽃은 이름과 색깔, 가격이 있다.
	- 화분은 제품 번호, 색깔, 모양, 꽃 이름이 있다.

2. 개념적 설계(개념 모델링)

![image](https://user-images.githubusercontent.com/54658614/215705598-770d8323-f9d6-4ed4-bc2a-1c6d1b585bd1.png)

3. 논리적 설계(논리 모델링)
 
![image](https://user-images.githubusercontent.com/54658614/215705734-398d083b-c9b0-409e-b3f8-21b6274067e2.png)

5. 물리적 설계(물리 모델링)

```SQL
FOLOWER
------------------------
FOWER_NAME:VARCHAR2(200),
COLOR:VARCHAR2(100),
PRICE:NUMBER
---------------------------------------
CONSTRAINT PRIMARY KEY(FLOWER_NAME)
---------------------------------------

POT
------------------------
POT_ID:VARCHAR2(100),
POT_COLOR:VARCHAR2(100),
SHAPE:VARCHAR2(200),
FLOWER_NAME:VARCHAR2(200),
---------------------------------------
CONSTRAINT FOREIGN KEY(FLOWER_NAME) REFERENCES FLOWER(FLOWER_NAME)
---------------------------------------
```

```SQL
/*
FOLOWER
------------------------
FOWER_NAME:VARCHAR2(200),
COLOR:VARCHAR2(100),
PRICE:NUMBER
---------------------------------------
CONSTRAINT PRIMARY KEY(FLOWER_NAME)
---------------------------------------
*/

DROP TABLE FLOWER;

CREATE TABLE FLOWER(
	FLOWERNAME VARCHAR2(200),
	FLOWERCOLOR VARCHAR2(100),
	FLOWERPRICE NUMBER,
	CONSTRAINT FLOWER_PK PRIMARY KEY(FLOWERNAME)
);

SELECT * FROM FLOWER;
 
/*
POT
------------------------
POT_ID:VARCHAR2(100),
POT_COLOR:VARCHAR2(100),
SHAPE:VARCHAR2(200),
FLOWER_NAME:VARCHAR2(200),
---------------------------------------
CONSTRAINT FOREIGN KEY(FLOWER_NAME) REFERENCES FLOWER(FLOWER_NAME)
---------------------------------------
*/
CREATE TABLE POT(
	POTID VARCHAR2(100),
	POTCOLOR VARCHAR2(100),
	POTSHAPE VARCHAR2(200),
	NAME VARCHAR2(200),
	CONSTRAINT POT_PK PRIMARY KEY(POTID),
	CONSTRAINT POT_FK FOREIGN KEY(NAME) REFERENCES FLOWER(FLOWERNAME)
);

SELECT * POT;
```

# DML(Data Manipulation Language)
-  데이터 조작어
### 1. SELECT
- 테이블에서 원하는 데이터를 조회할 때 사용하는 키워드
```SQL
   SELECT 컬럼명1,컬럼명2... FROM 테이블명
   WHERE 조건식;
```
### 조건절
- 원하는 자료를 검색하기 위한 조건절
- WHERE 절에서는 결과를 제한하기 위한 조건을 기술할 수 도 있다.
- WHERE절은 조회하려는 데이터에 특정 조건을 부여할 목적으로 사용하기 때문에 FROM절 뒤에 오게 된다.

### WHERE 절의 조건식은 아래 내용으로 구성된다.
- <b>WHERE 조건식</b> 형태로 많이 사용이 된다.
- 컬럼명(보통 조건식의 좌측에 위치)
- 비교 연산자 ( 초과,미만,이상,이하,같다,같지않다,그리고And,또는Or)
    - \> , < : 초과, 미만
    - \>=, <= : 이상, 이하
    - = : 같다
    - < >, !=, ^= : 같지않다.
    - AND : 두 조건식이 모두 참이면 참
    - OR : 둘 중 하나라도 참이면 참
- 문자,숫자,표현식(보통 조건식의 우측에 위치)
- 비교 칼럼명(JOIN 사용시)

### 조건식에서 NULL 사용하기
```SQL
컬럼명 IS NULL : 컬럼 값이 NULL이면 참
컬럼명 IS NOT NULL : 컬럼 값이 NULL이 아니면 참
```

### 2. INSERT:추가
- 테이블에 데이터를 추가할 때 사용하는 키워드
```SQL
INSERT INTO 테이블명(컬럼명1, 컬럼명2...) VALUES(값1,값2...) DEFAULT 쓸 때
INSERT INTO 테이블명 VALUES(값1,값2,....) 무조건 만든 컬럼 개수만큼 값을 넣어야함
```

### 3. UPDATE
- 테이블의 내용을 수정할 때 사용하는 키워드
```SQL
   UPDATE 테이블명
   SET 기존컬럼명 = 새로운 값
   WHERE 조건식 조건을 달지 않으면 테이블 전체가 바뀌어 버린다.
```

### 4. DELETE
- 삭제 ※TRUNCATE는 다 날려버리는건데 DELETE는 1개씩 지운다.
- 행 1개가 통째로 날아간다.
```SQL
   DELETE FROM 테이블명
   WHERE 조건식
```

## SELECT

```SQL
예) employees(사원)테이블의 모든 정보를 조회하시오

select * from employees; 

예) departments(부서)테이블의 모든 정보를 조회하시오

select * from departments;

예) 사원테이블에서 first_name(이름),job_id(직종),salary(급여)를 조회해보자!

select first_name, job_id, salary from employees;

-- 정보가 많고 컬럼이 많아도 나한테 필요한것만 골라낼수 있기 때문에 속도가 빠르다
-- 자바로 데이터를 가져오려고 생각하면 if-while-반복문 돌리면서 찾아줘야 한다.
-- DB는 맞는 정보를 찾아서 바로 화면에 뿌려주는 구조이기 때문에 많은양의 데이터를 관리하는데는 데이터베이스가 경제적이다.

-- 스키마 작성 사원 테이블에서 컬럼이 영어로 되어있기 때문에 뭐라고 되어있는지 한눈에 보기 힘들다.
-- 메모장에다 사원테이블이 갖고 있는 컬럼들이 각각 어떤 정보를 저장하기 위해서 만들어져있는지 컬럼들인지를 한번에 정리를 하자.

문) 사원테이블에서 사번, 이름,입사일,급여를 검색하시오
SELECT employee_id, first_name, hire_date, salary FROM employees;

컬럼에 없는 정보를 출력하고 싶을 때가 있다

예) 사원테이블에서 사번, 이름, 직종, 급여, 보너스, 실제의 보너스 금액을 출력

select employee_id, first_name, job_id, salary, commission_pct,
-- *를 통한 연산을 수행
 salary*commission_pct as comm //as를 빼고 한칸 띄우고 써도 별칭으로 써진다.
 from employees;

실제로 컬럼에는 없지만 간단한 연산을 통하여 컬럼에 존재하지 않는 내용도 조회하는 것이 가능하다~
컬럼에 없던 것이기 때문에 컬럼에 연산식이 그대로 나온다. 연산식이 길어질수록 보기 않좋기 때분에 별칭을 써준다.

SELECT comm from employees; 로 별칭으로 조회가 가능해진다.
```

```SQL
예) 사원테이블에서 급여가 10000이상인 사원들의 정보를 사번, 이름, 급여 순으로 출력

select employee_id, first_name, salary from employees where salary >=10000;

where절은 from 뒤에 있음

예) where절에 문자를 비교하고 싶다면
where first_name='Michael';
*==이 아님 주의, 반드시 홑따옴표로 쓴다.

예) 사원테이블에서 이름이 Michael인 사원의 사번, 이름을 조회
SELECT employee_id, first_name FROM employees WHERE first_name='Michael';

문제) 사원테이블에서 직종이 IT_PROG인 사원들의 정보를 사번, 이름, 직종, 급여 순으로 출력

select employee_id,first_name,job_id,salary from employees where job_id='IT_PROG';

예) 사원테이블에서 급여가 10000이상이면서 13000이하인 사원의 정보를 이름, 급여 순으로 조회
안타깝게도 데이터베이스에서는 && 나 ||를 쓸수가 없다 and , or로 작성을 해야한다.
SELECT first_name, salary FROM employees WHERE salary >= 10000 AND salary <= 13000;


문제) 사원테이블에서 입사일이 05년9월21일인 사원의 정보를 사번, 이름, 입사일 순으로 출력

select employee_id, first_name, hire_date from employees where hire_date='2005-09-21';


예) 사원테이블에서 입사일이 05년9월21일 이후에 입사한 사원의 정보를 사번, 이름, 입사일 순으로 출력

select employee_id, first_name, hire_date from employees where hire_date >='2005-09-21';


- 데이터베이스는 날짜의 크기비교가 가능하다.

예) 사원테이블에서 06년도에 입사한 사원들의 정보를 사번, 이름, 직종, 입사일 순으로 출력

select employee_id, first_name, job_id, hire_date from employees where hire_date>='2006-01-01' 
and hire_date<='2006-12-31'

문제) 사원테이블에서 급여가 4000~ 8000사이의 사원의 이름,직종,급여를 출력
select first_name, job_id, salary from employees where salary >=4000 and salary<=8000;


문제) 사원테이블에서 직종이 SA_MAN이거나 IT_PROG인 사원들의 모든정보를 출력하시
select * from employees where job_id = 'SA_MAN' or job_id='IT_PROG';


문제) 사워테이블에서 급여가 2200, 3200, 5000, 6800를 받는 사원들의 정보를 사번, 이름 직종, 급여 순으로 출력
select employee_id, fist_name, job_id, salary 
from employees 
where salary='2200' or salary = '3200' or salary='5000' or salary='6800';
```

### SQL연산자
1. BETWEEN : A와 B사이의 값을 조회할 때 사용
2. IN : OR을 대신해서 사용하는 연산자
3. LIKE : 유사검색

```SQL
--BETWEEN연산자 AND연산자를 대체함
예) 사원테이블에서 06년도에 입사한 사원들의 정보를 사번, 이름, 직종, 입사일 순으로 출력
select employee_id, first_name, job_id, hire_date from employees where hire_date between'01/01/2006' and '12/31/2006'; 날짜는 문자열로 인식함

문제) 사원테이블에서 급여가 5000이상이고 6000이하인 사원의 정보를 사번, 이름, 급여순으로 출력
select employee_id, first_name, salary from employees where salary between 5000 and 6000;


--IN연산자
예) 직종이 SA_MAN , IT_PROG인 사원들의 정보를 이름, 직종순으로 출력
select first_name, job_id from employees where job_id IN ('SA_MAN','IT_PROG');

문제) 급여가 2200, 3200, 5000을 받는 사원들의 정보를 이름, 직종, 급여순으로 출력하되 in연산자를 사용하시오

SELECT first_name,job_id,salary from employees WHERE salary=2200 or salary=3200 or salary=5000
select first_name,job_id,salary from employees where salary in (2200,3200,5000);


예) 직종이 'SA_MAN', 'IT_PROG'가 아닌 모든 사원들의 정보를 출력
select * from employees where job_id not in('SA_MAN','IT_PROG');
```

## LIKE연산자(유사검색)
- 쿼리문에 WHERE절에 주로 사용되며 부분적으로 일치하는 속성을 찾을 때 사용뇌다.
- % : 모든값
- _ : 하나의 값

ex)'M%' : M으로 시작하는 모든 값<br>
ex)'%a' : a로 끝나는 모든 값<br>
ex)'%a%' : 값의 어디든 a를 포함하고 있는 모든 값<br>
ex)'%M%I% : M과 I를 포함하고 있는 데이터<br>
ex)'M_ _ _ _' : M으로 시작하는 값들 중 전체 길이가 5글자인 값<br>

```SQL
예)사원테이블에서 사원들의 이름 중 M으로 시작하는 사원의 정보를 사번, 이름, 직종 순으로 출력
select employee_id, first_name, job_id from employees where first_name LIKE 'M%';
%는 뒤로는 뭐가 몇글자가 오든 상관 안하겠다는 의미

문)사원테이블에서 이름이 d로 끝나는 사원의 사번, 이름 직종을 출력
select employee_id ,first_name, job_id from employees where first_name LIKE'%d';

예)이름의 어디라도 a가 포함되어 있는 사원의 정보를 이름, 직종 순으로 출력
select first_name, job_id from employees where first_name LIKE'%a%';

예)이름의 첫글자가 M이면서 총 7글자의 이름을 가진 사원의 정보를 사번, 이름순으로 검색
select employee_id, first_name from employees where first_name like 'M______'

문제) 사원테이블에서 이름의 세번째 글자에 a가들어가는 사원들의 정보를 사번, 이름 순으로 출력
select employee_id, first_name from employees where first_name like '_ _ a%';

문제) 이름에 소문자o가 들어가면서 이름이 a로 끝나는 사원들의 정보를 이름, 급여 순으로 조회
select first_name, salary from employees where first_name like '%o%a';

문제) 이름이 H로 시작하면서 6글자 이상인 사원들의 정보를 사번, 이름 순으로 조회
select employee_id ,first_name from employees where first_name like'H_ _ _ _ _%';

문제) 사원테이블에서 이름에 s자가 포함되어 있지 않은 사원들만 사번, 이름으로 검색하시오
select employee_id, first_name from employees where first_name not like'%s%';

LIKE를 사용하여 여러 개의 문자를 검색하기 위해서는 OR연산자를 사용하여 여러개의 LIKE 조건을 부여할 수 있다.
예시) SELECT * FROM EMPLOYEES WHERE FIRST_NAME LIKE '%el%' OR FIRST_NAME LIKE '%en%';

언더바 문자 자체를 조회하고 싶으면 이스케이프 문자를 사용해야 한다.
'%\_%'

```
## INSERT
```SQL
INSERT INTO TBL_STUDENT
(ID, NAME, MAJOR, GENDER, BIRTH)
VALUES(0,'한동석','컴퓨터공학과','A',to_date('1980-01-02','YYYY-MM-DD'));

ban_char 위반 오류 뜸

INSERT INTO TBL_STUDENT
(ID, NAME, MAJOR, GENDER, BIRTH)
VALUES(0,'한동석','컴퓨터공학과','M',to_date('1979-01-02','YYYY-MM-DD'));

ban_date 위반 오류 뜸

INSERT INTO TBL_STUDENT
(ID, NAME, MAJOR, GENDER, BIRTH)
VALUES(0, '한동석', '컴퓨터공학과', 'M' , to_date('2000-05-05','YYYY-MM-DD'));

SELECT * FROM TBL_STUDENT;

INSERT INTO TBL_STUDENT
(ID,NAME,MAJOR,BIRTH) --GENDER 생략해보기
VALUES(0,'홍길동','컴퓨터공학과',TO_DATE('2000-09-05','YYYY-MM-DD'));

STD_PK 위반 오류 학번이 같을수는 없다!

INSERT INTO TBL_STUDENT
(ID,NAME,MAJOR,BIRTH) --GENDER 생략해보기
VALUES(1,'홍길동','컴퓨터공학과',TO_DATE('2000-09-05','YYYY-MM-DD'));

GENDER를 넣지 않았지만 오류가 나지 않는다 DEFAULT 값으로 여자로 넣었기 때문에

```
## DELETE
```SQL
--삭제 : 부모와 자식중 자식테이블에서 참조하는 값들을 먼저 삭제해야 한다.

DELETE FROM POT WHERE NAME = '장미';
DELETE FROM FLOWER WHERE FLOWERNAME = '장미';
```

## UPDATE
```SQL
UPDATE POT
SET POTCOLOR = 'WHITE'
WHERE NAME = '할미꽃' AND POTSHAPE = '타원형';
```

### ORDER BY (정렬)
- 질의 결과에 반환되는 행들을 특정 기준으로 정렬하고자 할 때 사용
- ORDER BY절은 SELECT절의 가장 마지막에 기술
- ASC : 오름차순(생략가능)
- DESC: 내림차순(생략불가)

```SQL
예) 사원테이블에서 급여를 많이받는 사원순으로 사번, 이름, 급여, 입사일을 출력하시오 단, 급여가 같을 경우
     입사일이 빠른순으로 정렬
SELECT EMPLOYEE_ID,FIRST_NAME,SALARY,HIRE_DATE FROM EMPLOYEES ORDER BY SALAY DESC, hire_date ASC;
오름차순은 안써도 defalut로 적용 조건(WHERE)절이 없다면 그냥 FROM 뒤에 ORDER BY를 적는다.

정렬을 하고 봤더니 똑같은 급여를 받는 사람이 생각보다 많다. 이런 경우에 먼저 입사한 사람을 먼저 보여주면 좋겠는데 내가 정렬
하고자 하는 기준이 똑같을 때 다른 정렬 기준을 두번째 세번째 추가적으로 정렬기준을 정할 수 있다.

문제)사원테이블에서 부서번호가 빠른순, 부서번호가 같다면 직종이 빠른순, 직종까지 같다면 급여를 많이 받는순으로
	사번,이름, 부서번호, 직종,급여순으로 출력

select employee_id, first_name, department_id, job_id, salary
from employees 
order by department_id, job_id, salary DESC;

문) 급여가 15000이상인 사원들의 사번, 이름, 급여, 입사일을 입사일이 빠른 순으로 조회

SELECT EMPLOYEE_ID, FIRST_NAME, SALARY, HIRE_DATE FROM EMPLOYEES WHERE SALARY >=15000 ORDER BY HIRE_DATE ASC;
```
