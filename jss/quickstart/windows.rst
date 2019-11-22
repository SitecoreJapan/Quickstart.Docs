###########################
環境の整備 ( Windows 編)
###########################


************************
システム環境の整備
************************

環境を整えるために、以下のコンポーネントをインストールしてください。

1. `Node.js <https://nodejs.org/ja/>`_ (LTS版) をダウンロードします

.. image:: images/winnodejs01.png
   :align: center
   :width: 400px
   :alt: Node.js をダウンロード

2. ダウンロードしたファイルをインストールします。

.. image:: images/winnodejs02.png
   :align: center
   :width: 400px
   :alt: Node.js インストール

3. ターミナルでバージョンを確認します。

.. code-block:: doscon

  PS C:\Users\Sitecore> node --version
  v12.13.1
  PS C:\Users\Sitecore>
   
******************************
JSS コマンドのインストール
******************************

JSS アプリを作るためのコマンドをインストールします。今回は以下のような手順で進めました。

.. code-block:: doscon

  PS C:\Users\Sitecore> npm -g install @sitecore-jss/sitecore-jss-cli
  npm WARN deprecated joi@14.3.1: This module has moved and is now available at @hapi/joi. Please update your dependencies as this version is no longer maintained an may contain bugs and security issues.
  npm WARN deprecated hoek@6.1.3: This module has moved and is now available at @hapi/hoek. Please update your dependencies as this version is no longer maintained an may contain bugs and security issues.
  npm WARN deprecated topo@3.0.3: This module has moved and is now available at @hapi/topo. Please update your dependencies as this version is no longer maintained an may contain bugs and security issues.
  npm WARN deprecated fsevents@1.2.9: One of your dependencies needs to upgrade to fsevents v2: 1) Proper nodejs v10+ support 2) No more fetching binaries from AWS, smaller package size
  ...
  + @sitecore-jss/sitecore-jss-cli@12.0.0
  added 354 packages from 233 contributors in 25.913s

コマンドラインのインストールが完了です。

***************************
サンプルプロジェクトの作成
***************************

今回は React のプロジェクトを作成します。アプリ名を決めて、以下のようにコマンドを実行してください。

.. code-block:: doscon

  jss create <your-app-name> <app-template-name>

後者の sample に関しては、 `Sitecore JavaScript Services <https://github.com/Sitecore/jss>`_ からソースコードをダウンロードする形となります。
今回は、以下のように実行します。

.. code-block:: doscon

  PS C:\Users\Sitecore> jss create sample-app react
  JSS CLI is running in global mode because it was not installed in the local node_modules folder.
  Acquiring templates from https://github.com/Sitecore/jss/archive/master.zip...
  Extracting template react...
  mkdir C:\Users\Sitecore\sample-app\data\
  mkdir C:\Users\Sitecore\sample-app\data\component-content\
  mkdir C:\Users\Sitecore\sample-app\data\component-content\Styleguide\

                      __________
                    __ / / __/ __/
                   / // /\ \_\ \  
                   \___/___/___/
  
  JSS application sample-app is ready!

  Next steps:
  * Enable source control (i.e. git init)
  * Try out your application with cd sample-app then jss start
  * Connect to Sitecore with jss setup (optional)
  * Check out the JSS documentation at https://jss.sitecore.net

  Enjoy!
  PS C:\Users\Sitecore>

Enjoy! まで表示されれば、`sample-app` のフォルダの中にサンプルプロジェクトが出来上がります。

********************
サンプルアプリの実行
********************

早速作成されたディレクトリに移動して実行します。

.. code-block:: doscon

  cd sample-app
  jss start

コマンドで `jss start` を実行すると、しばらくするとアクセスできる URL が表示されます（環境によってはブラウザが起動して表示されます）。

.. image:: images/jsssample01.png
   :align: center
   :width: 400px
   :alt: 起動中

.. image:: images/jsssample02.png
   :align: center
   :width: 400px
   :alt: URL が表示される

表示された URL はサンプルのページが表示されています。

.. image:: images/jsssample03.png
   :align: center
   :width: 400px
   :alt: サンプルのサイト

ページが表示されていれば、完了となります。

**************
関連サイト
**************

* `Quick Start <https://jss.sitecore.com/docs/getting-started/quick-start>`_
