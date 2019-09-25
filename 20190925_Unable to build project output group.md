

#### visual studio 2017でVBビルドする時のビルドエラー  ####


##### 1.ERROR: Unable to build project output group 'コンテンツ ファイル from sharp_netprint2 (Active)
- ソリューションエクスプローラーでファイルに黄色三角びっくりマークがついているファイルの有無を確認
- あれば、削除してからリビルド


##### 2.デプロイしても画像が反映されない
- 画像がプロジェクトファイルに追加されていない
- ソリューションエクスプローラー右クリック⇒追加⇒既存の項目から追加



参考資料
- https://www.hanselman.com/blog/visualstudiomsiproblemsunabletobuildprojectoutputgroupcontentfilesfromsomewebactive.aspx
