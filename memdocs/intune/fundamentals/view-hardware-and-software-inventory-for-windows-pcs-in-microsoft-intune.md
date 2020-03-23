---
title: 檢視 Windows 電腦的硬體和軟體清查
titleSuffix: Microsoft Intune
description: 如何檢視您使用 Intune 軟體用戶端作為電腦管理之 Windows 桌上型電腦的硬體和軟體資訊。
keywords: ''
author: dougeby
ms.author: dougeby
manager: dougeby
ms.date: 06/26/2019
ms.topic: archived
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: medium
ms.technology: ''
ms.assetid: 3c10f4c9-520b-4864-92fc-a45a9f640ad4
ms.reviewer: owenyen
ms.suite: ems
search.appverid: MET150
ms.custom: intune-classic-keep
ms.collection: M365-identity-device-management
ms.openlocfilehash: 9e2d5e3f1e5839040c3ffd2229c34f3063a3ce87
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/13/2020
ms.locfileid: "79354694"
---
# <a name="view-hardware-and-software-inventory-for-windows-pcs"></a>檢視 Windows 電腦的硬體和軟體清查

[!INCLUDE [classic-portal](../includes/classic-portal.md)]

> [!NOTE]
> 本主題中的資訊僅適用於使用 Intune 軟體用戶端作為電腦所管理的 Windows 桌上型電腦。 如果想要檢視註冊為行動裝置的 Windows 電腦清查，請參閱[在 Intune 中檢視裝置詳細資料](../remote-actions/device-inventory.md)。

Intune 會收集您使用 Intune 軟體用戶端作為電腦管理之桌上型電腦的硬體和軟體詳細資訊。 請使用下列程序中的資訊，瞭解如何建立：

- 列出您所管理之電腦的硬體功能相關資訊的報表。

- 列出每部電腦所安裝軟體的報表。

- 如何重新整理電腦清查以確保報表中的資料是最新的。

## <a name="to-display-information-about-pcs-you-manage"></a>顯示您所管理電腦的相關資訊

1. 在 [Microsoft Intune 管理主控台](https://manage.microsoft.com/)中，選擇 [報表]  &gt; [電腦清查報表]  。

2. 在 [建立新報表]  頁面上，接受預設值或進行自訂，以篩選報表將傳回的結果。 例如，您可以選擇只讓執行 Windows 8.1 的電腦顯示在報表中。

3. 選擇 [檢視報表]  ，在新視窗中開啟 [電腦清查報表]  。

    您可以選取每個欄標題，依任何一欄排序報表，例如 [名稱]  、[底座類型]  或 [製造商]  。

## <a name="to-display-software-installed-on-pcs-you-manage"></a>顯示您所管理電腦上安裝的軟體

1. 在 [Microsoft Intune 管理主控台](https://manage.microsoft.com/)中，選擇 [報表]  &gt; [軟體清查報表]  。

2. 在 [建立新報表]  頁面上，接受預設值或進行自訂，以篩選報表將傳回的結果。 例如，您可以選擇只讓 Microsoft 發佈的軟體顯示在報表中。

3. 選擇 [檢視報表]  ，在新視窗中開啟 [軟體清查報表]  。

    您可以選擇每個欄標題，依任何一欄排序報表，例如 [名稱]  、[發行者]  或 [類別]  。 您可以選擇清單項目旁的方向箭頭，展開清單中的更新來顯示更多詳細資訊 (例如安裝軟體的電腦)。

## <a name="to-refresh-computer-inventory-to-ensure-it-is-current"></a>若要重新整理電腦清查以確保它是最新的

1. 在 [Microsoft Intune 管理主控台](https://manage.microsoft.com/)中，選擇 [群組]  &gt; [所有裝置]  (或您要重新整理清查的電腦所屬其他群組)。

2. 選取電腦，或按住 **Ctrl** 鍵選取多部電腦。

3. 在工作列上，選擇 [遠端工作]  &gt; [重新整理清查]  。

4. 若要檢視工作狀態，請選擇頁面右下角的 [遠端工作]  。

    [工作狀態]  對話方塊會顯示目前的遠端工作、工作狀態、裝置名稱和任何回報的錯誤，並提供疑難排解資訊的連結。

## <a name="see-also"></a>請參閱

[使用 Intune 軟體用戶端執行的一般 Windows 電腦管理工作](common-windows-pc-management-tasks-with-the-microsoft-intune-computer-client.md)
