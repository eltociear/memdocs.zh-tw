---
title: 從網路共用下載定義
titleSuffix: Configuration Manager
description: 了解如何手動從 Microsoft 下載最新的定義更新，然後將用戶端設定為下載這些定義。
ms.date: 11/18/2019
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: ddef4d2a-f481-4020-9ddd-9cca5f9795cb
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 9afeee7f7111994f0ae3891c7ecd99a11d7edd7d
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81697226"
---
# <a name="enable-endpoint-protection-malware-definitions-to-download-from-a-network-share"></a>啟用 Endpoint Protection 惡意程式碼定義，從網路共用下載

適用於：  Configuration Manager (最新分支)

 您可以手動從 Microsoft 下載最新的定義更新，然後將用戶端設定為從網路上的共用資料夾下載這些定義。 當您使用此更新來源時，使用者也可以初始定義更新。

> [!NOTE]
>  用戶端必須具有共用資料夾的讀取權，才能夠下載定義更新。

 如需如何下載定義及引擎更新以將其儲存在檔案共用上的詳細資訊，請參閱 [Install the latest Microsoft antimalware and antispyware software](https://www.microsoft.com/wdsi/definitions) (安裝最新的 Microsoft 反惡意程式碼和反間諜功能軟體)。

## <a name="to-configure-definition-downloads-from-a-file-share"></a>設定檔案共用中的定義下載

1.  在 Configuration Manager 主控台中，按一下 [資產與合規性]  。

2.  在 [資產與合規性]  工作區中，展開 [Endpoint Protection]  ，然後按一下 [反惡意程式碼原則]  。

3.  開啟 [預設反惡意程式碼原則]  的 [內容] 頁面，或建立新的反惡意程式碼原則。 如需有關如何建立反惡意程式碼原則的詳細資訊，請參閱[如何建立和部署 Endpoint Protection 的反惡意程式碼原則](endpoint-antimalware-policies.md)。

4.  在 [反惡意程式碼內容] 對話方塊的 [安全情報更新]  區段中，按一下 [設定來源]  。
    - 自 Configuration Manager 1902 版起，**定義更新**區段重新命名為**安全情報更新**。

5.  在 [設定定義更新來源]  對話方塊中，選取 [來自 UNC 檔案共用的更新]  。

6.  按一下 [確定]  關閉 [設定定義更新來源]  對話方塊。

7.  按一下 [設定路徑]  。 然後，在 [設定定義更新 UNC 路徑]  對話方塊中，將一或多個 UNC 路徑新增至網路共用上定義更新檔的位置。

8.  按一下 [確定]  關閉 [設定定義更新 UNC 路徑]  對話方塊。


> [!div class="button"]
> [下一個步驟 >](endpoint-antimalware-policies.md)
> 
> [!div class="button"]
> [上一步 >](endpoint-configure-alerts.md)
