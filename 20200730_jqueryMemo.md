

#### 作業時のメモ ####


##### 1.画面トップにスクロール
```
<script type="text/javascript">
$(function() {
	$('#testName').click(function() {
		$('html, body').animate({scrollTop:0},'fast');
		$('html, body').animate({scrollLeft:0},'fast');
		return false;
	});
});
</script>
```

- https://www.losttechnology.jp/WebDesign/2011/scrolltotop.html
- https://www.puzzle-web.jp/archive/1949/


##### 2.セレクトボックスios(ドラム式)/android、値変更検知イベント
```
$(function() {
  if ( navigator.userAgent.indexOf('iPhone') > 0 || navigator.userAgent.indexOf('iPad') > 0 || navigator.userAgent.indexOf('iPod') > 0 ){
    $('#selectIntonation').focusout(function () {
      // iosの場合、セレクトボックスはドラム式で、値変更検知イベントはfocusoutを使用
      iosTest();
    });
  }else if( navigator.userAgent.indexOf('Android') > 0 ){
    $('#selectIntonation').bind('change', function () {
      // androidの場合、値変更検知イベントはchangeを使用
      androidTest();
    });
  }
})
```
- 同種類のイベント:focusin,focusout,blur,change
- https://qiita.com/aruri/items/71fa2aa07c26799ce3cf
- https://kinocolog.com/ios_select/

##### 3.カタカナチェック、全角スペース、半角スペースチェック正規表現
- 全角カタカナ（空文字はOK,全角スペースはOK）
```
function kanaChecker(str){
  // 値が全角カタカナではない場合はtrueを返す
  str = (str==null)?"":str;
  if(str.match(/^[ァ-ヶー　]+$/)){    //"ー"の後ろの文字は全角スペースです。
    return false;
  }else{
    return true;
  }
}
```


- 全角ひらがなチェック（空文字はOK,全角スペースはOK）
```
// 全角ひらがなチェック
function hiraChecker(str){
  // 値が全角ひらがなではない場合はtrueを返す
  str = (str==null)?"":str;
  if(str.match(/^[ぁ-んー　]*$/)){    //"ー"の後ろの文字は全角スペースです。
    return false;
  }else{
    return true;
  }
}
```

- 空白チェック(全角スペース/半角スペース/スペース連続)
```
// 空白チェック(全角スペース/半角スペース)
function emptyChecker(str){
  str = (str==null)?"":str;
  // 空/全角スペース/半角スペースの場合trueを返す
  if(str == '' || str.match(/^\s+$/)){
    return true;
  }else{
    return false;
  }
}
```

- https://javascript.programmer-reference.com/js-check-zenkaku-katakana/
