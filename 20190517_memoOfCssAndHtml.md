

#### CSS/HTML/JavaScript作業時のメモ ####


##### 1.flexボックスの使用
```
display: flex
flex-direction: column(縦の時設定)
flex: 1
```
- 伸ばさない要素はwidthを指定(二個以上の場合設定幅設定しなくてよい)
- 幅を伸ばす要素はflex: 1を指定(残りの幅を全部与える意味)
- 上記二要素の親にはdisplay: flexを指定
- https://qiita.com/hashrock/items/939684b9207dbab1d59e
- https://liginc.co.jp/web/html-css/css/21024(justfy-content込)


##### 2.inline-block、いくつかのinput枠を揃える
```
<label for="title" >title:</label>
・・・
<label for="username">username:</label>
・・・
label{
    display: inline-block;
    text-align: right;
    vertical-align: top;
}
```
- https://blog.csdn.net/GorgeousChou/article/details/79685139
- https://www.jb51.net/html5/172213.html


##### 3.ダブルタッチ拡大禁止
```
htmlの<head>の最初に下記を追加：
<meta name="viewport" content="width=device-width, initial-scale=1.0, minimum-scale=1.0, maximum-scale=1.0, user-scalable=no">
```
- https://qiita.com/102Design/items/1cfc04b405bf8787474a


##### 4.金額三桁カンマ入り
```
  function removeComma(strVal){
    // 空の場合0返却
    if (strVal == ''){
      return 0;
    }else{
      //カンマを外す(gは全体、なければ一個目のみ置換え)
      return strVal.replace( /,/g , "" );
    }
  }

  function addComma(numVal) {
    // 空の場合そのまま返却
    if (numVal == ''){
      return '';
    }
    // 3桁カンマ区切りへ
    return numVal.toString().replace(/\B(?=(\d{3})+(?!\d))/g, ',');
  }
  ★メタ文字の意味
    \B : 単語の境界以外の位置
    (?=AAA) : AAAという文字列の直前の位置を表す肯定の先読み
    (?!AAA) : AAA*ではない文字列の直前の位置*を表す否定の先読み
    \d : 1個の半角数字(0123456789)
    (pattern) : グループ化 括弧内の文字列をひとつの塊として扱う
    {n} : 文字の個数を指定する
    + : 直前の文字が1文字以上

  ★要素への分解
    \B : 空白やカンマ、ピリオド、改行などの前後をマッチの対象から除外する
    (?=) : 位置にマッチさせる
    (\d{3})+ : 半角数字3つが一つ以上続く範囲にマッチさせる
    (?!\d) : 数字以外の文字の直前を指定することで、空白やカンマ、ピリオド、改行などの直前から(数字の後ろの方から)マッチさせる
  ```
- https://webllica.com/add-comma-as-thousands-separator/
- https://qiita.com/hikey/items/8f8b13ba4942377a5754


##### 5.JavaScript内にhtml設定(ajax)
```
function getHistory(id){
  $.ajax({
    url: '<%=baseURL%>/XXX/XXX/history',
    type: 'POST',
    data: {
      'user': id,
    },
    timeout: 10000
  }).done(function(historys){
    console.log(historys);
    if(historys && historys.length > 0){
      const area = $('#historyArea');
      historys.forEach(function(history){
        const record = $('<div class="historyRecord"></div>');
        const data = $('<div class="historyData"></div>');
        const price = $('<div class="historyPrice"></div>');
        const title = $('<div class="historyTitle"></div>');
        const date = $('<div class="historyDate"></div>');
        const payment = history.payment_type == 1 ? 'charge' : 'pay';
        const priceMinus = history.payment_type == 1 ? '' : '-';
        title.text(history.place + ' : ' + payment);
        const objDate = new Date(history.create_date);
        const dateStr = objDate.getFullYear() + '-' + fillingZero(objDate.getMonth() + 1) + '-' + fillingZero(objDate.getDate()) + ' ' + fillingZero(objDate.getHours()) + ':' + fillingZero(objDate.getMinutes());
        date.text(dateStr);
        const priceStr = priceMinus + addComma(history.price);
        price.append('<img src="<%=baseURL%>/images/1.jpg" alt="">');
        price.append('<p class="priceStr">' + priceStr + '</p>');
        data.append(title);
        data.append(date);
        record.append(data);
        record.append(price);
        area.append(record);
      });
    }
  });
}
function fillingZero(value) {
  return ("0" + value).slice(-2);
};
```
- https://qiita.com/zakiyamaaaaa/items/bdda422db2ccbaea60d9
- https://qiita.com/hisamura333/items/e3ea6ae549eb09b7efb9
- promise:http://liubin.org/promises-book/


