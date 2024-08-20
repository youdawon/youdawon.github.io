---
layout: post
date: 2024-08-20
title: "[Design Pattern] Iterator Pattern"
tags: [Design Pattern, Iterator Pattern, ]
categories: [Design Pattern, ]
---


**이터레이터 패턴**은 실제 소프트웨어 개발에서 매우 자주 사용되는 패턴이다. 특히, 다양한 컬렉션(리스트, 집합, 맵 등)을 순회하는 작업에서 이터레이터 패턴이 자연스럽게 적용된다.


#### **1. Java 컬렉션 프레임워크**


Java의 **컬렉션 프레임워크**에서 이터레이터 패턴이 많이 사용된다. `List`, `Set`, `Map`과 같은 컬렉션들은 `Iterator` 인터페이스를 통해 요소를 순회할 수 있다. `for-each` 구문이나 `Iterator` 인터페이스를 직접 사용하는 경우 모두 이터레이터 패턴의 사용 사례이다.


#### **예시**



{% raw %}
```java
List<String> list = new ArrayList<>();
list.add("Item 1");
list.add("Item 2");
list.add("Item 3");

Iterator<String> iterator = list.iterator();
while (iterator.hasNext()) {
    System.out.println(iterator.next());
}
```
{% endraw %}



이 코드에서 `iterator()` 메서드는 `Iterator` 객체를 반환하고, 이를 통해 `List`의 요소들을 순차적으로 접근할 수 있다. `hasNext()`와 `next()` 메서드를 사용해서 요소를 하나씩 처리할 수 있는 구조가 바로 이터레이터 패턴이다.


#### **2. 데이터베이스 커서 (Cursor)**


데이터베이스에서 **커서(Cursor)**를 사용해 결과 집합을 순회하는 것도 이터레이터 패턴의 일종이다. 커서는 SQL 쿼리의 결과를 한 줄씩 처리할 수 있도록 해주는 메커니즘인데, 이 과정에서 이터레이터 패턴이 적용된다.


#### **예시**



{% raw %}
```java
ResultSet resultSet = statement.executeQuery("SELECT * FROM users");
while (resultSet.next()) {
    String name = resultSet.getString("name");
    System.out.println(name);
}
```
{% endraw %}



여기서 `ResultSet` 객체는 데이터베이스의 결과 집합을 순차적으로 접근할 수 있도록 도와준다. `next()` 메서드를 사용해 다음 레코드로 이동하면서 데이터를 처리하는 구조는 이터레이터 패턴을 기반으로 하고 있다.


#### **3. XML/JSON 파싱**


XML이나 JSON 데이터를 파싱할 때도 이터레이터 패턴이 사용된다. SAX(단순 API for XML) 파서나 JSON 파서는 데이터를 스트림으로 읽어들이면서 이터레이터 패턴을 사용해 요소를 순차적으로 처리한다.


#### **예시 (XML 파싱)**



{% raw %}
```java
XMLStreamReader reader = XMLInputFactory.newInstance().createXMLStreamReader(new FileInputStream("data.xml"));
while (reader.hasNext()) {
    int event = reader.next();
    if (event == XMLStreamConstants.START_ELEMENT) {
        System.out.println("Start Element: " + reader.getLocalName());
    }
}
```
{% endraw %}



SAX 파서나 StAX 파서에서 `hasNext()`와 `next()` 메서드를 사용해 XML의 각 요소를 순차적으로 읽어들이는 방식도 이터레이터 패턴의 적용 사례이다.


#### **4. 프레임워크 및 라이브러리에서의 사용**


많은 프레임워크와 라이브러리에서 이터레이터 패턴이 널리 사용된다. 예를 들어:

- **Spring Data JPA**: 쿼리 결과를 순차적으로 처리할 때.
- **Hibernate**: 데이터베이스 엔티티를 순차적으로 조회할 때.
- **Apache Commons Collections**: 다양한 컬렉션을 순회할 때.

이들 프레임워크는 내부적으로 이터레이터 패턴을 활용해 개발자가 일관된 방식으로 데이터를 처리할 수 있도록 해준다.

