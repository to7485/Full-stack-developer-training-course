# DCL(Data Controll Language)
- 데이터 제어어
- 데이터베이스에 접근하고 객체들을 사용하도록 권한을 주고 회수하는 명령어

## DCL의 종류
- GRANT : 권한 부여
- REVOKE : 권한 강탈


## CMD로 오라클에 접속하여 존재하는 계정 검색

```SQL
SQLPLUS SYSTEM/1234

SELECT USERNAME FROM DBA_USERS;

USERNAME
------------------------------------------------------------
SYS
SYSTEM
ANONYMOUS
TEST_PM
APEX_PUBLIC_USER
FLOWS_FILES
APEX_040000
OUTLN
DIP
ORACLE_OCM
XS$NULL

USERNAME
------------------------------------------------------------
MDSYS
CTXSYS
DBSNMP
XDB
APPQOSSYS
HR
sj
```

## SCOTT계정 등록하기
```SQL
오라클 설치된 폴더에서 SCOTT 검색
SQL> @C:\oraclexe\app\oracle\product\11.2.0\server\rdbms\admin\scott.sql
SQL> SHOW USER;
USER is "SCOTT"

scott의 비밀번호는 TIGER로 되어 있기 때문에 소문자로 변경

SQL> alter user scott identified by tiger;

User altered.

SQL> conn scott/tiger;
Connected.
```


## SCOTT을 통해 BABY라는 아이디를 만드려 했지만 권한이 없어 실패
```sql
SQL> create user baby identified by baby;
create user baby identified by baby
                               *
ERROR at line 1:
ORA-01031: insufficient privileges
```
- BABY라는 계정을 만들 때 BABY가 사용할 저장소를 만들어야 되는데 이 저장소를 테이블 스페이스라고 한다.
``` sql
SQL> conn sys as sysdba
Enter password:
Connected.
SQL> show user
USER is "SYS"
SQL> select tablespace_name, status, contents from dba_tablespaces;

TABLESPACE_NAME                                              STATUS
------------------------------------------------------------ ------------------
CONTENTS
------------------
SYSTEM                                                       ONLINE
PERMANENT

SYSAUX                                                       ONLINE
PERMANENT

UNDOTBS1                                                     ONLINE
UNDO


TABLESPACE_NAME                                              STATUS
------------------------------------------------------------ ------------------
CONTENTS
------------------
TEMP                                                         ONLINE
TEMPORARY

USERS                                                        ONLINE
PERMANENT
------------------------------------------------------------------------------------
```
```sql
SQL> select file_name, tablespace_name,autoextensible from dba_data_files;
							ㄴ용량이 다 차면 자동으로 증가하는지
FILE_NAME
--------------------------------------------------------------------------------
TABLESPACE_NAME                                              AUTOEX
------------------------------------------------------------ ------
C:\ORACLEXE\APP\ORACLE\ORADATA\XE\USERS.DBF
USERS                                                        YES

C:\ORACLEXE\APP\ORACLE\ORADATA\XE\SYSAUX.DBF
SYSAUX                                                       YES

C:\ORACLEXE\APP\ORACLE\ORADATA\XE\UNDOTBS1.DBF
UNDOTBS1                                                     YES


FILE_NAME
--------------------------------------------------------------------------------
TABLESPACE_NAME                                              AUTOEX
------------------------------------------------------------ ------
C:\ORACLEXE\APP\ORACLE\ORADATA\XE\SYSTEM.DBF
SYSTEM
```

## 테이블 스페이스
- 오라클은 데이터를 관리하는 시스템이다.
- 따라서 데이터를 어딘가에 저장해 놓고 사용해야 하는데, 데이터 저장 단위 중 가장 상위의 개념이 테이블스페이스이다.
- 테이블들을 담을 커다란 공간이 테이블스페이스이다.

### 테이블 스페이스의 생성
- BABY라는 이름으로 200MB의 크기로 생성할 것이다.
- 논리적 개념인 테이블스페이스도 물리적으로는 파일로 존재하므로 실제 저장될 파일의 이름과 위치가 필요하다.
- 오라클이 설치된 'C:\oraclexe\app\oracle\oradata\XE' 폴더에 BABY.dbf라는 이름으로 생성을 할 것이다.
- 데이터가 늘어나 테이블스페이스가 꽉 찰 것을 대비해 '5MB'씩 자동으로 증가 옵션도 추가할 것이다.

```sql
CREATE TABLESPACE 테이블스페이스명 DATAFILE '경로와 이름' SIZE 크기 AUTOEXTEND 크기 (MAXSIZE 크기);

- 최대크기는 생략 가능하다.
```
### BABY라는 이름의 테이블스페이스 생성하기
```sql
SQL> CREATE TABLESPACE BABY DATAFILE'C:\oraclexe\app\oracle\oradata\XE\BABY.DBF'SIZE 200M AUTOEXTEND ON NEXT 5M MAXSIZE 300M;

Tablespace created.
```
### SCOTT에게 계정 생성권한주기
- scott 계정에게 계정 생성권한을 주고 BABY계정을 만든다.
```sql
SQL> grant create user to scott; -> 스콧에게 계정을 만들 권한을 줌

Grant succeeded.

SQL> conn scott/tiger
Connected.
SQL> create user baby identified by baby;

User created.
```
### 생성한 BABY권한으로 로그인을 시도한다.
```sql
SQL> conn baby/baby
ERROR: create session이라는 권한이 없어서 로그인이 안된다.
ORA-01045: user BABY lacks CREATE SESSION privilege; logon denied


Warning: You are no longer connected to ORACLE.
SQL> conn system/1111 -> system 계정으로 로그인하여 권한을 줘야 한다.
Connected.
SQL> grant create session to baby;

Grant succeeded.

SQL> conn baby/baby
Connected.
```

