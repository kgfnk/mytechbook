# samba

- [公式](https://www.samba.org/)
- [日本 Samba ユーザー会 Web サイト](http://www.samba.gr.jp/)

## 概要

CentOS 7.3 へ sambaをインストールした時のメモ

- 認証なし
- ユーザーホームを共有設定

### 対象

CentOS Linux 7.3

## インストール

```sh
$ su -
$ yum install samba
```

## バージョン確認

```sh
$ smbd -V
Version 4.4.4
```

## 設定

ユーザー・共有フォルダ追加
```sh
$ useradd samba
$ passwd samba

$ chmod 777 /home/samba
```

smb.confを変更
```sh
$ cd /etc/samba
$ cp smb.conf smb.conf.org
$ vi /etc/samba/smb.conf
```

以下のように変更(※編集後のdiff結果)
```diff
$ diff -u smb.conf.org smb.conf
--- smb.conf.org        2017-xx-xx xx:xx:xx.xxxxxxxxx +0900
+++ smb.conf    2017-xx-xx xx:xx:xx.xxxxxxxxx +0900
@@ -4,16 +4,20 @@
 # you modified it.

 [global]
-       workgroup = SAMBA
+       workgroup = WORKGROUP
        security = user

        passdb backend = tdbsam
+       map to guest = Bad User

        printing = cups
        printcap name = cups
        load printers = yes
        cups options = raw

+       dos charset = CP932
+       unix charset = UTF-8
+
 [homes]
        comment = Home Directories
        valid users = %S, %D%w%S
@@ -34,3 +38,11 @@
        write list = root
        create mask = 0664
        directory mask = 0775
+
+[Share]
+       path = /home/samba
+       writable = yes
+       guest ok = yes
+       guest only = yes
+       create mode = 0777
+       directory mode = 0777
```

### \[global\]
|設定        |値       |意味                                                                  |
|------------|---------|----------------------------------------------------------------------|
|workgroup   |WORKGROUP|Windowsのワークグループ名に合わせる                                   |
|dos charset |CP932    |Windowsの文字コードを指定                                             |
|unix charset|UTF-8    |sambaサーバーの文字コードを指定                                       |
|map to gust |Bad User |アカウントが無いユーザーがアクセスした場合はゲストアカウントとして扱う|

### \[Share\]
|設定          |値         |意味                                                                |
|------------  |-----------|--------------------------------------------------------------------|
|path          |/home/samba|共有するパス                                                        |
|writable      |yes        |書き込み可                                                          |
|gust ok       |yes        |ゲストユーザーでの接続許可                                          |
|gust only     |yes        |ゲストユーザーのみ接続を許可                                        |
|create mode   |0777       |ファイルへのアクセス権(777)を付与                                   |
|directory mode|0777       |ディレクトリのアクセス権(777)を付与                                 |

Sambaサービスの起動と自動起動の設定
```sh
$ systemctl start smb
$ systemctl enable smb
```

#### 補足
※NetBIOSの名前解決を行う場合は、「nmbd」を起動

/etc/samba/smb.conf
```
[global]
netbios name = host_name
```

```sh
$ systemctl start nmb
$ systemctl enable nmb
```

## セキュリティ周りの許可設定

SELinuxにユーザーホームへのアクセスを許可する
```sh
$ getsebool samba_enable_home_dirs
samba_enable_home_dirs –> off
$ setsebool -P samba_enable_home_dirs on
$ getsebool samba_enable_home_dirs
samba_enable_home_dirs --> on
$ restorecon -R /home/samba
```

FirewalldへSambaサービスの許可を設定
```sh
$ firewall-cmd --add-service=samba --permanent
$ firewall-cmd --reload
```

## 参考

[CentOS 7 : Samba : フルアクセスの共有フォルダ作成 ： Server World](https://www.server-world.info/query?os=CentOS_7&p=samba)
