################################################
Sitecore Containers を利用してインストール
################################################

********************************
ファイルのダウンロード
********************************

Sitecore を Docker に展開するための定義ファイルを Sitecore Download にて提供しています。

ページの項目で、Download options for Sitecore Container deployments にある Container Deployment Package のファイルをダウンロードしてください。

.. image:: images/container01.png
   :align: center
   :width: 400px
   :alt: ファイルのダウンロード

ファイル名は SitecoreContainerDeployment 10.0.0 rev. 004346-027.zip になります。

ファイルをダウンロードしたら、以下のディレクトリに展開をします。

c:\\projects\container

展開したディレクトリに作成された、以下のディレクトリに PowerSHell で移動します。

C:\\projects\\container\\ltsc2019\\sitecore-xp0

********************************
.env ファイルの編集
********************************

インストールをする環境定義ファイルとなる .env ファイルを編集する必要があります。デフォルトでは以下のようになっています。

.. code-block:: 

    COMPOSE_PROJECT_NAME=sitecore-xp0
    SITECORE_DOCKER_REGISTRY=scr.sitecore.com/sxp/
    SITECORE_VERSION=10.0.0-ltsc2019
    SITECORE_ADMIN_PASSWORD=
    SQL_SA_PASSWORD=
    TELERIK_ENCRYPTION_KEY=
    SITECORE_IDSECRET=
    SITECORE_ID_CERTIFICATE=
    SITECORE_ID_CERTIFICATE_PASSWORD=
    SITECORE_LICENSE=
    CM_HOST=xp0cm.localhost
    ID_HOST=xp0id.localhost
    TRAEFIK_IMAGE=traefik:v2.2.0-windowsservercore-1809
    TRAEFIK_ISOLATION=hyperv
    ISOLATION=default

サーバー名となる CM_HOST および ID_HOST を変更する場合は、このファイルから直接変更をしてください。

続いて PowerShell で一括で変更することができる init.ps1 のファイルを Github からダウンロードしてください。

https://github.com/Sitecore/docker-examples/blob/develop/getting-started/init.ps1

ダウンロードした init.ps1 ファイルを展開したフォルダの中にコピーしてください。

C:\\projects\\container\\ltsc2019\\sitecore-xp0

.. image:: images/container02.png
   :align: center
   :width: 400px
   :alt: ファイルのダウンロード

続いて、init.ps1 のファイルに記載されている $SitecoreAdminPassword と $SqlSaPassword を変更します。

.. code-block:: powershell

    [CmdletBinding()]
    Param (
        [Parameter(Mandatory = $true)]
        [string]
        [ValidateNotNullOrEmpty()]
        $LicenseXmlPath,
        
        # We do not need to use [SecureString] here since the value will be stored unencrypted in .env,
        # and used only for transient local example environment.
        [string]
        $SitecoreAdminPassword = "Pleasechang3p@ssword",
        
        # We do not need to use [SecureString] here since the value will be stored unencrypted in .env,
        # and used only for transient local example environment.
        [string]
        $SqlSaPassword = "Pleasechang3p@ssword"
    )

必要な変更がをしたあと、PowerShell の管理者権限で init.ps1 を実行してください。

ライセンスファイルの場所を指定する必要があるため、事前に同じフォルダにファイルをコピーしておき、ファイルを指定してください。

.. image:: images/container03.png
   :align: center
   :width: 400px
   :alt: init.ps1 実行

処理が終わったタイミングで、 .env ファイルには必要となる更新が完了しています。

********************************
docker-compose の実行
********************************

設定が完了した段階で、以下のコマンドを実行してください。

.. code-block:: 

   docker-compose.exe up --detach

自動的にイメージのダウンロードをして、Docker イメージが構成されていきます。

