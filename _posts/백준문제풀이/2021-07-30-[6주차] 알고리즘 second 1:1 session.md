---
title: "[21.07.30] 알고리즘 6주차 - second 1:1 session"
date: 2021-07-30 23:00:28 -0400
toc: true
toc_sticky: true
categories: Algorithm_Problems
---

# [6주차] 알고리즘 second 1:1 session 

<div class="notice--primary" markdown="1">
📜 [<u>2021.7.29</u> 23:00 진행] 
</div>  

## [LeetCode - Find And Replace in String](https://leetcode.com/problems/find-and-replace-in-string/) 

### 문제 설명

You are given a 0-indexed string s that you must perform k replacement operations on. The replacement operations are given as three 0-indexed parallel arrays, indices, sources, and targets, all of length k.

To complete the ith replacement operation:

Check if the substring sources[i] occurs at index indices[i] in the original string s.
If it does not occur, do nothing.
Otherwise if it does occur, replace that substring with targets[i].
For example, if s = "abcd", indices[i] = 0, sources[i] = "ab", and targets[i] = "eee", then the result of this replacement will be "eeecd".

All replacement operations must occur simultaneously, meaning the replacement operations should not affect the indexing of each other. The testcases will be generated such that the replacements will not overlap.

For example, a testcase with s = "abc", indices = [0, 1], and sources = ["ab","bc"] will not be generated because the "ab" and "bc" replacements overlap.
Return the resulting string after performing all replacement operations on s.

A substring is a contiguous sequence of characters in a string. 

### 입출력 예

<div class="notice--primary" markdown="1">
🌝 <u>입출력 예 #1</u>     

<img width="507" alt="스크린샷 2021-07-30 오후 2 11 29" src="https://user-images.githubusercontent.com/63195670/127603672-2488d051-e295-425d-9e19-f6cd84fe538b.png">
	
</div>  

<div class="notice--primary" markdown="1">
🌝 <u>입출력 예 #2</u>     

<img width="507" alt="스크린샷 2021-07-30 오후 2 11 45" src="https://user-images.githubusercontent.com/63195670/127603691-32ebe0ea-4367-4ef2-862c-08e204c4b8e6.png">
</div> 

### Question Clarifying & Time, Space Complexity 


   ```python
"""
input :
0-indexed string
array indices, sources, targets.


output :
return the resulting string after performing all replacement operations on s.

[result operation]
1. Check if the substring sources[i] occurs at index indices[i] in the original strings.
2. If it does not occur, do nothing.
3. Otherwise if it does occur, replace that substring with targets[i].

Constraints:
1 <= s.length <= 1000
k == indices.length == sources.length == targets.length
1 <= k <= 100
0 <= indexes[i] < s.length
1 <= sources[i].length, targets[i].length <= 50
s consists of only lowercase English letters.
sources[i] and targets[i] consist of only lowercase English letters.

edge case : 


Solution : 
indices를 기준으로 오름차순 정렬 -> 일단 index까지는 더해준다.(변화가 없는 문자열들) 
-> 만약 동일하다면 target을 append 해주고, 다르다면 그냥 본래 있던 걸 append 해준다.
-> start하는 index를 업데이트 (이때, index는 처음 주어진 문자열을 기준으로 세워져 있으므로 뒤에 len(source)를 더해주어야 함.)
-> 마지막으로 끝까지 더해주고 이를 문자열로 바꾼다.

Time Complexity : O(nlogn + n^2) -> O(n^2)


Space Complexity : O(n)


"""
   ```

### My Solution(Explanation) & Code

이 문제의 핵심은 `indices`를 기준으로 오름차순 정렬한 후, 생각하는 거였음!      
문제의 조건을 잘 생각해보면, 바꾸기 위해 주어지는 `source` 배열 내부의 문자열들이 서로 겹치는 부분이 없고, `indices`는 주어지는 본래 문자열 `s`의 `index`를 기준으로 한다. 즉, **정렬을 먼저 하고 문제를 생각해도 괜찮다**는 뜻!      

   
그럼 일단 `s`, `indices`, `sources`, `targets` 를 파라미터로 하는 함수 `findReplaceString`을 클래스 `Solution`안에 만들어주자.  
 
   ```python
class Solution:
    def findReplaceString(self, s, indices, sources, targets): 
   ```

