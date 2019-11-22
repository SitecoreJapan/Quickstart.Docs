#####################
作成したアプリの展開
#####################

ここでは実際に作成をした React で作った JavaScript のアプリを Sitecore に展開する手続きを進めます。

********************
JSS アプリの準備
********************

サンプルのアプリを作成した際には、 `sitecore\config\<appname>.config` という形で設定ファイルが作成されています。今回動作させるホスト名を `hostName` に設定します。

.. code-block:: xml

      <site patch:before="site[@name='website']"
            inherits="website"
            name="sample-app"
            hostName="sample-app.dev.local"
            rootPath="/sitecore/content/sample-app"
            startItem="/home"
            database="master" />

今回はデモ環境のため、このまま `sample-app.dev.local` の名前を、 `C:¥¥Windows¥¥System32¥¥drivers¥¥etc¥¥hosts` に追加します。

.. code-block:: 

    127.0.0.1    sample-app.dev.local

Sitecore がインストースされているインスタンスに対して、このホスト名を追加します。

.. image:: images/hostname01.png
   :align: center
   :width: 400px
   :alt: ホスト名を追加する


********************
Sitecore の準備
********************

作成したアプリを展開するにあたり、API Key を Sitecore 側で準備をする必要があります。API Key の作成は以下の手順でできます。

1. Sitecore に管理者権限でログインをします。
2. コンテンツエディターを開きます
3. `/sitecore/system/Settings/Services/API Keys` のアイテムを選択します

.. image:: images/apikey01.png
   :align: center
   :width: 400px
   :alt: API キーのアイテムを選択

4. API キーを作成します、ここではアプリ名で作成しました

.. image:: images/apikey02.png
   :align: center
   :width: 400px
   :alt: キーのアイテムを作成

5. API キーに以下の項目を設定します

設定名　            設定内容　今回の設定

CORS Origines         http://localhost:3000
認められたコントローラー  *
偽装ユーザー            extranet\anonymous
スロットルストラテジー    空欄

.. image:: images/apikey03.png
   :align: center
   :width: 400px
   :alt: キーのアイテムを作成

6. アイテムをパブリッシュします
7. アイテム ID を控えます

.. image:: images/apikey04.png
   :align: center
   :width: 400px
   :alt: アイテム ID

このサンプルでは、{45D95A97-1FD4-4403-BF9C-42BFD75843FE} がアイテム ID になります。

8. 作成したキーが利用できるか、以下の URL でアクセスをします

* http://sample-app.dev.local/sitecore/api/layout/render/jss?item=/&sc_apikey={YOUR_API_KEY_ID}

9. アクセスをすると、以下のように JSON 形式でデータが表示されます。

.. image:: images/apikey05.png
   :align: center
   :width: 400px
   :alt: 設定の最終確認

******************************
JSS アプリと Sitecore の接続
******************************

設定が完了したので、接続をする手順と接続を実施します。まず、コマンドとして `jss setup` を実行してください。

1. 最初にインスタンスの状態を聞いてきます。ここでは y を選択します。
2. 続いて Sitecore がインストールされているディレクトリ名を記載します。

.. code-block:: powershell

    PS C:\Users\Sitecore\sample-app> jss setup
    Is your Sitecore instance on this machine or accessible via network share? [y/n]: y
    Path to the Sitecore folder (e.g. c:\inetpub\wwwroot\my.siteco.re): C:\inetpub\wwwroot\sample-app.dev.local
    Sitecore hostname (e.g. http://myapp.local.siteco.re; see /sitecore/config; ensure added to hosts): http://sample-app.dev.local
    Sitecore import service URL [http://sample-app.dev.local/sitecore/api/jss/import]:
    Sitecore API Key (ID of API key item): {45D95A97-1FD4-4403-BF9C-42BFD75843FE}
    Please enter your deployment secret (32+ random chars; or press enter to generate one): 256655EC8F3A45B5AD90B63BC25B8067
    Deploy secret Sitecore config written to C:\Users\Sitecore\sample-app\sitecore\config\sample-app.deploysecret.config
    Ensure this configuration is deployed to Sitecore.
    JSS connection settings saved to C:\Users\Sitecore\sample-app\scjssconfig.json

    NEXT STEPS
    * Ensure the hostName in /sitecore/config/*.config is configured as sample-app.dev.local, and in hosts file if needed.
    * Deploy your configuration (i.e. 'jss deploy config')
    * Deploy your app (i.e. 'jss deploy app -c -d')
    * Test your app in integrated mode by visiting http://sample-app.dev.local
    PS C:\Users\Sitecore\sample-app>

jss deploy config

jss deploy app --includeContent --includeDictionary


http://sample-app.dev.local/



**************
関連サイト
**************

* `App Deployment <https://jss.sitecore.com/docs/getting-started/app-deployment>`_