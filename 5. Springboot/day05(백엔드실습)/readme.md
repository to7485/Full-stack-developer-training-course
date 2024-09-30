# 사용자 관리 시스템
- 사용자의 정보를 관리하는 기능을 갖는 API 만들기

## 프로젝트 생성하기
- start.spring.io에서 프로젝트 생성하기
- group : com.korea
- artifact : user
### 필요 라이브러리
- Spring Web
- h2
- lombok
- Spring Data JPA

## com.korea.user.model 패키지 생성하기
### UserEntity클래스 만들기
- 유저는 id,name,email 필드를 갖는다.
```java
package com.korea.user.model;

import jakarta.persistence.Entity;
import jakarta.persistence.GeneratedValue;
import jakarta.persistence.GenerationType;
import jakarta.persistence.Id;
import jakarta.persistence.Table;
import lombok.AllArgsConstructor;
import lombok.Builder;
import lombok.Data;
import lombok.NoArgsConstructor;

@Entity
@Table(name = "users")
@Data
@Builder
@NoArgsConstructor
@AllArgsConstructor
public class UserEntity {

    @Id
    //JPA에서 기본 키(id)를 자동으로 생성하는 방법을 정의하는 어노테이션이다.
    //H2와 같은 내장 데이터베이스를 사용하는 경우, 기본적으로 숫자 값이 증가하는 방식으로 ID가 설정된다.
    //예를 들어, 첫 번째 레코드의 ID는 1, 두 번째 레코드는 2, 세 번째 레코드는 3 등으로 순차적으로 증가하는 정수 값이 ID에 들어간다.
    @GeneratedValue(strategy = GenerationType.AUTO)
    private Long id;

    private String name;
    
    private String email;
}
```

## com.korea.user.dto패키지 생성하기
### UserDTO클래스 생성하기
- UserDTO는 id,name,email필드를 갖는다.
- DTO에서 Entity, Entity에서 DTO로 변환할 수 있는 기능이 있다.

```java
package com.korea.user.dto;

import com.example.demo.model.UserEntity;
import lombok.AllArgsConstructor;
import lombok.Builder;
import lombok.Data;
import lombok.NoArgsConstructor;

@Data
@Builder
@NoArgsConstructor
@AllArgsConstructor
public class UserDTO {

    private Long id;
    private String name;
    private String email;

    // Entity -> DTO 변환
    public UserDTO(UserEntity entity) {
        this.id = entity.getId();
        this.name = entity.getName();
        this.email = entity.getEmail();
    }

    // DTO -> Entity 변환
    public static UserEntity toEntity(UserDTO dto) {
        return UserEntity.builder()
                .id(dto.getId())
                .name(dto.getName())
                .email(dto.getEmail())
                .build();
    }
}
```

## com.korea.user.repository패키지 생성하기
### UserRepository클래스 생성하기
- JpaRepository를 상속받는다
- 이메일을 통해 유저를 찾는 findByEamil추상메서드를 추가한다.
```java
package com.korea.user.repository;

import org.springframework.data.jpa.repository.JpaRepository;
import org.springframework.stereotype.Repository;

import com.korea.user.model.UserEntity;

@Repository
public interface UserRepository extends JpaRepository<UserEntity, Long> {
    // 추가적으로 사용자 검색 기능이 필요하면 메서드를 정의할 수 있습니다.
    UserEntity findByEmail(String email);
}
```

# 사용자 생성하기
- 사용자를 생성하는 API 만들기

## com.korea.user.service패키지 생성하기
### UserService클래스 생성하기
- 사용자를 생성하는 create메서드 생성하기
- 생성하고 추가가 잘 됐는지 조회까지 한다.
```java
package com.korea.user.service;

@Service
@RequiredArgsConstructor
public class UserService {

    private final UserRepository repository;

	// 사용자 생성
	public List<UserDTO> create(UserEntity entity) {
		repository.save(entity); // 데이터베이스에 저장

		// 모든 사용자 반환 (저장된 사용자 포함)
		return repository.findAll().stream().map(UserDTO::new).collect(Collectors.toList());
	}
}
```

