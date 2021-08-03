---
title: "[21.08.03] 알고리즘 7주차 - first 1:1 session"
date: 2021-08-03 23:00:28 -0400
toc: true
toc_sticky: true
categories: Algorithm_Problems
---

# [7주차] 알고리즘 first 1:1 session 

<div class="notice--primary" markdown="1">
📜 [<u>2021.8.03</u> 오전 진행] 
</div>  

## 💬 [백준 - 괄호](https://www.acmicpc.net/problem/9012) 

### 📄 문제 설명

괄호 문자열(Parenthesis String, PS)은 두 개의 괄호 기호인 ‘(’ 와 ‘)’ 만으로 구성되어 있는 문자열이다. 그 중에서 괄호의 모양이 바르게 구성된 문자열을 올바른 괄호 문자열(Valid PS, VPS)이라고 부른다. 한 쌍의 괄호 기호로 된 “( )” 문자열은 기본 VPS 이라고 부른다. 만일 x 가 VPS 라면 이것을 하나의 괄호에 넣은 새로운 문자열 “(x)”도 VPS 가 된다. 그리고 두 VPS x 와 y를 접합(concatenation)시킨 새로운 문자열 xy도 VPS 가 된다. 예를 들어 “(())()”와 “((()))” 는 VPS 이지만 “(()(”, “(())()))” , 그리고 “(()” 는 모두 VPS 가 아닌 문자열이다. 

여러분은 입력으로 주어진 괄호 문자열이 VPS 인지 아닌지를 판단해서 그 결과를 YES 와 NO 로 나타내어야 한다. 

### 📁 입력

입력 데이터는 표준 입력을 사용한다. 입력은 T개의 테스트 데이터로 주어진다. 입력의 첫 번째 줄에는 입력 데이터의 수를 나타내는 정수 T가 주어진다. 각 테스트 데이터의 첫째 줄에는 괄호 문자열이 한 줄에 주어진다. 하나의 괄호 문자열의 길이는 2 이상 50 이하이다. 

### 📁 출력

출력은 표준 출력을 사용한다. 만일 입력 괄호 문자열이 올바른 괄호 문자열(VPS)이면 “YES”, 아니면 “NO”를 한 줄에 하나씩 차례대로 출력해야 한다.

### 💭 입출력 예

<div class="notice--primary" markdown="1">
🌝 <u>입출력 예 #1</u>     

[입력]   

   ```python
6   
(())())   
(((()())()   
(()())((()))   
((()()(()))(((())))()   
()()()()(()()())()   
(()((())()(
   ```  

[출력]    

   ```python
NO   
NO   
YES   
NO   
YES   
NO	  
   ```
</div>  

<div class="notice--primary" markdown="1">
🌝 <u>입출력 예 #2</u>     

[입력]   

   ```python     
3   
((   
))   
())(()   
   ```  

[출력]    

   ```python
NO   
NO      
NO	  
   ```
</div> 

### ✏️ Question Clarifying & Time, Space Complexity 


   ```python
"""
input :
입력의 첫 번째 줄에는 입력 데이터의 수를 나타내는 정수 T가 주어진다. 
각 테스트 데이터의 첫째 줄에는 괄호 문자열이 한 줄에 주어진다. 
 

output :
만일 입력 괄호 문자열이 올바른 괄호 문자열(VPS)이면 “YES”, 아니면 “NO”를 한 줄에 하나씩 차례대로 출력

constraint :
괄호 문자열(Parenthesis String, PS)은 두 개의 괄호 기호인 ‘(’ 와 ‘)’ 만으로 구성되어 있는 문자열
하나의 괄호 문자열의 길이는 2 이상 50 이하이다.

edge case:
positions list에 값이 하나 존재

Solution&Algorithm :
stack

Time Complexity :
O(N) 

Space Complexity :
O(k) ->  stack의 최대 크기, 최악의 경우 O(N)
"""
   ```

### ✏️ My Solution(Explanation) & Code

이 문제는 사실 전에 `LeetCode`에서 풀어봤던 문제랑 비슷해서 해결방법을 찾는 것 자체는 어렵지 않았음!       
다만 작은 실수를 곳곳에 해 놓아서 쬐끔 생각보다 오래 걸렸음. ㅇㅅㅇ   
실수 줄이자!      

   
그럼 일단 `백준`이라 따로 입력을 받아야 하므로 `sys` import 해주고, `Solution` 함수를 정의해주자.       
 
   ```python
import sys

def Solution(): 
   ```

그 후, 입력 데이터의 수를 나타내는 정수인 `T`를 입력받고, 이 개수만큼 for문을 돌려 각각의 입력 데이터를 입력받아 준다.    
또한 이 문제는 **stack**을 사용할 것이므로 stack인 `stackPS`를 선언하고 초기화까지 해 놓자.

   ```python
for i in range(T):
	# stackPS 선언 및 초기화
	stackPS = []

	# 각각의 괄호 문자열 입력받는다.
	newPS = sys.stdin.readline().rstrip()
   ```

이제 for문을 빠져나왔을 때, 이미 그 전에 `"NO"` 라고 판명난 경우를 제외하고 `stackPS`이 비었는지를 검사하기 위해 `boolean` 변수 `flag`를 선언하고 `True`로 초기화한다.         

   ```python
flag = True
   ```

그 이후로는 위에서 입력받았던 괄호 문자열인 `newPS`의 괄호 하나하나를 검사하는 과정을 코드로 작성하면 된다!     
우선 for문을 통해 `newPS`를 모두 돌자.  

   ```python
for PS in newPS:
   ```
   
검사하는 문자가 여는 괄호("(") 라면 일단 stackPS에 append한다.   

   ```python
# 여는 괄호라면 일단 append!
if PS == "(":
   ```

아닌 경우, 즉, 검사하는 괄호가 닫는 괄호(`")"`)라면 세가지 경우에 따라 다르게 코드를 짜 주면 된다.   

우선 `stackPS`에 아무 괄호 문자열도 존재하지 않을 경우에는 무조건 맞지 않으므로 `print("NO")`를 해주고 `flag` 를 `False`로 돌려준 후, `break`하자.    

또한 `stackPS`에 괄호 문자열이 존재하긴 하지만, 마지막이 `")"` 일 경우 역시 맞지 않으므로 동일하게 코드 작성 해주면 됨.     

`stackPS`에 괄호 문자열이 존재하고, 마지막이 `"("` 이면 짝이 맞는 경우이므로 `pop()` 해주고 for문을 계속 돌면 된다.    
        

   ```python
else:
	# stackPS에 아무 괄호 문자열도 존재하지 않을 경우
	if not stackPS:
		print("NO")
		flag = False
		break

	# 존재하고, 마지막이 "(" 일 경우
	elif stackPS[-1] == "(":
		stackPS.pop()

	# 존재하는데, 마지막이 ")"일 경우
	else:
		print("NO")
		flag = False
		break
   ```
  

마지막으로 for문을 다 돌고 빠져나왔을 때, 이미 그 전에 `"NO"` 라고 판명난 경우를 제외하기 위해 flag가 True인 경우만을 대상으로 stackPS가 비었으면 "YES"를, 아니라면 "NO"를 출력하면 끝!     

   ```python
if flag == True:
	if not stackPS:
		print("YES")
	else:
		print("NO")
   ```   	      
   
### ✏️ Final Code

   ```python
import sys

def Solution():
    # T 입력받는다.
    T = int(sys.stdin.readline())

    for i in range(T):
        # stackPS 선언 및 초기화
        stackPS = []

        # 각각의 괄호 문자열 입력받는다.
        newPS = sys.stdin.readline().rstrip()

        flag = True

        for PS in newPS:
            # 여는 괄호라면 일단 append!
            if PS == "(":
                stackPS.append(PS)
            else:
                # stackPS에 아무 괄호 문자열도 존재하지 않을 경우
                if not stackPS:
                    print("NO")
                    flag = False
                    break

                # 존재하고, 마지막이 "(" 일 경우
                elif stackPS[-1] == "(":
                    stackPS.pop()

                # 존재하는데, 마지막이 ")"일 경우
                else:
                    print("NO")
                    flag = False
                    break
        
        if flag == True:
            if not stackPS:
                print("YES")
            else:
                print("NO")
   ```
     

## 💬 [백준 - 어두운 굴다리](https://www.acmicpc.net/problem/17266)

### 📄 문제 설명

인하대학교 후문 뒤쪽에는 어두운 굴다리가 있다. 겁쟁이 상빈이는 길이 조금이라도 어둡다면 가지 않는다. 따라서 굴다리로 가면 최단거리로 집까지 갈수 있지만, 굴다리는 어둡기 때문에 빙빙 돌아서 집으로 간다. 안타깝게 여긴 인식이는 굴다리 모든 길 0~N을 밝히게 가로등을 설치해 달라고 인천광역시에 민원을 넣었다. 인천광역시에서 가로등을 설치할 개수 M과 각 가로등의 위치 x들의 결정을 끝냈다. 그리고 각 가로등은 높이만큼 주위를 비출 수 있다. 하지만 갑자기 예산이 부족해진 인천광역시는 가로등의 높이가 높을수록 가격이 비싸지기 때문에 최소한의 높이로 굴다리 모든 길 0~N을 밝히고자 한다. 최소한의 예산이 들 높이를 구하자. **단 가로등은 모두 높이가 같아야 하고, 정수이다.**   

다음 그림을 보자.    

<img width="461" alt="스크린샷 2021-08-03 오후 10 04 59" src="https://user-images.githubusercontent.com/63195670/128020408-11a47071-dbda-4812-b291-bc9f39933b18.png">    

다음 그림은 예제1에 대한 설명이다.   

<img width="509" alt="스크린샷 2021-08-03 오후 10 07 08" src="https://user-images.githubusercontent.com/63195670/128020621-e589e099-0712-4d9e-8ef8-acd34f55dd1d.png">    

가로등의 높이가 1일 경우 0~1사이의 길이 어둡기 때문에 상빈이는 지나가지 못한다.  

아래 그림처럼 높이가 2일 경우 0~5의 모든 길이 밝기 때문에 상빈이는 지나갈 수 있다.    

<img width="512" alt="스크린샷 2021-08-03 오후 10 08 22" src="https://user-images.githubusercontent.com/63195670/128020782-e29878c4-3c14-41a5-9b2a-3d6bc44e06e3.png">   

### 📁 입력 

첫 번째 줄에 굴다리의 길이 N 이 주어진다. (1 ≤ N ≤ 100,000)   

두 번째 줄에 가로등의 개수 M 이 주어진다. (1 ≤ M ≤ N)   

다음 줄에 M 개의 설치할 수 있는 가로등의 위치 x 가 주어진다. (0 ≤ x ≤ N)   

가로등의 위치 x는 오름차순으로 입력받으며 가로등의 위치는 중복되지 않으며, 정수이다.   

### 📁 출력

굴다리의 길이 N을 모두 비추기 위한 가로등의 최소 높이를 출력한다.   

### 💭 입출력 예

<div class="notice--primary" markdown="1">
🌝 <u>입출력 예 #1</u>     

[입력]   

   ```python
5
2
2 4
   ```             
      
    
[출력]    

   ```python    
2        
   ```
   
</div> 

<div class="notice--primary" markdown="1">
🌝 <u>입출력 예 #2</u>     

[입력]   

   ```python
3
1
0
   ```             
      
    
[출력]    

   ```python    
3        
   ```
   
</div> 



### ✏️ Question Clarifying & Time, Space Complexity

   ```python
"""
input :
첫 번째 줄에 굴다리의 길이 N 이 주어진다. 

두 번째 줄에 가로등의 개수 M 이 주어진다. 

다음 줄에 M 개의 설치할 수 있는 가로등의 위치 positions 가 주어진다. 


output :
굴다리의 길이 N을 모두 비추기 위한 가로등의 최소 높이를 출력

constraint :
(1 ≤ N ≤ 100,000)
(1 ≤ M ≤ N)
(0 ≤ positions ≤ N)
가로등의 위치 x는 오름차순으로 입력받으며 가로등의 위치는 중복되지 않으며, 정수이다. 

edge case:


Solution&Algorithm :
단순히 가장 큰 거리 구해서 그 때마다 업데이트 최종 리턴

Time Complexity :
O(n) 

Space Complexity :
O(n) 
"""
   ```
	
### ✏️ My Solution(Explanation) & Code

처음 생각나는 방법은 단순히 각 가로등의 위치를 검사할 때, 그 전 가로등과의 거리를 비교해서 가장 먼 거리를 업데이트한 후, 최종 리턴하는 방식이였다.      
 

일단 `Solution` 함수를 만들고 굴다리의 길이 `N`과 가로등의 개수`M`을 입력받아 주자.  

   ```python
import sys

def Solution():

    N = int(sys.stdin.readline())
    M = int(sys.stdin.readline())
   ```

그 후로는, 한 줄에 입력받는 위치값들을 띄어쓰기를 기준으로 나누어서 list에 넣어준다!     

   ```python
positions = list(map(int, sys.stdin.readline().split()))
   ```

이제 **가장 먼 거리**를 저장할 변수 `maxDistance`를 선언하고 0으로 초기화 해준다.     

   ```python
maxDistance = 0
   ```
   
다음으로는 `edge case`인 경우인, 만약 `positions` list에 값이 하나 존재한다면, 굴다리가 시작하는 위치 0과 굴다리의 끝인 N 과의 거리 중 더 먼 값을 `maxDistance`에 저장한다.    

   ```python
if len(positions) == 1:
	maxDistance = max(positions[0] - 0, N - positions[0])
   ```

`edge case`가 아닌 경우에는 `positions`의 마지막 위치에서 굴다리의 끝인 `N`과의 거리까지 검사해야 하므로 `positions`에 `N`을 `append` 해주자.  그 후, 검사하는 위치와 그 전 위치 사이의 거리를 따져야 하므로 `beforeX`, 즉, 전 위치를 저장할 변수까지 선언 후 `0`으로 초기화!    

   ```python
else:
	positions.append(N)
	beforeX = 0
   ```

이제 거의 다 왔다. 가장 중요한 부분! `positions`를 돌면서 현재 위치랑 바로 전 위치를 `currDistance`라는 변수에 넣고, 만약 두 위치 중 하나가 `0`이나 `N`을 포함한다면 (`N`을 포함하는 건 현재 위치만 가능!) 그대로 대입. 그 경우가 아니고 짝수라면 2로 나눈 값을, 홀수라면 2로 나눈 값에 1을 더해 대입하자.         

   ```python
for currX in positions:
	currDistance = currX - beforeX 

	if currX == 0 or beforeX == 0 or currX == N:
		currDistance = currDistance

	elif currDistance % 2 == 0:
		currDistance = currDistance // 2
            
	else:
		currDistance = currDistance // 2 + 1
   ```
다음으로 기존 `maxDistance`보다 `currDistance`가 더 크다면 `maxDistance`를 업데이트하고, `beforeX`에 `currX`를 넣어주어 다음 위치를 검사할 준비까지 마쳐주면 된다.     

   ```python
if maxDistance < currDistance:
	maxDistance = currDistance 

beforeX = curr
   ```

마지막으로 `maxDistance`를 print 해주면 끝!     

   ```python
print(maxDistance)
   ```

### ✏️ My Final Code
	
   ```python
import sys

def Solution():

    N = int(sys.stdin.readline())
    M = int(sys.stdin.readline())

    positions = list(map(int, sys.stdin.readline().split()))

    maxDistance = 0

    if len(positions) == 1:
        maxDistance = max(positions[0] - 0, N - positions[0])

    else:
        positions.append(N)
        beforeX = 0

        for currX in positions:
            currDistance = currX - beforeX 

            if currX == 0 or beforeX == 0 or currX == N:
                currDistance = currDistance

            elif currDistance % 2 == 0:
                currDistance = currDistance // 2
            
            else:
                currDistance = currDistance // 2 + 1
            

            if maxDistance < currDistance:
                maxDistance = currDistance 

            beforeX = currX
    
    print(maxDistance)    

   ```


이렇게 푸는 것도 좋다. 사실 이렇게 푸는 게 ( 왜 인지는 모르겠으나 ) 시간은 더 짧게 나오긴 하지만, 이보다 시간 복잡도는 줄일 수 있는 방법이 존재한다.      
바로 **이분 탐색**<sup>Binary Search</sup>을 이용하는 것!   
사실 이 문제는 이분 탐색을 이용하는 기본문제이지만, 왜인지 찾아보면 위 방법으로 푼 경우가 더 많았던....🤔    

### ✏️ Question Clarifying & Time, Space Complexity Using Binary Search

   ```python
"""
input :
첫 번째 줄에 굴다리의 길이 N 이 주어진다. 

두 번째 줄에 가로등의 개수 M 이 주어진다. 

다음 줄에 M 개의 설치할 수 있는 가로등의 위치 positions 가 주어진다. 


output :
굴다리의 길이 N을 모두 비추기 위한 가로등의 최소 높이를 출력

constraint :
(1 ≤ N ≤ 100,000)
(1 ≤ M ≤ N)
(0 ≤ positions ≤ N)
가로등의 위치 x는 오름차순으로 입력받으며 가로등의 위치는 중복되지 않으며, 정수이다. 

edge case:


Solution&Algorithm :
이분 탐색으로 해결 가능하다

Time Complexity :
O(log N) 

Space Complexity :
O(N) 
"""
   ```
	
### ✏️ My Solution(Explanation) & Code Using Binary Search

이분 탐색 방법도 사실 어렵지 않다.       

<div class="notice--primary" markdown="1">
🌝 <strong><u>여기서 잠깐!</u> 이분 탐색은 뭘까?</strong>   

간결하게 말하자면, <strong>정렬된 자료를 반으로 나누어 탐색하는 방법</strong>이다.

📌 <strong><u>개념 ?</u></strong>          

이분 탐색은 영어로 Binary Search 로 표기하며 이진탐색이라고도 한다.     
탐색할 데이터를 반으로 나누어 값 비교 후,  그 값이 존재하는 반만 탐색하는 방식을 반복하면서 목표값을 찾는 알고리즘임!        

<strong>이분 탐색의 시간복잡도</strong>는 <strong>O(log N)</strong>이고, 빠른 속도로 목표값을 찾을 수 있다는 것이 큰 장점이다.
	    

📌 <strong><u>주의사항</u></strong>         

이 이분탐색을 할 때 주의사항이 존재한다.    
반드시 <strong><u>오름차순으로 정렬되어 있어야 한다</u></strong>는 것!    

이분 탐색은 중간값을 계속 비교해서 목표값이 중간값보다 큰지 혹은 작은지를 비교하여 탐색하는 알고리즘이기에, 오름차순으로 정렬하지 않은 채 탐색할 경우 제대로 된 값을 찾을 수 없음.      

📌 <strong><u>구현 개요</u></strong>    

1. 자료의 중간 값 (mid)이 찾고자 하는 값인지 검사
2. 아니라면 대소관계 비교 후, start값과 end값 업데이트
3. 동일 연산 반복! (재귀 혹은 while문으로 구현 가능)       

📌 <strong><u>시간복잡도 (Big-O)</u></strong>    
       
우선, 이진 탐색을 반복할수록 남아있는 (탐색할) 자료의 개수는 반으로 줄어든다!

따라서 K번째 실행시 탐색할 남은 자료의 개수 : <code>N*(1/2)<sup>K</sup></code>    
탐색이 끝나는 시점에는 남은 자료의 개수가 1이 되어야 하므로 <code>N*(1/2)<sup>K</sup> = 1</code>
양변에 2<sup>K</sup>를 곱해주면   <code>2<sup>K</sup> = N</code> → <code>K = log<sub>2</sub>N</code>이다.   

K의 의미는 실행횟수이므로 자료의 갯수 N에 따른 시행횟수는 <code>log<sub>2</sub>N</code>임.     
즉, 시간 복잡도는 <strong>BigO 표기법</strong>으로 <code>O(logN)</code>으로 나타낼 수 있다.     
</div>

우선 이진 탐색에 따로 필요한 함수는 배제하고 생각해보자.     
동일하게 굴다리의 길이 `N`과 가로등의 개수`M`을 입력받아 주자.  

   ```python
import sys

    N = int(sys.stdin.readline())
    M = int(sys.stdin.readline())
   ```


그 후로는, 양 끝에 `0`과 `N`을 추가하고, 한 줄에 입력받는 위치값들을 띄어쓰기를 기준으로 나누어서 list에 넣어준다!     

   ```python
positions = [0] + list(map(int, sys.stdin.readline().split())) + [N]
   ```

이제 `start`와 `end`를 선언 후, 각각 `0`, `N`으로 초기화하고, 가장 먼 거리를 담을 변수인 `maxDistance` 역시 선언 후 `0`으로 초기화 해주자.    

   ```python
start, end = 0, N
maxDistance = 0
   ```
   
다음으로는 `start`가 `end`보다 커지기 전까지 while문을 돌면서 이진 탐색을 실행하면 된다!     
이등분해서 어느 쪽에 속하는지 확인 후, 포위망(?)을 좁혀나가는 방식이므로 일단 `(start + end) // 2`를 `middle`에 넣어주자.     
    
   ```python
while start <= end:
    # 이등분해서 어느 쪽에 속하는지 확인 후, 포위망 좁혀나가는 식!
    middle = (start + end) // 2
   ```

만약 현재 검사하는 위치와 그 다음 위치 사이의 거리가 `middle`보다 더 작은 쪽에 존재하는 경우 (이 여부는 `Binary Search`를 구현하는 함수 `Solution`에서 판단하도록 작성해주면 된다) 에는 `maxDistance`를 `middle`로 업데이트 후, `end`를 `middle-1`로 설정해서 다시 그 안에서 이분 탐색을 실시하면 된다.      

더 큰 쪽에 존재한다면 `start`	를 `middle+1`로 설정 후 while문을 이어서 수행하면 됨.   

   ```python
while start <= end:
    # 이등분해서 어느 쪽에 속하는지 확인 후, 포위망 좁혀나가는 식!
    middle = (start + end) // 2
    if Solution(positions, middle):
        # Distance가 middle보다 더 작은 쪽에 존재할 경우
        end = middle - 1
        maxDistance = middle
    else:
        # Distance가 middle보다 더 큰 쪽에 존재할 경우
        start = middle + 1
   ```

이제 거의 다 왔다. 가장 중요한 부분! `postion`을 확인하면서 만약 `middle`보다 거리가 멀다면 `0`을 리턴하고, 모두 아니라면 `1`을 리턴하도록 하면 됨!

이 때 주의해야 할 점이 `0(position[0])`이나 `N(position[-1])`을 포함하고 있는 경우는 2로 나눈 값이 아닌, 그 자체를 가로등의 높이로 판단해야 하므로 2로 나누지 않아야 함!             
자세한 설명은 주석을 참고하자.    

   ```python
# positions와 middle을 파라미터로 받는 Solution 함수!
def Solution(positions, middle):
    if positions[1]-positions[0] > middle:
    	# 만약 0 포함 거리가 middle보다 크다면 0 리턴
        return 0
    if positions[-1]-positions[-2] > middle:
    	# 만약 N 포함 거리가 middle보다 크다면 0 리턴
        return 0
    for i in range(1, len(positions)-2):
    	# 만약 위 경우들 제외 거리가 middle보다 크다면 0 리턴
        if (positions[i+1]-positions[i])/2 > middle:
            return 0
    # 아니라면 1 리턴
    return 1
   ```
   
마지막으로 `maxDistance`를 출력해주면 끝!     

   ```python
print(maxDistance)
   ```

### ✏️ My Final Code Using Binary Search
	
   ```python
import sys

def Solution(positions, middle):
    if positions[1]-positions[0] > middle:
        return 0
    if positions[-1]-positions[-2] > middle:
        return 0
    for i in range(1, len(positions)-2):
        if (positions[i+1]-positions[i])/2 > middle:
            return 0
    return 1

N = int(sys.stdin.readline())
M = int(sys.stdin.readline())

positions = [0] + list(map(int, sys.stdin.readline().split())) + [N]

start, end = 0, N
maxDistance = 0

while start <= end:
    # 이등분해서 어느 쪽에 속하는지 확인 후, 포위망 좁혀나가는 식!
    middle = (start + end) // 2
    if Solution(positions, middle):
        # Distance가 middle보다 더 작은 쪽에 존재할 경우
        end = middle - 1
        maxDistance = middle
    else:
        # Distance가 middle보다 더 큰 쪽에 존재할 경우
        start = middle + 1
print(maxDistance)
   ```
	    
<div class="notice--primary" markdown="1">
🌟 <strong>1 Session 의 <u>포인트</u></strong>    
 - stack      
 - 이진탐색<sup>Binary Search</sup>     
</div>

## 🔗 참고 사이트  

- [Binary Search 관련 참고 사이트 1](https://riswell1992.tistory.com/4)     
- [Binary Search 관련 참고 사이트 2](https://wayhome25.github.io/cs/2017/04/15/cs-16/)
