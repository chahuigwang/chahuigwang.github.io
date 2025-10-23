---
title: Java - Lambda
date: 2025-10-24 00:58:00 +0900
categories: [Programming Languages, Java]
tags: [java]
---

# 람다(Lambda)
---

## 람다식(Lambda Expression)이란?
람다식은 하나의 메서드만 가진 함수형 인터페이스(Functional Interface)를 간단히 표현하는 문법이다

> 람다식은 다른 말로 익명 메소드라고도 한다.

`new 인터페이스() { ... }` 이러한 함수형 인터페이스를 구현하는 익명 클래스(anonymous class)의 객체를 짧고 간결하게 표현하는 방법이다.

### 기본 문법
```java
(매개변수목록) -> {실행문}
```

### 예시(Thread)
- 쓰레드를 만들때 사용하는 Runnable 인터페이스의 경우 run()메소드를 하나만 가지고 있다.
- Runnable을 이용하여 쓰레드를 만드는 방법  

```java
public class LambdaExam {

    public static void main(String[] args) {
        new Thread(new Runnable() {
            
            @Override
            public void run() {
            for (int i = 0; i < 10; i++){
                System.out.println("hello");
            }
        }}).start();
    }   
}
```
- 쓰레드가 실행되면 쓰레드 생성자 안에 넣은 run()메소드가 실행된다.
- 자바는 메소드만 매개변수로 전달할 방법이 없다. 인스턴스만 전달 할 수 있다.
- 그렇기때문에 run()메소드를 가지고 있는 Runnable객체를 만들어서 전달한다.  

- **람다식을 이용해서 수정한 코드**

```java
public class LambdaExam {

    public static void main(String[] args) {
        new Thread(() -> {
            for (int i = 0; i < 10; i++){
                System.out.println("hello");
            }
        }).start();
    }   
}
```
- ()->{ ..... } 부분이 람다식, 다른말로 익명 메소드
- JVM은 Thread 생성자를 보고 `() -> {}` 이 무엇인지 대상을 추론한다.
- JVM은 Thread 생성자가 Runnable 인터페이스를 구현한 것이 와야하는 것을 알게 되고, 람다식을 Runnable을 구현하는 객체로 자동으로 만들어서 매개변수로 넣어준다.