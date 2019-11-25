#####################################
Sitecore Connect for Sitecore CMP
#####################################

.. todo:: 本文書は Sitecore 9.3 リリース後に更新予定です。

Sitecore Connect for Sitecore CMP 1.0.0 を利用することで、Content Hub で作成したコンテンツを、Sitecore のアイテムとして追加することができるようになります。

ここではモジュールのインストールと動作検証まで紹介をします。

**************************
必要システム
**************************

Sitecore Connect for Sitecore CMP 1.0.0 は以下のシステムで利用することができます。

* Sitecore Experience Platform 9.2
* Sitecore Experience Manager 9.2
* Sitecore Experience Platform 9.1
* Sitecore Experience Manager 9.1

.. note:: 本文書は Sitecore Experience Platform 9.2 の内容となっています。

**************************
モジュールのダウンロード
**************************

以下のページからモジュールのダウンロードをします。

* `Sitecore Connect for Sitecore CMP 1.0.0 <https://dev.sitecore.net/Downloads/Sitecore_Connect_for_Sitecore_CMP/10/Sitecore_Connect_for_Sitecore_CMP_100.aspx>`_

この解説では `Sitecore Connect CMP for Sitecore XP 9.2` をダウンロードしてインストールを進めます。

**************************
モジュールのインストール
**************************

モジュールのインストールは、「コントロールパネル」－「パッケージをインストールする」を開いてください。

.. image:: images/chcmp01.png
   :align: center
   :width: 400px
   :alt: モジュールのインストール
   
モジュールのインストールが完了すれば、あとは設定のみとなります。

*************************************
Microsoft Azure Service Bus の設定
*************************************

Sitecore Content Hub CMP と Sitecore の接続をする際に Microsoft Azure Service Bus の設定が必要となります。ここではサンプルを1つ作成します。

.. image:: images/chcmp02.png
   :align: center
   :width: 400px
   :alt: Service Bus の作成
   
設定する項目は以下の通りです

=================== ==========================
設定項目            設定値
=================== ==========================
名前                名前を設定します
価格レベル          Standard
サブスクリプション  お持ちのサブスクリプション
リソースグループ    追加するリソースグループ
場所                利用するデータセンター
=================== ==========================

今回は以下のように設定をしました。

.. image:: images/chcmp03.png
   :align: center
   :width: 400px
   :alt: 名前空間の作成
   
作成した Service Bus を開いて、左側のメニューからエンティティの中にあるトピックを選択します。

.. image:: images/chcmp04.png
   :align: center
   :alt: トピック
   
新しいトピックを作成します

.. image:: images/chcmp05.png
   :align: center
   :width: 400px
   :alt: トピックの追加
   
今回は以下のように設定をします。

=============================== ===============
設定項目                        設定値
=============================== ===============
名前                            m_out
トピックの最大サイズ            1GB
メッセージの Time to Live       14日
重複データ検出を有効にする      チェック無し
パーティション分割を有効にする  チェック無し
=============================== ===============

.. image:: images/chcmp06.png
   :align: center
   :width: 400px
   :alt: トピックの作成
   
作成をした m_out のトピックを開きます。ここで、サブスクリプションを作成します。

.. image:: images/chcmp07.png
   :align: center
   :width: 400px
   :alt: サブスクリプションの追加
   
============================ ===========
設定項目                     設定値
============================ ===========
名前                         sitecore
メッセージの Time to Live    14日
ロック期間                   30秒
最大配信数                   1
============================ ===========

.. image:: images/chcmp08.png
   :align: center
   :width: 400px
   :alt: サブスクリプションの作成
  
これで Service Bus の準備完了となります。

************************
Content Hub CMP の設定
************************

スーパーユーザーの作成
=======================

CMP から Azure Servie Bus にメッセージを送るための管理者を作成します。Content Hub の管理画面で、「管理」―「ユーザー」を開いて、「ユーザーの追加」をクリックします。

.. image:: images/chcmp09.png
   :align: center
   :width: 400px
   :alt: ユーザーの追加

ユーザーグループのタブを選択し、「グループメンバーシップ」に `Superusers` を追加してください。

.. image:: images/chcmp10.png
   :align: center
   :width: 400px
   :alt: Superusers の追加

保存をクリックすると、警告が出てきますが、今回は `Superusers` の追加で問題ないので、そのまま続けます。

アカウントのパスワードを設定するために、作成したユーザーのプロファイルの編集を開きます。開いた後、パスワードリセットをするためのメールアドレスを入れてください。

.. image:: images/chcmp11.png
   :align: center
   :width: 400px
   :alt: プロファイルの編集