## com.korea.user.controller
### UserController클래스 생성하기
- HTTP 메서드 : POST
- 메서드명 : createUser
```java
package com.korea.user.controller;

@RestController
@RequestMapping("/users")
@RequiredArgsConstructor
public class UserController {

    private final UserService userService;

    // 사용자 생성
	// 사용자 생성
	@PostMapping
	public ResponseEntity<List<UserDTO>> createUser(@RequestBody UserDTO dto) {
		UserEntity entity = UserDTO.toEntity(dto);
		List<UserDTO> users = userService.create(entity);
		return ResponseEntity.ok(users);
	}
}
```

# 모든 사용자 조회
- 모든 사용자를 조회할 수 있는 API 만들기
### UserService클래스에 코드 추가하기
- getAllUsers()메서드 생성하기
```java
// 모든 사용자 조회
public List<UserDTO> getAllUsers() {
    // 모든 사용자 엔티티를 가져와서 DTO로 변환 후 반환
    return repository.findAll().stream()
            .map(UserDTO::new)  // UserEntity -> UserDTO로 변환
            .collect(Collectors.toList());
}
```
### UserController클래스에 코드 추가하기
- HTTP 메서드 : GET
- 메서드명 : getAllUsers
```java
// 모든 사용자 조회
@GetMapping
public ResponseEntity<List<UserDTO>> getAllUsers() {
    List<UserDTO> users = userService.getAllUsers();
    return ResponseEntity.ok(users);
}
```

# 이메일을 통해 사용자 검색하기
### UserService클래스에 코드 추가하기
- getUserByEmail()메서드 생성하기
```java
// 이메일로 사용자 검색
public UserDTO getUserByEmail(String email) {
    UserEntity entity = repository.findByEmail(email);
    return new UserDTO(entity);
}
```

### UserController클래스에 코드 추가하기
- HTTP메서드 : GET
- 메서드명 : getUserByEmail
- 리소스 : /{eamil}
```java
// 이메일로 사용자 검색
@GetMapping("/{email}")
public ResponseEntity<UserDTO> getUserByEmail(@PathVariable String email) {
    UserDTO user = userService.getUserByEmail(email);
    return ResponseEntity.ok(user);
}
```

# ID를 통해 이름과 이메일 수정하기
### UserService클래스에 코드 추가하기
- getUserByEmail()메서드 생성하기
```java
// 사용자 정보 업데이트 (ID 기반)
public List<UserDTO> updateUser(UserEntity entity) {
    // Optional로 ID를 통해 사용자 찾기
    Optional<UserEntity> userEntityOptional = repository.findById(entity.getId());

    // 사용자가 존재할 경우 업데이트 로직 실행
    userEntityOptional.ifPresent(userEntity -> {
        // 이름과 이메일을 업데이트
        userEntity.setName(entity.getName());
        userEntity.setEmail(entity.getEmail());

        // 업데이트된 사용자 정보 저장
        repository.save(userEntity);
    });

    return getAllUsers();
}
```

### UserController클래스에 코드 추가하기
- HTTP메서드 : PUT
- 메서드명 : updateUser
```java
// 사용자 정보 수정 (ID 기반)
@PutMapping
public ResponseEntity<?> updateUser(@RequestBody UserDTO dto) {
    UserEntity entity = UserDTO.toEntity(dto);
    List<UserDTO> updatedUser = userService.updateUser(entity);

    return ResponseEntity.ok(updatedUser);
    }
```

# 삭제하기
- ID를 가지고 유저를 삭제하는 API 만들기
### UserService클래스에 코드 추가하기
- 메서드명 deleteUser
- 삭제 성공시 true, 실패시 false를 반환합니다.
```java
// 사용자 삭제
public boolean deleteUser(Long id) {
    // 먼저 사용자가 존재하는지 확인
    Optional<UserEntity> userEntityOptional = repository.findById(id);

    if (userEntityOptional.isPresent()) {
        // 존재하면 삭제 수행
        repository.deleteById(id);
        return true;  // 삭제 성공
    } else {
        return false; // 삭제 실패 (사용자가 없음)
    }
}
```

### UserController클래스에 코드추가하기
- HTTP메서드 : DELETE
- 메서드명 : deleteUser
- 리소스 : /{id}
```java
// 사용자 삭제 (ID 기반)
@DeleteMapping("/{id}")
public ResponseEntity<?> deleteUser(@PathVariable Long id) {
    boolean isDeleted = userService.deleteUser(id);
    if (isDeleted) {
        return ResponseEntity.ok("User deleted successfully");
    } else {
        return ResponseEntity.status(404).body("User not found with id " + id);
    }
}
```