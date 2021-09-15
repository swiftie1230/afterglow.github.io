---
title: "[21.09.15] TIL"
date: 2021-09-15 23:50:28 -0400
toc: true
toc_sticky: true
categories: TIL
---


📝 [21.09.15]

# 오늘의 나 💭

## 👩🏻‍💻 ℙ𝕣𝕠𝕘𝕣𝕒𝕞𝕞𝕚𝕟𝕘 𝕊𝕥𝕦𝕕𝕪

### ☝🏻 <u>객체지향프로그래밍</u>

#### ✔️ **lec 03**

##### 📑 **<u>OOP Concepts</u>**   

📌 <u>Information Hiding/Encapsulation</u>    

📌 <u>Class vs Object</u>    

- `int x;`    
<u><strong>[type]</strong></u> :  similar to class not in the memory, it’s just a type, 
<u><strong>[variable]</strong></u> : similar to object exist in a memory, so you can actually see an existance in a memory.   

📌 <u>Inheritance</u>     

📌 <u>Polymorphism</u>


##### 📑 **<u>C++ Instruction & structure</u>** 

📌 <u>C++ compilation</u>    

📌 <u>Standard Input/Output: cin(keyboard), cout(screen)</u>   

📌 <u>Functions</u>   

📌 <u>Array, Pointer, dynamic allocation</u>    

- **Array/Pointer** : almost same as C

- **Dynamic allocation** : memory allocation is done (at[during] run-time [execution-time]) <-> compile time (something is determined)

📌 <u>class</u>   

- data structure type that can contain member data and member functions   

- **class constructor/destructor** :   
 member function that is automatically called when the object is created/deleted.        


### ☝🏻 <u>오토마타와 형식언어</u>

#### ✔️ **lec 03** 

##### 📑 **<u>NFA (Nondeterministic Finite Automata)</u>**   

📌 <u>DFA와의 차이</u>    

- Two choices

- No transition : the automaton hangs 

📌 <u>Accept and Reject</u>    

<div class="notice--primary" markdown="1">
<u><strong>An NFA accepts a string</strong></u>:   
when <u><strong>there is a computation of the NFA that accepts the string</strong></u>
i.e.    
When there exists a case such that
<u><strong>all the input (string) is consumed</u> AND the automaton is in a <u>final state</u></strong>.   
</div>    

<div class="notice--primary" markdown="1">
<u><strong>An NFA rejects a string</strong></u>:    
when <strong>there is <u>no computation of the NFA that accepts the string</u></strong>.
</div>   

📌 <u>Language accepted</u>     

- Same as DFA ( 하나라도 존재하면 ) and FInal State!

📌 <u>lambda-transitions (lambda-transitions)</u>    

- DFA에는 없음

- head does not move (symbol을 안 움직이고 더 안 읽는다는 소리)

- state만 바꿈

📌 <u>Powerset</u>    

- powerset of Q = Q의 모든 부분집합들의 집합 : 2<sup>Q</sup>

📌 <u>Transition Function</u>   

- 결과가 집합

📌 <u>Why Nondeterminism ?</u>   

- Best case in multiple choices

	- Automatic backtracking
	- Hide unnecessary details

- Good fit to (transform) other notations

- Easy to design

##### 📑 **<u>Equivalence of Machines</u>**   

📌 <u>Every DFA is trivially an NFA</u>    

📌 <u>NFAs and DFAs have the
same computation power or
are equally powerful</u>    


### ☝🏻 <u>iOS_스터디</u>

#### ✔️ **<u>iOS 두잇 책 2회독 : 챕터 4 "피커 뷰" 부분 다시보며 공부</u>**     

📌 **<u>피커 뷰의 `Style`과 `Mode` 변경 가능</u>**      

📌 **<u>changeDatePicker</u> : <u>데이트 피커를 선택할 때 발생하는 액션 함수</u>**     

- 🔮 **<u>datePickerView</u>** : sender `UIDatePicker` 자료형의 인수를 따로 저장해준다.         

- 날짜를 출력하기 위하여 `DateFormatter`라는 클래스 상수 `formatter`를 선언 

