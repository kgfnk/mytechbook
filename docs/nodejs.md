# node.js

- [公式](https://nodejs.org/ja/)

## 概要

サーバーサイドJavaScript実行環境

- npm(node.jsのpackage管理ツール)

## インストール

Windows
```sh
$ cinst nodejs.install
```

Mac
```sh
$ brew install node
```

CentOS
```sh
$ sudo yum install nodejs
```

### バージョン確認
```sh
$ node -v
v8.1.2
$ npm -v
5.0.3
```

## 使い方

Expressを利用した簡単なHello Worldプログラム

プロジェクト用フォルダ作成
```sh
$ mkdir project
$ cd project
```

初期化
```sh
$ npm init
package name: (project)
version: (1.0.0)
description:
entry point: (index.js)
test command:
git repository:
keywords:
author:
license: (ISC)
```
入力を促されるが全てEnterでOK。package.jsonが作成されるので後で変更。

package.json
```json
{
  "name": "project",
  "version": "1.0.0",
  "description": "",
  "main": "index.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "author": "",
  "license": "ISC"
}
```

[公式|package.json](https://docs.npmjs.com/files/package.json)

Hello World用プログラム作成

index.js
```javascript
var express = require('express');
var app = express();

app.get('/', function (req, res) {
  res.send('Hello World!');
});

app.listen(3000, function () {
  console.log('Server running at http://localhost:3000/');
});
```

```
$ npm install express --save
$ node index.js
Server running at http://localhost:3000/
```
ブラウザからアクセス
<http://localhost:3000/>

### 補足

```
project
│  index.js
│  package-lock.json
│  package.json
│
└─node_modules
```
※node_modulesは`package.json`で管理されるためバージョン管理から外すこと


## 主要なコマンド

### npm

|コマンド                            |説明                                                           |
|----------------------------------- |---------------------------------------------------------------|
|`$ npm help`                        |ヘルプ表示                                                     |
|`$ npm search [keyword]`            |パッケージ検索                                                 |
|`$ npm ls`                          |インストール済みのパッケージを表示                             |
|`$ npm install [pkgname]`           |パッケージをインストール                                       |
|`$ npm install [pkgname] --save`    |パッケージをインストールし、package.jsonへ保存する             |
|`$ npm install [pkgname] --save-dev`|パッケージをインストールし、package.jsonへ保存する(開発環境用) |
|`$ npm install`                     |package.jsonに従ってパッケージをインストール                   |
|`$ npm uninstall [pkgname]`         |パッケージをアンインストール                                   |
|`$ npm info [pkgname]`              |パッケージの情報を見る                                         |

### グローバルへのインストール

|コマンド                            |説明                                                           |
|----------------------------------- |---------------------------------------------------------------|
|`$ sudo npm ls -g`                  |グローバルへインストールされたパッケージを表示                 |
|`$ sudo npm install -g [pkgname]`   |パッケージをグローバルへインストール                           |
|`$ sudo npm uninstall -g [pkgname]` |パッケージをグローバルからアンインストール                     |

※グローバルへのアクセス`-g`は、管理者権限で行う方が良い。

## パッケージ検索

[公式](https://www.npmjs.com/)

### よく使うパッケージ

#### express

Webアプリケーションフレームワーク

[公式](http://expressjs.com/)

#### forever

デーモン起動

[node.jsスクリプトをforeverでデーモン化する](http://onlineconsultant.jp/pukiwiki/?node.js%20node.js%E3%82%B9%E3%82%AF%E3%83%AA%E3%83%97%E3%83%88%E3%82%92forever%E3%81%A7%E3%83%87%E3%83%BC%E3%83%A2%E3%83%B3%E5%8C%96%E3%81%99%E3%82%8B)
[Node.jsでforeverを使ってスクリプトの起動を永続化する - Qiita](http://qiita.com/setouchi/items/0dcc5869e7eb0ab524ea)

#### mocha

テストフレームワーク

[MochaでJavaScriptのテストを書く - CLOVER](http://d.hatena.ne.jp/Kazuhira/20160306/1457271963)

#### nock

テスト時にモックレスポンスを返す

[MochaとNockでモックサーバーを作ってレスポンスのテスト | MMMブログ](http://blog.mmmcorp.co.jp/blog/2015/11/16/nock-with-mocha/)

#### gulp

タスクランナー

[gulpを利用してmochaで書かれたテストを実行する - テノニッキ (@hideack 's diary)](http://hideack.hatenablog.com/entry/2014/10/04/195322)

#### その他

- supertest
- body-parser
- cjson
- log4js
- date-utils
- morgan
- range_check
- randomstring
- node-yaml-config


## 参考

- [npmでnode.jsのpackageを管理する - Qiita](http://qiita.com/sinmetal/items/395edf1d195382cfd8bc)
- [npmコマンドの使い方 - Qiita](http://qiita.com/yoh-nak/items/8446bf12094c729d00fe)
