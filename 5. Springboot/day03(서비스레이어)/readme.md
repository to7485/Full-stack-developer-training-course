# 서비스 레이어
 - 서비스레이어는 컨트롤러와 퍼시스턴스 사이에서 비즈니스 로직을 수행하는 역할을 한다.
 - HTTP와 긴밀히 연결된 컨느롤러에서 분리돼 있고, 또 데이터베이스와 긴밀히 연관된 퍼시스턴스와도 분리되어 있다.
 - 따라서 서비스 레이어에서는 우리가 개발하고자 하는 로직에 집중할 수 있다.

## com.example.demo.service 패키지 생성하기
- TodoService클래스 만들기

## @Service
- 스프링 프레임워크에서 제공하는 애노테이션 중 하나로, **서비스 레이어(Service Layer)**에 사용되는 클래스를 명시할 때 사용된다.
- 이 애노테이션을 사용하면 스프링이 해당 클래스를 **스프링 컨테이너에서 관리하는 빈(bean)**으로 등록하고, 비즈니스 로직을 처리하는 역할을 맡는다.

### 주요기능과 역할
1. 비즈니스 로직을 담당하는 클래스 표시
   - @Service는 주로 비즈니스 로직을 처리하는 클래스에 붙인다. 
   - 이 클래스는 데이터 액세스, 계산, 트랜잭션 처리 등의 주요 작업을 수행한다.
   - 서비스 레이어는 **컨트롤러(프레젠테이션 레이어)**와 퍼시스턴스(영속 레이어) 간의 중간 계층으로, 복잡한 비즈니스 규칙을 처리하는 데 사용된다.

2. 스프링 빈으로 등록
    - @Service 애노테이션이 붙은 클래스는 **스프링 빈(Bean)**으로 등록되어 **DI(Dependency Injection, 의존성 주입)**를 통해 다른 클래스에서 주입(injection)될 수 있다.
    - 즉, 스프링은 애플리케이션이 실행될 때 이 클래스의 객체를 생성하고 관리하며, 다른 컴포넌트에서 필요할 때 자동으로 주입해준다.

3. 계층 구조의 명확성
   - @Service는 계층화된 아키텍처에서 서비스 레이어의 역할을 명확하게 구분하는 데 도움을 준다. 
   - 이를 통해 각 레이어의 책임을 분리하고, 코드의 가독성과 유지보수성을 향상시킨다.
   - 스프링은 @Service, @Repository, @Controller 등을 통해 각 클래스가 어떤 역할을 하는지 직관적으로 알 수 있게 해준다.

```java
package com.example.demo.service;

import org.springframework.stereotype.Service;

@Service
public class TodoService {

	public String testService() {
		return "Test Service";
	}
}
```
- 서비스를 만들었으니, 이 서비스를 사용하기 위해 TodoController에 추가해주자.

## TodoContoller클래스에 코드 추가하기
```java
package com.example.demo.controller;

import java.util.ArrayList;
import java.util.List;

import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.http.ResponseEntity;
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.RestController;

import com.example.demo.dto.ResponseDTO;
import com.example.demo.service.TodoService;

@RestController
@RequestMapping("todo")
public class TodoController {

	@Autowired
	private TodoService service;
	
	@GetMapping("/test")
	public ResponseEntity<?> testTodo(){
		String str = service.testService();//테스트 서비스 사용
		List<String> list = new ArrayList<>();
		list.add(str);
		ResponseDTO<String>response = ResponseDTO.<String>builder().data(list).build();
		return ResponseEntity.ok().body(response);
		
	}
}
```
- 애플리케이션을 재시작하고 포스트맨을 이용해 GET localhost:9090/todo/test 요청을 보내보자
- "Test Service"를 담은 ResponseDTO가 반환되는 모습을 볼 수 있다.

![img](img/서비스테스트.png)

## 퍼시스턴스 레이어 : 스프링 데이터 JPA
- 우리 애플리케이션은 Todo 아이템을 DB에 저장해야 한다.
### 관계형 데이터베이스를 자바와 연결하려면 어떻게 해야하는가?
1. DBMS를 설치해야 한다. 
   - MYSQL이라면 Workbench같은 MySQL 클라이언트를 설치한다.
   - 클라이언트는 데이터베이스에 연결하는 작업을 도와준다.
   - 클라이언트를 이용해 데이터베이스에 연결되면 쿼리를 작성한다.
