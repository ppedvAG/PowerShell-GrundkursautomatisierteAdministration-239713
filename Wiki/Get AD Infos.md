```powershell
Get-ADUser -Filter * -Properties Department,LastLogon,LastLogonTimestamp | `
Where-Object -FilterScript {[DateTime]::FromFileTime($PSItem.LastLogon) -lt (Get-Date).AddDays(-90)} | `
Format-Table -Property Givenname,Surname,name,@{name="LastLogon";expression={[DateTime]::FromFileTime($PSItem.LastLogon)}}
```

Diese Abfrage zeigt einem alle User die sich schon länger als 90 Tage nicht mehr angemeldet haben.