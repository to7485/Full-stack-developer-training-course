# TCL(Transaction Control Language): (DML을 위한 명령어) 트랜젝션 제어 언어
- 트랜잭션 : 데이터베이스의 작업을 처리하는 논리적 연산 단위[분리될 수 없는 최소 단위]
    - 어떠한 작업을 하기 위해서는 Select ,Insert, Update 를 사용해야 하는데 이걸 하나의 작업 단위라고 한다.


## 트랜잭션의 특성
- 원자성(Atomicity) : 원자와 같이 데이터베이스 연산들이 나눌수도, 줄일수 없는 하나의 유닛으로서 취급됨.
    - 트랜잭션에 정의된 연산들은 모두 성공적으로 실행되던지 아니면 전혀 실행되지 않은 상태로 남아야 함

```SQL
10,000원이 든 계좌 A에서 0원이 든 계좌 B로 돈 10,000원을 입금한다.
-- query1
UPDATE 계좌
SET 잔액 = 0
WHERE 계좌번호 = A;
-- query2
UPDATE 계좌
SET 잔액 = 10000
WHERE 계좌번호 = B;
``` 
- 일관성(Consistency) : 데이터베이스의 트랜잭션이 제약조건, cascades, triggers를 포함한 정의된 모든 조건에 맞게 데이터 값이 변경됨
    - 트랜잭션 실행 전의 데이터베이스 내용이 잘못되지 않으면 트랜잭션 실행 후에도 데이터베이스 내용이 잘못되면 안됨

- 고립성(Isolation) : 특정 DBMS에서 다수의 유저들이 같은 시간에 같은 데이터에 접근하였을 때 수행중인 트랜잭션이 완료될 때 까지<br> 다른 트랜잭션의 요청을 막음으로서 데이터가 꼬이는걸 방지한다.
    - 트랜잭션 실행 도중에 다른 트랜잭션의 영향을 받아 잘못된 결과를 만들면 안됨

- 영속성,지속성(Durability) : 트랜잭션 실행이 성공적일 때, 그 트랜잭션이 갱신한 데이터베이스 내용은 영구적으로 저장됨.


## TCL의 종류

- COMMIT : DML로 변경된 데이터를 데이터베이스에 적용할 때 사용
  - INSERT,UPDATE,DELETE문 등을 사용한 후 변경 작업을 데이터베이스에 반영하기 위해 사용
  - COMMIT문 사용시 이전 데이터는 영원히 지워짐
  - COMMIT문 사용시 모든 사용자가 변경된 데이터 확인 가능
  - SQLServer는 기본적으로 AUTO COMMIT모드이므로 자동으로 COMMIT을 수행한다.<br> (DML문이 성공하면 자동으로 COMMIT을 실행한다.)
  - COMMIT 실행시 하나의 트랜잭션 과정을 종료<br> → COMMIT이 실행되기 전에 다른 사용자가 완료되지 않은 데이터를 보거나 변경할 수 없음<br>

사용법 : COMMIT;<br>

- ROLLBACK : DML로 변경된 데이터를 변경 이전 상태로 되돌릴 때 사용
    - 데이터에 대한 변경사항 취소
    - ROLLBACK문 사용시 이전 데이터 다시 재저장 -> COMMIT되지 않은 상위 트랜잭션을 모두 ROLLBACK시킴
    - ROLLBACK문 사용시 관련 행의 잠금(LOCKING)이 풀려 다른 사용자들이 데이터 변경 가능
    - SQL Server는 기본적으로 AUTO COMMIT모드이므로 자동으로 COMMIT, 오류가 발생하면 자동으로 ROLLBACK처리

사용법 : ROLLBACK;<br>

- SAVEPOINT : 오류 복구 처리에 효과적인 방법 -> 전체 트랜잭션을 ROLLBACK하지 않고도 오류 복귀 가능
    - 효과적으로 오류 복구 처리를 위해 저장점을 저장할 때 사용<br> -> 전체 트랜잭션을 ROLLBACK하지 않고 현시점에서 SAVEPOINT까지 일부 트랜잭션만 오류 복귀 가능
    - 복잡한 대규모 트랜잭션에서 에러가 발생했을 때 주로 사용
    - 복수의 저장점 정의 가능
    - 저장점까지 롤백할 때는 "ROLLBACK TO 저장점;" 사용