### BABY계정과 테이블 스페이스 연결하기
- 방금 만든 테이블스페이스와 baby 계정을 연결해야 한다. 안그러면 default 값인 user로 간다.
```sql
SQL> conn baby/baby
Connected.
SQL> alter user baby default tablespace BABY; 
권한이 없으니 system으로 다시 로그인 하자.

SQL> conn system/1111
Connected.

디폴트 스페이스를 베이비로 바꿀거임
SQL> alter user baby default tablespace BABY; 
User altered.

임시저장소는 temp로 해놓겠다.
SQL> alter user baby temporary tablespace TEMP; 

User altered.

저 baby라는 계정이 baby테이블스페이스의 어느정도 양을 쓸꺼냐 무한으로 쓸거임
SQL> alter user baby default tablespace BABY QUOTA unlimited on baby;

User altered.

SQL> conn baby/baby
Connected.
```

## BABY 계정으로 테이블 만들어보기
```SQL
SQL> create table test001(id varchar2(10), pw varchar2(10), age number, constraints baby_pk primary key(id));
create table test001(id varchar2(10), pw varchar2(10), age number, constraints baby_pk primary key(id))
*
ERROR at line 1:
ORA-01031: insufficient privileges --> 테이블 생성 권한이 없음

SQL> conn system/1111  
Connected.
SQL> grant create table to baby; -> 권한 줌

SQL> create table test001(id varchar2(10), pw varchar2(10), age number, constraints baby_pk primary key(id));

Table created. --> 테이블 생성 DBvear로 확인하기

SQL> select * from test001;

no rows selected

new connection -> oracle -> localhost, xe, baby,baby -> driver Setting
ok -> test
```

# INDEX
- SELECT문을 통해 데이터를 조회하려는 테이블이 너무 거대한 경우, 정렬되지 않은 모든 데이터를 순차적으로 검색하면 조회 결과를 구하기까지 오랜 시간이 걸린다.
- 오라클 데이터베이스에서 테이블내의 원하는 레코드를 빠르게 찾아갈 수 있도록 만들어진 데이터 구조이다.
- 원하는 책을 찾은 것과 비슷하다.
- 책이 정리가 안되어있으면 찾는데 시간이 오래 걸릴 것이다.
- 도서관처럼 색인을 통해 정리해두는 것이 인덱스이다.

## INDEX의 생성
- 인덱스는 테이블 내의 1개의 컬럼, 혹은 여러 개의 컬럼을 이용하여 생성될 수 있다.
- 많은 데이터가 있다면 인덱스를 만들어놓는것이 효과적이다.
- 데이터가 적으면 정리하고 찾는거보다, 그냥 찾는것이 더 빠르다.
- 규모가 큰 테이블, 여러 번 생성, 수정, 삭제가 발생하지 않는 테이블에 적합하다.

### 자동 인덱스
- PRIMARY KEY 또는 UNIQUE에 의해 자동으로 생성되는 INDEX
- 가장 기본적인 B-Tree INDEX로 인덱스

#### B-Tree
- 제목의 순서에 따라 책들을 정리해놓고 해당되는 위치를 찾아가는 것이다.
```
ㄱ - 가.게.기.고.구...
ㄴ - 나.네.니.노.누...
ㄷ - 다.데.디.도.두...
```

### 수동 인덱스
- 사용자가 직접 생성한 INDEX를 의미한다.
```SQL
CREATE INDEX 인덱스명 ON 테이블명(컬럼1,컬럼2,컬럼3.....);
```

## INDEX 조회
- 인덱스는 USER_INDEXES 시스템 뷰에서 조회할 수 있음
```SQL
SELECT * FROM ALL_INDEXS WHERE TABLE_NAME = '테이블 명':
```

## INDEX 삭제
- 조회 성능을 높이기 위해 만든 객체지만 저장공간을 많이 차지하며 DDL작업(INSERT, DELETE, UPDATE) 시 부하가 많이 발생해 전체적인 데이터베이스 성능을 저하시킨다.
- DBA는 주기적으로 INDEX를 검토하여 사용하지 않는 인덱스는 삭제하는 것이 데이터베이스 전체 성능을 향상 시킬 수 있다.
```SQL
DROP INDEX 인덱스명;
```

## INDEX REBUILD
- 생성된 인덱스는 기본적으로 ROOT, BRANCH, LEAF로 구성된 트리 구조를 가지며 DDL 작업이 오랜시간 발생하면 트리의 하위 레벨이 많아져 트리 구조의 한쪽이 무거워지는 현상이 생긴다.
- 이러한 현상은 인덱스의 검색속도를 저하시키고 전체 데이터베이스의 성능에 영향을 미친다. 그러므로 주기적으로 INDEX를 리빌딩하는 작업을 해줘야 한다.

```SQL
ALTER INDEX 인덱스명 REBUILD;
```