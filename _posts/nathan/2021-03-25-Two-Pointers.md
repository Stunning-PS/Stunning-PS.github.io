---
title : Two-Pointer 알고리즘 - Nathan
tags : 배열, 그리디, 투포인터
layout : article
author : Nathan Hong
mathjax : true
date : 2021-03-25
---


- [Two-Pointer 알고리즘](#Two-Pointers)
  - [Two-Pointer 문제](#Two-Pointer-문제)
  - [코드](#Two-Pointer-코드)
  

## Two-Pointers
---

- Two Pointers는 뜻 그래도 2개의 포인터를 조작해 문제를 해결하는 알고리즘이다.
- 풀고자 하는 문제에 맞게 2개의 포인터를 1차원 배열에 위치시켜 문제의 해를 찾아나가는 과정이라고 보면된다.
- Two-Pointer 알고리즘 같은 경우 개념이나 이론이 크게 존재하지 않기 때문에 문제를 통해 이해하는 것이 가장 좋디

### Two-Pointer 문제
---

[2003번: 수들의 합 2](https://www.acmicpc.net/problem/2003)

문제 내용

- N개의 수로 된 수열 `A[1], A[2], …, A[N]` 이 있다. 이 수열의 i번째 수부터 j번째 수까지의 합 `A[i] + A[i+1] + … + A[j-1] + A[j]`가 M이 되는 경우의 수를 구하는 프로그램을 작성하시오.

**예제**

```xml
10 5
1 2 3 4 2 5 3 1 1 2
```

**문제 접근법  1. 완전 탐색**

- 3중 for문을 통해 시작점, 끝점을 지정해 두 지점의 합을 구해 경우의 수를 구하는 방법
- 부분합 배열을 만들어 2중 for문으로 구하는 방법
- 그러나 위 2가지 모두 시간 초과가 나기 때문에 개선이 필요

**문제 접근법 2. Two-Pointer**

- **위 문제에 Two-Pointer 적용**
- start, end  두 개의 포인터 구성
    - start : 부분배열의 앞 쪽을 가르키는 인덱스
    - end : 부분배열의 뒤 쪽을 가르키는 인덱스
- start, end 0에서 시작
- start ≤ end 만족하면서 포인터를 이동시킴
    - 부분 배열의 합 < 구해야하는 값
        - end를 오른쪽으로 한 칸 이동하여 부분 배열의 크기를 증가
    - 부분 배열의 합 ≥ 구해야하는 값
        - start를 오른쪽으로 한칸 이동하여 부분 배열의 크기를 감소
        - 부분 배열의 합 = 구해야하는 값일 경우 경우의 수를 증가시킴

### Two-Pointer 코드
---

```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;

public class Main {

    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        String[] NM = br.readLine().split(" ");
        int N = Integer.parseInt(NM[0]);
        int M = Integer.parseInt(NM[1]);
        String[] values = br.readLine().split(" ");
        int[] A = new int[N + 1];

        for (int i = 0; i < N; i++) {
            A[i] = Integer.parseInt(values[i]);
        }

        int start = 0;
        int end = 0;
        int currentSum = 0;
        int ans = 0;

        while (end <= N) {
            if (currentSum < M) {
                currentSum += A[end++];
            } else {
                if (currentSum == M) {
                    ans++;
                }
                currentSum -= A[start++];
            }
        }

        System.out.println(ans);
    }
}
```

**참고**

[[Algorithm] Two Pointers, 투 포인터](https://ssungkang.tistory.com/entry/Algorithm-Two-Pointers-%ED%88%AC-%ED%8F%AC%EC%9D%B8%ED%84%B0)