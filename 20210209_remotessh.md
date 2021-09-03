
## visualstudio codeでリモートSSH ##

#### 一段SSH ####
- クライアント側で公開鍵作成
```
$ ssh-keygen -C "comment"
# -C はコメント(任意)
Generating public/private rsa key pair.
Enter file in which to save the key (/Users/test/.ssh/id_rsa):
# 生成される鍵のファイル名の指定(任意)
Enter passphrase (empty for no passphrase):
# 鍵へのパスワード(任意)
Enter same passphrase again:
```

- 公開鍵をサーバーに登録
```
$ mkdir ~/.ssh
$ chmod 700 ~/.ssh
$ cat id_rsa.pub >> ~/.ssh/authorized_keys
$ chmod 600 ~/.ssh/authorized_keys
```

- visualstudio code remote SSHプラグインをインストール、configファイルに下記を記載
```
Host     work
HostName work/ipアドレス
User     ***
```


#### 多段SSH ####
```
Host           step
HostName       step/ipアドレス
port           22
User           ***
IdentityFile   ~/.ssh/id_rsa

Host           work
HostName       work/ipアドレス
User           ***
IdentityFile   ~/.ssh/id_rsa
ProxyCommand   C:\Windows\System32\OpenSSH\ssh.exe -l %r -o StrictHostKeyChecking=no -o UserKnownHostsFile=/dev/null step/ipアドレス  -W %h:%p
#ProxyCommand  ssh -CW %h:%p step
```

- 参考
- https://qiita.com/lasta/items/41e95a2fdded18c34dae
- https://www.suzu6.net/posts/205-ssh-config-proxycommand-windows10/



#### 下記エラー出た時解決方法 ####
```
Bad owner or permissions on
kex_exchange_identification: Connection closed by remote host
```
- 解決方法：C:\Users\ユーザー名の下の.sshフォルダを消す
- 参考
- https://qiita.com/kure/items/3a5dc31c8bf0b0eb2f1b
