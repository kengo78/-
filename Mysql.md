### 入門編 
****  
#### 起動コマンド  
mysql -h db -t -u dbuser -pdbpass myapp < main.sql   
#### ターミナルコマンド
ターミナルをクリアーにしたい。  
clear || control + L  
一つのデータをtable,一行一行をレコード、列をカラム呼ぶ。  
#### コマンド 
***
```SQL
CREATE TABLE ("テーブル名") (
    "カラム名" "データ型",
    "カラム名" "データ型",
    "カラム名" "データ型",
);

レコードの挿入insert
INSET INTO
    "テーブル名" ("カラム名","カラム名,...,"カラム名")
VALUES
    ('内容','内容',...,'内容');

テーブルの構造の確認  
DESC "テーブル名";

テーブルの一覧を見る
"SHOW TABLES;

テーブルの削除
DROP TABLE IF EXISTS "テーブル名";

レコードの確認
SELECT * FROM "テーブル名";
*は全部抽出を意味する。

コメントアウト
-- aaa
# aaa
/*
aaa
aaa
*/
```

SQL データベースに問い合わせをするという意味で、クエリと呼ばれる。  
クエリ、慣習的に、SQLがあらかじめ用意している命令は*大文字*、自分でつけるテーブル名やカラム名は*小文字*することが多い。  

#### データ型  
##### 数字
TINYINT(整数) -128 ~ +128  
INT -21億 ~ +21億  
BIGINT -922京　～　+922京  

TINYINT *UNSIGNED* 0 ~ 255  
INT UNSIGNED 0 ~ 42億  
BIGINT UNSIGNED 0 ~ 1844京  

DECIMAL 固定小数点 通常使う  
FLOAT 浮動小数点  
DOUBLE 浮動小数点（高精度)  
##### 文字列  
CHAR 0 ~ 255文字（固定長のデータ）
VARCHAE 0 ~ 65535文字（文字数がバラバラになるようなデータ）
TEXT それ以上　   
ENUM 特定の文字列から１つ  
SET　特定の文字列から複数  
##### 真偽値
BOOL TRUE / FALSE   
TINYINT(1) 1 / 0  
##### 日時
DATE 日付  
TIME 時間  
DATETIME 日時  
##### データがないときの処理
値を設定しなかったとき→NULL という特殊な値  
値が設定されていないとき、エラーではじきたい カラムに NOT NULLをつける   

