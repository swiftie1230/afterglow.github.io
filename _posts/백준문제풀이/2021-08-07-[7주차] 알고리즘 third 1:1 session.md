---
title: "[21.08.07] 알고리즘 7주차 - third 1:1 session"
date: 2021-08-07 17:00:28 -0400
toc: true
toc_sticky: true
categories: Algorithm_Problems
---

# [7주차] 알고리즘 third 1:1 session 

<div class="notice--primary" markdown="1">
📜 [<u>2021.8.07</u> 오전 진행] 
</div>  

## 💬 [LeetCode - Bulls and Cows](https://leetcode.com/problems/bulls-and-cows/) 

### 📄 문제 설명

You are playing the Bulls and Cows game with your friend.

You write down a secret number and ask your friend to guess what the number is. When your friend makes a guess, you provide a hint with the following info:

- The number of "bulls", which are digits in the guess that are in the correct position.    

- The number of "cows", which are digits in the guess that are in your secret number but are located in the wrong position. Specifically, the non-bull digits in the guess that could be rearranged such that they become bulls.

Given the secret number secret and your friend's guess guess, return the hint for your friend's guess.

The hint should be formatted as "xAyB", where x is the number of bulls and y is the number of cows. Note that both secret and guess may contain duplicate digits.

### 💭 입출력 예

<div class="notice--primary" markdown="1">
🌝 <u>입출력 예 #1</u>     

[입력]   

   ```python
secret = "1807", guess = "7810"  
   ```  

[출력]    

   ```python
"1A3B"	   
   ```
</div>  

<div class="notice--primary" markdown="1">
🌝 <u>입출력 예 #2</u>     

[입력]   

   ```python
secret = "1123", guess = "0111"  
   ```  

[출력]    

   ```python
"1A1B"	   
   ```
</div> 

<div class="notice--primary" markdown="1">
🌝 <u>입출력 예 #3</u>     

[입력]   

   ```python
secret = "1", guess = "0"  
   ```  

[출력]    

   ```python
"0A0B"	   
   ```
</div>

<div class="notice--primary" markdown="1">
🌝 <u>입출력 예 #4</u>     

[입력]   

   ```python
secret = "1", guess = "1"  
   ```  

[출력]    

   ```python
"1A0B"	   
   ```
</div>

### ✏️ Question Clarifying & Time, Space Complexity 


   ```python
"""
input :
secret : the secret number
guess : friend's guess

output :
the number of "bulls" + "A"
the number of "cows" + "B"

"bulls" = digits in the guess that are in the correct position.
"cows" = digits in the guess that are in your secret number but are located in the wrong position.

Constraints:
1 <= secret.length, guess.length <= 1000
secret.length == guess.length
secret and guess consist of digits only.

edge case:

Solution&Algorithm :
비교해 가면서 완전히 같으면 bulls, 

한 번 더 돌면서 해당 글자가 있다면 counts로 세서 더 작은 값을 더해준다. 
그 후 guess에서는 다 replac, 즉, 없애준다. (다시 비교하면 안 되므로)

마지막에 리턴할 때, bulls에 들어가 있는 글자들은 cows에 들어가면 안되므로 뺴준 걸 cows로!


Time Complexity :
O(N) 

Space Complexity :
O(N) -> 실제 저장되는 메모리 크기는 일정! (remain : 10)
"""
   ```

### ✏️ My Solution(Explanation) & Code

이 문제는 `secret`와 `guess`의 문자를 하나씩 비교해가면서 위치와 숫자 모두 같으면 `bulls`수를 증가시키고, 아니라면 `remain` 딕셔너리에서 해당 글자에 대한 `value` 숫자를 증가시켜 준 후, `cows` 의 수는 `remain`의 `value`에서 더 작은 값을 더하여 구하는 것이 핵심이다.            
   
그럼 일단 `Solution` 클래스에서, secret와 guess를 파라미터로 하는 `getHint`함수를 정의해주자.       
 
   ```python
class Solution:
    def getHint(self, secret, guess): 
   ```

그 후, 한자리 숫자는 0-9까지 총 10개 뿐이므로, 한자리 숫자를 string 형태로 바꾼 값을 key로 하는 remain 딕셔너리를 선언하고 [0, 0]으로 초기화해주자..    

