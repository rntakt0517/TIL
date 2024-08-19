# Web

[웹이란](#웹이란)

[웹 구조화](#웹-구조화)

[웹 스타일링](#웹-스타일링)

[CSS Box Model](#css-box-model)

---

## 웹이란

- **World Wide Web** : 인터넷으로 연결된 컴퓨터들이 정보를 공유하는 거대한 정보 공간

- **Web** : Web site, Web appliation 등을 통해 사용자들이 정보를 검색하고 상호 작용하는 기술

- **Web site**: 인터넷에서 여러 개의 Web page가 모인 것으로, 사용자들에게 정보나 서비스를 제공하는 공간

- **Web page** : HTML, CSS 등의 웹 기술을 이용하여 만들어진, "Web site"를 구성하는 하나의 요소

---

## 웹 구조화

- **<mark>HTML</mark>** : HyperText Markup Language, 웹 페이지의 의미와 구조를 정의하는 언어

- **Hypertext** : 웹 페이지를 다른 페이지로 연결하는 링크, 참조를 통해 사용자가 한 문서에서 다른 문서로 즉시 접근할 수 있는 텍스트
  
  - 특징 : 비선형성 / 상호연결성 / 사용자 주도적 탐색

- **Markup Language** : 태그 등을 이용하여 문서나 데이터의 구조를 명시하는 언어
  
  - ex) HTML, Markdown
  
  - 예시)
    
    ![image](https://github.com/user-attachments/assets/ce7183f2-3048-4a35-93e7-3b83976a94d7)

- **HTML 구조**
  
  - `<!DOCTYPE html>` : 해당 문서가 html로 문서라는 것을 나타냄
  
  - `<html></html>` : 전체 페이지의 콘텐츠를 포함
  
  - `<title></title>` : 브라우저 탭 및 즐겨찾기 시 표시되는 제목으로 사용
  
  - `<head></head>` : HTML 문서에 관련된 설명, 설정 등 컴퓨터가 식별하는 메타데이터를 작성, 사용자에게 보이지 않음
  
  - `<body></body>` : HTML 문서의 내용을 나타냄, 페이지에 표시되는 모든 콘텐츠를 작성, 한 문서에 하나의 body 요소만 존재

- **HTML Element(요소)**
  
  - 하나의 요소는 여는 태그와 닫는 태그 그리고 그 안의 내용으로 구성됨
  
  - 닫는 태그는 태그 이름 앞에 슬래시가 포함됨
    
    > 닫는 태그가 없는 태그도 존재
  
  ```html
    <a href="https://www.google.com/">구글</a>
    <img src="images/sample.png" alt="컴퓨터">
    <img src="https://picsum.photos/200/300" alt="랜덤이미지">
  ```

- **HTML Attributes(속성)**
  
  - 사용자가 원하는 기준에 맞도록 요소를 설정하거나 다양한 방식으로 요소의 동작을 조절하기 위한 값
  
  - 목적
    
    - 나타내고 싶지 않지만 추가적인 기능, 내용을 담고 싶을 때 사용
    
    - CSS에서 스타일 적용을 위해 해당 요소를 선택하기 위한 값으로 활용됨
  
  - 작성 규칙
    
    1. 속성은 요소 이름과 속성 사이에 공백이 있어야 함
    
    2. 하나 이름의 속성들이 있는 경우엔 속성 사이에 공백으로 구분함
    
    3. 속성 값은 열고 닫는 따옴표롤 감싸야 함

- **HTML 구조 예시**
  
  - VS code에서 `art`+`b`하면 페이지 열림
    
    > `!`+`Tab` 하면 구조가 자동으로 생성됨
  
  - Chrome에서 `F12` 또는 `Ctrl`+`Shift`+`i`

- **HTML Text structure**
  
  - HTML의 주요 목적 중 하나는 텍스트 구조와 의미를 제공하는 것
  
  - ex) h1요소는 단순히 텍스트를 크게만 만드는 것이 아닌 현재 문서의 최상위 제목이라는 의미를 부여하는 것
  
  - 대표적인 HTML Text structure
    
    - Heading & Paragraphs : `h1~6`, `p`
    
    - Lists : `ol`, `ul`, `li`
    
    - Empahsis & Importance : `em`, `strong`

---

## 웹 스타일링

- **<mark>CSS</mark>** : Cascading Style Sheet, 웹 페이지의 디자인과 레이아웃을 구성하는 언어
  
  ![image](https://github.com/user-attachments/assets/3793ab63-d406-433f-a0f2-5d8c80d4812f)
  
  - 적용 방법
    
    1. ~~인라인(Inline) 스타일~~
       
       - HTML 요소 안에 style 속성 값으로 작성
    
    2. 내부(Internal) 스타일 시트
       
       - head 태그 안에 style 태그에 작성
    
    3. 외부(External) 스타일 시트
       
       - 별로 CSS 파일 생성 후 HTML link 태그를 사용해 불러오기

- **CSS Selectors** : HTML 요소를 선택하여 스타일을 적용할 수 있도록 하는 선택자
  
  - 종류
    
    - 기본 선택자 : 전체(`*`), 요소(`tag`), **클래스**(`class`), 아이디(`id`), 속성(`attr`)
      
      > 뒤로 갈 수록 가중치가 더 커짐
    
    - 결합자 (Combinators) : 자손 (`" "(space)`), 자식 (`">"`)

- **명시도** : Specificity, 결과적으로 요소에 적용할 CSS 선언을 결정하기 위한 알고리즘
  
  - <mark>명시도가 높은 순</mark>
    
    1. ~~Importance~~ : `!important`
    
    2. Inline 스타일
    
    3. 선택자 : id > class > 요소
    
    4. 소스 코드 선언 순서
  
  - 계단식 : Cascadel, 한 요소에 동일한 가중치를 가진 선택자가 적용될 때 CSS에서 마지막에 나오는 선언이 사용됨

- 상속
  
  - 상속 되는 속성
    
    - Text 관련 요소(font, color, text-align), opacity, visibility 등
  
  - 상속 되지 않는 속성
    
    - Box model 관련 요소(width, height, border ,box-sizing ...)
    
    - position 관련 요소(position, top/right/bottom/left, z-index) 등
  
  > CSS 상속 여부 확인
  > 
  >  : MDN의 각 속성별 문서 하단에서 상속 여부를 확인할 수 있음

---

## CSS Box Model

웹 페이지의 모든 HTML 요소를 감사는 사각형 상자 모델

- **<mark>박스 타입</mark>** : 페이지에서의 배치 흐름 및 다른 박스와 관련된 동작 방식이 달라짐
  
  1. Block box
  
  2. Inline box

- 박스 표시(Display) 타입
  
  1. **Outer display type**
     
     - **block** 특징 (아래로 이동)
       
       - 항상 새로운 행으로 나뉨
       
       - width와 height 속성 사용 가능
       
       - padding, margin, border로 인해 다른 요소를 상자로부터 밀어냄
       
       - width 속성을 지정하지 않으면 박스는 inline 방향으로 사용 가능한 공간을 모두 차지함
       
       - 대표적인 blck 타입 태그 : `h1~6`, `p`, `div`
     
     - **inline** 특징 (오른쪽으로 이동)
       
       - 새로운 행으로 넘어가지 않음
       
       - width와 height 속성을 사용할 수 없음
       
       - 수직 방향 : padding, margin, border가 적용되지만 다른 요소를 밀어낼 수는 없음
       
       - 수평 방향 : padding, margins, borders가 적용되어 다른 요소를 밀어낼 수 있음
       
       - 대표적인 inline 타입 태그 : `a`, `img`, `span`, `strong`, `em`
     
     - **Normal flow** : 일반적인 흐름 또는 레이아웃을 변경하지 않은 경우의 요소 배치
       
       ![image](https://github.com/user-attachments/assets/370fd61e-8047-4e12-a30c-516b89a2432c)
  
  2. **Inner display type**
     
     - 박스 내부의 요소들이 어떻게 배치될지를 결정
     
     - 속성 : flex
     
     - 추후 CSS layout - Flexbox에서 진행 예정


