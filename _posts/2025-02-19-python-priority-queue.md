---
title: 파이썬 우선순위 큐, heapq
date: 2025-02-19 22:01:00 +0900
categories: [Programming Languages, Python]
tags: [programming languages, python]
---

# 파이썬 우선순위 큐 - heapq
---
파이썬에서는 우선순위 큐 모듈로 PriorityQueue와 heapq를 제공한다.
- PriorityQueue: Thread-Safe 하지만 느림
- heapq: Thread-Non-Safe 하지만 빠름

코딩테스트 상황에서는 Thread-Safe를 보장하지 않아도 되기 때문에 heapq를 사용한다.

## heapq 사용법
- 모듈 import
```python
import heapq
```

- 원소 추가
```python
heap = []
heapq.heappush(heap, item)
```

- 원소 삭제
```python
heapq.heappop(heap)
```

- 리스트 x를 힙으로 변환
```python
heapq.heapify(x)
```