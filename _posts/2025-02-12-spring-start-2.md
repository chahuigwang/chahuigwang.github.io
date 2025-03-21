---
title: 백엔드 개발
date: 2025-02-12 21:37:00 +0900
categories: [Spring, Spring 입문]
tags: [spring]
image: /assets/img/posts/spring-start-2-1-cropped.png
---

# Spring 입문 - 백엔드 개발
---
### 일반적인 웹 애플리케이션 계층 구조
![](/assets/img/posts/spring-start-2-1.png)
- 컨트롤러: 웹 MVC의 컨트롤러 역할
- 서비스: 핵심 비즈니스 로직 구현
- 리포지토리: 데이터베이스에 접근, 도메인 객체를 DB에 저장하고 관리
- 도메인: 비즈니스 도메인 객체, 예) 회원, 주문, 쿠폰 등등 주로 데이터베이스에 저장하고 관리됨

## 테스트 케이스 작성
- 개발한 기능을 실행해서 테스트 할 때 자바의 main 메서드를 통해서 실행하거나, 웹 애플리케이션의 컨트롤러를 통해
서 해당 기능을 실행한다. 이러한 방법은 준비하고 실행하는데 오래 걸리고, 반복 실행하기 어렵고 여러 테스트를 한번
에 실행하기 어렵다는 단점이 있다. 자바는 JUnit이라는 프레임워크로 테스트를 실행해서 이러한 문제를 해결한다.
- `src/test/java` 하위 폴더에 생성
- 클래스명: 일반적으로 `"테스트할 클래스명 + Test"`으로 작성 ex) `MemoryMemberRepositoryTest`
- @Test - 테스트할 메소드 정의
- @BeforeEach - 각 테스트 실행 전에 호출된다.
- @AfterEach - 각 테스트 실행 후에 호출된다.