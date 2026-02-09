---
title: Next Permutation
date: 2026-02-09 16:57:00 +0900
categories: [Algorithm, 알고리즘]
tags: [algorithm]
---

# Next Permutation
---
- Next Permutation : 현 순열에서 사전 순으로 다음 순열 생성

### 알고리즘
- 배열을 오름차순(사전 순으로 가장 작은 순열)으로 정렬한 후 시작한다.
- 아래 과정을 반복하여 사전 순으로 다음으로 큰 순열 생성(가장 큰 순열(내림차순 순열)을 만들 때까지 반복)
  1. 피벗(pivot) 찾기
     - 배열의 뒤에서부터 탐색하며 a[i-1] < a[i] 를 만족하는 위치(감소하는 위치)를 찾는다.
       - 이때 i-1이 피벗
       - 만약 이런 위치를 찾지 못하면 -> 현재 순열이 가장 큰 순열
  2. 교환 대상 찾기
     - 피벗의 오른쪽에서
       - a[pivot]보다 큰 값 중
       - 가장 오른쪽에 있는(가장 작은) 값을 찾는다.
  3. 피벗과 교환
  4. 피벗 오른쪽을 오름차순으로 정렬

### 예제 코드 - {1, 2, 3, 4}

```java
import java.util.Arrays;

public class NextPermutation {

    static int[] elementList = {1, 2, 3, 4};
    static final int N = 4;

    public static void main(String[] args) {
        // 배열을 오름차순으로 정렬
        Arrays.sort(elementList);

        do {
            System.out.println(Arrays.toString(elementList)); // 사전 순으로 가장 작은 순열 최초 한번 처리
        } while(nextPermutation());
    }

    static boolean nextPermutation() {
        //1. 피벗(i - 1) 찾기
        int i = N - 1;
        while(i > 0 && elementList[i-1] >= elementList[i]) i--;
        if(i == 0) return false;

        // 2. 교환 대상 찾기
        int j = N - 1;
        while(elementList[i-1] >= elementList[j]) j--;

        // 3. i-1번째 값과 j번째 값 교환
        swap(i - 1, j);

        // 4. i부터 끝까지 오름차순 정렬
        reverse(i, N - 1);

        return true;
    }

    // idx1번째 값과 idx2번째 값 교환
    static void swap(int idx1, int idx2) {
        int temp = elementList[idx1];
        elementList[idx1] = elementList[idx2];
        elementList[idx2] = temp;
    }

    // start부터 end까지의 값을 뒤집는다.
    static void reverse(int start, int end) {
        while(start < end) {
            swap(start++, end--);
        }
    }
}
```

---
## Next Permutation을 활용한 조합

> 0과 1로 이루어진 비트 배열에 nextPermutation을 적용하면 1의 위치가 바뀌는 모든 경우가 생성되고, 그 위치를 “선택”으로 해석하면 조합이 된다.

### 예제 코드 - {1, 2, 3, 4} 중 2개를 선택하는 조합

```java
public class NextPermutationCombination {

    static int[] elementList = {1, 2, 3, 4};
    static final int ELEMENT_COUNT = 4;
    static final int SELECT_COUNT = 2;

    // 1이면 선택, 0이면 미선택
    static int[] select = new int[ELEMENT_COUNT];

    public static void main(String[] args) {
        // select 배열을 사전 순으로 가장 작은 상태로 설정
        for(int selectIdx = ELEMENT_COUNT - SELECT_COUNT; selectIdx < ELEMENT_COUNT; selectIdx++) { // 뒤의 SELECT_COUNT개를 1로 설정
            select[selectIdx] = 1;
        }

        do {
            printCombination();
        } while(nextPermutation());
    }

    static void printCombination() {
        for(int idx = 0; idx < ELEMENT_COUNT; idx++) {
            if(select[idx] == 1) {
                System.out.print(elementList[idx] + " ");
            }
        }
        System.out.println();
    }

    // select 배열을 nextPermutation
    static boolean nextPermutation() {
        //1. 피벗(i - 1) 찾기
        int i = ELEMENT_COUNT - 1;
        while(i > 0 && select[i-1] >= select[i]) i--;
        if(i == 0) return false;

        // 2. 교환 대상 찾기
        int j = ELEMENT_COUNT - 1;
        while(select[i-1] >= select[j]) j--;

        // 3. i-1번째 값과 j번째 값 교환
        swap(i - 1, j);

        // 4. i부터 끝까지 오름차순 정렬
        reverse(i, ELEMENT_COUNT - 1);

        return true;
    }

    // idx1번째 값과 idx2번째 값 교환
    static void swap(int idx1, int idx2) {
        int temp = select[idx1];
        select[idx1] = select[idx2];
        select[idx2] = temp;
    }

    // start부터 end까지의 값을 뒤집는다.
    static void reverse(int start, int end) {
        while(start < end) {
            swap(start++, end--);
        }
    }
}
```