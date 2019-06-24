## 20190620

Django 공부를 시작했다. Youtube에서 아주 좋은 인강을 찾아서 그거보고 방학 때 공부하면 Django를 어느정도 이해하고 사용할 수 있을 것 같다.

[Corey Schafer ](https://www.youtube.com/watch?v=UmljXZIypDc&list=PL-osiE80TeTtoQCKZ03TU5fNfx2UY6U4p)

**우선 Django는 Flask와 달리 django-amdin command와 manage.py에 인자를 전달함으로써 애플리케이션을 이용한다.**

이 부분으로 인해, 코딩 자체보단 Django 관련 command들의 이해와 Framework의 Structure를 이해하는 게 중요한 것 같다.

### 요약

`django-admin startproject {projectName}`  and `django-admin startapp {appName]`

django project Structure에 대해. router 설정하는 대략적 방법. view functions를 전달하는 방법.

`python manage.py runserver`

### 내용

`django-admin startproject {projectName} `  으로 project를 만든다.

projectName Directroy 안에 manage.py와 다시 projectName 이라는 Directory가 생긴다.

![0620_tree](imgs/0620_tree.png)

이런 식으로 project directory가 생성된다. 맨위의 Directory 를 root Directory라고 하겠다

그 root Directroy에서 `django-admin startapp {appName}`  으로 project내의 app을 만든다.

![0620_tree2](imgs/0620_tree2.png)

tutorial directory의 내부의 

&#95;&#95;init&#95;&#95;.py"는 그냥 얘네가 패키지라는 것을 알려주기 위함이고

settings.py는 내가 생성한 project에 관한 설정들을 python file로 저장해놓는 곳이다.

urls.py 는 router를 설정하는 파일이다.

__app__ directory 에서 내가 관리할 file은

`views.py` 와 `urls.py`이다.

`urls.py`는 내가 새로 만들어야하는 파일이다. tutorial directory `urls.py`와 같은 형식으로 참고해서 적어주자

이 때의 root 경로는 내가 나중에 tutorial directory의 `urls.py` 에서 설정하기 나름이다. 만약에 `blog/` 다음의 router들을 생성하고 있다면, tutorial/urls.py에서 `"blog/"` 에 대한 view function에 indclude("appOne.urls") 이런 식으로 정의해주면. 알아서 appOne/urls.py의 경로가 `blog/` 

`views.py` 가 비로소 드디어 client가 해당 url에 접속했을 때 수행할 view functions를 정의하는 공간이다.

django.http의 HttpResponse모듈을 이용해 client에게 response를 전달한다.

## 20190622

### 요약

smtplib 모듈을 이용해 email을 보내봤다. 자세히는 아직 다루지 못했지만, 작동은 한다.

패키지에 대한 이해가 조금 필요할 듯하다. 그냥 간단하게 조금 확인해보고싶어서 temp.py 등으로 임의로 테스트 해보려는데 패키지가 아니면 모듈을 이용할 수 없다는둥 이래저래 오류가 많이 뜨더라.

Template을 이용해 html file을 정의하는 법에 조금 익숙해졌다. `base.html`을 만들어 `guestbook.html`이 상속받을 수 있게 설계했다.

SQLite3 DB를 이용하는 법을 배웠다.

### 내용

#### How to use SQLite 

자신의 app의 디렉토리에 있는 models.py로 가준다.

![0622_model](imgs/0622_model.png)

이런 식으로 적절히 django.db의 models.Model 클래스를 상속받는 나의 데이터 model 클래스를 정의한다.

app의 모델을 정의했으면 `manage.py`가 있는 프로젝트의 root directory로 가서 

`python manage.py makemigrations blogApp`  을 통해 blogApp의 db model을 다시 만들어주고

`python manage.py migrate blogApp`  을 통해 내 프로젝트의 db에 적용해준다.



#### 기타 template 사용법
in base.html

    {% block content %}
    {% endblock content %}

in guestbook.html ( 예를들어 )

    {% extends "blogApp/base.html" %}
    {% block content %}
    추가하고픈 내용
    {% endblock content %}


## 20190623

### 요약

django 에서 DB를 다루는 법을 좀 더 알 게 되었다.

POST 로 전달받은 Guestbook 내용을 통해 DB에 정보를 추가할 수 있어졌다.

Bootstrap 의 Grid Layout에 대해 좀 더 감이 잡혔다.

template에 인자를 전달하고 사용해보았다.

### 내용

#### DB 다루는법

나의 Django Projcet의 DBShell을 이용하려면 ( 나의 경우 SQLite3 )

`python manage.py dbshell` or 

```
$ sqlite3
$ .open {DB File Name} 
```

을 통해 가능하다.

참고로 sqlite3 shell을 이용하고 싶다면 따로 설치해주어야하고.

```
python manage.py shell
>>> from {app name.models} import {modelName}
>>> {modelName}.objects.all()
>>> {modelName}.objects.filter(name="test").delte()
```

등으로도 DB를 관리할 수 있다.

`python manage.py sqlmigrate {appName} {migrateNumber}`

을 통해 SQL language로 해당 migration을 할 때 어떤 작업을 수행하는 지 볼 수 있다







#### Django Query

view function이 인자로 받는 request를 이용해

`request.POST.get("이름")` or `request.GET.get("이름")` or `request.GET["이름"]` 등등으로 query data를 얻을 수 있다.



#### template에 인자 전달하기

in view function definition

```
dataObject={"articles":Article.objects.all()}
return render(request, "blogApp/guestbook.html", dataObject)
```

위와같이 QuerySet을 다시 dictionary 등에 대입하여 전달한다.



#### Bootstrap Grid

row는 margin -15px

col은 padding +15px

container -> row -> col 순으로 배열해야하는데

row 전에는 한 번이라도 container가 와야 깔끔히 사용가능하고 그 이후엔

row->col만 써도 깔끔. 계속 container->row->col 식으로 사용하면 점점 좁아짐.



#### 보완할 점 및 궁금한 점

html file의 structure가 좀 더러워서 bootstrap도 좀 더 개념을 잡으면서 정리해보고 싶긴한데, front 보단 backend에 더 관심이 많아서 일단 보류함.

POST request에 대해 response를 보낼 때 view function에 decorator로 @csrf_exempt  이걸 적던데, 왜 쓰는 건지...?

guestbook delete는 구현헀는데, guestbook modify는 새로 수정창을 열어야해서 어떻게 구현할 지 고민 중..



## 20190624

### 요약

aws ec2 instance를 이용해 server을 돌렸다.



### 설명

#### EC2 Instance로 서버돌리기

포트와 아이피가 어떤 식으로 바인딩되는 지에 대한 이해가 있어야 명확히 서버를 돌리고 포트를 바인딩 하는 원리를 알 수 있다.

우선은 nohup을 통해 background 에서 detach mode로 python을 실행시킬 수 있었다.

ex) `nohup python manage.py runserver 0:80`

#### 시간 이용하기

models.py 에서 `from django.utils import timezone`과

테이블의 요소로서 `time=models.DateTimeField(default=timezone.now)`로 함수의 리턴값이 아닌 now라는 함수 자체를 default의 값으로 전달한다.

이후 template에서는 [Django date filter](https://docs.djangoproject.com/en/2.2/ref/templates/builtins/#date) 참고하여 time및date를 이용할 수 있다. ex) `{{ article.time|date:"Y.m.d. H:i" }}`







