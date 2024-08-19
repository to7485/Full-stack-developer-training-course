# SUBQUERY
- 특정 sql문장 안에 또 다른 sql문장이 포함되어 있는 것
- 여러번 DB접속이  필요한 상황을 한번으로 줄여서 속도를 증가시킬 수 있다.
- 서브쿼리를 사용할 수 있는 곳.
  1) where, having
  2) select, delete문의 from절
  3) update문의 set
  4) insert문의 into
```SQL
예) 사원테이블에서 이름이 'Michael'이고, 직종이 'MK_MAN'인 사원의 급여보다
많이 받는 사원들의 정보를 사번, 이름, 직종, 급여 순으로 출력

데이터베이스에 한번만 접근을 하는걸로는 답을 구하기가 어렵다.

1) 이름이 Michael이고, 직종이 'MK_MAN'인 사원의 급여 구하기
  select salary from employees where first_name = 'Michael' and job_id = 'MK_MAN'; --13000

2)13000보다 급여가 높은 사원들의 정보
  select employee_id, first_name, job_id, salary from employees where salary > 13000;

SELECT문을 몇개 작성해야하는지 알면 SUBQUERY를 작성하는건 어렵지 않다.

3) 위의 두 쿼리문을 subquery를 통해 하나로 합쳐보자
select employee_id, first_name, job_id, salary
from employees
where salary > (select salary
		 from employees 
		 where first_name = 'Michael' and job_id = 'MK_MAN');

문제) 사번이 150번인 사원의 급여와 같은 급여를 받는 사원들의 정보를 사번, 이름, 급여 순으로 출력
select employee_id, first_name, salary
from employees 
where salary = (select salary 
		from employees 
		where employee_id = 150);

문제) 월급이 회사의 평균월급 이상인 사람들의 이름과 월급을 조회
select first_name, salary from employees where salary>=(select avg(salary) from employees);


문제) 사번이 111번인 사원의 직종과 같고 사번이 159번인 사원의 급여보다 많이 받는 사원들의 정보를 사번, 이름, 직종, 급여 순으로 출력
select employee_id,FIRST_NAME, job_id, salary 
from employees 
where JOB_ID = (SELECT JOB_ID FROM EMPLOYEES
		WHERE EMPLOYEE_ID = 111)
		AND SALARY > (SELECT SALARY 
				FROM EMPLOYEES
				WHERE EMPLOYEE_ID = 159);

문제) 직종, 평균급여를 출력하되
평균급여가 Bruce사원보다 큰(초과) 경우를 조회
SELECT JOB_ID, AVG(SALARY)
FROM EMPLOYEES
GROUP BY JOB_ID,
HAVING AVG(SALARY) > (SELECT SALARY
			FROM EMPLOYEES
			WHERE FIRST_NAME = 'Bruce');

문제) 사원테이블에서 성에 'Bat'이라는 단어를 포함하고 있는 사원과 같은 부서에서 근무하는 사원의 부서번호,이름을 출력
select department_id, first_name, last_name
from employees
where department_id = (select department_id 
			from employees 
			where last_name like 'Bat%');
      
문제) Bruce와 같은 부서에서 근무하고 있는 사원들의 이름을 출력
select first_name from employees where department_id = (select department_id from employees where first_name='Bruce');


문제) 사워테이블에서 last_name이 Kochhar의 급여보다 많이받는 사원들의 사번, 성,직종, 급여를 출력
select employee_id, last_name, job_id,salary from employees where salay > (select salary from employees where last_name ='Kochhar');

문제) 사원테이블에서 급여가 가장 적은 사람의 사번, 이름, 급여를 출력
select employee_id, first_name, salary from employees where salary = (select MIN(salary) from employees);

문제) 사원테이블에서 직종이 SA_REP인 사원의 최소급여보다 적으면서(미만) 직종이 SH_CLERK은 아닌 사원들의 이름 직종 급여를 출력
select first_name, job_id, salary from employees where salary <(select MIN(salary) from employees where job_id = 'SA_REP') and not job_id = 'SH_CLERK';
														-- job_id !='SH_CLERK'
														-- job_id NOT IN('SH_CLERK')
														-- job_id <> 'SH_CLERK';

문제) 사원테이블에서 100번 부서의 최소 급여보다 많이 받는(초과) 다른 모든 부서의 부서번호, 최소급여를 출력하세요
select department_id,MIN(salary) from employees group by department_id having MIN(salary) > (select MIN(salary) from employees where department_id = '100');


문제) 137번 사원보다 월급이 크거나 같고 149번 사원보다는 월급이 작거나 같은 사원의 이름과 월급을 조회
select first_name, salary 
from employees 
where salary between (select salary 
                      from employees where employee_id = 137) and (select salary 
                                                                   from employees where employee_id = 149);
```

