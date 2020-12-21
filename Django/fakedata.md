## Create Test Command

Create Management Folder in Your App folder

create `__init.py__` in `management` folder

create `commands`folder in `management` folder

create `__init.py__` in `commands ` folder 

create `testCommand.py` in `commands` folder

```python
# testCommand.py
from django.core.management.base import BaseCommand
from {django-apps}.models import {models.element}


class Command(BaseCommand):
    # 가짜로 생성할 데이터와 관련된 코드
    pass
```

<br>

```shell
$ python manage.py testCommand
```

<br>

## [django-seed](https://github.com/Brobin/django-seed)

 ImageField, TextField, CharField에 맞춤형 데이터를 넣어줌

```shell
$ pip install django-seed
```



