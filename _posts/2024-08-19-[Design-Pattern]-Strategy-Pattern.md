---
layout: post
date: 2024-08-19
title: "[Design Pattern] Strategy Pattern"
tags: [Design Pattern, Strategy Pattern, ]
categories: [Design Pattern, ]
---


**전략 패턴**은 객체지향 설계에서 자주 사용되는 디자인 패턴 중 하나로, **동일한 작업을 여러 가지 방법으로 수행할 수 있게 하는 패턴**이다. 이 패턴은 알고리즘을 하나의 인터페이스로 정의하고, 각 알고리즘을 별도의 클래스로 캡슐화하여 필요에 따라 실행 시점에 알고리즘을 선택할 수 있게 한다.


#### **1. 핵심 개념**

- **인터페이스 정의**: 전략 패턴에서는 공통된 작업을 수행하는 인터페이스(또는 추상 클래스)를 정의한다.
- **구체적인 전략 클래스**: 각 알고리즘 또는 행동은 이 인터페이스를 구현한 구체적인 클래스들로 캡슐화된다.
- **컨텍스트 클래스**: 컨텍스트 클래스는 클라이언트가 설정한 전략 객체를 사용해 작업을 수행해. 이 클래스는 특정 전략을 선택하고 실행하는 역할을 한다.

#### **2. 전략 패턴의 구성 요소**

- **Strategy (전략 인터페이스)**: 실행될 알고리즘을 정의하는 인터페이스 또는 추상 클래스.
- **ConcreteStrategy (구체적인 전략 클래스)**: `Strategy` 인터페이스를 구현하는 구체적인 알고리즘 클래스들.
- **Context (컨텍스트 클래스)**: `Strategy` 객체를 포함하고 있으며, 클라이언트가 설정한 구체적인 전략을 사용하여 작업을 실행한다.

#### **3. 전략 패턴의 장점**

- **유연성**: 새로운 전략을 추가하더라도 기존 코드를 수정할 필요가 없다. 전략을 확장하거나 교체할 수 있는 유연성을 제공한다.
- **유지보수성**: 각 알고리즘이 별도의 클래스로 분리되어 있어, 코드의 가독성과 유지보수성이 향상된다.
- **재사용성**: 각 전략 클래스는 독립적이기 때문에, 다른 컨텍스트에서도 쉽게 재사용할 수 있다.

#### **4. 전략 패턴의 단점**

- **클래스 증가**: 전략을 추가할 때마다 새로운 클래스가 필요하므로, 클래스의 수가 증가할 수 있다.
- **복잡성**: 전략 패턴을 잘못 사용하면 코드가 복잡해질 수 있어. 특히 간단한 작업에 대해서는 과도한 설계가 될 수 있다.

#### **5. 전략 패턴의 사용 예시**

- **로그 처리**: 다양한 로그 처리 방식(콘솔 출력, 파일 기록, 원격 서버 전송)을 동적으로 선택할 수 있도록 전략 패턴을 사용할 수 있다.
- **인증 방식**: 여러 인증 방법(Basic Authentication, OAuth, JWT)을 필요에 따라 적용할 수 있도록 전략 패턴을 사용할 수 있다.
- **정렬 알고리즘**: 특정 조건에 따라 다양한 정렬 알고리즘(퀵 정렬, 병합 정렬 등)을 선택하여 사용할 수 있다.
- **결제 수단**: 전자상거래 시스템에서 신용카드, PayPal, 가상화폐 등 다양한 결제 수단을 전략 패턴으로 구현하여 유연하게 선택할 수 있다.

#### **6. 코드 예시**

1. 로그 처리에 전략 패턴 적용


