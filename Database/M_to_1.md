# 다 대 일 관계

# Many to one relationships

한 테이블의 0개 이상의 레코드가 다른 테이블의 레코드 한 개와 관련된 관계

### Comment - Article

0개 이상(N)의 댓글은 1개의 게시글에 작성될 수 있다.

- 테이블 관계
  ![alt text](image-33.png)

## 댓글 모델 정의

- **ForeignKey 클래스의 인스턴스 이름은 참조하는 모델 클래스 이름의 단수형으로 작성하는 것을 권장

- 외래 키는 ForeignKey 클래스를 작성하는 위치와 관계없이 테이블의 마지막 필드로 생성됨
  
  ```py
  # articles/models.py
  class Comment(models.Model):
  article = models.ForeignKey(상대 모델 클래스, on_delete=models.CASCADE)
  ```

### Foreignkey(to, on_delete)

한 모델이 다른 모델을 참조하는 관계를 설정하는 필드 

- to
  - 참조하는 모델 class 이름
- on_delete
  - 외래 키가 참조하는 객체(1)인 클래스가 삭제 됐을 때,
  - 외래키를 가진 객체(N)를 어떻게 처리할 지를 정의하는 설정(데이터 무결성)
- on_delete의 'CASCADE'
  - 참조된 객체(부모객체)가 삭제 될 때 이를 참조하는 모든 객체도 삭제되도록 지정
  - N:1관계 표현
  - 데이터베이스에서 외래 키로 구현

## 역참조

- N:1관계에ㅓ 1에서 N을 참조하거나 조회하는 것 (1 -> N)
- 모델 간의 관계에서 관계를 정의한 모델이 아닌, 관계의 대상이 되는 모델에서 연결된 객체들에 접근하는 방식
- N은 외래 키를 가지고 있어 물리적으로 참조가 가능하지만, 1은 N에 대한 참조 방법이 존재하지 않아 별도의 역참조 키워드가 필요

![alt text](image-35.png)

### related manager

N:1  혹은 M:N관계에서 역참조 시에 사용하는 매니저

- 'objects' 매니저를 통해 QuerySet API를 사용했던 것처럼 사용
- 이름 규칙
  - **N:1관계에서 생성되는 Related manager의 이름은 "모델명_set" 형태로 자동 생성됨
    - 관계를 직접 정의하지 않은 모델에서 연결된 객체들을 조회할 수 있게 함
  - 특정 댓글의 게시글 참조 (Comment -> Article)
    - comment.article
  - 특정 게시글의 댓글 목록 참조 (Article -> Comment)
    - article.comment_ser.all()

## 댓글 create 구현

1. 사용자로부터 댓글 데이터를 입력 받기 위한 CommentForm 정의
   ![alt text](image-36.png)
2. detail view 함수에서 CommentForm을 사용하여 detail 페이지에 렌더링
   ![alt text](image-37.png)
3. 
- Comment 클래스의 외래 키 필드 article 또한 데이터 입력이 필요한 필드이기 때문에 출력 되는 것
- **하지만, 외래 키 필드 데이터는 사용자로부터 입력 받는 값이 아닌 view 함수 내에서 다른 방법으로 전달 받아 저장 돼야함.
  ![alt text](image-38.png)
4. CommentForm의 출력 필드 조정하여 외래 키 필드가 출력되지 않도록 조정
   ![alt text](image-39.png)
5. 
- 출력에서 제외된 외래키 데이터는 detail 페이지의 URL을 살펴보면
- path('<int:pk>/', views.detail, name='detail')에서 해당 게시글의 pk값이 사용되고 있다.
- 댓글의 외래 키 데이터에 필요한 정보가 바로 게시글의 pk 값
6. url 작성 및 action 값 작성
   ![alt text](image-40.png)
7. comments_create view 함수 정의
   - url로 받은 pk 인자를 게시글을 조회하는 데 사용 
     ![alt text](image-41.png)

### save(commit=False)

DB에 저장 요청을 보내지 않고 인스턴스만 반환
(Create, but don't sace the new instance)

8. save의 commit 인자를 활용해 외래 키 데이터 추가 입력
   ![alt text](image-42.png)

## 댓글 READ 구현

- detail view 함수에서 전체 댓글 데이터를 조회
  ![alt text](image-43.png)
  ![alt text](image-44.png)

## 댓글 DELETE 구현

- 댓글 삭제 url
  ![alt text](image-45.png)
- 댓글 삭제 view
  ![alt text](image-46.png)
- 댓글 삭제 버튼
  ![alt text](image-47.png)

### 데이터 무결성

- 데이터베이스에 저장된 데이터의 정확성, 일관성, 유효성을 유지하는 것
- 데이터베이스에 저장된 데이터 값의 정확성을 보장하는 것
- 중요성
  - 데이터의 신뢰성 확보
  - 시스템 안정성
  - 보안 강화

### admin site등록

Comment 모델을 admin site에 등록해 CRUD 확인
![alt text](image-48.png)

#### 대체 콘텐츠 출력

- 댓글이 없는 경우
  DTL의 'for empty' 태그 활용 
  ![alt text](image-49.png)

- 댓글 갯수 출력
  ![alt text](image-50.png)