- `formatter`의 `dataFormat` 속성을 설정하자.   

- 선택한 날짜를 포맷대로, 문자열 변환 후 label에 표시      

📌 **<u>Timer 기능 추가</u>**     

- 변수 및 상수 추가 
	- 타이머가 구동되면 실행할 함수 지정 (`timeSelector`)   

	- `interval`

- 타이머를 설정하기 위해 `scheduledTimer` 함수 사용

- 타이머가 동작할 때 실행할 함수 작성 : `NSDate()`로 현재 시간 가져오기


#### ✔️ **<u>iOS 꼼꼼한 재은씨 Ch 2.1 부분 공부 + 과제 수행!</u>**     

📌 **엔트리 포인트와 앱의 초기화 과정**   

- `Objective - C`의 경우 
	
	- `main()` 함수 실행  →`UIApplicationMain()` 함수 호출  → `UIApplication` 객체 생성  → `Info.plist` 파일을 바탕으로 앱에 필요한 데이터와 객체를 로드  → `AppDelegate` 객체를 생성하고 `UIApplication` 객체와 연결  → 실행 준비  → 실행 완료 직전 필요한 매소드를 호출  

- `Swift`의 경우

	- `UIApplicationMain()` 함수를 직접 호출할 수 없으므로, 앱 델리게이트 역할을 할 클래스에 @UIApplicationMain 어노테이션을 걸어 표시

📌 **MVC 패턴**    

<div class="notice--primary" markdown="1">
소스 코드 설계 기법으로써, <strong><u>모델(Model) - 뷰(View) - 컨트롤러(Controller)</u></strong>로 이어지는 세 개의 핵심 구조를 이용하여 애플리케이션을 설계하는 것을 말한다.     

<strong>모델</strong>은 <strong>데이터</strong>를, <strong>뷰</strong>는 데이터에 대한 <strong>화면 표현</strong>을 담당하며, <strong>컨트롤러</strong>는 <strong>모델과 뷰 사이에 위치</strong>하여 데이터를 가공하여 뷰로 전달하고, 뷰에서 발생하는 이벤트를 입력받아 처리하는 역할을 담당한다.    

프로그램을 특성에 따라 서로 영향을 미치지 않을 수 있는 범위로 분리해 놓아 수정하더라도 서로에게 영향을 미치지 않게 된다.     
즉, 프로그램이 훨씬 더 유연해지는 결과를 얻을 수 있다.     
</div>

📌 **앱의 상태 변화**     

- 상태 : 화면에 나타났거나, 화면으로부터 숨겨졌거나 등을 의미  

-  운영체제가 처리하는 영역   

- 상태 변화 종류 ( 앱의 라이프 사이클을 구성 )  

	- Not Running
	
	- Inactive
	
	- Active
	
	- Background
	
	- Suspend
- 앱의 실행 상태가 변화할 때마다 앱 객체는 앱 델리게이트에 정의된 특정 메소드를 호출

	- 메소드 내부에 적절한 커스텀 코드를 작성함으로써 우리가 원하는 작업이 실행되도록 할 수 있다!   
   

## 🌝 𝕄𝕪 𝕆𝕨𝕟    

✔️ **콘팀 일정 정리**          

✔️ **[21:00] 콘팀 회의**     

✔️ **백신 1차 접종 😶‍🌫️**      

_
  
# 그냥...끄적임 ✍🏻

오... 백신 접종받은 후에 팔이 아프다는 게 이런 느낌인지 전혀 예상 못함 💭     
뭔가 심하게 멍든 느낌이랄까.       
그래도 평소에 허약 중에 허약 체질이라 내심 걱정했는데 정말 다행이다..! (._.)     

이제 슬슬 과제들이 나올 기미가 보인다.     
고대로 다시 들어가주면 안될까....T^T     


_

# 오늘의_글귀 📄

	네가 걷는 모든 길의 이름은 성장이다.  


<div class="notice--primary" markdown="1">
오늘의 <strong>TIL</strong>은 여기까지!     
      
<strong><u>앞으로의 나에게도 화이팅</u></strong>! 🌸 
</div>