{% raw %}
```java
// 로그 전략 인터페이스
public interface LogStrategy {
    void log(String message);
}

// 콘솔 로그 전략
public class ConsoleLogStrategy implements LogStrategy {
    @Override
    public void log(String message) {
        System.out.println("Console Log: " + message);
    }
}

// 파일 로그 전략
public class FileLogStrategy implements LogStrategy {
    @Override
    public void log(String message) {
        // 파일에 로그를 쓰는 코드 (예시로 간단히 표현)
        System.out.println("File Log: " + message);
    }
}

// 원격 서버 로그 전략
public class RemoteLogStrategy implements LogStrategy {
    @Override
    public void log(String message) {
        // 원격 서버로 로그를 전송하는 코드 (예시로 간단히 표현)
        System.out.println("Remote Log: " + message);
    }
}

// 로그 컨텍스트 클래스
public class LoggerContext {
    private LogStrategy logStrategy;

    // 전략 설정 메서드
    public void setLogStrategy(LogStrategy logStrategy) {
        this.logStrategy = logStrategy;
    }

    // 로그 메시지 출력 메서드
    public void log(String message) {
        logStrategy.log(message);
    }
}

// 클라이언트 코드
public class Main {
    public static void main(String[] args) {
        LoggerContext logger = new LoggerContext();

        // 콘솔 로그 사용
        logger.setLogStrategy(new ConsoleLogStrategy());
        logger.log("This is a console log message.");

        // 파일 로그 사용
        logger.setLogStrategy(new FileLogStrategy());
        logger.log("This is a file log message.");

        // 원격 서버 로그 사용
        logger.setLogStrategy(new RemoteLogStrategy());
        logger.log("This is a remote server log message.");
    }
}
```
{% endraw %}


1. 인증 방식에 전략 패턴 적용


{% raw %}
```java
// 인증 전략 인터페이스
public interface AuthStrategy {
    boolean authenticate(String username, String password);
}

// 기본 인증 전략 (username과 password를 직접 비교)
public class BasicAuthStrategy implements AuthStrategy {
    @Override
    public boolean authenticate(String username, String password) {
        // 예시: username과 password를 단순히 비교 (실제로는 더 복잡한 검증 로직이 필요)
        return "admin".equals(username) && "password".equals(password);
    }
}

// OAuth 인증 전략
public class OAuthStrategy implements AuthStrategy {
    @Override
    public boolean authenticate(String username, String password) {
        // OAuth 인증 처리 로직 (여기선 간단히 표현)
        System.out.println("Authenticating using OAuth for user: " + username);
        return true; // 실제로는 OAuth 토큰 검증 등이 필요함
    }
}

// JWT 인증 전략
public class JWTStrategy implements AuthStrategy {
    @Override
    public boolean authenticate(String username, String password) {
        // JWT 토큰을 검증하는 로직 (여기선 간단히 표현)
        System.out.println("Authenticating using JWT for user: " + username);
        return true; // 실제로는 JWT 토큰 파싱 및 검증이 필요함
    }
}

// 인증 컨텍스트 클래스
public class AuthContext {
    private AuthStrategy authStrategy;

    // 전략 설정 메서드
    public void setAuthStrategy(AuthStrategy authStrategy) {
        this.authStrategy = authStrategy;
    }

    // 인증 실행 메서드
    public boolean authenticate(String username, String password) {
        return authStrategy.authenticate(username, password);
    }
}

// 클라이언트 코드
public class Main {
    public static void main(String[] args) {
        AuthContext authContext = new AuthContext();

        // 기본 인증 사용
        authContext.setAuthStrategy(new BasicAuthStrategy());
        boolean isAuthenticated = authContext.authenticate("admin", "password");
        System.out.println("Basic Authenticated: " + isAuthenticated);

        // OAuth 인증 사용
        authContext.setAuthStrategy(new OAuthStrategy());
        isAuthenticated = authContext.authenticate("admin", "password");
        System.out.println("OAuth Authenticated: " + isAuthenticated);

        // JWT 인증 사용
        authContext.setAuthStrategy(new JWTStrategy());
        isAuthenticated = authContext.authenticate("admin", "password");
        System.out.println("JWT Authenticated: " + isAuthenticated);
    }
}
```
{% endraw %}