<div class="notice--primary" markdown="1">
🌝 <strong><u>여기서 잠깐!</u> 왜 [0, 0]으로 초기화해주는 걸까?</strong>        

배열의 첫번째 원소는 secret에서 bulls가 아니라서 일단 남겨놓은 해당 문자의 개수를, 두번째 원소는 guess에서의 bulls가 아니라서 일단 남겨놓은 해당 문자의 개수를 나타낸다!    
</div>

   ```python
remain = {str(i):[0, 0] for i in range(10)}
   ```

이제 bulls의 개수를 가리킬 변수 `bullDigits`와 cows의 개수를 가리킬 변수 `cowsDigits`를 선언 후 초기화해주자.             

   ```python
bullDigits = 0
cowsDigits = 0
   ```

그 이후로는 전체 index를 돌면서 해당 문자가 bulls인지를 검토한 후, 맞다면 bullDigit를 1 증가시켜 주고, 아니라면 remain 딕셔너리에서 secret과 guess의 해당 index의 문자를 key로 하는 value를 1씩 증가시켜 주면 된다.     

   ```python
for i in range(len(guess)):
	if guess[i] == secret[i]:
		bullDigits += 1
	else:
		remain[secret[i]][0] += 1
		remain[guess[i]][1] += 1
   ```

다음으로, 각각의 keys()에 대한 value를 돌면서 더 작은 값을 cowsDigits에 더해주자!     

   ```python
for i in remain.keys():
	cowsDigits += min(remain[i])
   ```
   
마지막으로 출력 형식에 맞게 출력하면 끝!    

   ```python
return str(bullDigits) + "A" + str(cowsDigits) + "B"
   ```
     
### ✏️ Final Code

   ```python
class Solution:
    def getHint(self, secret, guess):
        remain = {str(i):[0, 0] for i in range(10)}

        bullDigits = 0
        cowsDigits = 0

        for i in range(len(guess)):
            if guess[i] == secret[i]:
                bullDigits += 1
            else:
                remain[secret[i]][0] += 1
                remain[guess[i]][1] += 1
        
        for i in remain.keys():
            cowsDigits += min(remain[i])
        
        return str(bullDigits) + "A" + str(cowsDigits) + "B"
   ```

## 💬 [LeetCode - Find Duplicate File in System](https://leetcode.com/problems/find-duplicate-file-in-system/)

### 📄 문제 설명

Given a list `paths` of directory info, including the directory path, and all the files with contents in this directory, return *all the duplicate files in the file system in terms of their paths*. You may return the answer in **any order**.

A group of duplicate files consists of at least two files that have the same content.

A single directory info string in the input list has the following format:

- `"root/d1/d2/.../dm f1.txt(f1_content) f2.txt(f2_content) ... fn.txt(fn_content)"`

It means there are `n` files (`f1.txt, f2.txt ... fn.txt`) with content (`f1_content, f2_content ... fn_content`) respectively in the directory `"root/d1/d2/.../dm"`. Note that `n >= 1` and `m >= 0`. If `m = 0`, it means the directory is just the root directory.

The output is a list of groups of duplicate file paths. For each group, it contains all the file paths of the files that have the same content. A file path is a string that has the following format:

`"directory_path/file_name.txt"`     

### 💭 입출력 예

<div class="notice--primary" markdown="1">
🌝 <u>입출력 예 #1</u>     

[입력]   

   ```python
paths = ["root/a 1.txt(abcd) 2.txt(efgh)","root/c 3.txt(abcd)","root/c/d 4.txt(efgh)","root 4.txt(efgh)"]
   ```             
      
    
[출력]    

   ```python    
[["root/a/2.txt","root/c/d/4.txt","root/4.txt"],["root/a/1.txt","root/c/3.txt"]]        
   ```
   
</div> 

<div class="notice--primary" markdown="1">
🌝 <u>입출력 예 #2</u>     

[입력]   

   ```python
paths = ["root/a 1.txt(abcd) 2.txt(efgh)","root/c 3.txt(abcd)","root/c/d 4.txt(efgh)"]
   ```             
      
    
[출력]    

   ```python    
[["root/a/2.txt","root/c/d/4.txt"],["root/a/1.txt","root/c/3.txt"]]        
   ```
   
