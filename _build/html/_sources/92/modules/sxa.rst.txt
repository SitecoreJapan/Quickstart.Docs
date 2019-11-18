#####################################
Sitecore Experience Accelerator
#####################################

Sitecore Experience Accelerator 1.9.0 モジュールのインストールについて紹介をしています。

*************************
モジュールのダウンロード
*************************

モジュールに関しては、Sitecore Download サイトから入手することができます。

* `Sitecore Experience Accelerator 1.9.0 <https://dev.sitecore.net/Downloads/Sitecore_Experience_Accelerator/19/Sitecore_Experience_Accelerator_190.aspx>`_ 

    * Sitecore Experience Accelerator for 9.2
    * Sitecore PowerShell Extension 5.0 for Sitecore 9.2

上記のモジュールをダウンロードした後、次のステップに進みます。

****************************
モジュールのインストール
****************************

モジュールのインストールは以下の手順で進めていきます。

* 管理者の権限でログインをします
* スタート画面からコントロールパネルを選択
* 「管理」グループにある `パッケージをインストールする` を選択します

.. image:: images/jss02.png
   :align: center
   :width: 400px
   :alt: パッケージをインストールする

* まず最初に、`Sitecore PowerShell Extension 5.0 for Sitecore 9.2` のファイルをアップロードします。

.. image:: images/sxa01.png
   :align: center
   :width: 400px
   :alt: PowerShell モジュール

* インストールを実行します
* 続いて `Sitecore Experience Accelerator for 9.2` のファイルをアップロードします。

.. image:: images/sxa02.png
   :align: center
   :width: 400px
   :alt: SXA モジュール

* インストールを完了させます。

*************************
日本語リソースの追加
*************************

Sitecore Experience Accelerator はコンポーネントに関する日本語リソースが提供されていますが、自動的にインポートされることはありません。このため、以下の手順でインポートをしてください。

* `グローバリゼーション` エリアの `言語ファイルをインポートする` をクリック
* モジュールのインストールが完了した後、 /temp/SXAtranslations のフォルダに `ja-JP.xml` が展開されているため、そのファイルを指定します。

.. image:: images/sxa03.png
   :align: center
   :width: 400px
   :alt: 日本語リソース

* データベースとして `core` を対象としてインポートをします。

上記で Sitecore Experience Accelerator のインストールは完了となります。

***************
次のステップ
***************

インストールが完了したあと、簡単な使い方を説明している :doc:`Sitecore Experience Accelerator クイックガイド</sxa/index>` を参考にしてください。