```sql
create table if not exists Todo(
    id varchar2(100) NOT NULL PRIMARY KEY,
    userId varchar2(100) NOT NULL,
    title varchar2(100) NOT NULL,
    done boolean DEFAULT false
)
```
2. 테이블을 생성하고 아이템을 몇 개 넣었다고 가정하자.
    - 우리는 이후 아이템을 검색하기 위해 SELECT쿼리를 날린다.
```SQL
SELECT id, title, done
FROM Todo
WHERE id="ff80808177"
```
3. 쿼리를 날리면 조건에 맞는 결과가 반환된다
4. 우리는 이렇게 반환된 결과를 자바 애플리케이션 내에서 사용해야 한다.
5. 이뿐만 아니라 테이블을 생성하는 것도, 테이블에 엔트리를 추가하는것도, 수정, 삭제하는것도 다 웹 서비스의 일부로 동작해야 한다.
6. JDBC드라이버를 통해 자바와 연결을 한다.

```JAVA
String sqlSelectAllTodos="SELECT * FROM Todo where USER_ID= "+request.getUserId();
String connectionUrl="jdbc:mysql://mydb:3306/todo";
try{
    //1.데이터베이스에 연결
    Connection conn = DriverManager.getConnection(connectionUrl, "username","password");
    //2. SQL쿼리 준비
    PreparedStatement ps = conn.preparedStatement(sqlSelectAllTodos);
    //3. 쿼리 실행
    ResultSet rs = ps.executeQuery();

    //결과를 객체로 파싱
    while(rs.next()){
        long id = rs.getString("id");
        String title = rs.getString("title");
        Boolean isDone = rs.getBoolean("done");

        todos.add(new Todo(id,title,isDone));
    } catch(SQLException e){
        //handle the exception
    }
}
```
- Connection을 이용해 데이터베이스에 연결하고 쿼리문을 ResultSet클레스에 결과를 담아온다.
- 그리고 While문 내부에서 ResultSet을 Todo객체로 바꾼다.
- 이 일련의 작업을 ORM(Object-Relation-Mapping)이라고 한다.
7. 테이블을 자바 내에서 사용하기 위해 이 작업을 엔티티마다 해야한다. 보통 테이블 하나마다 그에 상응하는 엔티티클래스가 존재한다.
8. 또 이런 작업을 집중적으로 해주는 DAO클래스를 작성해야 한다.
9. 시간이 흐르면서 반복작업을 줄이기 위해 Hibernate와 같은 ORM프레임워크가 나왔고, 더 나아가 JPA같은 도구들이 개발됐다.

## 데이터베이스와 스프링 데이터 JPA 설정
1. 데이터베이스에 연결하기 위해서는 데이터베이스가 필요하다.
2. 우리는 프로젝트를 생성할 때 H2를 추가했었다.

## H2 데이터베이스 관리 시스템
- 자바 기반의 **경량형 관계형 데이터베이스 관리 시스템(RDBMS)**이다.
- 주로 개발 및 테스트 환경에서 사용되며, 메모리 기반 데이터베이스나 디스크 기반 데이터베이스로 구성할 수 있다.
- H2는 오픈 소스로 제공되며, 빠르고 가벼운 성능 때문에 애플리케이션 개발 시 간편하게 데이터베이스를 설정하고 사용할 수 있다.

### 주요 특징
1. 메모리 기반과 디스크 기반 지원
   1. 메모리 기반 데이터베이스: 애플리케이션이 실행되는 동안에만 데이터베이스가 유지되며, 애플리케이션이 종료되면 데이터가 사라진다. 
      1. 개발 및 테스트에 유용하다.
   2. 디스크 기반 데이터베이스: 데이터가 영구적으로 저장되며, 애플리케이션이 종료되어도 데이터를 유지한다.

2. 자바 기반
   1. H2는 자바로 작성된 데이터베이스 엔진으로, 자바 애플리케이션과의 통합이 매우 용이하다. 
   2. JAR 파일로 제공되며, 자바 애플리케이션에서 쉽게 임베드할 수 있다.
