---
title: "[21.07.24] 알고리즘 5주차 - second 1:1 session"
date: 2021-07-25 21:35:28 -0400
toc: true
toc_sticky: true
categories: Algorithm_Problems
---

# [5주차] 알고리즘 second 1:1 session 

<div class="notice--primary" markdown="1">
📜 [<u>2021.7.24</u> 21:00, <u>2021.7.25</u> 12:30 진행] 
</div>  

## [백준 - 에디터](https://www.acmicpc.net/problem/1406)

### 문제 설명

한 줄로 된 간단한 에디터를 구현하려고 한다. 이 편집기는 영어 소문자만을 기록할 수 있는 편집기로, 최대 600,000글자까지 입력할 수 있다.

이 편집기에는 '커서'라는 것이 있는데, 커서는 문장의 맨 앞(첫 번째 문자의 왼쪽), 문장의 맨 뒤(마지막 문자의 오른쪽), 또는 문장 중간 임의의 곳(모든 연속된 두 문자 사이)에 위치할 수 있다. 즉 길이가 L인 문자열이 현재 편집기에 입력되어 있으면, 커서가 위치할 수 있는 곳은 L+1가지 경우가 있다.

이 편집기가 지원하는 명령어는 다음과 같다.

<img width="944" alt="스크린샷 2021-07-24 오후 10 51 35" src="https://user-images.githubusercontent.com/63195670/126870532-7be6eff2-e569-4c6b-9976-8e007b9eca5d.png">  

초기에 편집기에 입력되어 있는 문자열이 주어지고, 그 이후 입력한 명령어가 차례로 주어졌을 때, 모든 명령어를 수행하고 난 후 편집기에 입력되어 있는 문자열을 구하는 프로그램을 작성하시오. 단, 명령어가 수행되기 전에 커서는 문장의 맨 뒤에 위치하고 있다고 한다.

### 입력
첫째 줄에는 초기에 편집기에 입력되어 있는 문자열이 주어진다. 이 문자열은 길이가 N이고, 영어 소문자로만 이루어져 있으며, 길이는 100,000을 넘지 않는다. 둘째 줄에는 입력할 명령어의 개수를 나타내는 정수 M(1 ≤ M ≤ 500,000)이 주어진다. 셋째 줄부터 M개의 줄에 걸쳐 입력할 명령어가 순서대로 주어진다. 명령어는 위의 네 가지 중 하나의 형태로만 주어진다.

### 출력
첫째 줄에 모든 명령어를 수행하고 난 후 편집기에 입력되어 있는 문자열을 출력한다.   

### 입출력 예

<div class="notice--primary" markdown="1">
🌝 <u>입출력 예 #1</u>     

[입력]   

    abcd
		3
		P x
		L
		P y  
      
    
[출력]    
    
      abcdyx 

🌝 <u>입출력 예 #2</u>     

[입력]   

		abc
		9
		L
		L
		L
		L
		L
		P x
		L
		B
		P y   
      
    
[출력]    
    
      yxabc   
      
      
🌝 <u>입출력 예 #3</u>     

[입력]   

		dmih
		11
		B
		B
		P x
		L
		B
		B
		B
		P y
		D
		D
		P z  
      
    
[출력]    
    
      yxz  

</div> 

### Question Clarifying & Time, Space Complexity 


	"""
	input :
	첫째 줄에는 초기에 편집기에 입력되어 있는 문자열이 주어진다.
	둘째 줄에는 입력할 명령어의 개수를 나타내는 정수 M이 주어진다.
	셋째 줄부터 M개의 줄에 걸쳐 입력할 명령어가 순서대로 주어진다.
	
	output :
	첫째 줄의 문자열에서 모든 명령어를 수행하고 난 후 편집기에 입력되어 있는 문자열을 출력한다.
	
	constraint :
	문자열은 길이가 N이고, 영어 소문자로만 이루어져 있으며, 길이는 100,000을 넘지 않는다.
	1 ≤ M ≤ 500,000
	명령어는 "L", "D", "B", "P $" 네 가지 중 하나의 형태로만 주어진다.
	명령어가 수행되기 전에 커서는 문장의 맨 뒤에 위치한다.
	
	edge case:
	
	Solution&Algorithm :
	Stack 이용 
	
	명령어에 따라 if 문 구성

	input() -> sys stdin.readline()으로 !

	[]<- ^ ->[]
	[]<-
	
	Time Complexity : O(N)
	
	Space Complexity : O(N)
	
	"""