デフォルト値を設定してあげる DEFALUT 'デフォルトの値'  
値に制限を付ける  
カラム名　INT CHECK (カラム名　=> 0 AND　カラム名　<=100) とすると  
likesには０以上１００以下の値しか設定することができない。    
重複したデータを防ぐ。  
カラム名 データ型 UNIQUEとすると、重複をはじいてくれる。   
レコードを一位に識別してくれるキー  
id INT AUTO_INCREMENT(これはPRIMARY KEY(id)とした時のみ使える。)  
```
id INT AUTO_INCREMENT

PRIMARY KEY (id);
```
idを設定るすることで、データをいじりやすくなる。    
#### データの抽出  
***
```SQL
DROP TABLE IF EXISTS posts;
CREATE TABLE posts (
  id INT NOT NULL AUTO_INCREMENT,
  message VARCHAR(140), 
  likes INT,
  PRIMARY KEY (id)
);

INSERT INTO posts (message, likes) VALUES 
  ('Thanks', 12),
  ('Arigato', 4),
  ('Merci', 4),
  ('Gracias', 15),
  ('Danke', 23); 
  
-- SELECT id, message FROM posts;

-- > >= < <=
-- SELECT * FROM posts WHERE likes >= 10;

-- = != <>(!=と同じ)
SELECT * FROM posts WHERE message = 'Danke';
SELECT * FROM posts WHERE message != 'Danke';
SELECT * FROM posts WHERE message <> 'Danke';

SELECT * FROM posts;

SELECT * FROM posts WHERE likes >= 10 AND likes <= 20;
SELECT * FROM posts WHERE likes BERWEEN 10 AND 20;
SELECT * FROM posts WHERE likes NOT BETWEEN 10 AND 20;

SELECT * FROM posts WHERE likes = 4 OR likes = 12;
SELECT * FROM posts WHERE likes IN (4,12);
SELECT * FROM posts WHERE likes NOT IN (4,12);

-- %: 0文字以上の任意の文字 前方一致
-- _:任意の一文字

SELECT * FROM posts WHERE message LIKE 't%';前方一致

 SELECT * FROM posts WHERE message LIKE BINARY 't%';前方一致 BINARYは大文字小文字区別

SELECT * FROM posts WHERE message LIKE '%su';後方一致
SELECT * FROM posts WHERE message LIKE '%i%';含む

SELECT * FROM posts WHERE message LIKE '__%';
messageが任意の１文字が２つ続いて、その次がaでその後が０文字以上の任意の文字列
→３文字目がaのレコードのみ取り出せる
SELECT * FROM posts WHERE message NOT LIKE '__a%';
３文字目がa以外のレコードが抽出できる。  
SELECT * FROM posts WHERE message LIKE  '%\_%';
SELECT * FROM posts WHERE message LIKE '%\%%';
\でエスケープすれば、%や_を含む文字列を抽出できる。

NULLの抽出条件  
SELECT * FROM posts;
SELECT * FROM posts WHERE likes != 12;
SELECT * FROM posts WHERE likes != 12 OR likes IS NULL;
SELECT * FROM posts WHERE likes IS NOT NULL;

-- 並び替え
SELECT * FROM posts ORDER BY likes;--昇順
SELECT * FROM posts ORDER BY likes DESC;--降順
SELECT * FROM posts ORDER BY likes DESC,message;--降順のアルファベット順
SELECT * FROM posts ORDER BY likes DESC,message LIMIT 3;--上位３件

SELECT * FROM posts ORDER BY likes DESC,message LIMIT 3 OFFSET 2;
SELECT * FROM posts ORDER BY likes DESC,message LIMIT 2,3;
-- 上位２件を除いて、３件分抽出。

-- 関数
SELECT 
  likes * 500 / 3 AS bonus,
  FLOOR(likes * 500 / 3) AS floor,
  CEIL(likes * 500 / 3) AS ceil,
  ROUND(likes * 500 / 3) AS round,
  ROUND(likes * 500 / 3, 2) AS round2
FROM 
  posts;

--文字列の抽出
SELECT message, SUBSTRING(message,3) FROM posts;
SELECT message, SUBSTRING(message, 3, 2) FROM posts;
SELECT message, SUBSTRING(message, -2) FROM posts;

--文字列の連結
SELECT CONCAT(message, ' - ', likes) FROM posts;
SELECT message,LENGTH(message) AS len FROM posts;
-- LENGTHは日本語に対して使うときは、CHAR_LENGTHにしないと挙動がおかしくなる。

--日時操作

INSERT INTO posts (message, likes, created) VALUES 
  ('Thanks', 12, '2020-05-01'),
  ('Merci', 4, '2020-05-03'),
  ('Arigato', 4, '2020-06-14'),
  ('Gracias', 15, '2020-07-04'),
  ('Danke', 8, '2020-08-22');

SELECT created, YEAR(created) FROM posts;
SELECT created, MONTH(created) FROM posts;
SELECT created, DAY(created) FROM posts;

SELECT 
  created,
  DATE_FORMAT(created, '%M %D %Y, %W') AS date
FROM
 posts;
SELECT 
  created,
  DATE_ADD(created, INTERVAL 7 DAY) AS next
FROM
 posts;
 
SELECT 
  created,
  NOW(),
  DATEDIFF(created,NOW()) AS diff
FROM 
  posts;

--値の更新
UPDATE posts SET likes = likes + 5 WHERE likes >= 10;
UPDATE 
  posts
SET
  likes = likes + 5,
  message = UPPER(message)
WHERE
  likes >= 10;
SELECT * FROM posts;

--レコードの削除
DELETE FROM posts WHERE likes < 10;
TRUNCATE TABLE posts;--テーブルごと削除 
INSERT INTO posts (message, likes) VALUES ('tui tui', 10);

SELECT * FROM posts;

--レコードの作成日時や更新日時を自動で設定るする方法を見ていきましょう。

DROP TABLE IF EXISTS posts;
CREATE TABLE posts (
  id INT NOT NULL AUTO_INCREMENT,
  message VARCHAR(140), 
  likes INT,
  created DATETIME DEFAULT NOW(),
  updated DATETIME DEFAULT NOW() ON UPDATE NOW(),
  PRIMARY KEY (id)
);

INSERT INTO posts (message, likes) VALUES 
  ('Thanks', 12),
  ('Merci', 4),
  ('Arigato', 4),
  ('Gracias', 15),
  ('Danke', 8);

SELECT id, created, updated FROM posts;
SELECT SLEEP(3);--3秒待機
UPDATE posts SET likes = 100 WHERE id = 1;
SELECT id, created, updated FROM posts;

--テーブルの設計の変更
ALTER TABLE posts ADD author VARCHAR(255);
ALTER TABLE posts ADD author VARCHAR(255) AFTER id ;
ALTER TABLE posts ADD author VARCHAR(255) FIRST ;
ALTER TABLE posts DROP message;
ALTER TABLE posts CHANGE likes points INT;
DROP TABLE If EXISTS messages;
ALTER TABLE posts RENAME messages;
SHOW TABLES;
```