그 후, `indices`를 기준으로 `sources`, `target`까지 모두를 `zip`으로 묶어 정렬한 후, 이를 `infoOperation`에 저장해주자.

   ```python
# indices를 기준으로 오름차순 정렬
infoOperation = sorted(zip(indices, sources, targets), key=lambda x:x[0])
   ```

이제 `infoOperation`을 돌면서 만약 해당 문자열이 `s`에서 `indices` 배열값 `index`에 존재하면 `target`으로 바꿔주고, 존재하지 않는다면 기존 문자열을 그대로 이어붙이는 과정을 수행하면 됨!   
그런데 이때 리턴할 새로운 문자열을 저장하는 변수와, 그 전 infoOperation 검사가 끝난 위치가 어디인지를 저장하는 변수가 필요하므로, 이 둘을 먼저 선언하고 초기화해주자.         

   ```python
answer = []
start = 0
   ```

그 이후로는 위에서 말한 것처럼 `infoOperation`을 돌면서 만약 해당 문자열이 `s`에서 `indices` 배열값 `index`에 존재하면 `target`으로 바꿔주고, 존재하지 않는다면 기존 문자열을 그대로 이어붙이는 과정을 작성하면 된다.   
자세한 설명은 주석 참고.        

   ```python
for index, source, target in infoOperation:
	# 일단 해당 index까지는 변하지 않으니까 그대로 
	answer.append(s[start:index])
            
	# 만약 0 - len(source) 이 동일하다면 append
	if s[index: index + len(source)] == source:
		answer.append(target)
            
	# 다르다면 본래 있던 거 그냥 넣어준다.
	else:
		answer.append(s[index:index + len(source)])
	
	# 다음 검사는 어디서부터 시작해야하는지를 저장해 놓는다. (업데이트 해 놓는다.)
	start = index + len(source)
   ```
  

마지막으로는 `answer`를 문자열로 변환한 값에 마지막 `infoOperation` 검사가 끝난 `index`인 `start`부터 `s` 문자열 끝까지 더해준 후, 이를 `return`하면 끝!

   ```python
return "".join(answer) + s[start:]
   ```   	      
   
### Final Code


   ```python
class Solution:
    def findReplaceString(self, s, indices, sources, targets):
        # indices를 기준으로 오름차순 정렬한다.
        infoOperation = sorted(zip(indices, sources, targets), key=lambda x:x[0])

        start = 0
        res = []

        for index, source, target in infoOperation:
            # 일단 index까지는 더해준다.(변화가 없는 문자열들)
            res.append(s[start:index])

            # 만약 동일하다면 target을 append 해주고,
            if s[index:index+len(source)] == source:
                res.append(target)

            # 다르다면 그냥 본래 있던 걸 append 해준다.
            else:
                res.append(s[index:index+len(s)])
            
            # start하는 index를 업데이트 (이때, index는 처음 주어진 문자열을 기준으로 세워져 있으므로 뒤에 len(source)를 더해주어야 함.)
            start = index+len(source)
        
        # 마지막으로 끝까지 더해주고 이를 문자열로 바꾼다.
        return "".join(res) + s[start:]
   ```
     

## 4번

### 문제 설명

You're given an integer `start` and a list `edges` of pairs of integers.    
The list is what's called an adjacency list, and it represents a graph. The number of vertices in the graph is equal to the length of `edges`, where each index `i` in `edges` contains vertex `i`'s outbound edges, in no particular order. Each individual edge is represented by an pair of two numbers, `[destination, distance]`, where the destination is a positive integer denoting the destination vertex and the distance is a positive integer representing the length of the edge(the distance from vertex `i` to vertex destination). Note that these edges are directed, meaning that yiu can only travel from a particular vertex to its destination - not the other way around(unless the destination vertex itself has an outbound edge to the original vertex).    

Write a function that computes the lengths of the shortest path between `start` and all of the other vertices in the graph using Dijkstra's algorithm and returns them in an array. Each index `i` in the output array should represent the length of the shortest path between start and vertex i. If no path is found from `start` to vertex `i`, then `output[i]` should be `-1`.    

Note that the graph represented by `edges` won't contain any self-loops (vertices that have an outbound edge to themselves) and will only have positively weighted edges(i.e., no negative distances).     

If you're unfamiliar with Dijkstra's algorithm, we recommend watching the Conceptual Overview section of this question's video explanation before starting to code.

### 입출력 예