# CONCATENATION(연결)
- CONCATENATION(연결) : ||

```SQL
--EMPLOYEES 테이블에서 사원들의 이름 연결하기
SELECT FIRST_NAME||' '||LAST_NAME FROM EMPLOYEES;

--OO의 급여는 OO이다.
SELECT FIRST_NAME||'의 급여는'||SALARY||'이다' FROM EMPLOYEES;
```

# AS(ALIAS)
- AS(ALIAS) : 별칭(컬럼이 너무 길다면 별명을 쥐서 대신 사용할 수 있음)
    - SELECT절
        - AS 뒤에 별칭 작성(대소문자를 구분할 때, 공백문자가 들어갈 때, 특수문자가 들어갈 때는 쌍따옴표에 꼭 감싸야 한다.)
        - 한칸 띄우고 작성
    - FROM절 : 한 칸 띄우고 작성

## 별칭의 특징
- 테이블에 별칭을 줘서 컬럼을 단순, 명확히 할 수 있다.
- 현재의 SELECT 문장에서만 유효하다.
- 테이블 별칭은 길이가 30자까지 가능하나 짧을수록 좋다.
- 테이블 별칭에는 의미가 잇어야 한다.
- FROM절에 테이블 멸칭 설정시 해당 테이블 별칭은 SELECT문장에서 테이블 이름 대신에 사용한다.

```SQL
SELECT COUNT(SALARY) AS 갯수,
       MAX(SALARY) AS 최대값,
       MIN(SALARY) AS 최소값,
       SUM(SALARY) AS 합계,
       AVG(SALARY) AS 평균 FROM EMPLOYEES;

--EMPLOYEES 테이블에서EMPLOYEE_ID를 "사번"으로 FIRST_NAME을 "이름"로, SALARY를 "급여"로 바꿔서 검색
SELECT EMPLOYEE_ID AS "사번", FIRST_NAME AS "이름", SALARY AS "급여" FROM EMPLOYEES;

두개 이상의 테이블에서 각각의 컬럼을 조회하려고 한다면 어떤테이블에서 온 컬럼인지 확실하게 적어줘야 한다.
SELECT EMPLOYEES.DEPARTMENT_ID, EMPLOYEES.DEPARTMENT_ID 
FROM EMPLOYEES, DEPARTMENTS;

근데 테이블명이 길기 때문에 FROM절에서 별칭을 준다.
SELECT E.DEPARTMENT_ID, D.DEPARTMENT_ID 
FROM EMPLOYEES E, DEPARTMENTS D;
```

# JOIN
- 데이터베이스에서 '두 개 이상의 테이블'을 연결하여 '하나의 결과의 테이블'로 만드는 것을 의미한다.
- 이를 통해 데이터를 효율적으로 검색하고 처리하는데 도움을 준다.
- JOIN을 사용하는 이유는 데이터베이스에서 테이블을 분리하여 '데이터 중복을 최소화'하고 '데이터의 일관성'을 유지하기 위함이다.
- 여러가지 JOIN의 방식이 있으며 JOIN방식에 따라 결과가 달라진다.

## JOIN의 종류
### 1. Inner Join
- 각 테이블에서 조인 조건에 일치되는 데이터만 가져온다.
- A와 B테이블의 공통된 부분을 의미한다 보통 교집합 이라고 부른다.

```SQL
테이블명A INNER JOIN 테이블명B ON 조건식
테이블명A JOIN 테이블명B ON 조건식
```

