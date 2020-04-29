---
title: 從 Microsoft 下載定義
titleSuffix: Configuration Manager
description: 了解如何啟用從 Microsoft Updates 針對 Configuration Manager 下載 Endpoint Protection 惡意程式碼定義。
ms.date: 11/18/2019
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: ab7626ae-d4bf-4ca6-ab25-c61f96800a02
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 1f0d8ac635d514e750584126458bfde6b5fc24ee
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81697236"
---
# <a name="enable-endpoint-protection-malware-definitions-to-download-from-microsoft-updates"></a>啟用 Endpoint Protection 惡意程式碼定義，從 Microsoft Updates 下載

適用於：  Configuration Manager (最新分支)

當您選擇從 Microsoft Update 下載定義更新檔時，用戶端會在反惡意程式碼原則對話方塊 [安全情報更新]  區段中所定義的間隔檢查 Microsoft Update 網站。

 當用戶端並沒有 Configuration Manager 站台的連線，或是要讓使用者可以初始定義更新時，這個方法就很有用。

> [!IMPORTANT]
> - 用戶端必須要能夠在網際網路上存取 Microsoft Update，以使用這個方法來下載定義更新。
> - 自 Configuration Manager 1902 版起，[定義更新]  區段重新命名為 [安全情報更新]  。

## <a name="using-the-microsoft-malware-protection-center-to-download-definitions"></a>使用 Microsoft 惡意程式碼防護中心下載定義
 您可以將用戶端設定為從 Microsoft 惡意程式碼防護中心下載定義更新。 如果 Endpoint Protection 用戶端尚無法從其他來源下載更新，則會使用此選項來下載定義更新。 如果 Configuration Manager 基礎結構發生問題造成無法傳遞更新時，此更新方法就很有用。

> [!IMPORTANT]
>  用戶端必須要能夠在網際網路上存取 Microsoft Update，以使用這個方法來下載定義更新。
> 
> 
> [!div class="button"]
> [下一個步驟 >](endpoint-antimalware-policies.md)
> 
> [!div class="button"]
> [上一步 >](endpoint-configure-alerts.md)
