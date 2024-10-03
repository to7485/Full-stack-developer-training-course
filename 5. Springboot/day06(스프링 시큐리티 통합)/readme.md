# 스프링 시큐리티 통합
- 사용자에 관련된 클래스들은 로그인 여부를 저장하지 않는다는 점 때문에 불완전하다.
- 스프링 시큐리티와 JWT 토큰을 이용해 해결할 것이다.

## 로그인 유지 구현
- 모든 API 요청에 토큰을 보내는 것이다.
- 그러면 각 API는 맨 처음 토큰을 확인함으로써 접근을 허용 또는 거부하는 코드를 실행할 것이다.
- 문제는 모든 API가 이 작업을 해야 한다는 것이다.
- createTodo, getTodo, updateTodo, deleteTodo 총 네 개의 API가 존재한다.
- 50개가 넘는 API를 관리한다고 생각하면 코드를 50번 반복해야 한다는 뜻이다.
- 우리는 스프링 시큐리티를 이용해 코드를 한번만 작성하고, 이 코드가 모든 API를 수행하기 바로 전에 실행되도록 설정하고 구현할 것이다.

## JWT 생성 및 반환 구현
- 유저 정보를 바탕으로 헤더와 페이로드를 작성하고 전자 서명을 한 후 토큰을 반환할것이다.
- 구현을 위해서 JWT관련 라이브러리를 디펜던시에 추가해야 한다.
- build.gradle의 dependencies 부분에 Jjwt라이브러리를 추가해주자.

```groovy
	// https://mvnrepository.com/artifact/io.jsonwebtoken/jjwt-api
	implementation group: 'io.jsonwebtoken', name: 'jjwt-api', version: '0.11.5'
	// https://mvnrepository.com/artifact/io.jsonwebtoken/jjwt-impl
	runtimeOnly group: 'io.jsonwebtoken', name: 'jjwt-impl', version: '0.11.5'
	// https://mvnrepository.com/artifact/io.jsonwebtoken/jjwt-gson
	implementation group: 'io.jsonwebtoken', name: 'jjwt-gson', version: '0.11.5'
```

### com.example.demo.security패키지 만들기
- security패키지에서 인증과 인가를 위한 모든 클래스를 관리할 것이다.
- TokenProvider클래스를 만들어 유저 정보를 받아 JWT를 생성하자.
```java
package com.example.demo.security;

import java.time.Instant;
import java.time.temporal.ChronoUnit;
import java.util.Date;

import org.springframework.stereotype.Service;

import com.example.demo.model.UserEntity;

import io.jsonwebtoken.Claims;
import io.jsonwebtoken.Jwts;
import io.jsonwebtoken.SignatureAlgorithm;
import lombok.extern.slf4j.Slf4j;

@Slf4j
@Service
public class TokenProvider {
	private static final String SECRET_KEY = "eyJhbGciOiJIUzUxMiJ9eyJSb2xlIjoiQWRtaW4iLCJJc3N1ZXIiOiJJc3N1ZXIiLCJVc2VybmFtZSI6IkphdmFJblVzZSIsImV4cCI6MTcyNzk3NzQ2OSwiaWF0IjoxNzI3OTc3NDY5fQ3WUk1X983GsejnQZJSNQKjZBfBeSzOK4cAxpndz0G3pSItFPDiDVnSfD0ZsQzVCSkSMKQozyMVDjt9VYTcJw";

	public String create(UserEntity userEntity) {
		// 기한 지금으로부터 1일로 설정
		Date expiryDate = Date.from(
						Instant.now()
						.plus(1, ChronoUnit.DAYS));

		/*
		{ // header
		  "alg":"HS512"
		}.
		{ // payload
		  "sub":"40288093784915d201784916a40c0001",
		  "iss": "demo app",
		  "iat":1595733657,
		  "exp":1596597657
		}.
		// SECRET_KEY를 이용해 서명한 부분
		Nn4d1MOVLZg79sfFACTIpCPKqWmpZMZQsbNrXdJJNWkRv50_l7bPLQPwhMobT4vBOG6Q3JYjhDrKFlBSaUxZOg
		 */
		// JWT Token 생성
		return Jwts.builder()
						// header에 들어갈 내용 및 서명을 하기 위한 SECRET_KEY
						.signWith(SignatureAlgorithm.HS512, SECRET_KEY)
						// payload에 들어갈 내용
						.setSubject(userEntity.getId()) // sub
						.setIssuer("demo app") // iss
						.setIssuedAt(new Date()) // iat
						.setExpiration(expiryDate) // exp
						.compact();
	}

	public String validateAndGetUserId(String token) {
		// parseClaimsJws메서드가 Base 64로 디코딩 및 파싱.
		// 즉, 헤더와 페이로드를 setSigningKey로 넘어온 시크릿을 이용 해 서명 후, token의 서명 과 비교.
		// 위조되지 않았다면 페이로드(Claims) 리턴
		// 그 중 우리는 userId가 필요하므로 getBody를 부른다.
		Claims claims = Jwts.parser()
						.setSigningKey(SECRET_KEY)
						.parseClaimsJws(token)
						.getBody();

		return claims.getSubject();
	}
}
```
- create()는 JWT라이브러리를 이용해 JWT토큰을 생성한다.
- 토큰을 생성하는 과정에서 우리가 임의로 지정한 SECRET_KEY를 개인키로 사용한다.
- 두 번째 메서드 validateAndGetUserId()는 토큰을 디코딩, 파싱 및 위조여부를 확인한다.
- 이후 우리가 원하는 유저의 아이디를 반환한다.
- 라이브러리 덕에 우리가 굳이 JSON을 생성, 서명, 인코딩, 디코딩, 파싱하는 작업을 하지 않아도 된다.
- TokenProvider를 작성했다면, 이제 로그인 부분에서 TokenProvider를 이용해 토큰을 생성 후 UserDTO에 이를 반환해야 한다.

