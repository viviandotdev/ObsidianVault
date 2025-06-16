---
created: 2023-09-02 15:40
modified: 2025-06-14T19:07:59-04:00
alias: 
---
up::  [[My Tools]]
tags:: 
related: 

## Windows

[The 10 Best Windows Productivity Apps in 2022 - YouTube](https://www.youtube.com/watch?v=BQKfAxFgi-E)

### Windows Apps
1. Notion
2. Microsoft Edge
3. Flow Launcher
4. Espanso
5. WinGet
	_WinGet_ is the _Windows_ Package Manager.
	[App Installer - Microsoft Store Apps](https://apps.microsoft.com/store/detail/app-installer/9NBLGGH4NNS1?hl=en-us&gl=us)
6. Everything
	Search for everything
7. [PowerToys](https://github.com/microsoft/PowerToys/releases/)

### Drivers
1. [Precision Touchpad Driver Implementation for Apple MacBook / Magic Trackpad](https://github.com/imbushuo/mac-precision-touchpad)


[[Windows]]


- [ ] documemt your steps
- [ ] insatll windows,
    
- [ ] run the debloat script to remove all the apps
    
    - [x] [https://github.com/Raphire/Win11Debloat](https://github.com/Raphire/Win11Debloat)
    
    ```jsx
    & ([scriptblock]::Create((irm "<https://raw.githubusercontent.com/Raphire/Win11Debloat/master/Get.ps1>"))) -RunDefaults -Silent -RemoveApps -RemoveCommApps -RemoveW11Outlook -RemoveDevApps -RemoveGamingApps -DisableDVR -ClearStart -ClearStartAllUsers -DisableTelemetry -DisableBing -DisableSuggestions -DisableLockscreenTips -RevertContextMenu -ShowHiddenFolders -ShowKnownFileExt -HideDupliDrive -TaskbarAlignLeft -HideSearchTb -ShowSearchIconTb -ShowSearchLabelTb -ShowSearchBoxTb -HideTaskview -HideChat -DisableWidgets -DisableCopilot -DisableRecall -HideGallery
    ```
    
    - [ ] [https://github.com/LeDragoX/Win-Debloat-Tools](https://github.com/LeDragoX/Win-Debloat-Tools)
- [x] run the sysconfig them to turn off all the processes
    
    [https://www.youtube.com/watch?v=Vhc6J5eK6mc](https://www.youtube.com/watch?v=Vhc6J5eK6mc)
    
- [ ] the fix for windows it error
    
- [ ] run the scipt to remove windows defender
    
    - [ ] [https://github.com/ionuttbara/windows-defender-remover](https://github.com/ionuttbara/windows-defender-remover)
- [x] run the chrititus script to install aapps and tweaks
    
    - [x] [https://github.com/ChrisTitusTech/winutil](https://github.com/ChrisTitusTech/winutil)

[https://www.youtube.com/watch?v=iBiNfa32AnE](https://www.youtube.com/watch?v=iBiNfa32AnE)

- [ ] use auto hotkeys to map alt q for ctrl to quit the openede app

