##########################
コンテンツのインポート
##########################

CSV ファイルで定義されたデータに関して、コマンドを利用してインポートを実行します。

.. code-block:: 

  $importData = Import-CSV "C:\Temp\test.csv"
  foreach ( $row in $importData ) {
      $item = Get-Item -Path master:$($row.ItemPath) -ErrorAction SilentlyContinue
      
      if ($item) {
          $item.Editing.BeginEdit()
          $item["Title"] = $row.Title
          $item["Text"] = $row.Text
          $item.Editing.EndEdit() | Out-Null
      }
      else {        
          Write-Host "Couldn't find: $($row.ItemPath)"
      }
  }

すでにエクスポートしたデータをオフラインで変更、それをインポートを実行しています。アイテムがない場合は、アイテムがないというメッセージを出しています。これを応用して、アイテムがない場合は作成をするようにします。

.. code-block:: 

  $importData = Import-CSV "C:\Temp\test.csv"
  foreach ( $row in $importData ) {
      $item = Get-Item -Path master:$($row.ItemPath) -ErrorAction SilentlyContinue
    
      if ($item) {
          $item.Editing.BeginEdit()
          $item["Title"] = $row.Title
          $item["Text"] = $row.Text
          $item.Editing.EndEdit() | Out-Null
      }
      else {
          $newItem = New-Item -Path $row.ItemPath -Name $row.Name -ItemType "Sample/Sample Item"
          $newItem.Editing.BeginEdit()
          $newItem["Title"] = $row.Title
          $newItem["Text"] = $row.Text
          $newItem.Editing.EndEdit() | Out-Null
        
          Write-Host "Create new Item: $($row.ItemPath)"
      }
  }


*********************************
PowerShell コンテンツのインポート
*********************************

.. raw:: html

    <iframe width="560" height="315" src="https://www.youtube.com/embed/np8I8UBR8CY" frameborder="0" allowfullscreen></iframe>


**********
参考記事
**********
* `Working with items <https://doc.sitecorepowershell.com/working-with-items>`_
* `Using Sitecore Powershell Extensions to import CSV data <https://www.kasaku.co.uk/2016/04/10/importing-csv-data-in-sitecore/>`_
