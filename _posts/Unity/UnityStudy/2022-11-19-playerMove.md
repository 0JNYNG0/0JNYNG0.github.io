---
title:  "[Unity 2D] 플레이어 이동" 
excerpt: "유니티 학습 노트"

categories:
  - Unitystudy
tags:
  - [Unity2D]

toc: true
toc_sticky: true
 
date: 2022-11-19
last_modified_at: 2022-11-19

---
```
하나씩 차근차근 개인적으로 공부한 것을 기록하는 블로그입니다.
참고하시고 잘못되거나 고쳐야 할 부분이 있다면 지적 부탁드립니다!
읽어주셔서 감사합니다🙂
```
## 폴더 및 C#스크립트 파일 생성
따로 스크립트 폴더를 만들고 해당 스크립트 폴더 안에 C# Script 파일을 만들자.<br>
이 파일은 하나의 컴포넌트의 역할을 하며 사용하고자 하는 오브젝트의 컴포넌트란에 Drag&Drop으로 부착하거나 Add Component를 통해서 추가가 가능하다.

## C# 스크립트
```c#
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class Player : MonoBehaviour
{
    public Vector2 inputVec;
    public float speed;

    Rigidbody2D rigid;

    void Awake()
    {
        rigid = GetComponent<Rigidbody2D>(); // 초기화 작업
    }

    void Update()
    {
        // GetAxis = 부드럽게 보정됨 / GetAxisRaw = 수치가 알맞게 끊어지도록 설정됨
        inputVec.x = Input.GetAxisRaw("Horizontal");
        inputVec.y = Input.GetAxisRaw("Vertical");
    }

    void FixedUpdate()
    {
        Vector2 nextVec = inputVec.normalized * speed * Time.fixedDeltaTime;

        rigid.MovePosition(rigid.position + nextVec);
    }
}

```
***
```c#
public class Player : MonoBehaviour {
    public Vector2 inputVec;
    public float speed; // 스크립트 파일 외부에서도 접근 가능

    Rigidbody2D rigid; // 따로 접근 불가능
}

* MonoBehaviour : 기본적인 게임 로직 구성에 필요한 것들을 지닌 클래스
```
- `public 타입 변수명;`
    <br>
    맨앞에 **public**을 붙여줌으로써 컴포넌트에서 사용자가 실시간으로 바뀌는 값을 보거나 따로 접근, 조작이 가능해진다.
<br>

## 키보드 입력 받기
```c#
Vector2 inputVec;

void Update()
    {
        inputVec.x = Input.GetAxisRaw("Horizontal");
        inputVec.y = Input.GetAxisRaw("Vertical");
    }
```
- `Input.GetAxisRaw("InputName");`
    <br>
    **<u>Edit - Project Settings - Input Manager</u>** 에서 **InputName**으로 넣어줄 이름을 확인할 수 있고, Negative Button, Positive Button 등을 자유롭게 설정할 수 있다.<br>
    (Horizontal, Vertical 같이 기본적으로 설정되어있는 이름들이 존재하고 커스텀이 가능하다)
    - **GetAxisRaw** : 더욱 명확한 입력값 컨트롤이 가능해짐
    - **GetAxis** : GetAxisRaw와 달리 입력값이 약간 미끄러지듯 부드럽게 보정됨
<br>

## 플레이어 이동 구현
```c#
Rigidbody2D rigid; // 물리를 처리하는 Rigidbody 변수

void Awake()
{
    rigid = GetComponent<Rigidbody2D>(); // 초기화 작업
}
```
- `GetComponent<T>();` : 해당 오브젝트에서 컴포넌트를 가져오는 함수
    <br>
    < >안에 원하는 컴포넌트의 타입을 적어 해당 컴포넌트를 가져올 수 있다.
    <br><br>

```c#
public float speed;

void FixedUpdate()
{
    Vector2 nextVec = inputVec.normalized * speed * Time.fixedDeltaTime;

    rigid.MovePosition(rigid.position + nextVec);
}
```
- 물리적인 이동 구현에는 다양한 방법이 존재한다.
    1. 힘 전달 : `rigid.AddForce(inputVec);`
    2. 속도 제어 : `rigid.velocity = inputVec;`
    3. 위치 이동 : `rigid.MovePosition(rigid.position + inputVec);`
    <br>
    ex) 뱀서라이크류 게임은 플레이어가 상하좌우 이동이 구현되어야 하므로 '위치 이동'을 사용한다.
    - 개발하는 게임의 특성에 따라 자유롭게 선택
    <br><br>
- `FixedUpdate(){ }` : 물리 연산 프레임마다 호출되는 생명주기
    <br>
    그냥 매 프레임마다 호출되는 Update()와는 달리 물리 연산을 해야할 때 주로 사용한다.
    <br><br>
- `Vector2 nextVec = inputVec.normalized * speed * Time.fixedDeltaTime`
    <br>
    사용자의 입력에 일정한 시간동안 일정한 값만큼 이동해야 하기 때문에 입력에 따른 새로운 Vector2 값을 만들어준다.
    - `.normalized` : 벡터 값이 어느 방향이든지 크기가 1이 되도록 좌표가 수정된 값 (이 작업이 없다면 수평, 수직 이동보다 대각선 이동 속도가 훨씬 빨라질 것이다)
    - `Time.fixedDeltaTime` : 물리 프레임 중 한 프레임이 소비한 시간
        <br>
        `fixedDeltaTime`은 FixedUpdate에서 사용하는 반면에 `Time.deltaTime`은 한 프레임이 소비한 시간으로 Update에서 사용한다.
    - `rigid.MovePosition(rigid.position + nextVec);`
        <br>
        물리 변수 rigid의 위치를 바꿔주는 MovePosition() 함수에 '해당 플레이어의 위치 + 물리 프레임에 따라 바뀐 벡터값'을 넣어 위치를 옮겨준다.

<br><br>