## UserController에 코드 수정하기
```java
package com.example.demo.controller;

@Slf4j
@RestController
@RequestMapping("/auth")
public class UserController {

	@Autowired
	private UserService userService;

///////////////////Token Provider 주입////////////////
	@Autowired
	private TokenProvider tokenProvider;
///////////////////Token Provider 주입////////////////


	@PostMapping("/signup")
	public ResponseEntity<?> registerUser(@RequestBody UserDTO userDTO) {
		try {
			// 리퀘스트를 이용해 저장할 유저 만들기
			UserEntity user = UserEntity.builder()
							.email(userDTO.getEmail())
							.username(userDTO.getUsername())
							.password(passwordEncoder.encode(userDTO.getPassword()))
							.build();
			// 서비스를 이용해 리파지토리에 유저 저장
			UserEntity registeredUser = userService.create(user);
			UserDTO responseUserDTO = UserDTO.builder()
							.email(registeredUser.getEmail())
							.id(registeredUser.getId())
							.username(registeredUser.getUsername())
							.build();
			// 유저 정보는 항상 하나이므로 그냥 리스트로 만들어야하는 ResponseDTO를 사용하지 않고 그냥 UserDTO 리턴.
			return ResponseEntity.ok(responseUserDTO);
		} catch (Exception e) {
			// 예외가 나는 경우 bad 리스폰스 리턴.
			ResponseDTO responseDTO = ResponseDTO.builder().error(e.getMessage()).build();
			return ResponseEntity
							.badRequest()
							.body(responseDTO);
		}
	}

	@PostMapping("/signin")
	public ResponseEntity<?> authenticate(@RequestBody UserDTO userDTO) {
		UserEntity user = userService.getByCredentials(
						userDTO.getUsername(),
						userDTO.getPassword());

		if(user != null) {
			///////////////////토큰 생성////////////////
			final String token = tokenProvider.create(user);
         ///////////////////토큰 생성////////////////
			final UserDTO responseUserDTO = UserDTO.builder()
							.username(user.getUsername())
							.id(user.getId())
                     //////토큰 주입///////
							.token(token)
                     //////토큰 주입///////
							.build();
			return ResponseEntity.ok().body(responseUserDTO);
		} else {
			ResponseDTO responseDTO = ResponseDTO.builder()
							.error("Login failed.")
							.build();
			return ResponseEntity
							.badRequest()
							.body(responseDTO);
		}
	}
}
```
- 포스트맨을 켜고 회원가입을 한후 로그인을 해서 token필드가 반환되는지 확인해보자.

