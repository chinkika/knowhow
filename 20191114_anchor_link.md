

#### 作業時のメモ　アンカーリンク ####


##### 1.ページ内リンク
```
html：
<a id="name" class="anchor"></a>

css:
a.anchor{
    display: block;
    padding-top: 70px;
    margin-top: -70px;
}
※display: blockが肝
※paddingをmarginで打ち消すような感じで、+と-で同じ数字を入れる
```

- https://y-com.info/contents/?p=5641
- http://www2.otani.ac.jp/fkdsemi/css_oyo/link_hannou/link_hannou.html
- http://www6.plala.or.jp/go_west/nextcss/column/tech/sidemenu.htm

##### 2.アンカーリンクずれる
```
<script>
$(window).on('load', function() {
    var hash = window.location.hash;
    var position = $(hash).offset().top;
    function scroll(position){
      $('html, body').animate({
        scrollTop : position
      }, 100);
    }
    scroll(position);
  });
</script>
```

- https://entrys.jp/html5/column/2289/

##### 3.疑似要素を使う
```
#ターゲット要素::before {
    content: "";
    display: inline-block;
    height: 50px;
    margin-top: -50px;
    vertical-align: top;
}
```
- https://www.tomotanuki.com/entry/web-in-page-link-fixed

##### 4.他参考リンク
- https://mdstage.com/html-css/html-intermediate/anchor#section6
- https://kumiko-jp.com/archives/215120.html
