## 20190620

Django 공부를 시작했다. Youtube에서 아주 좋은 인강을 찾아서 그거보고 방학 때 공부하면 Django를 어느정도 이해하고 사용할 수 있을 것 같다.

[Corey Schafer](https://www.youtube.com/watch?v=UmljXZIypDc&list=PL-osiE80TeTtoQCKZ03TU5fNfx2UY6U4p)

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

`urls.py`는 tutorial directory `urls.py`와 같은 형식으로 참고해서 적어주자.

`views.py` 가 비로소 드디어 client가 해당 url에 접속했을 때 수행할 view functions를 정의하는 공간이다.

django.http의 HttpResponse모듈을 이용한
