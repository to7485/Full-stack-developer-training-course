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

- 스프링 시큐리티는 스프링 기반 애플리케이션에서 **인증**(Authentication)과 **인가**(Authorization)를 처리하기 위한 강력한 보안 프레임워크다. 
- 스프링 애플리케이션에서 보안과 관련된 다양한 요구 사항을 손쉽게 구현할 수 있도록 돕는다.

## 주요 개념

1. **인증(Authentication)**
   - 사용자가 누구인지 확인하는 과정.
   - 사용자가 애플리케이션에 접근할 때 제공한 자격 증명(예: 사용자명, 비밀번호)을 확인하여 신원을 검증하는 단계.
   
2. **인가(Authorization)**
   - 인증된 사용자가 어떤 리소스에 접근할 수 있는지 결정하는 과정.
   - 사용자에게 주어진 역할(Role)과 권한(Authority)에 따라 리소스에 대한 접근 권한을 부여한다.

3. **필터 기반 아키텍처**
   - 스프링 시큐리티는 필터 체인을 기반으로 동작한다.
   - HTTP 요청이 들어오면 여러 보안 필터들이 순차적으로 실행되어 요청을 처리하고, 보안 관련 로직을 적용한다.

## 스프링 시큐리티와 서블릿 필터
- API가 실행될 때마다 사용자를 인증해주는 부분을 구현해야 한다.
- 스프링 시큐리티를 이용해서 해결한다고 했는데 어떤원리로 해결을 해주는걸까?
- HTTP 요청과 응답을 가로채어, 요청이 컨트롤러에 도달하기 전 또는 응답이 클라이언트에 전달되기 전에 필요한 전처리 또는 후처리를 수행하는 데 사용된다. 
- 주로 보안, 로깅, 인증, 인코딩 설정, 데이터 압축 등의 작업을 처리하는 데 유용하다.
- 우리는 서블릿 필터를 구현하고 서블릿 필터를 서블릿 컨테이너가 실행하도록 설정해주기만 하면 된다.

![img](img/스프링부트작동원리.jpg)

### 서블릿 필터예제
```java
package com.example.demo.security;

//서블릿 필터란 HttpFilter또는 Filter를 상속하는 클래스이다.
// HttpFilter 클래스를 상속받아 서블릿 필터 구현
public class ExampleServletFilter extends HttpFilter {

    // TokenProvider 객체를 이용해 토큰을 검증하고 사용자 정보를 가져오는 역할
    private TokenProvider tokenProvider;

    // 필터의 주요 로직을 처리하는 메서드로, 요청이 필터를 거칠 때마다 실행됨
    @Override
    protected void doFilter(HttpServletRequest request, HttpServletResponse response, FilterChain chain)
            throws IOException, ServletException {
        try {
            // HTTP 요청에서 Bearer 토큰을 파싱하여 가져옴
            final String token = parseBearerToken(request);
            
            // 토큰이 존재하고 값이 유효할 때
            if (token != null && !token.equalsIgnoreCase("null")) {
                // 토큰을 검증하여 사용자 ID를 가져옴 (유효하지 않은 토큰일 경우 예외 발생)
                String userId = tokenProvider.validateAndGetUserId(token);
                
                // 사용자 인증 후, 필터 체인의 다음 필터를 실행 (인증된 사용자 요청 처리)
                chain.doFilter(request, response);
            }
        } catch (Exception e) {
            // 예외가 발생하면 HTTP 응답을 403 Forbidden으로 설정
            response.setStatus(HttpServletResponse.SC_FORBIDDEN);
        }
    }

    // Authorization 헤더에서 Bearer 토큰을 파싱하는 메서드
    private String parseBearerToken(HttpServletRequest request) {
        // HTTP 요청의 헤더에서 Authorization 값을 가져옴
        String bearerToken = request.getHeader("Authorization");
        
        // Bearer 토큰 형식일 경우에만 토큰 값을 반환
        if (StringUtils.hasText(bearerToken) && bearerToken.startsWith("Bearer ")) {
            return bearerToken.substring(7); // 'Bearer ' 문자열을 제거하고 토큰만 반환
        }
        return null; // Bearer 토큰이 없을 경우 null 반환
    }
}
```
- 이렇게 필터를 구현하고 나면 서블릿 컨테이너(톰캣)가 ExampleServletFilter를 사용하도록 어딘가에 설정해야 한다.
```xml
<filter>
	<filter-name>ExampleServletFilter</filter-name>
	<filter-class>com.example.demo.security.ExampleServletFilter </filter-class>
</filter>

<filter-mapping>
	<filter-name>ExampleServletFilter</filter-name>
	<url-pattern>/todo</url-pattern>
</filter-mapping>
```
- 스프링부트를 사용하지 않는 웹 서비스의 경우 web.xml과 같은 설정 파일에 이 필터를 어느 경로(/todo)에 적용해야 하는지 알려줘야 한다.
- 서블릿 컨테이너가 서블릿 필터 실행시 xml에 설정된 필터를 실행시켜준다.
![img](img/필터의개수.jpg)
- 서블릿 필터가 꼭 한 개일 필요는 없다.
- 걸러내고 싶은 모든 것을 하나의 클래스에 담으면 그 크기가 매우 커질것이다.
- 그래서 기능에 따라 다른 서블릿 필터를 작성할 수 있고 이 서블릿 필터들을 FilterChain을 이용해 연쇄적으로 순서대로 실행할 수 있다.
- doFilter()메서드가 다음으로 부를 필터를 FilterChain안에 갖고 있어 다음 필터를 실행할 수 있다.

