

#### CSS/HTML/JavaScript作業時のメモ ####


- flexボックスの使用
```
display: flex
flex-direction: column(縦の時設定)
flex: 1
```
  - 伸ばさない要素はwidthを指定(二個以上の場合設定幅設定しなくてよい)
  - 幅を伸ばす要素はflex: 1を指定(残りの幅を全部与える意味)
  - 上記二要素の親にはdisplay: flexを指定
  - https://qiita.com/hashrock/items/939684b9207dbab1d59e


- inline-block、いくつかのinput枠を揃える
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


- ダブルタッチ拡大禁止
```
htmlの<head>の最初に下記を追加：
<meta name="viewport" content="width=device-width, initial-scale=1.0, minimum-scale=1.0, maximum-scale=1.0, user-scalable=no">
```
  - https://qiita.com/102Design/items/1cfc04b405bf8787474a


- 金額三桁カンマ入り
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


- JavaScript内にhtml設定(ajax)
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


- ポップアップメニュー/画像保存禁止
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


- サイズを指定時のpx/rem/%
  - https://qiita.com/39_isao/items/e8242901ba1aadb75676


- 画像を上下中央に配置
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
