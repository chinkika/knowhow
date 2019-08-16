

#### Heroku+node.jsでlinebot開発環境構築(作業メモ) ####


##### 1.Herokuとは
- Paasです。linebotからのメッセージを処理して返事するAPIサーバとして利用します。(Rest APIができればHerokuじゃなくてもよい、git pushすれば勝手にデプロイされるのが楽)


##### 2.node.js
- サーバサイドでJavaScriptを動かすプログラムです。


##### 3.構築流れ
- １．lineアカウントの作成
- ２．ボットサーバーの作成(Heroku＋Node.js)
  - node.jsのインストール
  - gitのインストール
  - Herokuのアカウント作成(メールアドレス、パスワードは記号必要：https://signup.heroku.com/jp)
  - Heroku Command line interface(CLI)インストール
  - アプリケーション作成
  - Rest API


##### 4.Heroku
```
heroku login

git clone https://github.com/heroku/node-js-getting-started.git

cd node-js-getting-started

heroku create  アプリケーション名　→ Create an app on Heroku

git push heroku master　→ deploy your code

heroku ps:scale web=1　→ Ensure that at least one instance of
the app is running

heroku open　→ https://アプリケーション名.herokuapp.com/ 上でページが開ける

heroku logs --tail　→ ログを確認する

npm install　→ 必要なライブラリをインストール

heroku local web　→ ローカルサーバーを立ち上げ、curlコマンドでPOSTしてみる

git add .　→ 修正したソースをコミット
git commit -m "Add cool face API"
git push heroku master

heroku config:set SECRET_KEY="****" --app アプリケーション名　→Herokuの環境変数に情報をセット
```


##### 5.Rest API
- Webシステムを外部から利用するためのプログラムの呼び出し規約(API)の種類の一つで、RESTと呼ばれる設計原則に従って策定されたもの。
- REpresentational State Transferの略、RESTの4つの設計原則
  - セッションなどの状態管理を行わない。(やり取りされる情報はそれ自体で完結して解釈することができる)
  - 情報を操作する命令の体系が予め定義・共有されている。（HTTPのGETやPOSTメソッドなど）
  - すべての情報は汎用的な構文で一意に識別される。（URLやURIなど）
  - 情報の内部に、別の情報や(その情報の別の)状態へのリンクを含めることができる。


##### 6.ボットサーバー
- ボットサーバとして使うサーバは、Node.jsとHerokuの準備で準備したHerokuのインスタンスを使用します。
これをボットサーバとして機能するように修正していきます。必要なことは、
  - LINE Developersからチャネルの開設してChannel Secretとアクセストークンを取得
  - Heroku上のREST APIをLINE BOTのWebhookに反応できるように修正
  - LINE DevelopersでREST APIのURLをWebhookとして設定
  - 署名を検証する
    - npm install @line/bot-sdk --save　→ middlewareを使用

参照先
- https://qiita.com/TakuTaku04/items/cb71f10669a9e9cbf71b
- Heroku Dev Center：https://devcenter.heroku.com/articles/getting-started-with-nodejs#set-up
- Heroku:https://qiita.com/TakuTaku04/items/6ecc533385559f4660bd
