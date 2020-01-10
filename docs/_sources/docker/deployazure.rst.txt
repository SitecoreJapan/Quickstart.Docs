#############################
Microsoft Azure への展開
#############################

Microsoft Azure には Docker のコンテナを管理するためのサービスとして、`Container Registry <https://azure.microsoft.com/ja-jp/services/container-registry/>`_ を提供しています。

*******************************
Container Registry の作成
*******************************

Azure ポータル画面、およびコマンドラインでも作成することができますが、ここでは Visual Studio Code のサイドバーで作業を進めます。まず作成をしたいサブスクリプションを選択して、右クリックしてください。メニューにある `Create Registry...` を選択します。

.. image:: images/vscode06.png
   :align: center
   :alt: Azure Account

画面の上部にダイアログが表示されて、Registry name の入力を促してきます。

.. image:: images/vscode07.png
   :align: center
   :width: 400px
   :alt: Registry name

Enter を入力すると次のパラメーターが表示されます。どの価格を利用するのか、という選択肢となります。ここでは、 Standard を選択してください。

.. image:: images/vscode08.png
   :align: center
   :width: 400px
   :alt: プランの選択

続いてリソースグループを選択します。新規に作成することも可能です。

.. image:: images/vscode09.png
   :align: center
   :width: 400px
   :alt: リソースグループの選択

最後にデータセンターを選択してください。

.. image:: images/vscode10.png
   :align: center
   :width: 400px
   :alt: データセンターの選択

実際に作成されたレジストリを見ることができます。

.. image:: images/vscode11.png
   :align: center
   :alt: 作成されたレジストリを確認


******************************************
Container Registry にイメージをコピーする
******************************************

ローカルで作成をした Docker イメージを Azure の Container Registry に展開します。まず上記で作成をした Azure Contaner Registry を標準に設定します。Visual Studio Code でレジストリを右クリックして、Set as Default とします。

.. image:: images/acr01.png
   :align: center
   :alt: コンテナレジストリを標準に設定する

以下のイメージをコピーする形で進めていきます。

.. code-block:: 

    sitecore-xp-sxa-cd
    sitecore-xp-sxa-solr
    sitecore-xp-sxa-sqldev
    sitecore-xp-sxa-standalone
    sitecore-xp-xconnect
    sitecore-xp-xconnect-automationengine
    sitecore-xp-xconnect-indexworker
    sitecore-xp-xconnect-processingengine

.. image:: images/acr02.png
   :align: center
   :width: 400px
   :alt: コンテナレジストリを標準に設定する

まず、Push する先のレジストリに対してログインを実行します。

.. code-block:: 

    az acr login --name sitecoredockerjp

.. image:: images/acr03.png
   :align: center
   :width: 400px
   :alt: レジストリにログイン

ログインに成功した後は、左側の一覧から順に Push を実行していきます。今回はまず最初に sitecore-xp-xconnect を push します。

.. image:: images/acr04.png
   :align: center
   :alt: sitecore-xp-xconnect を Push 

実際にイメージの名前を入力が促されるため、イメージの名前そのままを指定して Enter を押します。

.. image:: images/acr05.png
   :align: center
   :width: 400px
   :alt: 名前を指定します 

続いて、Push のプロセスが走ります。

.. image:: images/acr06.png
   :align: center
   :width: 400px
   :alt: Push を実行しています

Push が完了したかどうか、Azure ポータルで確認をしてください。

.. image:: images/acr07.png
   :align: center
   :width: 400px
   :alt: Azure ポータルで確認

