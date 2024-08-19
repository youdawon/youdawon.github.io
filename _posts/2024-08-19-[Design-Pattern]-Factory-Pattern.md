---
layout: post
date: 2024-08-19
title: "[Design Pattern] Factory Pattern"
tags: [Design Pattern, Factory Pattern, ]
categories: [Design Pattern, ]
---


팩토리 패턴(Factory Pattern)은 객체 생성에 관련된 디자인 패턴 중 하나로, **객체 생성의 책임을 별도의 클래스나 메서드로 캡슐화하여, 객체 생성 과정을 클라이언트 코드에서 분리하는 패턴이다**. 이 패턴은 특히 객체 생성 로직이 복잡하거나 다양한 하위 클래스 중에서 선택적으로 객체를 생성해야 할 때 유용하다.


#### 핵심 개념


팩토리 패턴은 주로 다음 두 가지 형태로 나눌 수 있다.

1. **Simple Factory (간단한 팩토리)**
	- **개념**: 객체 생성 로직을 하나의 팩토리 클래스에 모아놓는 패턴. 클라이언트는 이 팩토리 클래스를 통해 객체를 생성한다.
	- **특징**:
		- 간단한 구조로, 하나의 클래스에서 모든 객체를 생성한다.
		- 새로운 객체를 추가할 때, 팩토리 클래스의 코드 수정이 필요하다.
	- **장점**: 구현이 간단하고 이해하기 쉽다.
	- **단점**: 확장성이 떨어지며, 새로운 객체를 추가할 때 기존 팩토리 클래스에 의존해야 한다.
2. **Factory Method (팩토리 메서드)**
	- **개념**: 객체 생성의 책임을 하위 클래스에 위임하는 패턴. 추상 팩토리 클래스가 팩토리 메서드를 정의하고, 각 하위 클래스가 구체적인 객체를 생성한다.
	- **특징**:
		- 객체 생성 로직이 하위 클래스로 분산된다.
		- 새로운 객체를 추가할 때 기존 코드를 수정할 필요 없이 새로운 하위 클래스를 추가하기만 하면 된다.
	- **장점**: 확장성이 뛰어나며, 코드의 유연성을 높인다.
	- **단점**: 구조가 더 복잡해지고, 관리해야 할 클래스가 많아진다.

#### **팩토리 패턴의 주요 특징**

- **객체 생성 로직의 캡슐화**: 객체 생성 로직을 클라이언트 코드에서 분리하여, 클라이언트가 객체 생성의 세부 사항을 알 필요 없게 한다.
- **코드 재사용성**: 공통된 객체 생성 로직을 한 곳에 모아두기 때문에 코드 재사용성이 높아진다.
- **확장성**: 특히 Factory Method 패턴의 경우, 새로운 객체 타입을 쉽게 추가할 수 있어 시스템의 확장성이 뛰어나다.
- **유지보수성 향상**: 객체 생성 로직이 집중 관리되므로, 수정이나 업데이트가 필요할 때 유지보수가 쉬워진다.

#### **사용 예시**

- **데이터베이스 연결**: 다양한 데이터베이스(예: MySQL, PostgreSQL 등)에 대한 연결 객체를 생성할 때 팩토리 패턴을 사용하면, 데이터베이스 타입에 따라 다른 연결 객체를 생성할 수 있다.
- **UI 컴포넌트 생성**: 다양한 스타일의 UI 컴포넌트를 필요에 따라 생성할 때 팩토리 패턴을 사용하여 다양한 컴포넌트를 관리할 수 있다.
- **로거 시스템**: 로깅 대상(파일, 콘솔 등)에 따라 다른 로거 객체를 생성할 때 사용된다.

#### 코드 예시

1. Simple Factory 패턴


