---
title: "[21.07.22] 알고리즘 5주차 - first 1:1 session”
date: 2021-07-24 16:00:28 -0400
toc: true
toc_sticky: true
categories: Algorithm_Problems
---

# [5주차] 알고리즘 first 1:1 session 

<div class="notice--primary" markdown="1">
📜 [<u>2021.7.22</u> 00:00 진행] 
</div>  

## 프로그래머스 - 크레인 인형뽑기 게임

### 문제 설명

게임개발자인 "죠르디"는 크레인 인형뽑기 기계를 모바일 게임으로 만들려고 합니다.   
"죠르디"는 게임의 재미를 높이기 위해 화면 구성과 규칙을 다음과 같이 게임 로직에 반영하려고 합니다.

![](https://grepp-programmers.s3.ap-northeast-2.amazonaws.com/files/production/69f1cd36-09f4-4435-8363-b71a650f7448/crane_game_101.png)

게임 화면은 "1 x 1" 크기의 칸들로 이루어진 "N x N" 크기의 정사각 격자이며 위쪽에는 크레인이 있고 오른쪽에는 바구니가 있습니다. (위 그림은 "5 x 5" 크기의 예시입니다). 각 격자 칸에는 다양한 인형이 들어 있으며 인형이 없는 칸은 빈칸입니다. 모든 인형은 "1 x 1" 크기의 격자 한 칸을 차지하며 격자의 가장 아래 칸부터 차곡차곡 쌓여 있습니다. 게임 사용자는 크레인을 좌우로 움직여서 멈춘 위치에서 가장 위에 있는 인형을 집어 올릴 수 있습니다. 집어 올린 인형은 바구니에 쌓이게 되는 데, 이때 바구니의 가장 아래 칸부터 인형이 순서대로 쌓이게 됩니다. 다음 그림은 [1번, 5번, 3번] 위치에서 순서대로 인형을 집어 올려 바구니에 담은 모습입니다.

![](https://grepp-programmers.s3.ap-northeast-2.amazonaws.com/files/production/638e2162-b1e4-4bbb-b0d7-62d31e97d75c/crane_game_102.png)

만약 같은 모양의 인형 두 개가 바구니에 연속해서 쌓이게 되면 두 인형은 터뜨려지면서 바구니에서 사라지게 됩니다. 위 상태에서 이어서 [5번] 위치에서 인형을 집어 바구니에 쌓으면 같은 모양 인형 두 개가 없어집니다.

![](https://grepp-programmers.s3.ap-northeast-2.amazonaws.com/files/production/8569d736-091e-4771-b2d3-7a6e95a20c22/crane_game_103.gif)

크레인 작동 시 인형이 집어지지 않는 경우는 없으나 만약 인형이 없는 곳에서 크레인을 작동시키는 경우에는 아무런 일도 일어나지 않습니다. 또한 바구니는 모든 인형이 들어갈 수 있을 만큼 충분히 크다고 가정합니다. (그림에서는 화면표시 제약으로 5칸만으로 표현하였음)  
게임 화면의 격자의 상태가 담긴 2차원 배열 board와 인형을 집기 위해 크레인을 작동시킨 위치가 담긴 배열 moves가 매개변수로 주어질 때, 크레인을 모두 작동시킨 후 터트려져 사라진 인형의 개수를 return 하도록 solution 함수를 완성해주세요.  
 
<div class="notice--primary" markdown="1">
⚠️ <u>[제한사항]</u>

* board 배열은 2차원 배열로 크기는 "5 x 5" 이상 "30 x 30" 이하입니다.   
* board의 각 칸에는 0 이상 100 이하인 정수가 담겨있습니다.
	- 0은 빈 칸을 나타냅니다.    
	- 1 ~ 100의 각 숫자는 각기 다른 인형의 모양을 의미하며 같은 숫자는 같은 모양의 인형을 나타냅니다.    
* moves 배열의 크기는 1 이상 1,000 이하입니다.   
* moves 배열 각 원소들의 값은 1 이상이며 board 배열의 가로 크기 이하인 자연수입니다.   
</div>   

### 입출력 예
<img width="414" alt="스크린샷 2021-07-24 오후 1 40 04" src="https://user-images.githubusercontent.com/63195670/126857540-f0c722ce-0552-4078-a49b-89179f4e679f.png">

### 입출력 예에 대한 설명
<div class="notice--primary" markdown="1">
🌝 <u>입출력 예 #1</u>
인형의 처음 상태는 문제에 주어진 예시와 같습니다. 크레인이 [1, 5, 3, 5, 1, 2, 1, 4] 번 위치에서 차례대로 인형을 집어서 바구니에 옮겨 담은 후, 상태는 아래 그림과 같으며 바구니에 담는 과정에서 터트려져 사라진 인형은 4개 입니다.    

<img src="https://grepp-programmers.s3.ap-northeast-2.amazonaws.com/files/production/bb0f59c7-6b72-485a-8302-217fe53ea88f/crane_game_104.jpg">

</div> 

### Question Clarifying & Time, Space Complexity 

	"""
	input:
	board(게임 화면이 담긴 2차원 배열)
	moves(크레인 뽑을 위치?를 담은 배열)
	
	output:
	작동이 끝나서 터트려서 사라진 인형의 개수 return
	
	constraint: ( 복붙! )
	- board 배열은 2차원 배열로 크기는 "5 x 5" 이상 "30 x 30" 이하입니다.
	- board의 각 칸에는 0 이상 100 이하인 정수가 담겨있습니다.
	- 0은 빈 칸을 나타냅니다.
	1 ~ 100의 각 숫자는 각기 다른 인형의 모양을 의미하며 같은 숫자는 같은 모양의 인형을 나타냅니다.
	moves 배열의 크기는 1 이상 1,000 이하입니다.
	moves 배열 각 원소들의 값은 1 이상이며 board 배열의 가로 크기 이하인 자연수입니다.
	
	edge case: - 
	
	Solution:
	new =
	딕셔너리: 2차원 배열을 돌면서 for i for j -> j+1 : append
	-> {1: 화난 오리, 2: 오리, 오리, 강아지, ..}
	stack.pop , answer += 2
	"""

###My Solution(Explanation) & Code

일단 `board`와 `moves`를 파라미터로 하는 Solution 함수를 선언.   

	def Solution(board, moves): 

그 후로는 , 새로운 딕셔너리 `new`, 반환할 값을 저장하는 변수 `answer`, 그리고 문제에서의 바구니 역할을 하는 `stack`인 `basketStack` 등 위에서 Solution을 생각했을 때 필요한 변수들을  선언하고, 초기화해주자.

	answer = 0
	new = {}
	basketStack = []

다음으로는, 배열에서 0은 인형이 없는 칸을 의미하므로 0은 제외한,  `board` 배열에 있는 나머지 수들(인형의 종류를 나타내는 수들!)을 위에서부터 순차적으로 딕셔너리 `new`에 저장하는 방법을 생각해 보았다.    
그 이유는 이렇게 열을 기준으로 인형을 위에서부터 뽑아야 하는데, 지금 현재 주어진 `board`로는  열이 아닌 행 기준으로 보기 편하기 때문.   
그렇기 때문에 **moves에 들어오는 숫자들을 key로 해서**, 열 기준, **0을 제외한 수들**을 위에서부터 순차적으로 **딕셔너리 new에 저장**해보았다.

	for i in range(len(board)):
		    for j in range(len(board[i])):
		          if board[i][j] != 0:
		                if j + 1 not in new.keys():
		                    new[j + 1] = [board[i][j]]
		                else:
		                    new[j + 1].append(board[i][j])

`moves`에 있는 수들을 순차적으로 `basketStack`에 넣어준다. 이때, 일단 `new.keys()`에 그 열이 존재해야 하고, 존재한다면 그 `new[i]` 안에 수들도 존재해야 하므로, 이 조건은 반드시 넣어주어야 한다!  

	for i in moves:
		   if i in new.keys() and new[i]:

만약 `basketStack`의 길이가 0이라면, `new[i][0]`을 넣어주자.    

	if len(basketStack) == 0:
	                basketStack = [new[i][0]]
	     
<div class="notice--primary" markdown="1">
⚠️ <u>여기서 주의!</u>    
이 조건을 고려하지 않고 바로 비교한다면, basketStack에 어떤 값도 들어가 있지 않기 때문에 basketStack[-1]과 비교하는 과정에서 IndexError: list index out of range 라는 오류가 발생한다.
</div>

그리고 `basketStack`의 길이가 0이 아니라면, 비교 후, 같다면 `basketStack`에서는 `pop`, `answer`(터트려진 인형의 개수)을 2개 더해주고, 다르다면 `basketStack`에 `append` 해준다.

	else:
	          	    if new[i][0] == basketStack[-1]:
	                    basketStack.pop()
	                    answer += 2
	                else:
	                    basketStack.append(new[i][0])

그리고 선택된 인형은 `board`에서 빠지는 인형이므로 `del` 해주자.   

	del new[i][0]

마지막으로 `answer` 리턴해주면 끝!  

	return answer

### Final Code

	def Solution(board, moves):
	    answer = 0
	    new = {}
	    basketStack = []
	
	    # 0 제외 board 배열에 있는 수들을 위에서부터 순차적으로  moves에 들어오는 숫자들을 key로 하는 딕셔너리 new에 저장!
	    for i in range(len(board)):
	        for j in range(len(board[i])):
	            if board[i][j] != 0:
	                if j + 1 not in new.keys():
	                    new[j + 1] = [board[i][j]]
	                else:
	                    new[j + 1].append(board[i][j])
	                    
		# moves에 있는 수들을 순차적으로 basketStack에 넣어준다.
	    for i in moves:
	    	# 이때, 일단 new.keys()에 존재해야 하고, 존재한다면 그 new[i] 안에 수들도 존재해야 함.
	        if i in new.keys() and new[i]:
	            if len(basketStack) == 0:
	                basketStack = [new[i][0]]
	            else:
	            	# 마지막 인형의 종류가 같다면 basketStack에서 pop, answer도 +2 해준다. (2개 추가)
	                if new[i][0] == basketStack[-1]:
	                    basketStack.pop()
	                    answer += 2
	                else:
	                    basketStack.append(new[i][0])
	            # new배열에서는 그 인형이 사라진 것이므로 del 해줌.
	            del new[i][0]
	
	    return answer

## 백준 - [2531번] 회전 초밥 게임

### 문제 설명

회전 초밥 음식점에는 회전하는 벨트 위에 여러 가지 종류의 초밥이 접시에 담겨 놓여 있고, 손님은 이 중에서 자기가 좋아하는 초밥을 골라서 먹는다. 초밥의 종류를 번호로 표현할 때, 다음 그림은 회전 초밥 음식점의 벨트 상태의 예를 보여주고 있다. 벨트 위에는 같은 종류의 초밥이 둘 이상 있을 수 있다. 



새로 문을 연 회전 초밥 음식점이 불경기로 영업이 어려워서, 다음과 같이 두 가지 행사를 통해서 매상을 올리고자 한다.

원래 회전 초밥은 손님이 마음대로 초밥을  고르고, 먹은 초밥만큼 식대를 계산하지만, 벨트의 임의의 한 위치부터 k개의 접시를 연속해서 먹을 경우 할인된 정액 가격으로 제공한다. 
각 고객에게 초밥의 종류 하나가 쓰인 쿠폰을 발행하고, 1번 행사에 참가할 경우 이 쿠폰에 적혀진 종류의 초밥 하나를 추가로 무료로 제공한다. 만약 이 번호에 적혀진 초밥이 현재 벨트 위에 없을 경우, 요리사가 새로 만들어 손님에게 제공한다.  
위 할인 행사에 참여하여 가능한 한 다양한 종류의 초밥을 먹으려고 한다. 위 그림의 예를 가지고 생각해보자. k=4이고, 30번 초밥을 쿠폰으로 받았다고 가정하자. 쿠폰을 고려하지 않으면 4가지 다른 초밥을 먹을 수 있는 경우는 (9, 7, 30, 2), (30, 2, 7, 9), (2, 7, 9, 25) 세 가지 경우가 있는데, 30번 초밥을 추가로 쿠폰으로 먹을 수 있으므로 (2, 7, 9, 25)를 고르면 5가지 종류의 초밥을 먹을 수 있다. 

회전 초밥 음식점의 벨트 상태, 메뉴에 있는 초밥의 가짓수, 연속해서 먹는 접시의 개수, 쿠폰 번호가 주어졌을 때, 손님이 먹을 수 있는 초밥 가짓수의 최댓값을 구하는 프로그램을 작성하시오. 

### 입력
첫 번째 줄에는 회전 초밥 벨트에 놓인 접시의 수 N, 초밥의 가짓수 d, 연속해서 먹는 접시의 수 k, 쿠폰 번호 c가 각각 하나의 빈 칸을 사이에 두고 주어진다. 단, 2 ≤ N ≤ 30,000, 2 ≤ d ≤ 3,000, 2 ≤ k ≤ 3,000 (k ≤ N), 1 ≤ c ≤ d이다. 두 번째 줄부터 N개의 줄에는 벨트의 한 위치부터 시작하여 회전 방향을 따라갈 때 초밥의 종류를 나타내는 1 이상 d 이하의 정수가 각 줄마다 하나씩 주어진다. 

### 출력
주어진 회전 초밥 벨트에서 먹을 수 있는 초밥의 가짓수의 최댓값을 하나의 정수로 출력한다.   

### 입출력 예

<div class="notice--primary" markdown="1">
🌝 <u>입출력 예 #1</u>
입력    
	8 30 4 30
	7
	9
	7
	30
	2
	7
	9
	25
출력    
	5
</div> 

### Question Clarifying & Time, Space Complexity 

	"""
	input :
	첫 번째 줄
	N -> 회전 초밥 벨트에 놓인 접시의 수
	d -> 초밥의 가짓수
	k -> 연속해서 먹는 접시의 수
	c -> 쿠폰 번호
	
	두 번째 줄부터 N개의 줄
	벨트의 한 위치부터 시작해서 회전 방향을 따라갈 때 초밥의 종류를 나타내는 1 이상 d 이하의 정수가 각 줄마다 하나씩 주어진다.
	
	output :
	주어진 회전 초밥 벨트에서 먹을 수 있는 초밥의 가짓수의 최댓값을 하나의 정수로 출력!
	
	constraint :
	2 ≤ N ≤ 30,000, 2 ≤ d ≤ 3,000, 2 ≤ k ≤ 3,000 (k ≤ N), 1 ≤ c ≤ d
	
	edge case:
	
	
	Solution&Algorithm :
	일단 연속되면서 가짓수가 가장 다양한 k개의 접시들 list 를 먼저 찾는다.
	( 모두 다른 게 최댓값이 아닐 수 있으므로 노가다?하면서 최댓값 계속 업데이트해야 할 듯 )
	-> k이고, 쿠폰으로 주어진 번호가 없는 list 는 기존 가짓수 + 1 해서 바로 반환!
	
	
	Time Complexity :
	입력받아서 list 생성 : O(N + k-2) = O(N)
	가장 다양한 접시 list 찾기 : O(Nk)
	c 있는지 확인 : O(k)
	
	따라서 O(N(k+1))
	
	
	Space Complexity :
	
	O(Nk) -> currlist 가 각각 생성
	
	
	N -> 회전 초밥 벨트에 놓인 접시의 수
	d -> 초밥의 가짓수
	k -> 연속해서 먹는 접시의 수
	c -> 쿠폰 번호
	"""
	
### My Solution(Explanation) & Code

일단 시간을 줄이기 위해 단순한 input() 쓰기보다는 `sys` import 해서 각각의 변수들(`N`, `d`, `k`, `c`)을 띄어쓰기 단위로 입력받는다.   

	import sys
		def Solution():
	    	N, d, k, c = map(int, sys.stdin.readline().split())

🌝 <u>여기서 잠깐!</u> sys.stdin.readline()은 뭘까?   

한 두줄 입력받는 문제들과 다르게, 반복문으로 여러줄을 입력 받아야 할 때 input()으로 입력 받는다면 시간초과가 발생할 수 있다.   
그렇기에 반복문으로 여러 줄 입력받는 상황에서는 반드시 sys.stdin.readline()을 사용해야 시간 초과가 발생하지 않는다.    

📌 한 개의 정수를 입력받을 때    

	import sys
	a = int(sys.stdin.readline())

😨 그냥 a = sys.stdin.readline() 하면 안되나요?    
👉 sys.stdin.readline()은 한줄 단위로 입력받기 때문에, 개행문자가 같이 입력 받아진다.     
만약 3을 입력했다면, 3\n 이 저장된다는 소리!    
또한, 변수 타입이 <u>문자열 형태(str)</u>로 저장되기 때문에, 정수로 사용하기 위해서 형변환을 거쳐야 한다.

📌 정해진 개수의 정수를 한줄에 입력받을 때   

	import sys
	a,b,c = map(int,sys.stdin.readline().split())

map()은 반복 가능한 객체(리스트 등)에 대해 각각의 요소들을 지정된 함수로 처리해주는 함수이다.
위와 같이 사용한다면 a,b,c에 대해 각각 int형으로 형변환이 가능!

📌 임의의 개수의 정수를 한줄에 입력받아 리스트에 저장할 때      

	import sys
	data = list(map(int,sys.stdin.readline().split()))

split()은 문자열을 나눠주는 함수인데, 괄호 안에 특정 값을 넣어주면 그 값을 기준으로 문자열을 나누고, 아무 값도 넣어주지 않으면 공백(스페이스, 탭, 엔터 등)을 기준으로 나누어준다.

list()는 자료형을 리스트형으로 변환해주는 함수이다.    
map()은 맵 객체를 만들기 때문에, 리스트형으로 바꿔주기 위해서 list()로 감싸주었다.

📌 임의의 개수의 정수를 n줄 입력받아 2차원 리스트에 저장할 때      

	import sys
	data = []
	n = int(sys.stdin.readline())
	for i in range(n):
		data.append(list(map(int,sys.stdin.readline().split())))
		
이렇게 한다면 각 요소의 길이가 동일한 2차원 리스트도 만들 수 있고,
각각 길이가 다른 2차원 리스트도 입력 받을 수 있다.

📌 문자열 n줄을 입력받아 리스트에 저장할 때     

	import sys
	n = int(sys.stdin.readline())
	data = [sys.stdin.readline().strip() for i in range(n)]   
	
strip()은 문자열 맨 앞과 맨 끝의 공백문자를 제거한다.
아래의 예시 참고!    

👉 입력    

3   
안녕안녕      
나는 지수야    
헬륨가스 마셨더니 이렇게됐지    
👉 출력     
['안녕안녕', '나는 지수야', '헬륨가스 마셨더니 이렇게됐지']   
</div>

그 후로는, 회전 초밥 벨트에 놓인 접시를 모두 가지는 배열 `dishList` 와, 가장 많은 종류의 수를 나타내는 변수 `most` 를 선언하고 초기화 해주자.

	dishList = []
    most = 0

이제 순차적으로 N개의 접시를 입력받고, 이를 `dishList`에 append!

	for i in range(N):
        dishList.append(int(sys.stdin.readline()))

이제 dishList를 for loop을 통해 돌면서, **현재 확인하는 접시가 이미 접시 리스트에 존재하는지의 여부**를 알기 위해 필요한 배열 `currdishList`, **종류의 수**를 나타내는 변수 `count`, 그리고 마지막으로 **c (쿠폰 번호) 가 존재하는지의 여부**를 나타내는 변수 `flag` 를 선언하고 초기화한다.  

	for i in range(N):
        currdishList = []
        count = 0
        flag = 0

각각의 접시에서 시작하여 K개만큼 검사하면서 이미 존재하는지 확인 후, 없으면 count 를 하나 증가시켜 주고 `currdishList`에도 append를 해준다.  
또한, `dishList[(i+j) % N]`가 `c`라면 `flag`를 `1`로 바꿔주자.    

	for j in range(k):
        if dishList[(i+j) % N] not in currdishList:
            if c == dishList[(i+j) % N]:
                flag = 1
            count += 1
            currdishList.append(dishList[(i+j) % N])
	     
<div class="notice--primary" markdown="1">
🌝 <u>여기서 잠깐!</u>    
dishList[(i+j) % N]처럼 사용하는 이유는 <u>회전초밥</u>이기 때문이다.    
즉, 우리가 list 형태로 저장해 놓았기에 회전초밥 dishList의 <u>마지막 접시</u>에서 시작하게 되면, k개를 모두 검사하지 못한다.    
따라서 나머지를 이용하여 list의 길이보다 커지게 되면 list의 처음부터 다시 시작할 수 있도록 한 것!
</div>

각 접시에서 K개의 접시들을 검사한 후, 만약 `count`가 `K`이고(즉, `K`개의 접시들의 종류가 모두 다르고), `flag` 가 0이라면( 쿠폰 번호인 접시가 존재하지 않는다면), 이미 최댓값이므로 바로 `count + 1` 을 리턴한다.

	 if count == k and flag == 0:
          return count + 1

위 조건을 만족하지 않는 경우에는 most를 업데이트 해주면 된다.   

	most = max(most, count)

마지막으로 모든 for 문을 돌고 빠져나온 경우는 mostDishlist 중 쿠폰에 존재하는 접시가 있는 경우밖에 없으니 그냥 most 리턴! 

	return most
	

### My Final Code
	
	# 시간 초과 줄이기 위해 sys 입력 방식 사용
	import sys
	
	
	def Solution():
	    # 일단 띄어쓰기 단위로 N, d, k, c 입력받았다!
	    N, d, k, c = map(int, sys.stdin.readline().split())
	    dishList = []
	    most = 0
	
	    # 총 N개의 접시 입력받는다.
	    for i in range(N):
	        dishList.append(int(sys.stdin.readline()))
	
	    # 가장 다양한 접시 list 찾기.
	    for i in range(N):
	        currdishList = []
	        count = 0
	        flag = 0
	        for j in range(k):
	            if dishList[(i+j) % N] not in currdishList:
	                if c == dishList[(i+j) % N]:
	                    flag = 1
	                count += 1
	                currdishList.append(dishList[(i+j) % N])
	
	        # k이고 c 없으면 바로 리턴
	        if count == k and flag == 0:
	            return count + 1
	
	        most = max(most, count)
	
	    # mostDishlist 중 쿠폰에 존재하는 접시가 있는 경우밖에 없으니 그냥 리턴!
	    return most

이 방법도 틀린 건 아니다. 출력은 문제 없이 나옴.    
그런데 이 문제의 시간제한은 1초로, 이렇게 `이중 for문`을 사용해서 문제를 풀면 시간초과가 뜬다. 

따라서 이 문제는 시간 복잡도를 줄여, `sliding window`를 이용해서 푸는 것이 더 좋은 방법!

### Silding Window Solution(Explanation) & Code

일단 시간을 줄이기 위해 단순한 input() 쓰기보다는 `sys` import 해서 각각의 변수들(`N`, `d`, `k`, `c`)을 띄어쓰기 단위로 입력받는다.    
또한 각 접시가 존재하는지의 여부를 따지기 위해 `defaultdict`를 사용할 것이기 때문에 이 역시 import 해준다.

	import sys
	from collections import defaultdict
		def Solution():
    			N, d, k, c = map(int, sys.stdin.readline().split())

🌝 <u>여기서 잠깐!</u> defaultdict은 뭘까?   

defaultdict()는 딕셔너리를 만드는 dict 클래스의 서브 클래스이다.     
작동하는 방식은 거의 동일한데, defaultdict는 인자로 주어진 객체의 기본값을 딕셔너리의 초깃값으로 지정할 수 있다. 즉, defaultdict라는 말 그대로 처음 키를 지정할 때 값을 주지 않으면 해당 키에 대한 값으로 디폴트 값을 지정하겠다는 뜻!

📌 기본적인 작동방식      

	# 외부 함수이기 때문에 import 해야 한다.
	from collections import defaultdict 
	# int_dict는 디폴트 값이 int인 딕셔너리!
	int_dict = defaultdict(int)
	
위와 같이 설정을 하면 값을 지정하지 않은 키는 그 값으로 0이 지정되고, 키에 명시적으로 값을 지정하게 되면 그 값이 지정된다.    

📌 default 값으로 list를 줬을 때 작동방식    

	list_dict = defaultdict(list)
	#'key1'에 값을 지정하지 않고, 'key2'에는 'test' 라는 값을 지정해 주었다 가정하자.
위의 경우 list_dict['key1'] = [] , list_dict['key1'] = 'test' 이다.    
즉, 위와 같이 설정을 하면 값을 지정하지 않은 키는 그 값으로 빈 리스트가 지정되고, 키에 명시적으로 값을 지정하게 되면 그 값이 지정된다는 뜻!     

📌 그렇다면 defaultdict()를 언제 사용하는 것이 좋을까?
       
👉 키의 개수를 세야 하는 상황이나, 리스트, 셋의 항목을 정리해야 하는 상황에 적절하다. 
</div>

그 후로는, 동일하게 가장 많은 종류의 수를 나타내는 변수 `most` 를 선언하고 초기화 해주자.

    most = 0

이제 순차적으로 N개의 접시를 입력받고, 이를 이용하여 회전 초밥 벨트에 놓인 접시를 모두 가지는 배열 `dishList`를 만든다!    

<div class="notice--primary" markdown="1">
🌝 <u>코드를 조금 더 줄여봤음!</u>    
</div>

	dishList = [int(sys.stdin.readline()) for _ in range(N)]

회전초밥임을 고려해서 뒤에 `k`개 만큼 더 이어붙여주자.

	dishList += dishList[:k]

이제 `Silding window` 를 이용하기 위해 2개의 포인터를 선언하고 초기화!

	left = 0
    right = 0
	     
이미 존재하는지 확인하기 위해 `whetherIn` 이라는 `defaultdict` 를 생성해준다.

	 whetherIn = defaultdict(int)
	 
`보너스 접시 c`는 무조건 먹으므로 일단 추가해주고.

	whetherIn[c] += 1
	
처음에 일단 k 구간씩 `right 포인터`를 이동시키며 검사하면서 초밥의 종류를 추가하고, 개수도 1씩 추가한다. 

    while right < k:
        whetherIn[dishList[right]] += 1
        right += 1

이제 본격적으로 `Silding Window`를 구현해보자.   

우선 `right 포인터`가 `dishList`의 끝에 도착할 때까지 `while문`을 돈다.

    while right < len(dishList):

일단 most를 업데이트 해주고! ( 가장 종류가 많은 수를 가질 수 있도록 )

	most = max(most, len(whetherIn))

슬라이딩을 구현해 준다. 

<div class="notice--primary" markdown="1">
🌝 <u>자세한 설명은 주석을 참고</u>해주세요!
</div>

	# 맨 왼쪽 초밥 제거.
    whetherIn[dishList[left]] -= 1

    # 0이 되면 없다는 뜻이므로 제거해주자. 왜냐면 우리는 whetherIn의 length 로 판단하는 거니까.
    if whetherIn[dishList[left]] == 0:
        del whetherIn[dishList[left]]

    # 오른쪽 초밥을 추가.
    whetherIn[dishList[right]] += 1

    # 왼쪽 위치 + 1
    left += 1

    # 오른쪽 위치 + 1
    right += 1
	

### Silding Window Final Code
	
	# 시간 초과 줄이기 위해 sys 입력 방식 사용
	import sys
	from collections import defaultdict
	
	
	def Solution():
	    # 일단 띄어쓰기 단위로 N, d, k, c 입력받았다!
	    N, d, k, c = map(int, sys.stdin.readline().split())
	    dishList = []
	    most = 0
	
	    # 총 N개의 접시 입력받는다.
	    dishList = [int(sys.stdin.readline()) for _ in range(N)]
	
	    # 회전 초밥임을 고려
	    dishList += dishList[:k]
	
	    # sliding window 를 위한 두개의 포인터 선언
	    left = 0
	    right = 0
	
	    # 이미 존재하는지의 여부를 따지기 위해 whetherIn 이라는 defaultdict 생성
	    whetherIn = defaultdict(int)
	
	    # 보너스 접시 c는 무조건 먹으므로 일단 추가
	    whetherIn[c] += 1
	
	    # 처음에 일단 K 구간만큼 검사하면서 초밥의 종류 추가 and 1씩 추가. right 이동해준다.
	    while right < k:
	        whetherIn[dishList[right]] += 1
	        right += 1
	
	    # silding window 적용
	    while right < len(dishList):
	        # 일단 most 업데이트
	        most = max(most, len(whetherIn))
	
	        # 맨 왼쪽 초밥 제거.
	        whetherIn[dishList[left]] -= 1
	
	        # 0이 되면 없다는 뜻이므로 제거해주자. 왜냐면 우리는 whetherIn의 length 로 판단하는 거니까.
	        if whetherIn[dishList[left]] == 0:
	            del whetherIn[dishList[left]]
	
	        # 오른쪽 초밥을 추가.
	        whetherIn[dishList[right]] += 1
	
	        # 왼쪽 위치 + 1
	        left += 1
	
	        # 오른쪽 위치 + 1
	        right += 1
	
	    return most
	    
	    
<div class="notice--primary" markdown="1">
🌟 <u>이번 Session 의 포인트</u>    
- sys.stdin.readline()      
- defaultdict()   
- Silding Window    
</div>