3. SQL 표준 지원
   1. H2는 표준 SQL을 지원하므로, 다른 데이터베이스 시스템(MySQL, PostgreSQL 등)에서 사용되는 SQL 문을 대부분 동일하게 사용할 수 있다.

4. 내장형 및 서버 모드
   1. 내장형 모드: H2 데이터베이스를 애플리케이션 내부에 임베드하여 사용할 수 있다. 
        - 이 모드에서는 애플리케이션 내에서만 데이터베이스에 접근 가능하다.
   2. 서버 모드: H2를 독립된 데이터베이스 서버로 설정하여 네트워크를 통해 여러 클라이언트가 접근할 수 있게 할 수 있다.

5. 간편한 설정 및 사용
   1. 설정이 매우 간단하며, 스프링 부트와 같은 프레임워크에서 별도의 설정 없이도 인메모리 데이터베이스로 바로 사용할 수 있다.
   2. 웹 기반의 H2 콘솔(http://localhost:9090/h2-console에 접속하면, SQL 쿼리를 직접 실행하거나 데이터를 조회할 수 있다.)을 제공하여, 브라우저를 통해 데이터베이스에 쉽게 접근하고 SQL 쿼리를 실행할 수 있다.

6. 빠른 성능
   1. H2는 메모리 기반으로 동작할 때 매우 빠른 성능을 제공하며, 디스크 기반에서도 경량화된 구조로 효율적인 성능을 제공한다.

## JPA
- 자바에서 객체와 관계형 데이터베이스 간의 데이터를 매핑(ORM: Object-Relational Mapping)하기 위한 표준 API다.
- JPA는 자바 객체를 데이터베이스의 테이블과 매핑하고, 데이터베이스의 데이터를 자바 객체로 변환하여 쉽게 다룰 수 있게 해준다.
- 이를 통해 개발자는 데이터베이스의 세부 사항에 구애받지 않고 객체 지향적으로 데이터베이스를 처리할 수 있다.

### 주요 개념
1. ORM(Object-Relation Mapping)
    - JPA는 자바 객체와 데이터베이스의 테이블을 매핑한다.
    - 자바 객체를 데이터베이스의 테이블로, 객체의 필드를 테이블의 컬럼으로 매핑함으로써, 객체 지향적인 방식으로 데이터베이스 작업을 수행할 수 있다.
    - 예를 들어, 데이터베이스의 사용자 테이블을 User 객체와 매핑할 수 있으며, 데이터베이스에 쿼리를 작성하지 않고도 자바 코드로 데이터를 처리할 수 있다.
2. Persistence Context
    - JPA에서 엔티티(Entity) 객체를 관리하는 일종의 캐시 역할을 한다.
    - 이 컨텍스트를 통해 엔티티 객체를 추적하고, 변경된 내용을 자동으로 데이터베이스에 반영한다.
    - JPA는 객체를 영속성 컨텍스트에서 관리하고, 이를 통해 트랜잭션 내에서 데이터베이스 작업을 처리한다.
3. Entity
   - JPA에서 관리되는 자바 객체를 **엔티티(Entity)**라고 한다.
   - 엔티티 클래스는 데이터베이스의 테이블과 매핑되며, 객체의 속성은 테이블의 컬럼과 매핑된다.
   - 엔티티 클래스는 @Entity 애노테이션을 통해 정의된다.

## Spring DAta JPA
-  Spring Data 프로젝트의 일부로, **JPA(Java Persistence API)**를 쉽게 사용할 수 있도록 도와주는 Spring 기반의 데이터 액세스 프레임워크다.
- Spring Data JPA는 Repository 패턴을 기반으로 하여, 데이터베이스와 상호작용할 때 개발자가 반복적으로 작성해야 하는 코드들을 자동으로 처리해준다.

```java
※ Repository 패턴 예시

//UserRepository는 사용자 데이터를 처리하는 Repository 인터페이스다.
//여기서 데이터베이스에 직접 접근하는 코드를 작성하지 않고, 데이터를 저장, 조회, 삭제하는 기능만 정의하고 있다.
public interface UserRepository {
    User findById(Long id);
    List<User> findAll();
    User save(User user);
    void deleteById(Long id);
}




//UserRepository 인터페이스를 구현하는 구현 클래스다.
//여기서 데이터를 저장하거나 조회하는 로직을 캡슐화한다.
import java.util.HashMap;
import java.util.List;
import java.util.ArrayList;
import java.util.Map;

public class UserRepositoryImpl implements UserRepository {
    private Map<Long, User> database = new HashMap<>();

    @Override
    public User findById(Long id) {
        return database.get(id);
    }

    @Override
    public List<User> findAll() {
        return new ArrayList<>(database.values());
    }

    @Override
    public User save(User user) {
        database.put(user.getId(), user);
        return user;
    }

    @Override
    public void deleteById(Long id) {
        database.remove(id);
    }
}
```

### 주요특징
1. Repository 기반 데이터 액세스
    - Spring Data JPA는 Repository 인터페이스를 기반으로 데이터베이스에 접근한다. 
    - 이 인터페이스를 확장함으로써 복잡한 데이터 액세스 코드를 작성하지 않고도 CRUD(Create, Read, Update, Delete) 작업을 자동으로 처리할 수 있다.
2. 자동화된 CRUD 작업
    - Spring Data JPA는 기본적인 CRUD 메서드를 자동으로 제공한다. 
    - findAll(), save(), delete()와 같은 메서드를 별도의 구현 없이 바로 사용할 수 있다.
3. 쿼리 메서드(Query Method)
    - JPA 쿼리 메서드를 작성할 때 메서드 이름만으로 SQL 쿼리를 자동 생성할 수 있다. 
    - 메서드 이름을 분석하여 해당 메서드에 맞는 SQL 문을 실행한다.
    - 예를 들어, findByUsername(String username) 메서드는 자동으로 SELECT * FROM User WHERE username = ? 쿼리를 실행한다.

## TodoEntity클래스 수정하기
- 보통 데이터베이스 테이블마다 그에 상응하는 엔티티클래스가 존재한다고 했다.
- 우리 프로젝트에서는  Todo테이블에 상응하는 TodoEntity가 존재한다.
- 하나의 엔티티 객체는 데이터베이스 테이블의 한 행에 해당한다.
- 엔티티 클래스는 클래스 그 자체가 테이블을 정의해야 한다.
- ORM이 어떤 엔티티를 보고 어떤 테이블의 어떤 필드에 매핑해야 하는지 알 수 있어야 한다는 뜻이다.
- 또 어떤 필드가 기본키인지, 외래키인지 구분할 수 있어야 한다.
- 이런 데이터베이스 테이블 스키마에 대한 정보는 javax.persistence가 제공하는 JPA 관련 어노테이션을 사영혼다.

### 주의할 점
1. 클래스에는 매개변수가 없는 생성자가 필요핟.
2. Getter/Setter가 필요하다.
3. 세번째는 기본키를 지정해줘야 한다.


```java
package com.example.demo.model;

//이전 (JPA 2.x 버전까지): javax.persistence.Entity
//현재 (JPA 3.0 버전 이후): jakarta.persistence.Entity
import jakarta.persistence.Entity;
import lombok.AllArgsConstructor;
import lombok.Builder;
import lombok.Data;
import lombok.NoArgsConstructor;

@Builder
@NoArgsConstructor
@AllArgsConstructor
@Data
//자바 클래스를 엔티티로 지정하기 위해 사용한다.
//이름을 부여하고 싶다면 @Entity("TodoEntity") 처럼 매개변수를 넣을 수 있다.
@Entity
//테이블이름을 지정하기 위해 @Table 어노테이션을 사용한다.
//이 엔티티는 데이터베이스의 Todo테이블에 매핑된다는 뜻이다.
//만약 @Table을 추가하지 않거나, 추가해도 name을 명시하지 않는다면 @Entity의 이름을 테이블로 간주한다.
//만약 @Entity에 이름을 지정하지 않는 경우 클래스의 이름을 테이블 이름으로 간주한다.
@Table(name="Todo")
public class TodoEntity {
    @Id//기본키가 될 필드에 지정한다.
    @
	private String id; //이 객체의 id
	private String userId;//이 객체를 생성한 유저의 아이디
	private String title;//Todo 타이틀 예)운동 하기
	private boolean done;//true - todo를 완료한 경우(checked)	
}
```

