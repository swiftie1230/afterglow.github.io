---
title: "[21.07.29] 알고리즘 6주차 - first 1:1 session"
date: 2021-07-29 23:00:28 -0400
toc: true
toc_sticky: true
categories: Algorithm_Problems
---

# [6주차] 알고리즘 first 1:1 session 

<div class="notice--primary" markdown="1">
📜 [<u>2021.7.29</u> 23:00 진행] 
</div>  

## [LeetCode - Asteroid Collision](https://leetcode.com/problems/asteroid-collision/) 

### 문제 설명

We are given an array asteroids of integers representing asteroids in a row.

For each asteroid, the absolute value represents its size, and the sign represents its direction (positive meaning right, negative meaning left). Each asteroid moves at the same speed.

Find out the state of the asteroids after all collisions. If two asteroids meet, the smaller one will explode. If both are the same size, both will explode. Two asteroids moving in the same direction will never meet.  

### 입출력 예

<div class="notice--primary" markdown="1">
🌝 <u>입출력 예 #1</u>     

[입력]   

   ```python
aseroids = [8, -8] 
   ``` 
    
[출력]   
 
   ```python
[5, 10]   
   ```
	
</div>  

<div class="notice--primary" markdown="1">
🌝 <u>입출력 예 #2</u>     

[입력]   

   ```python
aseroids = [8, -8] 
   ```     
    
[출력]    

   ```python  
[]   
   ``` 
   
</div>

<div class="notice--primary" markdown="1">
🌝 <u>입출력 예 #3</u>     

[입력]   

   ```python
aseroids = [10, 2, -5] 
   ```       
    
[출력]    

   ```python    
[10]   
   ``` 

</div>

<div class="notice--primary" markdown="1">     
🌝 <u>입출력 예 #4</u>     

[입력]   

   ```python
aseroids = [-2, -1, 1, 2] 
   ```      
    
[출력]    

   ```python   
[-2, -1, 1, 2]   
   ``` 

</div> 

### Question Clarifying & Time, Space Complexity 


   ```python
"""
input :
array asteroids of integers representing asteriods in a row. 

For each asteroid, the absolute value represents its size, and the sign represents its direction 
(positive meaning right[->], negative meaning left[<-]). 
Each asteroid moves at the same speed.

If two asteroids meet, the smaller one will explode. 
If both are the same size, both will explode. 
Two asteroids moving in the same direction will never meet.

Exploded asteriods will not be printed out.

( 방향과 순서도 생각해야 함! )

output :
The state of the asteroids after all collisions.

Constraints:

2 <= asteroids.length <= 104
-1000 <= asteroids[i] <= 1000
asteroids[i] != 0

edge case :
방금 들어온 운석이 음수일 때, 그 전 운석 역시 음수라면 비교 X

Solution : 
일단 바로 옆에 있는 것과 비교해서 충돌 후, 존재하는지, 아니면 파괴되는지를 결정하는 것이므로 stack을 사용하는 것이 좋을 듯 하다.

stack에 차례로 저장하면서, 방금 들어온 운석으로 기존 운석을 파괴할 수 있는지 확인.

- 일단 방금 들어온 운석이 양수라면? 일단 append
- 방금 들어온 운석이 음수라면?
(stack의 길이가 0이 아니기만 하면 됨. 바로 전 운석이 양수일 때만 비교해야 함 -> 음수인 경우는 비교 안 해도 됨!)
들어온 운석만 파괴된다 -> break
둘다 파괴된다 -> pop(), break
전 운석만 파괴된다 -> pop(), continue


Time Complexity : O(n)

Space Complexity : O(kn) k: stack에서 pop() 당할 수 있는 최대의 개수

"""
   ```

### My Solution(Explanation) & Code

이 문제는 운석의 방향까지 생각해야 하는 문제이다.   
음수가 왼쪽을 향하는 운석, 양수가 오른쪽을 향하는 운석이라는 점을 기억하자.   

   
일단 `asteroids`를 파라미터로 받는 Solution 함수를 선언한다..  
 
   ```python
def Solution(asteroids): 
   ```