사용법 : SAVEPOINT 세이브포인트이름;<br>
ROLLBACK TO 세이브포인트이름;<br>

```SQL
디비버는 AUTO COMMIT 상태가 default이다.
위 작업표시줄에 T 모양을 눌러 수동 COMMIT으로 바꾸자.

-- EMPLOYEES 테이블에서 JOB_ID가 'IT_PROG'인 사람들의 이름을 자신의 이름으로 바꾸기
UPDATE EMPLOYEES
SET FIRST_NAME = '이현준'
WHERE JOB_ID = 'IT_PROG';

SELECT * FROM EMPLOYEES WHERE JOB_ID = 'IT_PROG';
이름이 전부 바뀐걸 확인하고 잘못 바꿨다고 생각하면 위에 롤백 버튼을 눌러 원래대로 되돌리면 된다.

-- EMPLOYEES 테이블에서 JOB_ID가 'IT_PROG'인 사람들 삭제하기
DELETE FROM EMPLOYEES
WHERE JOB_ID = 'IT_PROG';

-- EMPLOYEES 테이블에서 급여가 8000이상인 사람 삭제하기
DELETE FROM EMPLOYEES
WHERE SALARY >= 8000;
```
## CASE문
- CASE WHEN THEN ELSE END 어떠한 조건에 맞춰 값을 출력해주는 문법
- CASE WHEN 조건식 THEN '참 값' ELSE '거짓 값' END

데이터의 값을 WHEN의 조건과 차례대로 비교한 후 일치하는 값을 찾아 THEN 뒤에 있는 결과값을 리턴합니다.<br>
 
ELSE는 일치하는 값이 없을 때 선택할 디폴트값인데 필요 없으면 생략할 수 있습니다.<br>
WHEN의 값 중 일치하는 것이 없고 ELSE도 없다면 CASE 문은 NULL을 리턴합니다.<br>


```SQL

SELECT ename
     , deptno
     , CASE WHEN deptno = '10' THEN 'New York'
            WHEN deptno = '20' THEN 'Dallas'
            ELSE 'Unknown'
       END AS loc_name
  FROM emp
 WHERE job = 'MANAGER';
 
 
SELECT ROUND(AVG(CASE JOB_ID WHEN 'IT_PROG' THEN SALARY END),2) 평균급여

FROM EMPLOYEES;
CASE 와 WHEN 사이에 비교하고자 하는 Column 을 넣고
WHEN 과 THEN 사이에 비교하고자 하는 값을 넣어서 비교하는 방법입니다.
 
 SELECT ename
     , deptno
     , CASE deptno 
            WHEN 10 THEN 'New York'
            WHEN 20 THEN 'Dallas'
            ELSE 'Unknown'
       END AS loc_name
  FROM scott.emp
 WHERE job = 'MANAGER'
 
 -- where절에서의 사용
 SELECT ename, sal, CASE
			WHEN sal >= 2900 THEN '1등급'
			WHEN sal >= 2700 THEN '2등급'
			WHEN sal >= 2000 THEN '3등급'
		END AS SAL_GRADE
FROM EMP a
WHERE job = 'MANAGER' AND (CASE WHEN sal >= 2900 THEN 1
				WHEN sal >= 2700 THEN 2
				WHEN sal >= 2000 THEN 3
			    END) = 1;


--EMP 테이블에서 SAL 3000이상이면 HIGH 1000이상이면 MID, 다 아니면 LOW
SELECT * FROM EMP;
SELECT ENAME 사원명, SAL 급여,
CASE
		WHEN SAL >= 3000 THEN 'HIGH'
		WHEN SAL >= 1000 THEN 'MID'
		ELSE 'LOW'
END
FROM EMP;

만약 WHEN 뒤의 조건 중 참인 것이 두 개 이상이라면 먼저 만나는 조건을 선택합니다.
CASE 문은 전체적으로 하나의 값으로 평가되며 값이 올 수 있는 모든 곳에 올 수 있습니다.
따라서 SELECT 문의 필드 목록에 사용할 수도 있고 WHERE 절의 조건문에도 사용할 수 있습니다.


--STADIUM 테이블에서 SEAT_COUNT 0DLTKD 30000이하면 'S'
--30001이상 50000이하면 'M' 다 아니면 'L'
--중첩 케이스문
SELECT STADIUM_NAME 경기장, SEAT_COUNT 좌석수,
	CASE
		WHEN SEAT_COUNT BETWEEN 0 AND 30000 THEN 'S'
		ELSE
		(
		CASE
			WHEN SEAT_COUNT BETWEEN 30001 AND 50000 THEN 'M'
			ELSE 'L'
		END
		)
	END
FROM STADIUM;

--PLAYER 테이블에서 WEIGHT가 50이상 70이하이면 'L'
--71이상 80이하면 'M' NULLL이면 '미등록' 다 아니면 'H'
SELECT PLAYER_NAME 선수이름 ,WEIGHT||'KG' 몸무게,
	CASE
		WHEN WEIGHT BETWEEN 50 AND 70 THEN 'L'
		WHEN WEIGHT BETWEEN 71 AND 80 THEN 'M'
		ELSE
		(
		CASE 
			WHEN WEIGHT IS NULL THEN '미등록'
			ELSE 'H'
		END
		)
	END 체급
FROM PLAYER; 
```

