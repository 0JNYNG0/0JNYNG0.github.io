---
title:  "[Unity Basis] 유니티 게임오브젝트의 흐름 (LifeCycle)" 
excerpt: "[골드메탈] 유니티 입문 강좌"

categories:
  - Unitystudy
tags:
  - [Unity2D]

toc: true
toc_sticky: true
 
date: 2022-11-29
last_modified_at: 2022-11-29

---
```
하나씩 차근차근 개인적으로 공부한 것을 기록하는 블로그입니다.
참고하시고 잘못되거나 고쳐야 할 부분이 있다면 지적 부탁드립니다!
읽어주셔서 감사합니다🙂
```
***
🌟**유튜브 '골드메탈'님의 [유니티 입문강좌] 강좌를 보고 정리해놓은 글입니다.**🌟<br>
<a href="https://www.youtube.com/watch?v=PyN3JkPTpAI&list=PLO-mt5Iu5TeYI4dbYwWP8JqZMC9iuUIW2&index=6">골드메탈님의 [유니티 입문강좌 B5] 보러가기 🎮</a>
{: .notice--primary}

## Awake() - 초기화 (최초)
- Awake : 게임 오브젝트를 처음 생성할 때 최초 1번 실행

```c#
void Awake()
{
    Debug.Log("플레이어 데이터가 준비되었습니다.");
}
```

## Start() - 초기화 (프레임 시작)
- Start : 업데이트 시작 직전 최초 1번 실행

```c#
void Start()
{
    Debug.Log("사냥 장비를 챙겼습니다.");
}
```

## FixedUpdate() - 프레임 (물리)
- FixedUpdate : 물리 연산 업데이트<br>
컴퓨터 사양에는 전혀 영향을 받지않고 고정된 실행 주기로 꾸준히 일정하게 호출하기 때문에 CPU를 많이 사용하게된다. 이렇기 때문에 물리 연산과 관련된 로직만 넣는다. 대략 보통 50프레임 정도로 호출된다.

```c#
void FixedUpdate()
{
    Debug.Log("이동중"); // 프레임 별로 계속 호출됨
}
```

## Update() - 프레임 (로직)
- Update : 게임 로직 업데이트<br>
물리 연산을 제외한 나머지 주기적으로 작동해야하는 로직을 넣을 때 주로 사용한다. Update는 개개인의 컴퓨터 사양에 따라 실행 주기가 떨어질 수 있다. FixedUpdate와 달리 보통 60프레임 정도로 호출된다. 이 프레임 호출은 컴퓨터 사양 및 상황에 영향을 미친다.

```c#
void Update()
{
    Debug.Log("몬스터사냥!");
}
```

## LateUpdate() - 프레임 (후처리)
- LateUpdate : 모든 업데이트가 끝난 후 실행<br>
보통 플레이어를 따라가는 카메라나 로직의 후처리를 주로 다루기 위해 사용한다.

```c#
void LateUpdate()
{
    Debug.Log("경험치 획득.");
}
```
Update()에서 호출하는 것과 LateUpdate()에서 호출하는 로그가 같은 속도로 찍히는 것을 확인해볼 수 있다.

## OnDestroy() - 해제
- OnDestroy : 게임 오브젝트가 삭제될 때 실행

```c#
void OnDestroy()
{
    Debug.Log("플레이어 데이터를 해제하였습니다.");
}
```
Hierarchy 창에서 오브젝트가 삭제될 때 해당 OnDestroy 함수 내 로직이 실행된다.

## OnEnable() - 활성화
- OnEnable : 게임 오브젝트가 활성화 되었을 때 실행<br>
Awake() 실행과 Start() 실행 사이에 OnEnable()이 최초 실행되고 활성화 할 때마다 매번 실행된다.

```c#
void Enable()
{
    Debug.Log("플레이어 로그인했습니다.");
}
```


## OnDisable() - 비활성화
- OnDisable : 게임 오브젝트가 비활성화 되었을 때 실행<br>
오브젝트를 비활성화 했을 때마다 매번 실행된다.

```c#
void Enable()
{
    Debug.Log("플레이어 로그아웃 했습니다.");
}
```

<br>