그 후, stack으로 풀 것이기 때문에 `asteroidStack`을 선언하고 초기화해준다.

   ```python
asteroidStack = []
   ```

이제 `asteroids` 배열을 for문을 통해 돌면서, 만약 검사하는 수가 양수면 append해주자.    

   ```python
for asteroid in asteroids:
	# 만약 들어온 수가 양수면 append
	if asteroid > 0:
		asteroidStack.append(asteroid)
   ```

들어온 수가 음수라면, 3가지 경우의 수에 따라 다르게 생각을 해 주어야 한다.    

우선 검사하는 음수인 현재 운석이 충돌 후 사라졌는지를 구분해 주기 위해 변수 `flag`를 선언하고 `True`로 초기화 해주자.     

   ```python
if asteroid < 0:
	flag = True
   ```
  
<div class="notice--primary" markdown="1">
🌝 <u>여기서 잠깐!</u> flag라는 변수의 구체적인 용도는 무엇일까?        

📌 Why   

while문이 종료된 후, flag가 True라면 사라지지 않았다는 소리이므로 후에 이 운석을 append() 해 주려는 용도임!      

</div>


우선 바로 전 운석이 음수인 경우는 append()만 해 주면 되므로, **바로 전 운석이 양수인 경우**, 즉, **충돌이 일어나는 경우**만을 생각해보자.      

첫 번째 경우로는,  **충돌 후 자신이 사라지는 경우**, 즉, **절댓값이 음수 운석이 더 작은 경우**가 있을 수 있다.     
이 때는 자신이 사라지므로 `flag`를 `False`로 바꿔주고, while문을 빠져나온 후, 다음 운석을 검사하면 됨.    

   ```python
while asteroidStack and asteroidStack[-1] > 0:
	if asteroidStack[-1] + asteroid > 0:
		flag = False
		break
   ```   	   
 
두 번째 경우로는 **둘다 사라지는 경우**, 즉, **절댓값이 동일한 경우**가 있을 것이다.    
이때 역시 자신이 사라지므로 `flag`를 `False`로 바꿔주는 건 맞지만, 추가로 그 전 운석도 사라지므로 `pop()` 까지 한 후 `break`을 해주자.     

   ```python
if asteroidStack[-1] + asteroid == 0:
	flag = False
	asteroidStack.pop()
	break
   ``` 
마지막으로 **자신이 사라지지 않고, 그 전 운석이 사라지는 경우**, 즉, **절댓값이  음수 운석이 더 큰 경우**가 존재한다.   
이럴 때는 그 전 운석이 사라지므로 `pop()`만 해주고, 자신이 사라지거나 운석 배열 끝에 도달할 때까지 while문을 이어서 돌아야 하므로 `break`는 해주지 않는다.     

   ```python
else:
	asteroidStack.pop()
   ```

이제 while문 안쪽 코드 작성은 끝났다! 만약 while문을 다 돌았는데, `flag`가 `True`라면 음수 운석이 사라지지 않았다는  뜻이므로 `append()`를 해 주면 된다.    

   ```python
 if flag == True:
	asteroidStack.append(asteroid)
   ```
   
마지막으로 `asteroidStack`을 return 해주면 끝!    
   ```python
return asteroidStack
   ```
   
   
### Final Code


   ```python
class Solution:
    def asteroidCollision(self, asteroids):
        asteroidStack = []

        for asteroid in asteroids:
            # asteroid가 양수이면 append
            if asteroid > 0:
                asteroidStack.append(asteroid)

            # asteroid가 음수이면, 우선 asteroidStack에 운석 존재하는지 확인
            if asteroid < 0:
                flag = True

                # 있고, 바로 전이 음수가 아닌 양수일 때
                while asteroidStack and asteroidStack[-1] > 0:
                    # 만약 자신이 사라진다면 flag = False 
                    if (asteroidStack[-1] + asteroid) > 0:
                        flag = False
                        break

                    # 둘 다 사라지는 경우에는 pop과 false 둘다 해 주어야 한다.
                    if (asteroidStack[-1] + asteroid) == 0:
                        asteroidStack.pop()
                        flag = False
                        break

                    # 아니라면, 자신이 사라지기 전까지 pop()해준다.       
                    else:
                        asteroidStack.pop()
                
                # 자신이 사라진 경우가 아닐 때만 append 해준다.
                if flag == True:
                    asteroidStack.append(asteroid)
                
        
        return asteroidStack
   ```
     

