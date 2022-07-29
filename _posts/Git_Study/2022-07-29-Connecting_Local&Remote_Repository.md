---
title: "[22.07.29] How to Connect Local and Remote repository"
date: 2022-07-29 03:00:28 -0400
toc: true
toc_sticky: true
categories: Git_Study
---
     
     
# ✏️ <u>How to Connect Local and Remote repository</u>  

이미 학교에서까지 배웠는데도 항상 헷갈릴 뿐더러, 인터넷에 제대로 된 깔끔한 과정을 정리해 놓은 곳이 없는 것 같아 이렇게 내가 직접 정리해 보기로 결정! 사실 내가 볼 용도라고 하는 게 가장 적절하겠다.             

물론, 이미 깃 초기 설정은 완료한 상태라고 가정한다.


## 📝 1. Create an Remote Repository : 우선 원격 저장소를 생성하자

새로운 원격 저장소를 Github에서 생성하자.

<img width="788" alt="Screen Shot 2022-07-29 at 4 11 32 PM" src="https://user-images.githubusercontent.com/63195670/181703794-06f069b8-a14a-4a1d-821e-500ff30427e0.png">

여기서 나는 `Front_Study`라는 이름으로 생성했다.


* * *


## 📝 2. Next, Designate a Local Repository : 다음으로, 로컬 저장소를 지정 & 설정한다

1. 로컬저장소로 지정하고 싶은 폴더로 이동한다.


2. `git init` 명령어를 입력한다. (해당 폴더를 git 로컬저장소로 설정하는 명령어라고 생각!)


* * *


## 📝 3. Connet Local & Remote Repository : 로컬 저장소와 원격 저장소를 연결한다

`git remote add origin [깃허브 주소]`를 입력!


<img width="811" alt="Screen Shot 2022-07-29 at 4 20 12 PM" src="https://user-images.githubusercontent.com/63195670/181705020-ff7cd6ad-cf73-46e9-8b7f-c3c0ac5ed647.png">


* * *


## 📝 4. Rename the master branch to main : 기본 브랜치의 이름을 master에서 main으로 재설정한다

터미널에 `git branch -M main`를 입력!

자동으로 재설정하는 코드이다.

<div class="notice--primary" markdown="1">
🙋🏻‍♀️ <strong><u>여기서 잠깐!</u> : <u>왜 굳이?</u></strong>    

올 6월 Go 언어가 인종차별적 요소나 주종 관계의 의미를 담고 있는 whitelist/blacklist와 master/slave라는 용어를 프로젝트에서 제거하기로 결정하면서 업계 전반에 이런 부분을 제거하는 움직임이 일어났다.(이 부분에 대해서 그런 의미로 받아들여지지 않는다는 반대 의견도 있지만 불편한 사람이 있다면 바꾸는 게 맞는다고 생각한다.)

이후 master를 기본 브랜치로 사용하던 Git에서도 이 논의가 이루어졌고 브랜치를 사용자가 지정할 수 있도록 변경하였다.(Regarding Git and Branch Naming 참고) 사실 master는 관례상 최초 생성하는 기본 브랜치로 사용하는 이름일 뿐 다른 의미는 없고 실제 많은 저장소가 기본 브랜치를 다른 브랜치로 바꾸어서 사용하고 있었다.

이어서 GitHub도 기본 브랜치를 master에서 main으로 변경하기로 했고 이는 10월 1일부터 적용되었다. 그래서 이제 저장소를 생성할 때 초기화 옵션을 선택하면 main 브랜치가 기본브랜치로 생성됨을 알려준다.

초기화하지 않고 저장소를 생성할 때의 커맨드라인 안내 메시지도 main으로 초기화하도록 변경되었다. 이전에는 git이 알아서 기본으로 master를 기본으로 사용하였지만 main은 그렇지 않기 때문에 명시적으로 git branch -M main으로 브랜치를 생성하는 명령어가 추가되었다!
    
</div>


* * *


## 📝 5. If there are early files, PULL them: 만약 존재할 때를 생각해 Pull 먼저 하기

터미널에 `git pull origin main`를 입력!

**이미 원격 저장소에 파일들이 있을 때를 대비**하여 일단 pull 먼저! 

반대의 경우라면 굳이 안 해도 되겠지.


* * *


## 📝 6. add & commit to Local Repository: 로컬 저장소에 파일 add & commit 하기

1. `git add .`

2. `git commit -m "[메세지 내용]"` 명령어를 입력한다. (해당 폴더를 git 로컬저장소로 설정하는 명령어라고 생각!)

3. `git push origin main`

이후 원격 저장소를 확인해보면 성공적으로 sync 되어 업데이트 된 것을 확인할 수 있다. 