# 스프링 시큐리티(Spring Security)

스프링 시큐리티는 스프링 기반 애플리케이션에서 **인증**(Authentication)과 **인가**(Authorization)를 처리하기 위한 강력한 보안 프레임워크다. 스프링 애플리케이션에서 보안과 관련된 다양한 요구 사항을 손쉽게 구현할 수 있도록 돕는다.

## 주요 개념

1. **인증(Authentication)**
   - 사용자가 누구인지 확인하는 과정.
   - 사용자가 애플리케이션에 접근할 때 제공한 자격 증명(예: 사용자명, 비밀번호)을 확인하여 신원을 검증하는 단계.
   
2. **인가(Authorization)**
   - 인증된 사용자가 어떤 리소스에 접근할 수 있는지 결정하는 과정.
   - 사용자에게 주어진 역할(Role)과 권한(Authority)에 따라 리소스에 대한 접근 권한을 부여한다.

3. **필터 기반 아키텍처**
   - 스프링 시큐리티는 필터 체인을 기반으로 동작한다. HTTP 요청이 들어오면 여러 보안 필터들이 순차적으로 실행되어 요청을 처리하고, 보안 관련 로직을 적용한다.

### 필터
- HTTP 요청과 응답을 가로채어, 요청이 컨트롤러에 도달하기 전 또는 응답이 클라이언트에 전달되기 전에 필요한 전처리 또는 후처리를 수행하는 데 사용된다. 
- 주로 보안, 로깅, 인증, 인코딩 설정, 데이터 압축 등의 작업을 처리하는 데 유용하다.


   
4. **SecurityContext**
   - 사용자의 인증 정보를 저장하는 객체.
   - 인증된 사용자의 세션에 `SecurityContext`가 저장되며, 이 컨텍스트를 통해 현재 사용자에 대한 정보를 언제든지 참조할 수 있다.

## 동작 원리

스프링 시큐리티는 주로 다음과 같은 단계로 동작한다:

### 1. **필터 체인(Filter Chain)**
스프링 시큐리티의 핵심은 **필터 체인**(Filter Chain)이다. 필터 체인은 들어오는 HTTP 요청에 대해 여러 필터들이 순차적으로 작동하며, 각각의 필터가 특정 보안 관련 작업을 수행한다.<br>

   - 스프링 시큐리티는 여러 보안 필터로 구성된 필터 체인을 사용하여 HTTP 요청을 처리한다.
   - 가장 중요한 필터 중 하나는 `UsernamePasswordAuthenticationFilter`로, 로그인 요청을 처리하고 사용자 인증을 담당한다.
   - 필터 체인은 순차적으로 요청을 가로채어 인증과 인가 과정을 수행한다.

#### 필터의 종류
 - **`UsernamePasswordAuthenticationFilter`**: 기본적인 로그인 요청을 처리하는 필터로, 사용자가 제출한 자격 증명(아이디/비밀번호)을 검증한다.
 - **`BasicAuthenticationFilter`**: HTTP Basic 인증을 처리하는 필터로, Authorization 헤더에 포함된 자격 증명을 검증한다.
 - **`SecurityContextPersistenceFilter`**: `SecurityContext`를 세션에서 불러오거나 저장하는 역할을 한다. 사용자의 인증 정보를 보존하는 데 사용된다.
 - **`ExceptionTranslationFilter`**: 인증 또는 인가 과정에서 발생한 예외를 처리하는 필터다. 접근이 거부되었을 때 적절한 응답을 반환한다.
 - **`FilterSecurityInterceptor`**: 최종 필터로, 모든 요청에 대한 보안 처리를 완료한 후 접근 권한을 확인한다.

#### **필터 체인의 실행 순서**
- HTTP 요청이 애플리케이션으로 들어오면 스프링 시큐리티의 필터 체인에 의해 첫 번째 필터가 실행된다.
- 각 필터는 요청을 처리한 후 다음 필터로 넘기며, 요청 처리의 흐름이 필터 체인 전체를 거친다.
- 필터 체인의 마지막에 도달하면 최종적으로 컨트롤러가 요청을 처리하게 된다.

