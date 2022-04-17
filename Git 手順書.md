## Git main ブランチ作成とリモートレポジトリへのpush
1. githubにてレポジトリを作成
2. 追加したファイルがある階層へと移動する
```
echo '# Django_boardapp' >> README.md(なくてもよい)
git init
git add -A(-Aは全ファイル追加、二回目以降は差分のみ追加される、ファイル名を指定するとそのファイルの差分のみ追加)
git status で状態を確認(しなくてもよい)
git commit -m 'First commit'
git branch -M main (マスターブランチの設定)
git remote add origin 追加したいレポジトリのURL(例:https://github.com/kengo78/Django_boardapp.git)
git push -u origin main
```
## 開発用ブランチにMainブランチの最新コードを取り込む
1. mainブランチへ移動
```
git checkout main
```
2. git pullでmainブランチを最新にする
```
git pull origin main
```
3. 開発用ブランチを作成し移動
```
git branch develop(ブランチ名)
```
4. merge コマンドでmainブランチの内容を取り込む
```
git merge main
```
5. 取り込んだものをリモートにpush
```
git push origin 開発用ブランチ名
```

## ローカルのリモートブランチを最新化
```
git fetch
```

### ブランチの削除
```
git branch -d 指定ブランチ
'''
## 開発現場でのgit pushの利用例
1. 機能追加/修正対応するGitHubのIssue作成
2. Issueに対応する作業ブランチ作成
3. 作業完了後に作業ブランチをGitHubへpush（←この段階でgit pushを使用します。）
4. GitHub上の作業ブランチからプルリクエストを作成
5. プルリクエストをmasterブランチにmerge

## mainブランチからほかのブランチへの反映手順
1. 対象のGitレポジトリの管理ディレクトリへ移動する
2. 開発用ブランチに切り替える
```
git checkout 開発用ブランチ
```
3. mainブランチから開発用ブランチへマージする
```
git merge origin main
```
