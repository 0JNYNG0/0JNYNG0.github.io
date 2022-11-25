---
title:  "[Unity 2D] 2D 오브젝트 만들기 및 스프라이트 설정" 
excerpt: "[골드메탈] 뱀서라이크 강좌 노트"

categories:
  - Unitystudy
tags:
  - [Unity2D]

toc: true
toc_sticky: true
 
date: 2022-11-18
last_modified_at: 2022-11-23

---

```
하나씩 차근차근 개인적으로 공부한 것을 기록하는 블로그입니다.
참고하시고 잘못되거나 고쳐야 할 부분이 있다면 지적 부탁드립니다!
읽어주셔서 감사합니다🙂
```
***
🌟**유튜브 '골드메탈'님의 [유니티 뱀서라이크] 강좌를 보고 정리해놓은 글입니다.**🌟<br>
<a href="https://www.youtube.com/watch?v=qOTbP9ciJ88" class="btn btn--warning">골드메탈님의 [뱀서라이크 강좌] 보러가기 🎮</a>
{: .notice--primary}

## 2D 스프라이트
- **스프라이트 시트** or **아틀라스** : 여러 스프라이트를 하나로 묶어놓은 형태

- 픽셀아트 스프라이트 설정
    1. ***Pixel Per Unit*** : 해당 픽셀의 **실제 크기(px)**
    2. ***Filter Mode*** : **Point**
    3. ***Compression*** : **None**
<br><br>
![sprite_inspector_base](https://user-images.githubusercontent.com/67769404/202730056-f8fe01de-af8e-4de4-933e-da61780b7a78.png)

## 2D Sprites Slice
- 스프라이트 시트 or 아틀라스의 픽셀아트 자르기
    - 먼저, ***Sprite Mode***를 **Multiple**로 변경해야 한다.
    <br><br>
    ![sprite_inspector_spritemode](https://user-images.githubusercontent.com/67769404/202730618-392dcea3-37a1-48c1-835d-8c13a16c2ab1.png)
    <br><br>
    - Sprite Editor 클릭
        - 좌측 상단 Slice 항목 클릭
            - Pixel Size(X, Y) 및 Padding(X, Y) 설정
            - Slice 버튼 클릭
            <br><br>
            ![spriteEditor_type](https://user-images.githubusercontent.com/67769404/202731234-85640b3f-0d56-41f4-84f4-cdf3c9c5e096.png)
            <br><br>
            ![spriteEditor_Slice](https://user-images.githubusercontent.com/67769404/202731739-4f356424-c1dc-4c2d-88a0-aec8eb2d4662.png)
            <br><br> 
    - 명확하게 스프라이트 상태를 확인하고자 할 때는 우측 상단 Apply 버튼 옆 RGB 버튼을 클릭한다.
    <br><br>
    ![spriteEditor_rgb](https://user-images.githubusercontent.com/67769404/202732416-4e9e4a03-6e9b-4168-977d-d00cfa39c9dc.png)
    <br><br>
    ![spriteEditor_rgb_](https://user-images.githubusercontent.com/67769404/202732335-228a98db-51b4-472f-92fc-1de7d625711d.png)
    <br><br>
    - 잘린 스프라이트 하나씩 클릭하여 각 스프라이트의 이름을 바꿔줄 수 있다.
    <br><br>
    ![spriteEditor_name](https://user-images.githubusercontent.com/67769404/202732749-2f06db70-ea49-4938-8637-9f2de9452109.png)
    <br><br>
    - 우측 상단 Apply 버튼을 눌러 마무리하면 기존 아틀라스 파일에 Slice 처리된 파일들이 생긴다.
    <br><br>
    ![spriteEditor_apply](https://user-images.githubusercontent.com/67769404/202732976-fbc8abeb-c5c1-4581-adbb-6b4014ed806d.png)
    <br><br>
    ![spriteEditor_apply_sprites](https://user-images.githubusercontent.com/67769404/202733275-a3131524-b2a2-407a-b3d7-1ec3e600727a.png)

## 3D 아이콘 크기 조절
Scene 창 우측 상단 맨 끝 부분에 기즈모 버튼을 클릭하여 크기 조절 및 다른 설정들이 가능하다.

## 컴포넌트
게임 객체는 컴포넌트들로 구성되어있다.
Add Component 버튼을 눌러 다양한 컴포넌트를 추가할 수 있다.
- **SpriteRenderer** : 스프라이트를 화면에 그려주는 컴포넌트
    - Additional Settings의 Order in Layer 값을 변경해주어 우선적으로 스프라이트를 그릴 순서를 정해줄 수 있다.(큰 수가 더 위에 그려짐)
<br><br>
- **Rigidbody 2D** or **Rigidbody** : 물리 처리를 담당하는 컴포넌트
    - 기본적으로 중력의 영향을 받기 때문에 게임 종류에 따라 중력을 처리할 필요가 없다면 따로 설정해주어야 한다.
    <br>-> Rigidbody 컴포넌트 내 **Gravity Scale** 값 조절
<br><br>
- **Capsule Collider 2D** : 물리적 충돌이 일어날 표면 부분을 결정하는 컴포넌트(알약 캡슐 모양)
    - Box Collider, Circle Collider 등등 다양한 모양의 Collider 컴포넌트가 존재
    - 충돌면을 컴포넌트 내 **size** 및 **offset** 등으로 자유롭게 설정할 수 있다.
<br><br>