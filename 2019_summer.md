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

### 설명

How to use SQLite 

자신의 app의 디렉토리에 있는 models.py로 가준다.

![0622_model](0622_model.png)

이런 식으로 적절히 django.db의 models.Model 클래스를 상속받는 나의 데이터 model 클래스를 정의한다.

app의 모델을 정의했으면 `manage.py`가 있는 프로젝트의 root directory로 가서 

`python manage.py makemigrations blogApp`  을 통해 blogApp의 db model을 다시 만들어주고

`python manage.py migrate blogApp`  을 통해 내 프로젝트의 db에 적용해준다.

#### 기타 template 사용법
in base.html

`{% block content %}

{% endblock content %}`

in guestbook.html ( 예를들어 )

`{% extends "blogApp/base.html" %}

{% block content %}

추가하고픈 내용

{% endblock content %}`

