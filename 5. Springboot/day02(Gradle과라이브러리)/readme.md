# Gradle
- **Gradle**은 자바, 코틀린, 그루비(Groovy) 등 다양한 프로그래밍 언어를 지원하는 **빌드 자동화 도구**이다. 
- Gradle은 의존성 관리, 테스트 실행, 배포, 패키징 등의 빌드 작업을 자동화하며, **유연성**과 **확장성**을 중시한다.
- 특히 **멀티 프로젝트 빌드**와 **병렬 빌드**에 강력한 성능을 발휘하며, 자바 기반 프로젝트에서는 Maven이나 Ant의 대안으로 많이 사용된다.

### Gradle의 주요 특징

1. **의존성 관리**:
   - Gradle은 Maven Central, JCenter, Ivy 같은 **의존성 저장소**에서 외부 라이브러리를 쉽게 가져와 사용할 수 있도록 도와준다.
   - 이를 통해 개발자는 필요한 라이브러리를 직접 다운로드하지 않고, 빌드 시 자동으로 라이브러리를 다운로드하고 관리할 수 있다.

2. **DSL (Domain-Specific Language)**:
   - Gradle은 빌드 스크립트를 작성할 때 **그루비(Groovy)** 또는 **코틀린(Kotlin)** 기반의 DSL을 사용한다. 
   - 이 DSL을 사용해 빌드 로직을 간결하고 유연하게 작성할 수 있다.
   - `build.gradle` 파일에 그루비 기반으로 빌드 설정을 작성하거나, `build.gradle.kts` 파일에 코틀린 기반으로 작성할 수 있다.

3. **멀티 프로젝트 빌드**:
   - Gradle은 여러 프로젝트를 하나로 묶어 **멀티 프로젝트 빌드**를 지원합니다. 
   - 대규모 애플리케이션 개발 시 여러 모듈을 독립적으로 빌드하면서, 이들 간의 의존성을 쉽게 관리할 수 있다.

4. **병렬 빌드**:
   - Gradle은 **병렬 빌드**를 지원하여 여러 작업을 동시에 처리할 수 있습니다. 이를 통해 빌드 시간을 크게 단축할 수 있습니다.

5. **플러그인 시스템**:
   - Gradle은 다양한 **플러그인**을 제공하여 빌드 작업을 확장할 수 있습니다. 특히 자바, 스프링 부트, 안드로이드 개발에서 유용한 플러그인이 많이 사용됩니다.
   - 예: `java` 플러그인, `application` 플러그인, `spring-boot` 플러그인, `kotlin` 플러그인 등.

6. **유연성**:
   - Gradle은 빌드 과정을 매우 세밀하게 제어할 수 있는 유연성을 제공합니다. 필요한 경우 Ant와 같은 다른 빌드 도구와 함께 사용할 수도 있습니다.


## **`build.gradle`**
- 프로젝트의 주요 빌드 설정을 정의하는 파일입니다. 여기에 의존성, 플러그인, 태스크(작업) 등을 정의할 수 있습니다.

### plugins
- Gradle에서 빌드 작업을 확장하고 자동화할 수 있도록 해주는 기능이다.
- 플러그인을 통해 다양한 기능을 추가할 수 있는데, 프로젝트에 필요한 빌드 작업이나 설정을 플러그인을 통해 쉽게 적용할 수 있다.
- 여러 작업을 미리 정의해둔 기능 모음이라고 생각하면 된다.
```groovy
plugins {
	id 'java' //자바 프로젝트에서 필수적인 빌드 작업들을 제공하는 플러그인이다.자바 코드를 컴파일하고, 테스트 코드를 실행하며, JAR 파일을 생성하는 작업을 자동으로 처리해준다.
	id 'org.springframework.boot' version '3.2.10'//스프링 부트 관련 종속성을 관리하고, 스프링 부트 애플리케이션을 패키징하거나 실행하는 데 필요한 작업들을 자동으로 제공해준다.
	id 'io.spring.dependency-management' version '1.1.6'//라이브러리나 플러그인의 의존성 버전을 쉽게 관리하고, 중복된 의존성이나 버전 충돌 문제를 방지해준다.
}
```
### group
- 프로젝트의 그룹 ID를 설정한다.

