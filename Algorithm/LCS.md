# Longest Common Substring
최장 공통 문자열
- 한 번에 이어진 공통 문자열 찾기
### 알고리즘
- 2차원 배열 사용 (LCS)
	- 두 문자열을 행, 열에 매칭
	- i,j == 0 일때는 0을 넣어서 마진값 설정
	- i, j가 1 이상일 때부터 검사
1. 두 문자열의 한 글자씩 비교
2. 다르면 LCS\[i]\[j]에 0 표시
3. 같으면 LCS\[i-1]\[j-1]값을 찾아 +1
4. 반복
### 코드
```python
if i == 0 or j == 0:
	LCS[i][j] = 0
elif stringA[i] == stringB[j]:
	LCS[i][j] = LCS[i-1][j-1] + 1
else:
	LCS[i][j] = 0
```
# Longest Common Subsequence
최장 공통 부분수열
- 이어지지 않아도 공통인 부분수열 찾기
## 길이 구하기
### 알고리즘
- 문자열 찾기와 같이 2차원 배열에 매칭 & 마진값 설정
1. 두 문자열 한글자씩 비교
2. 다르면 LCS\[i-1]\[j] 와 LCS\[i]\[j-1] 중에 큰 값 표시
3. 같으면 LCS\[i-1]\[j-1] + 1
4. 반복
### 코드
```python
if i == 0 or j == 0:
	LCS[i][j] = 0
elif stringA[i] == stringB[j]:
	LCS[i][j] = LCS[i - 1][j - 1] + 1
else:
	LCS[i][j] = max(LCS[i - 1][j], LCS[i][j - 1])
```
## 수열 찾기
### 알고리즘
1. LCS 배열 *가장 마지막 값*에서 시작, 결과값을 저장할 result 배열 준비
2. LCS\[i-1]\[j] 와 LCS\[i]\[j-1] 중 현재 값과 같은 값 찾기
	1. 있으면 해당 값으로 이동
	2. 없으면 result에 해당 문자를 넣고 LCS\[i-1]\[j-1] 로 이동
3. 2번 과정 반복하다가 0으로 이동하면 종료
4. result의 역순이 정답
### 코드
```python
result = []  
j, i = N, M  
while i>=0 and j>=0:  
    if LCS[i][j] == 0:  
        break  
    if LCS[i][j] == LCS[i][j-1]:  
        i, j = i, j-1  
    elif LCS[i][j] == LCS[i-1][j]:  
        i, j = i-1, j  
    else:  
        result.append(B[i-1])  
        i, j = i-1, j-1
```
- [!] 두 문자열의 길이와 인덱스를 잘 설정해야함