# Data Types

[Numeric Type](#numeric-type)

- int, float

[Sequence Types](#sequence-types)

- str, list, tuple, range

[Non-sequence Types](#non-sequence-types)

- dict, set

[Other Types](#other-types)

- None, boolean, collection

[Type Conversion](#type-conversion)

- 암시적, 명시적 형변환

---

## Numeric Type

- **int** : 정수 자료형
  
  - 2진수 (binary) : `0b숫자`
  
  - 8진수 (octal) : `0o숫자`
  
  - 16진수 (hexadecimal) : `0x숫자`

- **float** : 실수 자료형
  
  - 소수점 있는 자료
  
  - 유한 정밀도 : 무한대 숫자는 가장 가까운 값
  
  - Floating point rounding error (부동소수점 에러) 해결책 : decimal 모듈 사용
  
  - 지수 표현 방식 : `3.14 = 314e-2`

- **complex** : 복소수

---

## Sequence Types

- **특징**
  
  - 순서 (Sequence) : 순서는 있는데, 정렬은 아님
  
  - 인덱싱 (Indexing) : 인덱스 (index)를 사용하여 특정 위치의 값 선택이나 수정 가능
    
    - 0부터 순서대로
    
    - 음수 인덱스 존재 (뒤부터 -1)
  
  - 슬라이싱 (Slicing) : 인덱스 범위를 조절해 부분적인 값 추출 가능
    
    - 값 사이 기준으로 자르기 : `변수명[2:4]`
    
    - 처음과 끝 생략 가능 : `변수명[:3]`
    
    - 0부터 4까지 2개씩 자르기 : `변수명[0:5:2]`
    
    - 반대로 출력 : `변수명[::-1]`
  
  - 길이 (Length) : `len()` 함수를 사용하여 저장된 값의 개수(길이) 구할 수 있음
  
  - 반복 (Iteration) : 반복문을 사용하여 저장된 값들을 반복적으로 처리 가능

- **str** : 문자열
  
  - 숫자가 있는 변경 불가능한 시퀀스 자료형
  
  - 단일 문자나 여러 문자의 조합
  
  - 작은 따옴표, 큰 따옴표 상관 없음
  
  - Escape sequence
    
    - `\n` 줄 바꿈
    
    - `\t` 탭
    
    - `\\` 백슬래시
    
    - `\'` 작은 따옴표
    
    - `\"` 큰 따옴표
  
  - <mark>f-string</mark>
    
    - <mark>문자열 `f 또는 F` 접두어를 붙이고 표현식을 `{expression}`으로 작성</mark>
    
    - 문자열에 파이썬 표현식의 값을 삽입

- **list** : 변경 가능한 시퀀스 자료형
  
  - 0개 이상의 객체를 포함하여 데이터 목록을 저장
  
  - 대괄호 []로 표기
  
  - 어떤 자료형도 저장 가능
  
  - 중첩된 리스트에서 객체 뽑기: `my_list[3][1]`

- **tuple** : 변경 불가능한 시퀀스 자료형
  
  - list 표현과 같으나 소괄호 ()로 표기
  
  - 개발자가 직접 사용하기 보다 '파이썬 내부 동작'에서 주로 사용

> 요소 하나일 때 `(1,)` 이렇게 해서 int가 되지 않게 하기

- **range** : 연속된 정수 시퀀스를 생성하는 변경 불가능한 자료형
  
  - 함수형 `range(시작 값, 끝 값, 증가 값)`
  
  - `range(n)` 0부터 n-1까지의 숫자 시퀀스
  
  - `range(n,m)` n부터 m-1까지의 숫자 시퀀스

> 주로 반복문과 함께 활용

---

## Non-sequence Types

- **dict** : <mark>key - value 쌍으로 이루어진 순서와 중복이 없는 변경 가능한 자료형</mark>
  
  - key는 변경 불가능한 자료형만, value는 모든 자료형 가능
  
  - 중괄호 {}로 표기
  
  - 딕셔너리는 키에 접근해 값을 얻어냄

- **set** : 순서와 중복이 없는 변경 가능한 집합 자료형
  
  - 수학에서의 집합과 동일한 연산 처리 가능
    
    - 합집합 `|`
    
    - 차집합 `-`
    
    - 교집합 `&`
  
  - 중괄호 {}로 표기

> `a = {}` 빈 처리하면 **dict**, 빈 set하려면 `set()`라고 표현

---

## Other Types

- **None** : 파이썬에서 '값이 없음'을 표현하는 자료형
  
  - 맨 앞 N 무조건 대문자로 작성

- **boolean** : 참(`True`)과 거짓(`False`)을 표현하는 자료형
  
  - 비교 / 논리 연산의 평가 결과로 사용
  
  - 주로 조건 / 반복문과 함께 사용

- **Collection** : 여러 개의 항목 또는 요소를 담는 자료 구조

---

## Type Conversion

- **암시적 형변환** : 파이썬이 자동으로 수행하는 형변환
  
  ```python
  True = 1
  False = 0
  ```

- **명시적 형변환** : 프로그래머가 직접 지정하는 형변환
  
  - `str -> int` : 형식에 맞는 숫자만 가능
  
  - `int -> str` : 모두 가능
