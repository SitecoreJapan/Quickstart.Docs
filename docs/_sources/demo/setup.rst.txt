###############
セットアップ
###############

******************************
セットアップの準備
******************************

今回は c:\\projects\\sitecore.demo.platform のフォルダを作成して、リポジトリのクローンを準備します。 C:\\Projects に移動をして

.. code-block:: powershell

    git clone https://github.com/Sitecore/Sitecore.Demo.Platform.git

.. image:: images/git01.png
   :align: center
   :width: 400px
   :alt: git clone

を実行します。また、利用するライセンスファイルを c:\licence のフォルダにコピーして

c:\\licence\\licence.xml

でアクセスできるようにします。

******************************
Docker の環境を整える
******************************

Windows Server で Docker を動かすための手順は、マイクロソフトの以下のサイトが参考になります。

* `作業の開始:コンテナー用の Windows を準備する <https://docs.microsoft.com/ja-jp/virtualization/windowscontainers/quick-start/set-up-environment?tabs=Windows-Server>`_

PowerShell を管理者の権限で開き、PowerShell のギャラリーから、Docker-Microsoft PackageManagement Provider をインストールします。

.. code-block:: powershell

   Install-Module -Name DockerMsftProvider -Repository PSGallery -Force

.. image:: images/docker01.png
   :align: center
   :width: 400px
   :alt: DockerMsftProvider

PackageManagement PowerShell モジュールを使用して、最新バージョンの Docker をインストールします。

.. code-block:: powershell

   Install-Package -Name docker -ProviderName DockerMsftProvider

.. image:: images/docker02.png
   :align: center
   :width: 400px
   :alt: docker install

Sitecore のデモでは Linux のイメージも利用するため、LinuxKit をインストールします。まず、以下のサイトから release.zip をダウンロードします。

* `LinuxKit <https://github.com/linuxkit/lcow/releases>`_

ダウンロードしたファイルは、 C:\\Program Files\\Linux Containers のフォルダを作成して展開します。コピーしたファイルはダウンロード後ブロックされているため、ファイルのプロパティを開いて、ダイアログの一番下のチェックボックスをチェックして適用して、ブロックを解除してください。

.. image:: images/docker03.png
   :align: center
   :width: 400px
   :alt: release.zip

.. image:: images/linuxkit01.png
   :align: center
   :width: 400px
   :alt: linuxkit

Windows コンテナと Linux コンテナを同時に動かすために、Experimental の設定を変更します。この設定は、 C:\ProgramData\docker\config\daemon.json のファイルを新規作成して、以下のコードを書き込んでください。ProgramData のフォルダは隠しフォルダになっていますので、

.. code-block:: json

   {
      "experimental": true
   }

.. image:: images/docker04.png
   :align: center
   :width: 400px
   :alt: experimental を有効にする

Docker の必要なモジュールのインストールが完了した段階で、一度再起動してください。

******************************
デモ環境を展開する
******************************

Docker で展開するために便利な SitecoreDockerTools のインストール、ライセンスファイルの準備を進めていく形となりますが、デモの中に init.ps1 という形で一気に設定を変更するスクリプトを提供しています。

まずリポジトリをコピーしたディレクトリに移動して、以下のコマンドを実行してください。ライセンスファイルのパスは別のパスにする場合は、書き換えて実行してください。

.. code-block:: powershell

    .\init.ps1 -InitEnv -LicenseXmlPath C:\license\license.xml -AdminPassword b

.. image:: images/docker05.png
   :align: center
   :width: 400px
   :alt: init.ps1 を実行する

途中で mkcert のコマンドを実行するにあたり、ダイアログが表示されます。今回は はい をクリックしてください。しばらくすると、スクリプトの実行が完了となります。

これでデモ環境を立ち上げるための基本的な設定が完了したことになります。

実際に実行するための手順に入ります。まず、Docker のイメージをダウンロードします。

.. code-block:: powershell

    docker-compose pull

.. image:: images/docker07.png
   :align: center
   :width: 400px
   :alt: docker-compose pull

エラーが出た場合も、もう一度 pull を実行することで完了させてください。

続いて、コンテナを起動します。以下のコマンドでコンテナが動きます。

.. code-block:: powershell

    docker-compose up -d

エラーが出た場合も、もう一度実行することで全てのコンテナが動くようになります。

.. image:: images/docker08.png
   :align: center
   :width: 400px
   :alt: docker-compose up -d

初回起動に関しては、データをインポートするのに時間がかかります。以下のコマンドで、インポートの状況を確認してください。

.. code-block:: powershell

    docker-compose logs -f init

最後に以下の行が表示されれば、インポートが完了となります。

.. code-block::

   init_1                 |       3/3/2021 9:02:51 AM No jobs are running. Monitoring stopped.

.. image:: images/docker09.png
   :align: center
   :width: 400px
   :alt: Monitoring stopped.

******************************
デモ環境にアクセスする
******************************

Web サイトの URL は標準では以下のようになっています。 cm サーバーにログインをするパスワードは、 init.ps1 で設定したパスワードとなります。

* https://cd.lighthouse.localhost
* https://cm.lighthouse.localhost/sitecore
