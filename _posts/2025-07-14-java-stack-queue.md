---
title: Java - Stack & Queue
date: 2025-07-13 20:40:00 +0900
categories: [Programming Languages, Java]
tags: [java]
---

# Stack & Queue
---
## Stack
### Stack 객체 생성
```java
Stack<E> stack = new Stack<E>();
```

### Stack 주요 메소드
- push(E item) : 주어진 객체를 스택에 넣는다.
- peek() : 스택의 맨 위 객체를 가져온다.(객체를 스택에서 제거하지 않는다.)
- pop() : 스택의 맨 위 객체를 가져온다.(객체를 스택에서 제거한다.)

---
## Queue
### Queue 객체 생성
```java
Queue<E> queue = new LinkedList<E>();
```

### Queue
- offer(E e) : 주어진 객체를 넣는다.
- peek() : 객체 하나를 가져온다.(객체를 큐에서 제거하지 않는다.)
- poll() : 객체 하나를 가져온다.(객체를 큐에서 제거한다.)