## 仮想環境構築
```
python3 -m venv env
```
## Django インストール
```
source env/bin/activate #仮想環境構築
pip install Django
```

## プロジェクト作成
```
django-admin startproject プロジェクト名 .
```

## アプリ作成
```
python manage.py startapp アプリ名
```

## サーバー立ち上げ
```
python manage.py runserver
```

## モデル作成後にすること
1. migrationファイルの作成
2. migrationファイルをもとにmigrateの実行
```
python manage.py makemigrations 
python manage.py migrate
```

## Superuserの作成
```
python manage.py createsuperuser
```
## Superuserの情報を忘れてしまったとき
```
python manage.py shell
users = User.objects.all()
user = users[0]
user
[usr_infoの表示]
user.set_password('newpass')
user.save()
```

## Djangoのマイグレーションをロールバックしたい

1. ```python manage.py showmigrations``` でマイグレーション履歴を確認
2. ```python manage.py migrate APPLICATION_NAME MIGRATION_NAME```で指定したマイグレーションファイルまで戻る
3. マイグレーションファイルの削除
### 完全に初期化したい場合
```
python manage.py migrate APPLICATION_NAME zero
```
