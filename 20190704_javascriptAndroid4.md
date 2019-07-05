

#### 作業時のメモAndroid4.4.4使えない構文 ####


##### 1.letが使えない
- 対策：varに変更

##### 2.クラスが使えない
- 対策：objectへ変更
- 変更前
```
class settings{
    constructor(type, nUp, start){
      this.type = type; //1:file 0:image
      this.nUp  = nUp;  //0:1-UP 1:2-UP
      this.start= start;//-1:全ページ
    }
}
//default設定:1:file/0:1-UP/全ページ
var setting = new settings(1, 0, -1);
```
- 変更後
```
var setting = {
    type:  1,//1:file 0:image
    nUp:   0,//0:1-UP 1:2-UP
    start:-1,//-1:全ページ
};
```

##### 3.アロー関数が使えない
- 変更前
```
liff.sendMessages(createMessage()).then(() => {
    close();
});
```
- 変更後
```
liff.sendMessages(createMessage()).then(function() {
    close();
});
```


##### 4.テンプレート文字列が使えない
```
const name = 'soarflat';

console.log('My name is ' + name); // OK=> My name is soarflat
console.log("My name is " + name); // OK=> My name is soarflat
console.log(`My name is ${name}`); // NG=> My name is soarflat
```

- 上記は仕事中に出会った使えない構文、他にもありますので、下記を参考
- https://qiita.com/soarflat/items/b251caf9cb59b72beb9b
