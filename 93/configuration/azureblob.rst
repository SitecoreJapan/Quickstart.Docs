##################################
Sitecore blob storage の設定
##################################

Sitecore 9.3 からは Azure のストレージサービスとなる Azure Blob Storage の利用ができるようになりました。この設定を編集サーバー、配信サーバーに対して設定することで、ストレージを共有することができるようになります。ここでは実際に使うための手順を紹介します。

*************
事前の準備
*************

=================================
データベースのクリーンアップ
=================================

モジュールのセットアップの前に、一度 SQL データベースのクリーンアップを実行します。下記の画面は `コントロールパネル` - `管理ツール` を開きます。

.. image:: images/Azureblob01.png
   :align: center
   :width: 400px
   :alt: 管理ツールを開く

続いて `Database and Operations` を選択すると `Database Cleanup` を開きます。

.. image:: images/Azureblob02.png
   :align: center
   :width: 400px
   :alt: Database Cleanup

この画面で、左側の `Databases` からは `master` と `web` を選択、右側のタスクから `Cleanup blobs` をチェックして実行してください。

.. image:: images/Azureblob03.png
   :align: center
   :width: 400px
   :alt: Cleanup Blobs

=================================
Azure Blob ストレージの準備
=================================

Sitecore と接続するための Azure Storage を準備します。リソースの追加から `ストレージ` グループにある `ストレージアカウント` を選択します。：

.. image:: images/Azureblob04.png
   :align: center
   :width: 400px
   :alt: ストレージアカウント

ここではストレージアカウント名をとデータセンターを設定して作成を実行します。

.. image:: images/Azureblob05.png
   :align: center
   :width: 400px
   :alt: 作成

しばらくすると作成をしたリソースグループに、リソースアカウントが表示されます。作成したリソースアカウントを開き、アクセスキーを選択しあｍす。

.. image:: images/Azureblob06.png
   :align: center
   :width: 400px
   :alt: アクセスキー

ここにあるアクセスキーは後ほど利用する形となります。

********************
モジュールの展開
********************

モジュールの展開方法はいくつか用意されています。今回は仮想マシンに構築しているデモ環境を利用するため、Webdeploy を利用せずに手作業で設定していきます。Sitecore のインストールページから、Blob storage のパッケージをダウンロードします。

* `Download options for Blob Storage <https://dev.sitecore.net/Downloads/Sitecore_Experience_Platform/93/Sitecore_Experience_Platform_93_Initial_Release.aspx>`_ 

ダウンロードした zip ファイルを展開します。

.. image:: images/Azureblob07.png
   :align: center
   :width: 400px
   :alt: ファイルの展開

展開したフォルダにアクセスして、 `Content\WebSite` を開くことで3つのフォルダが展開されていることがわかります。

.. image:: images/Azureblob08.png
   :align: center
   :width: 400px
   :alt: website を確認

展開されたファイルを実際の Sitecore の Web サイトにコピーをしていきます。まず、 `App_Config - Modules` の下に `Sitecore.AzureBlobStorage` のフォルダをコピーします。

.. image:: images/Azureblob09.png
   :align: center
   :width: 400px
   :alt: Modules にコピー

続いて `App_Data` のフォルダに `Migration` と `Transforms` のフォルダをコピーします。

.. image:: images/Azureblob10.png
   :align: center
   :width: 400px
   :alt: App_Data にコピー

最後に `bin` にある 5 つのファイルをコピーします。

.. image:: images/Azureblob11.png
   :align: center
   :width: 400px
   :alt: bin のファイルをコピー

ここから接続の設定になります。まず、`App_config\Connection.Strings.config` に以下の1行を追加してください。：

.. code-block::

    <add name="azureblob" connectionString="<AzureStorageConnectionString>"/>

ここで設定する `AzureStorageConnectionString` は既に作成をしている Azure Storage の接続文字列となります。

続いてストレージ名を記載します。この設定は `\App_Config\Modules\Sitecore.AzureBlobStorage\Sitecore.AzureBlobStorage.config` が設定ファイルになります。ファイルを開くと以下の記載があります。

.. code-block::

  <param name="containerName">blobcontainer</param>

`containerName` がコンテナの名前となります。今回はデフォルトの名前 `blobcontainer` で作成します。

Azure の管理画面に戻り、ストレージアカウントを開きます。コンテナーの項目をクリックします。：

.. image:: images/Azureblob12.png
   :align: center
   :width: 400px
   :alt: コンテナーの作成

コンテナーを作成します。

.. image:: images/Azureblob13.png
   :align: center
   :width: 400px
   :alt: 新しいコンテナー

設定はこれで完了となります。

********************
Blob データの移行
********************

ここで紹介している手順は `Use the blob migration tool <https://doc.sitecore.com/developers/93/sitecore-experience-manager/en/use-the-blob-migration-tool.html>`_ で紹介している手順となります。

すでにメディアライブラリで管理しているファイルを Azure Blob Storage に移行していきます。このための PowerShell のスクリプトが、`App_Data\Migration` に用意されています。

.. image:: images/Azureblob14.png
   :align: center
   :width: 400px
   :alt: マイグレーションのスクリプト

PowerShell で処理できるように、AzureRM をインストールします。まず、既に入っているかどうかを確認します。入っていなければ、`Install-Module` コマンドでインストールをします。途中 PSGallery を利用するか？という質問が出てきますので Y を入力して Enter を入れれば AzureRM がインストールされます。

.. code-block::

  Get-Module -Name AzureRm -ListAvailable
  Install-Module -Name AzureRM

インストールが終わったあと、モジュールのインストールを確認します。

.. code-block::

   Get-Module -Name AzureRm -ListAvailable 

.. image:: images/Azureblob15.png
   :align: center
   :width: 400px
   :alt:  AzureRm 

これで準備が完了しました。実際に PowerShell のスクリプトのあるフォルダに移動して、以下の1行を実行してください。

.. code-block::

    .\Invoke-Migration.ps1 -SqlDBConnectionNames @("master", "web") -AzureBlobConnectionName "azureblob" -BlobContainerName "blobcontainer" -Force *>&1 | Tee-Object -FilePath Invoke-Migration.log


.. image:: images/Azureblob16.png
   :align: center
   :width: 400px
   :alt:  Invoke-Migration 

処理が進むと、Azure Storage のコンテナにファイルがコピーされていることがわかります。

.. image:: images/Azureblob17.png
   :align: center
   :width: 400px
   :alt:  ストレージにコピー 

これにより Sitecore のメディアファイルを Azure のストレージに展開することができました。

*************
参考動画
*************

ここまでの手順を動画としてまとめました。

.. raw:: html

    <iframe width="560" height="315" src="https://www.youtube.com/embed/dqm7Tkc2a5g" frameborder="0" allowfullscreen></iframe>


*************
参考サイト
*************

* `Sitecore blob storage <https://doc.sitecore.com/developers/93/sitecore-experience-manager/en/sitecore-blob-storage.html>`_
* `Azure BlobをメディアライブラリーのBlobストレージとして使用する - マイグレーション編 <https://www.pine4.net/Memo2/Article/Archive/Use-Azure-Blob-as-Media-Library-Blob-Storage-Migration>`_