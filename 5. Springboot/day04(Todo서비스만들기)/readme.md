# Todo서비스 만들기
- 스프링과 JPA를 기반으로 생성,검색,수정,삭제 API를 만들어보자.
- 각 기능별 작성 순서는 다음과 같다.
```
영속레이어 > 서비스레이어 > 표현레이어
```


## 로그
- 소프트웨어 시스템이나 애플리케이션에서 동작 상태나 이벤트가 발생했을 때, 그 내용을 기록한 정보다.
- 개발자, 운영자, 또는 시스템이 해당 애플리케이션의 상태를 파악하거나 문제 해결을 위해 사용한다.
- 주로 애플리케이션의 실행 흐름, 오류 또는 성능 문제를 추적하고 분석하는 데 매우 중요한 도구다.

### 로그의 주요 목적
1. 디버깅
    - 애플리케이션에서 발생한 문제나 버그를 추적하고 원인을 파악하기 위해 사용된다. 
    - 디버깅 시 로그를 통해 애플리케이션이 어떤 작업을 하고 있었는지, 어떤 오류가 발생했는지를 알 수 있다.
2. 모니터링
    - 애플리케이션이 예상대로 작동하는지 확인하고, 시스템 성능을 모니터링하기 위해 사용된다. 
    - 예를 들어, 응답 속도, 메모리 사용량 등을 로그로 기록하여 애플리케이션의 성능을 분석할 수 있다.
3. 문제 해결
    - 애플리케이션에서 예상치 못한 상황이 발생했을 때, 로그를 통해 그 문제를 해결하는 데 필요한 정보를 얻을 수 있다. 
    - 특히, 시스템이 갑작스럽게 중단되거나 성능 저하가 발생했을 때, 그 원인을 파악하는 데 중요한 역할을 한다.
4. 보안 감사
    - 애플리케이션에 대한 보안 감사 및 추적을 위해 사용된다. 
    - 시스템에 대한 접근 시도나 비정상적인 활동을 로그로 기록하여, 보안 위협을 감지하고 대응할 수 있다.

### 로그의 주요 구성 요소
1. 타임스탬프 : 로그가 기록된 시간. 이는 이벤트가 발생한 시점을 추적하는 데 매우 중요하다.
2. 로그 레벨(Log Level) : 로그의 중요도를 나타내며, 보통 아래와 같은 레벨이 사용된다.
   1. TRACE: 가장 낮은 수준의 로그. 아주 상세한 디버깅 정보.
   2. DEBUG: 개발 과정에서 주로 사용되는 디버깅 정보.
   3. INFO: 시스템의 정상적인 동작을 나타내는 정보.
   4. WARN: 예상치 못한 상황이 발생했지만, 시스템이 정상적으로 동작하는 경우.
   5. ERROR: 오류가 발생했으며, 시스템이 정상적으로 동작하지 않는 경우.
   6. FATAL: 매우 심각한 오류로, 시스템이 더 이상 동작할 수 없는 경우.
3. 메시지 : 로그에 기록된 이벤트에 대한 설명. 어떤 일이 일어났는지 명확하게 기술한다.
4. 이벤트 소스 : 로그가 기록된 위치, 예를 들어 특정 클래스, 메서드, 또는 모듈

## Slf4j(Simple Logging Facade for Java)
- Java 애플리케이션에서 사용하는 로깅 프레임워크에 대한 통합된 인터페이스를 제공하는 로그 추상화 라이브러리다.
- SLF4J는 로그를 작성하는 표준 인터페이스를 제공하고, 실제로 로그를 기록하는 것은 Logback, Log4j 같은 다른 로깅 프레임워크가 담당하는 방식이다.

### SLF4J가 필요한 이유
- 과거에는 애플리케이션에서 로그를 기록하기 위해 다양한 로깅 프레임워크가 사용되었다.
- 이들은 각각 고유한 API를 가지고 있어서, 만약 다른 로깅 프레임워크로 교체하려면 코드를 전부 수정해야 했다.
- SLF4J는 여러 로깅 프레임워크에 대한 추상화 레이어를 제공해 개발자는 한 가지 방식으로 로그를 작성하고, 나중에 어떤 로깅 프레임워크를 사용할 지결정 할 수 있게 되었다.

### SLF4J의 역할
1. 로깅 프레임워크의 추상화
    - 개발자가 SLF4J API를 사용하여 로그를 기록하면, SLF4J가 이를 구체적인 로깅 프레임워크에 전달한다.
    - 스프링은 기본적으로 Logback 라이브러리를 사용한다.
2. 호환성 유지
    - SLF4J 덕분에 애플리케이션의 로깅 구현체를 변경할 때 기존 코드를 수정할 필요 없이 로깅 라이브러리만 바꿔서 사용할 수 있다.

## TodoService에 코드 추가하기
- TodoService클래스에 @Slf4j 어노테이션 추가하기
```java

@Slf4j
@Service
public class TodoService {
	
	@Autowired
	private TodoRepository repository;

	public String testService() {
		... 중략
	}
}
```

## Create Todo구현
- Todo 아이템을 생성하는 기능을 구현해보자
  
## 영속레이어의 구현
- TodoRepository는 JpaRepository를 상속하므로 JpaRepository가 제공하는 다양한 메서드를 사용할 수 있다.
- 엔티티를 저장하기 위해 save()메서드를 사용하고, 새 Todo 리스트를 반환하기 위해 findByUserId()메서드를 사용한다.

## 서비스레이어 구현
- TodoService클래스에 Todo아이템을 생성하기 위한 비즈니스로직을 작성한다.
- create()메서드를 작성한다.
### create 메서드의 구성
- 검증
  - 넘어온 엔티티가 유효한지 검사하는 로직
  - 이 부분은 코드가 더 커지면 TodoValidator 클래스로 분리시킬 수 있다.
- save()
  - 엔티티를 데이터베이스에 저장한다.
  - 로그를 남긴다.
- findByUserId()
  - 저장된 엔티티를 포함하는 새 리스트를 반환한다.

```java
package com.example.demo.service;

import java.util.List;

import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.stereotype.Service;

import com.example.demo.model.TodoEntity;
import com.example.demo.persistence.TodoRepository;

import lombok.extern.slf4j.Slf4j;

@Slf4j
@Service
public class TodoService {
	
	@Autowired
	private TodoRepository repository;

	public String testService() {
		...
	}
	
	
	public List<TodoEntity> create(TodoEntity entity){
		//매개변수로 넘어온 Entity가 유효한지 검사한다.
		if(entity == null) {
			log.warn("Entity cannot be null.");
			throw new RuntimeException("Entity cannot be null");
		}
		
		if(entity.getUserId() == null) {
			log.warn("Unknown user");
			throw new RuntimeException("Unknown user");
		}
		
		repository.save(entity);
		
        //{}는 SLF4J에서 제공하는 플레이스홀더로, 두 번째 매개변수로 전달된 entity.getId() 값이 여기에 대입되어 출력된다.
		log.info("Entity Id : {} is saved",entity.getId());
		
		return repository.findByUserId(entity.getUserId());
	}
}
```
