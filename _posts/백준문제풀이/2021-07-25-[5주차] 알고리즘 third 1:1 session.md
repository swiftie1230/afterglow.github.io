---
title: "[21.07.25] 알고리즘 5주차 - second 1:1 session"
date: 2021-07-28 15:35:28 -0400
toc: true
toc_sticky: true
categories: Algorithm_Problems
---

# [5주차] 알고리즘 third 1:1 session 

<div class="notice--primary" markdown="1">
📜 [<u>2021.7.25</u> 11:00 진행] 
</div>  

## 12번

### 문제 설명

Write a function that takes in a sorted array of distinct integers and returns the first index in the array that is equal to the value at that index.    
In other words, your fucntion should return the minimum index where `index == array[index]`.    
If there is no such index, your function should return `-1`.  

### 입출력 예

<div class="notice--primary" markdown="1">
🌝 <u>입출력 예 #1</u>     

[입력]   

      array = [-5, -3, 0, 3, 4, 5, 9] 
      
    
[출력]    
    
      3 //  3 == array[3]    

</div> 

### Question Clarifying & Time, Space Complexity 
* First Raw-Thinking

	```python
	"""
	input :
	a "sorted array" of "distinct" integers
	서로 다른 정수로 이루어진 정렬된 배열
	
	output :
	return the first index in the array that is equal to the value at that index.
	즉, index 와 동일한 값을 가지는 배열 값 중  첫번째 값의 index 를 리턴하라는 말이다.
	
	If there is no such index, your function should return -1.
	그러한 index 가 존재하지 않는다면, 당신의 function 은 -1을 리턴해야 한다.
	
	constraint :
	
	
	edge case:
	빈 배열이 들어온다면 -1을 리턴해야 한다.
	
	Solution&Algorithm :
	일단 array 를 한 번 for loop 을 이용하여 돌면서 같은지 확인한다.
	만약 같고, 그 전에 정해진 값이 없다면 바로 return.
	
	
	Time Complexity : 최악의 경우 O(N)
	
	Space Complexity : O(N)
	
	"""
	```

### Solution(Explanation) & Code

사실 처음에 떠올랐던 방법은 매우 간단했다.    

* 일단 `array`를 파라미터로 받는 Solution 함수를 선언.  
 
	```python
	def Solution(array): 
	```

* 그 후, `array`를 for loop을 통해 돌면서 만약 index와 동일한 값을 찾으면 바로 리턴하게 하면 끝이다.   
만약 찾지 못했다면 `-1`을 반환하는 것까지 꼼꼼하게 추가해주자.

	```python
	for i in range(len(array)):
	        if array[i] == i:
	            return i
	    return -1
	```

	     
### My Final Code

* First Raw-Thinking

	```python
	def solution(array):
	    for i in range(len(array)):
	        if array[i] == i:
	            return i
	    return -1
	```


하지만 이 문제를 조금 더 깊게 고민해 보면 정렬된 array라는 점이 눈에 들어올 것이다.       
이를 생각하여 array를 반으로 나눈 후, 왼쪽 부분은 뒤에서부터, 오른쪽 부분은 동일하게 앞에서부터 검사하면 조금 더 효율적인 해결코드를 짤 수 있음!     

특히 index와 같은 값이 `array`의 중간에 위치할 경우, 훨씬 빠르게, 효율적으로 구할 수 있다.

### Question Clarifying & Time, Space Complexity 
* Second Thinking

	```python
	"""
	11:04 - 11:34
	input:
	서로 다른 integer 를 갖는 sorted array
	
	output:
	값 = index ( 최소 )  값을 리턴
	없다면, -1
	
	constraint:
	입력으로 들어오는 배열의 값들이 서로 다 다르다.
	
	edge case:
	빈 배열 -> 그냥 -1 바로 리턴?
	
	solution:
	반 나누고 그 전 먼저 가장 큰 인덱스부터 검사 -> 만약 인덱스보다 더 작으면 굳이 검사 필요 X
	나머지 경우,
	for 문으로 array 를 돌면서 index 랑 값이 같은지 확인해서 나오면 그냥 바로 리턴 ( 최솟값 )
	끝까지 돌았으면 -1
	
	Time:
	O(N) -> 최악의 경우
	
	Space:
	O(N) -> 처음 array ?
	"""
	```

### Solution(Explanation) & Code

두 번째 방법도 사실 간단하다!      

* 일단 `array`를 파라미터로 받는 Solution 함수를 선언.  
 
	```python
	def Solution(array): 
	```

* 그 후, `array`의 길이가 0이라면 바로 -1을 리턴하는 edge case도 추가해주자.

	```python
	if len(array) == 0:
	    return -1
	```
	
* 다음으로, array를 반으로 나누었을 때의 왼쪽 부분을 뒤에서부터 검사하는 코드를 짜야 한다.    

<div class="notice--primary" markdown="1">
🌝 <u>여기서 잠깐!</u> 뒤에서부터 검사하는 이유는 뭘까?       

📌 Reason   

