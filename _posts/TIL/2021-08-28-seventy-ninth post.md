---
title: "[21.09.06] TIL"
date: 2021-09-06 23:50:28 -0400
toc: true
toc_sticky: true
categories: TIL
---


📝 [21.09.06]

# 오늘의 나 💭

## 👩🏻‍💻 ℙ𝕣𝕠𝕘𝕣𝕒𝕞𝕞𝕚𝕟𝕘 𝕊𝕥𝕦𝕕𝕪   

### ☝🏻 <u>객체지향프로그래밍</u>

#### ✔️ **[10:00] ZOOM 강의 참여**

##### 📑 **<u>Software Crisis</u>**   

<div class="notice--primary" markdown="1">
rapid increases in computer power and the complexity of the problems (SW).    
<strong>Software technology can not follow the complexity.</strong>        
<strong><u>the difficulty of writing correct, understandable, and verifiable
computer programs</u></strong>    
</div>

##### 📑 **<u>SoftWare Life Cycle ( Software development process )</u>** 

`Requirement Analysis` → `Design` → `Implementation` → `Test` → `Maintainance`  

##### 📑 **<u>Software Engineering</u>** 

<div class="notice--primary" markdown="1">
The establishment and use of sound engineering principles in order to <strong><u>economically obtain software</u> that is <u>reliable</u> and works <u>efficiently</u></strong>    
</div>

##### 📑 **<u>Goals of SE</u>** 

📌 Maintainability     

📌 Dependability    

📌 Efficiency   

📌 Usability     

##### 📑 **<u>Programming Methodology</u>** 

📌 Unstructed Programming 

- ex) assembly..

📌 Procedure Programming 

- ex) C

📌 Modular(Structured) Programming

📌 Object-Oriented Programming	 

- ex) C++, JAVA, python 

### ☝🏻 <u>iOS_스터디</u>

#### ✔️ **iOS 두잇 책 '스와이프 제스처 사용하기' 부분 공부 + 과제 수행!**     

##### 📑 <u>스와이프 제스처 사용하기</u> : <u>UISwipeGestureRecognizer</u>    

📌 <strong><u>스와이프 제스처 인식</u></strong>      

: `UISwipeGestureRecognizer` 클래스 상수의 direction 속성에 원하는 방향을 설정 → 뷰 객체의 `addGestureRecognizer` 메서드를 사용해 원하는 방향의 스와이프 제스처를 등록        

   ```swift
// 위쪽 방향의 스와이프 제스처 인식 부분 구현 
let swipeUp = UISwipeGestureRecognizer(target: self, action: #selector(ViewController.[액션 메서드](_:)))
swipeUp.direction = UISwipeGestureRecognizer.Direction.up
self.view.addGestureRecognizer(swipeUp)
   ```     

📌 <strong><u>액션 메서드 구현하기</u></strong>    

: 스와이프 제스처를 행했을 때 실행하고 싶은 부분을 구현한 메서드를 의미한다. 정말 실행하고 싶은 것들을 구현해 놓으면 됨.              


📌 <strong><u>멀티 터치 스와이프 제스처 인식하기</u> : <u>`.numberOfTouchesRequired`</u></strong>              

   ```swift
let numOfTouches = [원하는 터치의 개수]

swipeUp.numberOfTouchesRequired = numOfTouches
   ```

##### 📑 <u>추가 지식</u>    

📌 **시뮬레이터에서 두 손가락을 사용하려면? : `option` 키**   

- **같은 방향으로 스와이프하고 싶다면? : `option` 키 + `shift` 키**


#### ✔️ **iOS 두잇 책 '핀치 제스처 사용해 사진 확대 / 축소하기' 부분 공부 + 과제 수행!**     

##### 📑 <u>핀치 제스처 사용하기</u> : <u>UIPinchGestureRecognizer</u>    

📌 <strong><u>핀치 제스처 등록하기</u></strong>      

: `UIPinchGestureRecognizer` 클래스 상수의 pinch를 선언 → 뷰 객체의 `addGestureRecognizer` 메서드를 사용해 핀치 제스처를 등록        

   ```swift
// 위쪽 방향의 스와이프 제스처 인식 부분 구현 
let pinch = UIPinchGestureRecognizer(target: self, action: #selector(ViewController.doPinch(_:)))
self.view.addGesture(pinch)
   ```     

📌 <strong><u>액션 메서드 구현하기</u></strong>    

: 핀치 제스처를 행했을 때 실행하고 싶은 부분인 확대/축소를 구현한 메서드를 의미한다.   

   ```swift
imgPinch.transform = imgPinch.transform.scaledBy(x: pinch.scale, y: pinch.scale)
pinch.scale = 1
   ```              

## 🛠️ 𝔾𝕚𝕥𝕙𝕦𝕓  	

### ☝🏻 <u>iOS_스터디</u>

✔️ **iOS 두잇 책 '스와이프 제스처 사용하기' 부분 과제 수행한 것 레퍼지토리에 업로드**  

- 📁 SwipeGesture
   
- 📁   GalleryAppSwipeGesture (SwipeGesture_mission)

✔️ **iOS 두잇 책 '핀치 제스처 사용해 사진 확대 / 축소하기' 부분 과제 수행한 것 레퍼지토리에 업로드**  

- 📁 PinchGesture
   
- 📁   PinchGalleryApp (PinchGesture_mission)


## 🌝 𝕄𝕪 𝕆𝕨𝕟    

✔️ **콘팀 일정 정리 👩🏻‍💻**  

✔️ **알고리즘 스터디 일정 정하기**  

✔️ **[21:00] 모냉고 회의**               
    

  

_
  
# 그냥...끄적임 ✍🏻

적어도 내가 한다고 선택한 일들은 해내야 하지 않겠어...?         
그리고 가치가 없는 것들은 생각하지도 말기.        
상처받지 않는 건 온전히 나의 몫.             
_

# 오늘의_글귀 📄

	쉽게 이룰 수 있는 것은 없습니다.
	각오를 단단히 다지세요.


<div class="notice--primary" markdown="1">
오늘의 <strong>TIL</strong>은 여기까지!     
      
<strong><u>앞으로의 나에게도 화이팅</u></strong>! 🌸 
</div>
