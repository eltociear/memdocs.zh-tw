---
title: 針對套件轉換管理員進行疑難排解
titleSuffix: Configuration Manager
description: 了解如何在 Configuration Manager 中使用套件轉換管理員來進行問題的疑難排解。
ms.date: 08/24/2018
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: cb616925-bb94-4b7c-a867-b3d95aef4d5e
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 05110714d3aa8ca48ff9384f0116338b0092fde1
ms.sourcegitcommit: a77ba49424803fddcaf23326f1befbc004e48ac9
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/27/2020
ms.locfileid: "83877630"
---
# <a name="troubleshoot-package-conversion-manager"></a>針對套件轉換管理員進行疑難排解

適用於：Configuration Manager (最新分支)

<!--1357861-->

使用套件轉換管理員時，請利用本文的資訊來協助您進行問題的疑難排解。



## <a name="sms-provider"></a>SMS 提供者

套件轉換管理員會使用 SMS 提供者。 如需詳細資訊，請參閱[規劃 SMS 提供者](../../core/plan-design/hierarchy/plan-for-the-sms-provider.md)。

如果 SMS 提供者無法正常運作，包含套件轉換管理員的 Configuration Manager 主控台就無法運作。



## <a name="package-readiness"></a>套件整備

將套件轉換為應用程式之前，先使用套件轉換管理員的**分析**功能來分析套件。 分析之後，在 Configuration Manager 主控台的 [套件] 節點中，新增**整備**欄。 套件清單會顯示已分析套件的下列其中一個整備狀態：

- **自動**：套件可以使用 [轉換] 功能直接進行轉換。      

  > [!NOTE]  
  > 自動轉換不會將 WQL 查詢轉換為應用程式需求。 使用**修正並轉換**程序來轉換這些查詢。  

- **手動**：套件需要一些新增或變更，才能使用 [修正並轉換] 功能進行轉換。  

- **不適用**：套件不適合進行轉換。 請更正封裝的任何問題，或繼續部署成封裝。  

- **錯誤**：套件包含錯誤。 先手動更正這些錯誤，然後您才能分析並轉換它。  

Configuration Manager 主控台中 [套件] 節點的詳細資料窗格會顯示任何整備問題。 選取套件，然後在詳細資料窗格中選取 [摘要]  索引標籤。



## <a name="log-files"></a>記錄檔

### <a name="enable-logging"></a>啟用記錄

當您針對套件轉換管理員啟用記錄時，它會記錄它的所有動作、例外狀況和錯誤。

若要在 Configuration Manager 中啟用此元件的記錄，請修改 **Microsoft.ConfigurationManagement.exe.Config**。根據預設，此設定檔位於下列路徑：  
`C:\Program Files (x86)\Microsoft Endpoint Manager\AdminConsole\bin\Microsoft.ConfigurationManagement.exe.config`  

> [!IMPORTANT]
> 從 1910 版開始，此路徑已變更為使用 `Microsoft Endpoint Manager` 資料夾。 請確定您不會使用可能存在於另一個資料夾中的較舊版本檔案。

在最後一個 **sources** 元素之後的 **system.diagnostics** 元素中，插入下列 **switches** 和 **trace** XML 元素：

``` XML
</sources>

    <switches>
      <add name="PcmLogging" value="3"/>
    </switches>
    <trace autoflush="true" indentsize="4">
      <listeners>
        <add name="PcmTraceListener" type="Microsoft.ConfigurationManagement.UserCentric.Logging.RolloverLogTraceListener, Microsoft.ConfigurationManagement.UserCentric.Logging" initializeData="%UserProfile%\AppData\Local\Temp\PcmTrace.log"/>
      </listeners>
    </trace>

</system.diagnostics>
```

這個範例會使用 **PCMTrace.log** 檔案。 這個記錄位於執行 Configuration Manager 主控台的電腦上的下列路徑中：  
`%UserProfile%\AppData\Local\Temp`

若要設定詳細資料的層級，請變更 **PcmLogging** 追蹤參數設定。 將此值設定為四種詳細資料層級，從最不詳細 (`1`) 到最詳細 (`4`)。


### <a name="smsprovlog"></a>SMSProv.log

在某些情況下，對套件轉換程序進行疑難排解的相關資訊位於 **SMSProv.log** 檔案中。 這個檔案會擷取來自 Configuration Manager SMS 提供者的資訊。

根據預設，此記錄檔位於 Configuration Manager 站台伺服器上的下列路徑中：  
`C:\Program Files\Microsoft Configuration Manager\Logs`

如果您看到下列其中一個錯誤訊息，則 **SMSProv.log** 檔案可能包含相關的疑難排解資訊：

- `The SMS Provider reported an error`

- `Generic Failure`

這些錯誤訊息通常表示站台伺服器上發生錯誤，但不會將錯誤資訊傳送至 Configuration Manager 主控台。

如需詳細資訊，請參閱[套件轉換管理員錯誤訊息的技術參考](error-messages.md)。



## <a name="changing-package-attributes-after-analysis"></a>分析後變更封裝屬性

當您分析套件且其整備狀態為**自動**或**手動**之後，如果您變更了任何相關屬性，則轉換程序可能會失敗。

例如，您分析套件且其整備狀態為**自動**。 然後您將另一個程式新增至套件。 套件轉換可能會失敗。

如果您需要在分析之後對套件進行變更，請在轉換之前重新執行分析。 



## <a name="see-also"></a>請參閱

[套件轉換管理員錯誤訊息的技術參考](error-messages.md)
