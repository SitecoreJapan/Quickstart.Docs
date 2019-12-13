##########################
新しいバージョンの追加
##########################


アイテムの新しいバージョンをコマンドで作成することができます。
例えば、英語のコンテンツを元にポルトガル語、英語（米国）の新しいバージョンを作成しつつ、Title フィールドに関してはスキップする、という記載をする場合は以下のような記載となります。

.. code-block:: powershell

  Add-ItemVersion -Path "master:\content\home" -Language "en" -TargetLanguage "pl-pl", "en-us" -IfExist Skip -IgnoredFields "Title"

上記のコマンドを実行すると、`master:\content\home` にポルトガル語と英語（米国）が追加されるのがわかります。

また、アイテムのバージョンを追加していく内容は以下のように実行することができます。

.. code-block:: powershell

  Add-ItemVersion -Path "master:\content\home" -Language ja-JP -IfExist Append


***************************
PowerShell Add-NewVersion
***************************

.. raw:: html

    <iframe width="560" height="315" src="https://www.youtube.com/embed/iifqa1X-nHw" frameborder="0" allowfullscreen></iframe>

************
参考ページ
************
* `New-ItemVesion <https://doc.sitecorepowershell.com/appendix/common/add-itemversion>`_
