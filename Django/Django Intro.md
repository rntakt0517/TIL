# Django

[Web Application](#web-application)

[Framework](#framwork)

[Django Design Pattern](#django-design-pattern)

[요청과 응답](#요청과-응답)

[루틴](#루틴)

---

## Web Application

- **Web application (web service) 개발**
  
  - 인터넷을 통해 사용자에게 제공되는 소프트웨어 프로그램을 구축하는 과정
  
  - 다양한 디바이스 (모바일, 태블릿, PC 등)에서 웹 브라우저를 통해 접근하고 사용

- **클라이언트와 서버**
  
  - 클라이언트 (Client) : 서비스를 요청하는 주체 ex) 웹 브라우저
  
  - 서버 (Server) : 클라이언트의 요청에 응답하는 주제 ex) 웹 페이지

- **Fronted & Backend**
  
  - 프론트엔드 (Frontend) : 사용자 인터페이스(UI)를 구성하고, 사용자가 애플리케이션과 상호작용할 수 있도록 함 ex) HTML, CSS 등
  
  - 백엔드 (Backend) : 서버 측에서 동작하며, 클라이언트의 요청에 따라 처리와 데이터베이스와의 상호작용 등을 담당 ex) Python, 데이터베이스, API 등

---

## Framework

- **Web Framework **: 웹 애플리케이션을 빠르게 개발할 수 있도록 도와주는 친구

- <mark>**가상 환경**</mark>
  
   : Python 애플리케이션과 그에 따른 패키지를 따로 관리할 수 있는 **독립적인** 실행 환경
  
  > - 가상 환경은 Python 환경을 "On/Off"로 전환하는 개념
  > 
  > - 가상환경은 "방"이 아니라 "도구 세트"
  > 
  > - 프로젝트마다 별도의 가상환경 사용
  > 
  > - 일반적으로 가상환경 폴더 venv는 관련된 프로젝트와 동일한 경로에 위치
  > 
  > - 가상환경 venv는 gitignore에 작성되어 원격 저장소에 공유되지 않음
  
  - **가상 환경 venv 생성**
    
    `python -m venv venv`
  
  - **가상 환경 활성화**
    
    `source venv/Scripts/activate`
  
  - **환경에 설치된 패키지 목록 확인**
    
    `pip list`
  
  - **설치된 패키지 목록 생성**
    
    `pip freeze > requirements.txt`
    
    > - 주요 특징
    >   
    >   - 가상 환경의 패키지 목록을 쉽게 공유 가능
    >   
    >   - 프로젝트의 의존성을 명확히 문서화
    >   
    >   - 동일한 개발 환경을 다른 시스템에서 재현 가능
    > 
    > - 주의사항
    >   
    >   - <mark>**의존성 패키지 관리**</mark>
    >     
    >     : 한 소프트웨어 패키지가 다른 패키지의 기능이나 코드를 사용하기 때문에 그 패키지가 존재해야만 제대로 작동하는 관계
    >   
    >   - 환성화된 가상환경에서 실행해야 정확한 패키지 목록 생성
    >   
    >   - 시스템 전역 패키지와 구분 필요
  
  - 패키지 목록 기반 설치
    
    `pip install -r requirements.txt`
  
  - **가상환경 비활성화**
    
    `deactivate`

- **Django framework** : Python 기반의 대표적인 웹 프레임워크
  
  - 장점 : 다양성, 확장성, 보안, 커뮤니티 지원
  - 명령어
    - **Django 프로젝트 생성**
      
      `django-admir startproject firstpjt .`
    
    - **Django 서버 실행**
      
      `python manage.py runserver`
    
    - **서버 확인**
      
      `ctrl` + 링크 클릭
    
    - **Django 서버 끄기**
      
      `ctrl` + `c`

---

## Django Design Pattern

- **디자인 패턴**
  
  - 소프트웨어 설계에서 발생하는 문제를 해결하기 위한 일반적인 해결책
  
  - (공통적인 문제를 해결하는데 쓰이는 형식화 된 관행)
  
  - "애플리케이션의 구조는 이렇게 구성하자"라는 관행"

- <mark>**MVC 디자인 패턴**</mark>
  
  - Model, View, Controller
  
  - 애플리케이션을 구조화하는 대표적인 패턴
  
  - "데이터" & "사용자 인터페이스" & "비즈니스 로직"을 분리
    
    > 시각적 요소와 뒤에서 실행되는 로직을 서로 영향 없이 독립적이고 쉽게 유지 보수할 수 있는 애플리케이션을 만들기 위해

- <mark>**MTV 디자인 패턴**</mark>
  
  - Model, Template, View
  
  - Django에서 애플리케이션을 구조화하는 패턴
  
  - 기존 MVC 패턴과 동일하나 단순히 명칭을 다르게 정의한 것

- **Django project**
  
  - 애플리케이션의 집합
  
  - DB 설정, URL 연결, 전체 앱 설정 등을 처리

- **Django application**
  
  - 독립적으로 작동되는 기능 단위 모듈
  
  - 각자 특정한 기능을 담당하며 다른 앱들과 함께 하나의 프로젝트를 구성

- 앱을 사용하기 위한 순서
  
  1. **앱 생성**
     
     `python manage.py startapp articles`
  
  2. **앱 등록**
     
     `INSTALLED_APPS = [앞에 작성...]`

- <mark>**프로젝트 구조**</mark>
  
  - **`settings.py`** : 프로젝트의 모든 설정을 관리
  
  - **`urls.py`** : 요청 들어오는 URL에 따라 이에 해당하는 적절한 views를 연결
  
  - `__init__.py` : 해당 폴더를 패키지로 인식하도록 설정하는 파일
  
  - `asgi.py` : 비동기식 웹 서버와의 연결 관련 설정
  
  - `wsgi.py` : 웹 서버와의 연결 관련 설정
  
  - `manage.py`
    
     : Django 프로젝트와 다양한 방법으로 상호작용 하는 커맨드라인 유틸리티

- <mark>**앱 구조**</mark>
  
  - ****`admin.py` : 관리자용 페이지 설정
  
  - **`models.py`** : DB와 관련된 Model을 정의. MTV 패턴의 M
  
  - **`views.py`** : HTTP 요청을 처리하고 해당 요청에 대한 응답을 반환. MTV 패턴의 V
  
  - `apps.py` : 앱의 정보가 작성된 곳
  
  - `tests.py` : 프로젝트 테스트 코드를 작성하는 곳

---

## 요청과 응답

![image](https://github.com/user-attachments/assets/791cb739-099b-49ab-8954-e97bec7cf02f)

1. <mark>**URLs**</mark>
   
   - `from articles import views` : articles 패키지에서 views 모듈을 가져오는 것
   
   - **`urlpatterns = [..., path('index/', views.index),]`**
     
     : url 경로는 반드시 `/`로 끝나야 함
   
   > `http://127.0.0.1:8000/index/`로 요청이 왔을 때 request 객체를 views 모듈의 index view 함수에게 전달하며 호출

2. <mark>**View**</mark>
   
   - ```python
     from Django.shortcuts import reder
     
     def index(request):
         return render(request, 'articles/index.htlml')
     ```
   
   > view 함수가 정의되는 곳
   > 
   > 특정 경로에 있는 template과 request 객체를 결합해 응답 객체를 반환

3. <mark>**Template**</mark>
   
   1. `articles` 앱 폴더 안에 `templates` 폴더 생성
   
   2. `templates` 폴더 안에 `articles` 폴더 생성
   
   3. `articles` 폴더 안에 템플릿 파일 생성
   
   > **`app폴더 / templates / articles/index.htlml`**

---

## 루틴

1. 가상환경 생성

2. 가상환경 활성화

3. Django 설치

4. 패키지 목록 파일 생성 (패키지 설치시마다 진행)

5. `.gitignore` 파일 생성 (첫 add 전)

6. git 저장소 생성 (git init)

7. Django 프로젝트 생성


