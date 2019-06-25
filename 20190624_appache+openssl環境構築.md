
#### windows10でappache+openssl環境構築メモ ####


##### 1.appache
- 下記サイト最新のappacheをダウンロード(今回はhttpd-2.4.39-win64-VS16.zip使用)
- https://www.apachelounge.com/
- 解凍したApache24を好きなところに格納(今回はDドライブの直下)
- D:\Apache24\conf\httpd.confの下記内容を修正
```
Define SRVROOT "D:/Apache24"
↑自分の環境に合わせて修正、Apache24フォルダの格納ところ
↓下記の設定値は現状環境のパスと一致するかどうか確認
ServerRoot "${SRVROOT}"
DocumentRoot "${SRVROOT}/htdocs"
ScriptAlias /cgi-bin/ "${SRVROOT}/cgi-bin/"
```
- \bin\httpd.exeを実行してみる、エラー無し、ブラウザーで「It works」表示されればOK
- コマンドプロンプトを起動、httpd起動、ブラウザーでhttp://localhostを実行も同じ

##### ２.openSSL
- Windows上でhttps://～でローカルPCのファイルにアクセスできるようにするためには、
Apacheに同梱されているopenssl.exeを使って秘密鍵・公開鍵・証明書を作成する必要があります。
- ①秘密鍵（server.key）の生成

```
d:\Apache24\bin>openssl.exe genrsa -out ..\conf\server.key 1024
Loading 'screen' into random state - done
Generating RSA private key, 1024 bit long modulus
...............................++++++
.............................................++++++
e is 65537 (0x10001)
```
これでd:\Apache24\confに秘密鍵（server.key）が生成されます。

- ②公開鍵（server.csr）の生成

```
d:\Apache24\bin>openssl.exe req -new -key ..\conf\server.key -out ..\conf\server
.csr -config ..\conf\openssl.cnf
Loading 'screen' into random state - done
You are about to be asked to enter information that will be incorporated
into your certificate request.
What you are about to enter is what is called a Distinguished Name or a DN.
There are quite a few fields but you can leave some blank
For some fields there will be a default value,
If you enter '.', the field will be left blank.
-----
Country Name (2 letter code) [AU]:JP
State or Province Name (full name) [Some-State]:Nara
Locality Name (eg, city) []:City
Organization Name (eg, company) [Internet Widgits Pty Ltd]:Company
Organizational Unit Name (eg, section) []:Section
Common Name (e.g. server FQDN or YOUR name) []:127.0.0.1
Email Address []:foo@bar.com

Please enter the following 'extra' attributes
to be sent with your certificate request
A challenge password []:
An optional company name []:
```
最後の「A challenge password」「An optional company name」入力しなくてもよい、
これでd:\Apache24\confに公開鍵（server.csr）が生成されます。


- ③証明書（server.crt）の生成

```
d:\Apache24\bin>openssl.exe x509 -in ..\conf\server.csr -out ..\conf\server.crt
-req -signkey ..\conf\server.key -days 365
Loading 'screen' into random state - done
Signature ok
subject=/C=JP/ST=Nara/L=City/O=Company/OU=Section/CN=127.0.0.1/emailAddress=cpitest.0002@gmail.com
Getting Private key
```
これでd:\Apache24\confに証明書（server.crt）が生成されます。


- ④httpd-ssl.confの修正

```
d:\Apache24\conf\extra\httpd-ssl.conf
…前略…
#   General setup for the virtual host
DocumentRoot "d:/Apache24/htdocs"
…後略…
```

- ⑤httpd.confの修正

```
修正前
#LoadModule ssl_module modules/mod_ssl.so
#Include conf/extra/httpd-ssl.conf
修正後
LoadModule ssl_module modules/mod_ssl.so
Include conf/extra/httpd-ssl.conf
```
修正後、Apacheを再起動します。


##### 3.ソースとmklink
- ソースをgitからダウンロード
- htmlファイルのhttps://@FQDN@をhttps://localhost:80に一括置換
- コマンドプロンプトD:\Apache24\htdocsのしたで、シンボリックリンクをhotdocsに作成
```
mklink /D (Apacheインストールディレクトリ)\htdocs\faq D:\gitclone\FAQ\faq
```
ブラウザから https://localhost/faq/ja/index.html 



- 参考リンク
  - http://www.koikikukan.com/archives/2013/12/03-012345.php
