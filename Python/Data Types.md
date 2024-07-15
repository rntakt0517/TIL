# Data Types

    [Numeric Type](#numeric-type)

    [Sequence Types](#sequence-types)

    [Non-sequence Types](#non-sequence-types)

    [Boolean, None, Functions](#boolean-none-functions)

---

## Numeric Type

- **int**: 정수 자료형
  
  - 2진수 (binary): 0b
  
  - 8진수 (octal): 0o
  
  - 16진수 (hexadecimal): 0x

- **float**: 실수 자료형
  
  - 소수점 있는 자료
  
  - 유한 정밀도: 무한대 숫자는 가장 가까운 값
  
  - Floating point rounding error (부동소수점 에러) 해결책: decimal 모듈 사용
  
  - 지수 표현 방식: `3.14 = 314e-2`

- complex

---

## Sequence Types

- **특징**
  
  - 순서 (Sequence): 순서는 있는데, 정렬은 없음
  
  - 인덱싱 (Indexing): 인덱스 (index)를 사용하여 특정 위치의 값 선택이나 수정 가능
    
    - 0부터 순서대로
    
    - 음수 인덱스 존재 (뒤부터 -1)
  
  - 슬라이싱 (Slicing): 인덱스 범위를 조절해 부분적인 값 추출 가능
    
    - 값 사이 기준으로 자르기: `변수명[2:4]`
    
    - 처음과 끝 생략 가능: `변수명[:3]`
    
    - 0부터 4까지 2개씩 자르기: `변수명[0:5:2]`
    
    - 반대로 출력: `변수명[::-1]`
  
  - 길이 (Length): `len()` 함수를 사용하여 저장된 값의 개수(길이) 구할 수 있음
  
  - 반복 (Iteration): 반복문을 사용하여 저장된 값들을 반복적으로 처리 가능

- **str**
  
  - 숫자가 있는 변경 불가능한 시퀀스 자료형
  
  - 단일 문자나 여러 문자의 조합
  
  - 작은 따옴표, 큰 따옴표 상관 없음
  
  - Escape sequence
    
    - `\n` 줄 바꿈
    
    - `\t` 탭
    
    - `\\` 백슬래시
    
    - `\'` 작은 따옴표
    
    - `\"` 큰 따옴표
  
  - <mark>**f-string</mark>**
    
    - 문자열 f 또는 F 접두어를 붙이고 표현식을 {expression}으로 작성
    
    - 문자열에 파이썬 표현식의 값을 삽입

- list

- tuple

- range

---

## Non-sequence Types

- **set**

- **dict**

---

## Boolean, None, Functions
