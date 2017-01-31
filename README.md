vagrant-oracle12.1
==================

Vagrant + Oralce Linux 7.3 + Oracle Database 12c Release 1 (12.1.0.2) Enteprise Edition シングル環境の簡易セットアップ。

## ダウンロード

Oracle Database 12c Release 1 (12.1.0.2)のソフトウェアを以下からダウンロードし、Vagrantfileと同じディレクトリに展開。展開すると"database"というサブディレクトリになるはず。

http://www.oracle.com/technetwork/database/enterprise-edition/downloads/index.html

* linuxamd64_12102_database_1of2.zip
* linuxamd64_12102_database_2of2.zip

## Vagrant設定

プロキシを利用する必要がある場合、まずvagrant-proxyconfをインストールし、vagrant-proxyconf用の環境変数を設定しておく。

ホストがMacOS X or Linuxの場合:
```
export http_proxy=http://proxy.example.com:80
export https_proxy=http://proxy.example.com:80
vagrant plugin install vagrant-proxyconf

export VAGRANT_HTTP_PROXY=http://proxy.example.com:80
export VAGRANT_HTTPS_PROXY=http://proxy.example.com:80
export VAGRANT_FTP_PROXY=http://proxy.example.com:80
export VAGRANT_NO_PROXY=localhost,127.0.0.1
```

ホストがWindowsの場合:
```
SET http_proxy=http://proxy.example.com:80
SET https_proxy=http://proxy.example.com:80
vagrant plugin install vagrant-proxyconf

SET VAGRANT_HTTP_PROXY=http://proxy.example.com:80
SET VAGRANT_HTTPS_PROXY=http://proxy.example.com:80
SET VAGRANT_FTP_PROXY=http://proxy.example.com:80
SET VAGRANT_NO_PROXY=localhost,127.0.0.1
```

## セットアップ

`vagrant up`を実行すると、内部的に以下が動く。

* Oracle Linux 7.3のダウンロードと起動
* Oracle Preinstallation RPMのインストール
* ディレクトリの作成
* 環境変数の設定
* oracleユーザーのパスワード設定
* Oracle Databaseのインストール
* リスナーの作成
* データベースの作成

```
vagrant up
```

## 動作確認

ゲストOSに接続する。

```
vagrant ssh
```

CDBに接続する。

```
su - oracle
sqlplus system/oracle
```

PDBに接続し、サンプル表を確認する。

```
SHOW CON_NAME
ALTER SESSION SET CONTAINER = pdb1;
SHOW CON_NAME
SELECT * FROM hr.employees WHERE rownum <= 10;
```

## Author ##

[Shinichi Akiyama](https://github.com/shakiyam)

## License ##

[MIT License](http://www.opensource.org/licenses/mit-license.php)
