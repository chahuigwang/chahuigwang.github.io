---
title: 스프링 DB 접근 기술
date: 2025-02-14 16:54:00 +0900
categories: [Spring, Spring 입문]
tags: [spring]
---

# Spring 입문 - 스프링 DB 접근 기술
---
## 순수 JDBC

### JDBC란?
JDBC(Java Database Connectivity)는 자바에서 데이터베이스에 접속할 수 있도록 하는 자바 API이다. JDBC는 데이터베이스에서 자료를 쿼리하거나 업데이트하는 방법을 제공한다.

> 최근에는 JDBC API로 직접 코딩하는 방식은 거의 쓰이지 않는다.
{: .prompt-tip}

## 스프링 JdbcTemplate
- 스프링 JdbcTemplate과 MyBatis 같은 라이브러리는 JDBC API에서 본 반복 코드를 대부분 제거해준
다.
- SQL은 직접 작성해야 한다.

## JPA
- JPA(Java Persistence API)는 자바 진영에서 ORM(Object-Relational Mapping) 기술 표준으로 사용되는 인터페이스의 모음
- JPA는 기존의 반복 코드는 물론이고, 기본적인 SQL도 JPA가 직접 만들어서 실행해준다.
- JPA를 사용하면, SQL과 데이터 중심의 설계에서 객체 중심의 설계로 패러다임을 전환을 할 수 있다.
- JPA를 사용하면 개발 생산성을 크게 높일 수 있다.

## 스프링 데이터 JPA
- 리포지토리에 구현 클래스 없이 인터페이스 만으로 개발 가능
- 인터페이스를 통한 기본적인 CRUD
- `findByName()` , `findByEmail()` 처럼 메서드 이름 만으로 조회 기능 제공
- 페이징 기능 자동 제공

> 실무에서는 JPA와 스프링 데이터 JPA를 기본으로 사용하고, 복잡한 동적 쿼리는 Querydsl이라는 라이브러리를 사용하면 된다. Querydsl을 사용하면 쿼리도 자바 코드로 안전하게 작성할 수 있고, 동적 쿼리도 편리하게 작성할 수 있다. 이 조합으로 해결하기 어려운 쿼리는 JPA가 제공하는 네이티브 쿼리를 사용하거나, 스프링 JdbcTemplate를 사용하면 된다.
{: .prompt-info}