## [LeetCode - Count Square Submatrices with All Ones](https://leetcode.com/problems/count-square-submatrices-with-all-ones/)

### 문제 설명

Given a m * n matrix of ones and zeros, return how many square submatrices have all ones.

### 입출력 예

<div class="notice--primary" markdown="1">
🌝 <u>입출력 예 #1</u>     

[입력]   

   ```python
matrix = [[0,1,1,1],[1,1,1,1],[0,1,1,1]] 
   ```             
      
    
[출력]    

   ```python    
15         
   ```
   
</div> 

<div class="notice--primary" markdown="1">
🌝 <u>입출력 예 #2</u>     

[입력]   

   ```python
matrix = [[1, 0, 1],[1, 1, 0],[1, 1, 0]] 
   ```             
      
    
[출력]    

   ```python    
7         
   ```
   
</div> 


### Question Clarifying & Time, Space Complexity 

   ```python
"""
input :
m * n matrix of ones and zeros.

output :
return how many square submatrices have all ones.
변의 길이가 n인 정사각형이 몇 개 존재하는지를 모두 더해 리턴!

Constraints:

- 1 <= arr.length <= 300
- 1 <= arr[0].length <= 300
- 0 <= arr[i][j] <= 1

edge case :



Solution : 
"맨 왼쪽 위 꼭짓점"을 matrix를 돌면서 정해 놓은 후, 가능한 정사각형 모두 더한다.


Time Complexity : 
O(mn * k^2) -> 이때 k는 각각에서 가능한 최대 정사각형의 변의 길이(최악의 경우는 다 1이다가 마지막 줄에서 0 나오는 경우겠지?)

Space Complexity : O(mn) -> matrix

"""
   ```
	
### My Solution(Explanation) & Code

처음 생각했던 전체 Solution을 한번 정리해보자. 우선 `matrix`의 값들을 하나씩 검사하면서 만약 값이 `0`이 아니라면, (일단 변의 길이가 `1`인 정사각형을 그 자체로서 만족하므로) `answer`에 1을 더해주고, 그 후로는 큰 정사각형 범위의 값들을 하나씩 검토하면서 만약 모두 존재한다면 1씩 더해주는 방식을 채택했다.

이 해결 방법으로 이제 코드를 작성해 보자. 

일단 Solution 클래스 안에 `matrix`를 파라미터로 가지는 `countSquares `함수를 선언하고, 마지막에 반환할 값인 `answer`까지 선언하고 초기화해준다.     

   ```python
class Solution:
    def countSquares(self, matrix):
        answer = 0 
   ```

그 후로는, `matrix`를 돌면서 일단 검사하는 값이 0이 아니라면 answer 에 1을 더해준다. 

   ```python
if matrix[i][j] != 0:
	# 자신이 0이 아니면 일단 길이가 1인 정사각형 그 자체 만족하므로 answer += 1
	answer += 1
   ```

이제 검사하는 해당 값을 정사각형 가장 왼쪽이면서 위 꼭짓점이라고 가정했을 때, 큰 정사각형이 존재하는지 확인해 주어야 함! (진짜 노가다 방식)     
우선 해당 정사각형이 `matrix`의 범위 밖을 넘어가지는 않아야 하므로 최대 정사각형의 길이를 정해주자.    
 
   ```python
# matrix 길이 이상을 넘어가는 정사각형은 고려하지 않아야 하므로 min값을 구해서 range를 정한다.
maxSquareRange = min(len(matrix) - i, len(matrix[0]) - j)
   ```

다음으로는 변의 길이가 `n`인 정사각형을 만들 수 있는지를 확인하는 함수를 따로 작성한다. 만들 수 있다면 `True`, 아니라면 `False`를 리턴하는 함수임!    

