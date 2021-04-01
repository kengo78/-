# ruby on rails コマンド
## プロジェクト開始 
***
```ruby
rails new プロジェクト名(bundleが自動で実行)
rails new プロジェクト名 --skip-bundle(bundleを後で実行)
rails new プロジェクト名 -T (Unit::Testを使わないf.check_box :Rspecを使う)
```
## モデルの生成
***
```ruby
rails generate model モデル名の単数形　フィールド名の方と並び
rails generate model Person name:string age:integer memo:text
```
## カラムの追加
***
```ruby 
rails generate migration AddカラムToモデル名の複数形　フィール名と並び
rails generate migration AddNameToPeople name:string age:integer memo:text
```

## カラムの削除
```ruby
rails generate migration RenameカラムFromモデル名の複数形　フィールド名と並び
rails generate migration RenameNameFromPeople name:string age:integer memo:text
```
## コントローラー＆ビューの生成
***
```ruby
コントローラーのみ
rails generate controller コントローラー名
コントローラー＆ビュー
rails generate controller コントローラ名　アクション名
例：users_controller.rb とindex,edit,postのビューのページが生成される
rails generate controller Users index edit post
```
## migration
```ruby
最新状態へ
rake db:migrate
リセット（データベースの中身が空っぽになるので注意)
rake db:migrate:reset
seedデータの読み込み
rake db:seed
リセット＋シードデータの読み子もい
rake db:reset
```
## Deviseの導入
***
```ruby
rails g device:install
```

## データベース作成
***
```ruby 
データベースの作成
rails db:migrate
データベースの削除
rails db:drop
rake db:migrate
rake db:text:prepare
```

## テーブルに関する操作
***
```ruby
migrationファイルを実行し、テーブルを作成する（すべてのmigrationファイルが対象）
rails db:migrate

最新のmigrationを１つdownする
rails db:rollback

migrationの状態を確認する
rails db:migrate:status