##### 6.ポップアップメニュー/画像保存禁止
```
body{
-webkit-touch-callout: none;
-webkit-user-select: none;
}
img{
pointer-event: none;
}
```
- https://www.tam-tam.co.jp/tipsnote/html_css/post15170.html


##### 7.サイズを指定時のpx/rem/%
- https://qiita.com/39_isao/items/e8242901ba1aadb75676


##### 8.画像を上下中央に配置
- vertical-align:middle効かない時、spanで上下で挟んでflexを使用

```
<div id="inputClear" onclick="onInputClear()"  disabled="disabled">
  <span class="center"></span>
  <img src="<%=baseURL%>/images/clr.jpg" alt="" class="clr">
  <span class="center"></span>
</div>

/*css*/
img.clr{
  width: 1rem;
  margin-left: 10px;
  pointer-events: none;
 }
 .center{
   flex: 1;
   padding: 0.5rem;
 }
 #inputClear{        
  display: flex;
  flex-direction: column;
}
```

##### 9.radio/checkboxテキストと一緒に
```
<label for="left" class="subSelectItem">
  <input id="left" type="radio" name="order" value="1" checked>左
  <img src="../images/l.png" alt="" class="img">
</label>
<label for="right" class="subSelectItem">
  <input id="right" type="radio" name="order" value="2">右
  <img src="../images/2.png" alt="" class="img">
</label>

var elements = document.getElementsByName("order");
for (var i="", i=elements.length; i--; ){
  if(elements[i].checked){
    set = elements[i].value;
  }
}
```
- 選択項目と文字グループ選択(label使用)：http://www.1uphp.com/con1/form/label.html
- http://www-creators.com/archives/2386
- https://web-designer.cman.jp/html_ref/abc_list/input_radio/
- radio値を取得：https://lab.syncer.jp/Web/JavaScript/Snippet/30/

##### 10.クラス
- https://developer.mozilla.org/ja/docs/Web/JavaScript/Reference/Classes

##### 11.文書が長い時、・・・で省略表示(20190529)
セル幅の最大幅を200pxと決めて、それ以上になる文字列は省略する場合
```
.title {
    max-width: 200px;
    overflow: hidden;
    text-overflow: ellipsis;
    white-space: nowrap;
}
```
- https://qiita.com/tksnino/items/4cf63bd1fc86a69daba0

##### 12.ファイル構成(20190529)
```
<html>
  <head>
    <title>XXX画面</title>
    <script src="https://d.line-scdn.net/liff/1.0/sdk.js"></script>
    <script src="https://ajax.googleapis.com/ajax/libs/jquery/3.3.1/jquery.min.js"></script>
    <script type="text/javascript">
    </script>
    <style type="text/css">
    </style>
  </head>
  <body>
  </body>
</html>
```

##### 13.アイコンや画像など均等に配置する時(20190603)
- justify-content：space-aroundを使用
- https://xn--web-oi9du9bc8tgu2a.com/css-basis-flex/
- https://developer.mozilla.org/ja/docs/Web/CSS/justify-content


##### 14.画面サイズ変わった時のcss設定(20190603)
```
@media screen and (max-width: 767px) {}
@media screen and (max-width: 959px) {}
```


##### 15.html中にscriptを挟む時(20190603)
- getFullYearすべてのブラウザーで対応
```
<div class="CopyRignt">(C) 
  <span id="lblYear">
    <script type="text/javascript" language="JavaScript"><!--
    TYnow = new Date();
    document.write( TYnow.getFullYear() );
    --></script>
  </span> XXX CORPORATION</div>
</div>
```
- http://www.openreference.org/articles/view/191


##### 16.input入力を数字限定、入力後キーボードを隠す(20190613)
```
<!-- 数字正規表現[\d] -->
<input type="text" onkeyup="this.value=this.value.replace(/[^\d]/g,'')" placeholder="数字のみ">
```
- https://blog.csdn.net/redwolfchao/article/details/84973177
- https://mseeeen.msen.jp/javascript-blur-and-focus-with-buttons/

##### 17.文字と画像の中央配置(20190719)
```
.img{//画像のスタイルシートに下記を追加
vertical-align: middle;
}
```
- https://www.jianshu.com/p/398629d9f3d2


##### 18.タグa　リンクと画像の間改行したら画像の右下に線が出る(20190822)
```
<a href="#">
    <img src="sample.jpg">
</a>
解決方法：改行をなくす
<a href="#"><img src="sample.jpg"></a>
```
- https://giniland.com/html画像の右下に下線を消す方法/


