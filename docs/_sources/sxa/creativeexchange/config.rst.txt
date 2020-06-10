########################
@sxa/CLI
########################

テーマに関して、Creative Exchange Live を有効にするために、設定ファイルを変更します。環境として、Node.js が必要となりますので、すでにインストール済みとしてください。

.. note::

    ここで紹介をする設定は Sitecore Experience Platform 9.3 、および Sitecore Experience Accelerator 9.3 の環境を想定しています。gulp のバージョンは 3.9.x を利用します。

Sitecore がインストールされているフォルダの、 App_Config\Include\z.Feature.Overrides のフォルダにある z.SPE.Sync.Enabler.Gulp.config.disabled のファイルを有効にします。

.. image:: images/sxacxl01.png
   :align: center
   :width: 400px
   :alt: ファイルの変更

続いてコマンドとして利用する SXA CLI をインストールします。インストールの際には Windows のコマンドライン、もしくは Windows Termial から以下の２行を実行します。

.. code-block:: Batch

    npm config set @sxa:registry https://sitecore.myget.org/F/sc-npm-packages/npm/
    npm i -g @sxa/CLI

インストールの画面は以下の通りです。

.. image:: images/sxacxl02.gif
   :align: center
   :width: 400px
   :alt: コマンドのインストール

事前準備は完了しました。次のステップではインストールをしたコマンドを利用してテーマを作成します。

