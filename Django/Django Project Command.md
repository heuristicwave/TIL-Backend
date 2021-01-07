## Django Project Setting

### Using pipenv

```shell
$ pip install --user pipenv
# 안될 때
$ sudo -H pip install -U pipenv
```

Creating a bubble and activate

```shell
$ pipenv --three	# python 3.x
$ pipenv shell
```

Git

```shell
$ git init
$ git remote add origin {Repositoy URL}
$ git add .
$ git commit -m "commit message"
$ touch .gitignore		# add python git ignore
$ git push origin master
```

Install Django

```shell
# pip install Django : latest version
$ pipenv install Django==2.2.5	
```

Creating a config

```shell
$ django-admin startproject config
$ mv manage.py ../	# 밖으로 이동
$ mv config ../		# 내부에 있는 config 밖으로
# 이후 가장 밖에 있는 config 폴더 제거
```
> **startproject vs startapp**
>
> 장고 프로젝트를 처음 시작할 때는 `startproject` 이후, 프로젝트 안에서 새 앱을 추가할 때는 `startapp`

Changing a settings.py

```python
TIME_ZONE = 'Asia/Seoul'
```

Creating a project (구현에 필요한 기능 갯수 만큼 만듬)

```shell
$ django-admin startapp {application name + 's'}
```

*The name of the application must be written in a plural form.*

<br>

### Settings.py

구현에 필요한 앱 추가하기

```python
PROJECT_APPS = [
	'{app name}.apps.{apps.py의 method name}'
]
```

INSTALLED_APPS과 프로젝트 추가 앱 구분

```python
INSTALLED_APPS = DJANGO_APPS + PROJECT_APPS
```



**모델 수정(필드추가, ....) 후 반영하기**

```shell
# 선행작업, db.sqlite 3 파일 삭제
$ python manage.py makemigrations
$ python manage.py migrate
```

<br>

Creating a superuser

```shell
$ python manage.py createsuperuser
```

> [장고 Admin 계정_찾기](https://kitle.xyz/post/58/)





### models.py

테이블 설계 후 모델 반영시 변경사항 있을 때, **migration 초기화**

새로운 class생성하면 admin.py에 등록

<br>

각각의 어플리케이션 폴더 안에 **urls.py** 만들기

관련 함수 만들고 관련함수에 해당하는 이름으로 템플릿 만들기



`config settings.py`에 DIRS 추가

```python
"DIRS": [os.path.join(BASE_DIR, "templates")],
```



템플릿 이름과 extension 이름을 같게

view 이름은 urls.py 이름과 같게 
