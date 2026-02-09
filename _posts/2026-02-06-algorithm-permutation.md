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

    static final int ELEMENT_COUNT = 3;
    static int[] elementList = {1, 2, 3};
    static boolean[] elementUsedCheckList = new boolean[ELEMENT_COUNT];
    static final int SELECT_COUNT = 2;
    static int[] selectElementList = new int[SELECT_COUNT];

    public static void main(String[] args) {
        permutation(0);
    }

    static void permutation(int selectIdx) {
        // 1. 기저 조건(종료 조건)
        // 모든 원소를 선택했다면,
        if(selectIdx == SELECT_COUNT) {
            for(int idx = 0; idx < SELECT_COUNT; idx++) {
                System.out.print(selectElementList[idx] + " ");
            }
            System.out.println();
            return;
        }
        
        // 2. 전처리 로직
        // 아직 다 선택하지 않았다면,
        for(int elementIdx = 0; elementIdx < ELEMENT_COUNT; elementIdx++) {
            // 이미 선택한 원소라면 -> 패스
            if(elementUsedCheckList[elementIdx]) continue;
            
            // 해당 원소를 아직 사용하지 않았다.
            elementUsedCheckList[elementIdx] = true;
            selectElementList[selectIdx] = elementList[elementIdx];
            
            // 3. 재귀 호출
            permutation(selectIdx + 1);
            
            // 4. 후처리 로직
            elementUsedCheckList[elementIdx] = false;
        }
    }
}
```