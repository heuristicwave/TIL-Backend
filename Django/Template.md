## Template

템플릿은 View로부터 전달된 데이터를 템플릿에 적용해 Dynamic 한 웹페이지를 만드는데 사용



Django에서는 여러 템플릿 엔진을 선택해 사용할 수 있다.

> Default : django.template.backends.django.DjangoTemplates



### Template Language

#### 템플릿 변수

`{{ var }}` 로 둘러 쌓여 있는 변수, 변수 혹은 객체 속성을 위치 시킬 수 있다.

#### 템플릿 테그

`{% code %}` if, for-loop 과 같은 문장부터 내부 처리 결과를 덤프하는 등 여러 용도로 사용된다.

#### 템플릿 필터

변수의 값을 특정한 포맷으로 변형하는 기능을 한다

```
# 특정 날짜 포맷으로 변경
{{ createDate|date:"Y-m-d"}}

# 문자열을 소문자로 변경
{{ lastName|lower }}

# escape 필터
{{ content|escapte }}
```

#### 코멘트

```html
{# 1 라인 코멘트 #}
 
{% comment %}  
  <div>
      <p> 여러줄 코멘트 </p>
  </div>
{% endcomment %}
```

<br>

<br>

---

위 내용은 [PythonStudy](http://pythonstudy.xyz)를 보고 정리한 내용 입니다.