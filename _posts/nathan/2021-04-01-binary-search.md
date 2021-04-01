---
title : 이진 탐색이란? - Nathan
tags : 배열, 이진 탐색, 그리디
layout : article
author : Nathan Hong
mathjax : true
date : 2021-04-01
---


- [이진 탐색이란?](#이진-탐색이란?)
  - [알고리즘 동작 순서](#알고리즘-동작-순서)
  - [이진 탐색 코드](#이진-탐색-코드)
  - [예제. 수 찾기](#예제.-수-찾기)
  
  

## 이진 탐색이란?

---

- 정렬돼 있는 배열에서 특정한 값을 찾는 알고리즘
- 단순 완전탐색과 달리 중간에 있는 임의의 값을 선택한 후 찾고자 하는 값과 비교하며 탐색하는 알고리즘

### 알고리즘 동작 순서

---

```
13 15 25 35 51 65 75

찾을 값 : 65
```

- 임의의 가운데 값 35를 선택
- `65 > 35` 이므로 35보다 우측에 존재
    - 배열의 범위를 좁힘

    ```
    51 65 75
    ```

- 좁힌 범위에서 가운데 값을 선택 후 비교
    - 가운데 값 : 65
    - **가운데 값 == 찾을 값**
    - 탐색 종료
- 시간 복잡도 : `O(logN)`

### 이진 탐색 코드

---

```java
public int search(int[] array, int target) {
        Arrays.sort(array);
        int front = 0;
        int end = array.length - 1;
        int mid;
        while (front <= end) {
            mid = (front + end) / 2;

            if (array[mid] > target) {
                end = mid - 1;
            } else if (array[mid] < target) {
                front = mid + 1;
            } else {
                return mid;
            }
        }

        return -1;
}
```

### 예제. 수 찾기

---

[1920번: 수 찾기](https://www.acmicpc.net/problem/1920)

**풀이**

- 배열 A 정렬
- 주어진 M개의 수를 하나씩 배열 A에 이분 탐색을 진행
- 존재하면 1, 존재하지 않으면 0 출력

**코드**

```java
import java.io.*;
import java.util.Arrays;

public class Main {
    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));

        int N = Integer.parseInt(br.readLine());
        String[] inputN =  br.readLine().split(" ");
        int[] A = new int[N];

        for (int i = 0; i < N; i++) {
            A[i] = Integer.parseInt(inputN[i]);
        }

        int M = Integer.parseInt(br.readLine());
        String[] targets = br.readLine().split(" ");

        Arrays.sort(A);

        for (int i = 0; i < M; i++) {
            int result = binarySearch(A, Integer.parseInt(targets[i]));

            System.out.println(result);
        }

        br.close();
        bw.close();
    }

    public static int binarySearch(int[] array, int target) {
        int front = 0;
        int end = array.length - 1;
        int mid;

        while (front <= end) {
            mid = (front + end) / 2;

            if (array[mid] > target) {
                end = mid - 1;
            } else if (array[mid] < target) {
                front = mid + 1;
            } else {
                return 1;
            }
        }

        return 0;
    }
}
```