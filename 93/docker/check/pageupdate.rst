##########################
ページの更新
##########################


Sitecore は管理サーバー側で作業をして、ページの更新手続きをすると公開サーバーが変更される、という運用になります。今回はページの更新を実行します。まず、管理サーバーにログインをします（ /sitecore を URL に追加してください）。

.. image:: images/container05.png
   :align: center
   :width: 400px
   :alt: ログイン

管理者でログインをした後、`Content Editor` を開き、Home のアイテムを編集します。

.. image:: images/container06.png
   :align: center
   :width: 400px
   :alt: 管理画面

.. image:: images/container07.png
   :align: center
   :width: 400px
   :alt: Content Editor
   
.. image:: images/container08.png
   :align: center
   :width: 400px
   :alt: Home アイテムの編集

編集が終わったあと、保存、Publish を実行します（Publishing は Smart Publish を実行）。

.. image:: images/container09.png
   :align: center
   :width: 400px
   :alt: Smart Publish

.. image:: images/container10.png
   :align: center
   :width: 400px
   :alt: 公開完了

CD にアクセスしているページを再読込します。

.. image:: images/container11.png
   :align: center
   :width: 400px
   :alt: 更新完了

on Docker がタイトルに追加されており、ページが更新されていることを確認できました。

.. image:: images/container12.png
   :align: center
   :width: 400px
   :alt: on Docker が追加されています。
