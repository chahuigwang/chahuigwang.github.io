---
title: Java - Generic
date: 2025-07-13 16:59:00 +0900
categories: [Programming Languages, Java]
tags: [java]
---

# 제네릭(Generic)
---

## Generic이란?
> 클래스나 메서드에서 사용할 데이터 타입을 외부에서 지정할 수 있도록 하는 자바의 문법
{: .prompt-tip }

### 제네릭의 장점
- 컴파일 시 강한 타입 체크
- 타입 변환(casting)을 제거

## 제네릭 타입(class<T>, interface<T>)
- 제네릭 타입은 타입을 파라미터로 가지는 클래스와 인터페이스를 말한다.
- 제네릭 타입은 클래스 또는 인터페이스 이름 뒤에 "<>" 부호가 붙고, 사이에 타입 파라미터가 위치한다.

```java
public class 클래스명<T> { ... }
public interface 인터페이스명<T> { ... }
```

✅ 예시 : 제네릭 타입
```java
public class Box<T> {
    private T t;
    public T get() { return t; }
    public void set(T t) { this.t = t; }
}

public class BoxExample {
    public static void main(String[] args) {
        Box<String> box = new Box<String>();
        box.set("hello");
        String str = box.get();
    }
}
```

## 멀티 타입 파라미터(class<K, V, ...>, interface<K, V, ...>)
제네릭 타입은 두 개 이상의 멀티 타입 파라미터를 사용할 수 있는데, 이 경우 각 타입 파라미터를 콤마로 구분한다.

✅ 예시 : 제네릭 클래스
```java
public class Product<T, M> {
    private T kind;
    private M model;

    public T getKind() { return this.kind; }
    public M getModel() { return this.model; }

    public void setKind(T kind) { this.kind = kind; }
    public void setModel(M model) { this.model = model; }
}
```

## 제네릭 메소드
- 제네릭 메소드는 매개 타입과 리턴 타입으로 타입 파라미터를 갖는 메소드를 말한다.
- 제네릭 메소드를 선언하는 방법은 리턴 타입 앞에 <> 기호를 추가하고 타입 파라미터를 기술한 다음, 리턴 타입과 매개 타입으로 타입 파라미터를 사용하면 된다.  
`public <타입파라미터, ...> 리턴타입 메소드명(매개변수, ...) { ... }`

```java
public <T> Box<T> boxing(T t) { ... }
```

### 제네릭 메소드 호출 방식
- `리턴타입 변수 = <구체적타입> 메소드명(매개값); // 명시적으로 구체적 타입을 지정`
- `리턴타입 변수 = 메소드명(매개값);              // 매개값을 보고 구체적 타입을 추정`

```java
Box<Integer> box = <Integer>boxing(100);
Box<Integer> box = boxing(100);
```

## 제한된 타입 파라미터(&lt;T extends 상위타입&gt;)
- 타입 파라미터에 지정되는 구체적인 타입을 제한할 필요가 있을 때 사용

> 예를 들어 숫자를 연산하는 제네릭 메소드는 매개값으로 Number 타입 또는 하위 클래스 타입(Byte, Short, Integer, Long, Double)의 인스턴스만 가져야한다.
{: .prompt-tip }

- 상위 타입은 클래스뿐만 아니라 인터페이스도 가능하다.

> 인터페이스라고 해서 implements를 사용하지 않는다.
{: .prompt-warning }

```java
public <T extends 상위타입> 리턴타입 메소드(매개변수, ...) { ... }
```

## 와일드카드 타입(<?>, <? extends ...>, <? super ...>)
코드에서 ?를 와일드카드(wildcard)라고 부른다. 제네릭 타입을 매개값이나 리턴 타입으로 사용할 때 구체적인 타입 대신에 와일드카드를 다음과 같이 세 가지 형태로 사용할 수 있다.
- `제네릭타입<?>` : Unbounded Wildcards(제한 없음)  
  타입 파리미터를 대치하는 구체적인 타입으로 모든 클래스나 인터페이스 타입이 올 수 있다.
- `제네릭타입<? extends 상위타입>` : Upper Bounded Wildcards(상위 클래스 제한)  
  타입 파리미터를 대치하는 구체적인 타입으로 상위 타입이나 하위 타입만 올 수 있다.
- `제네릭타입<? super 하위타입>` : Lower Bounded Wildcards(하위 클래스 제한)  
  타입 파리미터를 대치하는 구체적인 타입으로 하위 타입이나 상위 타입이 올 수 있다.