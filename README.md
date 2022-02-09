# ダウンロード

```
git clone https://github.com/yoshiokaCB/django_vehicle_rest_api.git
cd django_vehicle_rest_api
```

# Docker image のビルド

```
docker build -t django_rest_api .
```

# Docker Image の起動とログイン

以下のコマンドを実行してコンテナを起動＆Bash でログインする。

```
docker run -it --rm -v "$PWD":/code -w /code -p 8000:8000 django_rest_api:latest /bin/bash
```

# DB 作成と初期設定

docker を起動後・ログイン後、以下のコマンドを実行して DB の作成とスーパーユーザーの登録を行う。

```
python manage.py makemigrations
python manage.py migrate
python manage.py createsuperuser
```

以下サンプル。
Email は空の状態でエンターで OK。
password は入力値によっては警告が出るが、無視して（Y）で OK。

```
Username (leave blank to use 'root'): admin
Email address:
Password:
Password (again):
The password is too similar to the username.
This password is too short. It must contain at least 8 characters.
This password is too common.
Bypass password validation and create user anyway? [y/N]: y
Superuser created successfully.
```

上記設定が終わったら、`exit` でコンテナを終了する。

# サーバー起動

設定終了後以下のコマンドでサーバー起動

```
docker run -it --rm -v "$PWD":/code -w /code -p 8000:8000 django_rest_api:latest \
/bin/bash -c "python manage.py runserver 0.0.0.0:8000"
```

http://localhost:8000/admin にアクセスして先ほど作成した superuser でログインできることを確認する。
