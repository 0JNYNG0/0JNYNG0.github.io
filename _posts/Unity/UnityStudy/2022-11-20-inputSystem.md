---
title:  "[Unity 2D] 새로운 Input System" 
excerpt: "[골드메탈] 뱀서라이크 강좌 노트"

categories:
  - Unitystudy
tags:
  - [Unity2D]

toc: true
toc_sticky: true
 
date: 2022-11-20
last_modified_at: 2022-11-24

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

## Input Manager
기존 Input Manager는 사용자 입력을 받는 오래된 인풋 방식이다.

## 새로운 방식 : Input System 패키지
- 설치<br>
Window -> Package Manager -> Unity Registry 목록으로 변경 -> Input System 설치(install)
<br>

![1111](https://user-images.githubusercontent.com/67769404/203807782-e6eecbd6-0c8c-429f-9412-0e51f689f29e.png)

- 컴포넌트 추가<br>
Add Component로 플레이어 오브젝트에 Player Input을 추가한다. 
<br>

![1111](https://user-images.githubusercontent.com/67769404/203808289-996679ca-994f-4b09-9612-36da6a23b752.png)

- Actions 설정<br>
Input System은 Actions라는 별도의 프로필 에셋이 필요하다.
    - Create Actions 클릭 후 폴더에 플레이어를 위한 "Player" 프로필 에셋 생성
    - 생성 후 Input Actions 창이 열리고 Action Maps 목록에 우리가 만든 Actions 프로필 에셋이 존재한다.
    - Actions 목록에는 다양한 디바이스 인풋들을 관리한다.
<br>

![1111](https://user-images.githubusercontent.com/67769404/203809653-ee2faed4-ef9c-49c6-867b-9744423e7afa.png)

Action Properties에서 세부적인 설정이 가능하다.
- Action > Action Type에서 버튼 클릭인지 값을 내보내는 것인지 설정할 수 있다.
- Action > Control Type에서 값의 형식을 결정한다.
- Interactions는 인풋의 호출 타이밍을 설정할 수 있다. 
    - Hold, Press, Slow Tap, Tap 종류 중에 선택하여 추가할 수 있다.
- Processors는 인풋의 값을 후보정한다.
    - Invert Vector 2, Nomalize Vector 2, Scale Vector 2, Stick Deadzone 종류 중에 선택하여 추가할 수 있다.
- 변경사항을 꼭 Save Asset을 눌러 저장해주어야 한다.
    - Auto-Save 체크박스에 체크하면 자동으로 저장되도록 할 수 있다.


## Input System 스크립트 적용
```c#
using UnityEngine.InputSystem;

public class Player : MonoBehaviour
{
    // void Update()
    // {
    //     inputVec.x = Input.GetAxisRaw("Horizontal")
    //     inputVec.y = Input.GetAxisRaw("Vertical")
    // }


    void OnMove(InputValue value)
    {
        inputVec = value.Get<Vector2>();
    }
}
```
- 기존 Update() 에서 인풋 값을 받아오는 처리를 새로운 함수 OnMove() 에서 간단하게 처리해줄 수 있다. (이 외의 다양한 함수들을 컴포넌트 내 Behavior 아랫단에서 확인할 수 있다.)<br>

![1111](https://user-images.githubusercontent.com/67769404/203811360-4d2ad2e7-d53b-488d-a257-988afd5fec03.png)

```c#
using UnityEngine.InputSystem;
```
Input System을 사용하기 위해 네임스페이스를 등록해준다.
```c#
void OnMove(InputValue value)
    {
        inputVec = value.Get<Vector2>();
    }
```
기존에 Update에서 x, y 인풋 입력 값을 처리해주는 작업은 필요가 없으므로 지운다.
- OnMove 함수는 InputValue 타입의 인자값을 받는다.
- 매개변수로 받아온 value에서 Get<Vector2>() 함수로 Vector2 값을 받아오고 해당 값을 우리가 만든 벡터 변수 inputVec에 넣어준다.
    - Get<T>: 프로필에서 설정한 컨트롤 타입 T 값을 가져오는 함수

- Actions 프로필 에셋에서 이미 normalized를 사용하였으므로 따로 벡터에 대한 normalized 처리는 할 필요가 없다.

<br><br>