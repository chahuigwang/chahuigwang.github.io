---
title: 객체 지향 설계와 스프링
date: 2025-02-14 19:38:00 +0900
categories: [Spring, Spring 핵심 원리(기본편)]
tags: [spring]
---

# Spring 핵심 원리(기본편) - 객체 지향 설계와 스프링
---

## 스프링의 핵심 개념
- 스프링은 자바 언어 기반의 프레임워크
- 자바 언어의 가장 큰 특징 - __객체 지향 언어__
- 스프링은 객체 지향 언어가 가진 강력한 특징을 살려내는 프레임워크
- 스프링은 __좋은 객체 지향__ 애플리케이션을 개발할 수 있게 도와주는 프레임워크

## 객체 지향 프로그래밍(OOP)의 특징
- 추상화
- 캡슐화
- 상속
- __다형성__

### 다형성 Polymorphism
- **역할**과 **구현**으로 세상을 구분
![](/assets/img/posts/객체지향설계와스프링1.jpg)
![](/assets/img/posts/객체지향설계와스프링2.jpg)

#### 역할과 구현을 분리
- 유연하고, 변경이 용이
- 확장 가능한 설계
- 클라이언트에 영향을 주지 않는 변경 가능

### Spring과 객체 지향
- 객체 지향에서 가장 중요한 개념은 __다형성__
- 스프링은 다형성을 극대화해서 이용할 수 있게 도와준다.
- 스프링에서 이야기하는 제어의 역전(IoC), 의존관계 주입(DI)은 다형성을 활용해서 역할과 구현을 편리하게 다룰 수 있도록 지원한다.
- 스프링을 사용하면 마치 레고 블럭 조립하듯이! 공연 무대의 배우를 선택하듯이! 구현을 편리하게 변경할 수 있다.

---

# 좋은 객체 지향 설계의 5가지 원칙(SOLID)
- [SRP: 단일 책임 원칙 (Single Responsibility Principle)](#srp)
- [OCP: 개방-폐쇄 원칙 (Open/Closed Principle)](#ocp)
- [LSP: 리스코프 치환 원칙 (Liskov Substitution Principle)](#lsp)
- [ISP: 인터페이스 분리 원칙 (Interface Segregation Principle)](#isp)
- [DIP: 의존관계 역전 원칙 (Dependency Inversion Principle)](#dip)

## SRP
- 한 클래스는 하나의 책임만 가져야한다.
- 하나의 책임의 기준 → 변경
> 변경이 있을 때 파급효과가 적으면 SRP를 잘 따른 것

## OCP
- 소프트웨어 요소는 **확장에는 열려** 있으나 **변경에는 닫혀** 있어야 한다.
- 다형성을 사용해 OCP 원칙을 지킬 수 있는 지 살펴보자

```java
public class MemberService {
    private MemberRepository memberRepository = new MemoryMemberRepository();
}
```

```java
public class MemberService {
    // private MemberRepository memberRepository = new MemoryMemberRepository();
    private MemberRepository memberRepository = new JdbcMemberRepository();
}
```
> MemberService 클라이언트가 구현 클래스를 직접 선택
{: .prompt-warning}

> 구현 객체를 변경하려면 클라이언트 코드를 변경해야한다.
{: .prompt-danger}

- 다형성을 사용했지만 OCP 원칙을 지킬 수 없다.
- 객체를 생성하교 연관관계를 맺어주는 별도의 조립, 설정자가 필요하다.

## LSP
- 프로그램의 객체는 프로그램의 정확성을 깨뜨리지 않으면서 하위 타입의 인스턴스로 바꿀 수 있어야 한다.
- 다형성에서 하위 클래스는 인터페이스 규약을 다 지켜야 한다는 것
- ex) 자동차 인터페이스의 엑셀은 앞으로 가라는 기능, 뒤로 가게 구현하면 LSP 위반

## ISP
- 특정 클라이언트를 위한 인터페이스 여러 개가 범용 인터페이스 하나보다 낫다.
- 자동차 인터페이스 -> 운전 인터페이스, 정비 인터페이스로 분리
- 사용자 클라이언트 -> 운전자 클라이언트, 정비사 클라이언트로 분리

## DIP
- 프로그래머는 **"추상화에 의존해야지, 구체화에 의존하면 안된다."**
- 의존성 주입은 이 원칙을 따르는 방법 중 하나
- 쉽게 이야기해서 구현 클래스에 의존하지 말고, 인터페이스에 의존하라는 뜻
- 앞에서 이야기한 **역할**에 의존해야 한다.
- 다형성을 사용해 DIP 원칙을 지킬 수 있는 지 살펴보자

```java
public class MemberService {
    private MemberRepository memberRepository = new MemoryMemberRepository();
}
```

> DIP 위반 - MemberService는 인터페이스에 의존하지만, 구현 클래스도 동시에 의존한다.
{: .prompt-danger}

## 정리
- 객체 지향의 핵심은 다형성
- 다형성 만으로는 쉽게 부품을 갈아 끼우듯이 개발할 수 없다.
- 다형성 만으로는 구현 객체를 변경할 때 클라이언트 코드도 함께 변경된다.
- 다형성 만으로는 OCP, DIP를 지킬 수 없다.

---

# 객체 지향 설계와 스프링
- 스프링은 다음 기술로 다형성 + OCP, DIP를 가능하게 지원
    - DI(Dependency Injection): 의존관계, 의존성 주입
    - DI 컨테이너
- 순수하게 자바로 OCP, DIP 원칙들을 지키면서 개발을 해보면, 결국 스프링 프레임워크를 만들게 된다. (더 정확히는 DI 컨테이너)