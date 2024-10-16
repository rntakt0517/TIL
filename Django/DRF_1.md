# DRF_1

[REST API](#rest-api)

[DRF with Single Model](#drf-with-single-model)

[CRUD with ModelSerializer](#crud-with-modelserializer)

---

## REST API

#### API (Application Programming Interface)

두 소프트웨어가 서로 통신할 수 있게 하는 메커니즘

- **역할** : 복잡한 코드를 추상화하여 대신 사용할 수 있는 몇 가지 더 쉬운 구문을 제공

- **Web API** : 웹 서버 또는 웹 브라우저를 위한 API

#### REST API

REST라는 설계 디자인 약속을 지켜 구현한 API

- **REST** (Representational State Transfer) : API Server를 개발하기 위한 일종의 소프트웨어 설계 방법론 (규칙 X)

- **RESTful API** : REST 원리를 따르는 시스템을 RESTful 하다고 부름

- **REST에서 자원을 정의하고 주소를 지정하는 방법**
  
  1. 자원의 **<mark>식별</mark>** : URI
  
  2. 자원의 **<mark>행위</mark>** : HTTP Methods
  
  3. 자원의 **<mark>표현</mark>** : JSON 데이터 (궁극적으로 표현되는 데이터 결과물)

#### 자원의 식별

- **URI** (Uniform Resource Identifier, 통합 자원 식별자)
  
  인터넷에서 리소스(자원)를 식별하는 문자열

- **URL** (Uniform Resource Locator, 통합 자원 위치)
  
  웹에서 주어진 리소스의 주소 (네트워크 상에 리소스가 어디 있는지를 알려주는 약속)
  
  - 가장 일반적인 URI
  
  - ![image](https://github.com/user-attachments/assets/8c143368-1578-401f-92c5-418745c1a8cf)
    
    1. **Schema** (or Protocol)
       
       브라우저가 리소스를 요청하는 데 사용해야 하는 규약
       
       - 기본적으로 웹은 http(s)를 요구
    
    2- **Domain Name**
    
       요청 중인 웹 서버를 나타냄 
    
    - 직접 IP 주소를 사용하는 것도 가능하지만
      
      사람이 외우기 어렵기 때문에 주로 Domain Name으로 사용
    
    3- **Port**
    
       웹 서버의 리소스에 접근하는데 사용되는 기술적인 문(Gate)
    
    - 표준 포트 (HTTP - 80, HTTPS - 443)만 작성 시 생략 가능
    
    4- **Path**
    
       웹 서버의 리소스 경로
    
    - 초기에는 실제 파일이 위치한 물리적 위치를 나타냈지만,
      
      오늘날은 실제 위치가 아닌 추상화된 형태의 구조를 표현
    
    5- **Parameters**
    
       웹 서버에 제공하는 추가적인 데이터
    
    - `&`기호로 구분되는 key-value 쌍 목록
    
    6- **Anchor**
    
       일종의 "북마크"를 나타내며 브라우저에 해당 지점에 있는 콘텐츠를 표시
    
    - `#` 이후 부분은 서버에 전송되지 않음

#### 자원의 행위

- HTTP Request Methods (HTTP verbs)
  
  리소스에 대한 행위(수행하고자 하는 동작)를 정의
  
  - `GET` : 서버에 리소스의 표현을 요청 (GET을 사용하는 요청은 데이터만 검색해야 함)
  
  - `POST` : 데이터를 지정된 리소스에 제출, 서버의 상태를 변경
  
  - `PUT` : 요청한 주소의 리소스를 수정
  
  - `DELETE` : 지정된 리소스를 삭제

- HTTP response status codes
  
  특정 HTTP 요청이 성공적으로 완료 되었는지 여부를 나타냄
  
  - Informational responses (100-199)
  
  - Successful responses (200-299)
  
  - Redirection messages (300-399)
  
  - Clinet error responses (400-499)
  
  - Server error responses (500-599)

#### 자원의 표현

- 응답 데이터 타입의 변화
  
  1. 페이지(html)만을 응답하는 서버
  
  2. 이제는 JSON 데이터를 응답하는 REST API 서버로의 변환
  
  3. Django는 더 이상 Template 부분에 대한 역할을 담당하지 않게 되며, Front-end와 Back-end가 분리되어 구성됨
  
  4. 이제부터 Django를 사용해 RESTful API 서버를 구축할 것

#### json 데이터 응답

1. 사전 준비
   
   - 사전 제공된 `99-json-response-practice` 기반 시작
   
   - 가상 환경 생성, 활성화 및 패키지 설치
   
   - migrate 진행
     
     `python manage.py migrate`
   
   - 준비된 fixtures 파일을 load하여 실습용 초기 데이터 입력
     
     `python manage.py loaddate articles.json`
   
   - `http://127.0.0.1:8000/api/v1/articles/` 요청 후 응답 확인

2. python으로 json 데이터 처리 하기
   
   - 준비된 python-request-sample.py 확인
     
     ```python
     # python-request-sample.py
     import requests
     from pprint import pprint
     response = requests.get('주소')
     # json을 python 타입으로 변환
     result = response.json()
     print(type(result))
     pprint(result)
     pprint(result[0])
     pprint(result[0].get('title'))
     ```

---

## DRF with Single Model

#### DRF (Django REST framework)

Django에서 Restful API 서버를 쉽게 구축할 수 있도록 도와주는 오픈소스 라이브러리

- 프로젝트 준비 : 위에 json 데이터 응답 사전 준비와 동일

- Postman
  
  API 개발 및 테스트를 위한 서비스
  
  - 요청 데이터 구성, 응답 확인, 환경 설정, 자동화 테스트 등 다양한 기능을 제공
  
  - Workspaces - My workspace
  
  - 화면 구성 안내
    
    ![image](https://github.com/user-attachments/assets/a951ce6d-84bf-436f-862a-a54149afe589)

#### Serializer

Serialization을 진행하여 Serialized data를 반환해주는 클래스

- Serialization (직렬화)
  
  어떠한 언어나 환경에서도 나중에 다시 쉽게 사용할 수 있는 포맷으로 변환하는 과정

- ModelSerializer
  
  Django 모델과 연결된 Serializer 클래스
  
  - 일반 Serializer와 달리 사용자 입력 데이터를 받아 자동으로 모델 필드에 맞추어 Serialization을 진행

---

## CRUD with ModelSerializer

- URL과 HTTP requests methods 설계
  
  ![image](https://github.com/user-attachments/assets/976f7b10-95bb-4d7f-98b0-81a2170a2e72)

#### Get method - <mark>조회</mark>

- GET - **List**
  
  1. 게시글 데이터 목록을 제공하는 ArticleListSerializer 정의
     
     ```python
     # articles/serializers.py
     from rest_framework import serializers
     from .models import Article
     class ArticleListSerializer(serializers.ModelSerializer):
         class Meta:
             model = Article
             fields = ('id', 'title', 'content',)
     ```
  
  2. url 및 view 함수 작성
     
     ```python
     # articles/urls.py
     urlpatterns = [
         path('articles/', views.article_list),
     ]
     ```
     
     ```python
     # articles/views.py
     from rest_framework.response import Response
     from rest_framework.decoreators import api_view
     from .models import Article
     from .serializers import ArticleListSerializer
     @api_view(['GET'])
     def article_list(request):
         articles = Article.objects.all()
         serializer = ArticleListSerializer(articles, many=True)
         return Response(serializer.data)
     ```
     
     > `api_view` decorator
     > 
     > - DEF view 함수에서는 필수로 작성되며 view 함수를 실행하기 전 HTTP 메서드를 확인
     > 
     > - 기본적으로 GET 메서드만 허용되며 다른 메서드 요청에 대해서는 405 Method Not Allowed로 응답
     > 
     > - DRF view 함수가 응답해야 하는 HTTP 메서드 목록을 작성
     > 
     > `many` 옵션
     > 
     > - Serialize 대상이 QuerySet인 경우 입력
     > 
     > `data` 속성
     > 
     > - Serialized data 객체에서 실제 데이터를 추출
  
  3- `http://127.0.0.1:8000/api/v1/articles/` 응답 확인

- GET - **Detail**
  
  1. 각 게시글의 상세 정보를 제공하는 ArticleSerializer 정의
     
     ```python
     # articles/serializers.py
     class ArticleSerializer(serializers.ModelSerializer):
         class Meta:
             model = Article
             fields = '__all__'
     ```
  
  2- url 및 view 함수 작성
     
     ```python
     # articles/urls.py
     urlpatterns = [
         path('articles/<int:article_pk>/' views.article_detatil),
     ]
     ```
     
     ```python
     # articles/views.py
     from .serializers import ArticleListSerializer, ArticleSerializer
     @api_view(['GET'])
     def article_detail(request, article_pk):
         article = Article.objects.get(pk=article_pk)
         serializer = ArticleSerializer(article)
         return Response(serializer.data)
     ```
  
  3- `http://127.0.0.1:8000/api/v1/articles/` 응답 확인

#### POST method - <mark>생성</mark>

- POST
  
  1. 게시글 데이터 생성하기
     
     - 데이터 생성이 성공했을 경우 201 Created 응답
     
     - 데이터 생성이 실패했을 경우 400 Bad request 응답
  
  2. article_list view 함수 구조 변경 (method에 따른 분기처리)
     
     ```python
     # articles/views.py
     from rest_framework import status
     @api_view(['GET', 'POST'])
     def article_list(request):
         if request.method == 'GET':
             articles = Article.objects.all()
             serializer = ArticleListSerializer(articles, many=True)
             return Response(serializer.data)
         elif request.method == 'POST':
             serializer = ArticleSerialize(data=request.data)
             if serializer.is_valid():
                 serializer.save()
                 return Response(serializer.data, status=status.HTTP_201_CREATED)
             return Response(serializer.errors, status=status.HTTP_400_BAD_REQUEST)
     ```
  
  3- POST `http://127.0.0.1:8000/api/v1/articles/` 응답 확인
  
  4- 새로 생성된 게시글 데이터 확인 : 
     
     GET `http://127.0.0.1:8000/api/v1/articles/21/`

#### DELETE method - <mark>삭제</mark>

- DELETE
  
  1. 게시글 데이터 삭제하기 (성공했을 경우는 204 No Content 응답)
     
     ```python
     # articles/views.py
     @api_view(['GET', 'DELETE'])
     def article_detail(request, article_pk):
         article = Article.objects.get(pk=article_pk)
         if request.method == 'GET':
             serializer = ArticleSerializer(article)
             return Response(serializer.data)
         elif request.method == 'DELETE':
             article.delete()
             return Response(status=status.HTTP_204_NO_CONTENT)
     ```
  
  2- DELETE `http://127.0.0.1:8000/api/v1/articles/21/` 응답 확인

#### PUT method - <mark>수정</mark>

- PUT
  
  1. 게시글 데이터 수정하기 (성공했을 경우는 200 OK 응답)
     
     ```python
     # articles/views.py
     @api_view(['GET', 'DELETE', 'PUT'])
     def article_detail(request, article_pk):
         ...
         elif request.method == 'PUT':
             serializer = ArticleSerializer(article, data=request.data, partial=True)
             if serializer.is_valid():
                 serializer.save()
                 return Response(serializer.data)
             return Response(serializer.errors, status=status.HTTP_400_BAD_REQUEST)
     ```
     
     > `partial` argument
     > 
     > - '부분 업데이트'를 허용하기 위한 인자
     > 
     > - 예를 들어 partial 인자 값이 False일 경우 게시글 title만을 수정하려고 해도 반드시 content 값도 요청 시 함께 전송해야 함
     > 
     > - 기본적으로 serializer는 모든 필수 필드에 대한 값을 전달 받기 때문
     >   
     >   즉, 수정하지 않는 다른 필드 데이터도 모두 전송해야 하며 그렇지 않으면 유효성 검사에서 오류가 발생
  
  2- PUT `http://127.0.0.1:8000/api/v1/articles/1/` 응답 확인
  
  3- GET `http://127.0.0.1:8000/api/v1/articles/1/` 수정된 데이터 확인
