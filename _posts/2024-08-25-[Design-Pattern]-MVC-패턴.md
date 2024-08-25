---
layout: post
date: 2024-08-25
title: "[Design Pattern] MVC 패턴"
tags: [Design Pattern, MVC Pattern, ]
categories: [Design Pattern, ]
---


**MVC 패턴**(Model-View-Controller Pattern)은 소프트웨어 공학에서 널리 사용되는 아키텍처 패턴으로, 사용자 인터페이스와 비즈니스 로직을 분리하여 애플리케이션을 더 모듈화하고 유지보수하기 쉽게 만드는 데 사용된다. 이 패턴은 특히 웹 애플리케이션과 같은 사용자 인터페이스 중심의 애플리케이션에서 자주 사용된다.


#### **MVC 패턴의 구성 요소**

1. **Model (모델)**
	- **역할**: 애플리케이션의 데이터와 비즈니스 로직을 관리한다. 모델은 데이터베이스에서 데이터를 가져오고, 저장하며, 수정하는 책임을 진다.
	- **특징**: 모델은 비즈니스 규칙을 구현하고, 데이터 처리 로직을 포함한다. 모델은 뷰와 컨트롤러와 독립적으로 동작하며, 데이터가 변경되면 자동으로 뷰에 통지할 수 있다.
2. **View (뷰)**
	- **역할**: 사용자 인터페이스(UI)를 담당한다. 뷰는 모델의 데이터를 받아서 사용자에게 표시한다.
	- **특징**: 뷰는 사용자가 상호작용할 수 있는 인터페이스 요소(예: HTML, CSS, JavaScript)를 포함하며, 데이터가 어떻게 표현되는지 결정한다. 뷰는 컨트롤러의 지시를 받아 화면을 갱신하거나 변경할 수 있다.
3. **Controller (컨트롤러)**
	- **역할**: 사용자의 입력을 처리하고, 모델과 뷰 사이의 상호작용을 관리한다. 컨트롤러는 사용자의 요청을 받아서 적절한 모델을 갱신하거나, 뷰를 업데이트하는 일을 수행한다.
	- **특징**: 컨트롤러는 모델과 뷰 사이의 중개자 역할을 하며, 뷰의 요청에 따라 모델의 데이터를 조작하거나, 모델의 상태에 따라 뷰를 업데이트한다.

#### **MVC 패턴의 동작 흐름**

1. **사용자 요청**: 사용자가 애플리케이션의 사용자 인터페이스(View)와 상호작용(예: 버튼 클릭, 폼 제출)하면, 이 요청은 컨트롤러(Controller)로 전달됩니다.
2. **컨트롤러 처리**: 컨트롤러는 사용자의 요청을 분석하고, 그에 따라 적절한 모델(Model)과 상호작용한다. 모델에서 데이터를 조회하거나 변경하는 작업이 이 단계에서 이루어진다.
3. **모델 업데이트**: 모델은 컨트롤러의 지시에 따라 데이터를 처리하고, 그 결과를 뷰에 반영할 준비를 한다.
4. **뷰 업데이트**: 모델에서 처리된 데이터를 기반으로 뷰(View)가 갱신되며, 변경된 화면이 사용자에게 보여진다.
5. **결과 출력**: 최종적으로 사용자는 요청의 결과를 뷰를 통해 확인할 수 있다.

#### **MVC 패턴의 장점**

- **분리된 관심사(Separation of Concerns)**: 모델, 뷰, 컨트롤러가 각기 다른 역할을 담당하여 코드의 응집도를 높이고, 모듈화를 개선합니다. 이를 통해 코드의 유지보수성과 재사용성이 높아진다.
- **유연성**: 뷰를 쉽게 변경하거나 교체할 수 있으며, 비즈니스 로직과 데이터 처리 로직을 독립적으로 관리할 수 있다.
- **테스트 용이성**: 각 컴포넌트가 분리되어 있어, 개별적으로 테스트하기 용이하다.

#### **MVC 패턴의 단점**

- **복잡성 증가**: MVC 패턴은 애플리케이션 구조를 명확하게 해주지만, 특히 소규모 프로젝트에서는 오히려 복잡성을 증가시킬 수 있다.
- **종속성 관리**: 모델과 뷰 사이의 종속성을 잘못 관리하면, 의도치 않게 서로 간섭할 수 있다.
- **과도한 설계**: 단순한 애플리케이션에서는 MVC 패턴이 불필요하게 느껴질 수 있으며, 설계가 지나치게 복잡해질 수 있다

#### **MVC 패턴의 예시 (Java)**



{% raw %}
```java
// Model
public class UserModel {
    private String name;

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }
}

// View
public class UserView {
    public void printUserDetails(String userName) {
        System.out.println("User: " + userName);
    }
}

// Controller
public class UserController {
    private UserModel model;
    private UserView view;

    public UserController(UserModel model, UserView view) {
        this.model = model;
        this.view = view;
    }

    public void setUserName(String name) {
        model.setName(name);
    }

    public String getUserName() {
        return model.getName();
    }

    public void updateView() {
        view.printUserDetails(model.getName());
    }
}

// Main Class
public class MVCPatternDemo {
    public static void main(String[] args) {
        UserModel model = new UserModel();
        UserView view = new UserView();
        UserController controller = new UserController(model, view);

        controller.setUserName("John Doe");
        controller.updateView();  // User: John Doe
    }
}
```
{% endraw %}


