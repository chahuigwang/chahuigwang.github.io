---
title: Java - static
date: 2025-07-09 19:38:00 +0900
categories: [Programming Languages, Java]
tags: [java]
---

# static - 클래스의, 공통적인
---
- static은 '클래스의' 또는 '공통적인'의 의미를 가지고있다.
- 인스턴스 변수는 하나의 클래스로부터 생성되었더라도 각기 다른 값을 유지하지만
- 클래스 변수(static 멤버변수)는 인스턴스와 관계없이 같은 값을 가진다.
- 하나의 변수를 모든 인스턴스가 공유하기 때문

> static은 멤버변수 뿐만 아니라 메소드에도 사용 가능하다.
>> - static메소드 내에서는 인스턴스 변수(static이 아닌 멤버변수) 사용 불가
>> - 인스턴스 변수를 사용하지 않는 메소드는 static메소드로 선언하는 것을 고려해볼 수 있다.
