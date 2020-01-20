

#### 作業時のメモ_Javascript で高さ幅設定 ####


##### 1.ドキュメント(ページ)のサイズ
```
// スクロールバー含ない
document.documentElement.clientWidth;
document.documentElement.clientHeight;

// スクロール含む
document.body.clientWidth;
document.body.clientHeight;
```


##### 2.（ブラウザ）ウインドウサイズを取得

```
// 垂直スクロールバー（表示されている場合）を含む、ブラウザウィンドウの ビューポート (viewport) の幅
window.innerWidth;
// 水平スクロールバー（表示されている場合）を含む、ブラウザウィンドウの ビューポート (viewport) の高さ
window.innerHeight;


// ブラウザウィンドウの外側の幅
window.outerHeight;
// ブラウザウインドウの外側の高さ
window.outerWidth;
```

##### 3.（PC・スマホなどの）画面のサイズ
```
window.parent.screen.width;
screen.width;
window.parent.screen.height;
screen.height;
```


##### 4.まとめ
![](20200120_clientWidth/20200120_clientWidth.gif)

|JavaScript|意味|現在値
|:-|:-|:-|
|screen.width|モニタサイズ(解像度)|1920
|screen.availWidth|タスクバーなどを除くモニタ有効域の幅|1920
|window.innerWidth|ブラウザ内の表示域(スクロールバーを含む)|1475
|window.outerWidth|ブラウザ表示域(ブラウザ全体の外周)|1491
|document.body.clientWidth|ブラウザ内の表示域(スクロールバーを除く)|1458
|document.body.offsetWidth|ブラウザ内の表示域(スクロールバーを除く)|1458
|document.body.scrollWidth|ブラウザ内の表示域(スクロールバーを除く)※widthを指定している場合は*1参照|1458
|document.documentElement.clientWidth|ブラウザ内の表示域(スクロールバーを除く)|1458
|document.documentElement.offsetWidth|ブラウザ内の表示域(スクロールバーを除く)|1458
|document.documentElement.scrollWidth|ブラウザ内の表示域(スクロールバーを除く)※widthを指定している場合は*1参照|1458

- 1：widthが指定されている場合、bodyの幅（スクロールで非表示部分も含む）とブラウザ内の表示域(スクロールバーを除く)の大きい方となる。


##### 4.参考になるリンク
- https://qiita.com/dokkoisho/items/2bfe259ec87c00e4bd98
- https://web-designer.cman.jp/javascript_ref/window/size/
