---
title: "[21.07.27] TIL"
date: 2021-07-27 23:40:28 -0400
toc: true
toc_sticky: true
categories: TIL
---

[21.07.27]

# *오늘의 나 🙌*

## ℙ𝕣𝕠𝕘𝕣𝕒𝕞𝕞𝕚𝕟𝕘 𝕊𝕥𝕦𝕕𝕪✔️   

- **{Golang_스터디}**

	* [14:00 - 15:30] Ch10 공부한 책 내용 공부 및 과제 수행

		- switch문


- **{iOS_스터디}**

	* **iOS 앱 관련 책 맵 뷰로 지도 나타내기까지 공부 + 과제 수행! (헷갈리는 부분 꼼꼼하게)**
		* **Map, MyHomePinMap**

		
			- 세그먼트 컨트롤 (Segemented Control)

			- MKMapKit, MKMapView
			
			- 지도 보여주기 위한 델리게이트

				* CLLocationManagerDelegate 채택, CLLocationManager
			
			- 위도와 경도로 원하는 위치 표시   

				* goLocation( [위도값], [경도값], [확대 정도] )     
				-> 위치 반환(CLLocationCoordinate2D)
					* CLLocationCoordinate2DMake
					* MKCoordinateSpan
					* MKCoordinateRegion
					* setRegion    
				* locationManager(_ manager, locations)    
				 -> 위치 업데이트 후 지도에 위치를 나타내고, 위치 정보 추출하여 텍스트로 표시.
					* CLGeocoder().reverseGeocodeLocation(locations, completionHandler : {...} )

					
			- 위도와 경도로 원하는 위치에 핀 설치   

				* setAnnotation( latitudeValue, longitudeValue, span, title, subtitle )
					- MKPointAnnotation()
					- coordinate(중앙 위치)를 goLocation에서 받아온 값으로 설정  

					
			- 현재 위치 표시하기

				* locationManager.startUpdatingLocation()    

				
		* **헷갈려서 따로 공부한 문법!**

			- Optional
			- self.
			- Delegate



- **{알고리즘_스터디}**

	* [13:00 - 14:00, 16:00 - 17:00] 알고리즘 2문제 풀기

		- 시간 복잡도, 공간 복잡도 생각하기!

	* 알고리즘 5주차 session 3 일단 내 문제 풀이까지 정리

- **{시스템_디자인}**

	* 4주차 내용 정리본 보며 복습!



## 𝔾𝕚𝕥𝕙𝕦𝕓 ✔️

- **{Golang_스터디}**

	* Ch10 공부한 책 내용과 과제 수행 코드 공동레퍼지토리에 업로드
	* 깃 블로그에 정리 내용 업로드!   


- **{iOS_스터디}**

	* iOS 앱 관련 책 공부하고 과제 수행한 것 레퍼지토리에 업로드

		* Map
		* MyHomePinMap

- **{깃_블로그}**

	* 깃 블로그 수정 / 변경!
		- iOS 카테고리
	

	

## 𝕄𝕪 𝕆𝕨𝕟✔️ 
- 올림픽! 🇰🇷 

- 봉사

- [21:00 - 22:00] 모냉고 전체 회의

- 내일 일정 수정 📜


오늘의 나는 여기까지! 
    
_
  
# *그냥...끄적임 ✍🏻*

방금 케냐랑 한 여자 배구 예선 보고 왔는데..     
아니- 판정 실화냐. o(｀ω´ )o    
기계로 No touch 라 판독됐는데 touch 했다고 판정 내리는 건 무슨 경우야...    
진짜 그 이후로 보는 내내 둘이서 씩씩댐 🤬    
그래도 끝까지 최선 다해서 이긴 우리나라 배구팀! 너무 멋지다! ✨     

내일은 프로젝트랑 알고리즘만 해야지....!   
나머지 시간에는 뭔가 알차면서 즐겁게 쉬고 싶은데, 뭘 할 수 있을까 🤔    
_


# *오늘의_글귀 📜*

	작은 찬사에 동요하지 말고 큰 비난에 아파하지 말자.	
	
	- 배두나

<div class="notice--primary" markdown="1">
<u>오늘의 TIL</u>은 여기까지!     
      
앞으로의 나에게도 화이팅 🌸 
</div> 
