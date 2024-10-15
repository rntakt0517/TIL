# M_to_N_2

---

## 팔로우 기능 구현

#### 프로필 페이지

- 각 회원의 개인 프로필 페이지에 팔로우 기능을 구현하기 위해 프로필 페이지를 먼저 구현하기
1. **url 작성**
   
   ```python
   # accounts/urls.py
   urlpatterns = [
       path('profile/<username>/', views.profile, name='profile'),
   ]
   ```

2. **view 함수 작성**
   
   ```python
   # accounts/views.py
   from django.contrib.auth import get_user_model
   def profile(request, username):
       User = get_user_model()
       person = User.objects.get(username=username)
       context = {
           'person': person,
       }
       return render(request, 'accounts/profile.html', context)
   ```

3. **profile 템플릿 완성**
   
   ```html
   <!-- accounts/profile.html -->
   <h1>{{ person.username }}님의 프로필</h1>
   <hr>
   <h2>{{ person.username }} 가 작성한 게시글</h2>
   {% for article in person.article_set.all %}
       <div>{{ article.title }}</div>
   {% endfor %}
   <hr>
   <h2>{{ person.username }} 가 작성한 댓글</h2>
   {% for comment in person.comment_set.all %}
       <div>{{ comment.content }}</div>
   {% endfor %}
   <hr>
   <h2>{{ person.username }} 가 좋아요한 게시글</h2>
   {% for article in person.like_articles.all %}
       <div>{{ article.title }}</div>
   {% endfor %}
   ```

4. **프로필 페이지로 이동할 수 있는 링크 작성**
   
   ```html
   <!-- articles/index.html -->
   <a href="{% url 'accounts:profile' user.username %}">내 프로필</a>
   <p>작성자 : <a href="{% url 'accounts:profile' article.user.username %}">{{ article.user }}</a></p>
   ```

5. **프로필 페이지 결과 확인**

#### 모델 관계 설정

- User(M) - User(N) : 0명 이상의 회원은 0명 이상의 회원과 관련
1. **ManyToManyField 작성**
   
   ```python
   # accounts/models.py
   class User(AbstractUser):
       followings = models.ManyToManyField('self', symmetrical=False, related_name='follewers')
   ```
   
   - 참조 : 내가 팔로우하는 사람들 (팔로잉, followings)
   
   - 역참조 : 상대방 입장에서 나는 팔로워 중 한 명 (팔로워, followers)
   
   > 바뀌어도 상관 없으나 관계 조회 시 생각하기 편한 방향으로 정한 것

2. **Migrations 진행 후 중개 테이블 확인**

#### 기능 구현

1. **url 작성**
   
   ```python
   # accounts/urls.py
   urlpatterns = [
       path('<int:user_pk>/follow/', views.follow, name='follow'),
   ]
   ```

2. **view 함수 작성**
   
   ```python
   # accounts/views.py
   @login_required
   def follow(request, user_pk):
       User = get_user_model()
       person = User.objects.get(pk=user_pk)
       if person != request.user:
           if request.user in person.followers.all():
               person.followers.remove(request.user)
           else:
               person.followers.add(request.user)
       return redirect('accounts:profile', person.username)
   ```

3. **프로필 유저의 팔로잉, 팔로워 수 & 팔로우, 언팔로우 버튼 작성**
   
   ```html
   <!-- accounts/profile.html -->
   <div>
       <div>
           팔로잉 : {{ person.following.all|length }} / 팔로워 : {{ person.followers.all|length }}
       </div>
       {% if request.user != person %}
           <div>
               <form action="{% url 'accounts:follow' person.pk %}" method="POST">
                   {% csrf_token %}
                   {% if request.user in person.followers.all %}
                       <input type="submit" value="Unfollow">
                   {% else %}
                       <input type="submit" value="Follow">
                   {% endif %}
               </form>
           </div>
       {% endif %}
   </div>
   ```

4. **팔로우 버튼 클릭 -> 팔로우 버튼 변화 및 중개 테이블 데이터 확인**

---

## Fixtures

Django가 데이터베이스로 가져오는 방법을 알고 있는 데이터 모음 (데이터는 데이터베이스 구조에 맞추어 작성 되어있음)

- 사용 목적 : 초기 데이터 제공

- 초기 데이터의 필요성 : 프로젝트의 앱을 처음 서정할 때 동일하게 준비된 데이터로 데이터베이스를 미리 채우는 것이 필요한 순간이 있음

- 사전준비 : M:N까지 모두 작성된 Django 프로젝트에서 유저, 게시글, 댓글 등 각 데이터를 최소 2~3개 이상 생성해두기

- `dumpadata` : 생성 (데이터 추출)

- `loaddata` : 로드 (데이터 입력)

#### dumpdata

데이터베이스의 모든 데이터를 추출

- 작성 예시
  
  ```bash
  python manage.py dumpdata [app_name[.ModelName] [app_name[.ModelName] ...]] > filename.jsone] ...]] > filename.json
  ```

- Fixtures 파일을 직접 만들지 말 것 (반드시 dumpdata 명령어를 사용하여 생성)

#### loaddata

Fixtures 데이터를 데이터베이스로 불러오기

- Fixtures 파일 기본 경로 : `app_name/fixtures/`

- load 진행 후 데이터가 잘 입력되었는지 확인
  
  ```bash
  python manage.py loaddmata articles.json users.json comments.json
  ```

- 순서 주의사항
  
  - 만약 loaddata를 한번에 실행하지 않고 별도로 실행한다면 모델 관계에 따라 load 순서가 중요할 수 있음
    
    - comment는 article에 대한 key 및 user에 대한 key가 필요
    
    - article은 user에 대한 key가 필요
  
  - 즉, 현재 모델 관계에서는 user -> article -> comment 순으로 data를 load 해야 오류가 발생하지 않음
    
    ```bash
    python manage.py loaddata user.json
    python manage.py loaddate articles.json
    python manage.py loaddate comments.json
    ```
