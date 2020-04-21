#############################
Sitecore Azure Toolkit 2.4
#############################

Sitecore は Microsoft Azure の PaaS に対応しており、展開方法としては Marketplace および Azure Toolkit を利用した展開ができるようになっています。ここでは Azure Toolkit を利用して展開する手順に関してまとめています。詳細に関しては、このページの一番下にある参考サイトをご覧ください。

*********************************
展開をするにあたって準備するもの
*********************************

以下のモジュールをダウンロードしてください。

* `Download options for Azure AppService - Packages for XP Single <https://dev.sitecore.net/Downloads/Sitecore_Experience_Platform/93/Sitecore_Experience_Platform_93_Initial_Release.aspx>`_
* `Sitecore Identity 4.0.0 <https://dev.sitecore.net/Downloads/Sitecore%20Identity/4x/Sitecore%20Identity%20400>`_
* `Sitecore Azure Toolkit 2.4.0 <https://dev.sitecore.net/Downloads/Sitecore_Azure_Toolkit/2x/Sitecore_Azure_Toolkit_240.aspx>`_
* `Sitecore-Azure-Quickstart-Templates <https://github.com/Sitecore/Sitecore-Azure-Quickstart-Templates>`_
 
Sample Powershell Script に関しては、README.md の中に含まれているためファイルはありません。新たに ps1 のファイルを作成してください。

*********************************
テンプレートのダウンロード
*********************************

必要なファイルだけダウンロードすることで、実際のインストールは可能ですが、今回はすべて手元にクローンを作成してから作業を進めていきます。

まず、Github で公開されている `Sitecore-Azure-Quickstart-Templates <https://github.com/Sitecore/Sitecore-Azure-Quickstart-Templates>`_ のクローンを作成します。クローンの作成先は今回は以下のフォルダとします。

.. code-block::

  C:\projects\Sitecore-Azure-Quickstart-Templates


.. image:: images/atk01.png
   :align: center
   :width: 400px
   :alt: リポジトリのクローンを作成


*******************************************
Microsoft Azure Powershell のインストール
*******************************************

Microsoft Azure Powershell をインストールします。PowerShell のコンソールを開いて、以下のコマンドを実行してください。

.. code-block:: Powershell

    Install-Module -Name AzureRM -AllowClobber


.. image:: images/Azinstall01.png
   :align: center
   :width: 400px
   :alt: Microsoft Azure Powershell をインストール

またこれとは別に Web Deploy 3.6 for Hosting Service も併せてインストールしてください。

********************************
Sitecore Azure Toolkit の展開
********************************

ダウンロードをした Sitecore Azure Toolkit を以下のフォルダに展開します。

.. code-block::

  C:\projects\sitecoreonazure

展開した後のファイル構成は以下のようになっています。

.. code-block::

  Windows PowerShell
  Copyright (C) Microsoft Corporation. All rights reserved.

  PS C:\Users\Administrator> cd \projects\sitecoreonazure
  PS C:\projects\sitecoreonazure> dir


      ディレクトリ: C:\projects\sitecoreonazure


  Mode                LastWriteTime         Length Name
  ----                -------------         ------ ----
  d-----       2019/12/13     12:57                Copyrights
  d-----       2019/12/13     12:57                resources
  d-----       2019/12/13     12:57                tools
  ------       2019/11/25     12:28           3109 README.txt
  ------       2019/11/25     12:28          22528 SitecoreLicense.html
  ------       2019/11/25     12:32           1532 version.txt


続いて、`Import-Module .\\tools\\Sitecore.Cloud.Cmdlets.psm1 -Verbose` のコマンドを実行します。

.. code-block::

  PS C:\projects\sitecoreonazure> Import-Module .\tools\Sitecore.Cloud.Cmdlets.psm1 -Verbose
  詳細: パス 'C:\projects\sitecoreonazure\tools\Sitecore.Cloud.Cmdlets.psm1' からモジュールを読み込んでいます。
  詳細: コマンドレット 'New-SCCargoPayload' をインポートしています。
  詳細: 関数 'ConvertTo-SitecoreWebDeployPackage' をインポートしています。
  詳細: 関数 'Set-SitecoreAzureTemplates' をインポートしています。
  詳細: 関数 'Start-SitecoreAzureDeployment' をインポートしています。
  詳細: 関数 'Start-SitecoreAzureModulePackaging' をインポートしています。
  詳細: 関数 'Start-SitecoreAzurePackaging' をインポートしています。
  PS C:\projects\sitecoreonazure>

