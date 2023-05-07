## はじめに
Dockerfileやdocker-compose.ymlを編集して更新した後、イメージやコンテナに反映させるためのコマンドのメモです。
案外シンプルでした。
なお、当記事でご紹介するのはdocker-composeで複数コンテナを管理している場合のものになります。

# Dockerfileの更新を反映させる

```
docker-compose up -d --build
```
※-dオプションは、バックグラウンドで起動するオプション

docker-compose upコマンドに--buildオプションを追加しています。

通常docker-compose upを実行すると、

①Dockerイメージをbuildして、
②runが実行される

という処理が実行されますが、もし既にDockerイメージがbuildされている場合は、
②のrunだけが実行されるようになっています。
そのため、Dockerfileを更新した後にdocker-compose up -dコマンドを実行しても、
新しいDockerイメージがbuildされず、古いイメージを元にrunが実行されてしまいます。
そこで、--buildオプションを追加することで、buildとrunを一緒に実行することができるようになるのです。

# docker-compose.ymlの更新を反映させる
```
docker-compose up -d
```
※-dオプションは、バックグラウンドで起動するオプション

こちらは、普段docker-composeでコンテナを起動するコマンドと変わらないですね。
更新後のdocker-compose.ymlを元に、コンテナの再構築が行われます。
