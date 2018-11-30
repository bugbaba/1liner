# 1liner
One liners that i have used myself and found useful


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

### To Get The Windows Defender excluded folders 
>>>
```
reg query "HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Defender\Exclusions\Paths"
```

### To get the certificates installed that are not in Microsoft Certificate Trust List - [SysInternals](https://docs.microsoft.com/en-us/sysinternals/downloads/sigcheck)
>>>
```
sigcheck.exe -tuv 
```

### Deleting event logs - priviledged access
`Note: This generated an event log of itself`
>>>
```
wevtutil cl system
wevtutil cl application
wevtutil cl security

```
