---
title: Intune 在中國由 21Vianet 營運
titleSuffix: ''
description: Intune 在中國由 21Vianet 營運。
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 05/27/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: high
ms.assetid: ''
ms.reviewer: amsaeedi
ms.suite: ems
search.appverid: MET150
ms.custom: intune-classic; get-started
ms.collection: M365-identity-device-management
ms.openlocfilehash: 879cb5d1659b886a01e564574452bd9e5370664c
ms.sourcegitcommit: b0ae4a9972bac3518d0d4f33e033ac492eefe3c1
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/28/2020
ms.locfileid: "84126810"
---
# <a name="intune-operated-by-21vianet-in-china"></a>Intune 在中國由 21Vianet 營運  

由 21Vianet 營運的 Intune 的設計可符合中國對雲端服務的安全性、可靠性與可擴縮性要求。 Intune 即服務是以 Microsoft Azure 為基礎而建置的。 由 21Vianet 營運的 Microsoft Azure 是位於中國、實體獨立的雲端服務執行個體。 其由 21Vianet 獨立營運及交易。 此服務使用由 Microsoft 授權給 21Vianet 的技術。

Microsoft 不會參與服務本身的實際營運。 服務由 21Vianet 獨立營運、提供及管理。 21Vianet 是位於中國的網際網路資料中心服務提供者。 其提供主機服務、受控網路服務，以及雲端運算基礎結構服務。 21Vianet 使用 Microsoft 授權的技術來營運當地資料中心，讓您能夠使用 Intune 服務，同時將您的資料保留在中國。 21Vianet 也為您提供訂用帳戶、帳單與支援服務。

[!INCLUDE [GDPR-related guidance](../includes/gdpr-dsr-and-stp-note.md)]

## <a name="feature-differences-in-intune-operated-by-21vianet"></a>由 21Vianet 營運之 Intune 中的功能差異

由於中國服務是由中國內部的合作夥伴營運，因此 Intune 會有一些功能上的差異。 

- 由 21Vianet 營運的 Intune 僅支援獨立部署。 System Center Configuration Manager 的共同管理支援目前正在開發中。
- 不支援從公用雲端移轉到主權雲端。 有興趣移至由 21Vianet 營運之 Intune 的客戶必須進行手動移轉。
- 目前不支援租用戶連結功能 (將裝置同步至 Intune，而不註冊以支援雲端主控台案例)。
- 由 21Vianet 營運的 Intune 不支援 Intune 代理程式，因此不支援舊版電腦管理。
- 對 Windows 10 管理的支援是透過新式 MDM 通道來達成的。
- 由 21Vianet 營運的 Intune 不支援內部部署 Exchange Connector。
- Windows Autopilot 與商務用市集功能目前無法使用。
- 因為中國不提供 Google 行動服務，所以由 21Vianet 營運之 Intune 的客戶無法使用需要 Google 行動服務的功能。 這些功能包括：
  - Google Play Protect 功能，例如 SafetyNet 裝置證明。
  - 從 Google Play 商店管理應用程式。
  - Android Enterprise 功能。 如需詳細資訊，請參閱此 [Google 文件](https://support.google.com/work/android/answer/6270910?hl=en)。
- 適用於 Android 的 Intune 公司入口網站應用程式會使用 Google 行動服務來與 Microsoft Intune 服務通訊。 由於 Google Play 服務在中國無法使用，因此某些工作最多可能需要 8 小時才能完成。 如需詳細資訊，請參閱這篇[文章](https://docs.microsoft.com/mem/intune/apps/manage-without-gms#limitations-of-intune-device-administrator-management-when-gms-is-unavailable)。 
- 為了遵循當地法規並提供改良的功能，在中國的 Intune 用戶端體驗 (公司入口網站應用程式) 可能會有所不同。
- 隔離 (Fencing) 功能無法使用。
- 行動應用程式管理 (MAM) 可用性視在中國可用的應用程式而定。

## <a name="you-control-customer-data"></a>控制客戶資料

在由 21Vianet 營運的 Microsoft Azure、Intune、Office 365 與 Power BI 中，您可以完全掌控您的資料：
- 您知道客戶資料的所在位置。
- 您可以控制客戶資料的存取權。
- 如果您離開服務，您可以控制客戶資料。
- 您可以控制客戶資料的安全性。

使用由 21Vianet 營運的 Microsoft Azure、Intune、Office 365 與 Power BI，您的資料完全由您所擁有：
- 21Vianet 不會使用客戶資料來發送廣告。
- 您可以控制客戶資料的存取權。
- 我們使用邏輯隔離來隔離每個客戶的資料。
- 我們提供簡單、透明的資料使用原則，並取得獨立的稽核。
- 我們的轉包商與我們訂有合約，必須符合我們的隱私權需求。

## <a name="data-subject-requests"></a>資料主體要求

由 21Vianet 營運之 Intune 的租用戶系統管理員角色可以透過下列方式要求資料主體的資料：

- 使用 Azure Active Directory 系統管理中心，租用戶系統管理員可以從 Azure Active Directory 與相關服務永久刪除資料主體。 如需詳細資訊，請參閱 [Azure 資料主體要求 - 刪除](https://docs.microsoft.com/microsoft-365/compliance/gdpr-dsr-azure?view=o365-worldwide#step-5-delete)
- 由 21Vianet 營運之 Microsoft 服務的系統產生記錄檔，可由租用戶系統管理員使用「資料記錄匯出」功能來匯出。 如需詳細資訊，請參閱 [Azure 資料主體要求 - 匯出](https://docs.microsoft.com/microsoft-365/compliance/gdpr-dsr-azure?view=o365-worldwide#step-6-export)。

## <a name="next-steps"></a>後續步驟

[深入了解 Intune 支援的設定](supported-devices-browsers.md)