### version
- 프로젝트 버전을 설정한다.
- SNAPSHOT은 아직 완성되지 않은 버전이라는 의미로 자주 사용된다.
```groovy
group = 'com.example'
version = '0.0.1-SNAPSHOT'
```
### 자바 버전 설정(toolchain)
- 자바 버전 17을 사용하도록 설정하는 부분이다. 
- Gradle은 toolchain을 통해 명시적으로 자바 버전을 관리할 수 있다. 
- 이 설정을 통해 자바 17 버전의 컴파일러와 런타임 환경에서 프로젝트가 빌드되도록 한다.
```groovy
java {
	toolchain {
		languageVersion = JavaLanguageVersion.of(17)
	}
}
```
### Configuration 설정
- 이 설정은 컴파일할 때만 사용되는 의존성 설정이다.
```groovy
configurations {
	compileOnly {
		extendsFrom annotationProcessor
	}
}
```

### 저장소 설정
- Gradle이 라이브러리를 다운로드 하는 곳을 레포지토리라고 한다.
- Maven Central을 주로 사용한다.
- 메이븐센트럴은 https://mvnrepository.com/repos/central이다.

```groovy
repositories {
	mavenCentral()
}
```
### 의존성 설정
- implementation: 프로젝트에서 런타임에 사용될 라이브러리를 정의한다.
    - spring-boot-starter-data-jpa: 스프링 부트에서 JPA(자바 퍼시스턴스 API)를 사용하기 위한 의존성이다.
    - spring-boot-starter-web: 웹 애플리케이션 개발을 위한 의존성이다. REST API, 웹 MVC 등을 지원한다.
    - com.google.guava:guava: 구글의 유명한 라이브러리인 Guava를 추가했다. 주로 컬렉션, 문자열 처리 등의 유틸리티 기능을 제공한다.
- compileOnly: 컴파일 시에만 필요한 라이브러리이다. 주로 애노테이션 프로세서를 사용하지만, 런타임에는 포함되지 않는다.
    - org.projectlombok:lombok: Lombok은 자바 코드에서 반복적인 Getter, Setter, 생성자 등을 자동으로 생성해주는 라이브러리이다. 컴파일 시에만 필요하다.
- runtimeOnly: 런타임에만 필요한 라이브러리를 정의한다.
    - com.h2database:h2: 내장형 데이터베이스 H2를 런타임에서 사용할 수 있도록 설정한다. 주로 테스트 환경이나 간단한 애플리케이션에서 사용된다.
- annotationProcessor: 컴파일 타임에 애노테이션을 처리하는 라이브러리다. Lombok 같은 애노테이션 프로세서를 등록하는 곳이다.

- testImplementation: 테스트 코드를 실행할 때 필요한 라이브러리이다.
    - spring-boot-starter-test: 스프링 부트에서 JUnit과 같은 테스트 기능을 제공하는 의존성이다.
- testRuntimeOnly: 테스트 환경에서만 사용할 수 있는 라이브러리이다.
    - junit-platform-launcher: JUnit 테스트 실행기이다.
```groovy
dependencies {
	implementation 'org.springframework.boot:spring-boot-starter-data-jpa'
	implementation 'org.springframework.boot:spring-boot-starter-web'
	compileOnly 'org.projectlombok:lombok'
	runtimeOnly 'com.h2database:h2'
	annotationProcessor 'org.projectlombok:lombok'
	testImplementation 'org.springframework.boot:spring-boot-starter-test'
	testRuntimeOnly 'org.junit.platform:junit-platform-launcher'
	// https://mvnrepository.com/artifact/com.google.guava/guava
	implementation group: 'com.google.guava', name: 'guava', version: '33.3.1-jre'
	
}
```
### 테스트 설정
- 테스트 설정
- JUnit 플랫폼을 사용해 테스트를 실행하도록 설정한다.
```groovy
tasks.named('test') {
	useJUnitPlatform()
}
```

## 디펜던시에 라이브러리 추가해보기
- Guava라이브러리 추가하기

### mvnrepository
- https://mvnrepository.com/로 이동해서 guava를 검색한다.

![img](img/mvn.png)

- 원하는 버전을 선택한다.
- 어떤 버전을 골라야할지 모르겠다면 이용자가 많은 버전을 사용하자.

