# CSS Layout

[CSS Box Model](#css-box-model)

- 타입, 표시 타입, 구성 요소

[CSS Layout](#css-layout)

- position, flexbox

---

## CSS Box Model

웹 페이지의 모든 HTML 요소를 감사는 사각형 상자 모델

- **박스 타입** : 페이지에서의 배치 흐름 및 다른 박스와 관련된 동작 방식이 달라짐
  
  1. Block box
  
  2. Inline box

- 박스 표시(Display) 타입
  
  1. **<mark>Outer display type</mark>**
     
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
  
  2. **<mark>Inner display type</mark>**
     
     - 박스 내부의 요소들이 어떻게 배치될지를 결정
     
     - 속성 : flex
     
     - 추후 CSS layout - Flexbox에서 진행 예정

- 박스 구성 요소
  
  ![image](https://github.com/user-attachments/assets/5ab18e0b-da82-48d3-9e0c-7464e0d72d89)
  
  - **Content box**
    
    - 실제 콘텐츠가 표시되는 영역 크기
    
    - width 및 height 속성을 사용하여 크기 조정
  
  - **Padding box**
    
    - 콘텐츠 주위에 공백
    
    - padding 관련 속성을 사용하여 크기 조정
  
  - **Border box**
    
    - 콘텐츠와 패딩을 래핑
    
    - 박스와 다른 요소 사이의 공백
    
    - margin 관련 속성을 사용하여 크기 조정
  
  - **Margin box**
    
    - 콘텐츠, 패딩 및 테두리를 래핑
    
    - 박스와 다른 요소 사이의 공백
    
    - margin 관련 속성을 사용하여 크기 조정
  
  > - **shorthand 속성**
  >   
  >   - `border` : width, style, color를 한번에 설정하기 위한 속성
  >   
  >   - `margin` & `padding` : 4방향의 속성을 각각 지정하지 않고 한번에 지정할 수 있는 속성
  > 
  > - **box-sizing 속성**
  >   
  >   - CSS는 border box가 아닌 content box의 크기를 width 값으로 지정 (불편)
  >   
  >   - 따라서 `box-sizing:`으로 대체 상자 모델로 변경할 수 있음
  > 
  > - **기타 display 속성**
  >   
  >   - `inline-block` 
  >     
  >     - inline과 block 요소 사이의 중간 지점을 제공하는 display 값
  >     
  >     - 새로운 행으로 넘어가지 않음
  >     
  >     - width 및 height 속성 사용 가능
  >     
  >     - padding, margin 및 border로 인해 다른 요소가 상자에서 밀려남
  >     
  >     > 요소가 줄 바꿈 되는 것을 원하지 않으면서 너비와 높이를 적용하고 싶은 경우에 사용
  >   
  >   - `none`
  >     
  >     - 요소를 화면에 표시하지 않고, 공간조차 부여되지 않음

---

## CSS Layout

각 요소의 위치와 크기를 조정하여 웹 페이지의 디자인을 결정하는 것

- <mark>**CSS Position**</mark>
  
  요소를 Normal Flow에서 제거하여 다른 위치로 배치하는 것
  
  - 이동 방향 : top, right, bottom, left
  
  - 목적 : 페이지 특정 항목의 위치를 조정하는 것
  
  - 유형
    
    1. **`static`**
       
       - 요소를 Normal Flow에 따라 배치
       
       - top, right, bottom, left 속성이 적용되지 않음
       
       - 기본 값
    
    2. **`relative`**
       
       - 요소를 Normal Flow에 따라 배치
       
       - 자신의 원래 위치(static)을 기준으로 이동
       
       - top, right, bottom, left 속성으로 위치를 조정
       
       - 다른 요소의 레이아웃에 영향을 주지 않음 (요소가 차지하는 공간은 static일 때와 같음)
    
    3. **`absolute`**
       
       - 요소를 Normal Flow에서 제거
       
       - 가장 가까운 relative 부모 요소를 기준으로 이동 (없다면 body 태그 기준)
       
       - top, right, bottom, left 속성으로 위치를 조정
       
       - 문서에서 요소가 차지하는 공간이 없어짐
    
    4. **`fixed`**
       
       - 요소를 Normal Flow에서 제거
       
       - 현재 화면영역(viewport)을 기준으로 이동
       
       - 스크롤해도 항상 같은 위치에 유지됨
       
       - top, right, bottom, left 속성으로 위치를 조정
       
       - 문서에서 요소가 차지하는 공간이 없어짐
    
    5. **`sticky`**
       
       - relative와 fixed의 특성을 결합한 속성
       
       - 스크롤 위치가 임계점에 도달하기 전에는 relative처럼 동작
       
       - 스크롤이 특정 임계점에 도달하면 fixed처럼 동작하여 화면에 고정됨
       
       - 만약 다음 sticky 요소가 나오면 다음 sticky 요소가 이전 sticky 요소의 자리를 대체 (두 요소의 고정되어야 할 위치가 겹치게 되기 때문)
    
    > ### z-index
    > 
    > - 정의
    >   
    >   - 요소의 쌓임 순서(stack order)를 정의하는 속성
    >   
    >   - 정수 값을 사용해 z축 순서를 지정
    >   
    >   - 값이 클수록 요소가 위에 쌓이게 됨
    >   
    >   - static이 아닌 요소에만 적용됨
    > 
    > - 특징
    >   
    >   - 기본값은 auto
    >   
    >   - 부모 요소의 z-index 값에 영향을 받음
    >   
    >   - 같은 부모 내에서만 z-index 값을 비교
    >   
    >   - 부모의 z-index가 낮으면 자식의 z-index가 아무리 높아도 부모보다 위로 올라갈 수 없음
    >   
    >   - z-index 값이 같으면 HTML 문서 순서대로 쌓임

- <mark>**CSS Flexbox**</mark>
  
  요소를 행과 열 형태로 배치하는 **1차원** 레이아웃 방식
  
  - 구성 요소
    
    ![image](https://github.com/user-attachments/assets/0594b731-2dd6-4f27-b816-989aac89be74)
    
    1. **main axis (주 축)**
       
       - flex item들이 배치되는 기본 축
       
       - main start에서 시작하여 main end 방향으로 배치 (기본 값)
    
    2. **cross axis (교차 축)**
       
       - main axis에 수직인 축
       
       - cross start에서 시작하여 cross end 방향으로 배치 (기본 값)
    
    3. **Flex Container**
       
       - `display : flex;` 혹은 `display: inline-flex;` 가 설정된 부모 요소
       
       - 이 컨테이너의 1차 자식 요소들이 Flex Item이 됨
       
       - flexbox 속성 값들을 사용하여 자식 요소 Flex Item들을 배치하는 주체
    
    4. **Flex Item**
       
       - Flex Container 내부에 레이아웃 되는 항목
  
  - 속성
    
    1. `Flex Container` 지정
       
       - flex item은 기본적으로 행(주 축의 기본값인 가로 방향)으로 나열
       
       - flex item은 주 축의 시작 선에서 시작
       
       - flex item은 교차 축의 크기를 채우기 위해 늘어남
    
    2. **`flex-direction`**
       
       - flex item이 나열되는 방향을 지정
       
       - column으로 지저할 경우 주 축이 변경됨
       
       - `-revers`로 지정하면 flex item 배치의 시작 선과 끝 선이 서로 바뀜
    
    3. **<mark>`flex-wrap`</mark>**
       
       - flex iem 목록이 flex container의 한 행에 들어가지 않을 경우 다른 행에 배치할지 여부 설정
       
       > **반응형 레이아웃**
       > 
       > - 다양한 디바이스와 화면 크기에 자동으로 적응하여 콘텐츠를 최적으로 표시하는 웹 레이아웃 방식
       > 
       > - `flex-wrap`을 사용해 반응형 레이아웃 작성
       >   
       >   (`flex-grow` & `flex-basis` 활용)
    
    4. **`justify-content`**
       
       - 주 축을 따라 flex item과 주위에 공간을 분배
       
       > `fustify-items` 및 `justify-self` 속성이 없는 이유
       > 
       > - 필요 없기 때문
       > 
       > - margin auto를 통해 정렬 및 배치가 가능
    
    5. **`align-content`**
       
       - 교차 축을 따라 flex item과 주위에 공간을 분배
       
       > - flex-wrap이 wrap 또는 wrap-reverse로 설정된 여러 행에만 적용
       > 
       > - 한 줄짜리 행에는 효과 없음
    
    6. **`align-items`**
       
       - 교차 축을 따라 flex item 행을 정렬
    
    7. **`align-self`**
       
       - ****교차 축을 따라 개별 flex item을 정렬
    
    8. **`flex-grow`**
       
       - 남는 행 여백을 비율에 따라 각 flex item에 분배
         
         (아이템이 컨테이너 내에서 확장하는 비율을 지정)
       
       > flex-grow의 반대는 flex-shrink
    
    9. **`flex-basis`**
       
       - flex item의 초기 크기 값을 지정
       
       - flex-basis와 width 값을 동시에 적용한 경우 flex-basis가 우선
    
    ![image](https://github.com/user-attachments/assets/e1a2fbe8-b167-4ddf-b8f7-6282cfd5a9b3)
