---
title: "[21.08.26] TIL"
date: 2021-08-26 23:50:28 -0400
toc: true
toc_sticky: true
categories: TIL
---


📝 [21.08.26]

# 오늘의 나 💭

## 👩🏻‍💻 ℙ𝕣𝕠𝕘𝕣𝕒𝕞𝕞𝕚𝕟𝕘 𝕊𝕥𝕦𝕕𝕪    
### ☝🏻 <u>프로그래밍 언어론</u>

#### ✔️ **INTRO 강의 수강하면서 필기**

##### 📑 **<u>Language Paradigms</u>**   
    
* Imperative (including Object-Oriented)

* Functional

* Logic

##### 📑 **<u>Quicksort를 통한 예시</u>** 

* Scheme

* APL

* Python

##### 📑 **<u>짧은 강의 소개 (OT)</u>** 	    


### ☝🏻 <u>iOS_스터디</u>

#### ✔️ **iOS 두잇 책 코어 그래픽스로 화면에 그림 그리기' 부분 공부 + 과제 수행!**     

##### 📑 **<u>화면에 그림 그리기</u> : <u>Core Graphics</u>**    

우선 그림을 그리기 위해 도화지 역할인 **콘텍스트<sup>context</sup> 를 생성**한다.      

그 후로 그리고 싶은 도형이나 그림을 **그리는 기능을 구현**하면 된다.     

**콘텍스트를 이미지 뷰의 크기와 같게 생성** 후,    

   ```swift
UIGraphicsBeginImageContext(imgView.frame.size)
   ```

생성한 **콘텍스트의 정보**를 가져온다.     

   ```swift
let context = UIGraphicsGetCurrentContext()!
   ```

그 후, 선의 굵기나 선 색상 등 **콘텍스트에 대한 여러 가지 설정**을 한다.        

   ```swift
context.setLineWidth(2.0)
context.setStrokeColor(UIColor.red.cgColor)
   ```

이후로는 화면에 그리고 싶은 그림에 따라 코드를 작성해 주면 된다.     

- **Draw Line** → 응용해서 **Draw Triangle** 가능

	* **시작 위치 (`context.move(to: CGPoint)`)**, **끝점 위치 (`context.addLine(to: CGPoint)`)**로 **<u>선</u>** 그릴 수 있다.

- **Draw Rectangle**

	* **왼쪽 위를 나타내는 점**, 그리고 **폭**과 **높이**로 **<u>사각형</u>**을 그릴 수 있다.    
	**(`context.addRect(CGRect)`)**

- **Draw Ellipse** → 응용해서 **Draw Circle** 가능

	* **위와 동일한 관련된 정보**로 그리는 사각형에 내접하는 **<u>타원</u>**이나 **<u>원</u>**을 그릴 수 있다.    
	**(`context.addEllipse(in: CGRect)`) : 원을 그리고 싶다면 width와 height를 동일하게 적어주면 된다.** 

- **Draw Arc**

	* **현재 위치 (`context.move(to: CGPoint)`)**, **두개의 접점**, 그리고 **반지름**을 통해 내접한 **<u>호</u>**를 그릴 수 있다.     
	**(`context.addArc(tangent1End: 접점1위치, tangent2End: 접점2 위치, radius: 반지름)`)**     
	**(`context.addLine(to: 접점 1)`)**


그린 도형에 색을 채울 수도 있다.

- 그린 **도형 채우기** (Fill)   
 
	   ```swift
	context.setFillColor(UIColor.red.cgColor)	// 채우고 싶은 색 정하기 
	   
	// 사각형 채울 시    
	let rectangle = CGRect(...)
	context.fill(rectangle)
	
	// 원이나 타원 채울 시
	let circle = CGRect(...)
	context.fillEllipse(in: circle)
	
	// 삼각형 채울 시
	context.fillPath()
	   ```
이후로는 현재 콘텍스트에 그려진 이미지를 가지고 와서 이미지 뷰에 나타낸 후,    

   ```swift
imgView.image = UIGraphicsGetImageFromCurrentImageContext()
   ```

그림 그리기를 끝내면 끝!     

   ```swift
UIGraphicsEndImageContext()
   ```

📑 **<u>추가 지식</u>**    

- **자동 레이아웃 정의 및 설정 방법**

	- 스택 뷰 (StackView) 안 구성 간 width 동일하게 만들기 : `해당 Stack View의 Distribution` → `Fill Equally`

📑 **<u>문법</u>**    

- **`/` 와 `%` 차이** : 몫과 나머지

## 🛠️ 𝔾𝕚𝕥𝕙𝕦𝕓  	

### ☝🏻 <u>iOS_스터디</u>

✔️ **iOS 두잇 책 '카메라와 포토 라이브러리에서 미디어 가져오기' 부분 과제 수행한 것 레퍼지토리에 업로드**  

- 📁 DrawGraphics
   
- 📁   DrawFlowerGraphic (DrawGraphics_mission)


## 🌝 𝕄𝕪 𝕆𝕨𝕟    

✔️ **콘팀 회의록 작성**   

✔️ **빵 외우기 🍞** 

- 케이크도!

✔️ **돌아오는 주차 강의 일정 정리**                
    

  

_
  
# 그냥...끄적임 ✍🏻

개강...말도 안된다아!!     
_

# 오늘의_글귀 📄

  그대가 지나가는 곳에 그대는 흔적을 남긴다.
  그 자국들이 그대 삶이라는 작품을 이룬다.
	
	- 신이 쉼표를 넣은 곳에 마침표를 찍지 말라


<div class="notice--primary" markdown="1">
오늘의 <strong>TIL</strong>은 여기까지!     
      
<strong><u>앞으로의 나에게도 화이팅</u></strong>! 🌸 
</div>
