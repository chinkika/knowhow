

#### 作業時のメモwslでvue visual studio codeデバッグ失敗 ####


##### 1.解決方法
- Error running browserasd: connect ECONNREFUSED 127.0.0.1:53885 vueプロジェクトのデバッグしたら、こんなエラーが出ていた、wslに入ってvscode用のフォルダを削除したら、解決
```
cd ~
rm -r .vscode-server
```

- wsl再起動
```
sudo shutdownがきかない
コマンドプロンプトで
wsl.exe --shutdown
```

- 参考リンク
  - https://github.com/microsoft/vscode-js-debug/issues/930
  - https://kagasu.hatenablog.com/entry/2020/01/02/155532
