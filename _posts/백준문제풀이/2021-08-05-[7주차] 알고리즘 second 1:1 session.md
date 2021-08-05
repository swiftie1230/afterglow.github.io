---
title: "[21.08.05] 알고리즘 7주차 - second 1:1 session"
date: 2021-08-05 17:00:28 -0400
toc: true
toc_sticky: true
categories: Algorithm_Problems
---

# [7주차] 알고리즘 second 1:1 session 

<div class="notice--primary" markdown="1">
📜 [<u>2021.8.05</u> 오전 - 점심 진행] 
</div>  

## 💬 [백준 - 다리놓기](https://www.acmicpc.net/problem/1010) 

### ✏️ 문제 설명

재원이는 한 도시의 시장이 되었다. 이 도시에는 도시를 동쪽과 서쪽으로 나누는 큰 일직선 모양의 강이 흐르고 있다. 하지만 재원이는 다리가 없어서 시민들이 강을 건너는데 큰 불편을 겪고 있음을 알고 다리를 짓기로 결심하였다. 강 주변에서 다리를 짓기에 적합한 곳을 사이트라고 한다. 재원이는 강 주변을 면밀히 조사해 본 결과 강의 서쪽에는 `N`개의 사이트가 있고 동쪽에는 `M`개의 사이트가 있다는 것을 알았다. (`N ≤ M`)

재원이는 서쪽의 사이트와 동쪽의 사이트를 다리로 연결하려고 한다. (이때 한 사이트에는 최대 한 개의 다리만 연결될 수 있다.) 재원이는 다리를 최대한 많이 지으려고 하기 때문에 서쪽의 사이트 개수만큼 (`N`개) 다리를 지으려고 한다. 다리끼리는 서로 겹쳐질 수 없다고 할 때 다리를 지을 수 있는 경우의 수를 구하는 프로그램을 작성하라.

