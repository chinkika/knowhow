
## wordpress ##

#### ローカス環境構築 ####
- Local(旧Local By Flywheel)ツールを使って環境構築
  - macのほうがかんたん
  - Windows上ユーザーアカウントに日本語が入ってしまったら、構築失敗する可能性高い

- 一番かんたんな構築方法
  - 用意するもの、本番環境からエクスポートしたSQLファイルとwp-contentフォルダ
  - 上記二つを一個zipに圧縮
  - localにdrag&drop、次へ
  - https://yagichon.com/local-by-flywheel-backwpup/

- 構築できたら、失敗しそうなところ
  - 「view site」でローカルサイトが開けるが、「admin」でWordPress管理画面開けない「not available」が表示される
  - プラグインが影響するかも、「wp-content」したの「plugins」フォルダ名前を適当に変更して、
  プラグインを無効にした状態で、もう一回「admin」を開く、開いたらプラグインを一個ずつ有効に戻し、
  どのプラグインが影響しているのを調べる
  - 今回の場合「all-in-one-wp-security-and-firewall」が影響しているのが分かった
  - https://wp-recipe.work/how-to-deactivate-plugins-while-wordpress-whiteout#:~:text=%E3%83%97%E3%83%A9%E3%82%B0%E3%82%A4%E3%83%B3%E3%83%95%E3%82%A9%E3%83%AB%E3%83%80%E3%82%92%E5%8F%B3,%E3%81%AB%E3%83%AD%E3%82%B0%E3%82%A4%E3%83%B3%E3%81%A7%E3%81%8D%E3%82%8B%E3%81%AF%E3%81%9A%E3%81%A7%E3%81%99%E3%80%82


#### contact-form ####
- Gmailの場合
  - WP Mail SMTP
  - Gmail APIの認証情報作成方法↓↓
  https://jajaaan.co.jp/app/business-tools/wordpress-gmail-gsuite/
- 普通の場合、レンタルサーバーにメールアドレスを一個取得して、設定する
