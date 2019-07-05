
#### batファイル作成に便利なコマンド ####


- 注釈は`::`を使用
- 情報を出力は`echo`を使用


- ディレクトリ移動する時、c/d/eドライブ考えず移動できる`/d`
```
cd /d D:\jmeter\apache-jmeter-4.0\bin
(現ディレクトリはC:\Users\chin\Desktop\test)
```
- ディレクトリ移動時、ディレクトリが簡単に取得できる
  - 例D:\jijs\bin\Test.bat

|コマンド|詳細|出力|
|:---------|:----------|:----------|
|%0|binファイル|D:\jijs\bin\Test.bat|
|%~0|全パス|D:\jijs\bin\Test.bat|
|%~f0|(file)全パス|D:\jijs\bin\Test.bat|
|%~d0|(dir)ドライブ|D:|
|%~p0|(path)パス-ドライブ無し|\jijs\bin\|
|%~n0|(name)ファイル名前|Test|
|%~x0|(exe)拡張子|.bat|
|%~s0|(Short)全パス|D:\jijs\bin\Test.bat|
|%~a0|(attribute)ファイル属性|–a——|
|%~t0|(time)ファイル修正日付|2016-06-23 17:10|
|%~z0|(Size)ファイルサイズ|696|
|%~$PATH:0|全パス|D:\jijs\bin\Test.bat|
|%~dp0|所在フォルダ|D:\jijs\bin\|
|%~nx0|ファイル全称|Test.bat|
|%~fs0|全パス|D:\jijs\bin\Test.bat|
|%~dp$PATH:0|フォルダ|D:\jijs\bin\|
|%~ftza0|ファイル全情報|–a—— 2016-06-23 17:10 696 D:\jijs\bin\Test.bat|
|%1|一個目引数||
|%2|二個目引数||
|cd /d [path]|他ドライブへ直接行ける||
- https://blog.csdn.net/jijianshuai/article/details/78833101


- 検索`findstr`
  - `/b `行首からマッチ
  - `/e `行末からマッチ
  - `/s `カレントディレクトリから検索
  - `/i `大文字小文字区別しない
  - `/?`ヘルプ
  - https://www.jb51.net/article/17848.htm


- ファイル探す`where`
  - アプリのインストール先を探せる`where java`
  - https://blog.csdn.net/grey_csdn/article/details/68938870


- 引数にデータの書き込みと読み出し
```
set TEST_CSV=log.csv
echo %TEST_CSV%
echo %JMETER_HOME%
```

- ファイル存在するかどうかの判定
  - if exist ファイル名　⇒存在判定
  - if not exist ファイル名　⇒存在しない判定


- フォルダ削除と作成
  - rmdir フォルダ名
  - md フォルダ名
  

- コマンドの実行結果を引数として使用したい
  - カレントディレクトリにあるcsvファイル名を取得して引数TEST_CSVに格納
  - パイプを使用する時、`^`を付けなければいけない
  ```
  for /F %%i in ('dir /b ^| findstr csv') do ( set TEST_CSV=%%i)
  ```


- ファイルへ保存とファイルから読み出す
  - カレントディレクトリにあるcsvファイル名を取得して引数TEST_CSVに格納
  ```
  dir /b | findstr csv > tmp.txt
  set /p TEST_CSV=<tmp.txt
  del tmp.txt
  ```

- batファイル例

```
set TEST_PATH=%~dp0
set JMETER_PATH=%JMETER_HOME%\bin

echo %TEST_PATH%
echo %JMETER_PATH%

::CSVファイル名を取得してTEST_CSVに保存しておく
for /F %%i in ('dir /b ^| findstr csv') do ( set TEST_CSV=%%i)
echo %TEST_CSV%

::テスト用フォルダに移動(パッチとCSVのあるフォルダ)
::既に生成されたoutputフォルダがあれば削除しておく
cd /d %TEST_PATH%
if exist output (rmdir /S /Q output)

::CSVファイルをjmeter作業フォルダにコピー
::こちらの例としては、環境変数JMETER_HOME=D:\jmeter\apache-jmeter-4.0
copy /y %TEST_CSV%    %JMETER_PATH%

::jmeterフォルダにoutputフォルダがあれば削除しておく
cd /d %JMETER_PATH%
if exist output (rmdir /S /Q output)

::テスト用フォルダにレポートを生成する(パッチとCSVのあるフォルダ)
jmeter -g %TEST_CSV% -o %TEST_PATH%\output
```


- 参考リンク
  - https://jmeter.apache.org/usermanual/generating-dashboard.html
  - https://www.cnblogs.com/guanfuchang/p/7844981.html