### 2. **인증(Authentication)**
   - 사용자가 로그인 요청을 하면, `AuthenticationManager`가 인증을 처리한다.
   - `AuthenticationManager`는 실제로 인증을 수행하는 `AuthenticationProvider`에게 인증을 위임한다.
   - 사용자가 입력한 자격 증명(예: 사용자명, 비밀번호)을 `UserDetailsService`와 같은 서비스에서 가져온 사용자 정보와 비교하여 인증 여부를 결정한다.
   - 인증이 성공하면, `Authentication` 객체가 생성되고, `SecurityContext`에 저장된다. 이 정보는 이후에 사용자의 세션에 저장된다.

### 3. **인가(Authorization)**
   - 사용자가 인증된 후, 스프링 시큐리티는 사용자가 요청한 리소스에 접근할 권한이 있는지 확인한다.
   - 이 과정에서 사용자의 역할(Role)과 권한(Authority)을 기반으로 접근 제어를 수행한다.
   - 특정 URL, 메서드, 리소스에 대한 접근 권한이 없으면 접근이 거부되고, `AccessDeniedException`이 발생한다.

### 4. **SecurityContextHolder**
   - 스프링 시큐리티는 `SecurityContextHolder`를 사용하여 현재 사용자의 보안 정보를 저장하고 관리한다.
   - `SecurityContextHolder`는 `SecurityContext`를 통해 인증된 사용자의 정보를 유지하며, 이 정보는 애플리케이션 어디서나 참조할 수 있다.

### 5. **세션과 토큰 관리**
   - 스프링 시큐리티는 세션 기반 인증뿐만 아니라, JWT 토큰을 활용한 인증 방식도 지원한다.
   - JWT와 같은 토큰 기반 인증을 사용할 경우, 사용자는 로그인 시 발급받은 토큰을 헤더에 포함하여 요청을 보낸다. 스프링 시큐리티는 이 토큰을 검증하여 인증 및 인가를 처리한다.

## 주요 컴포넌트

1. **`AuthenticationManager`**
   - 인증 요청을 처리하는 인터페이스로, `AuthenticationProvider`에게 인증을 위임한다.

2. **`AuthenticationProvider`**
   - 실제 인증 로직을 수행하는 클래스. 예를 들어, 사용자 자격 증명(아이디/비밀번호)을 검증한다.

3. **`UserDetailsService`**
   - 사용자 정보를 불러오는 서비스로, 인증 과정에서 사용자 정보를 조회하는 데 사용된다.

4. **`SecurityContext`**
   - 현재 인증된 사용자의 정보를 저장하는 객체. 세션에 저장되며, 언제든 참조 가능하다.

5. **`GrantedAuthority`**
   - 사용자가 가진 권한을 나타낸다. 사용자의 역할(Role)과 연관되어 접근 권한을 제어하는 데 사용된다.

## 스프링 시큐리티 설정

스프링 시큐리티는 크게 두 가지 방식으로 설정할 수 있다:

1. **XML 설정**: 과거 방식으로, 보안 설정을 XML 파일에 정의한다.
2. **Java Config 설정**: 현재는 주로 Java 기반 설정을 사용한다. `@EnableWebSecurity` 어노테이션을 사용하여 보안 설정을 활성화하고, `WebSecurityConfigurerAdapter`를 상속받아 보안 관련 설정을 커스터마이징한다.

```java
@EnableWebSecurity
public class SecurityConfig extends WebSecurityConfigurerAdapter {
    @Override
    protected void configure(HttpSecurity http) throws Exception {
        http
            .authorizeRequests()
                .antMatchers("/public/**").permitAll() // 특정 경로는 인증 없이 접근 가능
                .anyRequest().authenticated() // 그 외의 경로는 인증을 요구함
            .and()
            .formLogin() // 기본 로그인 페이지 사용
                .loginPage("/login") // 커스텀 로그인 페이지 경로
                .permitAll()
            .and()
            .logout() // 로그아웃 설정
                .permitAll();
    }
}
```