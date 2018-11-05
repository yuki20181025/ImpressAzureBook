# Azure実践ガイド サンプルコード
株式会社インプレス [Azure実践ガイド](https://book.impress.co.jp/books/1117101015) の第14章 「リファレンスアーキテクチャと構築テクニック」のサンプルコードです。

## 合計6パターン
* ASP .NET & Azure SQL Database Todoアプリケーション
  * DotNetIaaS
    * Windows仮想マシンにアプリをデプロイ
    * アプリのデプロイに時間がかかります (30分程度)
  * DotNetPaaS
    * Web Appにアプリを配置
  * DotNetPaaSMultiRegion
    * DotNetPaaSのマルチリージョンパターン
* Node.js & AngularJS & Cosmos DB Todoアプリケーション
  * NodeIaaS
    * Linux仮想マシンにコンテナー化したアプリをデプロイ
    * sshの公開鍵は別途作ってパラメータファイルで指定してください
  * NodePaaS
    * Web App for Containersにアプリを配置
  * NodePaaSMultiRegion
    * NodePaaSのマルチリージョンパターン

## 実行方法
各ディレクトリ下で、以下の手順を実行します。bashとAzure CLIの例です。

### サンプルパラメータファイルのコピー
```
cp sample.parameters.json parameters.json
```

### パラメータファイルの編集
書籍を参考に、パラメータファイル parameters.json の各パラメータを編集します。
他読者とリソース名が重複しないよう、prefixやDNSラベルの命名を工夫してください。

### リソースグループの作成
以下は .NET IaaSパターン向けのリソースグループを作る例です。
```
az group create -n azbook-dotnetiaas-rg -l japaneast
```

### テンプレートのデプロイ
以下は .NET IaaSパターン向けのテンプレートのデプロイする例です。先に編集したローカルのパラメータファイルを指定し、デプロイします。テンプレートのリポジトリをfork、cloneした場合は、--template-uriパラメータの変更を忘れないでください。
```
az group deployment create -g azbook-dotnetiaas-rg --template-uri https://raw.githubusercontent.com/ToruMakabe/ImpressAzureBook/master/DotNetIaaS/main.json --parameters ./parameters.json
```

## 改訂履歴

* 2018/11/05 test
* 2017/12/11: OMS Agent for Linuxのバージョンを1.4へアップデート
* 2017/12/11: サンプルパラメータのパスワード文字数を修正
* 2017/12/09: NSGルールの修正