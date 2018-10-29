# 1liner
One liners that i have found on useful


### Geting WiFi Credentials Saved in the System - Powershell
>>>
```
(netsh wlan show profiles) | Select-String '\:(.+)$' | %{$name=$_.Matches.Groups[1].Value.Trim(); $_} | %{(netsh wlan show profile name=$name key=clear)}  | Select-String 'Key Content\W+\:(.+)$' | %{$pass=$_.Matches.Groups[1].Value.Trim(); $_} | %{[PSCustomObject]@{ PROFILE_NAME=$name;PASSWORD=$pass }}
```



### To Read Emails From Outlook - Powershell
>>>
```
Add-type -assembly "Microsoft.Office.Interop.Outlook" | out-null; $olFolders = "Microsoft.Office.Interop.Outlook.olDefaultFolders" -as [type]; $outlook = new-object -comobject outlook.application; $namespace = $outlook.GetNameSpace("MAPI"); $folder = $namespace.getDefaultFolder($olFolders::olFolderInBox); $folder.items | Select-Object -Property Subject, ReceivedTime, SenderName, Body 

```
