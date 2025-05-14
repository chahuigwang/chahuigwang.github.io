---
title: 다이나믹 프로그래밍(Dynamic Programming)
date: 2025-05-13 20:18:00 +0900
categories: [Algorithm, Algorithms]
tags: [algorithm]
---

# 다이나믹 프로그래밍 Dynamic Programming
---

## 다이나믹 프로그래밍
- 다이나믹 프로그래밍: **메모리를 적절히 사용하여 수행 시간 효율성을 비약적으로 향상시키는 방법**
- 이미 계산된 결과(작은 문제)는 별도의 메모리 영역에 저장하여 다시 계산하지 않도록 한다.
- 다이나믹 프로그래밍의 구현은 일반적으로 두 가지 방식
    - 탑다운
    - 바텀업

## 다이나믹 프로그래밍의 조건
1. **최적 부분 구조(Optimal Substructure)**
    - 큰 문제를 작은 문제로 나눌 수 있으며 작은 문제의 답을 모아서 큰 문제를 해결할 수 있다.
2. **중복되는 부분 문제(Overlapping Subproblem)**
    - 동일한 작은 문제를 반복적으로 해결해야 한다.

## Example) 피보나치 수열
![](/assets/img/posts/fibonacci.png)
> 피보나치 수열은 다이나믹 프로그래밍의 사용 조건(**최적 부분 구조, 중복되는 부분 문제**)을 만족한다.

#### 단순 재귀 소스코드(Python)
```python
def fibo(x):
    if x == 1 or x == 2:
        return 1
    return fibo(x-1) + fibo(x-2)

print(fibo(4))
```

#### 시간 복잡도
- 다음과 같이 f(2)가 여러 번 호출되는 것을 확인할 수 있다. (**중복되는 부분 문제**)
![](/assets/img/posts/fibonacci2.png)

> O(2ⁿ)의 시간 복잡도를 가진다.

### 메모이제이션(Memoization)
- 한 번 계산한 결과를 메모리 공간에 메모하는 기법
    - 같은 문제를 다시 호출하면 메모했던 결과를 그대로 가져옴

#### 탑다운(메모이제이션) 다이나믹 프로그래밍 소스코드(Python)
```python
d = [0]*100

def fibo(x):
    if x == 1 or x == 2:
        return 1

    if d[x] != 0:
        return d[x]

    d[x] = fibo(x-1) + fibo(x-2)
    return d[x]

print(fibo(99))
```

#### 바텀업 다이나믹 프로그래밍 소스코드(Python)
```python
d = [0]*100

d[1] = 1
d[2] = 1
n = 99

for i in range(3, n+1):
    d[i] = d[i-1] + d[i-2]

print(d[n])
```

#### 메모이제이션 동작 분석
![](/assets/img/posts/fibonacci3.png)
> O(N)의 시간 복잡도를 가진다.

### 다이나믹 프로그래밍 문제 접근법
- 주어진 문제가 **다이나믹 프로그래밍 유형임을 파악**하는 것이 중요
- 우선 그리디, 구현, 완전 탐색 등의 아이디어로 문제를 해결할 수 있는지 검토
    - 다른 알고리즘으로 풀이 방법이 떠오르지 않으면 다이나믹 프로그래밍을 고려
- 일단 재귀 함수로 비효율적인 완전 탐색 프로그래밍을 작성한 뒤에, 작은 문제에서 구한 답이 큰 문제에서 그대로 사용될 수 있으면 코드를 개선하는 방법을 사용할 수 있다.