뒤에서부터 검사하는 이유는, 정렬된 값들이므로 만약 해당 index의 array 값이 index보다 작다면 그 앞은 검사할 필요가 없어지기 때문!    

다만, 뒤에서부터 검사하면 해당 index의 array 값이 index와 같다고 해서 그것이 반드시 최솟값이라는 보장은 할 수 없으므로, min을 통해 비교해주어야 한다.    

</div>

* 위의 `여기서 잠깐!`에서와 같이 최솟값이라는 보장이 없으므로, 최솟값을 저장해 줄 변수 mini까지 선언해주고 이를 가장 큰 값인 `len(array)`로 초기화해주자.

	```python
	mini = len(array)
	```
* 앞 부분은 뒤에서부터 검사! 자세한 설명은 주석에 달아놓았다.    

	```python
	# 앞 부분은 뒤에서부터 검사
	for i in range(len(array)//2, -1, -1):
	    # 만약 해당 index의 array 값이 index보다 더 작다면 바로 break
	    if array[i] < i:
	        break
	    # 같다면 mini 업데이트
	    if array[i] == i:
	        mini = min(mini, i)
	# mini와 len(array)가 같다는 건 바로 break되었다는 뜻이므로, 이 경우를 제외하고 mini를 리턴해주자.
	if mini != len(array):
	    return mini	
	```
* 앞 부분에서 mini가 나오지 않았다면 뒷 부분을 검사해주자. 뒷 부분은 동일하게 앞에서부터 검사해주면 끝!    
값이 없다면 `-1`을 리턴해주는 것도 추가해준다.

	```python
	for i in range(len(array)//2, len(array)):
	    if array[i] == i:
	        return i
	
	return -1
	```
     
### Final Code

* Second-Thinking

	```python
	def solution(array):
	    if len(array) == 0:
	        return -1
	
	    mini = len(array)
	
	    for i in range(len(array)//2, -1, -1):
	        if array[i] < i:
	            break
	        if array[i] == i:
	            mini = min(mini, i)
	
	    if mini != len(array):
	        return mini
	
	    for i in range(len(array)//2, len(array)):
	        if array[i] == i:
	            return i
	
	    return -1
	```



## 11번

### 문제 설명

Your're given two non-empty strings. The first one is a pattern consisting of only `"x"`s and/or `"y"`s; the other one is a normal string of alphanumeric characters. Write a function that checks whether the normal string matches the pattern.    

A string `S0` is said to match a pattern if replacing all `"x"`s in the pattern with some non-empty substring `S1` of `S0` and replacing all `"y"`s in the pattern with some non-empty substring `S2` of `S0` yields the same string `S0`.    

If the input string doesn't match the input pattern, the function should return an empty array; otherwise, it should return an array holding the strings `S1` and `S2` that represent `"x"` and `"y"` in the normal string, in that order. If the pattern doesn't contain any `"x"`s or `"y"`s, the respective letter should be represented by an empty string in the final array that you return.    

You can assume that there will never be more than one pair of strings `S1` and `S2` that appropriately represent `"x"` and `"y"` in the normal string.

### 입출력 예

<div class="notice--primary" markdown="1">
🌝 <u>입출력 예 #1</u>     

[입력]   

      pattern = "xxyxxy"       
      string = "gogopowerrangergogopowerranger"       
      
    
[출력]    
    
      ["go", "powerranger"]         

</div> 

### Question Clarifying & Time, Space Complexity 

* Clarify

	```python
	"""
	input :
	input :
	two "non-empty" strings.
	The first one is a patter consisting of only "x"s and/or "y"s.
	The other one is a normal string of alphanumeric characters.
	
	
	output :
	return an array holding the strings that represent "x" and "y" in the normal string
	
	If the input string doesn't match the input pattern,
	the function should return an empty array.
	
	Constraints:
	
	edge case : 
	처음에 y 먼저 들어오면 x와 y를 바꾸어 주는 과정이 따로 필요!
	
	Solution : 
	x 길이와 y 길이를 정해놓고, 이에 따라 주어진 문자열과 같은지 확인, 다르면 이어서 검사, 같다면 바로 리턴!
	x와 y라고 단정짓는 것보다는 처음 들어오는 문자를 기준(처음 들어오는 문자를 x라고 가정만(변수 이름만), 무조건 x라고 단정짓고 짜는 게 아니라!)으로 만든 후, 
	나중에 검사해서 x와 y를 바꾸어 리턴하면 편하지 않을까?
	
	Time Complexity : 
	O(N^2) -> for문 안에 문자열을 새로 만들어서 비교하는 과정이 존재하므로
	
	Space Complexity : 
	O(N^2) -> 최악의 경우 len(string)만큼 새로운 문자열 
	
	"""
	```
	
### Solution(Explanation) & Code

전체 Solution을 한번 정리해보자. 이 **문제의 핵심은 x의 길이를 1부터 찬찬히 늘려가며 y의 길이를 정하는 것**이다! 이 x와 y의 길이를 바탕으로 새로운 문자열을 만든 후, 이를 주어진 문자열과 비교하여 같다면 바로 return, 다르다면 이어서 검사하는 방법으로 풀 수 있다.    

