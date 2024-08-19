---
layout: post
date: 2024-08-17
title: "[DesignPattern] Singleton Pattern"
tags: [Design Pattern, Singleton Pattern, ]
categories: [Design Pattern, ]
---


---


#### 싱글톤 패턴 (Singleton Pattern) 정리


**목표**: 특정 클래스의 인스턴스가 애플리케이션 전역에서 오직 하나만 존재하도록 보장하고, 이 인스턴스에 전역적으로 접근할 수 있도록 한다.


**주요 특징**:

1. **인스턴스 하나**: 클래스의 인스턴스가 오직 하나만 생성되며, 이 인스턴스에 전역적으로 접근할 수 있다.
2. **전역 접근**: 애플리케이션의 모든 부분에서 인스턴스에 접근할 수 있는 전역적인 접근점을 제공한다.
3. **인스턴스 생성 제어**: 클래스 내에서 인스턴스의 생성과 관리를 직접 제어한다.

#### 1. 기본 구현 (Lazy Initialization)

1. **설명**:
- 인스턴스를 필요할 때까지 생성하지 않는다.
- `getInstance()` 메서드에서 인스턴스가 `null`이면 새로 생성한다.

**코드 예시**:



{% raw %}
```java
public class Singleton {
    private static Singleton instance;

    private Singleton() {
        // Private constructor to prevent instantiation
    }

    public static Singleton getInstance() {
        if (instance == null) {
            instance = new Singleton();
        }
        return instance;
    }
}
```
{% endraw %}



**장점**:

- 메모리 사용을 최소화한다. 인스턴스가 필요할 때만 생성된다.

**단점**:

- 멀티스레드 환경에서 동기화가 필요 없다. 인스턴스가 중복 생성될 수 있다.

#### 2. 동기화된 메서드 (Thread-Safe Singleton with Synchronization)


**설명**:

- `getInstance()` 메서드에 `synchronized`를 추가해 스레드 안전성을 보장한다.
- 동시에 여러 스레드가 호출할 때 인스턴스 생성이 중복되지 않도록 한다.

**코드 예시**:



{% raw %}
```java
public class Singleton {
    private static Singleton instance;

    private Singleton() {
        // Private constructor to prevent instantiation
    }

    public static synchronized Singleton getInstance() {
        if (instance == null) {
            instance = new Singleton();
        }
        return instance;
    }
}
```
{% endraw %}



**장점**:

- 스레드 안전성이 보장된다.

**단점**:

- 매 호출마다 동기화가 필요해 성능이 저하될 수 있다.

#### 3. 이른 초기화 (Eager Initialization)


**설명**:

- 클래스 로딩 시점에 인스턴스를 미리 생성한다.
- 초기화가 지연되지 않고 클래스 로딩 시점에 즉시 이루어진다.

**코드 예시**:



{% raw %}
```java
public class Singleton {
    private static final Singleton instance = new Singleton();

    private Singleton() {
        // Private constructor to prevent instantiation
    }

    public static Singleton getInstance() {
        return instance;
    }
}
```
{% endraw %}



**장점**:

- 인스턴스가 클래스 로딩 시점에 생성되므로 스레드 안전하다.

**단점**:

- 필요하지 않을 때도 메모리를 사용하므로 비효율적일 수 있다.

#### 4. 정적 내부 클래스 (Bill Pugh Singleton Design)


**설명**:

- 정적 내부 클래스를 사용해 지연 초기화한다.
- `SingletonHelper` 클래스가 실제로 사용될 때만 로딩된다.

**코드 예시**:



{% raw %}
```java
public class Singleton {
    private Singleton() {
        // Private constructor to prevent instantiation
    }

    private static class SingletonHelper {
        private static final Singleton INSTANCE = new Singleton();
    }

    public static Singleton getInstance() {
        return SingletonHelper.INSTANCE;
    }
}
```
{% endraw %}



**장점**:

- 지연 초기화와 스레드 안전성을 동시에 보장한다. 성능이 좋고 메모리 사용이 효율적이다.

**단점**:

- 정적 내부 클래스의 사용에 대한 이해가 필요하다.

**면접에서 자주 나오는 질문과 답변 포인트**:

1. **싱글톤 패턴이 필요한 이유는?**
	- 특정 클래스의 인스턴스가 오직 하나만 있어야 할 때 사용한다. 예를 들어 데이터베이스 연결이나 로그 기록과 같은 경우에 적합하다.
2. **싱글톤 패턴의 장점은?**
	- **전역 접근**: 인스턴스에 전역적으로 접근할 수 있다.
	- **자원 절약**: 인스턴스가 하나만 생성되므로 메모리와 자원을 절약할 수 있다.
	- **통일된 접근**: 애플리케이션 전역에서 통일된 방법으로 인스턴스에 접근할 수 있다.
3. **싱글톤 패턴의 단점은?**
	- **테스트 어려움**: 싱글톤 인스턴스가 전역적으로 존재하므로 단위 테스트 시 의존성 주입이 어려울 수 있다.
	- **확장성 문제**: 하나의 인스턴스만을 사용하므로 다중 스레드 환경에서 확장성 문제를 일으킬 수 있다.
4. **스레드 안전한 싱글톤 구현 방법은?**
	- **동기화**: `synchronized` 키워드를 사용하여 스레드 안전성을 보장할 수 있다.
	- **정적 내부 클래스**: JVM의 클래스 로딩 메커니즘을 활용하여 스레드 안전성과 성능을 개선할 수 있다.
5. **정적 내부 클래스 방식의 장점은?**
	- **지연 초기화**: `SingletonHelper` 클래스가 실제로 사용될 때까지 로딩되지 않으므로 지연 초기화가 가능하다.
	- **스레드 안전성**: JVM이 클래스 로딩을 스레드 안전하게 처리하므로 스레드 안전성을 보장한다.
6. **싱글톤 패턴과 싱글톤 객체의 메모리 문제는?**
	- 싱글톤 패턴은 메모리 자원을 적게 사용하지만, 전역 상태를 유지하므로 객체가 오래 살아남으면 메모리 누수 문제가 발생할 수 있다.

**면접 팁**:

- **구현 방법**: 다양한 싱글톤 패턴 구현 방법을 이해하고 각 방법의 장단점을 명확히 설명할 수 있어야 한다.
- **실제 사례**: 실제 프로젝트에서 싱글톤 패턴을 어떻게 사용했는지 구체적인 사례를 준비하는 것이 좋다.
- **문제 해결**: 싱글톤 패턴의 단점과 그에 대한 해결책(예: 스레드 안전성, 테스트 용이성 등)에 대해 논의할 수 있어야 한다.
- **패턴과 상황**: 싱글톤 패턴이 적합한 상황과 그렇지 않은 상황을 구분하여 설명할 수 있어야 한다.

이 내용을 바탕으로 싱글톤 패턴에 대한 면접 준비를 잘 할 수 있을 것이다.

