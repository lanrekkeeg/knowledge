
# Windows

## Activate SMB1 in Windows 10

Open a PowerShell with administrator rights:

```
Enable-WindowsOptionalFeature -Online -FeatureName smb1protocol
```