.. code-block:: 

    PS C:\projects\container\ltsc2019\sitecore-xp0> dir


        Directory: C:\projects\container\ltsc2019\sitecore-xp0

    Mode                 LastWriteTime         Length Name
    ----                 -------------         ------ ----
    d----          2020/09/29    13:53                mssql-data
    d----          2020/09/29    13:52                solr-data
    d----          2020/09/29    12:45                traefik
    -a---          2020/09/29    13:30          17730 .env
    -----          2020/07/15     8:57          11507 docker-compose.yml
    -a---          2020/09/29    13:23           4690 init.ps1
    -a---          2020/09/29    12:44          66651 license.xml

    PS C:\projects\container\ltsc2019\sitecore-xp0> docker-compose up --detach
    Creating network "sitecore-xp0_default" with the default driver
    Pulling mssql (scr.sitecore.com/sxp/sitecore-xp0-mssql:10.0.0-ltsc2019)...
    10.0.0-ltsc2019: Pulling from sxp/sitecore-xp0-mssql
    4612f6d0b889: Already exists                                                                                            
    c3aff4450246: Pull complete                                                                                             
    f25a846c89c4: Pull complete                                                                                             
    a8175160a4e0: Pull complete                                                                                             
    3adb3523ea68: Pull complete                                                                                             
    d251d4ad07b2: Pull complete                                                                                             
    654c7fa7df7f: Pull complete                                                                                             
    b023f816c51e: Pull complete                                                                                             
    886b229f408e: Pull complete                                                                                             
    8185df2c7f9f: Pull complete                                                                                             
    42720c3faf2f: Pull complete                                                                                             
    4e20a857bb9c: Pull complete                                                                                             
    e49f1d84993a: Pull complete                                                                                             
    115a3a76ba55: Pull complete                                                                                             
    bfad2c0ba839: Pull complete                                                                                             
    Digest: sha256:849a1bf63d780307e460d4612e719fdf563a1ca3a14e57c676fcc31df25b7286
    Status: Downloaded newer image for scr.sitecore.com/sxp/sitecore-xp0-mssql:10.0.0-ltsc2019
    Pulling solr (scr.sitecore.com/sxp/sitecore-xp0-solr:10.0.0-ltsc2019)...
    10.0.0-ltsc2019: Pulling from sxp/sitecore-xp0-solr
    4612f6d0b889: Already exists                                                                                            
    c3aff4450246: Already exists                                                                                            
    036ef77a41df: Pull complete                                                                                             
    2d2bc021b8bc: Pull complete                                                                                             
    613818764b2c: Pull complete                                                                                             
    fb0c6cd70749: Pull complete                                                                                             
    6e0b10f4ff30: Pull complete                                                                                             
    47fb72851813: Pull complete                                                                                             
    bf0f7dd4b8ea: Pull complete                                                                                             
    73e7adaa7cbc: Pull complete                                                                                             
    db590c2afa39: Pull complete                                                                                             
    44fa4b680467: Pull complete                                                                                             
    c73555995572: Pull complete                                                                                             
    8909a83cf450: Pull complete                                                                                             
    a20aeb2af3bd: Pull complete                                                                                             
    3c3d01093816: Pull complete                                                                                             
    4fc2886ee582: Pull complete                                                                                             
    70347b9c3b60: Pull complete                                                                                             
    24de3d09a6a4: Pull complete                                                                                             
    071fbcae1fb9: Pull complete                                                                                             
    48be54735626: Pull complete                                                                                             
    Digest: sha256:52d9c54e01617b6c01c3a01dd16b0330c7148faa827d6c63e7fbb3407f9457f8
    Status: Downloaded newer image for scr.sitecore.com/sxp/sitecore-xp0-solr:10.0.0-ltsc2019
    Pulling id (scr.sitecore.com/sxp/sitecore-id:10.0.0-ltsc2019)...
    10.0.0-ltsc2019: Pulling from sxp/sitecore-id
    4612f6d0b889: Already exists                                                                                            
    c3aff4450246: Already exists                                                                                            
    5ed7d395f4c8: Pull complete                                                                                             
    95c8d26c53de: Pull complete                                                                                             
    4ffb72f38d5c: Pull complete                                                                                             
    2e26b932189f: Pull complete                                                                                             
    790583a0dfa6: Pull complete                                                                                             
    448d86a5eb7e: Pull complete                                                                                             
    cd48f3ddbc76: Pull complete                                                                                             
    2ca50424880f: Pull complete                                                                                             
    48c17923e002: Pull complete                                                                                             
    Digest: sha256:86d7f54f9e880bdc881aa8924b1249efef6b4fb436fbeab6371bb94fe44f3fd9
    Status: Downloaded newer image for scr.sitecore.com/sxp/sitecore-id:10.0.0-ltsc2019
    Pulling xconnect (scr.sitecore.com/sxp/sitecore-xp0-xconnect:10.0.0-ltsc2019)...
    10.0.0-ltsc2019: Pulling from sxp/sitecore-xp0-xconnect
    4612f6d0b889: Already exists                                                                                            
    c3aff4450246: Already exists                                                                                            
    4c646724ced3: Pull complete                                                                                             
    a015adbfa3ae: Pull complete                                                                                             
    2ce9c006723e: Pull complete                                                                                             
    ddc80c76fa1f: Pull complete                                                                                             
    2905264c6711: Pull complete                                                                                             
    117f087febe4: Pull complete                                                                                             
    dbeba73a7c0e: Pull complete                                                                                             
    fdef365f897e: Pull complete                                                                                             
    2535e77c62f3: Pull complete                                                                                             
    7824e01a413c: Pull complete                                                                                             
    bf566e7179dd: Pull complete                                                                                             
    1307c637cda7: Pull complete                                                                                             
    0647043bb157: Pull complete                                                                                             
    f0d1a8e33742: Pull complete                                                                                             
    83e23ebab808: Pull complete                                                                                             
    c694b1753132: Pull complete                                                                                             
    5742a8fdc92a: Pull complete                                                                                             
    0d6fe6b819ba: Pull complete                                                                                             
    57817727438e: Pull complete                                                                                             
    Digest: sha256:8cc836c3bc7fe563b5b3b33cdb9f8b5dc723b9aeb39f4c6e9016e90e24dfe8b2
    Status: Downloaded newer image for scr.sitecore.com/sxp/sitecore-xp0-xconnect:10.0.0-ltsc2019
    Pulling cm (scr.sitecore.com/sxp/sitecore-xp0-cm:10.0.0-ltsc2019)...
    10.0.0-ltsc2019: Pulling from sxp/sitecore-xp0-cm
    4612f6d0b889: Already exists                                                                                            
    c3aff4450246: Already exists                                                                                            
    4c646724ced3: Already exists                                                                                            
    a015adbfa3ae: Already exists                                                                                            
    2ce9c006723e: Already exists                                                                                            
    ddc80c76fa1f: Already exists                                                                                            
    2905264c6711: Already exists                                                                                            
    117f087febe4: Already exists                                                                                            
    dbeba73a7c0e: Already exists                                                                                            
    fdef365f897e: Already exists                                                                                            
    2535e77c62f3: Already exists                                                                                            
    7824e01a413c: Already exists                                                                                            
    c371566dbb08: Pull complete                                                                                             
    0fa991b4b94d: Pull complete                                                                                             
    92b4351e507c: Pull complete                                                                                             
    57e637ca808e: Pull complete                                                                                             
    673668d01687: Pull complete                                                                                             
    639159dbabc1: Pull complete                                                                                             
    371995e293ee: Pull complete                                                                                             
    72a2e294b6fe: Pull complete                                                                                             
    114703e4df9d: Pull complete                                                                                             
    9b1467a8cb90: Pull complete                                                                                             
    bcff52cd103c: Pull complete                                                                                             
    e3cfbf43db0e: Pull complete                                                                                             
    Digest: sha256:194bb5324497eadeadb24bf9fe72bc9ee0578cdd162199a86be4427f01e4edac
    Status: Downloaded newer image for scr.sitecore.com/sxp/sitecore-xp0-cm:10.0.0-ltsc2019
    Pulling traefik (traefik:v2.2.0-windowsservercore-1809)...
    v2.2.0-windowsservercore-1809: Pulling from library/traefik
    65014b3c3121: Pull complete                                                                                             
    eac6fba788c9: Pull complete                                                                                             
    edc29de22414: Pull complete                                                                                             
    4b6882ac7e42: Pull complete                                                                                             
    423691ba5ecc: Pull complete                                                                                             
    84a00a51e357: Pull complete                                                                                             
    e0d82edeef84: Pull complete                                                                                             
    Digest: sha256:5cd37215ff336d5088132aa1b7ab5181672cc9cfb98449c8939d9e76527d5b38
    Status: Downloaded newer image for traefik:v2.2.0-windowsservercore-1809
    Pulling xdbsearchworker (scr.sitecore.com/sxp/sitecore-xp0-xdbsearchworker:10.0.0-ltsc2019)...
    10.0.0-ltsc2019: Pulling from sxp/sitecore-xp0-xdbsearchworker
    4612f6d0b889: Already exists                                                                                            
    c3aff4450246: Already exists                                                                                            
    4c646724ced3: Already exists                                                                                            
    a015adbfa3ae: Already exists                                                                                            
    2ce9c006723e: Already exists                                                                                            
    ddc80c76fa1f: Already exists                                                                                            
    cd4e4ea07ed8: Pull complete                                                                                             
    710c0b9b64ec: Pull complete                                                                                             
    8edbeed8c3fc: Pull complete                                                                                             
    75d324fa03be: Pull complete                                                                                             
    0711c8e4ad0b: Pull complete                                                                                             
    dbab781c751b: Pull complete                                                                                             
    fc87e8c69355: Pull complete                                                                                             
    fe3dce4d03d0: Pull complete                                                                                             
    Digest: sha256:b0e6c2aeeeb843326da7a593a614bcfb9d600de965ed92efa0dd6792d6eb2100
    Status: Downloaded newer image for scr.sitecore.com/sxp/sitecore-xp0-xdbsearchworker:10.0.0-ltsc2019
    Pulling xdbautomationworker (scr.sitecore.com/sxp/sitecore-xp0-xdbautomationworker:10.0.0-ltsc2019)...
    10.0.0-ltsc2019: Pulling from sxp/sitecore-xp0-xdbautomationworker
    4612f6d0b889: Already exists                                                                                            
    c3aff4450246: Already exists                                                                                            
    4c646724ced3: Already exists                                                                                            
    a015adbfa3ae: Already exists                                                                                            
    2ce9c006723e: Already exists                                                                                            
    ddc80c76fa1f: Already exists                                                                                            
    7f40a0ec8982: Pull complete                                                                                             
    f6522ea410a2: Pull complete                                                                                             
    b6fb2bdb322b: Pull complete                                                                                             
    0423e8e80e8c: Pull complete                                                                                             
    bb06431258a8: Pull complete                                                                                             
    82cc4d81b243: Pull complete                                                                                             
    e37b2afaa4f3: Pull complete                                                                                             
    65ca38493dc8: Pull complete                                                                                             
    Digest: sha256:409de3e289bbfa76b79f151be23360067639f3808dc6cc373601b78816ebaeda
    Status: Downloaded newer image for scr.sitecore.com/sxp/sitecore-xp0-xdbautomationworker:10.0.0-ltsc2019
    Pulling cortexprocessingworker (scr.sitecore.com/sxp/sitecore-xp0-cortexprocessingworker:10.0.0-ltsc2019)...
    10.0.0-ltsc2019: Pulling from sxp/sitecore-xp0-cortexprocessingworker
    4612f6d0b889: Already exists                                                                                            
    c3aff4450246: Already exists                                                                                            
    4c646724ced3: Already exists                                                                                            
    a015adbfa3ae: Already exists                                                                                            
    2ce9c006723e: Already exists                                                                                            
    ddc80c76fa1f: Already exists                                                                                            
    7f40a0ec8982: Already exists                                                                                            
    f6522ea410a2: Already exists                                                                                            
    9fedb7832b20: Pull complete                                                                                             
    937fb10c5004: Pull complete                                                                                             
    8293a43afdbc: Pull complete                                                                                             
    749bec3c9138: Pull complete                                                                                             
    a03fdcb99582: Pull complete                                                                                             
    281a5d7ebc45: Pull complete                                                                                             
    Digest: sha256:fd7dd84363ecab6bd18f9acf760ded9fa13ab742400f7cf290795ae03776c41c
    Status: Downloaded newer image for scr.sitecore.com/sxp/sitecore-xp0-cortexprocessingworker:10.0.0-ltsc2019
    Creating sitecore-xp0_solr_1  ... done                                                                                  
    Creating sitecore-xp0_mssql_1 ... done                                                                                  
    Creating sitecore-xp0_id_1       ... done                                                                               
    Creating sitecore-xp0_xconnect_1 ... done                                                                               
    Creating sitecore-xp0_cm_1       ... done                                                                               
    Creating sitecore-xp0_cortexprocessingworker_1 ... done                                                                 
    Creating sitecore-xp0_xdbsearchworker_1        ... done                                                                 
    Creating sitecore-xp0_xdbautomationworker_1    ... done                                                                 
    Creating sitecore-xp0_traefik_1                ... done                                                                 
    PS C:\projects\container\ltsc2019\sitecore-xp0>  

PowerShell で実行しているイメージは以下のような形です。

.. image:: images/container04.png
   :align: center
   :width: 400px
   :alt: docker-compose

done が表示された後、Docker のツールに含まれるダッシュボードを開くと、コンテナが稼働していることがわかります。

.. image:: images/container05.png
   :align: center
   :width: 400px
   :alt: docker dashboard   

.env ファイルで定義していたドメイン https://xp0cm.localhost/ にアクセスをします。以下のようにサンプルのサイトが起動しています。

.. image:: images/container06.png
   :align: center
   :width: 400px
   :alt: Sitecore の Welcome ページ   

既に init.ps1 にて定義した管理者のパスワードを利用してログインをします。

.. image:: images/container07.png
   :align: center
   :width: 400px
   :alt: Sitecore の管理画面   

無事、Container で Sitecore 10.0 を起動することができました。

*************
参考動画
*************

.. raw:: html

    <iframe width="560" height="315" src="https://www.youtube.com/embed/todOvW4FX1Y" frameborder="0" allowfullscreen></iframe>

