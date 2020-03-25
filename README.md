自己証明書作成手順
=================================================

自己証明書を作成する手順です


前提条件
-----------------------------

* chocolatey, 0.10.15
* mkcert, v1.4.1


ツールのインストール
-----------------------------

### chocolatey

公式ページ参照

- https://chocolatey.org/install


### mkcert

chocolateyを使ってインストールする。

```bash
choco install -y mkcert

Created a new local CA at "C:\Users\[ユーザ名]\AppData\Local\mkcert" �
The local CA is now installed in the system trust store! ⚡️
Note: Firefox support is not available on your platform. ℹ️
The local CA is now installed in Java's trust store! ☕️
```

コマンドを実行すると、作成されるCA証明書を信頼するか警告確認メッセージが出るので「はい」とする。

作成されたCA証明書は以下のディレクトリに格納されている。再配布する際に利用できる。

* `C:\Users\[ユーザ名]\AppData\Local\mkcert`

```bash
ll ~/AppData/Local/mkcert/
total 8.0K
-rw-r--r-- 1 [ユーザ名] 197121 1.7K  3月  3 16:38 rootCA.pem
-rw-r--r-- 1 [ユーザ名] 197121 2.5K  3月  3 16:38 rootCA-key.pem
```

ローカルCAの構築
-----------------------------

以下のコマンドを実行し、ローカルPCにCAを構築する。

この作業は一度のみでよい。

CAを一度構築すれば、同一PCでは何回でも証明書を発行できる。

```bash
mkcert -install
```

証明書作成
-----------------------------

以下のコマンドを実行し、CAで署名したサーバ証明書を作成する。

```bash
# 作成, mkcert [ドメイン名]
mkcert localhost

Using the local CA at "C:\Users\[ユーザ名]\AppData\Local\mkcert" ✨

Created a new certificate valid for the following names �
 - "localhost"

The certificate is at "./localhost.pem" and the key at "./localhost-key.pem" ✅


# 確認
ll
total 12K
-rw-r--r-- 1 [ユーザ名] 197121 1.6K  3月  3 16:48 localhost.pem
-rw-r--r-- 1 [ユーザ名] 197121 1.7K  3月  3 16:48 localhost-key.pem
```

