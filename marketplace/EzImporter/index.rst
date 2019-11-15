Ez Importer でデータインポート
===============================

ここでは Sitecore Marketplace で提供されている Ez Impoter に関する情報を提供しています。このモジュールを利用することで、Excel ファイルで定義されているデータが一括で Sitecore のアイテムとしてインポートされる形となります。

## 検証環境

今回は以下の環境でテスト、実行しました。モジュールとしてはテスト対象外のバージョンとなりますが、以下の手順に関しては動作します。

* Sitecore Experience Platform 9.1 Initial Release

## モジュールのダウンロード
[https://github.com/dresser/SitecoreEzImporter/releases](https://github.com/dresser/SitecoreEzImporter/releases) から今回は `Sitecore.EzImporter-1.0.3.zip` をダウンロードします。

## サンプルのダウンロード
上記のモジュールで必要となるサンプルデータを [Sitecore Marketplace - Ez Importer](https://marketplace.sitecore.net/Modules/E/Ez_Importer.aspx?sc_lang=en) からダウンロードします。ダウンロードするファイルは以下の２つとなります。

* `Sitecore.EzImporter.SampleMap-1.0.01.zip`
* `Cars-1.0.0.xlsx`

なお、上記の Excel ファイルと SampleMap の構造が若干違うため、Excel のファイルに関しては修正が必要となります。C1 セルの Body Type の間のスペースを削除してください。

<img src="images/car.PNG" alt="Excel">

## 日本語リソースのダウンロード
Ez Impoter は英語のリソースのみのため、この Github のリポジトリにて簡単なサンプル日本語リソースを用意しています。ダウンロードして利用してください。

## インストール

手順は非常にシンプルで、以下の手順を進めることで利用できるようになります。

* `Sitecore.EzImporter-1.0.3.zip` のモジュールインストール
* `Sitecore.EzImporter.SampleMap-1.0.01.zip` のモジュールインストール
* 日本語リソースのインポート ( `ez-importer-ja-jp.xml` は Core へ、`ez-importer-master-ja-jp.xml` は Master へ )

## インポート

ログイン後の画面に Ez Impoter が 追加されているためクリックします。画面が開いたあとには、ダウンロード、修正済の `Cars-1.0.0.xlsx` のファイルをドラッグ＆ドロップ、コンテンツのインポート先を指定して、Import ボタンを押すとデータが追加されます。

## 関連サイト一覧
* ブログ - [Ez Importer Excel Import Utility](https://www.matthewdresser.com/sitecore/ez-importer-excel-import-utility)
* Sitecore Marketplace - [Ez Importer](https://marketplace.sitecore.net/Modules/E/Ez_Importer.aspx?sc_lang=en)
* GitHub [SitecoreEzImporter](https://github.com/dresser/SitecoreEzImporter)

---
[目次に戻る](../README.md)
