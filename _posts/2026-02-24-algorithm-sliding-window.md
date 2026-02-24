---
title: 슬라이딩 윈도우
date: 2026-02-24 16:21:00 +0900
categories: [Algorithm, 알고리즘]
tags: [algorithm]
---

# 슬라이딩 윈도우(Sliding Window)
---
- 보통 배열이나 리스트에서 **고정된 크기**의 연속된 구간을 효율적으로 탐색하는 기법
- 고정 사이즈의 윈도우가 이동하면서 윈도우 내에 있는 데이터를 이용해 문제를 풀이하는 알고리즘
- 각 윈도우의 공통된 교집합의 정보를 재사용하고, 차이가 나는 양쪽 끝 원소만 갱신하는 방법
- 배열이나 리스트의 요소의 일정 범위의 값을 비교할 때 사용하면 매우 유용

![Sliding Window](/assets/img/posts/슬라이딩윈도우.png)

- 예제 : [BOJ 2559 - 수열](https://www.acmicpc.net/problem/2559)
  - N일의 온도의 수열에서 연속적인 K일의 온도의 합이 최대가 되는 값을 출력

```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.StringTokenizer;

public class Main {

    static BufferedReader br;
    static StringTokenizer st;

    static int[] temperatures;
    static int dayCount;
    static int windowSize; // window의 크기

    static int maxSum;

    public static void main(String[] args) throws IOException {
        init();
        slidingWindow();
        System.out.println(maxSum);
    }

    static void init() throws IOException {
        br = new BufferedReader(new InputStreamReader(System.in));
        st = new StringTokenizer(br.readLine().trim());

        dayCount = Integer.parseInt(st.nextToken());
        windowSize = Integer.parseInt(st.nextToken());

        temperatures = new int[dayCount];
        st = new StringTokenizer(br.readLine().trim());
        for(int dayIdx = 0; dayIdx < dayCount; dayIdx++) {
            temperatures[dayIdx] = Integer.parseInt(st.nextToken());
        }

        maxSum = 0;
    }

    static void slidingWindow() {
        int windowSum = 0;
        for(int dayIdx = 0; dayIdx < windowSize; dayIdx++) {
            windowSum += temperatures[dayIdx]; // 초기 window 합 : 0 ~ windowSize
        }

        maxSum = windowSum;
        for(int dayIdx = windowSize; dayIdx < dayCount; dayIdx++) {
            windowSum += temperatures[dayIdx]; // window 합 += 오른쪽 한칸
            windowSum -= temperatures[dayIdx - windowSize]; // window 합 -= 왼쪽 한칸
            maxSum = Math.max(maxSum, windowSum);
        }
    }
}
```