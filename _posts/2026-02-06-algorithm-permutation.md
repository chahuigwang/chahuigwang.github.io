---
title: 순열
date: 2026-02-06 09:06:00 +0900
categories: [Algorithm, 알고리즘]
tags: [algorithm]
---

# 순열(Permutaion)
---
- nPr : 서로 다른 n개에서 순서를 고려하여 r개를 택하여 일렬로 나열하는 경우의 수

## 구현
---
### 1. 중첩 반복문을 통한 구현

- 예제: {1, 2, 3} 중 2개 순열

```java
public class Permutation {

    public static void main(String[] args) {
        int[] arr = {1, 2, 3};
        final int SELECT_COUNT = 2; // 뽑는 개수

        for(int i = 0; i < arr.length; i++) {
            for(int j = 0; j < arr.length; j++) {
                if(i == j) continue;
                System.out.println(arr[i] + " " + arr[j]);
            }
        }
    }
}
```

- 출력 결과

```
1 2
1 3
2 1
2 3
3 1
3 2
```

- 한계점
  - 뽑는 개수(r)가 커지면 반복문의 개수도 증가
  - 확장성 ❌

---  

### 2. 재귀 함수를 통한 구현

- 예제: {1, 2, 3} 중 2개 순열

```java
public class Permutation {

    static int[] arr = {1, 2, 3};
    static boolean[] selected = new boolean[arr.length];
    static int[] perm = new int[2];
    static final int SELECT_COUNT = 2;

    public static void main(String[] args) {
        permutation(0);
    }

    static void permutation(int selectedCount) {
        // 1. 기저 조건(종료 조건)
        // 모든 원소를 선택했다면,
        if(selectedCount == SELECT_COUNT) {
            // 완성된 순열 처리
            for(int x : perm) {
                System.out.print(x + " ");
            }
            System.out.println();
            return;
        }

        // 2. 전처리 로직
        // 아직 다 선택하지 않았다면
        for(int idx = 0; idx < arr.length; idx++) {
            // 이미 선택한 원소라면 건너뜀
            if(selected[idx]) continue;

            // 해당 원소를 아직 선택하지 않았다.
            selected[idx] = true;
            perm[selectedCount] = arr[idx];
            
            // 3. 재귀 호출
            permutation(selectedCount + 1);
            
            // 후처리 로직
            selected[idx] = false; // 백트래킹
        }
    }
}
```