### My Solution(Explanation) & Code

일단 Solution 함수를 선언.   

	def Solution(): 

마지막에 리턴할 answer 변수와,  커서 왼쪽 문자열을 나타내는 stack인 stack_left와 커서 오른쪽 문자열을 나타내는 stack인 stack_right을 선언하고 초기화한다.     
이 때, 처음에 커서는 가장 오른쪽에서 시작하므로, 첫째 줄에서 입력받는 문자열을 stack_left에 넣어주면 됨!

    answer = ""    
    stack_left = list(stdin.readline().strip())
    stack_right = []

다음으로는, 두번째 줄에서 입력받는 명령어의 개수를 변수 M에 대입해주자.    

    M = int(input())   

세번째 줄부터는 명령들을 순차적으로 입력받게 되므로, M만큼 for문을 돌면서 문자가 무엇인지, 그 문자에 따른 정해진 절차를 수행하도록 하면 된다.     
각 절차를 수행하는 방식을 어떻게 구현했는지는 주석 참고!

    for _ in range(M):
        order = stdin.readline().strip()

        if order == "L" and len(stack_left) != 0:
            # 커서 바로 왼쪽에 있던 글자가 커서 오른쪽으로 넘어가므로, stack_left에 있던 마지막 수를 pop() 해서 stack_right()에 append 해준다.
            stack_right.append(stack_left.pop())

        elif order == "D" and len(stack_right) != 0:
            # 커서 바로 오른쪽에 있던 글자가 커서 왼쪽으로 넘어가므로, stack_right에 있던 마지막 수를 pop() 해서 stack_left()에 append 해준다.
            stack_left.append(stack_right.pop())

        elif order == "B" and len(stack_left) != 0:
            # 커서 바로 왼쪽에 있던 글자를 삭제하는 과정이므로 그냥 stack_left에서 pop()만 해주면 끝!
            stack_left.pop()

        # "P " 다음 글자가 각각 다르므로 첫 글자만 P면 수행한다.
        elif order[0] == "P":
        	# 커서 왼쪽에 order[2] 글자를 추가하는 과정이므로 stack_left에 append 해주면 끝! 
            stack_left.append(order[2])

stack_right을 뒤집어서 stack_left와 연결해주면 되므로, reverse()와 extend()를 사용해서 뒤집어 이어 붙여주자!   

    stack_right.reverse()
    stack_left.extend(stack_right)

<div class="notice--primary" markdown="1">
🌝 <u>여기서 잠깐!</u> append()와 extend()의 차이점은 뭘까?       

📌 차이점    

list.append(x)는 리스트 끝에 x 1개를 그대로 넣는다.      
그에 비교하여 list.extend(iterable)는 리스트 끝에 가장 바깥쪽 iterable의 모든 항목을 넣는다.     

📌 예시     

	x = ['Tick', 'Tock', 'Song']     
	y = ['Ping', 'Pong']    
	x.append(y)    
	print('x:', x)    

위와 같이 append일 경우, x는 ['Tick', 'Tock', 'Song', ['Ping', 'Pong']] 가 된다.      
즉, x: ['Tick', 'Tock', 'Song', ['Ping', 'Pong']] 가 출력된다.    

그러나 extend의 경우 조금 다르다.    

	x = ['Tick', 'Tock', 'Song']     
	y = ['Ping', 'Pong']    
	x.extend(y)    
	print('x:', x)      