![img](img/시큐리티적용.jpg)

- 스프링 시큐리티 프로젝트를 추가하면 스프링 시큐리티가 FilterChainProxy라는 필터를 서블릿 필터에 끼워넣어준다.
- FilterChainProxy클래스 안에는 내부적으로 필터를 실행시키는데 이 필터들이 스프링이 관리하는 스프링 빈 필터다.
- Filter를 만들기 위해 HttpFilter 대신 OncePerRequestFilter를 상속한다.
- web.xml이 없기 때문에 WebSecurityConfigurerAdapter클래스를 상속해 필터를 설정한다.

## JWT를 이용한 인증 구현
- 스프링 시큐리티를 사용해서 본격적으로 구현을 해보자.

### 1. 스프링 시큐리티 의존성 추가하기
```groovy
// https://mvnrepository.com/artifact/org.springframework.boot/spring-boot-starter-security
implementation group: 'org.springframework.boot', name: 'spring-boot-starter-security', version: '3.2.4'
```

### 2. JwtAuthenticationFilter 클래스 만들기
- com.example.demo.security에 만들기
```java
package com.example.demo.security;

import java.io.IOException;

import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.security.authentication.AbstractAuthenticationToken;
import org.springframework.security.authentication.UsernamePasswordAuthenticationToken;
import org.springframework.security.core.authority.AuthorityUtils;
import org.springframework.security.core.context.SecurityContext;
import org.springframework.security.core.context.SecurityContextHolder;
import org.springframework.security.web.authentication.WebAuthenticationDetailsSource;
import org.springframework.stereotype.Component;
import org.springframework.util.StringUtils;
import org.springframework.web.filter.OncePerRequestFilter;

import jakarta.servlet.FilterChain;
import jakarta.servlet.ServletException;
import jakarta.servlet.http.HttpServletRequest;
import jakarta.servlet.http.HttpServletResponse;
import lombok.extern.slf4j.Slf4j;

@Slf4j
@Component
public class JwtAuthenticationFilter extends OncePerRequestFilter{

	@Autowired
	private TokenProvider tokenProvider;
	
	
	//doFilterInternal() : 스프링 시큐리티의 OncePerRequestFilter를 상속받은 메서드로, 한 요청에 대해 한 번만 실행되도록 보장된다.
	@Override
	protected void doFilterInternal(HttpServletRequest request, HttpServletResponse response, FilterChain filterChain)
			throws ServletException, IOException {
		try {
			//parseBearerToken 메서드:
			//HTTP 요청 헤더에서 Authorization 값을 가져와 Bearer 토큰 형식인지 확인한 후, 토큰 값을 반환한다.
			//토큰이 없거나 유효하지 않으면 null을 반환한다.
			String token = parseBearerToken(request);
			log.info("Filter is running...");

			//토큰 검사하기. JWT이므로 인가 서버에 요청하지 않고도 검증 가능.
			if(token != null && !token.equalsIgnoreCase("null")) {

				//userId 가져오기. 위조된 경우 예외처리한다.
				//TokenProvider에서 토큰을 검증하고 userId를 가져옴
				String userId = tokenProvider.validateAndGetUserId(token);
				log.info("Authenticated user ID : " + userId);

				//인증 완료; SecurityContextHolder에 등록해야 인증된 사용자라고 생각한다.
				AbstractAuthenticationToken authentication = new UsernamePasswordAuthenticationToken(userId, null,AuthorityUtils.NO_AUTHORITIES);
				authentication.setDetails(new WebAuthenticationDetailsSource().buildDetails(request));
				SecurityContext securityContext = SecurityContextHolder.createEmptyContext();
				securityContext.setAuthentication(authentication);
				SecurityContextHolder.setContext(securityContext);
			}
		} catch (Exception e) {
			logger.error("Could not set user authentication in security context", e);
		}
		filterChain.doFilter(request, response);
	}
	
	private String parseBearerToken(HttpServletRequest request) {
		//Http 요청의 헤더를 파싱해 Barer 토큰을 반환한다.
		String bearerToken = request.getHeader("Authorization");
		
		if(StringUtils.hasText(bearerToken) && bearerToken.startsWith("Bearer ")) {
			return bearerToken.substring(7);
		}
		return null;
	}
	

}
```