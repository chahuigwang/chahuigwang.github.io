---
title: 조합
date: 2026-02-06 10:36:00 +0900
categories: [Algorithm, 알고리즘]
tags: [algorithm]
---

# 조합(Combination)
---
- nCr : 서로 다른 n개의 원소에서 r개를 중복 없이, 순서를 고려하지 않고 선택하는 것.

## 구현
### 재귀 함수를 통한 구현

- 예제: {1, 2, 3} 중 2개 순열

```java
public class Combination {

    static int[] arr = {1, 2, 3};
    static boolean[] selected = new boolean[arr.length];
    static int[] comb = new int[2];
    static final int SELECT_COUNT = 2;

    public static void main(String[] args) {
        combination(0, 0);
    }

    static void combination(int selectedCount, int start) {
        if(selectedCount == SELECT_COUNT) {
            for(int x : comb) {
                System.out.print(x + " ");
            }
            System.out.println();
            return;
        }

        for(int idx = start; idx < arr.length; idx++) {
            comb[selectedCount] = arr[idx];
            combination(selectedCount + 1, idx + 1);
        }
    }
}
```