

#### GoogleAnalytics追加 ####


- headタグの一番先頭に追加

```
<head>
  <!-- Global site tag (gtag.js) - Google Analytics -->
  <script async src="https://www.googletagmanager.com/gtag/js?id=GA_TRACKING_ID"></script>
  <script>
   window.dataLayer = window.dataLayer || [];
   function gtag(){dataLayer.push(arguments);}
   gtag('js', new Date());
   gtag('config', 'GA_TRACKING_ID');
  </script>
※GA_TRACKING_IDはGAアカウントの設定を見てみる、環境によってトラキングIDが違う。
```

- 共通に使用したいなら、jsファイルにする
```
コール側
<script src="../../common/js/GoogleAnalytics.js" type="text/javascript"></script>
コールされる側
var trID = '@tracker_id@';
const trSrc = 'https://www.googletagmanager.com/gtag/js?id=' + trackerID;
document.write('<script async src="' + trSrc + '"></script>');
window.dataLayer = window.dataLayer || [];
function gtag() {
    dataLayer.push(arguments);
}
gtag('js', new Date());
gtag('config', trID);
```

- クリックイベント追加
```
追跡したいところに追加
例：
<a href="link.html">リンク先へ</a>
<a href="link.html" onclick="gtag('event', 'click', {'event_category':'tap', 'event_label': 'linkaa', 'value':'0'});">リンク先へ</a>
```
  - カテゴリ、アクション、ラベルを任意で設定することができます、イメージとしては、カテゴリ ＞ アクション ＞ ラベル
  - 管理⇒目標、目標の設定はできますが、消すことができない、有効無効しか設定できない


- 参考リンク
  - https://anagrams.jp/blog/how-to-set-up-and-use-event-tracking-in-google-analytics/
  - https://developers.google.com/analytics/devguides/collection/gtagjs/events?hl=ja
