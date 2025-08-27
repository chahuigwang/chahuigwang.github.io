---
title: 스프링 컨테이너와 스프링 빈
date: 2025-08-27 18:38:00 +0900
categories: [Spring, Spring 핵심 원리(기본편)]
tags: [spring]
---

# Spring 핵심 원리(기본편) - 스프링 컨테이너와 스프링 빈
---

- [스프링 컨테이너 생성](#스프링-컨테이너-생성)
- [컨테이너에 등록된 모든 빈 조회](#컨테이너에-등록된-모든-빈-조회)
- [스프링 빈 조회 - 기본](#스프링-빈-조회---기본)
- [스프링 빈 조회 - 동일한 타입이 둘 이상](#스프링-빈-조회---동일한-타입이-둘-이상)
- [스프링 빈 조회 - 상속 관계](#스프링-빈-조회---상속-관계)
- [BeanFactory와 ApplicationContext](#beanfactory와-applicationcontext)
- [다양한 설정 형식 지원 - 자바 코드, XML](#다양한-설정-형식-지원---자바-코드-xml)
- [스프링 빈 설정 메타 정보 - BeanDefinition](#스프링-빈-설정-메타-정보---beandefinition)

## 스프링 컨테이너 생성
```java
ApplicationContext applicationContext = new AnnotationConfigApplicationContext(AppConfig.class);
```

- `ApplicationContext` 를 스프링 컨테이너라 한다.
- `ApplicationContext` 는 인터페이스이다.

### 스프링 컨테이너의 생성 과정
![](/assets/img/posts/spring-core-basic-2-1.png)
- `new AnnotationConfigApplicationContext(AppConfig.class)`
- 스프링 컨테이너를 생성할 때는 구성 정보를 지정해주어야 한다.
- 여기서는 `AppConfig.class` 를 구성 정보로 지정했다.

![](/assets/img/posts/spring-core-basic-2-2.png)
- 스프링 컨테이너는 파라미터로 넘어온 설정 클래스 정보를 사용해서 스프링 빈을 등록한다.

**빈 이름**
- 빈 이름은 메서드 이름을 사용한다.
- 빈 이름을 직접 부여할 수도 있다.
  - `@Bean(name="memberService2")`

![](/assets/img/posts/spring-core-basic-2-3.png)

![](/assets/img/posts/spring-core-basic-2-4.png)
- 스프링 컨테이너는 설정 정보를 참고해서 의존관계를 주입(DI)한다.

## 컨테이너에 등록된 모든 빈 조회
- 모든 빈 출력하기
  - `ac.getBeanDefinitionNames()` : 스프링에 등록된 모든 빈 이름을 조회한다.
  - `ac.getBean()` : 빈 이름으로 빈 객체(인스턴스)를 조회한다.
- `beanDefinition.getRole()`
  - `ROLE_APPLICATION` : 일반적으로 사용자가 정의한 빈
  - `ROLE_INFRASTRUCTURE` : 스프링이 내부에서 사용하는 빈

## 스프링 빈 조회 - 기본
스프링 컨테이너에서 스프링 빈을 찾는 가장 기본적인 조회 방법
- `ac.getBean(빈이름, 타입)`
- `ac.getBean(타입)`

## 스프링 빈 조회 - 동일한 타입이 둘 이상
- 타입으로 조회시 같은 타입의 스프링 빈이 둘 이상이면 오류가 발생한다. 이때는 빈 이름을 지정하자.
- `ac.getBeansOfType()` 을 사용하면 해당 타입의 모든 빈을 조회할 수 있다.

## 스프링 빈 조회 - 상속 관계
- 부모 타입으로 조회하면 자식 타입도 함께 조회한다.
> 모든 자바 객체의 최고 부모인 `Object` 타입으로 조회하면, 모든 스프링 빈을 조회한다.

![](/assets/img/posts/spring-core-basic-2-5.png)

## BeanFactory와 ApplicationContext
**BeanFactory**
- 스프링 컨테이너의 최상위 인터페이스다.
- 스프링 빈을 관리하고 조회하는 역할을 담당한다.
- `getBean()` 을 제공한다.
- 지금까지 사용한 대부분의 기능은 BeanFactory가 제공하는 기능이다.

**ApplicationContext**
- BeanFactory 기능을 모두 상속받아서 제공한다.
- 빈을 관리하고 조회하는 기능은 물론, 수 많은 부가기능을 제공한다.

**ApplicatonContext가 제공하는 부가기능**
![](/assets/img/posts/spring-core-basic-2-6.png)
- **메시지소스를 활용한 국제화 기능**
  - 예를 들어서 한국에서 들어오면 한국어로, 영어권에서 들어오면 영어로 출력
- **환경변수**
  - 로컬, 개발, 운영등을 구분해서 처리
- **애플리케이션 이벤트**
  - 이벤트를 발행하고 구독하는 모델을 편리하게 지원
- **편리한 리소스 조회**
  - 파일, 클래스패스, 외부 등에서 리소스를 편리하게 조회

## 다양한 설정 형식 지원 - 자바 코드, XML
스프링 컨테이너는 다양한 형식의 설정 정보를 받아들일 수 있게 유연하게 설계되어 있다.
- 자바 코드, XML, Groovy 등등

![](/assets/img/posts/spring-core-basic-2-7.png)

## 스프링 빈 설정 메타 정보 - BeanDefinition
- `BeanDefinition` 을 빈 설정 메타정보라 한다.
  - `@Bean` , `<bean>` 당 각각 하나씩 메타 정보가 생성된다.
- 스프링 컨테이너는 이 메타정보를 기반으로 스프링 빈을 생성한다.
- 스프링 컨테이너는 자바 코드인지, XML인지 몰라도 된다. 오직 `BeanDefinition`만 알면 된다.

![](/assets/img/posts/spring-core-basic-2-8.png)

![](/assets/img/posts/spring-core-basic-2-9.png)

- `AnnotationConfigApplicationContext` 는 `AnnotatedBeanDefinitionReader` 를 사용해서
`AppConfig.class` 를 읽고 `BeanDefinition` 을 생성한다.
- `GenericXmlApplicationContext` 는 `XmlBeanDefinitionReader` 를 사용해서 `appConfig.xml`
설정 정보를 읽고 `BeanDefinition` 을 생성한다.
- 새로운 형식의 설정 정보가 추가되면, XxxBeanDefinitionReader를 만들어서 `BeanDefinition` 을 생성하
면 된다.