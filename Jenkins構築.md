### Jenkins構築(gitlab)

##### １．運用環境
|項目|環境|
|:-|:-|
|PC|Mac mini（late2014)|
|OS|10.13.3macOS High Sierra|
|Xcode|9.4|
|Appium|1.9.0|
|iphoneSE|iOS11.4.1(15G77)|
|AQUOS|Android8.0.0|


##### ２．インストール方法
- 前提条件はJavaをインストールしておく
- 方法１：下記リンクからパケージをダウンロードしてインストール
  - https://jenkins.io/

- 方法２：brewでインストール
  - 下記コマンドでインストール
  ```
  $ brew install jenkins
  ```
  - 下記コマンドで起動
  ```
  $ java -jar /usr/local/opt/jenkins/libexec/jenkins.warもしくは
  $ brew services start jenkins
  ```
  - ブラウザを起動し、以下のURLを入れるとjenkins表示
  http://localhost:8080/


- 初回起動時にパスワードを入力して一個管理者権限のアカウントを作成
- オススメのプラグインをインストール
- 作成したアカウントでログイン

##### ３．JOB作成方法
- JOB作成前自分にとって必要なプラグインをインストール
  - jenkinsの管理→プラグインの管理を開く
    - GitLab Plugin
    - Git Plugin
    - Multiple SCMs plugin(２個以上のブランチクローンする時別のフォルダーに入れたい時便利)
    - Parameterized Trigger plugin(上下流JOBの間トリガを設定する時使う)
    - Slack Notification(結果をslackへ通知する時便利)
    - Xcode integration(iOSビルド時に使う)
  - 必要なプラグインにチェックを入れる→「再起動せずにインストール」
  - Webブラウザで下記を入力してjenkins再起動
  http://localhost:8080/restart


- gitlabの認証情報をjenkinsに設定しておく
  - access tokensの設定
    - gitlab開く→自分アカウントのsetting→access tokens→まだ未作成の場合一個個人用のトークンを作成
    ![](assets/markdown-img-paste-1.png)
    - jenkinsの管理→システムの設定→gitlab設定するところ→上記生成したAPIトークンを追加
    ![](assets/markdown-img-paste-2.png)

  - ssh認証鍵の設定
    - 下記コマンドでssh認証鍵を作成、公開鍵と秘密鍵がある
  ```
  $ ssh-keygen -t rsa -C "<macJenkinsUser>" -b 4096
  ```
    - ~/.ssh/の下に下記の二個ファイルが生成される
      - `id_rsa→秘密鍵`
      - `id_rsa.pub→公開鍵`
    - gitlab開く→自分アカウントのsetting→ssh keys→keyのところに上記の`公開鍵`を記入→add key
    ![](assets/markdown-img-paste-3.png)
    - jenkins開く→認証情報→認証情報の追加
      - 種類：SSHユーザー名と秘密鍵
      - スコープ：グローバル
      - ユーザー名：自分なりにわかりやすい名前
      - 秘密鍵：直接入力→上記の`秘密鍵`をコピペ
    ![](assets/markdown-img-paste-4.png)

- 新規ジョブ作成(必要に応じて項目設定)
  - フリスタイル
  - パイプライン

##### ４．構築中出会った問題に関する色々メモ
- ①複数のブランチをクローンする時同じフォルダになり、みにくい時
  - ジョブのソース管理のところ→追加の処理→check out to a sub-directory→サブフォルダを作成
  ![](assets/markdown-img-paste-5.png)
- ②ビルド・トリガ
  - gitlabのpushでビルドを起すに必要なwebhookは、jenkinsサーバー外部公開しないと通信できない
- ③周期ビルドのスケジュール設定
  - 記入仕方：`* * * * *`
  - 1個目の*は分、０〜５９
  - 2個目の*は時間、０〜２３
  - 3個目の*は日、１〜３１
  - 4個目の*は月、１〜１２
  - 最後の*は週、０〜７、０と７は全部日曜日の意味
  - 例：H/5 * * * *　→5分毎に実行
  - 例：H 2 * * *　→毎日2時実行
- ④shellスクリプト
  - $?：前回コマンド実行結果
  - if [ -f ファイルパス ]:ファイル存在を判断
  - curDateTime=date +%Y-%m-%d,%H:%M:%S：現在時間取得
  - echo $cnt > cnt：引数をファイルに保存
  - echo "今回実行時間:${runSecond}s" > runtime：文字と引数同時表示したい場合
  - mkdir -p フォルダ名：フォルダ存在の場合は無視
- ⑤jenkinsでコマンド実行権限がない場合の対処方法
  - jenkinsユーザーにsudo権限を付け、パスワード入力不要に設定変更
    - 下記のファイルをroot権限で開く   
    ```
    $ sudo visudo
    ```
    - 下記修正を加え、保存して閉じる
    ```
    Defaults:jenkins  !requiretty
    jenkins          ALL=(ALL)       NOPASSWD: ALL
    ```  
  - 上記方法で効かない場合、下記変更でコマンド実行権限をsudoにしてみる(欠点はパスワードをスクリプトに記入することで見られてしまう)
    ```
    mv fileA fileB → echo ユーザーパスワード |sudo -S mv fileA fileB
    ```
- ⑥gitlabブランチの変更履歴を取得するためのコマンド
```
git log -p -1(←数字の意味は表示する履歴の個数、1は最新の一個を表示)
```
- ⑦gitでソース管理用の基本コマンド
```
git status →変更点を表示
git add . →修正ファイルを追加
git commit -am ‘message’ →修正ファイルをメッセージ付でコミット
git push origin master →masterブランチにpush
```

##### 参考資料
- JenkinsとGitLabを連携
  https://qiita.com/takamii228/items/3598f403518c296f93f3
- 環境構築日本語
  http://toriaezu-engineer.hatenablog.com/entry/2016/11/19/104432
- 環境構築中国語
  https://blog.csdn.net/ruangong1203/article/details/73065410
- 秘密鍵
  https://www.cnblogs.com/milton/p/5761215.html
- Jenkinsにsudo
  https://qiita.com/kokoyoshi/items/dc38195472129b544348
- シェルスクリプト
  https://qiita.com/zayarwinttun/items/0dae4cb66d8f4bd2a337
- gitコマンド日本語
  https://git-scm.com/book/ja/v1/Git-%E3%81%AE%E5%9F%BA%E6%9C%AC-%E3%82%B3%E3%83%9F%E3%83%83%E3%83%88%E5%B1%A5%E6%AD%B4%E3%81%AE%E9%96%B2%E8%A6%A7
- git logコマンド中国語
  https://www.cnblogs.com/bellkosmos/p/5923439.html
