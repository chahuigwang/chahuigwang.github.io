---
title: 파이썬 문자열 뒤집기
date: 2025-02-12 23:37:00 +0900
categories: [Programming Languages, Python]
tags: [python]
---

# 파이썬 문자열 뒤집기(Slicing 활용)
---
## 파이썬 슬라이싱(Slicing)
- Slicing: 리스트에서 일부분을 추출할 때 사용
- 기본 사용법
```python
a[start:end:step]
```

## 문자열 뒤집기
> Slicing을 활용하여 문자열을 뒤집을 수 있다.

```python
str = str[::-1]
# ex) 'hello' -> 'olleh'
```

### 추가) 리스트(list) 뒤집기
- 문자열이 아닌 단순 리스트라면 reverse를 활용하여 간단하게 뒤집을 수 있다.
```python
my_list.reverse()
```