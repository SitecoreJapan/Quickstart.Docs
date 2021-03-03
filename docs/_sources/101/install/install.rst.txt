#############################################
Sitecore Experience Platform のインストール
#############################################

Sitecore Experience Platform 10.1 をインストールするために、Sitecore Instllation Assistant を利用して、まずは関連モジュールをインストールします。

今回は以下の環境にインストールをします。

* Windows Server 2019 Standard
* SQL Server 2019

****************************************
Sitecore のインストールプログラムの入手
****************************************

今回は Sitecore Install Assistant を利用してインストールを進めていきます。このため、以下の Web サイトからインストールファイルをダウンロードしてください。

* `Sitecore Experience Platform 10.1 <https://dev.sitecore.net/Downloads/Sitecore_Experience_Platform/101/Sitecore_Experience_Platform_101.aspx>`_

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

インストールが完了すると、`Close` のボタンが有効になります。

.. image:: images/sia05.png
   :align: center
   :width: 400px
   :alt: Close が有効に

一度ダイアログを閉じてください。

インストールが完了したあと、先ほど一度再起動が必要となっていますので、再起動します。

***********************
Solr のインストール
***********************

今回は、インストールモジュールに付属している Solr-SingleDeveloper.json ファイルを利用してインストールを実行します。以下のようにコマンドを実行してください。

.. code-block:: powershell

    Install-SitecoreConfiguration .\Solr-SingleDeveloper.json

以下のように表示されます。

.. image:: images/solr01.png
   :align: center
   :width: 400px
   :alt: Solr のインストール

インストールが完了すると、Solr のサービスが起動します。


********************
インストールの開始
********************

モジュールのインストールが完了すると、次は Sitecore のインストールとなります。ここではインストールツールに標準で提供されているスクリプトの値を変更します。

インストールをする際の設定を記載します。以下の項目を入力してください。以下の値は例となります。

============================= ==================== =======================
パラメータ                     入力値                説明 
============================= ==================== =======================
$SitecoreAdminPassword        b                    管理者パスワード
$SCInstallRoot                C:\\projects\\sif    インストールのルート
$SitecoreSiteName             任意   サイト名
$SqlAdminPassword             任意                  SQL Server パスワード
============================= ==================== =======================

.. image:: images/sia06.png
   :align: center
   :width: 400px
   :alt: インストールの基本設定

インストールを実行します。

.. code-block:: powershell

    .\XP0-SingleDeveloper.ps1

.. image:: images/sia07.png
   :align: center
   :width: 400px
   :alt: インストール

しばらくするとインストールが完了します。