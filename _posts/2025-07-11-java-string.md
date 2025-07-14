---
title: Java - 문자열 관련 Method
date: 2025-07-11 16:40:00 +0900
categories: [Programming Languages, Java]
tags: [java]
---

# Java 문자열 관련 Method
---
## String 관련 Method
- length() - 문자열의 길이
- isEmpty() - 문자열이 비었는지 확인

**문자 찾기**
- charAt(int index) - 특정 위치에 있는 문자 반환
- indexOf - 특정 문자 or 문자열이 처음 등장하는 위치 반환
    - indexOf(int ch)
    - indexOf(int ch, int fromIndex) // fromIndex :  탐색 시작 인덱스
    - indexOf(String str)	
    - indexOf(String str, int fromIndex)
- lastIndexOf - 특정 문자 or 문자열이 마지막으로 등장하는 위치 반환

**문자열 자르기**
- substring(int beginIndex)	
- substring(int beginIndex, int endIndex)

**문자 치환**
- replace(char oldChar, char newChar)
- replaceAll(String regex, String replacement)
- replaceFirst(String regex, String replacement)  


<br>
- equals(Object anObject) - 문자열 내용 비교
- split(String delimiter) - 문자열을 특정 구분자(delimiter)로 나누어 배열로 반환
- trim() - 문자열 앞뒤의 공백 제거

**문자열 ↔️ 정수 변환**
- Integer.parseInt(String s)
- Integer.toString(int num)
> String.valueOf() - int, double, boolean, char 등 모든 기본형을 문자열로 변환 가능