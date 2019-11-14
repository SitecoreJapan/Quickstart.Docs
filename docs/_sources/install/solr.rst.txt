Solr のインストール
================================

Sitecore Experience Platform は検索エンジンとして Solr を利用しています。インストールの前に、サービスとして起動している必要があります。

Solr をサービスとして立ち上げるためにはいくつか手順がありますが、今回はなるべく少ない手間でインストールすることができるように、PowerShell のスクリプトを利用します。

Java のインストール
*****************************

今回は OpenJDK をダウンロードしてインストールします。

* `OpenJDK <https://openjdk.java.net/>`_ にアクセス
* 左側にある「Installing」のメニューをクリック
* JDK 9 & Later の説明文の中にある jdk.java.net のリンクをクリック
* Ready for use: JDK 13 を選択
* Windows / x64	の zip ファイルをダウンロードします

.. image:: images/jdk01.png
   :align: center
   :width: 400px
   :alt: ダウンロード

ダウンロードが完了した後、以下のように展開します。

* ダウンロードをしたファイルを右クリック、「すべて展開」をクリックします

.. image:: images/jdk02.png
   :align: center
   :width: 400px
   :alt: 展開

* ダイアログの「参照」ボタンをクリックして、フォルダを指定します

.. image:: images/jdk03.png
   :align: center
   :width: 400px
   :alt: 参照

* c:\Program Files のフォルダを指定します

.. image:: images/jdk04.png
   :align: center
   :width: 400px
   :alt: フォルダ指定

* 「新しいフォルダー」をクリックして、表示されるダイアログで「続行」をクリックします。

.. image:: images/jdk05.png
   :align: center
   :width: 400px
   :alt: 権限の変更

* フォルダ名として「Java」を作成して選択をします。

.. image:: images/jdk06.png
   :align: center
   :width: 400px
   :alt: Java フォルダ


* 展開をクリックすると、改めて権限に関するダイアログが表示されます。これも「続行」をクリックします。

.. image:: images/jdk07.png
   :align: center
   :width: 400px
   :alt: 権限の変更

* ファイルが展開されます

.. image:: images/jdk08.png
   :align: center
   :width: 400px
   :alt: 展開


* 展開が完了後、フォルダ名を jre に変更します。

.. image:: images/jdk09.png
   :align: center
   :width: 400px
   :alt: フォルダ名の変更


OpenSSL のインストール
*****************************

以下のサイトから OpenSSL をダウンロードします。

* `Shining Light Productions <https://slproweb.com/products/Win32OpenSSL.html>`_

.. image:: images/openssl01.png
   :align: center
   :width: 400px
   :alt: ダウンロード

この文書では、Win64 OpenSSL v1.1.1d のバージョンをダウンロード、インストールしました。特別な手順はありません。最後に寄付のお願いが表示されますので、任意で寄付をしていただくと喜ばれると思います。

Path の調整
*****************************

Java および OpenSSL をインストールした後、実際にコマンドラインで実行できるように Path を追加します。Path の情報はシステムから書き込むことができます。ここでは以下のような手順で進めていきます。

* 検索ボックスで「システムの詳細設定」と入力し、右側に表示されているツールの下の「開く」をクリックします。

.. image:: images/path01.png
   :align: center
   :width: 400px
   :alt: システムの詳細設定

* 「詳細設定」タブにある「環境変数」をクリックします。

.. image:: images/path02.png
   :align: center
   :width: 400px
   :alt: 環境変数

* 下部にある「システム環境変数」のエリアの「新規」をクリックして新しい環境変数を追加します。

.. image:: images/path03.png
   :align: center
   :width: 400px
   :alt: 新規

* 変数名 `JAVA_HOME`、変数値に関しては「ディレクトリの参照」のボタンをクリックして、`C:\\Program Files\\java\\jre` を指定して、OK をクリックします。

.. image:: images/path04.png
   :align: center
   :width: 400px
   :alt: 新規追加

* Path を選択したあと、「編集」ボタンをクリックします。

.. image:: images/path05.png
   :align: center
   :width: 400px
   :alt: 編集

* `C:\Program Files\java\jre` と `C:\\Program Files\\OpenSSL-Win64` を追加します。

.. image:: images/path06.png
   :align: center
   :width: 400px
   :alt: ２つの Path を追加

* OK を押して終了します


PowerShell の実行権限の変更
*****************************

Solr をインストールするために、PowerShell の実行権限を確認します。検索ボックスで「PowerShell」と入力して、Windows PowerShell のツールを「管理者として実行する」を選択して起動します。

.. image:: images/solr02.png
   :align: center
   :width: 400px
   :alt: PowerShell の起動

続いて、`Get-ExecutionPolicy` のコマンドを実行します。 ::

   PS C:\Windows\system32> Get-ExecutionPolicy
   Restricted

Windows 10 では標準で `Restricted` で設定されています。このため、通常では PowerShell のスクリプトを実行することができません（詳しくは `About Execution Policies <https://docs.microsoft.com/ja-jp/powershell/module/microsoft.powershell.core/about/about_execution_policies?view=powershell-6>`_ を参照）。

ポリシーを変更するためには、`Set-ExecutionPolicy` のコマンドで変更をすることができます。今回はローカルのファイルのみ OK ということにするため、`RemoteSigned` を設定します。 ::

  PS C:\Windows\system32> Set-ExecutionPolicy RemoteSigned
  
  実行ポリシーの変更
  実行ポリシーは、信頼されていないスクリプトからの保護に役立ちます。実行ポリシーを変更すると、about_Execution_Policies
  のヘルプ トピック (https://go.microsoft.com/fwlink/?LinkID=135170)
  で説明されているセキュリティ上の危険にさらされる可能性があります。実行ポリシーを変更しますか?
  [Y] はい(Y)  [A] すべて続行(A)  [N] いいえ(N)  [L] すべて無視(L)  [S] 中断(S)  [?] ヘルプ (既定値は "N"): y
  PS C:\Windows\system32> Get-ExecutionPolicy
  RemoteSigned
  PS C:\Windows\system32>


これでダウンロードをした PowerShell のファイルを実行できるようになりました。

Solr スクリプトの実行
*****************************

Solr のインストールスクリプトを SitecoreJapan の GitHub からダウンロードをして、`c:\projects\solr` のフォルダにコピーをします。

* `SitecoreJapan/InstallScript <https://github.com/SitecoreJapan/InstallScript/tree/master/solr>`_

.. image:: images/solr01.png
   :align: center
   :width: 400px
   :alt: PowerShell スクリプトのダウンロード

* PowerShell を立ち上げて、`.\install-solr-7.5.0.ps1` とパスを指定してください。

.. image:: images/solr03.png
   :align: center
   :width: 400px
   :alt: PowerShell の起動

* 実行をすると、必要なモジュールをダウンロードしてセットアップを進めていきます

.. image:: images/solr04.png
   :align: center
   :width: 400px
   :alt: Solr インストールスクリプトの実行

* インストールが完了すると、ブラウザが立ち上がって Solr の管理画面が表示されます。

.. image:: images/solr05.png
   :align: center
   :width: 400px
   :alt: 管理画面

Solr のインストールが完了すると、Sitecore のインストールを進める形となります。
