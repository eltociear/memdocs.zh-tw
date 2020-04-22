---
title: 設定遠端控制
titleSuffix: Configuration Manager
description: 在 Configuration Manager 中設定遠端控制。
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 45affc27-aa11-4249-9493-082ac23a3a3d
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 1362f44c510fd34aebc6af77efc63e881c27688c
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81696466"
---
# <a name="configuring-remote-control-in-configuration-manager"></a>在 Configuration Manager 中設定遠端控制

適用於：  Configuration Manager (最新分支)

 這個程序會說明設定遠端控制的預設用戶端設定。 這些設定會套用至階層中的所有電腦。 如果您只想讓某些電腦套用這些設定，請將自訂裝置用戶端設定指派給包含那些電腦的集合。 如需詳細資訊，請參閱[如何設定用戶端設定](../../../../core/clients/deploy/configure-client-settings.md)。 

若要使用遠端協助或遠端桌面，它必須安裝及設定在執行 Configuration Manager 主控台的電腦上。 如需如何安裝及設定遠端協助或遠端桌面的詳細資訊，請參閱 Windows 文件。  

#### <a name="to-enable-remote-control-and-configure-client-settings"></a>啟用遠端控制及設定用戶端設定  

1. 在 Configuration Manager 主控台中，選擇 [系統管理]   > [用戶端設定]   > [預設用戶端設定]  。  

2. 在 [首頁]  索引標籤的 [內容]  群組中，選擇 [內容]  。  

3. 在 [預設]  對話方塊中，選擇 [遠端工具]  。  

4. 設定遠端控制、遠端協助和遠端桌面用戶端設定。 如需您可設定的遠端工具用戶端設定清單，請參閱[遠端工具](../../../../core/clients/deploy/about-client-settings.md#remote-tools)。  

   在 [電腦代理程式]  用戶端設定中設定 [顯示於軟體中心的組織名稱]  的值，就可以變更出現在 [ConfigMgr 遠端控制]  對話方塊中的公司名稱。  

   用戶端電腦會在下一次下載用戶端原則時，使用這些設定進行設定。 若要起始單一用戶端的原則擷取，請參閱[如何管理用戶端](../../../../core/clients/manage/manage-clients.md)。  

#### <a name="enable-keyboard-translation"></a>啟用鍵盤轉譯

根據預設，Configuration Manager 會將按鍵位置從檢視者的位置傳輸到共用者的位置。 如果檢視者和共用者的鍵盤設定不同，這可能會發生問題。 例如，具有英文鍵盤的檢視者會輸入"A"，但共用者的法文鍵盤會提供 "Q"。 您現在有選項可以設定遠端控制，讓字元本身從檢視者的鍵盤傳輸到共用者，以確保檢視者預期輸入的內容會抵達共用者端。

若要開啟鍵盤轉譯，請在 [Configuration Manager 遠端控制]  中，選擇 [動作]  ，然後選擇 [啟用鍵盤轉譯]  以傳輸按鍵位置。

> [!NOTE]
>
> ~!#@$% 等特殊按鍵不會正確轉譯。


## <a name="keyboard-shortcuts-for-the-remote-control-viewer"></a>遠端控制檢視器的鍵盤快速鍵

|鍵盤快速鍵|說明|  
|-----------------------|-----------------|  
|Alt+Page Up|從左到右切換各執行中程式。|  
|Alt+Page Down|從右到左切換各執行中程式。|  
|Alt+Insert|依執行中程式的開啟順序，來循環使用執行中程式。|  
|Alt+Home|顯示 [開始]  功能表。|  
|Ctrl+Alt+End|顯示 [Windows 安全性] 對話方塊 (Ctrl+Alt+Del)。|  
|Alt+Delete|顯示 Windows 功能表。|  
|Ctrl+Alt+減號 (位於數字鍵台)|將本機電腦的使用中視窗複製至遠端電腦剪貼簿。|  
|Ctrl+Alt+加號 (位於數字鍵台)|將整個本機電腦的視窗區域複製至遠端電腦剪貼簿。|  
