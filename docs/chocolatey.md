# chocolatey

- [公式](https://chocolatey.org/)
- [GitHub](https://github.com/chocolatey/chocolatey)

## 概要

Linuxのパッケージ管理ツールyumやapt-getのWindows。

### 対象

Windows 7

Windows 10 は、標準でパッケージ管理ソフトが入っている

- [Windowsでもパッケージ管理がしたい](http://dev.classmethod.jp/server-side/os/windows-packagemanagement/)

## インストール

[公式:Installing Chocolatey](https://chocolatey.org/install#installing-chocolatey)

コマンドプロンプト Or PowerShellより公式サイトに記載されているコマンドを実行  
**※管理者モードで実行する必要あり**

GUIもある模様[Chocolatey GUI をまず入れてみよう](http://hayashikejinan.com/windows/1145/)

## 使い方

コマンドプロンプトからコマンドを実行  
**※管理者モードで実行を推奨**

コマンドの省略名が利用可能
- `chocolatey` ⇒ `choco`
- `choco install` ⇒ `cinst`

### バージョン確認
```
$ choco -v
0.10.7
```

### help
```
$ choco --help
```

### 主要なコマンド
|コマンド                     |省略系               |説明                                               |
|---------------------------- |---------------------|---------------------------------------------------|
|`$ choco list`               |`$ clist`            |パッケージ一覧表示                                 |
|`$ choco list [pkgname]`     |`$ clist [pkgname]`  |パッケージ検索(alias=search)                       |
|`$ choco list -l`            |`$ clist -l`         |インストール済みパッケージ一覧表示                 |
|`$ choco info [pkgname]`     |-                    |パッケージの詳細を表示                             |
|`$ choco install [pkgname]`  |`$ cinst [pkgname]`  |パッケージのインストール                           |
|`$ choco uninstall [pkgname]`|`$ cuninst [pkgname]`|インストール済みパッケージの削除                   |
|`$ choco upgrade [pkgname]`  |`$ cup [pkgname]`    |インストール済みのパッケージをアップデート         |
|`$ choco upgrade all`        |`$ cup all`          |インストール済みのパッケージを**全て**アップデート |

パッケージ全体の更新
```
$ choco upgrade all -y
```

## アンインストール

[公式:Uninstalling Chocolatey](https://chocolatey.org/docs/uninstallation)

フォルダを削除
```
C:\ProgramData\chocolatey
```

## パッケージ検索

[公式](https://chocolatey.org/packages)

## 一括インストール

```
$ cinst packages.config
```

<iframe src="https://gist.github.com/kgfnk/a2c24db8891dae7d11a1a629ca9f75ca.pibb" width="100%" height="400" allowtransparency="true" frameborder="0"></iframe>

## 参考

- [Qiita:Chocolateyを使った環境構築の時のメモ](http://qiita.com/konta220/items/95b40b4647a737cb51aa)
