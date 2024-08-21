# Bootstrap

[Bootstrap이란](#bootstrap이란)

[사용 가이드](#사용-가이드)

[Reset CSS](#reset-css)

[Bootstrap 활용](#bootstrap-활용)

[Semantic Web](#semantic-web)

---

## Bootstrap이란

CSS 프론트엔드 프레임워크 (Toolkit)

- 미리 만들어진 다양한 디자인 요소들을 제공하여 웹 사이트 빠르고 쉽게 개발 가능

- 사용해보기
  
  1. Bootstrap 공식 문서 접속 https://getbootstrap.com/
  
  2. Docs -> Introduction -> Quick start
  
  3. "Include Brootstrap's CSS and JS" 코드 확인 및 가져오기 (head와 body에 bootstrap CDN이 포함된 코드 블록)

- **<mark>CDN</mark>** (Content Delivery Network)
  
  지리적 제약 없이 빠르고 안전하게 콘텐츠를 전송할 수 있는 전송 기술
  
  - 서버와 사용자 사이의 물리적인 거리를 줄여 콘텐츠 로딩에 소요되는 시간을 최소화 (웹 페이지 로드 속도를 높임)
  
  - 지리적으로 사용자와 가까운 CDN 서버에 콘텐츠를 저장해서 사용자에게 전달
  1. Bootstrap 홈페이지 - Download - "Compiled CSS and JS" 다운로드
  
  2. CDN을 통해 가져오는 bootstrap css와 js 파일을 확인
  
  3. bootstrap.css, bootstrap.js 파일 참고
  
  > 온라인 CDN 서버에 업로드 된 css 및 js 파일을 불러와서 사용하는 것

---

## 사용 가이드

![image](https://github.com/user-attachments/assets/95bb04cd-e229-4594-a73a-b2649340a7c5)

- Bootstrap에서 클래스 이름으로 Spacing을 표현하는 방법
  
  ![image](https://github.com/user-attachments/assets/6881ea8c-6e77-4f82-ba93-46552e52984a)

- Bootstrap에는 특정한 규칙이 있는 클래스 이름으로 스타일 및 레이아웃이 미리 작성되어 있음

---

## Reset CSS

모든 HTML 요소 스타일을 일관된 기준으로 재설정하는 간결하고 압축된 규칙 세트

- HTML Element, Table, List 등의 요소들에 일관성 있게 스타일을 적용 시키는 기본 단계

- **사용 배경**
  
  - 모든 브라우저는 각자의 'user agent stylesheet'를 가지고 있음
  
  - 문제는 이 설정이 브라우저마다 상이하다는 것
  
  - 모든 브라우저는 웹사이트를 동일하게 보이게 만들어야 하는 개발자에겐 매우 골치 아픈 일
  
  > 모두 똑같은 스타일 상태로 만들고 스타일 개발을 시작하자!

- **Normalize CSS**
  
  - Reset CSS 방법 중 대표적인 방법
  
  - 웹 표준 기준으로 브라우저 중 하나가 불일치 한다면 차이가 있는 브라우저를 수정하는 방법
  
  - bootstrap은 bootstrap-reboot.css라는 파일명으로 normalize.css 자체적 커스텀

---

## Bootstrap 활용

- **Typography** : 제목, 본문 텍스트, 목록 등
  
  - Display headings : 기존 Heading보다 더 눈에 띄는 제목이 필요할 경우 (더 크고 약간 다른 스타일)
  
  - Inline text elements : HTML inline 요소에 대한 스타일
  
  - Lists : HTML list 요소에 대한 스타일

- **Colors** : Text, Border, Background 다양한 요소에 사용하는 Bootstrap의 색상 키워드
  
  - Text colors, Background colors

- **Component** : 버튼, 네비게이션 바, 카드, 폼, 드롭다운 등 Bootstrap의  UI 관련 요소
  
  - Alerts, Badges, Buttons, Cards, Navbar 등
  
  - 이점 : 일관된 디자인을 제공하여 웹 사이트의 구성 요소를 구축하는 데 유용

---

## Semantic Web

웹 데이터를 의미론적으로 구조화된 형태로 표현하는 방식

- **HTML Semantic Element** : 기본적인 모양과 기능 이외에 의미를 가지는 HTML 요소
  
  - 검색엔진 및 개발자가 웹 페이지 콘텐츠를 이해하기 쉽도록
  
  - header, nav, main, article, section, aside, footer
  
  - div랑 완전 같은 역할이지만 이름만 다른 거임

- **CSS 방법론** : CSS를 효율적이고 유지 보수가 용이하게 작성하기 위한 일련의 가이드라인

- **<mark>OOCSS</mark>** (Object Oriented CSS) : 객체 지향적 접근법을 적용하여 CSS를 구성하는 방법론
  
  - 기본 원칙
    
    1. 구조와 스킨을 분리
       
       - 재사용 가능성을 높임
       
       - 모든 버튼의 공통 구조를 정의 + 각각의 스킨(배경색과 폰트 색상)을 정의
    
    2. 컨테이너와 콘텐츠를 분리
       
       - 객체에 직접 적용하는 대신 객체를 둘러싸는 컨테이너에 스타일을 저굥
       
       - 스타일을 정의할 때 위치에 의존적인 스타일을 사용하지 않도록 함
       
       - 콘텐츠를 다른 컨테이너로 이동 혹은 재배치할 때 스타일이 깨는 것을 방지


