---
title: 부분집합
date: 2026-02-06 11:16:00 +0900
categories: [Algorithm, 알고리즘]
tags: [algorithm]
---

# 부분집합(Subset)

- 용어
  - Subset : 부분집합 1개
  - Power Set : 모든 부분집합을 모은 집합

## 구현

### 재귀 함수를 통한 구현

```java
public class PowerSet {

    static int[] arr = {1, 2, 3};
    static boolean[] selected = new boolean[arr.length];

    public static void main(String[] args) {
        powerSet(0);
    }

    static void powerSet(int visitedIdx) {
        if(visitedIdx == arr.length) {
            for(int idx = 0; idx < arr.length; idx++) {
                if (selected[idx]) {
                    System.out.print(arr[idx] + " ");
                }
            }
            System.out.println();
            return;
        }

        selected[visitedIdx] = true;
        powerSet(visitedIdx + 1);

        selected[visitedIdx] = false;
        powerSet(visitedIdx + 1);
    }
}
```