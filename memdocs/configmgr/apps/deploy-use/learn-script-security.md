---
title: 深入了解 PowerShell 指令碼安全性
titleSuffix: Configuration Manager
description: 可協助您了解 PowerShell 指令碼安全性的資源。
ms.date: 03/22/2018
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: a0bd093d-67a5-4f74-bf79-dd604889f5ba
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 6b519d60be094bb7c39f738d04322009b36a409f
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2020
ms.locfileid: "82075858"
---
# <a name="learn-more-about-powershell-script-security"></a>深入了解 PowerShell 指令碼安全性

適用於：  Configuration Manager (最新分支)

系統管理員需負責驗證其環境中建議的 PowerShell 和 PowerShell 參數使用方式。 以下是一些有幫助的資源，可協助系統管理員了解 PowerShell 的強大功能及可能的風險面。 這是要協助降低潛在的風險面，以及允許使用安全的指令碼。

## <a name="powershell-script-security"></a>PowerShell 指令碼安全性
「執行指令碼」內建一項功能，可讓您以視覺方式檢閱及核准被要求在環境中執行的指令碼。 系統管理員應了解 PowerShell 指令碼可能含有混淆的指令碼：惡意且難以在指令碼核准過程中透過視覺檢查偵測到的指令碼。 就最佳做法而言，除了以視覺方式檢閱 PowerShell 指令碼之外，也使用特定檢查工具，將可協助偵測可疑的指令碼問題。 這些工具並不總是能夠判斷出 PowerShell 作者的意圖，以便讓人注意到可疑的指令碼。 不過，這些工具會要求系統管理員判斷它是否為惡意或故意的指令碼語法。

## <a name="recommendations"></a>建議
- 使用下列參考的各種連結來熟悉 PowerShell 安全性最佳做法。
- **簽署您的指令碼**：另一個確保指令碼安全的方法是在匯入指令碼以供使用之前，先進行審查，然後予以簽署。
- 請勿將祕密 (例如密碼) 儲存在 PowerShell 指令碼中，並請深入了解如何處理祕密。


## <a name="general-information-about-powershell-security-best-practices"></a>PowerShell 安全性最佳做法的一般相關資訊

以下是精選的一系列連結，可為 Configuration Manager 系統管理員提供一個了解 PowerShell 指令碼安全性最佳做法的起點。  

[PowerShell 安全性最佳做法簡介](https://blogs.msdn.microsoft.com/powershell/2013/12/16/powershell-security-best-practices/ ) \(英文\)

[PowerShell 安全性最佳做法 PowerPoint](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/74/metablogapi/1055.PowerShell-Security-Best-Practices_3CA24C32.pptx) \(英文\)

<iframe src="https://channel9.msdn.com/Events/Blue-Hat-Security-Briefings/BlueHat-Security-Briefings-Fall-2013-Sessions/PowerShell-Best-Practices/player" width="960" height="540" allowFullScreen frameBorder="0"></iframe>

[抵禦 PowerShell 攻擊 (PowerShell 小組部落格)](https://blogs.msdn.microsoft.com/powershell/2017/10/23/defending-against-powershell-attacks/) \(英文\)

[抵禦 PowerShell 攻擊 Twitter (Microsoft PowerShell 與安全性宣導員 Lee Holmes)](https://twitter.com/Lee_Holmes/status/922462821081694208) \(英文\)

[防止惡意程式碼導入](https://blogs.msdn.microsoft.com/powershell/2006/11/22/protecting-against-malicious-code-injection/) \(英文\)

[PowerShell The Blue Team 探討深度指令碼區塊記錄、受保護的事件記錄、反惡意程式碼掃描介面、安全碼產生 API](https://blogs.msdn.microsoft.com/powershell/2015/06/09/powershell-the-blue-team/) \(英文\)

[針對 Windows 10，有一個適用於反惡意程式碼掃描介面的 API](https://cloudblogs.microsoft.com/microsoftsecure/2015/06/09/windows-10-to-offer-application-developers-new-malware-defenses/?source=mmpc) \(英文\)

## <a name="powershell-parameters-security"></a>PowerShell 參數安全性
傳遞參數是一種讓指令碼保有彈性並延遲到執行階段再做決定的方式。 它也開啟了另一個風險面。 防止惡意參數或指令碼導入的最佳做法是：

- 只允許使用預先定義的參數。
- 使用規則運算式功能來驗證所允許的參數。
    - 範例：如果只允許特定範圍的值，請使用規則運算式來只檢查是否有可構成此範圍的字元或值。
    - 驗證參數有助於防止使用者嘗試使用可逸出的特定字元，例如引號。 請注意，引號可能有多種類型，因此使用規則運算式來驗證哪些字元是您已決定允許的，通常比嘗試定義所有不允許的輸入值簡單。
- 利用「PowerShell 資源庫」中的 PowerShell 模組["injection hunter"](https://www.powershellgallery.com/packages/InjectionHunter/1.0.0)。
    - 可能會有誤判的情況，因此當有項目被標示為可疑時，請尋找意圖來判斷是否真的有問題。 
- Microsoft Visual Studio 有一個指令碼分析器，可以協助檢查 PowerShell 語法。
- 這個標題為"DEF CON 25 - Lee Holmes - Get $pwnd:Attacking Battle Hardened Windows Server" (DEF CON 25 - Lee Holmes - 遭到入侵：攻擊戰鬥讓 Windows Server 變得更強) 的影片簡述您可以防護的問題類型 (尤其是 12:20 到 17:50 的這一段)：    <iframe width="560" height="315" src="https://www.youtube.com/embed/ahxMOAAani8" frameborder="0" allow="autoplay; encrypted-media" allowfullscreen></iframe>

## <a name="environment-recommendations"></a>環境建議
給 PowerShell 系統管理員的一般建議。
1. 部署 Windows 10 內建的最新版 PowerShell，例如第 5 版或更新版本。 或者，您也可以部署 [Windows Management Framework](https://www.microsoft.com/download/details.aspx?id=54616)。 
2. 啟用並收集 PowerShell 記錄，可視需要包含「受保護的事件記錄」。 將這些記錄合併至您的簽章、尋找及事件回應工作流程中。
3. 在高價值系統上實作「恰到好處的系統管理」，以消除或減少對這些系統進行的無限制系統管理存取。
4. 部署 Windows Defender 應用程式控制原則，以在允許預先核准的系統管理工作使用完整 PowerShell 語言功能的同時，又限制對 PowerShell 語言的一組有限子集進行互動和未經核准的使用。
5. 部署 Windows 10 以向您的防毒提供者提供 Windows Scripting Host (包括 PowerShell) 所處理之所有內容的完整存取權 (包括在執行階段產生或釐清的內容)。
