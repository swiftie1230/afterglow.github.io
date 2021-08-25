---
title: "[21.08.25] TIL"
date: 2021-08-25 23:50:28 -0400
toc: true
toc_sticky: true
categories: TIL
---


📝 [21.08.25]

# 오늘의 나 💭

## 👩🏻‍💻 ℙ𝕣𝕠𝕘𝕣𝕒𝕞𝕞𝕚𝕟𝕘 𝕊𝕥𝕦𝕕𝕪    

### ☝🏻 <u>iOS_스터디</u>

✔️ **모냉고 Project**

- <u>**로그인 & 회원가입 창 세부 구현 수정**</u>     

	*  비밀번호 가리기 & 보이기 주석 처리 완료.     

	*  구현 필요 없는 부분 정리 완료.

✔️ **iOS 두잇 책 '카메라와 포토 라이브러리에서 미디어 가져오기' 부분 공부 + 과제 수행!**     

📑 **<u>카메라와 포토 라이브러리 관련 앱 기능 구현</u> : <u>UIImagePickerController</u>**    

**카메라**와 **포토라이브러리**를 사용하기 위해서는 **`ImagePickerController`**와 이 컨트롤러를 사용하기 위한 **델리게이트 프로토콜**이 필요하다. 

또한 **미디어 타입이 정의된 헤더파일**이 있어야 한다.

- 다양한 타입들을 정의해 놓은 **헤더 파일 추가** : **`import MobileCoreServices`** 

- ImagePickerController를 사용하기 위한 **델리게이트 프로토콜 추가** : **`UINavigationControllerDelegate`**, **`UIImagePickerControllerDelegate`**
	
본격적으로 사진이나 비디오 촬영과 불러오기 기능을 구현하면 된다. 

- **사진이나 비디오 촬영 & 불러오기 기능 구현**하기

	* **`camera`**나 **`photoLibrary`**의 **사용 가능 여부** 우선 확인!
	* **촬영**이면 **저장 기능 허용**, **아니라면 허용하지 않는다**.
	* **델리게이트**와 **소스 타입**, **미디어 타입** 설정 
	* **촬영**이면 **편집 허용 X**, **아니라면 허용**!
	* **`present`**를 이용해서 뷰에 imagePicker가 보이게 한다.
	* **`camera`**나 **`photoLibrary`**를 **사용할 수 없을 경우**에는 **경고창**을 띄운다.
		
- **델리게이트 메서드 구현하기** 

	* 만약 촬영하거나 포토 라이브러리에서 선택을 하는 등 **<u>동작이 끝났을 경우</u>**
		- **`didFinishPickingMediaWithInfo`** 메서드 실행 : **<u>사진을 저장 & 보여줌</u>.**
	* 만약 동작이 실행되다 말았을 경우 (취소하는 경우)
		- **`imagePickerControllerDidCancel`** 메서드 실행 : **<u>취소 (초기 뷰 보여준다.)</u>**

📑 **<u>추가 지식</u>**    

- **자동 레이아웃 정의 및 설정 방법**

	- 스택 뷰 (StackView)

📑 **<u>문법</u>**    

- **카메라 사용 권한에 대한 키 입력하기** : `info.plist` → `Main storyboard file base name` → `Privacy - Camera Usage Description`

- **마이크로폰에 대한 접근 키 입력하기** : `info.plist` → `Main storyboard file base name` → `Privacy - Microphone Usage Description`

- **포토라이브러리 저장 키 입력하기** : `info.plist` → `Main storyboard file base name` → `Privacy - Photo Library Additions Usage Description`

- **포토라이브러리 접근 키 입력하기** : `info.plist` → `Main storyboard file base name` → `Privacy - Photo Library Usage Description`


## 🛠️ 𝔾𝕚𝕥𝕙𝕦𝕓  	

### ☝🏻 <u>iOS_스터디</u>

✔️ **모냉고 Project**     

- 개인레퍼지토리에 commit !

✔️ **iOS 두잇 책 '카메라와 포토 라이브러리에서 미디어 가져오기' 부분 과제 수행한 것 레퍼지토리에 업로드**  

- 📁 CameraPhotoLibrary
   
- 📁   CollagePhoto (CameraPhotoLibrary_mission)


## 🌝 𝕄𝕪 𝕆𝕨𝕟    

✔️ **산책**   

✔️ **같이 게임 몇 판** 

✔️ **이번 학기 필요한 전공서적 & 강의 일정 정리**                
_
  
# 그냥...끄적임 ✍🏻

하... 개강 두렵다 T^T      
아직 하지도 않았는데 벌써 종강 마려워요...   

괜찮을 줄 알았는데, 막상 저질러보니 모르겠다.       
살짝 생각이 없는 게 더 괜찮은 건가 🤔    
_

# 오늘의_글귀 📄

	지난날의 자기 결정을 후회하지 마라.
	그 땐 그게 최선이었기 때문에 너가 그렇게 결정한 거다.
	그 이유와 상황이 기억 안나는 것 뿐,
	
	과거의 너를 믿고 지금 열심히 살아.
	
	- 익명


<div class="notice--primary" markdown="1">
오늘의 <strong>TIL</strong>은 여기까지!     
      
<strong><u>앞으로의 나에게도 화이팅</u></strong>! 🌸 
</div>