これでツールの準備ができました。


***********************
ファイルの準備
***********************

以下のファイルを `C:\\projects\\sitecoreonazure` のフォルダに準備してください。

* ライセンスファイル
* 証明書 

証明書がない場合は、 `自己証明書の作成手順 <https://doc.sitecore.com/developers/93/sitecore-experience-manager/en/the-client-certificate-for-sitecore-deployments.html>`_ を参考にしてください。

続いて Azure の Blob にすでにダウンロード済のファイルを展開して、アップロードをします。必要なモジュールをアップロードして、インストールの際に利用できるようにしておきます。

.. image:: images/azureblob.png
   :align: center
   :width: 400px
   :alt: ファイルをアップロード


パラメーターのファイルに関して、今回は XP Single のイメージを利用するため、 C:\\projects\\Sitecore-Azure-Quickstart-Templates\\Sitecore 9.3.0\\XPSingle にある azuredeploy.parameters.json をコピーしてください。


************************************
実行ファイル、パラメーターの設定
************************************

展開のスクリプトファイル `azuretoolkit240.ps1 <https://github.com/SitecoreJapan/InstallScript/tree/master/930>`_ に関して、以下のパラメーターを変更してください。

.. code-block::

  # Specify the parameters for the deployment 
  $ArmTemplateUrl = "https://raw.githubusercontent.com/Sitecore/Sitecore-Azure-Quickstart-Templates/master/Sitecore%209.3.0/XPSingle/azuredeploy.parameters.json"
  $ArmParametersPath = ".\azuredeploy.parameters.json"
  $licenseFilePath = ".\license.xml"

  # Specify the certificate file path and password if you want to deploy Sitecore 9.0 XP or XDB configurations
  $certificateFilePath = "C:\projects\sitecoreonazure\sitecoreonazuredemo.pfx" 
  $certificatePassword = "qwer1234"
  $certificateBlob = $null

  $Name = "jpn-tokyo-sitecore-deploy930"
  $location = "JAPAN WEST"
  $AzureSubscriptionId = ""


===================== =======================================================================
パラメーター          内容  
===================== =======================================================================
$ArmTemplateUrl       標準のセットアップを考えているため、Github にある展開ファイルを設定 
$ArmParametersPath    Github からダウンロードした対象となるパラメーターファイル 
$licenseFilePath      ライセンスファイルのパスを設定 
$certificateFilePath  証明書のファイルのパス 
$certificatePassword  上記の証明書のパスワード 
$Name                 展開するリソースグループ名 
$location             展開するデータセンター名 
$AzureSubscriptionI   Azure Subscription の ID 
===================== =======================================================================


続いてパラメータファイルを設定しますが、 `azuredeploy.parameters.json` には Azure のストレージ、Blob にアップロードしているパッケージの URL を指定してください。

=========================== ===========================================
パラメーター                  内容 
=========================== ===========================================
location                    展開するデータセンター（ Japan West ) 
sitecoreAdminPassword       管理者パスワード  
sqlServerLogin              SQL Server ログイン名 
sqlServerPassword           SQL Server ログインパスワード 
siMsDeployPackageUrl        Sitecore Identity Server のパッケージ URL 
singleMsDeployPackageUrl    Sitecore のパッケージ URL 
xcSingleMsDeployPackageUrl  Sitecore xConnect のパッケージ URL 
=========================== ===========================================


****************
展開を実行する
****************

上記のように準備した後、あとはスクリプトを実行するのみです。まずは Powershell のコンソールから Azure にログインを実行します。

.. code-block::

  PS C:\projects\sitecoreonazure> Add-AzureRmAccount

続いて作成したスクリプトを実行すれば完了となります。

.. code-block::

  PS C:\projects\sitecoreonazure> .\deploy93.ps1

上記の設定がすべてクリアできていれば、40分ほどで展開が完了します。

***********
参考サイト
***********

* `Sitecore Azure Toolkit モジュールダウンロード <https://dev.sitecore.net/Downloads/Sitecore_Azure_Toolkit.aspx>`_
* Github `Sitecore-Azure-Quickstart-Templates <https://github.com/Sitecore/Sitecore-Azure-Quickstart-Templates>`_
* `Sitecore Azure Toolkit <https://doc.sitecore.com/developers/sat/20/sitecore-azure-toolkit/en/sitecore-azure-toolkit.html>`_
