# View

뷰는 웹 요청을 받아서 최종 응답 데이터를 웹 클라이언트로 반환하는 함수(호출 가능한 객체, callable)

웹 요청을 분석하고 DB처리 등 필요한 로직을 수행해 템플릿을 통해 화면해 표시할 데이터를 만들어, 최종 데이터를 클라이언트에게 응답해줌

<br>

## 제네릭 뷰

웹 프로그램 개발 시 공통적으로 사용하는 로직을 미리 개발하고 기본 클래스로 제공

클래스형 뷰를 작성하기 위해서는 제네릭 뷰를 상속받아 필요한 속성과 메소드를 오버라이딩 하는 작업이 필요

<br>

### 속성 오버라이딩

#### model

기본 뷰(View, TemplateView, RedirectView) 3개와 FormView를 제외하고는 모든 제네릭 뷰에서 사용하는 속성. 작업 대상 데이터가 들어 있는 모델을 지정. model 대신 queryset 속성으로 지정할 수도 있음. 다음 두가지 표현은 동일한 의미를 갖는다. `model = Bookmark` & `queryset = Bookmark.objects.all()`

> queryset 속성을 지정하면 model 속성은 무시

<br>

### 메소드 오버라이딩

#### get_quertset()

기본 뷰(View, TemplateView, RedirectView) 3개와 FormView를 제외하고는 모든 제네릭 뷰에서 사용하는 메소드



<br>

### View

모든 클래스형 뷰의 최상위 뷰

### Template View

단순하게 화면에 보여줄 템플릿 파일을 처리하는 간단한 뷰

```python
class HomeView(TemplateView):
	template_name = 'home.html'
```

### ListView 

여러 객체의 리스트를 보여주는 뷰(테이블의 모든 레코드에 대한 목록을 보여줌)

 path("{url}", ONLY FUNCTION), as_view()는 클래스를 함수로 만들어줌

```python
urlpatterns = [path("", {app_views}.{App-view.py Class-Name}.as_view(), name="home")]
```

### DetailView

특정 객체 하나에 대한 정보를 보여주는 뷰. 테이블에서 Primary Key로 지정된 레코드 하나에 대한 정보를 보여줌

`URLConf`에서 추출한 뷰로 넘어온 PK를 사용해 특정 레코드를 읽어올 수 있다.

```python
urlpatterns = [path("<int:pk>", views.reference_detail, name="detail")]
```



<br>

<br>

---

위 내용은 [파이썬 웹프로그래밍 - 김석훈](https://www.hanbit.co.kr/store/books/look.php?p_code=B7703021280)을 보고 정리한 내용 입니다.