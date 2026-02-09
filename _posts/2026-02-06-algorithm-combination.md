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

- 예제: {1, 2, 3} 중 2개를 선택하는 조합

### 재귀 함수를 통한 구현

```java
public class Combination {

    static int[] elementList = {1, 2, 3};
    static final int ELEMENT_COUNT = 3;
    static final int SELECT_COUNT = 2;
    static int[] selectElementList = new int[SELECT_COUNT];

    public static void main(String[] args) {
        combination(0, 0);
    }

    static void combination(int selectIdx, int elementIdx) {
        // 1. 모든 원소를 선택했다면 종료
        if(selectIdx == SELECT_COUNT) {
            for(int idx = 0; idx < SELECT_COUNT; idx++) {
                System.out.print(selectElementList[idx] + " ");
            }
            System.out.println();
            return;
        }
        
        // 2. 모든 원소를 확인했다면 종료
        if(elementIdx == ELEMENT_COUNT) {
            return;
        }
        
        // 3. 원소 선택
        selectElementList[selectIdx] = elementList[elementIdx];
        combination(selectIdx + 1, elementIdx + 1);
        
        // 4. 원소 선택 x
        selectElementList[selectIdx] = 0; // 초기화
        combination(selectIdx, elementIdx + 1);
    }
}
```

### 재귀 + for문

```java
public class CombinationWithLoop {

    static int[] elementList = {1, 2, 3};
    static final int ELEMENT_COUNT = 3;
    static final int SELECT_COUNT = 2;
    static int[] selectElementList = new int[SELECT_COUNT];

    public static void main(String[] args) {
        combination(0, 0);
    }

    static void combination(int selectIdx, int elementIdx) {
        // 1. 모든 원소를 선택했다면 종료
        if(selectIdx == SELECT_COUNT) {
            for(int idx = 0; idx < SELECT_COUNT; idx++) {
                System.out.print(selectElementList[idx] + " ");
            }
            System.out.println();
            return;
        }

        for(int idx = elementIdx; idx < ELEMENT_COUNT; idx++) {
            selectElementList[selectIdx] = elementList[idx];
            combination(selectIdx + 1, idx + 1);
        }
    }
}
```
