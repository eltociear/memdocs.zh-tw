---
title: 防毒軟體的排除項目
titleSuffix: Configuration Manager
description: 了解針對可能的問題進行疑難排解時，所使用的建議防毒軟體排除項目。
ms.date: 10/31/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: deb470e3-6f6b-4ccf-b3d8-1598d79d3490
author: mestew
ms.author: mstewart
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: f3f38de1d7440ffd0293bde359deeb6be3bbeffb
ms.sourcegitcommit: 214fb11771b61008271c6f21e17ef4d45353788f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/07/2020
ms.locfileid: "82906197"
---
# <a name="recommended-antivirus-exclusions-for-configuration-manager"></a>Configuration Manager 的建議防毒軟體排除項目

適用於：  Configuration Manager (最新分支)

此文章包含的建議可協助系統管理員判斷執行支援之 Configuration Manager 站台伺服器、站台系統與用戶端 (當搭配防毒軟體使用時) 版本的電腦上可能不穩定的原因。

> [!IMPORTANT]
>
> - 我們建議您暫時套用這些程序來評估系統。 如果您的系統效能或穩定性已藉由此文章中的建議來改善，請連絡您的防毒軟體廠商，以取得相關指示或更新版本的防毒軟體。
> - 此文章包含的資訊說明如何協助降低安全性設定，或如何暫時關閉電腦上的安全性功能。 您可以進行這些變更，以了解特定問題的本質。 在進行這些變更之前，建議您先評估在特定環境中實作此因應措施的相關風險。

## <a name="possible-symptoms"></a>可能徵兆 

防毒軟體即時保護可能會在 Configuration Manager 站台伺服器、站台系統與用戶端上造成許多問題。

以下是可能徵兆的非完整清單：

- 未安裝遠端站台系統元件。 SiteComp.log、Distmgr.log、hman.log 或其他 Configuration Manager 記錄檔可能包含錯誤 80070005 之類的錯誤。
- 無法使用用戶端推送來安裝 Configuration Manager 用戶端
- 用戶端清查資訊不正確、遺失或過期。
- 待處理項目 (backlog) 發生在 *Install_Directory*\Program Files\Microsoft Configuration Manager\Inboxes 資料夾中。
- 軟體中心未由用戶端系統上已部署的軟體填入，或未啟動。 此外，CCMRepair.log 檔案可能包含如下列範例所示的錯誤：

  > 資料庫驗證失敗，結果如下：0x80004005 但 DB:C:\Windows\CCM\filename.sdf 可以開啟，正在跳過 DB 修復。

- 無法安裝部署至用戶端的軟體。
- 軟體部署的合規性資料不正確。

## <a name="exclusions"></a>排除

為避免此類問題，建議您新增下列即時保護排除項目：

### <a name="default-installation-folders"></a>預設安裝資料夾

|  |  |
| - | - |
|*ConfigMgr 安裝資料夾*  |  %ProgramFiles%\Microsoft Configuration Manager  |  
|*MP 安裝資料夾*  |%ProgramFiles%\SMS_CCM  |  
|*用戶端安裝資料夾*  |%Windir%\CCM  |  

### <a name="folder-exclusions-for-site-servers"></a>站台伺服器的資料夾排除項目

- *ConfigMgr 安裝資料夾*\Inboxes
- *ConfigMgr 安裝資料夾*\Logs
- *ConfigMgr 安裝資料夾*\EasySetupPayload

### <a name="folder-exclusions-for-site-systems"></a>站台系統的資料夾排除項目

- 管理點
  - *MP 安裝資料夾*\ServiceData
  - 下列任一項目：
    - *ConfigMgr 安裝資料夾*\MP\OUTBOXES
    - *安裝磁碟機*\SMS\MP\OUTBOXES
- 發佈點
  - *用戶端安裝資料夾*\ServiceData
  - *ContentLib_Drive*\SMS_DP$
  - *ContentLib_Drive*\SMSPKG*Drive_Letter*$
  - *ContentLib_Drive*\SMSPKG
  - *ContentLib_Drive*\SMSPKGSIG
  - *ContentLib_Drive*\SMSSIG$
- 站台資料庫伺服器
  - [如何選擇防毒軟體以在執行 SQL Server 的電腦上執行](https://support.microsoft.com/en-us/help/309422) \(機器翻譯\)

### <a name="folder-exclusions-for-clients"></a>用戶端的資料夾排除項目

- *用戶端安裝資料夾*\\\*.sdf
- *用戶端安裝資料夾*\ServiceData
- C:\Windows\CCMCache
- C:\Windows\CCMSetup
- *用戶端安裝資料夾*\Logs

### <a name="file-exclusions-for-mps"></a>MP 的檔案排除項目

- POL00000.pol in
  - *MP 安裝資料夾*\PolReqStaging

### <a name="process-exclusions"></a>處理序排除專案

只有在積極的防毒程式將 Configuration Manager 程式檔案 (.exe 檔案) 視為高風險處理序時，才需要處理序排除項目。

- *ConfigMgr 安裝資料夾*\bin\64\Smsexec.exe
- 下列其中一個處理序：
  - *用戶端安裝資料夾*\Ccmexec.exe
  - *MP 安裝資料夾*\Ccmexec.exe
- *用戶端安裝資料夾*\CmRcService.exe (用戶端)
- *ConfigMgr 安裝資料夾*\bin\64\Sitecomp.exe
- *ConfigMgr 安裝資料夾*\bin\64\Smswriter.exe
- *ConfigMgr 安裝資料夾*\bin\64\Smssqlbkup.exe，或 SMS_*SQLFQDN*\bin\x64\Smssqlbkup.exe
- *ConfigMgr 安裝資料夾*\bin\64\Cmupdate.exe
- *用戶端安裝資料夾*\Ccmrepair.exe (用戶端)
- %*windir*%\CCMSetup\Ccmsetup.exe (用戶端)

## <a name="next-steps"></a>後續步驟

如需防毒軟體排除項目的詳細資訊，請參閱下列文章：

[Configuration Manager 最新分支防毒軟體排除項目 -System Center Premier Field Engineer 部落格](https://techcommunity.microsoft.com/t5/core-infrastructure-and-security/configuration-manager-current-branch-antivirus-exclusions/ba-p/884831) \(英文\)

[已更新的 System Center 2012 Configuration Manager 防毒軟體排除項目，含有關 OSD 與開機映像的詳細資料](https://techcommunity.microsoft.com/t5/core-infrastructure-and-security/updated-system-center-2012-configuration-manager-antivirus/ba-p/884371) \(英文\)

[如何選擇防毒軟體以在執行 SQL Server 的電腦上執行](https://support.microsoft.com/help/309422/how-to-choose-antivirus-software-to-run-on-computers-that-are-running-sql-server) \(機器翻譯\)

[執行目前支援之 Windows 版本的企業電腦的病毒掃描建議](https://support.microsoft.com/help/822158/virus-scanning-recommendations-for-enterprise-computers-that-are-running-currently-supported-versions-of-windows)