## PL/SQL
-오라클에서 지원하는 프로그래밍 언어의 특성을 수용하여 SQL에서는 사용할 수 벗는 절차적
-프로그래밍 기능을 가지고 있어 SQL의 단점을 보완하였다.

### PL/SQL문을 사용하는 이유
- 대용량 데이터를 연산해야 할 때, WAS등의 서버로 전송해서 처리하려면 네트워크에 부하가 많이 걸린다.
- 이때 프로시저나 함수를 사용하여 데이터를 연산하고 가공한 후에 , 최종 결과만 서버에 전송하면
- 부담을 많이 줄일 수 있다.
- 로직을 수정하기 위해 서버를 껐다 켜지 않아도 된다. 서버에서는 단순히 DB에 프로시저를 호출하여 사용하면 된다.
- 쿼리문을 직접 노출하지 않는 만큼, SQL injection의 위험성이 줄어든다.

## PL/SQL의 기본구조
```SQL
DECLARE(선언부) PL/SQL문에서 사용하는 모든 변수나 상수를 선언하는 부분

IS 

BEGIN(실행부) 절차적으로 SQL문을 실행할 수 있도록 절차적인 언어의 요소인 제어문, 반복문 함수의 정의 등 로직을 기술할 수 있는 부분
  쿼리문을 작성할 수 있다.
END(실행문종료)
```

## PL/SQL문의 종류
- 프로시저 : 리턴 값을 하나 이상 가질 수 있는 프로그램
- 함수 : 리턴 값을 반드시 반환해야 하는 프로그램
- 패키지 : 하나 이상의 프로시저, 함수, 변수 등의 묶음
- 트리거 : 지정된 이벤트가 발생하면 자동으로 실행되는 PL/SQL블록



### 오라클에서 콘솔로 보는 방법은 PUT_LINE이라는 프로시저를 사용
```SQL
 DBMS_OUTPUT.PUT_LINE('출력할 내용');
```

## 변수의 선언
```SQL
DECLARE
NAME VARCHAR2(20) := '홍길동';
AGE NUMBER(3) := 30;
BEGIN
	DBMS_OUTPUT.PUT_LINE('이름 : '|| NAME ||CHR(10)||'나이 : '|| AGE);
END;
```

## IF문

1. IF 조건 THEN 실행문;<br>END IF;
2. IF 조건 THEN 실행문;<br>ELSE 실행문;<br>END IF;
3. IF 조건 THEN 실행문;<br>ELSIF 조건문 THEN 실행문;<br>ELS 실행문;<br>END IF;

### 점수에 맞는 학점 출력하기

```SQL
DECLARE declare [선언부] - 변수, 상수를 선언할 수 있습니다
	SCORE NUMBER := 80; =은 같다 라는 뜻이기 때문에 :=로 써줘야 대입이 된다.
	GRADE VARCHAR2(5); 어떤 학점인지 정확히 할 수 없기 때문에 초기화를 할 수 없다.
BEGIN
	IF SCORE >= 90 THEN GRADE := 'A';
	ELSIF SCORE >= 80 THEN GRADE := 'B';
	ELSIF SCORE >= 70 THEN GRADE := 'C';
	ELSIF SCORE >= 60THEN GRADE := 'D';
	ELSE GRADE := 'F';
END IF;
DBMS_OUTPUT.ENABLE;
DBMS_OUTPUT.PUT_LINE('당신의 점수: '||SCORE||'점'||CHR(10)||'학점: '||GRADE);
END;

```
## 반복문