メールアドレスを設定したあと、「パスワードのリセット」のボタンが有効になるため、これをクリックしてパスワードをリセットします。

.. image:: images/chcmp12.png
   :align: center
   :width: 400px
   :alt: パスワードのリセット

パスワードリセットのメールが、指定したメールアドレスに届きます。メールは迷惑メールに入る可能性もあるため、迷惑メールフォルダも確認をしてください。

.. image:: images/chcmp13.png
   :align: center
   :width: 400px
   :alt: パスワードリセットのメール

パスワードをいれて、新しいパスワードを設定して下さい。

.. image:: images/chcmp14.png
   :align: center
   :width: 400px
   :alt: パスワードリセットの完了

新しいアカウントでログインが可能か確認をしてください。

.. image:: images/chcmp15.png
   :align: center
   :width: 400px
   :alt: パスワードリセットの完了

ユーザー名と設定したパスワードでログインが出来た段階で、管理者アカウントの完成となります。


アクションの作成
=================

Content Hub のアクションを作成します。「管理」－「アクション」を開き、「新規アクション」をクリックします。作成をする際には、形式を Azure Service Bus に変更することで、接続文字列などを入力できるようになります。

============== ===================
設定項目       設定値
============== ===================
名前           sitecore
ラベル 
形式           Azure Service Bus
接続文字列     （後述）
送信タイプ     トピック
送信先         m_out
============== ===================

接続文字列は Microsoft Azure から以下のように取得します。

1. 先ほど作成をした Service Bus の設定を開きます
2. 共有アクセスポリシーを選択します
3. 表示される `RootManageSharedAccessKey` をクリックします
4. プライマリ接続文字列 をコピーしてください

例
.. code-block::

  Endpoint=sb://名前.servicebus.windows.net/;SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=キー

.. image:: images/chcmp16.png
   :align: center
   :width: 400px
   :alt: プライマリ接続文字列

作成するアクションは以下のようになり、テスト接続に成功するか確認をしてください。

.. image:: images/chcmp17.png
   :align: center
   :width: 400px
   :alt: アクションの完成


トリガーの作成
================

続いて Content Hub のコンテンツのステートが変更されたタイミングで、作成をしたアクションが動くようにトリガーを設定します。「管理」－「トリガー」を開いて、「新規トリガー」を作成します。

基本の項目は以下のように今回は設定をします。

============== ===================
設定項目       設定値
============== ===================
名前           SitecoreCMP
目的           エンティティの変更
実行タイプ     バックグラウンドで 
============== ===================

.. image:: images/chcmp18.png
   :align: center
   :width: 400px
   :alt: 基本設定


続いて条件を開き「定義の追加」をクリックします。定義の追加では M.Content をまずは選択します。

.. image:: images/chcmp19.png
   :align: center
   :width: 400px
   :alt: M.Content の選択

続いて、条件を以下の画像のように設定をしてください。

.. image:: images/chcmp20.png
   :align: center
   :width: 400px
   :alt: 条件の選択

最後にアクションタブを選択し、「アクションの追加」をクリックします。ここで、先ほど作成をしたアクションを指定します。ここでは Sitecoreを作成したので、一番下の項目を選択します。

.. image:: images/chcmp21.png
   :align: center
   :width: 400px
   :alt: Sitecore の選択

選択をしたあと、保存をすると、トリガーに合わせてアクションが動くようになります。


************************
Sitecore の設定
************************

Content Hub から Service Bus につながりましたので、次は Service Bus と Content Hub に関する設定を Sitecore 側に追加していきましょう。


Service Bus に関する設定
=========================

Sitecore の設定としては、 /sitecore/system/Modules/CMP/Config にあるアイテムに設定を入れる必要があります。

============================ ===========================
設定項目                     設定値
============================ ===========================
Client Id                    LogicApp   
Client Secret                （後述）
ユーザー名                   作成した管理者名
Password                     作成した管理者のパスワード
Content Hub URI              Content Hub のサーバー URL
Connection String            Service Bus の Endpont 
Incoming topic name          m_out
Incoming subscription name   sitecore
Outgoing topic name          m_in
Default Language             en
============================ ===========================

Client Secret に関しては、Content Hub の管理画面から取得することができます。「管理」－「OAuth クライアント」をクリックして、今回利用する `LogicApp` の鉛筆マークをクリック、クライアントシークレットを取得してください。

.. image:: images/chcmp23.png
   :align: center
   :width: 400px
   :alt: クライアントシークレット

設定した内容は以下のようになります（設定項目は環境に合わせて入力してください）。

