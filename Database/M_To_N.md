# Many to many relationships

: 한 테이블의 0개 이상의 레코드가 다른 테이블의 0개 이상의 레코드와 관련된 경우

- 양 쪽 모두에서 N:1 관계를 가짐

- M:N 관계 주요 사항
  
  - M:N 관계로 맺어진 두 테이블에는 물리적인 변화가 없음
  
  - `ManyToManyField`는 중개 테이블을 자동으로 생성
  
  - `ManyToManyField`는 M:N 관계를 맺는 두 모델 어디에 위치해도 상관 없음
    
    - 대신 필드 작성 위치에 따라 참조와 역참조 방향을 주의할 것
  
  - N:1은 완전한 종속의 관계였지만, M:N은 종속적인 관계가 아니며 '의사에게 진찰받는 환자 & 환자를 진찰하는 의사' 이렇게 2가지 형태 모두 표현 가능

- 의사 - 환자 예시로 모델 생성 연습
  
  1. 예약 모델 생성
     
     - 환자 모델의 외래 키를 삭제하고 별도의 예약 모델을 새로 생성
     
     - 예약 모델은 의사와 환자에 각각 N:1 관계를 가짐
     
     > ```python
     > # hospitals/models.py
     > 
     > # 외래 키 삭제
     > clas Patient(models.Model):
     >     name = models.TextField()
     >     def __str__(self):
     >         return f'{self.pk}번 환자 {self.name}'
     > 
     > # 중개 모델 작성
     > class Reservation(models.Model):
     >     doctor = models.ForeignKey(Doctor, on_delete=models.CASCADE)
     >     patient = models.ForeignKey(Patiend, on_delete=models.CASCADE)
     >     def __str__(self):
     >         return f'{self.doctor_id}번 의사의 {self.patiend_id}번 환자'
     > ```
  
  2. 예약 데이터 생성
     
     - 데이터베이스 초기화 후 Migrations 진행 및 shell_plus 실행
     
     - 의사와 환자 생성 후 예약 만들기
     
     > ```python
     > doctor1 = Doctor.objects.create(name='allie')
     > patiend1 = Patient.objects.create(name='carol')
     > 
     > Reservation.objects.create(doctor=doctor1, patient=patient1)
     > ```
  
  3. 예약 정보 조회
     
     - 의사와 환자가 예약 모델을 통해 각각 본인의 진료 내역 확인
     
     > ```python
     > # 의사 -> 예약 정보 찾기
     > doctor1.reservation_set.all()
     > <QuerySet [<Reservation: 1번 의사의 1번 환자>]>
     > 
     > # 환자 -> 예약 정보 찾기
     > patiend1.reservation_set.all()
     > <QuerySet [<Reservation: 1번 의사의 1번 환자>]>
     > ```
  
  4. 추가 예약 생성
     
     - 1번 의사에게 새로운 환자 예약 생성
     
     > ```python
     > patient2 = Patiend.objects.create(name='duke')
     > 
     > Reservation.objects.create(doctor=doctor1, patient=patiend2)
     > ```
  
  5. 예약 정보 조회
     
     - 1번 의사의 예약 정보 조회
     
     > ```python
     > # 의사 > 환자 목록
     > doctor1.reservation_set.all()
     > <QuerySet [<Reservation: 1번 의사의 1번 환자>, <Reservation: 1번 의사의 2번 환자>]>
     > ```

---

## `ManyToManyField()`

: M:N 관계 설정 모델 필드