{% raw %}
```java
// 공통 응답 클래스 (추상 클래스)
public abstract class ApiResponse {
    private String resultCode;

    public String getResultCode() {
        return resultCode;
    }

    public void setResultCode(String resultCode) {
        this.resultCode = resultCode;
    }
}

// 구체적인 응답 클래스
public class UserApiResponse extends ApiResponse {
    private String userName;
    private int userId;

    // Getters and Setters for userName and userId
    public String getUserName() {
        return userName;
    }

    public void setUserName(String userName) {
        this.userName = userName;
    }

    public int getUserId() {
        return userId;
    }

    public void setUserId(int userId) {
        this.userId = userId;
    }
}

public class ProductApiResponse extends ApiResponse {
    private String productName;
    private double price;

    // Getters and Setters for productName and price
    public String getProductName() {
        return productName;
    }

    public void setProductName(String productName) {
        this.productName = productName;
    }

    public double getPrice() {
        return price;
    }

    public void setPrice(double price) {
        this.price = price;
    }
}

// Simple Factory 클래스
public class ApiResponseFactory {

    public static ApiResponse createResponse(String apiType) {
        if (apiType == null) {
            return null;
        }
        if (apiType.equalsIgnoreCase("USER_API")) {
            return new UserApiResponse();
        } else if (apiType.equalsIgnoreCase("PRODUCT_API")) {
            return new ProductApiResponse();
        }
        return null;
    }
}

// 클라이언트 코드
public class Main {
    public static void main(String[] args) {
        ApiResponse userResponse = ApiResponseFactory.createResponse("USER_API");
        userResponse.setResultCode("200");
        System.out.println("User API Response Code: " + userResponse.getResultCode());

        ApiResponse productResponse = ApiResponseFactory.createResponse("PRODUCT_API");
        productResponse.setResultCode("200");
        System.out.println("Product API Response Code: " + productResponse.getResultCode());
    }
}
```
{% endraw %}


1. Factory Method 패턴


{% raw %}
```java
// 공통 응답 클래스 (추상 클래스)
public abstract class ApiResponse {
    private String resultCode;

    public String getResultCode() {
        return resultCode;
    }

    public void setResultCode(String resultCode) {
        this.resultCode = resultCode;
    }
}

// 구체적인 응답 클래스
public class UserApiResponse extends ApiResponse {
    private String userName;
    private int userId;

    // Getters and Setters for userName and userId
    public String getUserName() {
        return userName;
    }

    public void setUserName(String userName) {
        this.userName = userName;
    }

    public int getUserId() {
        return userId;
    }

    public void setUserId(int userId) {
        this.userId = userId;
    }
}

public class ProductApiResponse extends ApiResponse {
    private String productName;
    private double price;

    // Getters and Setters for productName and price
    public String getProductName() {
        return productName;
    }

    public void setProductName(String productName) {
        this.productName = productName;
    }

    public double getPrice() {
        return price;
    }

    public void setPrice(double price) {
        this.price = price;
    }
}

// 추상 팩토리 클래스
public abstract class ApiResponseFactory {
    public abstract ApiResponse createResponse();

    public ApiResponse getResponse() {
        ApiResponse response = createResponse();
        return response;
    }
}

// 구체적인 팩토리 클래스
public class UserApiResponseFactory extends ApiResponseFactory {

    @Override
    public ApiResponse createResponse() {
        return new UserApiResponse();
    }
}

public class ProductApiResponseFactory extends ApiResponseFactory {

    @Override
    public ApiResponse createResponse() {
        return new ProductApiResponse();
    }
}

// 클라이언트 코드
public class Main {
    public static void main(String[] args) {
        ApiResponseFactory userFactory = new UserApiResponseFactory();
        ApiResponse userResponse = userFactory.getResponse();
        userResponse.setResultCode("200");
        System.out.println("User API Response Code: " + userResponse.getResultCode());

        ApiResponseFactory productFactory = new ProductApiResponseFactory();
        ApiResponse productResponse = productFactory.getResponse();
        productResponse.setResultCode("200");
        System.out.println("Product API Response Code: " + productResponse.getResultCode());
    }
}
```
{% endraw %}


