---
title: 使用原則來簡化 Windows 電腦管理
titleSuffix: Microsoft Intune
description: 描述 Windows 電腦管理原則和 Microsoft Intune Center 的設定。
keywords: ''
author: dougeby
ms.author: dougeby
manager: dougeby
ms.date: 01/01/2018
ms.topic: archived
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: medium
ms.technology: ''
ms.assetid: f0afda7e-f4c3-4bcd-b4bf-4304103cf73e
ms.reviewer: owenyen
ms.suite: ems
search.appverid: MET150
ms.custom: intune-classic-keep
ms.collection: M365-identity-device-management
ms.openlocfilehash: 275939c4c97b25f7e9b2ab179a7491d47801e48e
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/13/2020
ms.locfileid: "79355058"
---
# <a name="use-policies-to-simplify-windows-pc-management"></a>使用原則來簡化 Windows 電腦管理

[!INCLUDE [classic-portal](../includes/classic-portal.md)]

若要在 Windows 桌面執行 Intune 軟體用戶端，將 Windows 桌面作為電腦管理，您只能使用 Intune 管理主控台原則 [電腦管理]  下的原則。 管理主控台中列出的所有其他原則僅供行動裝置使用。 使用 [電腦管理]  原則，您可以設定 Microsoft Intune Center 的設定、控制電腦的更新，以及設定電腦的 Windows 防火牆。

![Windows 電腦的原則範本](./media/use-policies-to-simplify-windows-pc-management/pc_policy_template.png)

## <a name="manage-the-microsoft-intune-center"></a>管理 Microsoft Intune Center
使用者會將 Intune 軟體用戶端視為 **Microsoft Intune Center**。 Microsoft Intune Center 可讓使用者︰

- 從公司入口網站取得應用程式。

- 檢查更新。

- 管理 Microsoft Intune Endpoint Protection。

- 要求遠端協助。

Microsoft Intune Center 會安裝在所有受管理電腦上。 您可以在 Intune 中進行下列設定，而使用者會在 Microsoft Intune Center 中看到這些設定：

|原則設定|詳細資料|
|------------------|--------------------|
|**Name**|管理電腦的系統管理員名稱。<br />長度上限：40 個字元|
|**電話號碼**|管理電腦之系統管理員的電話號碼。<br />長度上限：20 個字元|
|**電子郵件地址**|管理電腦之系統管理員的電子郵件地址。<br />長度上限：40 個字元|
|**網站名稱**|使用者支援網站的名稱。<br />>長度上限：40 個字元|
|**網站 URL**|您的支援網站的 URL。<br />長度上限：150 個字元|
|**附註**|使用者看到的附註。<br />長度上限：120 個字元|

請參閱下列資源以取得您可以為 Windows 電腦設定之原則和設定的相關資訊︰

- [在 Microsoft Intune 中使用軟體更新讓 Windows 電腦維持最新狀態](keep-windows-pcs-up-to-date-with-software-updates-in-microsoft-intune.md) - 這些原則會讓受控的電腦檢查軟體更新，並從 Microsoft 和協力廠商下載軟體更新。 這些更新不包括 OS 升級 (例如從 Windows 7 升級為 Windows 10，或將一種 Windows 10 版本升級為更新版本)。

- [使用 Microsoft Intune 的 Endpoint Protection 協助保護 Windows 電腦](help-secure-windows-pcs-with-endpoint-protection-for-microsoft-intune.md) - 這些設定包括掃描排程，以及偵測到惡意程式碼時要採取的動作。

- [在 Microsoft Intune 中使用 Windows 防火牆原則協助保護 Windows 電腦](help-protect-windows-pcs-using-windows-firewall-policies-in-microsoft-intune.md) - 這些原則可簡化受管理電腦上的 Windows 防火牆設定管理。

## <a name="see-also"></a>請參閱

[使用 Intune 軟體用戶端執行的一般 Windows 電腦管理工作](common-windows-pc-management-tasks-with-the-microsoft-intune-computer-client.md)
