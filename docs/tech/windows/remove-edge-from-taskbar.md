---
title: Remove Edge From the Taskbar
---

![](/assets/images/ms-edge-ban.png)

If Microsoft Edge is automaticlly pinned to the taskbar after rebooting the PC, even after removing it, try these steps.

## Disable startup

1. Open Task Manager by right clicking on the start menu icon in the taskbar or by using the key combination ++ctrl+shift+esc++.
2. Open the **Startup** tab.
3. Right click on **Microsoft Edge** and select **Deactivate**.

Reboot your PC.

## Edit Layout Modification

1. Open the file: 

    ```
    %userprofile%\AppData\Local\Microsoft\Windows\Shell\LayoutModification.xml`.
    ```

1. Search for the follong line of code:

    ```xml
    <taskbar:UWA AppUserModelID="Microsoft.MicrosoftEdge_8wekyb3d8bbwe!MicrosoftEdge" />
    ```

1. Save and close the file.

Reboot your PC.