위와 같이 extend일 경우, x는 ['Tick', 'Tock', 'Song', 'Ping', 'Pong'] 가 된다.      
즉, x: ['Tick', 'Tock', 'Song', 'Ping', 'Pong'] 가 출력된다.     

append는 x 그 자체를 원소로 넣고 extend는 iterable의 각 항목들을 넣는 것!     
      
</div>
    
마지막으로는 answer에 stack_left를 join을 이용해 넣어주고, 리턴하면 끝!    

    return answer.join(stack_left)

<div class="notice--primary" markdown="1">
🌝 <u>여기서 잠깐!</u> .join()은 뭘까?   

📌 파이썬 join 함수 설명

함수의 모양은 아래와 같다.

	''.join(리스트)

	'구분자'.join(리스트)

join 함수는 매개변수로 들어온 리스트에 있는 요소 하나하나를 합쳐서 하나의 문자열로 바꾸어 반환하는 함수이다.

📌 ''.join(리스트)
''.join(리스트)를 이용하면 매개변수로 들어온 ['a', 'b', 'c'] 이런 식의 리스트를 'abc'의 문자열로 합쳐서 반환해주는 함수인 것입니다.

📌 '구분자'.join(리스트)
'구분자'.join(리스트)를 이용하면 리스트의 값과 값 사이에 '구분자'에 들어온 구분자를 넣어서 하나의 문자열로 합쳐줍니다.

📌 '_'.join(['a', 'b', 'c']) 라 하면 "a_b_c" 와 같은 형태로 문자열을 만들어서 반환해 줍니다.

맞다. 처음 언급했던 ''.join(리스트)는 '구분자'.join(리스트)에서 '구분자'가 그냥 공백인 것과 같습니다.

즉, 정리하자면 join함수의 찐 모양은 '구분자'.join(리스트)인 것!       
</div>
	     
### Final Code

	def Solution():
	
	    answer = ""
	
	    # 커서 왼쪽 stack 에 있는 문자열 -> 문자열 입력받아서 넣어준다.
	    stack_left = list(stdin.readline().strip())
	
	    # 커서 오른쪽에 있는 문자열
	    stack_right = []
	
	    # 두번째 줄에는 명령어의 개수를 입력받는다.
	    M = int(input())
	
	    # 명령들을 list 배열에 저장.
	    for _ in range(M):
	        order = stdin.readline().strip()
	
	        if order == "L" and len(stack_left) != 0:
	            stack_right.append(stack_left.pop())
	
	        elif order == "D" and len(stack_right) != 0:
	            stack_left.append(stack_right.pop())
	
	        elif order == "B" and len(stack_left) != 0:
	            stack_left.pop()
	
	        elif order[0] == "P":
	            stack_left.append(order[2])
	
	    stack_right.reverse()
	    stack_left.extend(stack_right)
	
	    return answer.join(stack_left)


	print(Solution())

## 백준 - [요세푸스 문제](https://www.acmicpc.net/problem/1158)

### 문제 설명

요세푸스 문제는 다음과 같다.

1번부터 N번까지 N명의 사람이 원을 이루면서 앉아있고, 양의 정수 K(≤ N)가 주어진다. 이제 순서대로 K번째 사람을 제거한다. 한 사람이 제거되면 남은 사람들로 이루어진 원을 따라 이 과정을 계속해 나간다. 이 과정은 N명의 사람이 모두 제거될 때까지 계속된다. 원에서 사람들이 제거되는 순서를 (N, K)-요세푸스 순열이라고 한다. 예를 들어 (7, 3)-요세푸스 순열은 <3, 6, 2, 7, 5, 1, 4>이다.

N과 K가 주어지면 (N, K)-요세푸스 순열을 구하는 프로그램을 작성하시오. 

### 입력
첫째 줄에 N과 K가 빈 칸을 사이에 두고 순서대로 주어진다. (1 ≤ K ≤ N ≤ 5,000)