![image](https://user-images.githubusercontent.com/54658614/230700010-b6b1bb7d-ad38-4478-bff7-d029b76c05b1.png)

- INNER JOIN은 교집합 연산과 같다. JOIN 하는 컬럼 값이 양쪽 테이블 데이터 집합에서 공통적으로 존재하는
데이터만 조인해서 결과 데이터 집합으로 추출

```SQL
<사용법>
SELECT 컬럼명1,컬럼명
FROM TABLE A (INNER) JOIN TABLE B
ON TABLEA.조인컬럼 = TABLEB.조인컬럼

SELECT 컬럼명1,컬럼명
FROM TABLE A , TABLE B
WHERE TABLEA.조인컬럼 = TABLEB.조인컬럼

```
### 1-1. SELF INNER JOIN
- 하나의 테이블 내에서 다른 컬럼을 참조하기 위해 사용하는 '자기 자신과의 조인'방법이다.
- 이를 통해 데이터베이스에서 한 테이블 내의 값을 다른 값과 연결할 수 있다.

```SQL
SELECT 테이블1.열, 테이블2.열
FROM 테이블1 t1
JOIN 테이블1 t2
ON 테이블1.열 = 테이블2.열;
```

### 1-2. CROSS INNER JOIN
- 두 개 이상의 테이블에서 '모든 가능한 조합'을 만들어 결과를 반환하는 조인 방법이다.
- 이를 통해 두 개 이상의 테이블을 조합하여 새로운 테이블을 생성할 수 있습니다
- Cross Join은 일반적으로 테이블 간의 관계가 없을 때 사용된다.
- 각 행의 모든 가능한 조합을 만들기 때문에 결과가 매우 큰 테이블이 될 수 있으므로 사용에 주의가 필요하다.

```SQL
SELECT 테이블1.열, 테이블2.열
FROM 테이블1 
CROSS JOIN 테이블2;
```

### 예제
```sql
CREATE TABLE 테이블A(
	A_id NUMBER,
	A_name varchar2(10)
);

CREATE TABLE 테이블B(
	B_id NUMBER,
	B_name varchar2(20)
);


INSERT INTO 테이블A values(1, 'John');
INSERT INTO 테이블A values(2, 'Jane');
INSERT INTO 테이블A values(3, 'Bob');

INSERT INTO 테이블B values(101, 'Apple');
INSERT INTO 테이블B values(102, 'Banana');


SELECT * FROM 테이블A CROSS JOIN 테이블B;
```
<hr>

### OUTER JOIN
- OUTER JOIN은 두 테이블에서 '공통된 값을 가지지 않는 행들'도 반환한다.
- Left Outer join, Right Outer join, Full Outer Join의 종류가 있다.

### 2. LEFT OUTER JOIN
- '왼쪽 테이블의 모든 행'과 '오른쪽 테이블에서 왼쪽 테이블과 공통된 값'을 가지고 있는 행들을 반환한다.
- 교집합의 연산결과와 차집합의 연산 결과를 합친것과 같다.
- 만약 오른쪽 테이블에서 공통괸 값을 가지고 있는 행이 없다면 NULL값을 반환한다.

![image](https://user-images.githubusercontent.com/54658614/230700152-a35a75ee-fa7a-4560-8f46-06075f033af4.png)

```SQL
<사용법>

SELECT 컬럼명1,컬럼명
FROM TABLE A LEFT OUTER JOIN TABLE B
ON TABLEA.조인컬럼 = TABLEB.조인컬럼
```

### 3. RIGHT OUTER JOIN
- LEFT OUTER JOIN의 반대이다.
- RIGHT OUTER JOIN 키워드의 오른쪽에 명시된 테이블에만 존재하는 데이터를 추출한다.

![image](https://user-images.githubusercontent.com/54658614/230700239-6fd82096-045a-4fbc-a077-25fbd4d78201.png)

<사용법>

```SQL
SELECT 컬럼명1,컬럼명
FROM TABLE A RIGHT OUTER JOIN TABLE B
ON TABLEA.조인컬럼 = TABLEB.조인컬럼
```

#### LEFT OUTER JOIN과 RIGHT OUTER JOIN중 무엇을 많이 사용할까?
- 상황에 따라 다르지만 대체로 'LEFT OUTER JOIN'을 더 많이 사용한다.
- 이는 대부분의 경우 왼쪽 테이블의 데이터를 중심으로 분석하고자 할 때가 많기 때문이다.

### 4. FULL OUTER JOIN
- 두 테이블에서 '모든 값'을 반환한다. 만약 공통된 값을 가지고 있지 않는 행이 있다면 NULL값을 반환한다.
- 합집합 연산 결과와 같다.
- 양쪽 테이블 데이터 집합에서 공통적으로 존재하는데이터, 한쪽에만 존재하는 데이터 모두 추출한다.

![image](https://user-images.githubusercontent.com/54658614/230700279-881f5fff-cc77-4f2d-8cfe-1c166f614356.png)

```SQL
<사용법>

SELECT 컬럼명1,컬럼명
FROM TABLE A FULL OUTER JOIN TABLE B
ON TABLEA.조인컬럼 = TABLEB.조인컬럼
```

```SQL
SELECT e.first_name, e.department_id, d.department_name -- -> 조건을 안써주면 그냥 맨위에꺼 가져옴
from employees e JOIN DEPARTMENTS d
ON e.department_id = d.department_id; ---> join에는 조건이 없을 수 없다.

--예) 부서(department), 지역(Locations)로 부터 부서이름과 city를 출력해보자

SELECT d.department_name, l.city 
FROM DEPARTMENTS d JOIN locations l
ON d.location_id = l.location_id;

--문) 지역(Locations), 나라(countries)를 조회하여 도시명과 국가명을 조회

SELECT L.CITY,C.COUNTRY_NAME
FROM LOCATIONS L JOIN COUNTRIES C
ON L.COUNTRY_ID = C.COUNTRY_ID;

--문) FIRST_NAME, LAST_NAME, JOB_ID, JOB_TITLE을 출력(EMPLOYEES,JOBS 테이블을 조회)

SELECT E.FIRST_NAME, E.LAST_NAME, J.JOB_ID, J.JOB_TITLE
FROM EMPLOYEES E JOIN JOBS J
ON E.JOB_ID = J.JOB_ID;

--문) 사원, 부서, 지역테이블로부터 FIRST_NAME, EMAIL, DEPARTMENT_ID, DEPARTMENT_NAME, LOCATION_ID,CITY
--정보를 출력하되, CITY가 'Seattle'인 경우만 출력하시오.

select e.first_name, e.email, e.department_id, d.department_name, d.location_id, l.city
from employees e JOIN departments d ON e.department_id = d.department_id
JOIN locations l ON d.location_id = l.location_id
and l.city = 'Seattle';

예시) 사원 테이블과 부서테이블의 LEFT OUTER JOIN을 이용하여 사원이 어느 부서에 있는지 조회하기
SELECT e.FIRST_NAME, d.DEPARTMENT_NAME
FROM employees e
LEFT OUTER JOIN departments d
ON e.DEPARTMENT_ID = d.DEPARTMENT_ID;

예시) 사원 테이블과 부서테이블의 RIGHT OUTER JOIN을 이용하여 사원이 어느 부서에 있는지 조회하기
SELECT e.FIRST_NAME, d.DEPARTMENT_NAME
FROM employees e
RIGHT OUTER JOIN departments d
ON e.DEPARTMENT_ID = d.DEPARTMENT_ID;

예시) 사원 테이블과 부서테이블의 FULL OUTER JOIN을 이용하여 사원이 어느 부서에 있는지 조회하기
SELECT e.FIRST_NAME, d.DEPARTMENT_NAME
FROM employees e
FULL OUTER JOIN departments d
ON e.DEPARTMENT_ID = d.DEPARTMENT_ID;
```
## 집합연산자
- JOIN과는 별개로 두개의 테이블을 합치는 방법이 있다.

### 1. UNION
- 두 개의 테이블에서 '중복을 제거하고 합친 모든 행'을 반환한다.

```SQL
SELECT 테이블1.컬럼1, 테이블1.컬럼2 FROM 테이블1
UNION
SELECT 테이블2.컬럼1, 테이블2.컬럼2 FROM 테이블2

-- EMPLOYEES 테이블과 DEPARTMENT테이블을 UNION한다.
-- 사원 이름과 부서이름의 모든 값을 가져와서 중복을 제거하고 합친다.
SELECT employees.FIRST_NAME FROM employees
UNION
SELECT departments.DEPARTMENT_NAME FROM departments;

출처: https://adjh54.tistory.com/155 [Contributor9:티스토리]
```

### 2. UNION ALL
- 두 개의 테이블에서 '중복을 제거하지 않고 모두 합친 모든 행'을 반환한다.

```SQL
SELECT 테이블1.컬럼1, 테이블1.컬럼2 FROM 테이블1
UNION ALL
SELECT 테이블2.컬럼1, 테이블2.컬럼2 FROM 테이블2

-- EMPLOYEES 테이블과 DEPARTMENT테이블을 UNION ALL한다.
-- 사원 이름과 부서이름의 모든 값을 가져와서 중복을 포함하여 합친다.
SELECT employees.FIRST_NAME FROM employees
UNION ALL
SELECT departments.DEPARTMENT_NAME FROM departments;


출처: https://adjh54.tistory.com/155 [Contributor9:티스토리]
```



# VIEW
- 하나 이상의 테이블이나 다른 뷰의 데이터를 볼 수 있게 하는 데이터베이스 객체이다.
- 실제 데이터는 뷰를 구성하는 테이블에 담겨 있지만 마치 테이블 처럼 사용할 수 있다.
- 테이블 뿐만 아니라 다른 뷰를 참조해 새로운 뷰를 만들어서 사용할 수 있다.

## VIEW의 사용 목적
- 코딩을 하다보면 여러개의 테이블에서 필요한 정보를 뽑아 사용할때가 많다.
- 이때 좀 더 편리하게 사용할 수 있는 방법중의 하나가 VIEW이다.
- VIEW를 사용하면 복잡한 쿼리문을 간단하게 만들어준다.
- 여러 테이브르이 JOIN과 GROUP BY같은 복잡한 쿼리를 VIEW로 저장시켜 놓으면 다음부터는 저장한 VIEW만 호출하면 된다.

## view의 특징

### 독립성 
- 테이블 구조가 변경되어도 뷰를 사용하는 응용 프로그램은 변경하지 않아도 된다.

### 편리성
- 복잡한 쿼리문을 뷰로 생성함으로써 관련 쿼리를 단순하게 작성할 수 있다.
- 또한 해당 형태의 SQL문을 자주 사용할 때 뷰를 이용하면 편리하게 사용할 수 있다.
      
### 보안성
- 직원의 급여정보와 같이 숨기고 싶은 정보가 존재한다면, 뷰를 생성할 때 해당 칼럼을 빼고 생성함으로써 사용자에게 정보를 감출 수 있다.

```SQL
-- VIEW의 생성
CREATE VIEW 뷰이름 AS
(
  쿼리문
)

-- VIEW의 수정
-- OR REPLACE 옵션은 기존의 정의를 변경하는 데 사용할 수 있다.
CREATE OR REPLACE VIEW 뷰이름 AS
(
  쿼리문
)

-- VIEW의 삭제
DROP VIEW 뷰이름 [RESTRICT OR CASCADE]
※RESTRICT : 뷰를 다른곳에서 참조하고 있다면 삭제가 취소된다.
※CASCADE : 뷰를 참조하는 다른 뷰나 제약 조건까지 모두 삭제된다.

```

```SQL
create view MY_EMPL AS
(
select employee_id, first_name, salary
from employees
);
SELECT * FROM MY_EMPL;

------------------------------------------------------------

create view MY_EMPL AS---> AS가 없으면 VIEW가 만들어 지지 않는다.
(
select employee_id, first_name, salary, (SALARY * COMMISSION_PCT) COMM
FROM EMPLOYEES
);
SELECT * FROM MY_EMPL;

---------------------------------------------------

create view DATA_PLUS AS
(
SELECT S.*,(S.COMMISSION_PCT * S.SALARY) COMM
FROM ( SELECT * FROM EMPLOYEES) S
	--EMPLOYEES S; 도 가능하다
);
SELECT * FROM DATA_PLUS;

------------------------------------------------------------

CREATE view DATA_PLUS AS
(
SELECT S.SALARY, RANK() OVER(ORDER BY SALARY DESC) rank
FROM EMPLOYEES S
);


SELECT * FROM DATA_PLUS;

------------------------------------------------------------

create view TEST AS
(
SELECT E.EMPLOYEE_ID, D.DEPARTMENT_NAME
FROM EMPLOYEES E, DEPARTMENTS D
WHERE E.DEPARTMENT_ID = D.DEPARTMENT_ID
);
SELECT * FROM TEST;
```
