* ### [Re-Install Windows Photo Viewer From Powershell](http://www.winhelponline.com/blog/reinstall-photos-app-windows-10/)
```sh
Get-AppxPackage -allusers Microsoft.Windows.Photos | Foreach {Add-AppxPackage -DisableDevelopmentMode -Register "$($_.InstallLocation)\AppXManifest.xml"}
Get-AppxPackage Microsoft.Windows.Photos -allusers | select PackageFullName
Add-AppxPackage -register "C:\Program Files\WindowsApps\Microsoft.Windows.Photos_2018.18011.13110.0_x64__8wekyb3d8bbwe\AppxManifest.xml" -DisableDevelopmentMode
```