- 의사 - 환자 예시로 모델 생성 연습
  
  1. 환자 모델에 `ManyToManyField` 작성
     
     - 의사 모델에 작성해도 상관없으며 참조/역참조 관계만 잘 기억할 것
     
     > ```python
     > # hospitals/models.py
     > 
     > class Patient(models.Model):
     >     # ManyToManyField 작성
     >     doctors = models.ManyToManyField(Doctor)
     >     name = models.TextField()
     > 
     >     def __str__(self):
     >         return f'{self.pk}번 환자 {self.name}'
     > ```
  
  2. 의사 1명과 환자 2명 생성
     
     > ```python
     > doctor1 = Doctor.objects.create(name='allie')
     > patiend1 = Patient.objects.create(name='carol')
     > patient2 = Patiend.objects.create(name='duke')
     > ```
  
  3. 환자가 예약 생성
     
     > ```python
     > # patient1이 doctor1에게 예약
     > patient1.doctors.add(doctor1)
     > 
     > # patient1 - 자신이 예약한 의사 목록 확인
     > patient1.doctors.all()
     > <QuerySet [<Doctor: 1번 의사 allie>]>
     > 
     > # doctor 1 - 자신의 예약된 환자 목록 확인
     > doctor1.patient_set.all()
     > <QuerySet [<Patient: 1번 환자 carol>]>
     > ```
  
  4. 의사가 예약 생성
     
     > ```python
     > # doctor1이 patient2에게 예약
     > doctor1.patiend_set.add(patient2)
     > 
     > # doctor 1 - 자신의 예약된 환자 목록 확인
     > doctor1.patient_set.all()
     > <QuerySet [<Patient: 1번 환자 carol>, <Patient: 2번 환자 duke>]>
     > 
     > # patient1 - 자신이 예약한 의사 목록 확인
     > patient1.doctors.all()
     > <QuerySet [<Doctor: 1번 의사 allie>]>
     > 
     > # patient2 - 자신이 예약한 의사 목록 확인
     > patient2.doctors.all()
     > <QuerySet [<Doctor: 1번 의사 allie>]>
     > ```
  
  5. 예약 취소하기
     
     - 이전에는 Reservation을 찾아서 지워야 했다면, 이제는 `.remove()`로 삭제 가능
     
     > ```python
     > # doctor1이 patient1 진료 예약 취소
     > doctor1.patient_set.remove(patient1)
     > ```
     > 
     > ```python
     > # patient2가 doctor2 진료 예약 취소
     > patient2.doctors.remove(doctor1)
     > ```

---

## `through` argument

: 중개 테이블에 '추가 데이터'를 사용해 M:N 관계를 형성하려는 경우에 사용

- 의사 - 환자 예시로 모델 생성 연습
  
  1. `Reservation` Class 재작성 및 `through` 설정
     
     - 이제는 예약 정보에 '증상'과 '예약일'이라는 추가 데이터가 생김
     
     > ```python
     > # hospitals/models.py
     > 
     > clas Patient(models.Model):
     >     doctors = models.ManyToManyField(Doctor, through='Reservation')
     >     name = models.TextField()
     >     def __str__(self):
     >         return f'{self.pk}번 환자 {self.name}'
     > 
     > # 중개 모델 작성
     > class Reservation(models.Model):
     >     doctor = models.ForeignKey(Doctor, on_delete=models.CASCADE)
     >     patient = models.ForeignKey(Patiend, on_delete=models.CASCADE)
     >     symptom = models.TextField()
     >     reserved_at = models.DateTimeField(auto_now_add=True)
     > 
     >     def __str__(self):
     >         return f'{self.doctor_id}번 의사의 {self.patiend_id}번 환자'
     > ```
  
  2. 의사 1명과 환자 2명 생성
     
     > ```python
     > doctor1 = Doctor.objects.create(name='allie')
     > patiend1 = Patient.objects.create(name='carol')
     > patient2 = Patiend.objects.create(name='duke')
     > ```
  
  3. Reservation class를 통한 예약 생성
     
     > ```python
     > reservation1 = Reservation(doctor=doctor1, patient=patient1, sysmtom='headache')
     > reservation1.save()
     > ```
  
  4. Patient 또는 Doctor의 인스턴스를 통한 예약 생성(`through_defaults`)
     
     > ```python
     > patient2.doctors.add(doctor1, through_defaults={'symptom':'flu'})
     > ```
  
  5. 예약 취소하기
     
     - 생성과 마찬가지로 의사와 환자 모두 각각 예약 삭제 가능
     
     > ```python
     > # doctor1이 patient1 진료 예약 취소
     > doctor1.patient_set.remove(patient1)
     > ```
     > 
     > ```python
     > # patient2가 doctor2 진료 예약 취소
     > patient2.doctors.remove(doctor1)
     > ```

---

## `ManyToManyField(to, **options)`

: M:N 관계 설정 시 사용하는 모델 필드

- `ManyToManyField` 특징
  
  - 양방향 관계 : 어느 모델에서든 관련 객체에 접근할 수 있음
  
  - 중복 방지 : 동일한 관계는 한 번만 저장됨

- `ManyToManyField`의 대표 인자 3가지
  
  - `related_name`
    
    : 역참조시 사용하는 manager name을 변경
    
    > ```python
    > class Patient(models.Model):
    >     doctors = models.ManyToManyField(Doctor, related_name='patients')
    >     name = models.TextField()
    > 
    > # 변경 전
    > doctor.patient_set.all()
    > # 변경 후 (변경 후 이전 manager name은 사용 불가)
    > doctor.patients.all()
    > ```
  
  - `symmetrical`
    
    : 관계 설정 시 대칭 유무 설정
    
    - `ManyToManyField`가 동일한 모델을 가리키는 정의에서만 사용
    
    - 기본 값 : `True`
      
      - `True`일 경우
        
        - source 모델의 인스턴스가 target 모델의 인스턴스를 참조하면 자동으로 target 모델 인스턴스도 source 모델 인스턴스를 자동으로 참조하도록 함(대칭)
        
        - 즉, 내가 당신의 친구라면 자동으로 당신도 내 친구가 됨
        
        - source 모델 : 관계를 시작하는 모델
        
        - target 모델 : 관계의 대상이 되는 모델
      
      - `False`일 경우
        
        - `True`와 반대(대칭되지 않음)
    
    > ```python
    > # 예시
    > 
    > class Person(models.Model):
    >     friends = models.ManyToManyField('self')
    >     # friends = models.ManyToManyField('self', symmetrical=False)
    > ```
  
  - `through`
    
    : 사용하고자 하는 중개모델을 지정
    
    - 일반적으로 '추가 데이터를 M:N 관계와 연결하려는 경우'에 사용

