---
title: Java - Stream
date: 2025-10-27 22:11:00 +0900
categories: [Programming Languages, Java]
tags: [java]
---

# 스트림(Stream)
---
## **스트림이란?**
- 스트림은 컬렉션(Collection) 데이터를 반복문 없이 함수형(선언형) 방식으로 처리할 수 있도록 지원하는 데이터 처리 흐름이다.
- 스트림은 데이터 소스를 추상화하고, 데이터를 다루는 데 자주 사요되는 메서드들을 정의해 놓았다.

> 데이터 소스를 추상화하였다는 것은, 데이터 소스가 무엇이든 간에 같은 방식으로 다룰 수 있게 되었다는 것과 코드의 재사용성이 높아진다는 것을 의미한다.
{: .prompt-tip}

### 스트림 특징
- 스트림은 데이터 소스를 변경하지 않는다.
- 스트림은 일회용이다.
- 스트림은 작업을 내부 반복으로 처리한다.

### 스트림의 연산
- 중간 연산 : 연산 결과과 스트림인 연산, 스트림에 연속해서 중간 연산할 수 있음  
  ![](/assets/img/posts/스트림1.png)

- 최종 연산 : 연산 결과가 스트림이 아닌 연산, 스트림의 요소를 소모하므로 단 한번만 가능  
  ![](/assets/img/posts/스트림2.png)

### Stream&lt;Integer&gt;와 IntStream
- 요소의 타입이 T인 스트림은 기본적으로 Steram&lt;T&gt; 이지만, 오토박싱&언박싱으로 인한 비효율을 줄이기 위해 데이터 소스의 요소를 기본형으로 다루는 스트림, IntStream, LongStream, DoubleStream이 제공된다.
- 일반적으로 Stream&lt;Integer&gt; 대신 IntStream 을 사용하는 것이 더 효율적이고, IntStream에는 int타입의 값으로 작업하는 데 유횽한 메서드들이 포함되어 있다.

## **스트림 만들기**
- 컬렉션으 최고 조상인 Collection에 stream()이 정의되어 있다.
- 그래서 Collection의 자손인 List와 Set을 구현한 컬렉션 클래스들은 모두 이 메서드로 스트림을 생성할 수 있다.
- stream()은 해당 컬렉션을 소스로 하는 스트림을 반환한다.
  `Stream<T> Collection.stream()`

## **Optional&lt;T&gt;**
- Optional&lt;T&gt;은 제네릭 클래스로 'T 타입의 객체'를 감싸는 Wrapper 클래스이다.
- 최종 연산의 결과를 그냥 반환하는 게 아니라 Option 객체에 담아서 반환하면, 반환된 결과가 null인지 매번 if문으로 체크하는 대신 Optional에 정의된 메서드를 통해서 간단히 처리할 수 있다.

### Optional 객체 생성하기
- `Optional<T> optVal = Optional.of(T t);` - 참조변수의 값이 null일 가능성이 있을 때
- `Optional<T> optVal = Optional.ofNullable(T t);` - 참조변수의 값이 null일 가능성이 없을 때
- `Optional<T> optVal = Optional.empty();` - 값이 없을 때

### Optional 객체의 값 가져오기
- get() : 값이 있으면 반환, 없으면 NoSuchElementException
- orElse(T other) : 값이 있으면 반환, 없으면 other 반환
- orElseGet(람다) : 값이 있으면 반환, 없으면 람다식 실행 후 반환
- orElseThrow(람다) : 값이 있으면 반환, 없으면 예외 던짐

<br>
- isPresent() : 값이 없으면 false, 있으면 true 반환
- ifPresent(람다) : 값이 있으면 주어진 람다식을 실행, 없으면 아무것도 하지않음