![img](img/versopm.png)

- Gradle을 선택하고 아래코드를 누르면 클립보드에 복사가 된다.

![img](img/copy.png)

- Gradle.build 파일의 dependencies부분에 붙혀넣기를 한다.

```groovy
dependencies {
	implementation 'org.springframework.boot:spring-boot-starter-data-jpa'
	implementation 'org.springframework.boot:spring-boot-starter-web'
	compileOnly 'org.projectlombok:lombok'
	runtimeOnly 'com.h2database:h2'
	annotationProcessor 'org.projectlombok:lombok'
	testImplementation 'org.springframework.boot:spring-boot-starter-test'
	testRuntimeOnly 'org.junit.platform:junit-platform-launcher'

	// https://mvnrepository.com/artifact/com.google.guava/guava
	implementation group: 'com.google.guava', name: 'guava', version: '31.1-jre'
}
```

## 롬복(Lombok)
- 롬복을 사용하면 더 이상 getter/setter, builder, constructor를 작성하는 데 시간을 소모할 피룡가 없다.
- 롬복이 제공하는 어노테이션 프로세서가 getter,setter,builder,constructor 프로젝트 컴파일 시 관련 코드를 자동으로 작성해준다.
- 따라서 롬복을 사용하면 코드의 양을 줄이고 개발 시간도 단축할 수 있다.
- 이클립스에서 롬복을 사용하려면 jar파일을 이용해 플러그인을 설치해야 한다.

### 이클립스에 롬복 설치
- 메이븐 레포지토리(https://mvnrepository.com/)에서 원하는 버전의 Jar를 받아온다.

![img](img/lombok.png)

- 다운로드가 완료되면 cmd를 열어 Jar파일이 다운로드된 디렉토리로 이동한 후 다음의 명령어로 롬복을 설치한다.

```
java -jar lombok-1.18.30.jar
```

![img](img/lombok2.png)

- 롬복이 자동으로 이클립스를 찾지 못한다면 왼쪽 아래 버튼을 눌러 이클립스 실행파일을 찾아준다.

![img](img/find.png)

- 오른쪽 아래 install/update버튼을 눌러 설치를 진행하면 끝난다.

![img](img/install.png)

- Quit installer 버튼을 누른후 이클립스를 껐다가 재시작한다.

- build.gradle 파일에서 롬복이 잘 추가됐는지 확인한다.
```
annotationProcessor 'org.projectlombok:lombok'
compileOnly 'org.projectlombok:lombok'
```
- Help > About Eclipse IDE로 들어가 About 하단에서 Lombok 설치 여부를 확인한다.

![img](img/about.png)

### DemoModel.java파일 생성하기
```java
package com.example.demo;

import lombok.Builder;
import lombok.NonNull;
import lombok.RequiredArgsConstructor;

@Builder
@RequiredArgsConstructor
public class DemoModel {

	@NonNull
	String id;
}
```
- outline탭에 다음과 같이 나오면 롬복이 잘 적용이 된것이다.

![img](img/lombok3.png)

### 만약 적용이 잘 안될 시
- 프로젝트 우클릭 > Properties > Java Compiler > Annotation Processing
- Enable project specific settings 체크하고 저장하기

## 포스트맨 API 테스트
- REST API는 크게 나눠 URI, HTTP메섣, 요청 매개변수 또는 요청바디로 구분도는데, 이를 브라우저에서 테스팅하는 것에는 한계가 있다.
- 테스트를 한다고 임시로 프론트엔드 UI를 만드는 것은 지속가능한 방법이 아니다.
- 사용이 간편하고 직관적인 GUI를 제공하는 포스트맨이라는 프로그램을 사용한다.
- 포스트맨을 사용하면 간단히 RESTful API를 테스트 할 수 있다.
- 또 테스트를 저장해 API 스모크 테스팅 용으로 사용할 수 있다.

### 포스트맨 설치하기
- https://www.postman.com/downloads/에서 다운후 설치해보자.

- +버튼을 누르면 새요청을 작성할 수 있다.
- 우리의 부트 어플리케이션을 실행한 후 포스트맨을 이용해 localhost:9090을 요청하고 결과를 보자.
