
## SQLインジェクション ##

#### SQLインジェクション ####
- 弱いSQL文で、不正に修正されたSQLが実行され、DBデータが盗まれた
- (--)ダブルハイフン

#### 種類 ####
- エラーベースSQLインジェクション
- マルチプルステートメント
- unionインジェクション
- ブラインドSQLインジェクション

#### 防止策 ####
- .NET LINQ、PL/SQLなどの言語を使用する
- 構文すべての変数をエスケープ処理する
- クエリにバインド機構（メカニズム）を実装
- バリデーションチェック
- データベースサーバのログの監視／解析

- 参考リンク
  - https://www.amiya.co.jp/column/sql_injection_20200518.html
  - https://www.ipa.go.jp/security/vuln/websecurity-HTML-1_1.html
