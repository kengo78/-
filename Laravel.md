### Laravelの導入 for Windows10 
***
1. composerのダウンロード  
   PHPのパッケージ管理ツール   
   getcomposer.orgが公式サイト。  
2. php -r "unlink('composer-setup.php');"  
#### Laravelのダウンロート
3. php composer.phar create-project --prefer-dist laravel/laravel "プロジェクト名"

#### Laravelのversion確認 
***
```
php artisan --version
```
というコマンドをたたく。  
```
Could not open input file: artisan
```
と表示される。   
これは、コマンドをたたくディレクトリが違う可能性が高い。Laravelアプリのホームディレクトリでたたく。   

#### アプリの設定
***
アプリの設定は、.envファイルとconfigファルダの中のファイルを作る。  
.envファイル、環境に依存するような設定値を書く。  
configフォルダにあるファイルから、.envファイルに書かれた値を参照する。    
こうすると、環境が変わった時に.envファイルの変更だけでよい。  
.envファイルの設定  
Timezone→'Asia/Tokyo  
locale 'ja'

#### モデルの生成
***
```
php artisan make:model Post --migration
```

#### データの挿入
***
```
php artisan tinker
```
'モデル名'::all()->toArray();
データベースにあるデータを配列で表示
'モデル名'::create([中身]);
```
Post::create(['title'=>'title 2','body'=>'body 2']);
```
これだと以下のようなエラーが出る。
```
Illuminate\Database\Eloquent\MassAssignmentException with message 'Add [title] to fillable property to allow mass assignment on [App\Models\Post].'
```
これはMassAssignmentというエラーで悪意のある、データの挿入を防ぐためのもので、modelの設定を変える必要がある。   

##### IPアドレスの確認方法  
```
ipconfig
```
コンソール（Powershell）にて確認。

##### Implicit Binding