<div class="notice--primary" markdown="1">
🌝 <u>입출력 예 #1</u>     

[입력]   

   ```python
start = 0
edges = [[[1, 7]], [[2, 6], [3, 20], [4, 3]], [[3, 14]], [[4,2]],[], []] 
   ```             
      
    
[출력]    

   ```python    
[0, 7, 13, 27, 10, -1]         
   ```
   
</div> 


### Question Clarifying & Time, Space Complexity 

   ```python
"""
input :
start (시작하는 edge)
edges (graph의 edges와 거리 관계를 나타낸 array)

output :
start에서 각각의 edges의 최단 경로 길이를 array에 담아서 리턴
path가 존재하지 않는다면 -1이 표시된다.

Constraints:
no negative distance, no self-loops

edge case : 

Solution : 
Dijkstra's algorithm(다익스트라 알고리즘)을 이용한다. 
1. 출발 노드와, 도착 노드를 설정
2. 알고 있는 모든 거리 값을 부여
3. 출발 노드부터 시작하여, 방문하지 않은 인저 노드를 방문, 거리를 계산한 다음, 현재 알고 있는 거리보다 짧으면 해당 값으로 갱신한다.
4. 현재 노드에 인접한 미방문 노드까지의 거리를 계산했다면, 현재 노드는 방문한 것이므로, 미방문 집합에서 제거한다.
5. 도착 노드가 미방문 노드 집합에서 벗어나면, 알고리즘을 종료한다.

다익스트라 알고리즘을 실행하는 중에는 방문하지 않은 인접 노드를 방문하는 부분이 있다. 
이 부분에서 우선순위 큐를 사용하면, 지금까지 발견된 가장 짧은 거리의 노드에 대해서 먼저 계산할 수 있으며, 더 긴 거리로 계산 되었을 시 스킵 또한 가능하다.

Time Complexity : O(n^2) -> 각 노드에 대해 모든 노드를 검사하는 경우가 최악이므로


Space Complexity : O(n) -> 모든 노드


"""
   ```
	
### My Solution(Explanation) & Code

우선 우선순위 큐를 구현을 위해 heapq를 import하고, 최소값을 업데이트 해주어야 하므로 이때 필요한 int형 최대값으로 초기화해주기 위해 sys를 Import해주자.  

<div class="notice--primary" markdown="1">
🌝 <u>여기서 잠깐!</u> heapq와 우선순위 큐는 뭘까?       

이 모듈은 우선순위 큐 알고리즘이라고도 하는 힙(heap) 큐 알고리즘의 구현을 제공한다.       
즉, heapq 모듈은 일반 list를 heap처럼 사용할 수 있도록 도와주는 모듈로서, <u>기본적으로 Python에 내장되어 있는 heapq 모듈은 최소 힙</u>이다.  그렇기에 최대 힙을 만들기 위해서는 데이터의 처리가 필요하다. (숫자라면 -를 붙이는 방법이 대표적이다!)    
<u>우선순위 큐를 만드는 데에 주로 사용</u>하고, 삽입, 제거의 시간복잡도는 O(logn)이다.    

📌 <u>힙의 정의</u>   

힙은 모든 부모 노드가 자식보다 작거나 같은 값을 갖는 이진 트리이다. 이 구현에서는 모든 k에 대해서 `heap[k] <= heap[2*k+1]`과 `heap[k] <= heap[2*k+2]`인 배열을 사용하고, 요소는 0부터 세는데, 비교를 위해 존재하지 않는 요소는 무한으로 간주한다. 힙의 흥미로운 특성은 가장 작은 요소가 항상 루트인 heap[0]이라는 점!     

📌 <u>How to make heap ?</u>     

힙을 만들려면, []로 초기화된 리스트를 사용하거나, 함수 heapify()를 통해 값이 들어 있는 리스트를 힙으로 변환 할 수 있다.

📌 <u>제공되는 함수</u>          

1. <u>heapq.heappush(heap, item)</u>      
	
	힙 불변성을 유지하면서, item 값을 heap으로 푸시한다.
	    
2.  <u>heapq.heappop(heap)</u>     

	힙 불변성을 유지하면서, heap에서 가장 작은 항목을 팝하고 반환한다. 힙이 비어 있으면, IndexError가 발생. 팝 하지 않고 가장 작은 항목에 액세스하려면, heap[0]을 사용하면 된다.     

