# パスワードのリセット

Sitecore のインストール後に、Admin のパスワードを一度リセットしたい場合は、Sitecore の Core データベースを開いて、以下の SQL を実行することで、パスワードを b に変更することができます。

```SQL
UPDATE dbo.aspnet_Membership 
SET [Password]='qOvF8m8F2IcWMvfOBjJYHmfLABc=', [PasswordSalt]='OM5gu45RQuJ76itRvkSPFw==', 
[IsApproved] = '1', [IsLockedOut] = '0'
WHERE UserId IN (SELECT UserId FROM dbo.aspnet_Users WHERE UserName = 'sitecore\Admin') 
```

## 参考サイト
* [Sitecore Blog : Reset the admin passord ](http://sitecoreblog.blogspot.com/2012/05/reset-admin-passord.html)

---
[戻る](../)