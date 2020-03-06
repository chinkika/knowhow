

#### 作業時のメモPostgreSQL ####


##### 1.postgreSQL期間絞って検索
- 登録が二週間以上のユーザーを削除したい場合
```
DELETE FROM pub.tmp_users WHERE regist_date < now() - interval '2 weeks';
↑↑2 weekを'2 months'、'3 days'に置き換えれば期間変更可能
```

- 具体的な期間を絞りたい場合
```
SELECT * FROM member
WHERE updated_at > '2020-03-05'
WHERE updated_at > '2020-03-05'
```
- https://mask.hatenadiary.com/entry/2015/02/09/210511


##### 2.postgreSQLで接続
```
psql -h ホスト名 -p ポート番号 -U ロール名 -d データベース名
ポート番号がない場合
psql -U ロール名 -h ホスト データベース
```
- https://www.dbonline.jp/postgresql/connect/index2.html


##### 3.postgreSQLのコマンド
```
\dt　→データ型一覧
\l　 →仕様可能なデータベース一覧
\q　 →postgreSQLから切断、exit
```
- https://www.dbonline.jp/postgresql/connect/index5.html

##### 4.postgreSQL文
- 基本sqlと同じな書き方
```
select count(*) from tmp_users where regist_date < now() - interval '2 week';
↑登録が二週間以上のユーザーのトータル人数
select * from tmp_users order by regist_date asc;
↑最も古いユーザーを調べる為時間でsort(ASC/DESC)
```

- postgresqlの使い方：https://www.dbonline.jp/postgresql/
