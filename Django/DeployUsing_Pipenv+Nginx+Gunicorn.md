# pipenv + Nginx, Gunicorn 배포

**Virtualenv** 를 사용하는 환경이 아닌 **Pipenv**를 사용하며 배운것들을 적었다.

<br>

### 사전 작업

*자세한 방법은 하단 참고자료를 통해 확인할 수 있다*

1. gunicorn, nginx 설치

   > ec2에서 nginx 설치하기 : [CentOS 7 Nginx 설치 방법](https://holjjack.tistory.com/114)

2. gunicorn 작동확인

3. Port Redirection

<br>

## Gunicorn

### 서비스 등록 스크립트 생성

`/etc/systemd/system/gunicorn.service` 파일을 아래와 같은 내용으로 생성한다.

```
[Unit]
Description=gunicorn daemon
After=network.target

[Service]
User=ec2-user
Group=ec2-user
WorkingDirectory=/home/ec2-user/django/repo
ExecStart=/usr/local/bin/pipenv run gunicorn --workers 3 \
        <wsgi가 위치한 폴더>.wsgi:application --bind 0.0.0.0:8000

[Install]
WantedBy=multi-user.target
```

> 본래 `--bind`부분에 `unix:/home/ec2-user/django/gunicorn.sock` 를 넣어 구동하면 repo의 상위 폴더에  ` gunicorn.sock`가 생긴다.
> nginx의 proxy_pass 부분도 `http://unix:/home/ec2-user/django/gunicorn.sock`을 기재해 sock로 구성하는 것이 맞는 방법 같은데... 이 부분에 대해서는 학습이 필요하다.

<br>

### 서비스 등록

```shell
sudo systemctl start gunicorn
sudo systemctl enable gunicorn
```

<br>

### 서비스 구동 확인 

```shell
sudo systemctl status gunicorn
```

<br>

## Nginx

### 사이트 설정 추가

ec2에 nginx를 받았을 때, `etc/nginx/sites-enabled` 와 `etc/nginx/sites-availabe` 이 존재하지 않는다. 해당 경로에 없다면 만들어주고 있으면 default 파일을 삭제하자. 

```
server {
        listen 80;
        server_name <IP or 도메인>;
        charset utf-8;

        location / {
        		include proxy_params;
        		proxy_pass http://0.0.0.0:8000
        }

        location /static/ {
                root /home/ec2-user/django/repo;
        }
        
        location /media/ {
                root /home/ec2-user/django/repo;
        }
}
```

<br>

### 사이트 추가

```shell
sudo ln -s /etc/nginx/sites-available/django_test /etc/nginx/sites-enabled
```

### 기동

```shell
sudo systemctl start nginx
```

<br>

#### 기타 도움이 되는 명령어

```shell
sudo systemctl daemon-reload
sudo systemctl stop, restart nginx
ps -ef
ps
pkill gunicorn
```

<br>

<br>

---

#### 참고자료

- gunicorn [사전작업](https://wikidocs.net/6601#_7)
- [Nginx, Gunicorn, Django 연동하기](https://velog.io/@y1andyu/Nginx-gunicorn-Django-%EB%B0%B0%ED%8F%AC%ED%95%98%EA%B8%B0#3-%EC%8B%9C%EC%9E%91)
