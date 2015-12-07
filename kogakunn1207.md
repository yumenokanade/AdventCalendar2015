この記事は [Kogakuin Univ Advent Calendar 2015](http://www.adventar.org/calendars/963) 7日目です。  
体を壊してしまったので結構辛いです。
- - -  
### はじめに
  
突然ですが、みなさんはデスクトップアプリケーション作りたいなぁと思ったことはありませんか？
私はほぼ毎日思ってます。
そこで今回はデスクトップアプリケーションを作りたいと思います。
HTMLとJSを使ってアプリケーションが作成できるElectronを使う。

### 工程
まず、Node.jsをインストールしてください。  
次に
```zsh
% npm -g install electron-prebuilt
% mkdir advent
% cd advent
% npm install -y
```

するとpackage.jsonというファイルが作成されます

```json
{
  "name": "advent",
  "version": "1.0.0",
  "description": "",
  "main": "main.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "keywords": [],
  "author": "",
  "license": "ISC"
}
```
mainなのでmain.jsに書き換えます。
そしてmain.jsファイルを作成します。
```javascript
var app = require("app");
var BrowserWindow = require("browser-window");

var mainWindow = null;

app.on("window-all-closed", function() {
    if (process.platform != "darwin") {
        app.quit();
    }
});

app.on("ready", function() {
    mainWindow = new BrowserWindow({
        // ウィンドウ作成時のオプション
    });

    // index.html を開く
    mainWindow.loadUrl("file://" + __dirname + "/index.html");

    mainWindow.on("closed", function() {
        mainWindow = null;
    });
});
```

```html
<h1>Hello,World</h1>
```
これで
```zsh
% electron .
```
すると

(∩´∀｀)∩ﾜｰｲ　できた♡
<img src="https://cloud.githubusercontent.com/assets/6219262/11626561/0cd4726a-9d27-11e5-815f-ba55a1ace37e.png" width=400 title="HelloWorld">  
### .exe や.appにしたい
electron-packagerを気合いでインストールしてください。

```zsh
% electron-packager . sample --platform=darwin,win32 --arch=x64 --version=0.30.0
```

## では
今回作るのは,画面にいつでもコーガくんです！！！  
デスクトップマスコットキャラほしくないですか？ないですか？  
  
<img src="https://cloud.githubusercontent.com/assets/6219262/11626610/69536294-9d27-11e5-83b0-cb0dff854a08.png" width=200 tilte="kogakunn2>


```bash 
body{
-webkit-app-region:drag;                   
-webkit-user-select:none;
\}
<img src="画像ファイル">
```
をindex.htmlに追加します。これでステータスバーがなくても動かすことができます  
  
次に,main.jsのMainWindowに以下を追加します
```javascript
frame:false
```
これでフレームを消すことができます  

はい。これで完成です。最後に
```zsh
$ electron-packager . sample --platform=darwin --arch=x64 --version=0.30.0 --icon=images/kogakunn.icns

```
--iconは作成したアプリケーションにアイコンを設定できます。

パッケージ化したら完成です。  
<img src="https://cloud.githubusercontent.com/assets/6219262/11626608/669bbb3c-9d27-11e5-893b-ffa464391e80.png" title="icon">
  
無事にデスクトップにコーガ君が映りましたか？

誰もいらないと思いますがDLできるようにしておきます。  

### 引用/参考
- [Electronでデスクトップウィジェットを作るまで](http://qiita.com/SallyAcolyte/items/94ed26ab62b8b32b1b2c)
