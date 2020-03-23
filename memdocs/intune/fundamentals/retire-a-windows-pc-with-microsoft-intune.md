---
title: 淘汰 Windows 電腦
titleSuffix: Microsoft Intune
description: 如何淘汰受 Intune 管理的 Windows 電腦。
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
ms.assetid: 5c916182-d99c-44c5-a779-3f596f261c40
ms.reviewer: owenyen
ms.suite: ems
search.appverid: MET150
ms.custom: intune-classic-keep
ms.collection: M365-identity-device-management
ms.openlocfilehash: e7d88b5ba8f5071821d1a9901a26bfb4a5a6fbd3
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/13/2020
ms.locfileid: "79356475"
---
# <a name="retire-a-windows-pc"></a>淘汰 Windows 電腦

[!INCLUDE [classic-portal](../includes/classic-portal.md)]

使用下列步驟，在電腦上執行 Intune 軟體用戶端，來淘汰您以電腦形式進行管理的桌面。 淘汰電腦後，即會將其從 Intune 管理中移除。 您無法透過 Intune 抹除電腦的方式，將其設回原始出廠設定。

1. 在 [Microsoft Intune 管理主控台](https://manage.microsoft.com/)中，選擇 [群組]  &gt; [所有裝置]  (或另一個群組，其中包含所要淘汰的電腦)。

2. 選取您要淘汰的裝置，然後選擇 [淘汰/抹除]  。

若要將電腦重新註冊到 Intune 中，請參閱[使用 Microsoft Intune 安裝 Windows 電腦用戶端](install-the-windows-pc-client-with-microsoft-intune.md)的指引，在電腦上重新安裝軟體用戶端。

如果電腦無法連線到 Intune，[儀表板]  工作區中會顯示相關訊息。

淘汰電腦時：

- 它會從 Intune 管理及清查中移除，而與該電腦相關聯的授權將可重複使用。 [淘汰/抹除] 會移除 Intune 軟體用戶端，但不會從電腦移除應用程式或資料。 這項淘汰作業不會在電腦上執行完整抹除。

- 其狀態不再顯示在 Intune 主控台中。

- Intune 會從電腦移除軟體用戶端。 如果電腦未連線到 Intune 服務，則會在下次連線時移除軟體用戶端。

- Microsoft Intune Endpoint Protection 會從電腦移除。 如果電腦已安裝其他端點防護應用程式且已停用，則在移除 Microsoft Intune Endpoint Protection 之後，該應用程式可以重新啟用，並確保您的電腦受到保護。

- 所有原則都會從電腦移除，而且原則所設定的值將會變更。

- 電腦不會再從 Intune 服務接收軟體更新或惡意程式碼定義更新。

- 已淘汰的電腦仍可使用 Windows Server Update Services、Windows Update 或 Microsoft Update 繼續接收更新 (依據這些電腦的設定方式而定)。

    > [!IMPORTANT]
    > 如果用戶端軟體是使用群組原則物件 (GPO) 安裝，您必須先移除群組原則物件 (GPO)，然後才能移除用戶端軟體，以避免重新安裝軟體。

    如果無法解除安裝 Endpoint Protection 用戶端，請參閱 [Endpoint Protection 疑難排解](/intune/troubleshoot-endpoint-protection-in-microsoft-intune)，以取得詳細說明。

## <a name="see-also"></a>請參閱

[使用 Intune 軟體用戶端執行的一般 Windows 電腦管理工作](common-windows-pc-management-tasks-with-the-microsoft-intune-computer-client.md)
