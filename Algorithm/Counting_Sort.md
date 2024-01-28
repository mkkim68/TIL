# 계수 정렬
>[!NOTE]
>O(n+k) 의 시간복잡도를 가진 정렬
> - k : 정렬을 수행할 배열의 가장 큰 값
	>- 생략되지 않고 남아있는 것은 수행시간에 영향을 끼치기 때문
	>- k < n이면 수행시간은 O(n), but 무한대로 크다면 정렬의 수행시간도 무한대가 됨

![img_1](https://blog.kakaocdn.net/dn/c4EqE0/btrAgosZxFA/mIpj3vVr10IxZdcHjzE1eK/img.gif)
![img_2](https://blog.kakaocdn.net/dn/bpfD1o/btrAj4f19DO/5UoKbXM9ojZ3QHqsszKHK1/img.gif)
## 조건
1. 데이터의 크기 범위가 제한된 경우
2. 데이터가 양의 정수인 경우
3. 가장 큰 데이터와 가장 작은 데이터의 차이가 1,000,000을 넘지 않는 경우
	- 필수 조건은 아니나 차이가 클 수록 메모리 사용이 많아짐
## Python
### 1. 리스트 자료형(배열)
```python
def counting_sort(arr):
	max_arr = max(arr)
	count = [0] * (max_arr + 1)
	sorted_arr = list()
	for i in arr: # 카운팅
		count[i] += 1
	for i in range(max_arr + 1): 
		for _ in range(count[i]): 
			sorted_arr.append(i) 
	return sorted_arr
```
- 백준 10989번 [수 정렬하기 3](https://www.acmicpc.net/problem/10989)
### 2. 딕셔너리 자료형
```python
def counting_sort(arr):
	count = dict() 
	sorted_arr = list() 
	
	for i in arr: 
		if i in count: 
			count[i] += 1 
		else: 
			count[i] = 1 
			
	for i in sorted(count.keys()): 
		for _ in range(count[i]): 
			sorted_arr.append(i) 
			
	return sorted_arr
```
- 장점
	- 데이터 크기가 제한된 경우에 메모리를 더 효율적으로 쓸 수 있음
- 단점
	- 배열 최대값이 매우 클 때 메모리를 비효율적으로 쓰게 됨
	- 음수가 존재하면 사용할 수 없음