---
layout: post
date: 2024-08-19
title: "[Spring] AOP, Filter, Interceptor 차이"
tags: [Spring, Filter, Interceptor, AOP, ]
categories: [Spring, ]
---


### **1. AOP(Aspect-Oriented Programming)**


#### **목적**

- **AOP**는 애플리케이션의 비즈니스 로직과 관련된 **횡단 관심사**(로깅, 트랜잭션 관리, 보안)를 모듈화하기 위해 사용된다. 예를 들어, 여러 서비스 메서드에서 공통적으로 필요한 로깅이나 트랜잭션 관리 같은 기능을 한 곳에서 관리할 수 있도록 한다.

#### **적용 범위**

- **메서드 수준**에서 주로 동작한다. 특정 메서드 호출 전후 또는 예외가 발생했을 때 실행되는 로직을 정의할 수 있다.
- **위치**: 인터셉터 이후, 컨트롤러가 실행된 후 비즈니스 로직이 호출될 때 작동한다.

#### **기술적 구현**

- **Aspect**: 관심사를 모듈화한 코드 블록으로, 주로 `@Aspect` 어노테이션을 사용해 정의한다.
- **Advice**: 실제로 실행되는 코드로, 메서드 호출 전(`@Before`), 후(`@After`), 또는 메서드 호출 시(`@Around`)에 실행될 수 있다.
- **Pointcut**: AOP가 적용될 지점을 정의하는 표현식으로, 특정 클래스나 메서드에 대해 적용할 수 있다.
- **프록시 패턴**을 이용해 메서드 호출을 가로채고, 그 전후에 추가 로직을 삽입한다.

#### **사용 예시**

- 트랜잭션 관리 (`@Transactional`)
- 로깅 (`@Before`, `@After` 어노테이션으로 메서드 호출 전후에 로그를 남김)
- 보안 (`@PreAuthorize` 어노테이션으로 권한 체크)

#### **2. Filter(필터)**


#### **목적**

- **Filter**는 **서블릿 요청/응답의 전후**에 실행되며, 주로 **요청을 가로채어** 전처리하거나 응답을 가공하는 데 사용된다. 예를 들어, 인코딩 설정, 보안 검증, 요청 로깅 등이 필터에서 처리될 수 있다.

#### **적용 범위**

- **HTTP 요청 수준**에서 동작해. 웹 애플리케이션 전반에 걸쳐 특정 URL 패턴에 대해 적용할 수 있다.
- **서블릿 컨테이너**에서 실행되는 구조로, 컨트롤러가 호출되기 전과 후에 요청과 응답을 필터링한다.
- 요청의 가장 첫 번째 단계에서 작동하고, 응답의 마지막 단계에서 작동한다. 주로 요청 전처리, 응답 후처리를 수행한다.

#### **기술적 구현**

- `javax.servlet.Filter` 인터페이스를 구현해서 사용한다.
- **doFilter** 메서드에서 요청 전처리와 후처리를 정의한다.
- 필터는 주로 `web.xml` 또는 `@WebFilter` 어노테이션을 통해 설정된다.

#### **사용 예시**

- 요청 인코딩 처리
- CORS 설정
- 보안 검증 (예: JWT 토큰 인증)

#### **예시 코드**



{% raw %}
```java
@WebFilter(urlPatterns = "/*")
public class MyFilter implements Filter {

    @Override
    public void doFilter(ServletRequest request, ServletResponse response, FilterChain chain)
            throws IOException, ServletException {
        System.out.println("Request received at Filter");
        chain.doFilter(request, response); // 다음 필터 또는 서블릿으로 요청을 넘김
        System.out.println("Response sent from Filter");
    }
}
```
{% endraw %}



#### **3. Interceptor(인터셉터)**


#### **목적**

- **Interceptor**는 **Spring MVC**에서 컨트롤러로 가는 요청을 가로채고, 그 전후에 추가 로직을 수행하는 데 사용돼. 주로 **인증, 권한 검사, 로깅** 등을 처리할 때 사용한다.

#### **적용 범위**

- **컨트롤러 수준**에서 동작한다. 특정 URL 패턴이나 요청에 대해 컨트롤러 호출 전후에 로직을 삽입할 수 있다.
- 필터 다음에 위치하며, 컨트롤러가 호출되기 전에 동작하고, 컨트롤러 메서드가 실행된 후에 동작한다.

#### **기술적 구현**

- `HandlerInterceptor` 인터페이스를 구현해서 사용한다.
- 세 가지 메서드를 제공한다:
	- **preHandle**: 컨트롤러의 메서드가 실행되기 전에 호출된다.
	- **postHandle**: 컨트롤러의 메서드가 실행된 후, 뷰가 렌더링되기 전에 호출된다.
	- **afterCompletion**: 뷰가 렌더링된 후에 호출된다.
- 인터셉터는 주로 `WebMvcConfigurer`를 통해 설정된다.

#### **사용 예시**

- 인증 및 권한 확인
- 로깅
- 사용자 활동 추적

#### **예시 코드**



{% raw %}
```java
public class MyInterceptor implements HandlerInterceptor {

    @Override
    public boolean preHandle(HttpServletRequest request, HttpServletResponse response, Object handler)
            throws Exception {
        System.out.println("Pre Handle method is Calling");
        return true; // true를 반환하면 컨트롤러로 요청이 전달됨
    }

    @Override
    public void postHandle(HttpServletRequest request, HttpServletResponse response, Object handler,
            ModelAndView modelAndView) throws Exception {
        System.out.println("Post Handle method is Calling");
    }

    @Override
    public void afterCompletion(HttpServletRequest request, HttpServletResponse response, Object handler, Exception ex)
            throws Exception {
        System.out.println("Request and Response is completed");
    }
}
```
{% endraw %}



#### **요청 처리 흐름**

1. **HTTP 요청**이 들어오면 먼저 **Filter**가 작동한다. 이 단계에서 인증이나 인코딩 처리, CORS 설정 같은 작업이 이루어진다.
2. 그다음, **Interceptor**가 동작한다. 요청이 컨트롤러에 도달하기 전이나 후에 인증, 권한 검사, 로깅 같은 작업을 수행한다.
3. 마지막으로, 컨트롤러가 비즈니스 로직을 실행할 때 **AOP**가 작동해서 메서드 호출 전후에 로깅, 트랜잭션 관리 등을 수행한다.
