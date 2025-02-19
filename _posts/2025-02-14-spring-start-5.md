---
title: AOP
date: 2025-02-14 17:52:00 +0900
categories: [Spring, Spring 입문]
tags: [spring]
---

# Spring 입문 - AOP
---
## AOP
- AOP: Aspect Oriented Programming
- 공통 관심 사항(cross-cutting concern) vs 핵심 관심 사항(core concern) 분리

### AOP가 필요한 상황
- 여러 메소드에서 공통, 반복되는 기능을 적용하고 싶을 때
- ex) 모든 메소드의 호출 시간을 측정하고 싶다면?
- 문제
    - 시간을 측정하는 기능은 핵심 관심 사항이 아니다.
    - 시간을 측정하는 기능은 공통 관심 사항이다.
    - 시간을 측정하는 로직을 변경할 때 모든 로직을 찾아가면서 변경해야 한다.
    - 시간을 측정하는 로직을 별도의 공통 로직으로 만들기 어렵다.
    - 시간을 측정하는 로직과 핵심 비즈니스의 로직이 섞여서 유지보수가 어렵다.

### AOP 사용 방법
- AOP 클래스 생성
- AOP 클래스에 @Aspect 적용
- @Around -> AOP를 적용할 패키지 설정
- AOP로 동작할 메소드 정의
- 컴포넌트 스캔 or 스프링 빈 설정 클래스에서 스프링 빈으로 등록

__AOP 적용 전 의존관계__
![](/assets/img/posts/spring-start-5-2.png)

__AOP 적용 후 의존관계__
![](/assets/img/posts/spring-start-5-1.png)

- 프록시라는 가짜 객체를 생성해서 의존관계를 주입한다.
- 가짜 객체가 실행이 완료된 후 진짜 객체를 실행한다.