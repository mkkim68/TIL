# Longest Increasing Subsequence
- 최장 증가 부분 수열
## DP 이용
- O(N^2)
```python
for now in range(1,n): # 맨처음엔 무조건 자기자신 하나이기 때문에 두번째부터 시작
    for before in range(now): # 자기 자신의 앞에 있는 것들하고 비교해 나감
        # 증가하는 값이라면
        if array[before] < array[now]: 
            # 이전 길이에 now 1개를 더한 값이 더 길다면 긴 값으로 변경
            if dp[now] < dp[before] + 1: 
                dp[now] = dp[before] + 1
                
# LIS의 길이는 dp에서 가장 큰 값을 의미함
answer = max(dp)
```
## 이분 탐색 이용
- O(NlogN)
```python
def binary_search(target,lis):
    start,end = 0,len(lis)-1
    while start < end:
        mid = (start + end) // 2 
        if lis[mid] == target:
            return mid
        elif lis[mid-1] < target < lis[mid]: 
            return mid
        elif target < lis[mid]:
            end = mid - 1
        else:
            start = mid + 1
    return start 

def sol():
    n = int(input())
    a = list(map(int,input().split()))
    lis = [a[0]] 
    for i in range(1,n):
        target = a[i]
        if lis[-1] < target: 
            lis.append(target)
        else:
            idx = binary_search(target,lis)
            lis[idx] = target

    return len(lis) 

print(sol())
```