</div>  
 

### ✏️ Question Clarifying & Time, Space Complexity

   ```python
"""
input :
paths : list of directory info (including the directory path, and all the files with contents in this directory.)

output :
list of groups of duplicate file paths.

Constraints:
1 <= paths.length <= 2 * 104
1 <= paths[i].length <= 3000
1 <= sum(paths[i].length) <= 5 * 105
paths[i] consist of English letters, digits, '/', '.', '(', ')', and ' '.
You may assume no files or directories share the same name in the same directory.
You may assume each given directory info represents a unique directory. 
A single blank space separates the directory path and file info.

edge case:
len()가 1이면 마지막에 answer에 append() 하면 안됨!

Solution&Algorithm :
비교해 가면서 동일한 내용을 담고 있으면 같은 딕셔너리(defaultdict) index에 담는다.

Time Complexity :
O(N) 

Space Complexity :
O(N)
"""
   ```
	
### ✏️ My Solution(Explanation) & Code

이 문제에서의 푸는 데 중요했던 부분은 **문자열의 특정 부분에서 split**해주고, **content를 기준으로 분류**하여 **`defaultdict`**에 담는 것이었음!        

**`defaultdict`**를 사용할 것이기에 일단 `collections`를 import 해주고, `Solution` 클래스에 `paths`를 파라미터로 받는 함수 `findDuplicate`을 만들어주자.         

   ```python
import collections

class Solution:
    def findDuplicate(self, paths):
   ```

다음으로는 **`Content`**를 기준으로 분류한 내용을 담아줄, 기본 값을 `list`로 하는 `defauldict`인 `classificationWithContent`를 선언해주자.            

   ```python
classificationWithContent = collections.defaultdict(list)
   ```

이제 `paths`의 `directortyInfo` 하나하나에 대해 우선 공백을 기준으로 `split` 한 후, 반환된 `list`를 `splitInfo`에 넣는다.      
이 `splitInfo`의 첫 번째 값은 `directoryPath`, 나머지는 여러 `files`에 대한 세부 정보를 의미함!  따라서 첫 번째 값은 `directoryPath`라는 변수에 넣어주고, 나머지는 일단 `files`라는 변수에 넣어주자.           

   ```python
for directoryInfo in paths:
            splitInfo = directoryInfo.split()
            
            directoryPath = splitInfo[0]
            files = splitInfo[1:]
   ```

<div class="notice--primary" markdown="1">
🌝 <strong><u>여기서 잠깐!</u> split()는 뭘까?</strong>        

파이썬에서 <strong>문자열을 나눌 때</strong> 주로 쓰는 str 클래스의 내부 함수로, 문자열 객체에서 바로 사용이 가능하다!     

이 함수는 기준 문자, 즉, <strong>구분자를 기준으로 문자열을 분리 후, 이를 리스트로 반환</strong>한다.    

📌 <strong><u>함수의 형태</u></strong>          

파라미터 형태에 따라 3가지 종류의 함수 형태를 가지고 있으며, 다음과 같이 구분 가능하다!        

<strong>1. 문자열.split('구분자')</strong>   
  함수의 파라미터로 지정된 특정 구분자를 기준으로 문자열을 나눈 후, 이 값들을 <code>list</code>로 반환한다.    
  구분자가 없을 경우, 함수가 자동으로 띄워쓰기, 엔터 등의 공백을 인식해서 문자열을 나눈다.    

<strong>2. 문자열.split('구분자', 분할횟수)</strong>    	    
  두 번째 파라미터인 분할 횟수만큼만 구분자를 기준으로 문자열을 나눈 후, 이 값들을 <code>list</code>로 반환한다.    
  
  반드시 이 함수는 <strong>구분자를 입력</strong>해야 한다! 만약 구분횟수만 입력한 경우 오류 발생함!    
  
<strong>3. 문자열.split(sep='구분자', maxsplit=분할횟수)</strong>    
  파라미터에 변수를 지정한 형태로, 바로 위의 함수와 동일한 기능을 수행한다.     
  
  이 함수 역시 <strong>반드시 구분자를 입력</strong>해야 한다! 만약 구분횟수만 입력한 경우 오류 발생함!    

