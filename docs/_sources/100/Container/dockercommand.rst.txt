######################
Docker コマンド一覧
######################

ここではよく利用する Docker のコマンド一覧を紹介しています。

*****************************
イメージ
*****************************

イメージの確認

.. code-block:: powershell

    docker images

イメージの削除

.. code-block:: powershell

    docker rmi [イメージID]

*****************************
コンテナの確認
*****************************

動作しているコンテナの確認

.. code-block:: powershell

    docker ps

停止しているコンテナの確認

.. code-block:: powershell

    docker ps -a

コンテナの削除

.. code-block:: powershell

    docker rm [コンテナID]

