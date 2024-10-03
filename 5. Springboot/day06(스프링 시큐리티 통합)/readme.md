# 스프링 시큐리티 통합
- 사용자에 관련된 클래스들은 로그인 여부를 저장하지 않는다는 점 때문에 불완전하다.
- 스프링 시큐리티와 JWT 토큰을 이용해 해결할 것이다.

## 로그인 유지 구현
- 모든 API 요청에 토큰을 보내는 것이다.
- 그러면 각 API는 맨 처음 토큰을 확인함으로써 접근을 허용 또는 거부하는 코드를 실행할 것이다.

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