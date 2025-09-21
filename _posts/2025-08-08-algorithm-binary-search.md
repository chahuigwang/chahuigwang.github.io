---
title: Binary Search
date: 2025-08-08 23:09:00 +0900
categories: [Algorithm, 알고리즘]
tags: [algorithm]
---

# 이분 탐색(Binary Search)
---
이분 탐색 : **정렬되어 있는** 리스트에서 **탐색 범위를 절반씩 좁혀가며 데이터를 탐색**하는 방법
- 시작점, 끝점, 중간점을 이용하여 탐색 범위를 설정

### 이분 탐색 구현 소스코드
```java
int binarySearch(int[] arr, int target, int start, int end) {
    while(start <= end) {
        int mid = (start + end) / 2;

        if(arr[mid] == target) return mid;
        else if(arr[mid] > target) end = mid - 1;
        else start = mid + 1;
    }
    return -1; // target을 찾지 못 했을 경우 -1 반환
}
```

### Java 라이브러리 메소드
- `Arrays.BinarySearch(Object[] arr, Object key)`
- `Collections.BinarySearch(List<T> list, T key)`

> key를 찾지 못 했을 경우 -(삽입될 위치 + 1)를 반환 -> 삽입될 위치 = -(리턴값 + 1)
{: .prompt-info }
