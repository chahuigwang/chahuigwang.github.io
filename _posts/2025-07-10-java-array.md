---
title: Java - array
date: 2025-07-10 17:14:00 +0900
categories: [Programming Languages, Java]
tags: [java]
---

# 배열(Array)
---
## 배열의 선언과 생성
```java
타입[] 변수이름;
변수이름 = new 타입[길이];

// 배열의 선언과 생성을 동시에
타입[] 변수이름 = new 타입[길이];
```

## 배열의 초기화
```java
int[] score = new int[5];
score[0] = 50;
score[1] = 60;
score[2] = 70;
score[3] = 80;
score[4] = 90;

// 배열의 선언과 초기화를 동시에
int[] score = new int[]{50, 60, 70, 80, 90};
int[] score = {50, 60, 70, 80, 90};
```

## 배열의 복사
```java
System.arraycopy(Object src, int srcPos, Object dest, int destPos, int length)
```

## 배열의 정렬
```java
Arrays.sort(arr); // 오름차순
Arrays.sort(arr, Collections.reverseOrder()); // 내림차순
```