</div>

   
다음으로는 `files`에서 각각의 `fileNameAndContent` 문자열의` ")"`를 제거해 준 후, 이를 다시 `"("` 기준으로 나눈 `list`를 `splitFile`에 저장해 주자.    

   ```python
for fileNameAndContent in files:
	splitFile.rstrip(")")
	splitFile = fileNameAndContent.split("(")
   ```

<div class="notice--primary" markdown="1">
🌝 <strong><u>여기서 잠깐!</u> strip(), lstrip(), rstrip()는 뭘까?</strong>        

Python에서 <code>strip()</code>을 이용하면 <strong>문자열에서 특정 문자를 제거</strong>할 수 있다. Java 등의 다른 언어들도 strip()을 제공하며, 기능은 모두 비슷함!     

<strong>인자에 아무것도 입력하지 않으면 공백을 제거</strong>하며, <strong>문자 1개를 전달하면 그 문자와 동일한 것을 모두 제거</strong>해 준다.       

또한 <strong>여러 문자를 제거</strong>할 수도 있는데, <strong>인자로 여러 문자를 전달</strong>하면 그 문자들과 동일한 것들을 모두 제거한다!       

📌 <strong><u>strip() 함수</u></strong>          

인자로 전달된 문자를 String의 <strong>왼쪽과 오른쪽 모두</strong>에서 제거하는 함수이다.       

📌 <strong><u>lstrip() 함수</u></strong>          

인자로 전달된 문자를 String의 <strong>왼쪽</strong>에서 제거하는 함수이다.       

📌 <strong><u>rstrip() 함수</u></strong>          

인자로 전달된 문자를 String의 <strong>오른쪽</strong>에서 제거하는 함수이다.       

</div>

이때 `splitFile`의 첫 번째 값은 파일 이름이므로 `fileName`에, 두 번째 값은 `content`이므로 `fileContent`에 저장해 준다.       

   ```python
fileName = splitFile[0]
fileContent = splitFile[1]
   ```

이 후, 실질적으로 마지막에 반환할 `list`에 들어갈 문자열인 `filePath`를 만들어주자!    
이는 `directoryPath + "/" + fileName` 만 해주면 됨.             

   ```python
filePath = directoryPath + "/" + fileName
   ```

다음으로는 `classificationWithContent` 딕셔너리에  해당 `fileContent`를 `key`로 하는 `value` `list`에 `filePath`를 append 해주면 for문 완성!         

   ```python
classificationWithContent[fileContent].append(filePath)
   ```
   
이제 반환할 리스트 `answer`를 선언하고 초기화 해준 후, `classificationWithContent.values()` 각각의 `value`의 길이가 `1`이 아닌 경우에만 `answer`에 append 해주자.       
하나인 경우는 **문제의 조건**에 따르면 반환값에 포함되지 않아야 하기 때문!     

   ```python
answer = []

for value in classificationWithContent.values():
	if len(value) != 1:
		answer.append(value)
   ```
마지막으로 answer 리턴해주면 끝!     

   ```python
return answer
   ```

### ✏️ Final Code
	
   ```python
import collections

class Solution:
    def findDuplicate(self, paths):
        classificationWithContent = collections.defaultdict(list)

        for directoryInfo in paths:
            splitInfo = directoryInfo.split()
            
            directoryPath = splitInfo[0]
            files = splitInfo[1:]

            for fileNameAndContent in files:
                splitFile.rstrip(")")
                splitFile = fileNameAndContent.split("(")
                
                fileName = splitFile[0]
                fileContent = splitFile[1]

                filePath = directoryPath + "/" + fileName

                classificationWithContent[fileContent].append(filePath)
        
        answer = []

        for value in classificationWithContent.values():
            if len(value) != 1:
                answer.append(value)
        
        return answer
   
   ```
   	    
<div class="notice--primary" markdown="1">
🌟 <strong>3 Session 의 <u>포인트</u></strong>    

 - split()   
 - strip(), lstrip(), rstrip()      
 - defaultdict()
     
</div>

## 🔗 참고 사이트  

- [**split()** 관련 참고 사이트](https://notstop.co.kr/1139/)     

- [**strip(), lstrip(), rstrip()** 관련 참고 사이트](https://codechacha.com/ko/python-string-strip/)