이 때, **x와 y 중 어떤 문자가 먼저 나오는지는 정해지지 않았기에 조심**해야 한다. 이에 대한 대처로 나는 처음 나오는 문자가 x라고 단정짓기보다는 변수의 이름만 countX, lengthX라고 짓고, pattern[0], 즉, pattern에서 처음 나오는 문자의 count, 그리고 length라고 지정해 주었다.    
그리고 마지막에 pattern[0]이 y라면 단순하게 x와 y를 바꾸어서 리턴하면 끝!

* 일단 문자열 `N`, `K` 를 파라미터로 하는 whatIsXY 함수와, 첫 번째 문자의 개수를 가지는 변수 `countX`, 나머지 문자의 개수를 가지는 변수 `countY`, 그리고 실제 비교 문자열에서 나머지 문자가 시작하는 index를 지정해 주기 위해 `pattern`에서의 나머지 문자가 처음 나오는 index를 저장하는 변수 `indexY`를 만들어주고 초기화 해주자.  

	```python
	class Solution:
	    def whatIsXY(self, pattern, string):
	        countX = 0
	        countY = 0
	        indexY = 0  
	```

* 그 후로는, `pattern` 문자열을 돌면서 개수를 세고, 나머지 문자가 처음 나오는 index를 찾으면 모두 저장해주자.

	```python
     # x와 y의 개수를 세서 저장
     for i in range(len(pattern)):
         if pattern[i] == pattern[0]:
             countX += 1
         else:
             if countY == 0:
                 # x와 y 중 나중에 나오는 문자가 처음 시작하는 index
                 indexY = i
             countY += 1
    ```

* 이제는 `string`을 돌면서 처음 나오는 문자와 나머지 문자의 길이를 지정해주고, 이 길이로 비교해줄 문자열을 구성하는 `x`와 `y`를 만들어준다.  자세한 설명은 주석 참고!
 
	```python
	# 처음 문자의 길이와 나머지 문자 길이로 문자열 비교하기 위한 for문
	for i in range(1, len(string)):
	
		# 처음 문자의 길이와 나머지 문자 길이를 결정해준다.
		lengthX = i
		lengthY = (len(string) - i*countX) // countY
            
		# 결정해준 x와 y 길이로 비교해줄 문자열 x와 y를 만들어준다.
		x = string[:i]
		y = string[(indexY*lengthX):indexY*lengthX+lengthY]
	```

* 다음으로는 위에서 만든 x와 y를 pattern을 참고하며 배열하여 비교할 전체 문자열을 만든다.

	```python
   	compareString = ""
   	for a in pattern:
   		if a == pattern[0]:
       	compareString += x
       else:
	       compareString += y
	```

* 만약 `compareString`과 `string`이 같다면, 첫 문자가 `x`인지 `y`인지 확인 후, `y`라면 바꾸어서 `list`에 담아 리턴해주면 끝!

	```python
   	if compareString == string:
   		if pattern[0] == "x":
       	   return [x, y]
        else:
           return [y, x]
	```

* 마지막으로 for문을 모두 돌았는데도 존재하지 않는다면 빈 배열 리턴해주는 것도 잊지 말자.   

	```python
	return []
	```

### Final Code

* CODE
	
	```python
	class Solution:
	    def whatIsXY(self, pattern, string):
	        countX = 0
	        countY = 0
	        indexY = 0
	
	        # x와 y의 개수를 세서 저장
	        for i in range(len(pattern)):
	            if pattern[i] == pattern[0]:
	                countX += 1
	            else:
	                if countY == 0:
	                    # x와 y 중 더 후에 나오는 문자가 처음 시작하는 index
	                    indexY = i
	                countY += 1
	        
	
	        # 처음 문자의 길이와 나머지 문자 길이로 문자열 비교하기 위한 for문
	        for i in range(1, len(string)):
	            # 처음 문자의 길이와 나머지 문자 길이를 결정해준다.
	            lengthX = i
	            lengthY = (len(string) - i*countX) // countY
	            
	            # 결정해준 x와 y 길이로 비교해줄 문자열 x와 y를 만들어준다.
	            x = string[:i]
	            y = string[(indexY*lengthX):indexY*lengthX+lengthY]
	            
	            # 비교할 전체 문자열 만들기!
	            compareString = ""
	            for a in pattern:
	                if a == pattern[0]:
	                    compareString += x
	                else:
	                    compareString += y
	            
	            # 같다면 첫 문자가 x가 y냐 구분해준 후, y라면 서로 바꾸어 리턴해준다.
	            if compareString == string:
	                if pattern[0] == "x":
	                    return [x, y]
	                else:
	                    return [y, x]
	        
	        return []
	```
	    
<div class="notice--primary" markdown="1">
🌟 <u>이번 Session 의 포인트</u>    

- <u>반으로 잘라서</u> 조금 더 효율적으로 푸는 방법!      
- <u>x와 y의 길이</u>로 푸는 방법! (뭔가 참신했음...🤭)      
</div>