이는 단순하게 `n` 범위 내의 모든 칸을 확인하면서, 만약 `0`이 들어간 칸이 존재한다면 바로 `False`리턴, 모두 통과한다면 `True`를 리턴하게 만들어 주었다.   

   ```python
def countBigSquares(self, matrix, i, j, n):
	for column in range(n+1):
		for row in range(n+1):
			if matrix[i+column][j+row] == 0:
				return False
	return True
   ```

이제 거의 다 왔다. 각각의 칸을 검토하는 부분에서 `1`부터 `maxSquareRange`까지의 범위만큼을 파라미터 `n`으로 하여 `countBigSquares`를 돌린 후, 만약 `True`가 나오면 `answer`에 1씩 더해주면 끝!   
이 때, 만약 `False`라면 더 큰 정사각형은 당연히 만들어질 수 없으므로 바로 break 해준다.    

   ```python
for m in range(1, maxSquareRange):
	# 존재한다면 answer에 1 더한다.
	if self.countBigSquares(matrix, i, j, m) == True:
		answer += 1
                        
	# 0이 나오면 더 큰 정사각형은 당연히 만들어질 수 없음. 따라서 break
	else:
		break
   ```

마지막으로 `answer`을 리턴해주면 끝!   

   ```python
return answer
   ```

### My Final Code
	
   ```python
class Solution:
    def countSquares(self, matrix):
        answer = 0

        for i in range(len(matrix)):
            for j in range(len(matrix[i])):
                if matrix[i][j] != 0:
                    # 자신이 0이 아니면 일단 길이가 1인 정사각형 그 자체 만족하므로 answer += 1
                    answer += 1
                    
                    # matrix 길이 이상을 넘어가는 정사각형은 고려하지 않아야 하므로 min값을 구해서 range를 정한다.
                    maxSquareRange = min(len(matrix) - i, len(matrix[0]) - j)
                    
                    for m in range(1, maxSquareRange):
                        # 존재한다면 answer에 1 더한다.
                        if self.countBigSquares(matrix, i, j, m) == True:
                            answer += 1
                        
                        # 0이 나오면 더 큰 정사각형은 당연히 만들어질 수 없음. 따라서 break
                        else:
                            break
        return answer
    
    # 변의 길이가 n인 정사각형을 만들 수 있는지 확인하는 함수
    # 만들 수 있으면 True, 아니라면 False 리턴한다.
    def countBigSquares(self, matrix, i, j, n):
        for column in range(n+1):
            for row in range(n+1):
                if matrix[i+column][j+row] == 0:
                    return False
        return True
   ```

사실 위 방법은 하나하나 따지는, 굉장히 비효율적인 해결 방법이다.    

이 문제는 **DP**, 즉, **Dynamic Programming** 방법을 이용하면 훨씬 더 효율적으로 해결할 수 있음!

<div class="notice--primary" markdown="1">
🌝 <u>여기서 잠깐!</u> Dynammic Programming은 뭘까?       

📌 정의   

큰 문제를 작은 문제로 나누어 푸는 방법을 일컫는 말이다.    
한국어로는 동적 계획법이라고도 한다.        

📌 Divide and Conquer(분할 정복) 와의 차이점     

거의 비슷하지만 작은 문제가 중복이 일어나느냐의 여부에서 결정적인 차이점이 존재한다.     
분할 정복은 단순히 큰 문제를 해결하기 어려워 작은 문제로 나누어 푸는 방법이기에 작은 문제에서 반복이 일어나는 부분이 없다.      
그에 반해 Dynamic Programming은 작은 부분 문제들이 반복되는 것을 이용해 풀어나가는 방법임!       

다시 말해, <u>Dynamic Programming은 Memoziation이 사용된다는 점에서 분할 정복과 다르다</u>고 할 수 있다.

📌 조건          

1. 작은 문제가 반복이 일어나야 한다.    
2.  같은 문제는 구할 때마다 정답이 같다.     

📌 Memoization          

Dynamic Programming에서는 작은 문제들이 반복되고 이 작은 문제들의 결과값이 항상 같기 때문에, 한 번 계산한 작은 문제들에 대한 값을 저장해 놓고 다시 사용한다.  이를 바로 Memoization 이라 하는 것!       

즉, <u>Dynamic Programming이란 하나의 문제를 단 한 번만 풀도록 하는 알고리즘</u>이라 할 수 있다!    

