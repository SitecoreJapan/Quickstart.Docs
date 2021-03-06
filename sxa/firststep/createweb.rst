#############################
テナントの作成、サイトの作成
#############################

Sitecore は複数の Web サイトを管理することができる仕組みとなっています。この際、サイト間で情報共有をしたい場合は、同じテナントの下に Web サイトを作成することで簡単に共有することができます。

ここではテナントの作成方法について、紹介をします。

****************
テナントの作成
****************

ログインをしたあと、コンテンツエディターを立ち上げてください。コンテンツエディターを立ち上げたあとアイテムとして Sitecore - コンテンツ が表示されているので、ここで右クリックをするとメニューが出てきます。メニューの項目から「挿入」を選択すると下のように挿入することができるアイテムとして「テナント」が表示されます。

.. image:: images/tenant01.png
   :align: center
   :width: 400px
   :alt: テナント作成


実行をすると、テナントを作成するにあたって必要となる設定項目が表示されます。ここではテナント名を `QuickStart` と設定します。モジュールに関しては今回はすべて選択します。

.. image:: images/tenant02.png
   :align: center
   :width: 400px
   :alt: ダイアログ


完了すると、テナントのアイテムが作成されます。このテナントで利用するtンプレート、テーマ、メディアライブラリの場所などがアイテムで定義されています。

.. image:: images/tenant03.png
   :align: center
   :width: 400px
   :alt: テナントの完成


これでテナントは完成しました。

****************
サイトの作成
****************

テナントの下にはサイトを構築することができます。今回は、作成をしたテナントを右クリックをしてサイトを追加するメニューを表示します。

.. image:: images/site01.png
   :align: center
   :width: 400px
   :alt: サイトの作成



暫くすると以下のようなダイアログが表示されます。

.. image:: images/site02.png
   :align: center
   :width: 400px
   :alt: ダイアログ


今回は以下のように設定していきます。

================ =======
設定項目         値 
================ =======
サイト名         demo 
ホスト名         * 
仮想フォルダー    / 
言語             ja-jp 
================ =======

設定をすると、以下のようになります。

.. image:: images/site03.png
   :align: center
   :width: 400px
   :alt: 一般設定


続いてタブを切り替えて設定を追加していきます。モジュールはすべてのモジュールを選択しておきます。

.. image:: images/site04.png
   :align: center
   :width: 400px
   :alt: モジュール設定


次にテーマのタブに切り替えます。ここでは、「新しいテーマを作成」のチェックボックスをチェック、またテーマとして「Basic2」と「Wireframe」を選択します。

.. image:: images/site05.png
   :align: center
   :width: 400px
   :alt: テーマの設定


最後にグリッドの設定ですが、標準で設定できる Bootstrap 4 を選択します。

.. image:: images/site06.png
   :align: center
   :width: 400px
   :alt: グリッド


上記の設定を確認しあと、OK ボタンを押すとサイトに必要な情報の入ったサイトが出来上がります。

.. image:: images/site07.png
   :align: center
   :alt: サイトの完成


これで、空っぽの Web サイトが出来上がりました。


*************
参考動画
*************

.. raw:: html

    <iframe width="560" height="315" src="https://www.youtube.com/embed/bKz7riJGqa0" frameborder="0" allowfullscreen></iframe>

