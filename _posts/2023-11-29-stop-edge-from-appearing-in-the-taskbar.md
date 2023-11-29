---
title: Stop Edge from appearing in the taskbar
categories: [PC,Windows 10]
tags: [pc,windows,taskbar]
pin: false
img_path: /assets/img/
image:
    path: ms-edge-ban.png
---

If Microsoft Edge is automaticlly pinned to the taskbar after rebooting the PC, even after removing it, try these steps.

## Disable startup in Task Manager

1. Open Task Manager by right clicking on the start menu icon in the taskbar or by using the key combination `ctrl` + `shift` + `esc`.
2. Open the Startup tab.
3. Right click on Microsoft Edge and select Deactivate.

Reboot your PC.

## Edit the LayoutModification file

1. Open this file: `%userprofile%\AppData\Local\Microsoft\Windows\Shell\LayoutModification.xml`.
2. Search for the follong line of code:
    ```xml
    <taskbar:UWA AppUserModelID="Microsoft.MicrosoftEdge_8wekyb3d8bbwe!MicrosoftEdge" />
    ```
3. Save and close the file.

Reboot your PC.