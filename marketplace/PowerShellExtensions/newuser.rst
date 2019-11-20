####################
新しいユーザーの作成
####################

スクリプトで新しいユーザーを追加することができます。

例えば、saitokoa というユーザーを作成する場合、以下のコマンドで作成できます。

.. code-block:: PowerShell

  New-User -Identity saitokoa

この場合、パスワードはまだ設定されていないためユーザーのアカウントが有効になっていません。アカウントを有効にする場合は、パスワードと一緒に設定をすることでログインが可能なアカウントの設定ができます。

.. code-block:: PowerShell

  New-User -Identity saitokoa -Enabled -Password b -Email saitokoa@sitecore.demo -FullName "Saito Koa"


****************************
PowerShell New-User
****************************

.. raw:: html

    <iframe width="560" height="315" src="https://www.youtube.com/embed/DAIjqXBMHU4" frameborder="0" allowfullscreen></iframe>


**************
参考ページ
**************

* `New-User <https://doc.sitecorepowershell.com/appendix/security/new-user>`_

