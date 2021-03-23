### Two-Pointer 알고리즘이란?

 Two-Pointer 알고리즘이란 해석 그대로 2개의 포인터를 두고 검색을 한다는 의미로, 주로 정렬된 리스트에서 **서로 다른 두개의 포인터를 이용해 순차적으로 접근하면서 원하는 타겟값에 도달할때까지 포인터를 조작**하는 알고리즘이다. Two Pointer를 활용하는 대표적인 문제로 아래가 존재한다.

> 정렬된 리스트 li 에서 합이 xx가 되는 순서쌍을 모두 구하여라
li = [ 1, 2, 4, 6, 11, 14, 16, 19 ]

해당 문제를 해결 하기 위한 방법은 크게 이중 for문을 사용하는 방법과 Two-pointer를 사용하는 방법이 존재한다.

- 이중 for문
    - 이중 반복문을 활용하여 모든 쌍을 탐색해서 조건을 만족하는 결과값을 구하는 방법
    - 이중 for문을 활용하기 때문에 **시간복잡도 O(n2)**

    ```jsx
    let li = [1,2,4,6,11,14,16,19]
    let ans = 12;

    for(let i = 0; i < li.size()-1; i++) {
    	for(let j = i+1; j < li.size(); j++) {
    		if(li[i] + li[j] == ans)
    			console.log(li[i] + " " + li[j]);
    	}
    }
    ```

- Two-pointer
    - 반복문 1개로 해결 가능
    - 두개의 포인터를 두고 양쪽에서 줄여나가거나, 한방향으로 같이 가며 검색하는 것
    - 정렬이 되어 있는 경우 시**간복잡도는 O(n)**, 정렬이 되어 있지 않아도 **시간복잡도는 O(nlogn)**

    ```jsx
    let li = [1,2,4,6,11,14,16,19]
    let ans = 12;

    let left = 0;
    let right = li.length-1;

    while(left <= right) {
    	let tmp = li[left] + li[right];

    	if(tmp > ans) // 큰 경우
    		right -= 1;
    	else if(tmp < ans) // 작은 경우
    		left += 1;
    	else { // 정답인 경우
    		console.log(li[i] + " " + li[j]);
    		left += 1;
    		right -= 1;
    	}
    }
    ```

**특징**

1. 두 개의 포인터를 활용하여 주로 배열, 리스트, linked list에서 검색을 빠르게 하기 위한 알고리즘
2. 이중 반복문 보다 훨씬 빠른 알고리즘으로 정렬되어 있는 경우 O(n), 정렬되어 있지 않은 경우 O(nlogn)의 시간복잡도를 가짐

### Two Pointer 알고리즘 구현 방법

> Two Pointer 알고리즘을 구현하는 방법은 위의 알고리즘 예시처럼 Opposite(양쪽 끝에서 두개의 포인터로 시작하는 방법)과 Equal(두 개의 포인터 모두 시작부분에서 시작하는 방법)이 있다.

### 1. Opposite directional(반대방향)

![https://s3-us-west-2.amazonaws.com/secure.notion-static.com/6b6fe5e9-48b9-43ca-a395-cdca36d898d9/Untitled.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/6b6fe5e9-48b9-43ca-a395-cdca36d898d9/Untitled.png)

배열의 양쪽 끝에서 각각 시작하며 start와 end가 서로 만날때까지(모든 경우를 확인할 때까지) 아래의 경우를 반복하는 방법

1. start와 end의 합이 원하는 타겟인 경우 출력하고 start+1, end-1을 해서 다음 부분을 검색
2. start, end의 합이 원하는 타겟보다 큰 경우 end-1을 통해서 움직임(감소)
3. start, end의 합이 원하는 타겟보다 작은 경우 start+1을 통해서 움직임(증가)

```jsx
배열에서 두 원소의 합이 타겟이랑 일치하는 것을 count해서 출력하는 문제

nums // 배열
target // 타겟 합

let start = 0;
let end = nums.length;
let counts = 0;

while(start <= end) {
	let sum = nums[start] + nums[end];
	if(sum == target) {
		counts++;
		start += 1;
		end -= 1;
	}
	else if(sum < target)
		start +=1;
	else 
		end -=1;
}
return counts;
```

문제 - leetcode

- 167. Two Sum I I
- 125. Valid Palindrome
- 283. Move Zeroes
- 344. Reverse String
- 27. Remove Element

### 2. Equal directional(같은 시작방향)

해당 방법은 일정 부분 배열들 사이의 합을 구하는 문제에 적합

![https://s3-us-west-2.amazonaws.com/secure.notion-static.com/9128acb2-37ce-4a2e-9b9d-00f775085026/Untitled.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/9128acb2-37ce-4a2e-9b9d-00f775085026/Untitled.png)

*해당 방법은 Sliding Window(슬라이딩 윈도우) 방법과 상당히 유사*

둘다 배열의 첫번째 원소부터 시작하며 항상 특정 한개의 포인터가 다른 한개의 포인터보다 작거나 같다고 명시를 해야 됨. 

1. 타겟 합보다 크거나 같을때까지 하나의 포인터를 오른쪽으로 이동시켜줌
2. 크거나 같게 되면 두번째 포인터를 한칸씩 증가시켜주며 타겟과 동일한지 여부를 확인
3. 1번과 2번을 반복하며 포인터들을 지속적으로 이동시켜줌

```jsx
배열에서 부분배열의 합이 타겟이랑 일치하는 것을 고르는 문제

nums // 배열
target // 타겟 합

let start = 0;
let end = 0;
let counts = 0;

while(end <= nums.length) {
	let tmp = nums[start] + nums[end];
	if(tmp > target)
		start++;
	else if(tmp < target)
		end++;
	else
		counts++;
}
return counts;
```

문제 - leetcode

- Find the maximum sum of any contiguous subarray of size k
- 141. Linked List Cycle
- 3. Longest Substring Without Repeating Characters
- 26. Remove Duplicates from Sorted Array

### 시간복잡도

→ 배열이 정렬이 되어 있는 경우 O(n), 정렬이 되어있지 않은 경우 O(nlogn)

### 참고자료

[Two Pointer Algorithm | Two Sum Problem | Solve DS Problems in O(N) Time](https://www.youtube.com/watch?v=2wVjt3yhGwg)

[https://velog.io/@adorno10/%ED%88%AC-%ED%8F%AC%EC%9D%B8%ED%84%B0-Two-Pointer](https://velog.io/@adorno10/%ED%88%AC-%ED%8F%AC%EC%9D%B8%ED%84%B0-Two-Pointer)