# Responsive Web

[Bootstrap Grid system](#bootstrap-grid-system)

[Grid system Breakpoints](#grid-system-breakpoints)

[CSS Layout 종합 정리](#css-layout-종합-정리)

[UX & UI](#ux--ui)

---

## Bootstrap Grid system

웹 페이지의 레이아웃을 조정하는 데 사용되는 **12개의 컬럼**으로 구성된 시스템

> **왜 12개일까?**
> 
> 1. 약수가 많음 (1, 2, 3, 4, 6, 12)
> 
> 2. 적당히 큰 수

- **Grid system 목적**
  
  - 반응형 디자인을 지원해 웹 페이지를 모바일, 태블릿, 데스크탑 등 다양한 기기에서 적절하게 표시할 수 있도록 도움
  
  - **<mark>반응형 웹 디자인 (Responsive Web Design)</mark>**
    
    디바이스 종류나 화면 크기에 상관없이, 어디서든 일관된 레이아웃 및 사용자 경험을 제공하는 디자인 기술
    
    ![image](https://github.com/user-attachments/assets/0b50a9d9-3457-486b-8eb3-821c6495ee7c)

- **Grid system 기본 요소**
  
  1. `Container` : Column들을 담고 있는 공간
  
  2. `Column` : 실제 컨텐츠를 포함하는 부분
  
  3. `Gutter` : 컬럼과 컬럼 사이의 여백 영역
  
  4. 1개의 `row` 안에 12개ㅢ column 영역이 구성

- **Grid system 실습**
  
  - **기본** : `col-n`
    
    ![image](https://github.com/user-attachments/assets/1c10e8ad-2825-4d59-8b28-773b9e2fd3f8)
  
  - **중첩 (Nesting)** : `row` 안에 `col-n`
    
    ![image](https://github.com/user-attachments/assets/a56f0b5e-13ff-46eb-b8c5-0212b65ee3ae)
  
  - **상쇄 (Offset)** : `col-n offset-n`
    
    ![image](https://github.com/user-attachments/assets/fb8925b1-c7dc-498e-ab61-8d98ee6f733f)
  
  - **Gutters** : `row g(x or y)-n` 안에 `col-n`
    
    Grid system에서 column 사이에 여백 영역 생성
    
    (컴터가 알아서 x축 : padding, y축 : margin)
    
    ![image](https://github.com/user-attachments/assets/89c98464-5bce-4913-9f07-9c2483c1729c)
  
  > - Grid cards : `row-cols-1 ros-cols-sm-3 row-cols-md-2 g-4`
  >   
  >   ![image](https://github.com/user-attachments/assets/e362b5d8-cf05-458b-ac73-2d02c6fa7219)

---

## Grid system Breakpoints

웹 페이지를 다양한 화면 크기에서 적절하게 배치하기 위한 분기점

- 화면 너비에 따라 **6개**의 분기점 제공 (xs, s, md, lg, xl, xxl)
  
  ![image](https://github.com/user-attachments/assets/7f3f4075-7e46-4376-a4d1-7f3b7ac1d480)
  
  - 각 breakpoints마다 설정된 최대 너비 값 **<mark>이상으로</mark>** 화면이 커지면 grid system 동작이 변경됨

- Breakpoints 실습 : `col-12 col-sm-6 col-md-2 col-lg-3 col-xl-4 box`
  
  ![image](https://github.com/user-attachments/assets/8ecc70cb-d6e6-445c-a695-c64b4d53a10b)

---

## CSS Layout 종합 정리

1. **Grid System** : 12개의 컬럼에 어떤 레이아웃 기술이 사용됐는지 생각해보기

2. **Flexbox** : 각 박스마다 어떤 레이아웃 기술이 사용됐는지 생각해보기

3. **Position** : header와 footer, nav에 어떤 레이아웃 기술이 사용됐는지 생각해보기
- CSS Layout 특징
  
  - CSS 레이아웃 기술들은 각각 고유한 특성과 장단점을 가지고 있음
  
  - 이들은 상호 보완적이며, 특정 상황에 따라 적합한 도구가 달라짐
  
  - 최적의 기술을 효과적으로 선택 및 활용하기 위해서는 다양한 실제 개발 경험이 필수

---

## UX & UI

- UX (User Experience)
  
  제품이나 서비스를 사용하는 사람들이 느끼는 전체적인 경험과 만족도를 개선하고 최적화하기 위한 디자인과 개발 분야
  
  - ex) 백화점 1층 향기, 러쉬 향기, 음악 검색 기능이 적절하고 정확하게 작동하는 것
  
  - 사람들의 마음과 생각을 이해하고 정리해서 제품에 녹여내는 과정
  
  - 유저 리서치, 데이터 설계 및 정제, 유저 시나리오, 프로토타입 설계
  
  - 기획자의 역할

- UI (User Interface)
  
  서비스와 사용자 간 상호작용을 가능하게 하는 디자인 요소들을 개발하고 구현하는 분야
  
  - ex) 리모컨, ATM, 웹 사이트
  
  - 예쁜 디자인보다는 사용자가 더 쉽고 편리하게 사용할 수 있도록 고려
  
  - 이를 위해서는 디자인 시스템, 중간 산출물, 프로토타입 등이 필요
  
  - 디자이너의 역할
