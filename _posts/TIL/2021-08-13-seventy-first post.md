---
title: "[21.08.13] TIL"
date: 2021-08-13 23:50:28 -0400
toc: true
toc_sticky: true
categories: TIL
---

📝 [21.08.13]

# 오늘의 나 💭

## 👩🏻‍💻 ℙ𝕣𝕠𝕘𝕣𝕒𝕞𝕞𝕚𝕟𝕘 𝕊𝕥𝕦𝕕𝕪    

### ☝🏻 <u>iOS_스터디</u>

#### ✔️ iOS 앱 관련 책 '음악 재생하고 녹음하기'까지 공부 + 과제 수행! (헷갈리는 부분 꼼꼼하게) : Audio, Audio_Mission 

##### 📑 **AVAudioPlayer**
- **프로그레스 뷰**<sup>Progress View</sup>
	
- **슬라이더**<sup>Slider</sup>
		
- **스택 뷰** : `Embeded in` → `Stack View`

- **오디오 재생을 위한 초기화** 

	<div class="notice--primary" markdown="1">
	💡 <strong><u>추가 지식</u> : <u>Bundle.main.url(for Resource: , withExtension: )</u></strong>    
	    
	우리가 관심 있는 번들이 있다면 그것이 무엇이든 Bundle.main 속성 타입을 사용해서 접근할 수 있다.     
	대부분의 경우 <code>url(forResource:withExtension:)</code> (또는 비슷한 것 중 하나)를 사용해서 특정 자원의 위치를 알아낼 수 있음!      
	
	예를 들어 만약 우리의 앱 번들이 Photo.jpg 라는 이름을 가진 파일을 포함하고 있다면 다음과 같이 URL을 만들어서 접근할 수 있다는 뜻이다.     
		
	```swift    
	Bundle.main.url(forResource: "Photo", withExtension: "jpg") 
	```    
  </div>


- **재생 시간 초기화하기**   

- **버튼 제어** :    
	**`[버튼 아울렛 변수].isEnabled` = `[Boolean 값]`**    
	
  **`[AVAudioPlayer 변수].play()`** : 재생   
  **`[AVAudioPlayer 변수].pause()`** : 일시 정지   
  **`[AVAudioPlayer 변수].stop()`** : 정지   		
  
- **재생 시간 표시 및 볼륨 제어** : timer 사용(`[AVAudioPlayer 변수].currentTime` , `[AVAudioPlayer 변수].duration` 이용하면 됨)    

- **녹음을 위한 초기화** : 녹음 파일이 재생 파일에 겹쳐서 저장되는 일을 막기 위한 함수 생성(조건문 사용)    

- **녹음 및 재생 모드 변경**    

- **녹음 및 정지 제어**

-  **녹음 시간 표시**

##### 📑 문법
- **do-try-catch문** : 오류가 발생할 수 있는 함수를 호출할 때 `do-try-catch`문을 사용한다.    

	<div class="notice--primary" markdown="1">
	🌟 <strong><u>여기서 잠깐!</u> : <u>여기서 오류 발생할 수 있는 함수는 무엇일까?</u></strong>      
    
	"<strong>func <code>함수명</code> <code>(입력 파라미터)</code> throws -> <code>리턴 파라미터</code></strong>" 형태를 가지는 함수를 의미한다.       
	</div> 


## 🛠️ 𝔾𝕚𝕥𝕙𝕦𝕓  	

### ☝🏻 <u>iOS_스터디</u>

✔️ **iOS 앱 관련 책 공부하고 과제 수행한 것 레퍼지토리에 업로드**     

 📁 Audio & Audio_Mission

✔️ **모냉고 Project**     

- 개인레퍼지토리 생성해서 commit !



## 🌝 𝕄𝕪 𝕆𝕨𝕟   

✔️ **보건소, 치과** 

✔️ **모냉고 iOS 회의**              

✔️ **모냉고 전체 회의**     

✔️ **🤫 구성**     

✔️ **빵 암기 🥖**     

_
  
# 그냥...끄적임 ✍🏻

쓸데없는 곳에서 자꾸 신경쓰이는 일이 일어나는 것 같은 요즘.      
왜 저래 진짜...       
저에게는 그런 것들에 쏟을 시간과 여유가 없으니 그냥 지나가주세요 🙅🏻‍♀️       

_

# 오늘의_글귀 📄

	눈 감지 말고 똑바로 봐.
	
	두려움의 실체는 생각과 다를 수 있어,
	
	- Finding Nemo 중


<div class="notice--primary" markdown="1">
오늘의 <strong>TIL</strong>은 여기까지!     
      
<strong><u>앞으로의 나에게도 화이팅</u></strong>! 🌸 
</div>
