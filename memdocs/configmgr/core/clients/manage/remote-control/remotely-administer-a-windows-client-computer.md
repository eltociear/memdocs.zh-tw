---
title: 遠端管理 Windows 電腦
titleSuffix: Configuration Manager
description: 使用 Configuration Manager 管理遠端的 Windows 用戶端電腦。
ms.date: 11/02/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 3c9648c4-645e-4e47-ae10-2da817b8c83b
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 801654b95470889d0b661315d40d3e00efa8e542
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81696406"
---
# <a name="how-to-remotely-administer-a-windows-client-computer-by-using-configuration-manager"></a>如何使用 Configuration Manager 從遠端管理 Windows 用戶端電腦

適用於：  Configuration Manager (最新分支) Configuration Manager 允許您使用 **Configuration Manager 遠端控制**連線到用戶端電腦。 開始使用遠端控制之前，請務必先檢閱下列文章中的資訊：  

-   [遠端控制的先決條件](prerequisites-for-remote-control.md)  

-   [設定遠端控制](configuring-remote-control.md)  

以下是啟動遠端控制檢視器的三種方式：  

-   在 Configuration Manager 主控台中。  

-   在 Windows 命令提示字元中。  

-   從執行 Configuration Manager 主控台 (位於 **Microsoft System Center** 程式群組) 之電腦的 Windows [開始]  功能表。  

## <a name="to-remotely-administer-a-client-computer-from-the-configuration-manager-console"></a>在 Configuration Manager 主控台從遠端管理用戶端電腦  

1.  在 Configuration Manager 主控台中，選擇 [資產與合規性]   > [裝置]  或 [裝置集合]  。  

3.  選取要遠端管理的電腦，然後在 [首頁]  索引標籤的 [裝置]  群組中，選擇 [開始]   > [遠端控制]  。  

    > [!IMPORTANT]  
    >  如果用戶端設定 [提示使用者提供遠端控制權限]  設為 [True]  ，在遠端電腦使用者對遠端控制提示表示同意前，不會啟動連線。 如需詳細資訊，請參閱[設定遠端控制](configuring-remote-control.md)。  

4.  [Configuration Manager 遠端控制]  視窗開啟後，您就可以從遠端管理用戶端電腦。 請使用下列選項設定連線。  

    > [!NOTE]  
    >  如果連線的電腦有多個監視器，遠端控制視窗會顯示所有監視器的畫面。  

    -   **File**
        - **連線** - 連線到另一部電腦。 使用遠端控制工作階段時無法使用此選項。  
        -   **中斷連線** - 中斷作用中的遠端控制工作階段連線，但不關閉 [Configuration Manager 遠端控制]  視窗。  
        - **結束** - 中斷作用中的遠端控制工作階段連線，並關閉 [Configuration Manager 遠端控制]  視窗。  

        > [!NOTE]  
        >  當您中斷遠端控制工作階段的連線時，會刪除您檢視電腦上的 Windows 剪貼簿內容。


    - **檢視**
      - **色彩深度** - 選擇每像素 16 位元或 32 位元。
      -  **全螢幕** - 最大化 [Configuration Manager 遠端控制]  視窗。 若要結束全螢幕模式，請按 Ctrl+Alt+Break。  
      - **為低頻寬連線最佳化** - 如果連線頻寬較低，請選擇此選項。
      - **顯示：**
        - **所有畫面** - 在 Configuration Manager 1902 中新增。 如果連線的電腦有多個監視器，遠端控制視窗會顯示所有監視器的畫面。 **所有畫面**是 1902 之前具有多個螢幕之電腦的唯一檢視。
        -  **第一個畫面** - 在 Configuration Manager 1902 中新增。 「第一個畫面」  位於頂端最左邊，如 Windows 顯示設定所示。 您無法選取特定的畫面。 當您切換檢視器的設定時，請重新連線遠端工作階段。 檢視器會儲存您的喜好設定以供未來的連線使用。
        -  **縮放至適當比例** - 將遠端電腦的顯示畫面縮放至適合 [Configuration Manager 遠端控制]  視窗的大小。
        - **狀態列** - 切換顯示 [Configuration Manager 遠端控制]  視窗的狀態列。  

       > [!NOTE]  
       >  檢視器會儲存您的喜好設定以供未來的連線使用。

    -   **動作**
        - **傳送 Ctrl+Alt+Del 按鍵** - 將 Ctrl+Alt+Del 按鍵組合傳送到遠端電腦。 
        - **啟用剪貼簿共用** - 讓您在遠端電腦上複製及貼上項目。 如果變更這個值，您必須重新啟動遠端控制工作階段，變更才會生效。   
          - 如果不想在 Configuration Manager 主控台中啟用剪貼簿共用，請在執行主控台的電腦上，將登錄機碼 **HKEY_CURRENT_USER\Software\Microsoft\ConfigMgr10\Remote Control\Clipboard Sharing** 的值設定為 **0**。
        - **啟用鍵盤轉譯** - 將執行主控台之電腦的鍵盤配置轉譯為連線裝置的配置。
        - **鎖定遠端鍵盤和滑鼠** - 鎖定遠端鍵盤與滑鼠，以防止使用者操作遠端電腦。  

    -   **說明**
        - **關於遠端控制** - 顯示檢視器的目前版本。  

5.  當遠端電腦上的使用者按一下 Configuration Manager **遠端控制**圖示時，即可檢視遠端控制工作階段的詳細資訊。 該圖示位於 Windows 通知區域，或遠端控制工作階段列上。  

## <a name="to-start-the-remote-control-viewer-from-the-windows-command-line"></a>從 Windows 命令列啟動遠端控制檢視器  

-   在 Windows 命令提示字元中，鍵入 _<Configuration Manager 安裝資料夾\>_ **\AdminConsole\Bin\i386\CmRcViewer.exe**  

CmRcViewer.exe 支援下列命令列選項：  

- *位址* - 指定 NetBIOS 名稱、完整的網域名稱 (FQDN) 或您想要連線的用戶端電腦 IP 位址。
- *站台伺服器名稱* - 指定要傳送遠端控制工作階段狀態相關訊息的目標 Configuration Manager 站台伺服器名稱。
- **/?** - 顯示遠端控制檢視器的命令列選項。  
     
**範例：CmRcViewer.exe** <位址\>  <\\\站台伺服器名稱>  

> [!NOTE]  
> 支援 Configuration Manager 主控台的所有作業系統上都支援遠端控制檢視器。 如需詳細資訊，請參閱 [Configuration Manager 主控台的支援設定](../../../plan-design/configs/supported-operating-systems-consoles.md)以及[遠端控制的必要條件](prerequisites-for-remote-control.md)。

## <a name="next-steps"></a>後續步驟

[稽核遠端控制使用情況](audit-remote-control-usage.md)
