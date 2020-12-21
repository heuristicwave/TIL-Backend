# Form

장고의 폼 동작은 Form 클래스로 폼을 정의하고 정의된 폼을 **뷰**에서 사용하며, 최종적으로 템플릿 엔진에 의해 HTML 텍스트로 렌더링 되어 보여진다.

- 일반 폼 : Form 클래스를 상속받아 정의
- 모델 폼 : **ModelForm 클래스**를 상속받아 정의. 폼 필드의 구성을 DB 모델 정의 기반으로 폼을 정의하는 경우에 사용. **modelform_factory() 함수**를 사용해 모델 폼을 정의할 수 도 있음.
- 폼셋 : 일반 폼을 여러개 묶어서 한 번에 보여주는 폼. formset_factory() 함수를 사용해 폼셋을 정의
- 모델 폼셋 : DB 모델에 기초해서 만든 모델 폼을 여러개 묶은 폼셋. modelformset_factory() 함수를 사용해 모델 품셋을 정의
- 인라인 폼셋 : 두 모델 간의 관계가 1:N인 경우, N 모델에 기초해서 만든 폼을 여러개 묶은 폼셋. inlineformset_factory() 함수를 사용해 인라인 폼셋 정의



<br>

## [일반 폼 정의](https://docs.djangoproject.com/en/3.1/topics/forms/modelforms/#field-types)

```python
from django import forms


class LoginForm(forms.Form):

    # 모델의 EmailField 필드는 폼의 EmailField 필드로 매핑
    email = forms.EmailField()
    # 모델의 CharField 필드는 폼의 CharField 필드로 매핑
    password = forms.CharField(widget=forms.PasswordInput)
```

<br>

## 모델 폼 정의

### ModelForm 클래스 방식

장고에서 기본으로 제공하는 ModelForm 클래스는 모델에 정의한 필드를 참조해서 모델 폼을 만든다.

```python
from django import forms


class PhotoForm(forms.ModelForm):
	class Meta:
        model = Photo
        fields = ['title', 'image', 'description']
        # fields = '__all__'		# 모델에 정의된 모든 필드를 폼에 포함
        # exclude = ['decription']	# 지정한 필드만 제외하고 모든 필드를 폼에 포함
```

### 제네릭 뷰에서 폼 정의

제네릭 뷰 중 CreateView와 UpdateView는 테이블의 레코드를 생성하거나 변경하는 역할을 한다. 이 경우 모델과 폼의 특징을 동시에 갖기에 ModelForm의 기능을 내부에 포함하고 있는 제네릭 뷰이다.

```python
class PhotoCreateView(CreateView):
    model = Photo
    fields = '__all__'
```

ModelForm에서 사용하는 Meta 클래스를 사용하지 않고, model과 fields 속성만 정의해 뷰처리를 한다.

<br><br>
<br>

---

위 내용은 [파이썬 웹프로그래밍 - 김석훈](https://www.hanbit.co.kr/store/books/look.php?p_code=B7703021280)을 보고 정리한 내용 입니다.