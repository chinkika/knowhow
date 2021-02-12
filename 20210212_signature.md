#### line署名認証追加作業時のメモ ####


##### x-line-signature
- https://developers.line.biz/media/partner-docs/LINE_BOT_Development_Guidelines.pdf
- C) LINE以外からの不正リクエスト防⽌（Webhook Authentication）
- https://developers.line.biz/ja/reference/messaging-api/#signature-validation
サンプルコードがありますが、node部分のコードをそのまま持ってきただけで下記のエラーが出る
```
TypeError [ERR_INVALID_ARG_TYPE]: The "data" argument must be one of type string, TypedArray, or DataView. Received type object
    at Hmac.update (internal/crypto/hash.js:58:11)
```

- 解決方法
```
update(body) ⇒ Buffer.from(JSON.stringify(body))
```

- 参考
  - https://qiita.com/yorifuji/items/71e31baf896adb69f567
  - https://stackoverflow.com/questions/61879580/nodejs-data-argument-must-be-of-type-string-buffer-typedarray-dataview-how-to
