---
title: DFS & BFS
date: 2025-03-06 20:37:00 +0900
categories: [Algorithm, 알고리즘]
tags: [algorithm]
---

# 그래프 탐색 알고리즘: DFS / BFS
---

## DFS(Depth-First Search)
- DFS: 깊이 우선 탐색, 그래프에서 **깊은 부분을 우선적으로 탐색**하는 알고리즘
- DFS는 **스택 자료구조(혹은 재귀 함수)** 를 이용하여 구현

### DFS 동작 과정
1. 탐색 시작 노드를 스택에 삽입하고 방문 처리
2. 스택의 최상단 노드에 방문하지 않은 인접한 노드가 하나라도 있으면 그 노드를 스택에 넣고 방문 처리. 방문하지 않은 인접 노드가 없으면 스택에서 최상단 노드를 꺼냄
3. 더 이상 2번 과정을 수행할 수 없을 때까지 반복

### 예시 그래프 및 구현
![](/assets/img/posts/graph.png)
- 방문 기준: 번호가 낮은 인접 노드부터
- 시작 노드: 1
- 방문 순서: `1 2 7 6 8 3 4 5 8`


#### Stack을 이용한 구현
```python
def dfs_stack(graph, start):
    visited = [False] * (len(graph) + 1)
    stack = [start]  # 1. 시작 노드를 스택에 삽입하고 방문 처리
    visited[start] = True
    print(start, end=' ')

    # 3. 더 이상 2번의 과정을 수행할 수 없을 때까지 반복
    while stack:
        # 2번 과정
        node = stack[-1]  # 최상단 노드 확인
        found = False  # 방문하지 않은 인접 노드가 있는지 체크

        for neighbor in graph[node]:  # 작은 번호부터 탐색
            if not visited[neighbor]:  # 인접 노드를 방문하지 않았다면
                stack.append(neighbor)
                visited[neighbor] = True  # 방문 처리
                print(neighbor, end=' ')
                found = True
                break
            
        if not found:  # 방문하지 않은 인접 노드가 없으면 pop
            stack.pop()

# 그래프 정의 (2차원 리스트)
graph = [
    [],
    [2, 3, 8],
    [1, 7],
    [1, 4, 5],
    [3, 5],
    [3, 4],
    [7],
    [2, 6, 8],
    [1, 7]
]

dfs_stack(graph, 1)
```

#### 재귀 함수를 이용한 구현
```python
def dfs(graph, v, visited):
    # 현재 노드를 방문 처리
    visited[v] = True
    print(v, end=' ')
    # 현재 노드와 연결된 다른 노드를 재귀적으로 방문
    for neighbor in graph[v]:
        if not visited[neighbor]:
            dfs(graph, neighbor, visited)

graph = [
    [],
    [2, 3, 8],
    [1, 7],
    [1, 4, 5],
    [3, 5],
    [3, 4],
    [7],
    [2, 6, 8],
    [1, 7]
]

visited = [False] * 9  # len(graph) + 1 

dfs(graph, 1, visited)
```

---

## BFS(Depth-First Search)
- BFS: 너비 우선 탐색, 그프에서 **가까운 노드부터 우선적으로 탐색**하는 알고리즘
- BFS는 **큐 자료구조**를 이용하여 구현

### BFS 동작 과정
1. 탐색 시작 노드를 큐에 삽입하고 방문 처리
2. 큐에서 노드를 꺼낸 뒤에 해당 노드의 인접 노드 중에서 방문하지 않은 노드를 모두 큐에 삽입하고 방문 처리
3. 더 이상 2번의 과정을 수행할 수 없을 때까지 반복

### 예시 그래프 및 구현
![](/assets/img/posts/graph.png)
- 방문 기준: 번호가 낮은 인접 노드부터
- 시작 노드: 1
- 방문 순서: `1 2 3 8 7 4 5 6`

```python
from collections import deque

def bfs(graph, start, visited):
    # 1. 탐색 시작 노드를 큐에 삽입하고 방문 처리
    queue = deque([start])
    visited[start] = True

    # 3. 더 이상 2번의 과정을 수행할 수 없을 때까지 반복
    while queue:
        # 2번 과정
        v = queue.popleft()  # 큐에서 노드를 꺼냄
        print(v, end=' ')
        # 해당 노드의 인접 노드 중에서 방문하지 않은 노드를 모두 큐에 삽입하고 방문 처리
        for neighbor in graph[v]:
            if not visited[neighbor]:
                queue.append(neighbor)
                visited[neighbor] = True
                
graph = [
    [],
    [2, 3, 8],
    [1, 7],
    [1, 4, 5],
    [3, 5],
    [3, 4],
    [7],
    [2, 6, 8],
    [1, 7]
]

visited = [False] * 9

bfs(graph, 1, visited)
```