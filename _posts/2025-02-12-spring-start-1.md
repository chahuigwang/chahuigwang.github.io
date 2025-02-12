---
title: Spring 웹 개발 기초
date: 2025-02-12 16:12:00 +0900
categories: [Spirng, Spring 입문]
tags: [spring]
---

# Spring 입문 - 스프링 웹 개발 기초
---
1. [Welcome Page](#welcome-page)
2. [정적 컨텐츠](#정적-컨텐츠)
3. [MVC와 템플릿 엔진](#mvc와-템플릿-엔진)
4. [API](#api)

## Welcome Page
`resources/static/index.html`
- 스프링 부트가 제공하는 Welcome Page 기능
    - `static/index.html` 을 올려두면 Welcome page 기능을 제공한다.

## 정적 컨텐츠
- 스프링 부트 정적 컨텐츠 기능

`resources/static/hello-static.html`

![](/assets/img/posts/spring-start-1-1.png)

## MVC와 템플릿 엔진

> MVC: Model, View, Controller
{: .prompt-info }

### Controller

```java
@Controller
public class HelloController {

	@GetMapping("hello-mvc")
	public String helloMvc(@RequestParam("name") String name, Model model) {
		model.addAttribute("name", name);
		return "hello-template";
	}
}
```

### View
`resources/templates/hello-template.html`

```html
<html xmlns:th="http://www.thymeleaf.org">
<body>
<p th:text="'hello ' + ${name}">hello! empty</p>
</body>
</html>
```

- 실행 
  - `http://localhost:8080/hello-mvc?name=spring`

![](/assets/img/posts/spring-start-1-2.png)

## API
**@ResponseBody 문자 반환**

```java
@Controller
public class HelloController {
   
    @GetMapping("hello-string")
    @ResponseBody
    public String helloString(@RequestParam("name") String name) {
        return "hello " + name;
    }
}
```

- `@ResponseBody` 를 사용하면 뷰 리졸버(`viewResolver`)를 사용하지 않음
- 대신에 HTTP의 BODY에 문자 내용을 직접 반환

**@ResponseBody 객체 반환**

```java
@Controller
public class HelloController {
    
    @GetMapping("hello-api")
    @ResponseBody
    public Hello helloApi(@RequestParam("name") String name) {
        Hello hello = new Hello();
        hello.setName(name);
        return hello;
    }

    static class Hello {
        private String name;

        public String getName() {
            return name;
        }

        public void setName(String name) {
            this.name = name;
        }
    }
}
```

- `@ResponseBody` 를 사용하고, 객체를 반환하면 객체가 JSON으로 변환됨

![](/assets/img/posts/spring-start-1-3.png)
- `@ResponseBody` 를 사용
  - HTTP의 BODY에 문자 내용을 직접 반환
  - `viewResolver` 대신에 `HttpMessageConverter` 가 동작
  - 기본 문자처리: `StringHttpMessageConverter`
  - 기본 객체처리: `MappingJackson2HttpMessageConverter`
  - byte 처리 등등 기타 여러 HttpMessageConverter가 기본으로 등록되어 있음