---
title: Microsoft Intune 中的 Windows 資訊保護設定
titleSuffix: Microsoft Intune
description: 了解您可用於管理 Windows 資訊保護的相關 Microsoft Intune 設定。
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 01/18/2018
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.reviewer: heenamac
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 0d127dd8ba455ecb7e10fc94c343d12099a678d5
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2020
ms.locfileid: "82079003"
---
# <a name="how-to-configure-windows-information-protection-in-microsoft-intune"></a>如何在 Microsoft Intune 中設定 Windows 資訊保護

[!INCLUDE [azure_portal](../includes/azure_portal.md)]

企業中員工擁有的裝置日漸增加，資料不慎從企業難以控管的應用程式和服務 (如電子郵件、社交媒體和公用雲端) 外洩的風險也更高。 例如，員工從個人電子郵件帳戶傳送最新的工程圖片、將產品資訊複製並貼到推文中，或將進行中的銷售報表儲存到公用雲端存放裝置。

**Windows 資訊保護**有助於防範這類可能的資料外洩，而不會干擾員工的體驗。 它也能協助保護企業應用程式與資料，防止企業擁有的裝置和員工帶到公司的個人裝置意外外洩資料，而且不需要對您的環境或其他應用程式進行任何變更。

Intune 原則會管理受 Windows 資訊保護、企業網路位置、保護等級和加密設定所保護的應用程式清單。

>[!NOTE]
> 若要搭配使用 Windows 10 公司入口網站應用程式和 Windows 資訊保護，則您必須在 Windows 資訊保護的「豁免」  模式下新增公司入口網站應用程式。 

如需詳細資訊，請參閱：
- [使用 Windows 資訊保護來保護您的企業資料](https://technet.microsoft.com/itpro/windows/keep-secure/protect-enterprise-data-using-wip)。
- [使用 Microsoft Intune 的傳統主控台建立 Windows 資訊保護 (WIP) 原則](https://docs.microsoft.com/windows/threat-protection/windows-information-protection/create-wip-policy-using-intune)
- [使用 Microsoft Intune 的 Azure 入口網站建立附帶 MDM 的 Windows 資訊保護 (WIP) 原則](https://docs.microsoft.com/windows/threat-protection/windows-information-protection/create-wip-policy-using-intune-azure)
- [使用 Microsoft Intune 的 Azure 入口網站建立附帶 MAM 的 Windows 資訊保護 (WIP) 原則](https://docs.microsoft.com/windows/threat-protection/windows-information-protection/create-wip-policy-using-mam-intune-azure)
