## Django

#### MVT 개발

MVT 방식을 통해 모델, 뷰, 템플릿 모듈 간에 독립성을 유지할 수 있고, loose coupling 설계 원칙에 부합



`startproject`, `startapp` 명령을 통해, 자동으로 프로젝트 뼈대에 해당하는 디렉터리와 파일 생성



Model : 테이블 정의

View : 애플리케이션의 제어 흐름 및 처리 로직 정의

Template : 사용자가 보게 될 화면의 모습 정의 (*.html 파일에 작성)

<br>

#### settings.py

- 데이터베이스 설정 : 디폴트로 SQLite3 데이터베이스 엔진 사용
- 애플리케이션 등록 : 프로젝트에 포함되는 애플리케이션을 등록
- 템플릿 항목 설정
- 정적 파일 항목 설정
- 타임존 지정

<br>

#### models.py

테이블을 정의하는 파일

데이터베이스 처리는 ORM 기법을 사용. 즉, 테이블을 클래스로 매핑해서 테이블에 대한 CRUD 기능을 클래스 객체에 대해 수행하면, 장고가 내부적으로 SQL 처리를 해 DB에 반영

테이블의 컬럼은 클래스의 변수로 매핑. 테이블 클래스는 django.db.models.Model 클래스를 상속받아 정의.

테이블의 신규 생성, 테이블 정의 변경 등 변경 사항을 DB에 반영해주는 것을 마이그레이션 이라함. 

<br>

#### URLconf (urls.py)

url과 뷰를 매핑해줌

프로젝트 전체 URL을 정의하는 **프로젝트 URL**과 앱마다 정의하는 **앱 URL**, 2계층으로 나눠 코딩

URL 패턴별로 이름을 지정할 수 있고, 패턴 그룹에 대해 namespace를 지정할 수 도 있음. 이를 통해 소스에 URL을 하드 코딩하지 않아도 필요한 URL을 추출하게 해줌

<br>

#### views.py

뷰 로직을 코딩하는 파일

- 함수형 뷰(Function-based view)

  ```python
  def post_list(request):
  	return HTTPResponse('Call post_list')
  ```

- 클래스형 뷰(Class-based view)

  ```python
  class PostListView(TemplateView):
  	template_name = 'blog/post_list.html'
  
  post_list = PostListView.as_view()
  ```
  
  장고가 제공하는 제네릭 뷰 사용 가능(재활용 및 확장성 측면 유리)

> 클래스형 뷰가 간단한 경우 views.py에 코딩할 필요 없이 URLconf에서 뷰 및 뷰 처리에 필요한 파라미터를 모두 지정할 수 있다.
>
> 그러나 MVT 원칙을 따르기 위해 views.py에 코딩하는것을 지향

<br>

#### templates

웹 페이지 별로 템플릿 파일(*.html)을 한곳에 모아두기 위해 템플릿 디렉터리

- 프로젝트 템플릿 디렉터리 : TEMPLATES 설정의 DIRS 항목에 지정된 디렉터리

  base.html 등 전체 프로젝트의 Look and Feel에 관련 파일 저장

- 앱 템플릿 디렉터리 : 각 애플리케이션 디렉터리마다 존재하는 `templates/` 디렉터리

  각 앱에서 사용하는 템플릿 파일을 저장

<br>

#### 장고 웹 프로그래밍 준비 사항

1. Allowed Hosts
2. 애플리케이션 설정파일 등록
3. 템플릿 항목 설정
4. 데이터 베이스 엔진 선택
5. 타임존 지정

<br>

### 에러 핸들링

<br>

자동 생성된 파일에서 syntax error가 생길때

> 가상환경에서 재작업
>
> ```python
> # 가상환경 진입
> $ . /activate
> 
> # 가상환경 탈출
> $ deactivate
> ```

<br>

외부 접속 허용 방법 

```shell
$ python manage.py runserver 0.0.0.0:8000
```
