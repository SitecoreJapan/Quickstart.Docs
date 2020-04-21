#############################################
Sitecore Experience Platform のインストール
#############################################

Sitecore Experience Commerce をインストールする最初のステップは、Sitecore Experience Platform 9.3 を事前にインストールしする必要があります。ここでは、Sitecore Instllation Assistant を利用して、まずは関連モジュールをインストールします。

今回は以下の環境にインストールをします。

* Windows Server 2019 Standard
* SQL Server 2019

****************************************
Sitecore のインストールプログラムの入手
****************************************

今回は Sitecore Install Assistant を利用してインストールを進めていきます。このため、以下の Web サイトからインストールファイルをダウンロードしてください。

* `Sitecore Experience Platform 9.3 Initial Release <https://dev.sitecore.net/Downloads/Sitecore_Experience_Platform/93/Sitecore_Experience_Platform_93_Initial_Release.aspx>`_

`Download options for On Premises deployment` のグループにある `Graphical setup package for XP Single` をダウンロードしてください。インストールファイルのダウンロードが完了した、ファイルを展開して次のステップに進みます。

***************************
モジュールのインストール
***************************

この手順に関しては、１つの環境で初回のみ実行するだけで完了です。すでに別の Sitecore をインストールしている場合は、スキップしてください。

Sitecore Install Assistant を立ち上げます。これはダウンロードをしたファイルを展開してください。ここでは、 `c:\\projects\\sif` に展開します。

.. image:: images/sia01.png
   :align: center
   :width: 400px
   :alt: フォルダ


`setup.exe` をダブルクリックすると、インストーラーが立ち上がり以下のような画面となります。

.. image:: images/sia02.png
   :align: center
   :width: 400px
   :alt: 起動画面

Start のボタンをクリックすると、モジュールのインストール画面になります。

.. image:: images/sia03.png
   :align: center
   :width: 400px
   :alt: モジュールインストール

Install のボタンをクリックして、必要なモジュールをインストールしてください。

.. image:: images/sia04.png
   :align: center
   :width: 400px
   :alt: インストール中

インストールが完了すると、`Next` のボタンが有効になります。

.. image:: images/sia05.png
   :align: center
   :width: 400px
   :alt: Next が有効に

一旦、ウィザードを閉じます

***********************
Solr のインストール
***********************

Sitecore Install Assistant は 9.3 より Solr のインストールにも対応しています。実際には Sitecore Install Framework のツールが sitecore-solr.json ファイルを利用して、Solr のインストールを行います。ここでは、このファイルを利用してインストールを実行します。

.. code-block:

    Install-SitecoreConfiguration .\Solr-SingleDeveloper.json

まず、以下の項目が表示されます。

.. image:: images/solr01.png
   :align: center
   :width: 400px
   :alt: Solr のインストール


********************
インストールの開始
********************

モジュールのインストールが完了すると、次は Sitecore のインストールとなります。ここではインストールツールに標準で提供されているスクリプトの値を変更します。

インストールをする際の設定を記載します。以下の項目を入力してください。以下の値は例となります。

============================= ==================== =======================
パラメータ                     入力値                説明 
============================= ==================== =======================
$SitecoreAdminPassword        b                    管理者パスワード
$SCInstallRoot                C:\projects\sif      インストールのルート
$SitecoreSiteName             sxa.storefront.com   サイト名
$SqlAdminPassword             任意                 SQL Server パスワード
============================= ==================== =======================

.. image:: images/sia06.png
   :align: center
   :width: 400px
   :alt: インストールの基本設定

インストールを実行します。

.. code-block:

    .\SC930-SingleDeveloper.ps1

.. image:: images/sia07.png
   :align: center
   :width: 400px
   :alt: インストール

ログイン画面が表示されれば、インストールが無事完了します。
