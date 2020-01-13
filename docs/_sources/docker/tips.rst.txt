################
Docker Tips
################


********************
ネットワークの変更
********************

仮想マシンで Docker を利用している場合、再起動するなどで network の再設定が必要となる場合があります。この場合、以下のコマンドでネットワークの再設定をしてください。

.. code-block:: 

    docker network connect <network name> <container name>

93x_default のネットワークに 93x_sql_1 のコンテナを接続する場合は、以下のコマンドを実行します。

.. code-block:: 

    docker network connect 93x_default 93x_sql_1
