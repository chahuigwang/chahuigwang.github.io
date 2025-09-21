---
title: DFS/BFS - 연결 요소의 개수
date: 2025-09-21 14:52:00 +0900
categories: [Algorithm, 문제 풀이]
tags: [algorithm, algorithm problems]
---

# 연결 요소의 개수
그래프가 주어졌을 때, 연결 요소의 개수를 구하는 문제 유형

## 예제
1. 음료수 얼려 먹기
    - 문제 설명
    ![](assets/img/posts/연결요소의개수1.png)

    - 문제 풀이
    
        ```java
        import java.util.Scanner;

        public class FreezeDrink {
            public static int n, m;
            public static int frame[][];

            public static void main(String[] args) {
                Scanner sc = new Scanner(System.in);

                n = sc.nextInt();
                m = sc.nextInt();
                sc.nextLine();

                frame = new int[n][m];
                for(int i = 0; i < n; i++) {
                    String row = sc.nextLine();
                    for(int j = 0; j < m; j++) {
                        frame[i][j] = row.charAt(j) - '0';
                    }
                }

                int count = 0;
                for(int i = 0; i < n; i++) {
                    for(int j = 0; j < m; j++) {
                        if(dfs(i, j)) count++;
                    }
                }

                System.out.println(count);
            }

            public static boolean dfs(int x, int y) {
                if(x <= -1 || x >= n || y <= -1 || y >= m) return false;

                if(frame[x][y] == 0) {
                    frame[x][y] = 1;

                    dfs(x - 1, y);
                    dfs(x, y - 1);
                    dfs(x + 1, y);
                    dfs(x, y + 1);
                    return true;
                }
                return false;
            }
        }
        ```

2. 백준 11724번: 연결 요소의 개수
    - 문제 설명  
        [BOJ11724](https://www.acmicpc.net/problem/11724)

    - 문제 풀이  
        ```java
        import java.util.ArrayList;
        import java.util.Scanner;

        public class BOJ11724 {
            public static ArrayList<ArrayList<Integer>> graph = new ArrayList<>();
            public static boolean[] visited;

            public static void main(String[] args) {
                Scanner sc = new Scanner(System.in);

                int n = sc.nextInt();
                int m = sc.nextInt();

                for(int i = 0; i <= n; i++) {
                    graph.add(new ArrayList<>());
                }
                visited = new boolean[n+1];

                for(int i = 0; i < m; i++) {
                    int u = sc.nextInt();
                    int v = sc.nextInt();
                    graph.get(u).add(v);
                    graph.get(v).add(u);
                }

                int count = 0;
                for(int i = 1; i <= n; i++) {
                    if(!visited[i]) {
                        dfs(i);
                        count++;
                    }
                }
                System.out.println(count);
            }

            public static void dfs(int x) {
                visited[x] = true;

                for(int neighbor : graph.get(x)) {
                    if(!visited[neighbor]) {
                        dfs(neighbor);
                    }
                }
            }
        }
        ```