📌 Bottom-up 과 Top-down          

Bottom-up은 작은 문제부터 차근차근 구해나가는 방법인 반면, Top-down은 큰 문제를 풀 때, 작은 문제가 아직 풀리지 않은 경우, 그제서야 작은 문제를 해결하는 방법이다. 즉, 재귀함수로 구현하는 경우가 대부분 Top-down이라고 생각하면 편리하다.              
      
</div>


### Question Clarifying & Time, Space Complexity Using Dynamic Programming 

   ```python
"""
input :
m * n matrix of ones and zeros.

output :
return how many square submatrices have all ones.
변의 길이가 n인 정사각형이 몇 개 존재하는지를 모두 더해 리턴!

Constraints:

- 1 <= arr.length <= 300
- 1 <= arr[0].length <= 300
- 0 <= arr[i][j] <= 1

edge case :


Solution : 
matrix[i][j]가 0이 아니라면 주변의 4개 점들에 저장한 값 중 min값 + 현재 변의 길이가 1인 정사각형의 수(1)를 더한다고 생각하면 됨. (현재 점을 가장 끝 점으로 하는 정사각형의 수를 세는 것!)


Time Complexity : 
O(mn)

Space Complexity : O(mn)

"""
   ```
	
### Solution(Explanation) & Code

전체 Solution을 한번 정리해보자. 이 **문제의 핵심은 matrix[i][j]가 0이 아니라면 주변의 4개 점들에 저장한 값 중 min값 + 현재 변의 길이가 1인 정사각형의 수(1)를 더하는 것**이다! 

일단 동일하게 Solution 클래스 안에 `matrix`를 파라미터로 가지는 `countSquares `함수를 만들어주자.    

   ```python
class Solution:
    def countSquares(self, matrix):
   ```
그 후로는, `matrix`의 칸 하나하나를 `2중첩 for문`을 통해 돌면서, 만약 해당 값이 `0`이 아니라면, **주변의 4개의 점들에 저장된 값중 최솟값**에 `1`(해당 칸은 그 자체로 변의 길이가 1인 정사각형이므로)을 더해준다. 

   ```python
for i in range(1, len(matrix)):
	for j in range(1, len(matrix[0])):
		# matrix[i][j]가 0이 아니라면 
		if matrix[i][j]:
				# 주변의 점들 중 min값 + 현재 변의 길이가 1인 정사각형의 수를 더한다고 생각하면 됨. (현재 점을 가장 끝 점으로 하는 정사각형의 수를 세는 것!)
				matrix[i][j] = min(matrix[i-1][j], matrix[i][j-1], matrix[i-1][j-1]) + 1
   ```

이제 최종 return할 answer를 선언하고 초기화 해준 후, matrix를 돌면서 answer에 모든 칸에 저장된 값을 더해주고 최종 값을 리턴하면 끝!
 
   ```python
answer = 0

for p in range(len(matrix)):
	answer += sum(matrix[p])
        
return answer
   ```

### Final Code Using Dynamic Programing 


	
   ```python
class Solution:
    def countSquares(self, matrix):
        
        for i in range(1, len(matrix)):
            for j in range(1, len(matrix[0])):
                # matrix[i][j]가 0이 아니라면 
                if matrix[i][j]:
                    # 주변의 점들 중 min값 + 현재 변의 길이가 1인 정사각형의 수를 더한다고 생각하면 됨. (현재 점을 가장 끝 점으로 하는 정사각형의 수를 세는 것!)
                    matrix[i][j] = min(matrix[i-1][j], matrix[i][j-1], matrix[i-1][j-1]) + 1

        answer = 0

        for p in range(len(matrix)):
            answer += sum(matrix[p])
        
        return answer
   ```
	    
<div class="notice--primary" markdown="1">
🌟 1 Session 의 <u>포인트</u>    
 - stack      
 - Dynamic Programming     
</div>

## 참고 사이트  

- [Dynamic Programming 관련 참고 사이트 1](https://galid1.tistory.com/507)     
- [Dynamic Programming 관련 참고 사이트 2](https://blog.naver.com/ndb796/221233570962)