- M:N 에서의 대표 조작 methods
  
  - `add()`
    
    : 관계 추가. 지정된 객체를 관련 객체 집합에 추가
  
  - `remove()`
    
    : 관계 제거. 관련 객체 집합에서 지정도니 모델 객체를 제거

---

## 좋아요 기능 구현

1. 모델 관계 설정
   
   - Article(M) - User(N) : 0개 이상의 게시글은 0명 이상의 회원과 관련
   
   - Article 클래스에 ManyToManyField 작성
   
   > ```python
   > # articles/models.py
   > 
   > class Article(models.Model):
   >     user = models.ForeignKey(settings.AUTH_USER_MODEL, on_delete=models.CASCADE)
   >     like_users = models.ManyToManyField(settings.AUTH_USER_MODEL)
   >     title = models.CharField(max_length=10)
   >     content = models.TextField()
   >     created_at = models.DateTimeField(auto_now_add=True)
   >     updated_at = models.DateTimeField(auto_now=True)
   > ```

2. Migration 진행 후 에러 발생 - 역참조 매니저 충돌했기 때문에
   
   - `like_users` 필드 생성 시 자동으로 역참조 매니저 `.article_set`가 생성됨
   
   - 그러나 이전 N:1(Article-User) 관계에서 이미 같은 이름의 매니저를 사용 중
     
     - `user.article_set.all()` : 해당 유저가 작성한 모든 게시글 조회
   
   - 'user가 작성한 글(`user.article_set`)'과 'user가 좋아요를 누른 글(``user.article_set`)'을 구분할 수 없게 된
   
   - user 와 관계된 ForeignKey 혹은 ManyToManyField 둘 중 하나에 `related_name` 작성 필요

3. 모델 관계 설정 - `related_name` 작성 후 Migration 재진행
   
   > ```python
   > # articles/models.py
   > 
   > class Article(models.Model):
   >     user = models.ForeignKey(settings.AUTH_USER_MODEL, on_delete=models.CASCADE)
   >     like_users = models.ManyToManyField(settings.AUTH_USER_MODEL, related_name='like_articles')
   >     title = models.CharField(max_length=10)
   >     content = models.TextField()
   >     created_at = models.DateTimeField(auto_now_add=True)
   >     updated_at = models.DateTimeField(auto_now=True)
   > ```
   
   - User-Article간 사용 가능한 전체 related manager
     - `article.user` : 게시글을 작성한 유저. N:1
     - `user.article_set` : 유저가 작성한 게시글(역참조). N:1
     - `article.like_users` : 게시글을 좋아요한 유저. M:N
     - `user.like_articles` : 유저가 좋아요한 게시글(역참조). M:N

4. 기능 구현
   
   1. url 작성
      
      > ```python
      > # articles/urls.py
      > 
      > urlpatterns = [
      >     ...
      >     path('<int:article_pk>/likes/', views.likes, name='likes'),
      > ]
      > ```
   
   2. view 함수 작성
      
      > ```python
      > # articles/views.py
      > 
      > @login_required
      > def likes(request, article_pk):
      >     article = Article.objects.get(pk=article_pk)
      >     if request.user in article.like_users.all():
      >         article.like_users.remove(request.user)
      >     else:
      >         article.like_users.add(request.user)
      >     return redirect('articles:index')
      > ```
   
   3. index 템플릿에서 각 게시글에 좋아요 버튼 출력
      
      > ```html
      > <!-- articles/index.html -->
      > 
      > {% for article in articles %}
      >     ...
      >     <form action="{% url 'articles:likes' article.pk %}" method="POST">
      >         {% csrf_token %}
      >         {% if request.user in article.like_users.all %}
      >             <input type="submit" value="좋아요 취소">
      >         {% else %}
      >             <input type="submit" value="좋아요">
      >         {% endif %}
      >     </form>
      >     <hr>
      > {% endfor %}
      > ```
   
   4. 
