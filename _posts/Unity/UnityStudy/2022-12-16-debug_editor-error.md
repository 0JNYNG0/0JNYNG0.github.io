---
title:  "[Unity Debug] VS 에디터 연결 문제" 
excerpt: "디버그 오류"

categories:
  - Unitystudy
tags:
  - [Debug]

toc: true
toc_sticky: true
 
date: 2022-12-16
last_modified_at: 2022-12-16

---
```
하나씩 차근차근 개인적으로 공부한 것을 기록하는 블로그입니다.
참고하시고 잘못되거나 고쳐야 할 부분이 있다면 지적 부탁드립니다!
읽어주셔서 감사합니다🙂
```
***

## 에디터 문제 발생
유니티에서 Visual Studio 에디터를 열어 코드를 작성하는데 자동완성이 되지 않는 경우가 생기거나 또 동시에 코드의 특정 함수나 클래스를 구분해주는, 정보를 알려주는 코드의 색깔이 안바뀌는 경우가 생긴다.<br>
- 자동완성 목록 보기 : ***Ctrl + Space***<br>

Ctrl + Space 를 눌러봐도 자동완성 목록이 뜨지 않는 경우! 다음과 같이 해결해보자.

## 해결 방법
- Edit > Preferences > External Tools 메뉴를 연다
- External Tools에서 External Script Editor를 사용하고자 하는 Visual Studio 프로그램으로 바꿔주고 Visual Studio가 켜져있다면 재실행하면 잘 될 것이다.
    - 오류가 났다면 Open by file extension 항목에 체크됐었을 것이다.
- 만약 Visual Studio가 항목에 없다면 Browse..을 눌러 Visual Studio가 설치된 경로를 찾아 직접 등록해줄 수 있다.
    - Visual Studio 설치 경로 (년도만 변경)<br>
    C:\Program Files (x86)\Microsoft Visual Studio\2017\Community\Common7\IDE\devenv

![111](https://user-images.githubusercontent.com/67769404/208123853-d4bf27f3-99e0-459c-be7b-4ac5e65cd9bb.png)<br><br>
![1111](https://user-images.githubusercontent.com/67769404/208123859-3ce1ce40-6b05-4b24-8881-093aa3de114b.png)
<br><br>

만약 Visual Studio를 유니티 설치를 할 때가 아닌, 따로 설치한 경우 직접 유니티 관련 설치를 진행해줘야 한다.
- Visual Studio 도구 > 도구 및 기능 가져오기 > Visual Studio Installer
- Installer 창에서 모바일 및 게임 항목에 "Unity를 사용한 게임 개발"을 설치하면 된다.<br>
![111](https://user-images.githubusercontent.com/67769404/208125488-527a69b1-9a87-4625-a573-102a0e622757.png)
<br><br><br>