---
layout: post
date: 2024-08-19
title: "[Design Pattern] Observer Pattern"
tags: [Design Pattern, Observer Pattern, ]
categories: [Design Pattern, ]
---


**옵저버 패턴(Observer Pattern)**은 객체 지향 설계에서 많이 사용되는 디자인 패턴 중 하나로, **일대다(one-to-many)** 의존성을 정의하는 패턴이다. 이 패턴을 통해 하나의 객체(주제, Subject)의 상태가 변경될 때, 그 상태 변화를 여러 다른 객체(옵저버, Observer)에게 자동으로 통지하고, 이들 옵저버가 그에 따라 동작할 수 있게 한다.


#### **핵심 개념**

- **Subject (주제)**: 상태를 가지고 있는 객체이다. 이 객체의 상태가 변경될 때, 옵저버들에게 그 변화를 통지하는 역할을 한다.
- **Observer (옵저버)**: 주제의 상태 변화를 감지하고, 그에 따라 동작을 수행하는 객체이다. 옵저버는 주제에 등록되어 있으며, 주제가 상태를 변경하면 이를 통지받는다.

#### **동작 방식**

1. **등록(Attach)**: 옵저버가 주제에 자신을 등록한다. 주제는 자신을 관찰하는 옵저버들의 목록을 관리한다.
2. **상태 변경**: 주제의 상태가 변경되면, 주제는 자신에게 등록된 모든 옵저버들에게 그 변화를 통지한다.
3. **통지(Notification)**: 옵저버는 주제로부터 상태 변경 통지를 받으면, 그에 따라 자신의 상태를 업데이트하거나, 필요한 동작을 수행한다.

#### **구조**

1. **Subject 인터페이스/클래스**: 옵저버들을 관리하며, 상태 변화 시 통지하는 메서드를 정의한다.
2. **ConcreteSubject 클래스**: 실제로 상태를 관리하고, 상태가 변경될 때 옵저버들에게 통지하는 구체적인 주제 클래스이다.
3. **Observer 인터페이스/클래스**: 주제의 상태 변화를 감지하고, 그에 따라 동작을 수행하는 메서드를 정의한다.
4. **ConcreteObserver 클래스**: 주제로부터 통지를 받고, 상태 변화에 따라 동작을 수행하는 구체적인 옵저버 클래스이다.

#### **예제 코드 (Java)**



{% raw %}
```java
// 옵저버 인터페이스
public interface Observer {
    void update(int state);
}

// 주제(Subject) 인터페이스
public interface Subject {
    void registerObserver(Observer observer);
    void removeObserver(Observer observer);
    void notifyObservers();
}

// 구체적인 주제(ConcreteSubject)
public class ConcreteSubject implements Subject {
    private List<Observer> observers = new ArrayList<>();
    private int state;

    public int getState() {
        return state;
    }

    public void setState(int state) {
        this.state = state;
        notifyObservers(); // 상태 변경 시 모든 옵저버에게 알림
    }

    @Override
    public void registerObserver(Observer observer) {
        observers.add(observer);
    }

    @Override
    public void removeObserver(Observer observer) {
        observers.remove(observer);
    }

    @Override
    public void notifyObservers() {
        for (Observer observer : observers) {
            observer.update(state); // 각 옵저버에게 상태 전달
        }
    }
}

// 구체적인 옵저버(ConcreteObserver)
public class ConcreteObserver implements Observer {
    private String name;

    public ConcreteObserver(String name) {
        this.name = name;
    }

    @Override
    public void update(int state) {
        System.out.println(name + " received update: State is now " + state);
    }
}

// 클라이언트 코드
public class Main {
    public static void main(String[] args) {
        ConcreteSubject subject = new ConcreteSubject();

        ConcreteObserver observer1 = new ConcreteObserver("Observer 1");
        ConcreteObserver observer2 = new ConcreteObserver("Observer 2");

        subject.registerObserver(observer1);
        subject.registerObserver(observer2);

        subject.setState(10); // 옵저버들에게 상태 변경 통지
        subject.setState(20); // 또다시 상태 변경 통지
    }
}
```
{% endraw %}



#### **실행 결과**



{% raw %}
```text
Observer 1 received update: State is now 10
Observer 2 received update: State is now 10
Observer 1 received update: State is now 20
Observer 2 received update: State is now 20
```
{% endraw %}



#### **사용 사례**

- **GUI 애플리케이션**: 버튼 클릭, 텍스트 입력 등 사용자 이벤트를 처리할 때 옵저버 패턴이 자주 사용된다.
- **모델-뷰-컨트롤러(MVC)**: 모델의 상태가 변경될 때 뷰가 이를 감지하고 업데이트하는 구조에서 옵저버 패턴이 사용된다.
- **이벤트 기반 시스템**: 주식 가격, 날씨 정보 등 실시간 데이터를 감지하고 처리하는 시스템에서 사용된다.

#### **장점**

- **느슨한 결합**: 주제와 옵저버 간의 결합도를 낮춰, 시스템의 유지보수성을 높인다.
- **자동 업데이트**: 주제의 상태가 변경될 때, 옵저버들이 자동으로 업데이트되므로 일관된 상태를 유지할 수 있다.

#### **단점**

- **복잡성 증가**: 옵저버가 많아질수록 시스템의 복잡도가 증가할 수 있다.
- **순환 참조**: 잘못된 설계로 인해 주제와 옵저버 간의 순환 참조가 발생할 수 있다.