##### 19.ios上CSSが効かない(20191222)
```
nav.open ul li a {
    margin-left: 13px;
    color: inherit;
    text-decoration: none;
    display: block;
    font-size: 15px;
    line-height: 1.8;
}
解決方法：下記を追加
-webkit-appearance: none;
```


##### 20.safari上設定された▶アイコンが表示されず、標準アイコンに変わった(20191223)
```
nav.open ul li a:before {
    content: "\25B6";
    color: #1da1f2;
}
解決方法：\FE0Eを追加
nav.open ul li a:before {
    content: "\25B6 \FE0E";
    color: #1da1f2;
}
```
- https://stackoverflow.com/questions/40630952/how-i-can-prevent-safari-on-ios-to-replace-triangle-with-ios-ui


##### 21.flexbox指定位置で改行したい(20191223)
- まずflexboxの設定として上下両端に合わせと左右両端に合わせにより四隅に配置されるように準備します。
```
.container {
  align-content: space-between;
  justify-content: space-between;
}
```
- 次に幅100%のダミー要素を用意することで、いつでも溢れて改行されるように準備します。
```
.container::after {
  content: '';
  width: 100%;
}
```
- 最後に折り返したい個所のorderを変更します。今回では3番目と4番目を1にします。
```
.box:nth-child(n+3) {
  order: 1;
}
```
- 以上により、order: 0としては.box_1、.box_2、.container::after、次にorder: 1として.box_3、.box_4の順になります。
そのため、１段目に.box_1と.box_2、２段目に.container::after、３段目に.box_3と.box_4が配置されるため、各ボックスが四隅に配置されることになります。
- https://ja.stackoverflow.com/questions/34331/flexboxで-1行に並ぶボックスの数を指定したい
- https://blog.8bit.co.jp/?p=16162
- https://qiita.com/junara/items/dd9f34a4f2baccf58b89


##### 22.閉じるボタンを一番上にかぶせる(20191223)
- まずflexboxの設定として上下両端に合わせと左右両端に合わせにより四隅に配置されるように準備します。
```
#storeDetailArea {
    border-top: 0px solid #DBDBDB;
    border-bottom: 0px solid #DBDBDB;
}
#storeDetailClose {
    width: 44px;
    height: 44px;
    float: right;
}
解決方法：外枠にposition: relative追加、中の閉じるボタンにposition: absoluteを設定
#storeDetailArea {
    border-top: 0px solid #DBDBDB;
    border-bottom: 0px solid #DBDBDB;
    position: relative;
}
#storeDetailClose {
    position: absolute;
    height: 44px;
    width: 44px;
    right: 0px;
    top: 0px;
}
```
- https://saruwakakun.com/html-css/basic/relative-absolute-fixed


##### 23.iPadOSでフォントサイズが変わる(20201113)
- safariでfont-size指定したが、デベロッパーツールで計算済みのスタイルを見ていたら、
勝手に変わる場合がある
- 対策：bodyにtext-size-adjust: none;を設定すると解決
```
text-size-adjust: none;
-webkit-text-size-adjust: none;
```
- https://qiita.com/murs313/items/20eeb63bb3e2c98fc737
- https://developer.mozilla.org/ja/docs/Web/CSS/text-size-adjust


##### 24.ボタン等無効に設定したい(20201120)
```
有効
$("#rbIptButton").prop("disabled",false);
有効
$("#rbIptButton").prop("disabled",true);
取得&判定
if($("#rbIptButton").prop("disabled")==true)
```
- https://www.sejuku.net/blog/44465
- https://qiita.com/ponsuke0531/items/ed8dc7991311a9a2a5a7


##### 25.chrome保存されたパスワードの自動入力を無効に(20201124)
```
autocomplete="new-password" による自動入力を抑止
```
- https://developer.mozilla.org/ja/docs/Web/Security/Securing_your_site/Turning_off_form_autocompletion


##### 26.正規表現(20201124)
```
fileName.match(/[\\\/:\*\?"<>\|%&]/) 
password.match(/^[a-zA-Z0-9!"-/:-@¥[-`{-~]+$/)
```
- https://qiita.com/grrrr/items/0b35b5c1c98eebfa5128


##### 27.正規表現(20201210)
```
ラジオボタンが無効に設定された時(disabled=true)、iOS端末でラジオボタンの上部が少し切れているように見える
回避策：
input[type="radio"] {
    -ms-transform: scale(1.5); /* IE 9 */
    -webkit-transform: scale(1.5); /* Chrome, Safari, Opera */
    transform: scale(1.5);
}
```
- http://www.htmq.com/css3/transform_scale.shtml
