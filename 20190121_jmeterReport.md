

#### jmeter でHTMLレポートを作成 ####


- テストからレポート生成
```
jmeter -n -t <test JMX file> -l <test log file> -e -o <Path to output folder>
例：jmeter -n -t "test.jmx" -l log.csv -e -o ./output
```
※非GUIモードでtest.jmx実行してテスト結果をlog.csvに保存し、htmlのレポートはoutputフォルダの中に「index.html」が生成されます。


- テスト実施済み、cvsファイル有る場合のレポート生成
```
jmeter -g <log file> -o <Path to output folder>
例：jmeter -g log.csv -o ./output
```
※既にある結果ファイルlog.csvからレポート生成、outputフォルダの中「index.html」が生成されます。
※コマンド実行でエラーが表示される場合、エラーメッセージに合わせてpropertiesファイルを変更する


- 参考リンク
  - https://jmeter.apache.org/usermanual/generating-dashboard.html
  - https://www.cnblogs.com/guanfuchang/p/7844981.html
