---
layout: post
date: 2024-08-19
title: "[Design Pattern] Proxy Pattern"
tags: [Design Pattern, Proxy Pattern, ]
categories: [Design Pattern, ]
---


**프록시 패턴(Proxy Pattern)**은 **구조적 디자인 패턴** 중 하나로, 다른 객체에 대한 접근을 제어하기 위해 대리자(Proxy)를 사용하는 패턴이다. 프록시 객체는 원래 객체(Real Subject)로의 접근을 제어하거나, 추가적인 기능을 제공할 수 있다. 프록시 패턴은 원래 객체의 대리자 역할을 하며, 원래 객체를 대신해 요청을 처리하거나, 요청 전후에 추가 작업을 수행할 수 있다.


#### **프록시 패턴의 주요 개념**

1. **Subject 인터페이스**:
	- 원래 객체와 프록시 객체가 공통으로 구현하는 인터페이스이다. 클라이언트는 이 인터페이스를 통해 원래 객체든 프록시 객체든 동일한 방식으로 사용할 수 있다.
2. **Real Subject (실제 객체)**:
	- 프록시 패턴에서 실제로 작업을 수행하는 객체이다. 프록시 객체는 이 객체에 대한 접근을 제어한다.
3. **Proxy (프록시 객체)**:
	- Real Subject에 대한 접근을 제어하거나, 요청 전후에 추가적인 작업을 수행하는 대리 객체이다. 프록시 객체는 Subject 인터페이스를 구현하여 Real Subject와 동일한 방식으로 사용될 수 있다.

#### **프록시 패턴의 종류**

1. **가상 프록시 (Virtual Proxy)**:
	- 실제 객체의 생성 비용이 클 경우, 실제 객체를 미리 생성하지 않고, 필요할 때 생성하여 사용할 수 있도록 하는 프록시. 예를 들어, 대용량 데이터를 다루는 객체를 미리 생성하지 않고, 실제로 필요할 때 생성하는 방식이다.
2. **원격 프록시 (Remote Proxy)**:
	- 원격 서버에 있는 객체에 대한 접근을 로컬에서 제어할 수 있도록 하는 프록시이다. 예를 들어, 클라이언트가 원격 서비스에 접근할 때, 원격 프록시가 중간에서 통신을 관리한다.
3. **보호 프록시 (Protection Proxy)**:
	- 객체에 대한 접근을 제어하여, 접근 권한이 있는지 확인하는 기능을 제공하는 프록시이다. 예를 들어, 특정 사용자만 접근할 수 있는 기능에 대해 보호 프록시가 접근 권한을 확인한다.

#### **프록시 패턴의 구조**



{% raw %}
```java
// Subject 인터페이스
public interface Subject {
    void request();
}

// RealSubject 클래스 (실제 객체)
public class RealSubject implements Subject {
    @Override
    public void request() {
        System.out.println("RealSubject: Handling request.");
    }
}

// Proxy 클래스 (프록시 객체)
public class Proxy implements Subject {
    private RealSubject realSubject;

    @Override
    public void request() {
        if (realSubject == null) {
            realSubject = new RealSubject(); // 실제 객체의 생성을 지연시킴
        }
        System.out.println("Proxy: Logging before handling request.");
        realSubject.request();
        System.out.println("Proxy: Logging after handling request.");
    }
}

// 클라이언트 코드
public class Client {
    public static void main(String[] args) {
        Subject proxy = new Proxy();
        proxy.request(); // 프록시를 통해 실제 객체에 접근
    }
}
```
{% endraw %}



#### **실행 결과**



{% raw %}
```text
Proxy: Logging before handling request.
RealSubject: Handling request.
Proxy: Logging after handling request.
```
{% endraw %}



#### **코드 설명**

- **Subject 인터페이스**: 클라이언트는 이 인터페이스를 통해 실제 객체든 프록시 객체든 동일한 방식으로 접근할 수 있다.
- **RealSubject**: 실제로 작업을 수행하는 객체이다.
- **Proxy**: RealSubject에 대한 접근을 제어한다. 이 예제에서는 실제 객체를 미리 생성하지 않고, 요청이 있을 때만 생성하여 작업을 수행하도록 한다. 또한 요청 전후에 로깅 기능을 추가하여, 부가적인 작업을 수행한다.

#### **프록시 패턴의 사용 사례**

1. **지연 초기화(Lazy Initialization)**: 객체의 생성 비용이 클 때, 실제 객체를 필요할 때만 생성하여 시스템 리소스를 효율적으로 관리할 수 있다.
2. **접근 제어**: 특정 객체에 대한 접근을 제한하거나, 접근 권한을 관리하는 경우 사용할 수 있다.
3. **원격 접근**: 원격 서버의 객체에 접근할 때, 프록시를 통해 통신을 관리할 수 있다.
4. **로깅 및 감사(Auditing)**: 객체의 메서드 호출 전후에 로깅이나 감사 기록을 남기는 경우 사용할 수 있다.

#### **장점**

- **객체 생성의 지연**: 실제 객체의 생성이 지연되기 때문에, 시스템 리소스를 효율적으로 사용할 수 있다.
- **접근 제어**: 객체에 대한 접근을 중앙에서 관리할 수 있어 보안성을 높일 수 있다.
- **추가 기능 제공**: 객체의 메서드 호출 전후에 추가적인 작업을 수행할 수 있다.

#### **단점**

- **복잡성 증가**: 프록시 객체를 추가함으로써 시스템의 구조가 복잡해질 수 있다.
- **성능 저하**: 프록시 객체가 실제 객체에 대한 추가적인 작업을 수행하기 때문에, 약간의 성능 저하가 발생할 수 있다.