.. image:: images/chcmp22.png
   :align: center
   :width: 400px
   :alt: Sitecore の設定


連携アイテムの作成
=======================

今回は Content Hub でブログの記事が投稿された場合に、Sitecore にブログのアイテムが作成される、という設定を追加します。まず、データのテンプレートを作成します。

1. テンプレートとして Blog テンプレートを作成、Title ( Single-line Text ）と Body ( Multi-line Text ）を作成します。

.. image:: images/chcmp24.png
   :align: center
   :width: 400px
   :alt: テンプレートの作成

2. 作成したテンプレートの「コンテンツタブ」を開いて、テンプレートのデータとして、Templates/CMP/Content Hub Entity のテンプレートを追加します。

.. image:: images/chcmp25.png
   :align: center
   :width: 400px
   :alt: テンプレートデータの追加

3. 続いてバケットを作成します。 `/sitecore/content/CMP` アイテムを右クリックして、バケットをつ追加します。

.. image:: images/chcmp26.png
   :align: center
   :width: 400px
   :alt: バケットの追加

4. 名前を今回は Blogs と指定します

.. image:: images/chcmp27.png
   :align: center
   :width: 400px
   :alt: ブログの作成

5. `/sitecore/system/Modules/CMP/Config` のアイテムを右クリックして、 `Entity Mapping` のアイテムを作成します。

.. image:: images/chcmp28.png
   :align: center
   :width: 400px
   :alt: エンティティマッピングの追加

6. Blog を作成
7. 作成した Blog アイテムを右クリックして、 `field Mapping` を作成します。今回は、`Body` と `Title` の２つを作成します。完成下ツリーは以下の通り。

.. image:: images/chcmp29.png
   :align: center
   :alt: ツリー構造

8. Blog アイテムには、以下の項目を設定します。

================ =============================
設定項目         設定値
================ =============================
Content Type Id  M.ContentType.Blog   
バケット         事前に作成をしたバケット
テンプレート     事前に作成をしたテンプレート
================ =============================

.. image:: images/chcmp30.png
   :align: center
   :width: 400px
   :alt: データの設定

9. Body と Title に関しては、Content Hub のフィールド名と作成をしたテンプレートのフィールド名のマッピングを設定します。今回は以下のように設定をします。

.. image:: images/chcmp31.png
   :align: center
   :width: 400px
   :alt: Body の設定

.. image:: images/chcmp32.png
   :align: center
   :width: 400px
   :alt: Title の設定

これで設定は一通り完了しました。なお、設定を反映させるためには Sitecore を一度再起動する必要があります。

************************
連携の確認
************************

実際に正しく動作しているか、確認をします。まず、作成した段階では何も Blogs のアイテムに含まれていないのを確認します。

.. image:: images/chcmp33.png
   :align: center
   :width: 400px
   :alt: 空のブログバケット

Content Hub にアクセスをして、右上にある「＋コンテンツ」のボタンをクリックします。

.. image:: images/chcmp34.png
   :align: center
   :width: 400px
   :alt: コンテンツの追加

今回はブログの設定をしているだけなので、コンテンツのタイプとして「ブログ」を選択します（ダイアログ一番下の項目）。

.. image:: images/chcmp35.png
   :align: center
   :width: 400px
   :alt: コンテンツの追加

右上にある「編集」ボタンをクリックします。

.. image:: images/chcmp36.png
   :align: center
   :width: 400px
   :alt: コンテンツの追加

タイトル、記事の入力エリアが有効になります。今回はテストのため簡単な記事を入れておきます。
   
.. image:: images/chcmp37.png
   :align: center
   :width: 400px
   :alt: コンテンツを入力

保存をして、ワークフローに関して「公開」まで進めていきます。しばらくすると、Sitecore にブログのアイテムが作成される、という設定を追加します。まず、データのテンプレートを作成します。

.. image:: images/chcmp38.png
   :align: center
   :width: 400px
   :alt: アイテムの完成

バケットの中にあるアイテムを参照するために、コンテンツエディターの「表示」エリアから「バケット」をチェックしますｓ。

.. image:: images/chcmp39.png
   :align: center
   :width: 400px
   :alt: バケットの確認

表示ができるモードに切り替わると、ツリービュー形式でアイテムを確認することができるようになります。

.. image:: images/chcmp40.png
   :align: center
   :width: 400px
   :alt: アイテムが表示さえる

表示されたアイテムを選択すると、Content Hub で入力された情報が反映されていることを確認できます。
   
.. image:: images/chcmp41.png
   :align: center
   :width: 400px
   :alt: アイテムの確認


このように、Content Hub で作成した情報を Sitecore で利用することができるようになります。