### 1. FOOR LOOP문
```SQL
FOR index in [REVERSE] 시작값 .. END값 LOOP
	STATEMENT 1    
	STATEMENT 2    
	...
END LOOP;

```
- index는 자동 선언되는 binary_integer형 변수이고, 1씩 증가 한다.
- REVERSE 옵션이 사용될 경우 index는 upper_bound에서 lower_bound까지 1씩 감소한다.
- IN 다음에는 SELECT문이 올 수 있다.

```SQL
BEGIN	FOR i in 1..4 LOOP	  	
		if mod(i, 2) = 0 then 			
			dbms_output.put_line( i || '는 짝수!!');		
		else
			dbms_output.put_line( i || '는 홀수!!');	
		end if;
	END LOOP;
END;

```
### 2. LOOP문
```SQL
LOOP
	PL/SQL STATEMENT 1
	다른 LOOP를 포함하여 중첩으로 사용 가능
	EXIT [WHEN CONDITION];
END LOOP;
```
- EXIT문이 사용되었을 경우, 무조건 LOOP문을 빠져나간다.
- EXIT WHEN 조건이 사용될 경우 WHEN절에서 LOOP를 빠져나가는 조건을 제어할 수 있다.


## 프로시저(PROCEDURE)
- PL/SQL의 대표적인 부 프로그램에 프로시저가 있다.
- 데이터베이스에 대한 일련의 작업을 정리한 절차를 RDBMS에 저장한 것으로 영구 저장 모듈이라고도 합니다.
- 일련의 쿼리를 마치 하나의 함수처럼 실행하기 위한 쿼리의 집합입니다.
- 거의 함수와 비슷하다.

### 장점
- 하나의 요청으로 여러 SQL문을 실행시킬 수 있습니다.
- 네트워크 소요 시간을 줄여 성능을 개선할 수 있습니다.
- 기능변경이 편하다.

### 단점
- 문자나 숫자 연산에 사용하면 오히려 C,JAVA보다 느린 성능을 볼 수 있다.
- 유지보수가 쉽지 않다.

## 프로시저의 생성
```SQL
CREATE OR REPLACE PROCEDURE 프로시져이름 (
        매개변수1 IN 데이터타입:= 값,
        매개변수2 IN 데이터타입%TYPE
)

IS
  함수 내에서 사용할 변수, 상수 등 선언 , 밑에서 반복되서 사용될 문장을 하나로 선언해서 사용하겠다.

BEGIN

    실행할 문장

END 프로시져 이름;
```

프로시저 사용시 매개변수를 정의한 순서에 맞게 값을 넣어줘야 전달이 된다.

```SQL
CALL 프로시저의 이름(값1,값2)
```

## day09 스크립트 생성하기
- 오라클에서 화면 출력을 위해서는 PUT_LINE이란 프로시저를 이용합니다.
- PUT_LINE은 오라클이 제공하는 프로지서로서, DBMS_OUTPUT 패키지에 묶여 있습니다!
- 그래서 PUT_LINE을 사용할때에는 DBMS_OUTPUT.PUT_LINE과 같이 사용을 해야 합니다.

```sql
BEGIN
	DMBS_OUTPUT.PUT_LINE('HELLO');
END;
```

