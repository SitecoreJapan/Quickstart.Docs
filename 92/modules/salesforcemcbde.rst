#######################################################
Sitecore Connect for SFMC - Behavioral Data Exchange
#######################################################

この文書では、 Sitecore Connect for Salesforce Marketing Cloud 3.0 のモジュールのうち、Behavioral Data Exchange に関するセットアップの手順を紹介しています。

.. note:: Sitecore Connect for Salesforce Marketing Cloud 3.0 は Sitecore Experience Platform 9.2 向けのモジュールとなります。Sitecore 9.0, 9.0.1, 9.1 を利用されている方は、別のバージョンのモジュールをご利用ください。

**************************
必要システム
**************************


Behavioral Data Exchange 3.0 は、以下の環境で利用することが可能です。

* Sitecore Experience Platform 9.2.0
* `Data Exchange Framework 3.0 <https://dev.sitecore.net/Downloads/Data_Exchange_Framework/3x/Data_Exchange_Framework_300.aspx>`_ 
* Salesforce Marketing Cloud の管理者権限

すでに上記の環境が整っていることを前提として、インストール、設定に関して紹介をしていきます。

**************************
モジュールのインストール
**************************

以下の手順でインストールを進めていきます。

1. モジュールを Sitecore Connect for Salesforce Marketing Cloud 3.0 にある Behavioral Data Exchange の Installation Package をクリックしてダウンロードをします。
2. インストールをする Sitecore の環境に管理者権限でログインをします
3. 「コントロールパネル」－「管理」パネル－「パッケージをインストールする」を開きます
4. ダウンロードしたモジュールのインストールをします

.. image:: images/sfmcbde01.png
   :align: center
   :width: 400px
   :alt: パッケージをインストールする

5．インストールの手順を確認します。

.. image:: images/sfmcbde02.png
   :align: center
   :width: 400px
   :alt: インストールの注意点


.. image:: images/sfmcbde02.png
   :align: center
   :width: 400px
   :alt: インストールの注意点

6. ファイルの上書きの警告が出た場合は、「はい」を選択してください。
7. インストールの手順で紹介されていた、「サイトコア クライアントを再起動します。」をチェックしてブラウザ側の設定をリセットします。

.. image:: images/sfmcbde03.png
   :align: center
   :width: 400px
   :alt: インストールの注意点

8. コンテンツエディターを開いて、 `/sitecore/system/Data Exchange` のアイテムを右クリック、`SFMC テナント用接続` を選択できるようになっている段階で、モジュールのインストールは成功しています。

.. image:: images/sfmcbde04.png
   :align: center
   :width: 400px
   :alt: インストールの注意点

**********************************
Salesforce Marketing Cloud の設定
**********************************