3. <u>heapq.heapify(x)</u>    

	리스트 x를 선형 시간으로 제자리에서 힙으로 변환한다.     
	
4. <u>heapq.heapreplace(heap, item)</u>    

	heap에서 가장 작은 항목을 팝하고 반환하며, 새로운 item도 푸시한다. 힙 크기는 변경되지 않으며, 힙이 비어 있으면, IndexError가 발생한다.      

	이 한 단계 연산은 heappop()한 다음 heappush()하는 것보다 더 효율적이며 고정 크기 힙을 사용할 때 더 적합할 수 있다. 팝/푸시 조합은 항상 힙에서 요소를 반환하고 그것을 item으로 대체한다.     

	반환된 값은 추가된 item보다 클 수 있다. 이를 원하지 않을 경우 (허용하지 않을 경우), 대신 두 값 중 작은 값을 반환하여, 힙에 큰 값을 남겨 두는 heappushpop()을 사용하는 것이 좋음!     
	
5. <u>heapq.merge(*iterables, key=None, reverse=False)</u>        

	여러 정렬된 입력을 단일 정렬된 출력으로 병합하는 함수로, (예를 들어, 여러 로그 파일에서 타임 스탬프 된 항목을 병합!) 정렬된 값에 대한 이터레이터를 반환한다.      

sorted(itertools.chain(*iterables))와 비슷하지만 이터러블을 반환하고, 데이터를 한 번에 메모리로 가져오지 않으며, 각 입력 스트림이 이미 (최소에서 최대로) 정렬된 것으로 가정한다.      

키워드 인자로 지정해야 하는 두 개의 선택적 인자가 있다.      

key는 각 입력 요소에서 비교 키를 추출하는 데 사용되는 단일 인자의 키 함수를 지정하고, 기본값은 None이다. (요소를 직접 비교합니다).      

reverse는 불리언 값으로, True로 설정하면 각 비교가 반대로 된 것처럼 입력 요소가 병합된다.       sorted(itertools.chain(*iterables), reverse=True)와 유사한 동작을 달성하려면 모든 이터러블이 최대에서 최소로 정렬되어 있어야 합니다.       

버전 3.5에서 변경: 선택적 key와 reverse 매개 변수가 추가됨 ?      

6. <u>heapq.nlargest(n, iterable, key = None)</u>     

	iterable에 의해 정의된 데이터 집합에서 n 개의 가장 큰 요소로 구성된 리스트를 반환한다. key가 제공되면 iterable의 각 요소에서 비교 키를 추출하는 데 사용되는 단일 인자 함수를 지정한다. (예를 들어, key=str.lower). sorted(iterable, key=key, reverse=True)[:n] 와 동일한 연산을 하는 것!       
	
7. <u>heapq.nsmallest(n, iterable, key = None)</u>     

	iterable에 의해 정의된 데이터 집합에서 n 개의 가장 작은 요소로 구성된 리스트를 반환한다. 동일하게 key가 제공되면 iterable의 각 요소에서 비교 키를 추출하는 데 사용되는 단일 인자 함수를 지정! (예를 들어, key=str.lower). sorted(iterable, key=key)[:n]와 동일한 연산을 수행한다.          


<u>마지막 두 함수 (nlargest, nsmallest) 는 작은 n 값에서 가장 잘 동작</u>한다. 값이 크면, sorted() 기능을 사용하는 것이 더 효율적! 또한, n==1일 때는, 내장 min()과 max() 함수를 사용하는 것이 더 효율적이며, 이 함수를 반복해서 사용해야 할 경우에는 iterable을 실제 힙으로 바꾸는 것이 좋다.         
      
</div>
 

일단 클래스 `Solution`에 `start`와 `edges`를 파라미터로 하는 함수 `findShortestPath`를 만들어주자.  

   ```python
class Solution:
    def findShortestPath(self, start, edges):
   ```

그 후로는, min값을 비교해서 업데이트 해야 하므로 `distances` 안의 모든 distance들을 **python에서 지원하는 int형 최댓값**으로 초기화 해주고, 업데이트가 한 번도 되지 않은 값, 즉, path가 없는 `edge`의 값은 `-1`로 바꾸기 위해 `flag`라는 배열을 만든 후, `False`로 모두 초기화 해주자.

   ```python
# 일단 python에서 지원하는 int형 최대값을 저장해 놓는다.
distances = [sys.maxsize for x in range(len(edges))]

# 업데이트가 한 번도 되지 않은 값, 즉, path가 없는 edge의 값은 -1로 바꾸기 위해 flag라는 배열 선언 및 초기화
flags = [False for x in range(len(edges))]
   ```