![image](https://github.com/to7485/DBMS1900/assets/54658614/3d5c8cee-8dbb-4dab-845a-f68b94d1a07c)

실행을 하면 결과를 내기 위한 권한이 없다고 나온다 CMD 창으로 이동을해서 권한을 줘보자.

```
CMD SQLPLUS SYS AS SYSDBA
1111로 접속

set serveroutput on ->서버에서 출력하는 거를 on으로 설정해라
EXIT
```

전체 구역 잡고 실행하기 

![image](https://github.com/to7485/DBMS1900/assets/54658614/e82b78ba-07f1-491e-a3ac-a819f6e12b62)

## 간단한 프로시저 만들어보기

![image](https://github.com/to7485/DBMS1900/assets/54658614/e3a34547-86e6-4150-a3a6-85637f282534)

X에 3을 넣는다고 가정하면 3이라는 값을 X에 전달하게 되고 X가 우측에 2X+1의 식에 값을 전달하게 되서 결과값이 나오게 된다.<br>
X의 역할은 외부에서 전달된 값과 F라는 함수를 연결해주는 매개체의 역할을 한다.

```SQL
CREATE OR REPLACE PROCEDURE F 프로시저 이름
(
	X  IN NUMBER 외부에서 전달받을 값이 있으면 매개변수에 정리를 해놓는다.
	   (외부에서 전달을 받을거라면 IN을 써야 한다.IN은 생략이 가능하다)
)
IS IS영역에다가 연산을 할껄 써야되는데 2X+1를 쓸껀데 변수를 선언할 필요는 없다.
BEGIN 
	DBMS_OUTPUT.ENABLE;
	DBMS_OUTPUT.PUT_LINE(2*X+1);
END;

호출 CALL F(2);

```

## 프로시저와 SQL
- 우리가 그동안 배운 DML과 프로시저를 접목시켜보자.

### JOBS테이블에 데이터를 INSERT해주는 프로시저 만들기
- 매번 INSERT INTO JOBS VALUES()를 해서 써주기가 너무 귀찮다.
- 프로시저를 만들어서 CALL 프로시저명(값1,값2...)만 해서 INSERT를 대신할 수 있다.

```SQL
SELECT * FROM JOBS; -> 4개의 컬럼값을 갖고 있는걸 확인할 수 있다.

CREATE OR REPLACE PROCEDURE MY_NEW_JOB_PROC -> 프로시저 이름이 조금 길긴한데 프로시저의 기능을 잘 설명하기 위해서는 조금 길어져도 상관이 없다.
(
	우리가 해당 테이블에 INSERT를 하기 위해서는 컬럼이 4개니까 4개의 값을 외부에서 받아야한다.
	그런데 사용자가 무슨 값을 넣을지 예측할 수 없다. 그렇기 때문에 CALL할때 전달해주는 값을 받아줄 매개변수가 있어야 한다.

	P_JOB_ID IN JOBS.JOB_ID%TYPE, ->JOB_ID의 타입을 그대로 가져가겠다.
	P_JOB_TITLE IN JOBS.JOB_TITLE%TYPE,
	P_MIN_SALARY IN JOBS.MIN_SALARY%TYPE,
	P_MAX_SALARY IN JOBS.MAX_SALARY%TYPE
)
IS
BEGIN
	INSERT INTO JOBS(JOB_ID,JOB_TITLE,MIN_SALARY, MAX_SALARY)
	VALUES(P_JOB_ID,P_JOB_TITLE,P_MIN_SALARY,P_MAX_SALARY);
	DBMS_OUTPUT.ENABLE;
	DBMS_OUTPUT.PUT_LINE('ALL DONE ABOUT '||' '||P_JOB_ID);
END;

```
- CREATE부터 END;까지 드래그하고 실행하기

```SQL
CALL MY_NEW_JOB_PROC('IT', 'Developer', 14000, 20000);

SELECT * FROM JOBS;

```
- 다시 프로시저를 실행하게 되면 PK 위반이라서 오류가 나게 된다.
- 오류가 나게 하는것이 아니라 PK가 겹치게 되면 수정이 되거나 삭제가되게 만들어보자.


## 프로시저 수정하기
- INSERT기능을 하는 프로시저를 만들었는데 PK제약조건으로 인해 겹칠 때가 있다.
- 데이터가 겹치가 되면 오류를 내는게 아니라 UPDATE를 해서 내용을 덮어버리자.

### 2023.12.13 오류 발견
- 무슨 이유인지는 모르겠으나  SQL문에는 이상이 없지만 커서를 end 끝에 두고 실행하면 오류간 나는 경우가 있다.
- CREATE부터 END까지 드래그를 한 후 실행을 하고 실행을 하면 프로시저가 문제없이 등록이 된다.

```SQL
CREATE OR REPLACE PROCEDURE MY_NEW_JOB_PROC
(--안에 개변수를 넣어야 하는데 현재 JOBS 테이블에서는 4개를 넣어야 한다.
 --사용자가 어떤걸 넣을지는 알수가 없다.
	P_JOB_ID IN JOBS.JOB_ID%TYPE, --JOB_ID의 타입을 그대로 가져가겠다
	P_JOB_TITLE IN JOBS.JOB_TITLE%TYPE,
	P_MIN_SALARY IN JOBS.MIN_SALARY%TYPE,
	P_MAX_SALARY IN JOBS.MAX_SALARY%TYPE
)
IS
	CNT NUMBER := 0;
BEGIN
	SELECT COUNT(JOB_ID) INTO CNT CNT JOBS로부터 CNT를 셋다면 변수에 저장을 해줘
	FROM JOBS WHERE JOB_ID = P_JOB_ID;
	IF CNT = 0 THEN 
		INSERT INTO JOBS(JOB_ID,JOB_TITLE,MIN_SALARY, MAX_SALARY) 
		VALUES(P_JOB_ID,P_JOB_TITLE,P_MIN_SALARY,P_MAX_SALARY);
		DBMS_OUTPUT.ENABLE;
		DBMS_OUTPUT.PUT_LINE('INSERT ALL DONE ABOUT '||' '||P_JOB_ID);
--P_JOB_ID와 JOB_ID 가 일치 하는 곳에서 CNT가 값이 올라갈 것이고 0개 일때는 일치하는게 없기 때문에 추가를 해주면 되죠?
	ELSE
		UPDATE JOBS --사용자가 전달한 PK값이 중복이 있기 때문에 오게 되는 것
			그렇기 때문에 이미 있는 값을 추가하는게 아니고 수정해주겠다
		SET
		JOB_TITLE = P_JOB_TITLE,
		MIN_SALARY = P_MIN_SALARY,
		MAX_SALARY = P_MAX_SALARY
		WHERE JOB_ID = P_JOB_ID;
		DBMS_OUTPUT.ENABLE;
		DBMS_OUTPUT.PUT_LINE('UPDATE ALL DONE ABOUT '||' '||P_JOB_ID);
	END IF;
END;
SELECT * FROM JOBS;

CALL MY_NEW_JOB_PROC('IT','Developer',5000,20000);

```
### 제거를 하는 프로시저 만들기
- JOB_ID 데이터를 하나 전달해서 DELETE문이 작동하는 프로시저 만들어보기

```SQL
CREATE OR REPLACE PROCEDURE DEL_JOB_PROC
(
	P_JOB_ID IN JOBS.JOB_ID%TYPE 보통 DELETE를 하면 하나의 행을 삭제하는데 중복되는 값이 있으면 안되기 때문에 PK 값을 매개변수로 받아서 삭제해보자.
)
IS
	CNT NUMBER := 0;
BEGIN
	SELECT COUNT(JOB_ID) INTO CNT
	FROM JOBS WHERE JOB_ID = P_JOB_ID; 값이 있는지 없는지 검사를 해야하기 때문에 CNT에 넣어주자.
	IF CNT !=0 THEN 0이 아니라는 것은 삭제할 JOB_ID가 존재하고 있다. 삭제해주자.
		DELETE FROM JOBS
		WHERE JOB_ID = P_JOB_ID;
		DBMS_OUTPUT.ENABLE;
		DBMS_OUTPUT.PUT_LINE('DELETE ALL DONE ABOUT '||' '||P_JOB_ID);
	ELSE
		DBMS_OUTPUT.ENABLE;
		DBMS_OUTPUT.PUT_LINE('NO EXIST '||' '||P_JOB_ID);
	END IF;
END;

```

## SEQUENCE
- 테이블에 값을 추가할 때 자동으로 순차적인 정수값이 들어가도록 설정해주는 객체

### 시퀀스 생성하기
```
시퀀스 생성하기(create sequence 시퀀스명;)
CREATE SEQUENCE MEMO_SEQ;
Start with 1 --1부터 카운팅
INCREMENT BY 1 --1씩 증가
CACHE 20; -- 미리 20개의 INDEX공간을 확보 20명이 동시에 접속해서 글을 써도 버벅거리지 않게 해준다.
NOCACHE; -- 1개의 INDEX공간만 확보
```
### 메모테이블 만들어보기
```
create table memo(
	idx NUMBER(3) primary key,
	title VARCHAR2(50) not null,
	content VARCHAR2(4000),
	pwd VARCHAR2(20) not null,
	writer VARCHAR2(100) not null,
	IP VARCHAR2(20),
	write_date DATE
	del_info NUMBER() ----  0, -1, 1
);
```
### MEMO_SEQ를 사용하여 MEMO테이블에 값을 추가
```
insert into MEMO values(memo_seq.nextval, '제목1', '내용1', '1111', '홍길동','192.1.1',sysdate );

insert into MEMO values(memo_seq.nextval, '제목2', '내용2', '1111', '홍길동2','192.1.1',sysdate );
```

