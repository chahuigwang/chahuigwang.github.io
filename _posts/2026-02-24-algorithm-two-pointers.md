---
title: 투 포인터
date: 2026-02-24 16:21:00 +0900
categories: [Algorithm, 알고리즘]
tags: [algorithm]
---

# 투 포인터(Two Pointers)
---
- 배열 또는 리스트에서 두 개의 포인터를 이용해 효율적으로 탐색하는 기법

### 예제
- 두 수의 합([BOJ 3273](https://www.acmicpc.net/problem/3273))
  - n개의 서로 다른 자연수로 이루어진 수열이 있다.
  - 각 수열의 항은 1보다 크거나 같고, 1,000,000보다 작거나 같은 자연수이다.
  - 2개의 항 (Ai, Aj) 을 선택하여 더한 값이 x를 만족하는 쌍의 수는?

  - 해결 방법 : 정렬 후 투 포인터 기법을 활용한다.

    ```java
    import java.io.BufferedReader;
    import java.io.IOException;
    import java.io.InputStreamReader;
    import java.util.Arrays;
    import java.util.StringTokenizer;

    public class Main {

        public static void main(String[] args) throws IOException {
            BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
            StringTokenizer st = new StringTokenizer(br.readLine().trim());

            int n = Integer.parseInt(st.nextToken());
            int[] sequence = new int[n];

            st = new StringTokenizer(br.readLine().trim());
            for(int i = 0; i < n; i++) {
                sequence[i] = Integer.parseInt(st.nextToken());
            }
            Arrays.sort(sequence); // 오름차순 정렬

            st = new StringTokenizer(br.readLine().trim());
            int target = Integer.parseInt(st.nextToken());

            int start = 0; // 가장 왼쪽부터 시작
            int end = n-1; // 가장 오른쪽부터 시작
            int sum = 0;
            int count = 0;

            while(start < end) {
                sum = sequence[start] + sequence[end];
                if(sum == target) {
                    count++;
                    // start는 오른쪽으로 1칸, end는 왼쪽으로 1칸 이동
                    start++;
                    end--;
                } else if (sum < target) {
                    start++; // start만 오른쪽으로 1칸 이동
                } else {
                    end--; // end만 왼쪽으로 1칸 이동
                }
            }

            System.out.println(count);
        }
    }
    ```

- 구간합([BOJ 2003](https://www.acmicpc.net/problem/2003))
  - N개의 수로 된 수열 A[1], A[2], …, A[N] 이 있다.
  - 이 수열의 i번째 수부터 j번째 수까지의 합 A[i] + A[i+1] + … + A[j-1] + A[j]가 M이 되는 경우의 수는?
  
  - 해결 방법 : 투 포인터 기법을 활용한다.

    ```java
    import java.io.BufferedReader;
    import java.io.IOException;
    import java.io.InputStreamReader;
    import java.util.StringTokenizer;

    public class Main {

        public static void main(String[] args) throws IOException {
            BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
            StringTokenizer st = new StringTokenizer(br.readLine().trim());

            int n = Integer.parseInt(st.nextToken());
            int target = Integer.parseInt(st.nextToken());
            int[] sequence = new int[n];

            st = new StringTokenizer(br.readLine().trim());
            for(int i = 0; i < n; i++) {
                sequence[i] = Integer.parseInt(st.nextToken());
            }

            int start = 0; // inclusive
            int end = 0; // exclusive
            int sum = 0; // start ~ end-1 까지의 합
            int count = 0;

            while(true) {
                if(sum >= target) {
                    if(sum == target) count++;
                    sum -= sequence[start++]; // start를 오른쪽으로 한칸 이동
                } else if (end == n) { // sum < target 이므로 end를 오른쪽으로 한칸 이동해야 하지만, end가 이미 오른쪽 끝인 경우
                    break;
                } else {
                    sum += sequence[end++]; // end를 오른쪽으로 한칸 이동
                }
            }

            System.out.println(count);
        }
    }
    ```