이제 **처음 시작하는 edge**인 `start`에 대해서 `distances[start]`의 값을 `0`으로, `flags[start]` 값은 `True`로 바꿔주자.   
 
   ```python
# 처음 값 
distances[start] = 0
flags[start] = True
   ```
   
다음으로는 큐를 선언하고 초기화 해 준 후, 시작 노드부터 탐색하기 위해 push 해준다.    

   ```python
# 큐 선언 및 초기화 해준다.
queue = []

# 시작 노드부터 탐색하기 위함.
heapq.heappush(queue, [distances[start], start])
   ```

이제 거의 다 왔다. queue가 비어있을 때까지 queue를 돌면서, 출발 노드부터 시작하여, 방문하지 않은 인접 노드를 방문, 거리를 계산한 다음, 현재 알고있는 거리보다 짧으면 해당 값으로 갱신한다.
현재 노드에 인접한 모든 미방문 노드까지의 거리를 계산했다면, 현재 노드는 방문한 것이므로, 미방문 집합에서 제거하면 됨. 자세한 설명은 주석 참고!   

   ```python
while queue:
	current_distance, current_destination = heapq.heappop(queue)

	# 더 크면 볼 필요 없다.
	if distances[current_destination] < current_distance:
		continue

	for new_destination, new_distance in edges[current_destination]:
		distance = current_distance + new_distance
		if distance < distances[new_destination]:
			# 만약 저장된 값보다 더 작으면 최솟값 업데이트
			distances[new_destination] = distance
			# 업데이트 한 번 되었으므로 -1이 될 수 없다. 따라서 True로 변경.
			flags[new_destination] = True
			# 다음 인접 거리를 계산하기 위해 큐에 삽입
			heapq.heappush(queue, [distance, new_destination])
   ```

마지막으로 flag를 검토하여 업데이트 되지 않은 값이 있다면, 이 값은 path가 존재하지 않는다는 뜻이므로 -1로 바꿔준 후, distances 리턴 해주면 끝!   

   ```python
for i in range(len(flags)):
	if flags[i] == False:
		distances[i] = -1
		
return distances
   ```

### My Final Code
	
   ```python
import heapq  # 우선순위 큐 구현을 위함
import sys

class Solution:
    def findShortestPath(self, start, edges):
        # 일단 python에서 지원하는 int형 최대값을 저장해 놓는다.
        distances = [sys.maxsize for x in range(len(edges))]

        # 업데이트가 한 번도 되지 않은 값, 즉, path가 없는 edge의 값은 -1로 바꾸기 위해 flag라는 배열 선언 및 초기화
        flags = [False for x in range(len(edges))]

        # 처음 값 
        distances[start] = 0
        flags[start] = True

        # 큐 선언 및 초기화 해준다.
        queue = []

        # 시작 노드부터 탐색하기 위함.
        heapq.heappush(queue, [distances[start], start])

        while queue:
            current_distance, current_destination = heapq.heappop(queue)

            # 더 크면 볼 필요 없다.
            if distances[current_destination] < current_distance:
                continue

            for new_destination, new_distance in edges[current_destination]:
                distance = current_distance + new_distance
                if distance < distances[new_destination]:
                    # 만약 저장된 값보다 더 작으면 최솟값 업데이트
                    distances[new_destination] = distance
                    # 업데이트 한 번 되었으므로 -1이 될 수 없다. 따라서 True로 변경.
                    flags[new_destination] = True
                    # 다음 인접 거리를 계산하기 위해 큐에 삽입
                    heapq.heappush(queue, [distance, new_destination])
        
        for i in range(len(flags)):
            if flags[i] == False:
                distances[i] = -1

        
        return distances
   ```

	    
<div class="notice--primary" markdown="1">
🌟 1 Session 의 <u>포인트</u>    
 - heapq      
 - 우선순위 큐     
</div>

## 참고 사이트  

- [heapq 관련 참고 사이트 1](https://justkode.kr/python/pygorithm-2)     
- [heapq 관련 참고 사이트 2](https://docs.python.org/ko/3/library/heapq.html)
