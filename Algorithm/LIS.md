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
- 이렇게 한 lis 배열 결과는 실제 lis와 다름(가짜 LIS임)
```python
def binary_search(target,lis):
    start, end = 0, len(lis)-1
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
## 이분 탐색 이용해서 실제 LIS 구하는 법
- O(NlogN)
```python
import bisect  
  
# 입력 데이터  
nums = [3, 7, 5, 2, 6, 1, 4]
N = len(nums)  
  
# 가짜 LIS를 위한 배열 (길이만 유지)  
lis = []    
parent = [-1] * N  # LIS를 추적하기 위한 부모 인덱스 저장  
  
# 실제 LIS를 만들기 위한 인덱스 저장 배열  
lis_indices = []  
  
for i in range(N):  
    num = nums[i]  
    idx = bisect.bisect_left(lis, num)  # LIS 배열에서 들어갈 위치 찾기  
  
    if idx == len(lis):  
        lis.append(num)  # LIS 길이 증가  
        lis_indices.append(i)  # LIS 값이 추가될 때 인덱스 저장  
    else:  
        lis[idx] = num  # LIS 값 갱신  
        lis_indices[idx] = i  # 해당 위치에 새로운 인덱스 갱신   
  
    # 이전 숫자가 LIS의 일부라면 부모 설정 (추적을 위해)  
    if idx > 0:  
        parent[i] = lis_indices[idx - 1]  # 올바른 부모 인덱스 저장  
  
# 🔹 역추적을 통해 실제 LIS 복원  
lis_length = len(lis)  # LIS 길이  
lis_seq = [-1] * lis_length  # LIS 값 저장할 리스트  
pos = lis_indices[-1]  # LIS의 마지막 원소 인덱스  
  
for i in range(lis_length - 1, -1, -1):  
    lis_seq[i] = nums[pos]  # LIS 값을 역추적하여 저장  
    pos = parent[pos]  # 부모 인덱스를 따라가면서 복원  
  
# 결과 출력  
{  
    "가짜 LIS (길이만 유지하는 배열)": lis,  
    "진짜 LIS (실제 수열 복원)": lis_seq  
}  
  
print(lis)  
print(lis_seq)
```