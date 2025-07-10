---
title: Java - final
date: 2025-02-14 19:38:00 +0900
categories: [Programming Languages, Java]
tags: [java]
---

# final - 마지막의, 변경될 수 없는
---
- final은 '마지막의', 또는 '변경될 수 없는(immutable)'의 의미를 가지고있다.
- 변수에 사용되면 값을 변경할 수 없는 상수가 된다.
> final은 클래스, 메소드에도 사용 가능하다.
- final이 붙은 변수는 상수이므로 일반적으로 선언과 동시에 초기화
- __클래스의 멤버변수인 경우 생성자를 통해 초기화 가능__

## final과 DI(Dependency Injection, 의존성 주입)
- 클래스의 멤버변수로 객체(인스턴스를) 가지는 경우, 이를 final로 선언하면 의존성 주입을 보장할 수 있다.
- 필드가 final이면 반드시 생성자에서 초기화 해야하기 때문   

`Example`
```java
@Controller
public class MemberController {

    private final MemberService memberService;  // final 사용

    @Autowired
    public MemberController(MemberService memberService) {
        this.memberService = memberService;
    }
}
```