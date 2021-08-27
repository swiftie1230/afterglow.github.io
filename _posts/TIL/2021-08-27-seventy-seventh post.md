---
title: "[21.08.27] TIL"
date: 2021-08-27 23:50:28 -0400
toc: true
toc_sticky: true
categories: TIL
---


📝 [21.08.27]

# 오늘의 나 💭

## 👩🏻‍💻 ℙ𝕣𝕠𝕘𝕣𝕒𝕞𝕞𝕚𝕟𝕘 𝕊𝕥𝕦𝕕𝕪    

### ☝🏻 <u>iOS_스터디</u>

#### ✔️ **iOS 두잇 책 '탭과 터치 사용해 스케치 앱 만들기' 부분 공부 + 과제 수행!**     

##### 📑 <u>탭 & 터치 기능 구현하기</u>   

📌 <u>멀티 터치 활성화</u>      

: 해당 뷰 선택  → `Attributes inspector`  → `Multiple Touch`       

📌 <u>터치 이벤트 메서드 구현(재정의)하기</u>              

   ```swift
// 터치 시작
override func touchesBegan(_ touches: Set<UITouch>, with event: UIEvent?) {

}

// 손가락이 움직였을 때
override func touchesMoved(_ touches: Set<UITouch>, with event: UIEvent?) {
        
}

// 화면에서 손가락을 떼었을 때
override func touchesEnded(_ touches: Set<UITouch>, with event: UIEvent?) {
        
}
   ```

📌 <u>motionEnded 메서드 구현(재정의)하기</u> : <u>.motionShake</u>              

   ```swift
override func motionEnded(_ motion: UIEvent.EventSubtype, with event: UIEvent?) {
        if motion == .motionShake {
            imgView.image = nil
        }
}
   ```

##### 📑 <u>추가 지식</u>    

- **화면 터치시 키보드 내리기 : [참고 링크](https://zeddios.tistory.com/132 )**

   ```swift
	override func touchesBegan(_ touches: Set<UITouch>, with event: UIEvent?) {
	        self.view.endEditing(true)
	        let touch = touches.first! as UITouch
	        
	        lastPoint = touch.location(in: imgView)
	    }
   ```    
- **Segemented Control**

- **`String` → `CGFloat`로 변환하기** : `CGFloat(Double(String값) ?? 0.0)`

## 🛠️ 𝔾𝕚𝕥𝕙𝕦𝕓  	

### ☝🏻 <u>iOS_스터디</u>

✔️ **iOS 두잇 책 '탭과 터치 사용해 스케치 앱 만들기' 부분 과제 수행한 것 레퍼지토리에 업로드**  

- 📁 TapTouch
   
- 📁   Sketch

- 📁   ChangeColorWidth (Sketch_mission)


## 🌝 𝕄𝕪 𝕆𝕨𝕟    

✔️ **예쁜 까페 (소소한 힐링..)**  

✔️ **빵 외우기 🍞** 

- 케이크도!

✔️ **돌아오는 주차 강의 일정 정리**                
    

  

_
  
# 그냥...끄적임 ✍🏻

오늘 정말 힐링하고 왔다.     
같이 까페에서 공부 후에 맛있는 것도 먹고..바람조차 완벽한 날씨에 저녁 야경도 보고...    
이런 게 힐링이구나, 하는 걸 느꼈다.       
항상 고마워 🤍

또, 누가 화요일에 차 끌고 믓지게 온다고 해서! 진짜 즉흥적으로 그 날 드라이브 가기로 했다 히희 🌝    
와중에 자기 운전실력은 괜찮은데 승차감은 보장 못한다고 ㅋㅋㅋㅋㅋㅋㅋ     
괜찮아!  난 널 믿어...ㅎㅎ 👀    

개강아...오지마....     
_

# 오늘의_글귀 📄

	안다고 무시하지 말고
	모른다고 좌절하지 말고
	사랑한다고 자만하지 말고
	넘어졌다고 자책하지 말고
	네가 소중하지 않다는 생각은
	더더욱 꺼내두지 말고


<div class="notice--primary" markdown="1">
오늘의 <strong>TIL</strong>은 여기까지!     
      
<strong><u>앞으로의 나에게도 화이팅</u></strong>! 🌸 
</div>