### 출력
예제와 같이 요세푸스 순열을 출력한다.  

### 입출력 예

<div class="notice--primary" markdown="1">
🌝 <u>입출력 예 #1</u>     

[입력]   

      7 3       
      
    
[출력]    
    
      <3, 6, 2, 7, 5, 1, 4>.     

</div> 

### Question Clarifying & Time, Space Complexity 

	"""
	input :
	첫째 줄에 N(전체 원을 이루며 앉아있는 사람의 수)과 K(제거할 사람의 번째 수)가 빈 칸을 사이에 두고 순서대로 주어진다.
	
	output :
	< > 안에 요세푸스 순열을 넣어 출력한다. 문자열을 만들어 놓고 마지막에 "<" 와 ">"를 추가해야 할듯.
	
	If the input string doesn't match the input pattern,
	the function should return an empty array.
	
	constraint :
	
	edge case:
	빈 배열이 들어온다면 -1을 리턴해야 한다.
	
	Solution&Algorithm :
	한바퀴를 돌고 그다음으로 돌아올때를 대비해 값을 나머지로 바꿈
	
	Time Complexity : O(N^2)
	
	Space Complexity : O(N)
	
	"""
	
### My Solution(Explanation) & Code

일단 각 변수 `N`, `K` 를 입력받고, 1부터 N까지의 값을 가지는 `arr`를 만들어주자.  

	def solution():
	
	    N, K = map(int, input().split())
	    arr = [i for i in range(1, N + 1)]  


그 후로는, 제거될 사람들을 넣을 문자열 (리턴할 문자열에 포함할!) 과 제거될 사람의 인덱스 번호를 가지는 변수 `answer`와 `num`을 선언하고 초기화 해준다.

    answer = "" 
    num = 0  

이제 순차적으로 list를 돌면서, `K-1`씩 `num`에 더해주고, 만약 `num`이 `arr`의 길이보다 크다면, 나머지 연산을 이용하여 리스트의 처음부터 다시 생각할 수 있도록 한다!     
`num`은 그 전 `num`과 `K-1` 차이가 나고, 이를 제거하는 것이 목적이므로 `arr`에서 `pop()`해주면 끝.    
또한, 출력할 때 숫자와 숫자 사이에 `", "`이 들어가므로 이에 대한 조건도 추가해주자.

	 for t in range(N):
	       num += K - 1
	       if num >= len(arr):  
	           num = num % len(arr)
	       if answer != "":
	           answer += ", "
	       answer += str(arr.pop(num))


마지막으로, `answer` 양 끝에 `"<"`, `">"` 추가해주고 `print` 하면 완료!

    	return "<" + answer + ">"


	print(solution())

### My Final Code
	
	def solution():
	
	    N, K = map(int, input().split())
	    arr = [i for i in range(1, N + 1)]  # 맨 처음에 원에 앉아있는 사람들
	
	    answer = ""  # 제거된 사람들을 넣을 문자열
	    num = 0  # 제거될 사람의 인덱스 번호
	
	    for t in range(N):
	        num += K - 1
	        if num >= len(arr):  
	            num = num % len(arr)
	        if answer != "":
	            answer += ", "
	        answer += str(arr.pop(num))
	
	    return "<" + answer + ">"


	print(solution())

이 방법도 틀린 건 아니다. 출력은 문제 없이 나옴.    
그런데 이 문제는 `queue`를 이용해서 풀면 시간 복잡도를 더 줄일수 있다!

### Queue Solution(Explanation) & Code

일단 `collections`에서 `deque`를 import 한다.    

	from collections import deque
       
<div class="notice--primary" markdown="1">
🌝 <u>여기서 잠깐!</u> Queue는 뭘까?   

큐란 목록 한쪽 끝에서만 자료를 넣고 다른 한쪽 끝에서만 자료를 빼낼 수 있는 자료구조이다. 먼저 집어넣은 데이터가 먼저 나오는 FIFO 구조로 데이를 저장한다. 큐에 새로운 데이터가 들어오면 큐의 끝에 데이터가 추가되며(enqueue), 반대로 삭제될 때는 첫 번째 위치의 데이터가 삭제된다(dequeue).    

