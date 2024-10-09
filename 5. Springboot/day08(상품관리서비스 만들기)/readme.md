# 상품관리 서비스 만들기
- 상품과 주문에 대한 관리를 할 수 있는 서비스를 만들어보자

## 백엔드 만들기
- 스프링부트 프로젝트 만들기
- Group : com.korea
- Artifact : product
### 필요 의존성
- Spring web
- H2
- lombok
- JPA

## Entity 만들기
- com.korea.product.model 패키지 생성하기
- ProductEntity클래스 생성하기
### 속성
- 상품id (primary key)
- 상품이름
- 상품재고
- 상품가격
- 등록날짜
- 수정날짜
```java
package com.korea.product.model;

import java.time.LocalDateTime;

import org.hibernate.annotations.CreationTimestamp;
import org.hibernate.annotations.UpdateTimestamp;

import jakarta.persistence.Entity;
import jakarta.persistence.GeneratedValue;
import jakarta.persistence.GenerationType;
import jakarta.persistence.Id;
import jakarta.persistence.Table;
import lombok.AllArgsConstructor;
import lombok.Builder;
import lombok.Data;
import lombok.NoArgsConstructor;

@Builder
@NoArgsConstructor
@AllArgsConstructor
@Data
@Entity
@Table(name = "Product")
public class ProductEntity {
    @Id
    @GeneratedValue(strategy = GenerationType.AUTO)
	private int productId;
	private String productName;
	private int productStock;
	private int productPrice;
	
	@CreationTimestamp//Insert 쿼리가 발생할 때 현재 시간 값을 적용시켜준다.
	private LocalDateTime registerDate;
	
	@UpdateTimestamp//Update 쿼리가 발생했을 때 현재 시간 값을 적용시켜준다.
	private LocalDateTime updateDate;

}

```
## DTO 만들기
- com.korea.product.dto 패키지 만들기
- ProductDTO 클래스 만들기
```java
package com.korea.product.dto;

import com.korea.product.model.ProductEntity;

import lombok.AllArgsConstructor;
import lombok.Builder;
import lombok.Data;
import lombok.NoArgsConstructor;

@Data
@Builder
@NoArgsConstructor
@AllArgsConstructor
public class ProductDTO {
	
	private int productId;
	private String productName;
	private int productStock;
	private int productPrice;
	private String registerDate;
	private String updateDate;
	
    // Entity -> DTO 변환
    public ProductDTO(ProductEntity entity) {
        this.productId = entity.getProductId();
        this.productName = entity.getProductName();
        this.productStock = entity.getProductStock();
        this.productPrice = entity.getProductStock();
        this.registerDate = entity.getRegisterDate();
        this.updateDate = entity.getUpdateDate();
    }

    // DTO -> Entity 변환
    public static ProductEntity toEntity(ProductDTO dto) {
        return ProductEntity.builder()
                .productId(dto.getProductId())
                .productName(dto.getProductName())
                .productStock(dto.getProductStock())
                .productPrice(dto.getProductPrice())
                .registerDate(dto.getRegisterDate())
                .updateDate(dto.getUpdateDate())
                .build();
    }
}
```

## ResponseDTO 만들기
- 클라이언트와 데이터를 직접적으로 주고받기 위한 ResponseDTO클래스 만들기
```java
package com.example.demo.dto;

import java.util.List;
import lombok.AllArgsConstructor;
import lombok.Builder;
import lombok.Data;
import lombok.NoArgsConstructor;

@Builder
@NoArgsConstructor
@AllArgsConstructor
@Data
public class ResponseDTO<T> {
	private String error;
	private List<T> data;
}

```
# 영속계층 만들기
## Repository 만들기
- com.korea.product.persistence 패키지 생성하기
- ProductRepository 인터페이스 생성하기
```java
package com.korea.product.persistence;

import org.springframework.data.jpa.repository.JpaRepository;
import org.springframework.stereotype.Repository;
import com.korea.product.model.ProductEntity;

@Repository
public interface ProductRepository extends JpaRepository<ProductEntity, Integer>{

}
```

# 서비스계층 만들기
## Service 만들기
- com.korea.product.service 패키지 생성하기
- ProductService 클래스 생성하기
- ProductRepository 주입하기
```java
@Service
@RequiredArgsConstructor
public class ProductService {

	private final ProductRepository p_repository;
}
```

# 표현계층 만들기
## Controller 만들기
- com.korea.product.controller 패키지 생성하기
- ProductController 클래스 생성하기
- ProductService 주입하기
```java
package com.korea.product.controller;

import org.springframework.web.bind.annotation.RestController;

import com.korea.product.service.ProductService;

import lombok.RequiredArgsConstructor;

@RestController
@RequiredArgsConstructor
public class ProductController {

	private final ProductService p_service;
}
```

## 모든 상품 조회하기
- 데이터베이스에 들어있는 모든 상품을 조회하시오
- 메서드명 : findAll();
### ProductService
```java
package com.korea.product.service;

import java.util.List;

import org.springframework.stereotype.Service;

import com.korea.product.model.ProductEntity;
import com.korea.product.persistence.ProductRepository;

import lombok.RequiredArgsConstructor;

@Service
@RequiredArgsConstructor
public class ProductService {

	private final ProductRepository p_repository;
	
	public List<ProductEntity> findAll() {
		return p_repository.findAll();
	}
}
```

### ProductController
```java
package com.korea.product.controller;

@RestController
@RequiredArgsConstructor
@RequestMapping("product")
public class ProductController {

	private final ProductService p_service;
	
	//조회하기
	@GetMapping
	public ResponseEntity<?> productList() {
		List<ProductEntity> entities = p_service.findAll();
		List<ProductDTO> dtos = entities.stream().map(ProductDTO::new).collect(Collectors.toList());
		ResponseDTO<ProductDTO> response = ResponseDTO.<ProductDTO>builder().data(dtos).build();
		return ResponseEntity.ok().body(response);
	}
}
```
- 포스트맨을 이용하여 결과를 확인해보세요
```json
{
    "error": null,
    "data": []
}
```
## 상품 추가하기
- db에 상품 추가하기
### ProductService
```java
//상품 추가하기
public List<ProductEntity> create(final ProductEntity entity) {
    // Validations
    validate(entity);

    p_repository.save(entity);
    return p_repository.findAll();
}

private void validate(final ProductEntity entity) {
    if(entity == null) {
        throw new RuntimeException("Entity cannot be null.");
    }
}
```

### ProductController
```java
@PostMapping
public ResponseEntity<?> createProduct(@RequestBody ProductDTO dto) {
    try {

        ProductEntity entity = ProductDTO.toEntity(dto);
        List<ProductEntity> entities = p_service.create(entity);
        List<ProductDTO> dtos = entities.stream().map(ProductDTO::new).collect(Collectors.toList());
        ResponseDTO<ProductDTO> response = ResponseDTO.<ProductDTO>builder().data(dtos).build();
        return ResponseEntity.ok().body(response);
    } catch (Exception e) {
        String error = e.getMessage();
        ResponseDTO<ProductDTO> response = ResponseDTO.<ProductDTO>builder().error(error).build();
        return ResponseEntity.badRequest().body(response);
    }
}
```
