# SQL

[Database](#database)

[Relational Database](#relational-database)

- [RDBMS](#rdbms)

[SQL](#sql)

[Single Table Queries](#single-table-queries)

- [Querying data](#querying-data)

- [Sorting data](#sorting-data)

- [Filtering data](#filtering-data)

- [Grouping data](#grouping-data)

[Managing Tables](#managing-tables)

- [Create a table](#create-a-table)

- [Modifying table fields](#modifying-table-fields)

- [Delete a table](#delete-a-table)

[Modifying Data](#modifying-date)

- [Insert data](#insert-data)

- [Update data](#update-data)

- [Delete data](#delete-data)

[Multi table queries](#multi-table-queries)

- [Join](#join)

- [Joining tables](#joining-tables)

---

## Database

: 체계적인 데이터 모음

#### 데이터

 : 저장이나 처리에 효율적인 형태로 변환된 정보

#### 데이터베이스 역할

: 데이터를 (구조적) 저장하고 조작 (CRUD)

---

## Realtional Database

: 데이터 간에 관계가 있는 데이터 항목들의 모음

- 테이블, 행, 열의 정보를 구조화하는 방식

- 서로 관련된 데이터 포인터를 저장하고 이에 대한 액세스를 제공

- 관계로 인해 두 테이블을 사용하여 데이터를 다양한 형식으로 조회 가능

#### 관계

: 여러 테이블 간의 (논리적) 연결

- **기본 키 (Primary Key)**
  
  : 각 데이터에 고유한 식별 값을 부여, 레코드의 식별자로 활용

- **외래 키 (Foreign Key)**
  
  : 주문 정보에 고객의 고유한 식별 값을 저장, 서로 다른 텡블 간의 관계를 만드는 데 사용

#### 키워드

- **Table (== Relation)** : 데이터를 기록하는 곳

- **Field (== Column, Attribute)** : 각 필드에는 고유한 데이터 형식(타입)이 지정됨

- **Record (== Row, Tuple)** : 각 레코드에는 구체적인 데이터 값이 저장됨

- **Database (== Schema)** : 테이블의 집합

---

# RDBMS

#### DBMS (Database Management System)

: 데이터베이스를 관리하는 소프트웨어 프로그램

- 데이터 저장 및 관리를 용이하게 하는 시스템

- 데이터베이스와 사용자 간의 인터페이스 역할

- 사용자가 데이터 구성, 업데이트, 모니터링, 백업, 복구 등을 할 수 있도록 도움

#### RDBMS (Relational Database Management System)

: 관계형 데이터베이스를 관리하는 소프트웨어 프로그램

- **SQLite**
  
  : 경량의 오픈 소스 데이터베이스 관리 시스템
  
    컴퓨터나 모바일 기기에 내장되어 간단하고 효율적인 데이터 저장 및 관리를 제공

- MySQL

- PostgreSQL

- Oracle Database

---

## SQL

: Structure Query Language

  데이터베이스에 정보를 저장하고 처리하기 위한 프로그래밍 언어

- 관계형 데이터베이스와의 대화를 위해 사용하는 프로그래밍 언어

- **SQL Statements**
  
  : SQL을 구성하는 가장 기본적인 코드 블록
  
  ```sql
  SELECT column_name FROM table_name;
  ```
  
  - SQL 키워드는 대소문자를 구분하지 않음 (하지만 대문자로 작성하는 것을 권장)
  
  - 각 SAL Statements의 끝에는 세미콜론`;`이 필요 (명령어의 마침표)
  
  - 해당 예시 코드는 SELECT Statement라 부름
  
  - 이 Statement는 `SELECT`, `FROM` 2개의 keyword로 구성 됨
  
  - 수행 목적에 따른 SQL Statements 4가지 유형
    
    ![image](https://github.com/user-attachments/assets/42e888da-c873-451a-ac99-043ff10d1174)

---

## Single Table Queries

- **<mark>SELECT statement 실행 순서</mark>**
  
  ![image](https://github.com/user-attachments/assets/7dba52dd-ab85-476e-857d-e1bf157729f4)
  
  1. 테이블에서 (FROM)
  
  2. 특정 조건에 맞추어 (WHERE)
  
  3. 그룹화 하고 (GROUP BY)
  
  4. 만약 그룹 중에서 조건이 있다면 맞추고 (HAVING)
  
  5. 조회하여 (SELECT)
  
  6. 정렬하고 (ORDER BY)
  
  7. 특정 위치의 값을 가져옴 (LIMIT)

---

## Querying data

- **SELECT**
  
  : 테이블에서 데이터를 조회 및 반환
  
  ```sql
  SELECT # 데이터를 선택하려는 필드를 하나 이상 지정
    select_list
  FROM # 데이터를 선택하려는 테이블의 이름을 지정
    table_name;
  ```
  
  - 두 가지 이상의 필드 선택은 `,`로 이어서 쓰기
  
  - `*`(aterisk)를 사용하여 모든 필드 선택
  
  - `필드명 AS '이름'`으로 하면 출력명 변경 가능
  
  - `Milliseconds / 60000 AS '재생 시간(분)'`으로 단위 값, 출력명 변경 가능

---

## Sorting data

- **ORDER BY**
  
  : 조회 결과의 레코드를 정렬
  
  ```sql
  # SELECT statement 이후
  ORDER BY
    column1 [ASC|DESC];
  ```
  
  - 기본이나 `ASC`는 오름차순, `DESC`가 붙으면 내림차순으로 조회
  
  - 두 가지 이상의 기준으로 하면 앞선 정렬이 같은 애들을 정렬함
  
  - NULL 값이 존재할 경우 오름차순 정렬 시 결과에 NULL이 먼저 출력

---

## Filtering data

#### Clause

- **DISTINCT**
  
  : 조회 결과에서 중복된 레코드를 제거
  
  ```sql
  SELECT DISTINCT
    select_list
  FROM
    table_name;
  ```

- <mark>**WHERE**</mark>
  
  : 조회 시 특정 검색 조건을 지정
  
  ```sql
  # SELECT statement 이후
  WHERE
    search_conditiona;
    # 비교연산자 및 논리연산자(AND, OR, NOT, ㅑ BETWEEN 등) 구문 사용
  ```
  
  - `LastNmae LIKE '%son';`으로 'son'으로 끝나는 데이터 조회
  - `FirstNmae LIKE '___a';`으로 4자리면서 'a'로 끝나는 데이터 조회

- **LIMIT**
  
  : 조회하는 레코드 수를 제한
  
  ```sql
  # SELECT statement 이후
  LIMIT [offset,] row_count; # 숫자
  ```
  
  - `row_count`는 조회하는 최대 레코드 수를 지정

#### Operator

- **Comparison (비교 연산자)** : `=`, `>=`, `<=`, `IS`, `LIKE`, `IN`, `BETWEEN`, `AND`

- **Logical (논리 연산자)** : `AND(&&)`, `OR(||)`, `NOT(!)`

- **IN** : 값이 특정 목록 안에 있는지 확인

- **LIKE** : 값이 특정 패턴에 일치하는지 확인 (wildcards와 함께 사용)
  
  > **wildcards**
  > 
  > - `%` : 0개 이상의 문자열과 일치 하는지 확인
  > 
  > - `_` : 단일 문자와 일치하는지 확인

---

## Grouping data

- **GROUP BY**
  
  : 레코드를 그룹화하여 요약본 생성 ('집계 함수'와 함께 사용)
  
  ```sql
  SELECT
    c1, c2, ..., cn, aggregate_function(ci)
  # From
  #   table_name
  GROUP BY
    c1, c2, ..., cn;
  ```
  
  - **Aggregation Functions (집계 함수)**
    
    : 값에 대한 계산을 수행하고 단일한 값을 반환하는 함수
    
      `SUM`, `AVG`, `MAX`, `MIN`, `COUNT`
  
  - `COUNT` 함수로 각 그룹에 대한 집계된 값을 계산
  
  - `AVG(Bytes) AS avg0fBytes`는 각 그룹에 대한 Bytes의 평균 값을 내림차순 조회
  
  - **HAVING**
    
    : 집계 항목에 대한 세부 조건을 지정
    
      주로 GROUP BY와 함께 사용되며 GROUP BY가 없다면 WEHRE처럼 동장
    
    ```sql
    SELECT
      Composer,
      AVG(Milliseconds / 60000) AS avg0fMinute
    FROM
      tracks
    GROUP BY
      Composer
    HAVING
      avg0fMinute < 10;
    ```

---

## Managin Tables

---

## Create a table

#### CREATE TABLE

: 테이블 생성

```sql
CREATE TABLE table_name (
  column_1 data_type constrainsts,
  column_2 data_type constraints,
  ...,
);
```

- **PRAGMA**
  
  : 테이블 schema(구조) 확인
  
  ```sql
  PRAGMA table_info('examples');
  ```
  
  - **cid**
    
    : Column ID를 의미하며 각 컬럼의 고유한 식별자를 나타내는 정수 값
    
      직접 사용않고 PRAGMA 명령과 같은 메타데이터 조회에서 출력 값으로 활용

#### SQLite 데이터 타입

- `NULL` : 아무런 값도 포함하지 않음을 나타냄

- `TEXT` : 문자열

- `INTEGER `: 정수

- `BLOB `: 이미지, 동영상, 문서 등의 바이너리 데이터

- `REAL `: 부동 소수점

#### Constraints (제약 조건)

: 테이블의 필드에 적용되는 규칙 또는 제한 사항

  데이터의 무결성을 유지하고 데이터베이스의 일관성을 보장

- `PRIMARY KEY` : 해당 필드를 기본 키로 지정 (INTEGER 타입에만 적용)

- `NOT NULL` : 해당 필드에 NULL 값을 허용하지 않도록 지정

- `FOREIGN KEY` : 다른 테이블과의 외래 키 관계를 정의

#### AUTOINCREAMENT keyword

: 자동으로 고유한 정수 값을 생성하고 할당하는 필드 속성

- 필드의 자동 증가를 나타내는 특수한 키워드

- 주로 primary key 필드에 적용

- `INTEGER PRIMARY KEY AUTOINCREAMENT`가 작성된 필드는 항상 새로운 레코드에 대해 이전 최대 값보다 큰 값을 할당

- 삭제된 값은 무시되며 재사용할 수 없게 됨

---

## Modifying table fields

#### ALTER TABLE

: 테이블 및 필드 조작

- ALTER TABLE **ADD COLUMN**
  
  : 필드 추가
  
  ```sql
  ALTER TABLE
    table_name
  ADD COLUMN
    column_definition;
  ```
  
  - 추가하고자 하는 필드에 NOT NULL 제약조건이 있을 경우 NULL이 아닌 기본 값 설정 필요 `NOT NULL DEFAULT 'default value';`
  
  - SQLite는 단일 문을 사용하여 한번에 여러 필드를 추가할 수 없음

- ALTER TABLE **RENAME COLUMN**
  
  : 필드 이름 변경
  
  ```sql
  ALTER TABLE
    table_name
  RENAME COLUMN
    current_name TO new_name
  ```

- ALTER TABLE **CROP COLUMN**
  
  : 필드 삭제
  
  ```sql
  ALTER TABLE
    table_name
  DROP COLUMN
    column_name
  ```

- ALTER TABLE **RENAME TO**
  
  : 테이블 이름 변경
  
  ```sql
  ALTER TABLE
    table_name
  RENAME TO
    new_table_name
  ```

---

## Delete a table

#### DROP TABLE

: 테이블 삭제

```sql
DROP TABLE table_name;
```

---

## Modifying Data

---

## Insert data

#### INSEAR

: 테이블 레코드 삽입

```sql
INSERT INTO table_name (c1, c2, ...) # 괄호 안에 필드 목록
VALUES (v1, v2, ...); # 괄호 안에 필드에 삽입할 값 목록 작
```

- 여러 개 한 줄씩 해서 한 번에 추가 가능

- `DATE()` 함수를 사용해 createdAt에 다음과 같은 데이터 추가 입력

---

## Update data

#### UPDATE

: 테이블 레코드 수정

```sql
UPDATE table_name
SET column_name = expression,
[WHERE
  condition];
```

- `WHERE`절을 작성하지 않으면 모든 레코드를 수정

---

## Delete data

#### DELETE

: 테이블 레코드 삭제

```sql
DELETE FROM table_name
[WHERE
  condition];
```

- `WHERE`절을 작성하지 않으면 모든 레코드를 삭제

- `WHERE`절 안에 SELECT, ORDER BY, LIMIT 넣어서 복잡하게 선택할 수도 있음

---

## Multi table Queries

---

## Join

: 관계, 여러 테이블 간의 (논리적) 연결

- 테이블을 분리하면 데이터 관리는 용이해질 수 있으나 출력시에는 문제가 있음

- 테이블 한 개 만을 출력할 수 밖에 없어 다른 테이블과 결합하여 출력하는 것이 필요

---

## Joining tables

#### JOIN

: 둘 이상의 테이블에서 데이터를 검색하는 방법

- **INNER JOIN**
  
  : 두 테이블에서 값이 일치하는 레코드에 대해서만 결과를 반환
  
  ```sql
  # SELECT statemant 이후
  INNER JOIN table_b
    ON table_b.fk = table_a.pk;
  ```

- **LEFT JOIN**
  
  : 오른쪽 테이블의 일치하는 레코드와 함께 왼쪽 테이블의 모든 레코드 반환
  
  ```sql
  # SELECT statemant 이후
  LEFT JOIN table_b
    ON table_b.fk = table_a.pk;
  ```
  
  - 왼쪽 테이블의 모든 레코드를 표기
  
  - 오른쪽 테이블과 매칭되는 레코드가 없으면 NULL을 표시
