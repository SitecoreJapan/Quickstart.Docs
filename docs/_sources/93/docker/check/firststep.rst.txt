####################
インストール後の処理
####################

インストール後の最初の処理を実行してみます。

**********************
インデックスの更新
**********************

`Control Panel` の `Indexing` にある `Populate Solr Managed Schema` を開きます。

.. image:: images/firststep01.png
   :align: center
   :width: 400px
   :alt: スキーマの設定

ダイアログの右下にある `Populate` のボタンをクリックして実行します。

.. image:: images/firststep02.png
   :align: center
   :width: 400px
   :alt: Populate

.. image:: images/firststep03.png
   :align: center
   :width: 400px
   :alt: 実行中

しばらくすると、処理が完了します。

.. image:: images/firststep04.png
   :align: center
   :width: 400px
   :alt: 処理の完了

続いて `Indexing` にある `Indexing Manager` を開きます。

.. image:: images/firststep01.png
   :align: center
   :width: 400px
   :alt: Indexing Manager

すべての項目をチェックして、Rebuild を実行します。

.. image:: images/firststep05.png
   :align: center
   :width: 400px
   :alt: インデックス一覧

.. image:: images/firststep06.png
   :align: center
   :width: 400px
   :alt: Rebuild 中

完了すると以下のような画面になります。

.. image:: images/firststep07.png
   :align: center
   :width: 400px
   :alt: Rebuild 中

続いて、Database にある `Rebuild link databases` を開きます。

.. image:: images/firststep01.png
   :align: center
   :width: 400px
   :alt: Rebuild link databases

Rebuild したいデータベースを選択して、実行します。

.. image:: images/firststep08.png
   :align: center
   :width: 400px
   :alt: Rebuild link databases

インデックス関連に関しては、これで手続きは終了となります。

************************
マーケティング定義の展開
************************

マーケティングに関する必要な設定を展開します。Analytics にある `Deploy marketing definitions` を開きます。

.. image:: images/firststep01.png
   :align: center
   :width: 400px
   :alt: Deploy marketing definitions 

ダイアログに表示されている項目を全て選択している状態で、`Deploy` ボタンをクリックしてください。

.. image:: images/firststep09.png
   :align: center
   :width: 400px
   :alt: Deploy marketing definitions 

.. image:: images/firststep10.png
   :align: center
   :width: 400px
   :alt: 設定完了画面 

これで Sitecore の設定自体は終了となります。