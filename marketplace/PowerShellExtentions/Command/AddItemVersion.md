# 新しいバージョンの追加

アイテムの新しいバージョンをコマンドで作成することができます。
例えば、英語のコンテンツを元にポルトガル語、英語（米国）の新しいバージョンを作成しつつ、Title フィールドに関してはスキップする、という記載をする場合は以下のような記載となります。

```PowerShell
Add-ItemVersion -Path "master:\content\home" -Language "en" -TargetLanguage "pl-pl", "en-us" -IfExist Skip -IgnoredFields "Title"
```
上記のコマンドを実行すると、`master:\content\home` にポルトガル語と英語（米国）が追加されるのがわかります。

また、アイテムのバージョンを追加していく内容は以下のように実行することができます。

```PowerShell
Add-ItemVersion -Path "master:\content\home" -Language ja-JP -IfExist Append
```

## 参考ページ
* [New-ItemVesion](https://doc.sitecorepowershell.com/appendix/common/add-itemversion)

---
[目次に戻る](../)