📌 Queue의 종류는?          

선형큐, 환형큐, 우선순위큐 등이 존재한다.    
	    

📌 Queue 구현하기         

Queue는 리스트로 구현하는 것도 가능하지만 효율적이지 않다. 리스트는 끝에 원소를 덧붙이거나, 끝에서 꺼내는 작업은 빠르지만 리스트의 맨 처음에 원소를 추가하거나 빼는 것은 느리다.       
Queue를 구현하려면, 양 끝에서 덧붙이기와 꺼내기가 빠르도록 설계된 collections.deque를 사용하거나, 파이썬에서 제공하는 Queue 모듈을 이용해 큐를 구현하는 것이 좋다.     
아니면 원소를 추가, 삭제하는데 효율적인 linked list를 활용할 수도 있다.    

📌 collections.deque 사용    

	from collections import deque
	
	# deque 선언
	dq = deque([])
	
	# deque에 데이터 추가
	dq.append()
	
	#deque의 첫번째 원소 제거
	dq.popleft()
        

📌 Queue 모듈 사용    
       
	import queue
	
	# queue 선언
	q = queue.Queue()
	
	# deque에 데이터 추가
	q.put()
	
	#deque의 첫번째 원소 제거
	q.get()
</div>

그 후로는, `deque` `numQueue`를 선언하고, 초기화해주고, 동일하게 `N`, `K`와 `answer`, `num` 을 선언하고 초기화 해주자.

	def solution():
	
	    numQueue = deque([])
	
	    N, K = map(int, input().split())
	
	    answer = ""  
	    num = 0 

이제 순차적으로 1부터  N까지를 일단 numQueue에 append를 이용해 넣어준다. 
	
	 for t in range(1, N+1):
        numQueue.append(t)  

그리고` K-1`명의 사람들은 뺀 후, 다시 맨 뒤에 넣어주고, K번째 수만 제거하여 `answer`에 붙이는 과정을 반복하면 끝!     
`answer` 중간중간에 `", "`와 `"<"`, `">"`를 붙이는 건 동일하다.    

	    for t in range(N):
	        # K-1개 만큼은 빼서 다시 뒤에 붙임
	        for i in range(K-1):
	            numQueue.append(numQueue.popleft())
	
	        # K 번째 수는 그냥 제거 후 answer에 붙인다.
	        if answer != "":
	            answer += ", "
	        answer += str(numQueue.popleft())
	
	    return "<" + answer + ">"
	
	
	print(solution())
	
### Using Queue Final Code
	
  # queue 이용해서 다시 풀어보자!

	from collections import deque
	
	
	def solution():
	
	    numQueue = deque([])
	
	    N, K = map(int, input().split())
	
	    answer = ""  # 제거된 사람들을 넣을 문자열
	    num = 0  # 제거될 사람의 인덱스 번호
	
	    for t in range(1, N+1):
	        numQueue.append(t)  # 맨 처음에 원에 앉아있는 사람들
	
	    for t in range(N):
	        # K-1개 만큼은 빼서 다시 뒤에 붙임
	        for i in range(K-1):
	            numQueue.append(numQueue.popleft())
	
	        # K 번째 수는 그냥 제거 후 붙인다.
	        if answer != "":
	            answer += ", "
	        answer += str(numQueue.popleft())
	
	    return "<" + answer + ">"
	
	
	print(solution())

	    
	    
<div class="notice--primary" markdown="1">
🌟 <u>이번 Session 의 포인트</u>    

- stack      
- extend()   
- .join()    
- Queue    
</div>

## 참고 사이트  

- [extend() 관련 참고 사이트](https://m.blog.naver.com/wideeyed/221541104629)     
- [queue 관련 참고 사이트](https://daimhada.tistory.com/107)
