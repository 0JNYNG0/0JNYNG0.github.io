---
title:  "[프론트엔드] CSS 선택자" 
excerpt: "FrontEnd Study"

categories:
  - FastCampus
tags:
  - [FastCampus, FrontEnd]

toc: true
toc_sticky: true
 
date: 2023-01-26
last_modified_at: 2023-01-26
---
```
하나씩 차근차근 개인적으로 공부한 것을 기록하는 블로그입니다.
참고하시고 잘못되거나 고쳐야 할 부분이 있다면 지적 부탁드립니다!
읽어주셔서 감사합니다🙂
```
<br>

# CSS 선택자 (CSS Selector)
CSS 선택자는 크게 다섯 가지로, **기본**, **복합**, **가상 클래스**, **가상 요소**, **속성**으로 나뉜다.

<br><br><br>

## 기본 선택자
다음 순서는 우선 순위 점수 크기별로 나열했으며, 순서대로 기억하면 좋다.
- `*` **전체 선택자**(Universal Selector) : **<u>모든 요소</u>**를 선택

- `ABC` **태그 선택자**(Type Selector) : **<u>태그 이름</u>**이 `ABC`인 요소 선택

- `.ABC` **클래스 선택자**(Class Selector) : HTML의 **<u>class 속성 값</u>**이 `ABC`인 요소 선택

- `#ABC` **아이디 선택자**(Id Selector) : HTML의 **<u>Id 속성 값</u>**이 `ABC`인 요소 선택

<br><br>

## 복합 선택자
- `ABCXYZ` **일치 선택자**(Basic Combinator) : 선택자 `ABC`와 `XYZ`를 **<u>동시에 만족</u>**하는 요소 선택
    ```css
        span.orange { color: red; }

        /* .orangespan { } 이는 구분이 어렵기 때문에 "태그 + 클래스" 순서처럼 태그가 앞에 오도록 작성한다. */
    ```

- `ABC > XYZ` **자식 선택자**(Child Combinator) : 선택자 `ABC`의 **자식 요소** `XYZ` 선택

- `ABC XYZ` **하위(후손) 선택자**(Descendant Combinator) : 선택자 `ABC`의 **하위 요소** `XYZ` 선택 (**<u>띄어쓰기</u>**가 선택자의 기호!!)

- `ABC + XYZ` **인접 형제 선택자**(Adjacent Sibling Combinator) : 선택자 `ABC`의 **다음 형제** 요소 `XYZ` **<u>하나</u>**를 선택

- `ABC ~ XYZ` **일반 형제 선택자**(General Sibling Combinator) : 선택자 `ABC`의 **다음 형제** 요소 `XYZ` **<u>모두</u>**를 선택

<br>

```
💡 CSS 선택자는 뒤에서부터 해석하면 구별하기 쉽다! 💡
```
``` css
ul > .orange { }
/* ex. orange 클래스에 해당하는 태그를 찾고, 이 중 <ul> 태그 안에 존재하는 태그들을 찾는다. */
```

<br><br>

## 가상 클래스 선택자
가상 클래스 선택자는 중간에 `:` 기호가 붙는다.
<br>

- `ABC:hover` **HOVER** : 선택자 `ABC` 요소에 **마우스 커서가 올라가 있는 동안** 선택

- `ABC:active` **ACTIVE** : 선택자 `ABC` 요소에 **마우스를 클릭하고 있는 동안** 선택

- `ABC:focus` **FOCUS** : 선택자 `ABC` 요소가 **포커스되면** 선택
    - Focus가 될 수 있는 요소 -> **<u>HTML 대화형 콘텐츠</u>**<br>
    `INPUT`, `A`, `BUTTON`, `LABEL`, `SELECT` 등 여러 요소가 존재하고 이런 HTML 대화형 콘텐츠를 제외하고도 `tabindex 속성`을 사용한 요소 또한 포함이 가능하다. (검색 : **HTML 대화형 콘텐츠 mdn**)

    - `tabindex` 속성은 Tab 키를 사용해 Focus 할 수 있는 순서를 지정하는 속성이며, 값으로 -1을 넣어주어 Focus가 될 수 있는 요소로 만들어줄 수 있다. (검색 : **tabindex mdn**)
    
    ```html
    <div class="box" tabindex="-1"></div>
    <!-- 논리적 흐름에 방해되지 않도록 꼭 -1을 값으로 넣어주도록 하자. -->
    ```

- `ABC:first-child` **FIRST CHILD** : 선택자 `ABC`가 **형제 요소 중 <u>첫째</u>**라면 선택

- `ABC:last-child` **LAST CHILD** : 선택자 `ABC`가 **형제 요소 중 <u>막내</u>**라면 선택

- `ABC:nth-child(n)` **NTH CHILD** : 선택자 `ABC`가 **형제 요소 중 <u>(n)째</u>**라면 선택
    - 이는 전체 선택자 `*`를 사용해 아래와 같이 다양하게 활용이 가능하다<br>

    ```css
    /* fruits 클래스 요소의 모든 하위 요소 중 2번 째 형제 요소를 선택한다 */
    .fruits *:nth-child(2) { }

    /* Zero-Based Numbering :: n은 0부터 시작한다 */

    /* 0, 2, 4, 6, ,,, 으로 짝수 번째 요소에 해당하는 형제 요소들을 모두 선택 */
    .fruits *:nth-child(2n) { }
    /* 1, 3, 5, 7, ,,, 으로 홀수 번째 요소에 해당하는 형제 요소들을 모두 선택 */
    .fruits *:nth-child(2n + 1) { }

    /* 짝수, 홀수 말고도 다양하게 조건을 걸어줄 수 있다 */

    /* 2, 3, 4, 5, ,,, 2번째 이후의 형제 요소들을 모두 선택 */
    .fruits *:nth-child(n + 2) { }
    /* 3, 2, 1 첫 번째부터 3번째 까지의 형제 요소들만 모두 선택 */
    .fruits *:nth-child(-n + 3)
    ```

- `ABC:not(XYZ)` **부정 선택자**(Negation) : 선택자 `XYZ`**가 아닌** `ABC` 요소 선택

<br><br>

## 가상 요소 선택자