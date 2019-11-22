#####################################
Sitecore Connect for Sitecore DAM
#####################################

.. todo:: 本文書は Sitecore 9.3 リリース後に更新予定です。

Sitecore Connect for Sitecore DAM 2.0.0  を利用することで、Sitecore の管理画面から直接 Content Hub で管理している画像を指定するようになります。ここではモジュールのインストールと動作検証まで紹介をします。

**************************
必要システム
**************************

Sitecore Connect for Sitecore DAM 2.0.0 は以下のシステムで利用することができます。

* Sitecore Experience Platform 9.2
* Sitecore Experience Platform 9.1.0, 9.1.1

なお、Sitecore Experience Manager、 Sitecore Experience Commerce でも上記のバージョンであればご利用いただけます。

****************************
Sitecore Content Hub の設定
****************************

まず最初に、Sitecore Experience Platform と Sitecore Content Hub の接続ができるように、設定を Sitecore Content Hub に追加していきます。

* 管理者の権限を持っているアカウントで Sitecore Content Hub にアクセスをして、「管理」―「設定」を開きます。
* 左側のメニューの`PortalConfiguratoin` をクリックします
* `CORSConfiguration` をクリックして設定画面を開きます
* 管理サーバーの URL を入力して保存をクリックします

.. image:: images/chdam04.png
   :align: center
   :width: 400px
   :alt: サーバー情報を追加

続いてログイン方法に関して、今回はシングルサインオン以外でログインをするために、ログインの設定を変更します。

* 管理者の権限を持っているアカウントで Sitecore Content Hub にアクセスをして、「管理」―「設定」を開きます。
* 左側のメニューの`Authentication` をクリックします
* 設定の表示を `Tree` から `Text` に変更します。

.. image:: images/chdam05.png
   :align: center
   :alt: テキストに切り替え

* ログインの設定で提供されている項目から、authentication_mode を “Passive” に変更します。また ExternalRedirectKeys を追加してください。追加した結果は以下のようになります。

.. code-block:: json

  {
  "Providers": [
    {
      "$type": "Stylelabs.M.Portal.Authentication.SamlAuthenticationProviderConfigurator, Stylelabs.M.Portal",
      "metadata_location": "---------------------",
      "sp_entity_id": "---------------------",
      "idp_entity_id": "-------------------------",
      "provider_name": "SSO",
      "authentication_mode": "Passive",
      "module_path": "AuthServices",
      "is_enabled": true
    }
  ],
  "ExternalRedirectKeys": {
    "Sitecore": "https://92sc.dev.local/"
  }
  }

変更しているのは2か所です、確認をして保存します。

*************************************
Sitecore Experience Platform の設定
*************************************

モジュールのダウンロード


続いて Sitecore の設定を開始します。まず、以下のページからモジュールのダウンロードをします。

* `Sitecore Connect for Sitecore DAM 2.0.0 <https://dev.sitecore.net/Downloads/Sitecore_Plugin_for_Stylelabs_DAM/20/Sitecore_Connect_for_Sitecore_DAM_200.aspx>`_

この解説では `Sitecore Connect for Sitecore DAM` をダウンロードしてインストールを進めます。

モジュールのインストール
========================

モジュールのインストールは、「コントロールパネル」－「パッケージをインストールする」を開いてください。

.. image:: images/chdam01.png
   :align: center
   :width: 400px
   :alt: ファイルを指定する

次へ、をクリックすると以下のような警告が出ます。

.. image:: images/chdam02.png
   :align: center
   :width: 400px
   :alt: アイテムに関する警告

上書きを選択した後、全てに適用をクリックしてください。しばらくすると、インストールが完了します。

.. image:: images/chdam03.png
   :align: center
   :width: 400px
   :alt: インストールが完了

続いて以下の手続きを実行します。

日本語リソースの追加
========================

日本語リソースは標準で入っていないため、以下から `20-damtoolbar-ja-jp.xml` をダウンロードしてください。

* https://github.com/SitecoreJapan/InstallScript/tree/master/ContentHub/DAM

このリソースは、 Core データベースに追加することで、日本語の表記を修正する形となります。


モジュールの設定
=====================

コンテンツエディターを開いて、`/sitecore/system/Modules/DAM/Config/DAM connector` のアイテムを選択します。

.. image:: images/chdam06.png
   :align: center
   :width: 400px
   :alt: アイテムの選択

日本語バージョンを追加して（共有リソースのため、英語で設定しても同じです）、DAM のインスタンス、検索ページ、Content Hub の Authentication で設定をした ExternalRedirectKeys のキーを設定します。

.. image:: images/chdam07.png
   :align: center
   :width: 400px
   :alt: アイテムの選択

これで設定は完了となります。

**********
動作確認
**********

リッチテキストエディタを利用して、Sitecore Content Hub にアクセスできるか確認をします。

1. インストールすると標準で用意されている `/sitecore/content/Home` のアイテムをコンテンツエディタで選択します。
2. `エディターで表示する` をクリックします

.. image:: images/chdam08.png
   :align: center
   :width: 400px
   :alt: エディタを表示

3. リッチテキストエディタにボタンが増えていることを確認します（左から５つめ）

.. image:: images/chdam09.png
   :align: center
   :width: 400px
   :alt: リボンを確認

4. ボタンをクリックします。ログイン画面が表示された場合は、Sitecore Content Hub のアカウントでログインをしてください。
5. DAM に登録されているアセットが表示されます。

.. image:: images/chdam10.png
   :align: center
   :width: 400px
   :alt: アセットを確認

6. 公開リンクのついているアイテムを選択します

.. image:: images/chdam11.png
   :align: center
   :width: 400px
   :alt: アセットの選択

7. 利用するアセットを選択すると、挿入された画面を確認することができます。

.. image:: images/chdam12.png
   :align: center
   :width: 400px
   :alt: 画像の挿入

OK を押して保存をして、画像のリンクが有効になっていれば、動作検証が完了となります。
