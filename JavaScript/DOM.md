# DOM

[ECMAScript](#ecmascript)

[변수](#변수)

[변수 선언 키워드](#변수-선언-키워드)

[DOM](#dom)

[DOM 조작](#dom-조작)

---

## ECMAScript

: Ecma International이 정의하고 있는 표준화된 스크립트 프로그래밍 언어 명세

- 스크립트 언어가 준수해야 하는 규칙, 세부사항 등을 제공

#### ECMAScript와 JavaScript

- JavaScript는 ECMAScript 표준을 구현한 구체적인 프로그래밍 언어

- ECMAScript의 명세를 기반으로 하여 웹 브라우저나 Node.js와 같은 환경에서 실행됨

- ECMAScript는 JavaScript의 표준이며,
  
  JavaScript는 ECMAScript 표준을 따르는 구체적인 프로그래밍 언어

- ECMAScript는 언어의 핵심을 정의하고,
  
  JavaScript는 ECMAScript  표주을 따라 구현된 언어로 사용됨

---

## 변수

#### 식별자 (변수명) 작성 규칙

- 반드시 문자, 달러 `$` 또는 밑줄 `_`로 시작

- 대소문자를 구분

- 예약어 사용 불가 (`for`, `if`, `function` 등)

#### 식별자 (변수명) Naming case

- **카멜 케이스** (camelcCase) : 변수, 객체, 함수에 사용

- **파스칼 케이스** (PascalCase) : 클래스, 생성자에 사용

- **대문자 스네이크 케이스** (SNAKE_CASE) : 상수(constants)에 사용

---

## 변수 선언 키워드

#### let

- 블록 스코프를 갖는 지역 변수를 선언
  
  > ###### 블록 스코프 (block scope)
  > 
  > - if, for, 함수 등의 중괄호`{}` 내부를 가리킴
  > 
  > - 블록 스코프를 가지는 변수는 블록 바깥에서 접근 불가능

- **재할당 가능**

- 재선언 불가능

- ES6에서 추가

- 필요한 경우에만 const에서 let으로 전환하여 사용
  
  - 재할당이 필요한 경우
  
  - let을 사용하는 것은 해당 변수가 의도적으로 변경될 수 있음을 명확히 나타냄
  
  - 코드의 유연성을 확보하면서도 const의 장점을 최대한 활용할 수 있음

#### const

- 블록 스코프를 갖는 지역 변수를 선언

- **재할당 불가능**

- 재선언 불가능

- ES6에서 추가

- 선언 시 반드시 초기값 설정 필요

- 변수 기본으로 사용
  
  - 코드의 의도 명확화
  
  - 버그 예방

---

## DOM

The Document Object Model

: 웹 페이지(Document)를 구조화된 객체로 제공하여 프로그래밍 언어가 페이지 구조에 접근할 수 있는 방법을 제공

- 문서 구조, 스타일, 내용 등을 변경할 수 있도록 함

- DOM API : 다른 프로그래밍 언어가 웹 페이지에 접근 및 조작할 수 있도록 페이지 요소들을 객체 형태로 제공하며 이에 따른 메서드 또한 제공

- 문서의 요소들을 객체로 제공하여 다른 프로그래밍 언어에서 접근하고 조작할 수 있는 방법을 제공하는 API

#### 특징

- DOM에서 모든 요소, 속성, 텍스트는 하나의 객체

- 모두 document 객체의 하위 객체로 구성됨
  
  > ###### 'document' 객체
  > 
  > - 웹 페이지 객체
  > 
  > - DOM Tree의 진입점
  > 
  > - 페이지를 구성하는 모든 객체 요소를 포함

#### DOM tree

- 브라우저는 HTML 문서를 해석하여 DOM tree라는 객체 트리로 구조화

- 객체 간 상속 구조가 존재

---

## DOM 조작

#### <mark>선택</mark>

- `document.querySelector()`
  
  : 제공한 선택자와 일치하는 element 한 개 선택
  
  - 제공한 선택자를 만족하는 첫 번째 element 객체를 반환 (없다면 null 반환)

- `document.querySelctorAll()`
  
  : 제공한 선택자와 일치하는 여러 element를 선택
  
  - 제공한 선택자를 만족하는 NodeList를 반환

#### <mark>조작</mark>

- **속성 조작**
  
  - **`classList` property**
    
    : 요소의 클래스 목록을 DOMTokenList(유사 배열) 형태로 반환
    
    - `element.classList.add()` : 지정한 클래스 값을 추가
    
    - `element.classList.remove()` : 지정한 클래스 값을 제거
    
    - `element.classList.toggle()` : 클래스가 존재한다면 제거하고 false를 반환
  
  - **일반 속성 조작 메서드**
    
    - `Element.getAttribute()` : 해당 요소에 지정된 값을 반환 (조회)
    
    - `Element.setAttribute(name, value)`
      
      : 지정된 요소의 속성 값을 설정, 이미 있으면 기존 값을 갱신
    
    - `Element.removeAttribute()` : 요소에서 지정된 이름을 가진 속성 제거

- **HTML 콘텐츠 조작**
  
  - **`textContent` property**
    
    : 요소의 텍스트 콘텐츠를 표현

- **DOM 요소 조작**
  
  - **`document.createElecment(tagName)`**
    
    : 작성한 tagName의 HTML 요소를 생성하여 반환
  
  - **`Node.appendChild()`**
    
    : 한 Node를 특정 부모 Node의 자식 NodeList 중 마지막 자식으로 삽입, 추가된 Node 객체를 반환
  
  - **`Node.removeChild()`**
    
    : DOM에서 자식 Node를 제거, 제거된 Node를 반환

- **style 조작**
  
  - **`styel` property**
    
    : 해당 요소의 모든 style 속성 목록을 포함하는 속성