![image](https://user-images.githubusercontent.com/63195670/128296449-92ce0a55-65c3-4313-99c9-fb190f7290ae.png) 

### ✏️ 입력

입력의 첫 줄에는 테스트 케이스의 개수 `T`가 주어진다. 그 다음 줄부터 각각의 테스트케이스에 대해 강의 서쪽과 동쪽에 있는 사이트의 개수 정수 `N`, `M` (`0 < N ≤ M < 30`)이 주어진다.

### ✏️ 출력

각 테스트 케이스에 대해 주어진 조건하에 다리를 지을 수 있는 경우의 수를 출력한다.

### ✏️ 입출력 예

<div class="notice--primary" markdown="1">
🌝 <u>입출력 예 #1</u>     

[입력]   

   ```python
3   
2 2   
1 5   
13 29   
   ```  

[출력]    

   ```python
1  
5  
67863915	   
   ```
</div>  


### ✏️ Question Clarifying & Time, Space Complexity 


   ```python
"""
input :
첫번째 줄에 테스트 케이스 수 T

그 다음 줄부터 각각의 테스트케이스에 대해 강의 서쪽과 동쪽에 있는 사이트 개수 N, M이 주어진다.


output :
각 테스트 케이스에 대해 다리끼리는 서로 겹쳐질 수 없다고 할 때, 다리를 지을 수 있는 경우의 수

constraint :
0 < N <= M < 30 

edge case:
N = M 이면 그냥 N 출력 
N이 1이라면 그냥 M 출력


Solution&Algorithm :
조합을 구하면 됨!

Time Complexity :
O(1) 

Space Complexity :
O(N) 
"""
   ```

### ✏️ My Solution(Explanation) & Code

문제 자체가 장황하지만, 수학적으로 보면 생각보다 진짜 간단하다!    
edge case인 N = M인 경우와 N = 1인 경우는 따로 작성해준 후, M개의 동쪽 사이트 중 N개를 순서 없이 선택하는 경우의 수와 동일하기 때문에 **조합**을 구하면 끝.          
   
그럼 일단 `백준`이라 따로 입력을 받아야 하므로 `sys`를 import 해주자.     그리고 우리는 각각의 경우의 수가 아닌, 전체 경우의 수만 구하면 되므로 팩토리얼을 이용해서 계산만 하면 됨!  따라서 `math`도 import 한 후, `Solution` 함수를 정의해주자.       
 
   ```python
import math 
import sys

def Solution(): 
   ```

그 후, 입력 데이터의 수를 나타내는 정수인 `T`를 입력받고, 이 개수만큼 for문을 돌려 각각의 입력 데이터인 `N`과 `M`을 입력받아 준다.    

   ```python
T = int(sys.stdin.readline())
	for i in range(T):
		N, M = map(int, sys.stdin.readline().split())
   ```

이제 `edge case` 먼저 고려해 작성해주자.   
만약 `N`이 `1`일 경우는 `M`을 출력해 준 후, 이후 for문 안은 볼 필요 없으므로 바로 `continue`!    
`N = M` 일 경우는 한가지 경우뿐이므로 `1`을 출력 후, 동일한 이유로 `continue` 해준다.          

   ```python
if N == 1:
	print(M)
	continue
if N == M:
	print(1)
	continue
   ```

그 이후로는 나머지 경우이므로 그냥 조합을 계산해서 출력해 주면 된다.    
<strong><code><sub>M</sub>C<sub>N</sub></code></strong> = <strong><code>M!/((M-N)!N!)</code></strong>이므로 이를 코드로 작성해주면 끝!     

   ```python
print(math.factorial(M) // (math.factorial(M-N) * math.factorial(N)))
   ```

<div class="notice--primary" markdown="1">
💡 <strong><u>추가 지식!</u> 파이썬에서의 팩토리얼, 순열, 조합 관련 함수들</strong>   

파이썬에서 팩토리얼, 순열, 조합 관련하여 간편하게 구할 수 있는 내장 함수가 존재할까?    
당연히 존재한다!      

📌 <strong><u>팩토리얼 함수</u> : <u>factorial()</u></strong>          

팩토리얼을 계산하는 함수는 <code>math</code>라는 라이브러리 안에 존재한다.    
따라서 이를 사용하려면 우선 <code>math</code>를 import 해 주어야 함!          

<strong>factorial()</strong>은 인자의 팩토리얼 값을 반환하며, 빠르다.     

특히 <code>math</code> 라이브러리에 있는 함수들은 <code>C</code>로 implement 되어 있는 경우가 많아 빠름!    
	    
📌 <strong><u>순열</u> : <u>permutations()</u></strong>         

순열을 계산하는 함수는 <code>itertools</code>라는 라이브러리 안에 존재한다.    
따라서 이를 사용하려면 우선 <code>itertools</code>를 import 해 주어야 함!          

<strong>permutations(iterable 객체, r)</strong>는 iterable 객체에서 <code>r</code>개의 데이터를 뽑아 <strong>일렬로 나열</strong>하는 모든 경우(순열)를 계산한다.         

이 때, 이 함수를 이용한 후에는 list() 메서드나 tuple() 메서드로 캐스팅해주어야만 한다!     

캐스팅해주지 않으면 출력할 때 <code>itertools.permutations object at 0x036B95A0'</code>와 같이 <code>0x036B95A0</code>라는 주소에 있는 객체라고만 뜸.    

따라서 우리가 원하는 값을 보고 싶다면 꼭! <strong><u>리스트나 튜플로 형태 변환</u></strong>을 시켜주어야 한다.   

   ```python
# ['A', 'B', 'C']에서 3개를 뽑아 나열하는 모든 경우
from itertools import permutations

data = ['A', 'B', 'C']

result = list(permutations(data, 3))

print(result) # [('A', 'B', 'C'), ('A', 'C', 'B'), ... , ('C', 'B', 'A')]
   ```          
       
📌 <strong><u>조합</u> : <u>combinations()</u></strong>    

순열을 계산하는 함수 역시 <code>itertools</code>라는 라이브러리 안에 존재한다.    
따라서 이를 사용하려면 우선 <code>itertools</code>를 import 해 주어야 함!          

<strong>combinations(iterable 객체, r)</strong>는 iterable 객체에서 <code>r</code>개의 데이터를 뽑아 <strong>순서 상관 없이 나열</strong>하는 모든 경우(조합)를 계산한다.         

이 때, 이 함수를 이용한 후에는 list() 메서드나 tuple() 메서드로 캐스팅해주어야만 한다!     

캐스팅해주지 않으면 출력할 때 <code>itertools.combinations object at 0x036B95A0'</code>와 같이 <code>0x036B95A0</code>라는 주소에 있는 객체라고만 뜸.    

따라서 우리가 원하는 값을 보고 싶다면 꼭! <strong><u>리스트나 튜플로 형태 변환</u></strong>을 시켜주어야 한다.   

   ```python
# ['A', 'B', 'C']에서 2개를 뽑아 순서 상관 없이 나열하는 모든 경우
from itertools import combinations

data = ['A', 'B', 'C']

result = list(combinations(data, 2))

print(result) # [('A', 'B'), ('A', 'C'), ('B', 'C')]
   ``` 
</div>

     
### ✏️ Final Code

   ```python
import math 
import sys


def Solution():
    T = int(sys.stdin.readline())
    for i in range(T):
        N, M = map(int, sys.stdin.readline().split())
        if N == 1:
            print(M)
            continue
        if N == M:
            print(1)
            continue
        print(math.factorial(M) // (math.factorial(M-N) * math.factorial(N))) 

Solution()
   ```

사실 위 방법으로 풀어도 된다.     
전혀 틀리거나 비효율적인 방법이 아님!     

🙋🏻‍♀️ **하지만 이 문제는 `Dynamic Programming`을 이용해 풀 수도 있다.**     

**`N`, `M`일 때 경우의 수**는 **`N-1`, `M-1`일 때의 경우의 수** + **`N`, `M-1` 일 때의 경우의 수**라는 사실을 이용하면 됨.    
즉, 최종 경우의 수는 마지막 서쪽의 사이트가 마지막 동쪽 사이트랑 연결되는 경우와 마지막 동쪽 사이트에 연결되지 않는 경우의 수를 더한 것과 마찬가지라는 걸 이용한 것!    

     
### ✏️ Question Clarifying & Time, Space Complexity Using Dynamic Programming


   ```python
"""
input :
첫번째 줄에 테스트 케이스 수 T

그 다음 줄부터 각각의 테스트케이스에 대해 강의 서쪽과 동쪽에 있는 사이트 개수 N, M이 주어진다.


output :
각 테스트 케이스에 대해 다리끼리는 서로 겹쳐질 수 없다고 할 때, 다리를 지을 수 있는 경우의 수

constraint :
0 < N <= M < 30 

edge case:
N = M 이면 그냥 N 출력 
N이 1이라면 그냥 M 출력


Solution&Algorithm :
DP (Dynamic Programming) 이용해서 풀기도 가능.
N, M일 때 경우의 수 = N-1, M-1일 때의 경우의 수 + N, M-1 일 때의 경우의 수

Time Complexity :
O(1) -> dp 크기 정해져 있으므로

Space Complexity :
O(1) -> dp 정해져 있으므로
"""
   ```

### ✏️ My Solution(Explanation) & Code Using Dynamic Programming     

   
그럼 일단 `백준`이라 따로 입력을 받아야 하므로 `sys` import 해주자.           
 
   ```python
import sys
   ```

그 후, 입력 데이터의 수를 나타내는 정수인 `T`를 입력받고, 최대값인 30까지의 수 `N`과 `M` 각각에 대해 계산한 조합을 저장할 2차원 배열을 선언하고 0으로 초기화한다.      

   ```python
dp = [[0]*30 for _ in range(30)]
   ```

다음으로는 for문을 이용해서 오름차순으로 각각의 2차원 배열을 채워나가면 된다.     
역시 edge case에 대해서는 따로 작성해 주고, 아닌 경우에만 `N-1`, `M-1`일 때의 경우의 수 + `N`, `M-1` 일 때의 경우의 수를 넣어주면 됨!              

   ```python
for i in range(30):
    for j in range(30):
        if i == 1:
            dp[i][j] = j
        else:
            if i == j:
                dp[i][j] = 1
            elif i < j:
                dp[i][j] = dp[i-1][j-1] + dp[i][j-1]
   ```

그 이후로는 `T`만큼 for문을 돌려 각각의 입력 데이터인 `N`과 `M`을 입력받아 준 후, 해당 조합 값을 위에서 만들었던 2차원 배열에서 찾아와서 출력해주면 끝!       

   ```python
for i in range(T):
    n, m = map(int, sys.stdin.readline().split())
    print(dp[n][m])
   ```
      
### ✏️ Final Code Using Dynamic Programming

   ```python
import sys

T = int(sys.stdin.readline())
dp = [[0]*30 for _ in range(30)]

for i in range(30):
    for j in range(30):
        if i == 1:
            dp[i][j] = j
        else:
            if i == j:
                dp[i][j] = 1
            elif i < j:
                dp[i][j] = dp[i-1][j-1] + dp[i][j-1]

for i in range(T):
    n, m = map(int, sys.stdin.readline().split())
    print(dp[n][m])
   ```


## 💬 [LeetCode - Decode String](https://leetcode.com/problems/decode-string/)

### ✏️ 문제 설명

Given an encoded string, return its decoded string.

The encoding rule is: `k[encoded_string]`, where the `encoded_string` inside the square brackets is being repeated exactly `k` times. Note that `k` is guaranteed to be a positive integer.

You may assume that the input string is always valid; No extra white spaces, square brackets are well-formed, etc.

Furthermore, you may assume that the original data does not contain any digits and that digits are only for those repeat numbers, `k`. For example, there won't be input like `3a` or `2[4]`.     

### ✏️ 입출력 예

<div class="notice--primary" markdown="1">
🌝 <u>입출력 예 #1</u>     

[입력]   

   ```python
s = "3[a]2[bc]"
   ```             
      
    
[출력]    

   ```python    
"aaabcbc"        
   ```
   
</div> 

<div class="notice--primary" markdown="1">
🌝 <u>입출력 예 #2</u>     

[입력]   

   ```python
s = "3[a2[c]]"
   ```             
      
    
[출력]    

   ```python    
"accaccacc"        
   ```
   
</div>  
 
<div class="notice--primary" markdown="1">
🌝 <u>입출력 예 #3</u>     

[입력]   

   ```python
s = "2[abc]3[cd]ef"
   ```             
      
    
[출력]    

   ```python    
"abcabccdcdcdef"        
   ```
   
</div>   

<div class="notice--primary" markdown="1">
🌝 <u>입출력 예 #4</u>     

[입력]   

   ```python
s = "abc3[cd]xyz"
   ```             
      
    
[출력]    

   ```python    
"abccdcdcdxyz"        
   ```
   
</div> 

### ✏️ Question Clarifying & Time, Space Complexity

   ```python
"""
input :
encoded s[i]


output :
Decoded s[i]

constraint :
1 <= s.length <= 30
s consists of lowercase English letters, digits, and square brackets '[]'.
s is guaranteed to be a valid input.
All the integers in s are in the range [1, 300].

edge case:



Solution&Algorithm :
숫자와 문자 구별!
숫자[문자] 형태를 숫자 * 문자 형태로 풀어서 넣어주는 게 필요할 듯
stack에 저장
3[a] -> aaa
3[a 2[c] -> cc -> 3[a2[c]] -> accaccacc

Time Complexity :
O(N) 

Space Complexity :
O(k) -> stack의 최대 크기 k, 최악의 경우 O(N) 
"""
   ```
	
### ✏️ My Solution(Explanation) & Code

이 문제에서의 푸는 데 중요했던 부분은 바로 **문자열에서 해당 부분이 문자인지 숫자인지를 판단**하는 것과, **`stack`을 이용하는 것**이었다!      

찬찬히 생각하다 보면 해결 방법 자체는 어렵지는 않은데, 찬찬히 생각을 "깊게" 해야 함. 😶‍🌫️  

우선 `Solution` 클래스에 `s`를 파라미터로 받는 함수 `decodeString`을 만들어주자.         

   ```python
class Solution:
    def decodeString(self, s):
   ```

다음으로는 숫자와 문자를 저장할 스택 역할을 해 줄 변수 `stack`을 선언해주고 초기화한다.   
또한, 현재 검사하는 문자열과 그 문자열을 몇 번 반복할지를 나타내는 숫자를 `stack`에 넣어주기 위해, 각각 변수 `string`과 `num`을 선언하고 초기화해주자.         

   ```python
stack = []
string, num = '', ''
   ```

이제 `s`의 문자 하나하나를 검사하면서 만약 문자가 숫자라면 `num`에, 알파벳이라면 `string`에 연결해준다.   
이 때 `num`만큼 `string`을 반복하는 것이 아니라, **현재 검사할 문자 전까지의 문자열을 `string`에, 그리고 현재 검사할 문자부터 시작하는 문자열을 반복하는 횟수를 `num`에 저장하는 것**이다.       

   ```python
for letter in s:
	if letter.isdigit():
		num+=letter
	elif letter.isalpha():
		string+=letter
   ```

<div class="notice--primary" markdown="1">
🌝 <strong><u>여기서 잠깐!</u> isdigit() 과 isalpha()는 뭘까?</strong>        

📌 <strong><u>isdigit() 함수</u> : <u>숫자인지 확인가능</u></strong>          

문자열의 구성문자가 숫자인지 확인할 때 사용할 수 있는 함수이다.    

문자열 전체를 넣어주면, 문자열에 숫자가 아닌 문자가 존재할 경우 False 리턴, 모두 숫자로 구성되어 있다면 True를 리턴한다.    

만약 문자열의 특정 문자를 넣어줬을 때, 해당 문자가 숫자라면 True를 리턴하고, 숫자가 아닌 알파벳, 한글, 기호, 공백 등이라면 False를 리턴한다!     

   ```python
# Example for isdigit

ex_01 = '123'
ex_02 = '010-1234-5678'
ex_03 = "전화번호010"
ex_04 = "Phone 010"

# print result of isdigit()

print(ex_01.isdigit())
print(ex_02.isdigit()) # 기호가 포함되여 False
print(ex_03.isdigit()) # 문자가 포함되어 False
print(ex_04.isdigit()) # 공백이 포함되어 False
   ```           

📌 <strong><u>isalpha() 함수</u> : <u>알파벳(또는 한글)인지 확인 가능</u></strong>         

문자열의 구성문자가 알파벳, 또는 한글인지 확인할 때 사용할 수 있는 함수이다.    

문자열 전체를 넣어주면, 문자열에 알파벳, 또는 한글이 아닌 문자가 존재할 경우 False 리턴, 모두 알파벳, 또는 한글로 구성되어 있다면 True를 리턴한다.    

만약 문자열의 특정 문자를 넣어줬을 때, 해당 문자가 알파벳, 또는 한글이면 True를 리턴하고, 알파벳, 또는 한글이 아닌 공백, 기호, 숫자 등이라면 False를 리턴한다!           

   ```python
# Example for isalpha

ex_01 = 'A'
ex_02 = 'S520'
ex_03 = "코드앵글러"
ex_04 = "Code_Angler"
ex_05 = "Code Angler"

# print result of isalpha()

print(ex_01.isalpha())
print(ex_02.isalpha()) # 숫자가 포함되여 False
print(ex_03.isalpha())
print(ex_04.isalpha()) # 기호가 포함되어 False
print(ex_05.isalpha()) # 공백이 포함되어 False
   ```
</div>
   
다음으로는 `"["`인 경우에는 새로운 괄호 안의 string이 시작되는 것을 나타내므로 그 전까지의 string과 num을 stack에 넣어주고, 이를 초기화해주면 된다.    

`"]"`인 경우에는 바로 전 `string`이 끝났다는 소리이므로 `stack`의 가장 위에 저장되어 있는 `string`과 `num`을 pop() 해 준 후, 이를 따로 `p`와 `n`에 저장해 주자.     
그리고 `string`을 그 전 문자열인 `p` 에 `n`번만큼 반복한`string`을 이어 붙여준 것으로 업데이트 해주면 끝!         

   ```python
elif letter=='[':
	stack.append((string, int(num)))
	string, num = '', ''
elif letter==']':
	p, n = stack.pop()
	string = p+string*n
   ```

마지막으로 for문을 다 돈 후, string을 리턴해주자.    

   ```python
return string
   ```

### ✏️ Final Code
	
   ```python
class Solution:
    def decodeString(self, s: str) -> str:
        stack = []
        string, num = '', ''
        for letter in s:
            if letter.isdigit():
                num+=letter
            elif letter.isalpha():
                string+=letter
            elif letter=='[':
                stack.append((string, int(num)))
                string, num = '', ''
            elif letter==']':
                p, n = stack.pop()
                string = p+string*n
            
        return string   
   ```
   	    
<div class="notice--primary" markdown="1">
🌟 <strong>2 Session 의 <u>포인트</u></strong>    

 - Dynamic Programming   
 - 파이썬에서의 팩토리얼, 순열, 조합      
 - stack
 - isdigit(), isalpha()
     
</div>

## 🔗 참고 사이트  

- [**파이썬에서의 팩토리얼, 순열, 조합** 관련 참고 사이트 1](https://velog.io/@leejaylight/파이썬-주요-라이브러리-활용)     

- [**파이썬에서의 팩토리얼, 순열, 조합** 관련 참고 사이트 2](https://mong9data.tistory.com/32)

- [**isdigit(), isalpha()** 관련 참고 사이트](https://velog.io/@code_angler/파이썬Python-문자숫자인지-확인하기isalpha-isdigit-isalnum)
