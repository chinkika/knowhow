

#### 作業時のメモ ####


##### 1.iPhoneX系端末横画面文言がノッチと被る対応
- 対策：「iPhone X」独自の仕様「Safe Area（セーフエリア）」
- 「viewport-fit=cover」を追加すると、画面いっぱい（100%）になる
- 「iOS 11.1」と「iOS 11.2」以降で異なる対応方法(env)
```
<meta name="viewport" content="width=device-width,initial-scale=1.0,user-scalable=no,viewport-fit=cover">

  body{
    padding-right:  constant(safe-area-inset-right);
    padding-left:  constant(safe-area-inset-left);
    padding-right:  env(safe-area-inset-right);
    padding-left:  env(safe-area-inset-left);
  }
```


- 参考リンク
- https://youtachannel.com/support-iphone-x-safe-area/
- https://medium.com/@onotakehiko/iphone-x-%E3%81%AE-safari-%E3%81%AB%E3%81%8A%E3%81%91%E3%82%8B-web-%E3%82%B3%E3%83%B3%E3%83%86%E3%83%B3%E3%83%84%E3%81%AE%E8%A1%A8%E7%A4%BA-58da5f503d0b
- https://qiita.com/keeey/items/c175bd8ef12ee65ac3fc


##### ２.横画面対応
- 縦横分けて書く
```
  @media (orientation: landscape) {
    body {
      flex-direction: row;
    }
  }

  @media (orientation: portrait) {
    body {
      flex-direction: column;
    }
  }
```

- 参考リンク
- https://developer.mozilla.org/ja/docs/Web/CSS/@media/orientation
