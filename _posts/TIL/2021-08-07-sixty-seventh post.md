---
title: "[21.08.07] TIL"
date: 2021-08-07 23:50:28 -0400
toc: true
toc_sticky: true
categories: TIL
---

📝 [21.08.07]

# 오늘의 나 💭

## 👩🏻‍💻 ℙ𝕣𝕠𝕘𝕣𝕒𝕞𝕞𝕚𝕟𝕘 𝕊𝕥𝕦𝕕𝕪    

###  ☝🏻 <u>시스템 디자인_스터디</u> 

✔️ **[15:00 - 17:00] 시스템 디자인 정기 세션**

### ☝🏻 <u>알고리즘_스터디</u>

✔️ **이번 주차 알고리즘 session 3 문제들 풀고 분석 (시간복잡도, 공간복잡도 고려해서!)** 

### ☝🏻 <u>iOS_스터디</u>
✔️ iOS 앱 관련 책 '테이블 뷰 컨트롤러 이용해 할 일 목록 만들기'까지 공부 + 과제 수행! (헷갈리는 부분 꼼꼼하게) : Table, TableWithIconPicker 
📑 **<u>테이블 뷰 컨트롤러 (TableView Controller)</u>**
- `Library` → `TableView Controller`
	
- `Editor` → `Embed in` → `Navigation Controller`
		
- **전환 화면 연결하기** : `Action Segue` → `Show`

- **새 View Controller 클래스 파일 연결하기** : `Cocoa Touch Class` → 스토리 보드에서 해당 뷰 컨트롤러와 연결

- **테이블 뷰에 셀 추가하기** : `TableView Controller` → `Prototype Cells` → `Attributes inspector` → `Identifier`에 셀 이름 지정하기

- **`override func prepare`** : 세그웨이를 이용하여 화면 전환하기 위해 사용.

	<div class="notice--primary" markdown="1">
	🌟 <strong><u>prepare 함수</u></strong>    
    
	: 해당 세그웨이가 해당 뷰 컨트롤러로 전환되기 직전에 호출되는 함수이며, 데이터 전달을 위해 사용된다.     
	</div>
				
- **`override func numberOfSections(in tableView: UITableView) -> Int {}`** : 테이블 안의 섹션의 개수 return    

- **`override func tableView(_ tableView: UITableView, numberOfRowsInSection section: Int) -> Int {}`** : 섹션당 열의 개수 return    

- **`override func tableView(_ tableView: UITableView, cellForRowAt indexPath: IndexPath) -> UITableViewCell {}`** : 앞에서 선언한 변수의 내용을 셀에 적용하는 함수!   

- **`override func tableView(_ tableView: UITableView, commit editingStyle: UITableViewCell.EditingStyle, ForRowAt indexPath: IndexPath) {}`** : 셀의 내용을 삭제하는 함수

-  **`override func tableView(_ tableView: UITableView, titleForDeleteConfirmationButtonForRowAt indexPath: IndexPath) ->String? {}`** : [Delete] 버튼의 `title`을 바꿀 때 사용

- **바 버튼으로 셀 목록 삭제 가능!** : `TableViewController.swift`  → `self.navigationItem.rightBarButtionItem = self.editButtonItem`

	<div class="notice--primary" markdown="1">
	🌟 <strong><u>버튼 위치</u></strong>    
    
	: 왼쪽에 추가하고 싶으면 <code>right</code>를 <code>left</code>로 수정하기만 하면 된다! 
	</div>

- **`override func tableView(_ tableView: UITableView, moveRowAt fromIndexPath: IndexPath, to: IndexPath){}`** : 목록 옮기는 기능의 함수 (`remove` 한 후, 새로운 위치에 `insert` 하는 식으로 옮기도록 블럭 안에서 구현해주면 된다.)

- **_ = navigationController?.popViewController(animated: true)** : 루트 뷰 컨트롤러로 돌아가는 코드 
- **override func viewWillAppear(_ animated: Bool) { [TableView 아울렛 변수].reloadData() }** : 테이블 뷰를 다시 불러옴으로써, 추가된 내용을 목록으로 불러들이는 기능을 수행한다.

📑 <u>문법</u>
- **프로토콜** : 단순한 **선언 형태의 설계도**라고 할 수 있다. 단, 이 프로토콜을 만들었다면 이를 **상속받은 클래스는 반드시 그 내의 함수를 만들어야 하며, 그렇지 않으면 에러가 발생**한다!

-  **자료형의 최댓값 / 최솟값** 

📑 <u>추가 지식</u>
- **자동 레이아웃 정의 및 설정 방법**
	- 미리보기 사용 : `[Adjust Editor Option]` → `[Preview]`

	- 자동 레이아웃 설정 
		- 정렬 조건, 제약 조건

		- SafeArea 영역 조절 : `SuperView`로 변경 

	- 스택 뷰 (StackView)

## 🛠️ 𝔾𝕚𝕥𝕙𝕦𝕓  
     
### ☝🏻 <u>알고리즘_스터디</u>

✔️ **이번 주차 알고리즘 session 3 문제들 풀이와 함께 깃 블로그에 업로드 (시간복잡도, 공간복잡도 고려해서!)** 

<div class="notice--primary" markdown="1">
🌟 <strong>Session 3의 <u>포인트</u></strong>    

 - split()   
 - strip(), lstrip(), rstrip()      
 - defaultdict()
     
</div>    
	

### ☝🏻 <u>iOS_스터디</u>

✔️ iOS 앱 관련 책 공부하고 과제 수행한 것 레퍼지토리에 업로드     

📁 Table

📁 TableWithIconPicker (Table_mission)


## 🌝 𝕄𝕪 𝕆𝕨𝕟 

✔️ **같이 미드!**  

✔️ **게임 몇 판!**         

✔️ 🤫 **구성 및 완성!**      

✔️ **내일 일정 정리**     

_
  
# 그냥...끄적임 ✍🏻

움..못 잘 것 같은..이 느낌..    
그래도 꼭 끝내야겠어! o(｀ω´ )o            
_

# 오늘의_글귀 📄

	하든지 안하든지 둘 중에 하나지.	
	그냥 노력하겠다는 말로 대충 넘어갈 생각하지 말아라.
	
	- 김연경 ✨

<div class="notice--primary" markdown="1">
오늘의 <strong>TIL</strong>은 여기까지!     
      
<strong><u>앞으로의 나에게도 화이팅</u></strong>! 🌸 
</div>
