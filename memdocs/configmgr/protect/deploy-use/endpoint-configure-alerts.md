---
title: 設定 Endpoint Protection 警示
titleSuffix: Configuration Manager
description: 了解如何在 Configuration Manager 中設定 Endpoint Protection 警示。
ms.date: 03/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: f504de3e-4caf-455c-80d7-a63f13f4c5d9
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 55877923ae2e9a7aa47b3ebe774f7dc0e4ea21a4
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81697336"
---
#  <a name="configure-alerts-for-endpoint-protection-in-configuration-manager"></a>在 Configuration Manager 中設定 Endpoint Protection 警示

適用於：  Configuration Manager (最新分支)

 您可以在 Microsoft Configuration Manager 中設定 Endpoint Protection 警示，以在階層中發生特定事件 (例如惡意程式碼感染) 時通知系統管理使用者。 Configuration Manager 主控台中的 Endpoint Protection 儀表板中，通知顯示在 [監視]  工作區的 [警示]  節點，或是可以用電子郵件傳送給指定的使用者。

 使用本主題中的下列步驟和增補程序，在 Configuration Manager 中設定 Endpoint Protection 的警示。

> [!IMPORTANT]
>  您必須擁有集合的 [強制執行安全性]  權限，以設定 Endpoint Protection 警示。

## <a name="steps-to-configure-alerts-for-endpoint-protection-in-configuration-manager"></a>在 Configuration Manager 中設定 Endpoint Protection 警示的步驟

1.  在 Configuration Manager 主控台中，按一下 [資產與合規性]  。

2.  在 [資產與相容性]  工作區中，按一下 [裝置集合]  。

3.  在 [裝置集合]  清單中，選取您要用於設定警示的集合，然後在 [首頁]  索引標籤的 [內容]  群組中按一下 [內容]  。

    > [!NOTE]
    >  您無法設定使用者集合的警示。

4.  如果您想要在 Configuration Manager 主控台的 [監視]  工作區中，檢視此集合的反惡意程式碼作業詳細資料，請在 [<集合名稱\>  屬性]  對話方塊的 [警示]  索引標籤上，選取 [在 Endpoint Protection 儀表板中檢視此集合]  。

    > [!NOTE]
    >  此選項無法供 [所有系統]  集合使用。

5.  在 [<集合名稱\>  屬性]  對話方塊的 [警示]  索引標籤中，按一下 [新增]  。

6.  在 [新增集合警示]  對話方塊的 [適用這些狀況時產生警示]  區段中，選取當發生指定的 Endpoint Protection 事件時，您希望 Configuration Manager 所產生的警示，然後按一下 [確定]  。

7.  在 [警示]  索引標籤的 [條件]  清單中，選取每個 Endpoint Protection 警示，然後指定下列資訊：

    -   **警示名稱** - 接受預設名稱或輸入新的警示名稱。

    -   **警示嚴重性** - 在清單中，選取要在 Configuration Manager 主控台中顯示的警示等級。

8.  根據您選取警示指定下列的額外資訊：

    -   **惡意程式碼偵測** - 您所監視集合中的任何電腦上偵測到惡意程式碼時，就會產生此警示。 **惡意程式碼偵測閾值** - 指定產生此警示的惡意程式碼偵測層級：

        -   **高 - 所有偵測** - 當指定集合中的一或多部電腦上偵測到任何惡意程式碼時，無論 Endpoint Protection 用戶端採用何種動作，都會產生警示。

        -   **中 - 已偵測，擱置動作** - 當指定集合中的一或多部電腦上偵測到惡意程式碼時，就會產生警示，而您必須手動移除惡意程式碼。

        -   **低 - 已偵測，仍在作用中** - 當指定集合中的一或多部電腦上偵測到惡意程式碼，且惡意程式碼還在活動時，就會產生警示。

    -   **惡意程式碼爆發** - 您所監視之集合中的指定百分比電腦上偵測到特定惡意程式碼時，就會產生此警示。

        -   **偵測到惡意程式碼的電腦百分比** - 當集合中的電腦所偵測到惡意程式碼的百分比超過您指定的百分比時，就會產生警示。 在 **1** 到 **99**的範圍中指定一個百分比。

            > [!NOTE]
            >  百分比值是根據集合中的電腦數目決定，但會排除沒有安裝 Configuration Manager 用戶端的電腦。 其會包含尚未安裝 Endpoint Protection 用戶端的電腦。

    -   **重複的惡意程式碼偵測** - 在您所監視之集合中的電腦上，在指定的小時數中偵測到特定惡意程式碼的次數超過指定次數時，就會產生警示。 指定下列資訊來設定此警示：

        -   **偵測到惡意程式碼的次數：** - 當集合中的電腦上偵測到相同惡意程式碼的次數超過指定次數時，就會產生警示。 在 **2** 到 **32**的範圍中指定一個數字。

        -   **偵測間隔 (小時)：** 指定偵測間隔 (以小時為單位)，在該間隔內必須執行一定數目的惡意程式碼偵測。 在 **1** 到 **168**的範圍中指定一個數字。

    -   **多重惡意程式碼偵測** - 在您所監視之集合中的電腦上，於指定的小時數中所偵測到惡意程式碼類型的數目超過指定數目時，就會產生此警示。 指定下列資訊來設定此警示：

        -   **偵測到的惡意程式碼類型數目：** 當在集合中的電腦上偵測到指定數目的不同惡意程式碼類型時，就會產生警示。 在 **2** 到 **32**的範圍中指定一個數字。

        -   **偵測間隔 (小時)：** 指定偵測間隔 (以小時為單位)，在該間隔內必須執行一定數目的惡意程式碼偵測。 在 **1** 到 **168**的範圍中指定一個數字。

9. 按一下 [確定]  以關閉 [<集合名稱\>  屬性]  對話方塊。  

## <a name="alert-for-outdated-malware-client"></a>到期惡意程式碼用戶端的警示

從 Configuration Manager 1702 版開始，您可以設定警示來確保 Endpoint Protection 用戶端未過期。 從任何裝置集合，您現在可以將資料行新增至下列屬性的清單：**反惡意程式碼用戶端版本**和 **Endpoint Protection 部署狀態**。 例如，在主控台中，巡覽至 [資產與相容性]   > [概觀]   > [裝置集合]   > [所有桌面和伺服器用戶端]  。 以滑鼠右鍵按一下資料行標頭，並選取要新增的資料行。 若要檢查警示，請檢視 [監視]  工作區中的 [警示]  。 如果超過 20% 的受管理用戶端執行反惡意程式碼軟體過期版本，則會顯示「反惡意程式碼用戶端版本已過期」警示。 此警示不會出現在 [監視]   > [概觀]  索引標籤上。若要更新過期的反惡意程式碼用戶端，請啟用反惡意程式碼用戶端的軟體更新。

若要設定產生警示的百分比，請展開 [監視]   > [警示]   > [所有警示]  ，然後按兩下 [反惡意程式碼用戶端已過期]  ，並修改 [如果具有反惡意程式碼用戶端過期版本的受管理用戶端百分比超過下列數值，則產生警示]  選項。

> [!div class="button"]
> [下一個步驟 >](endpoint-definition-updates.md)
> 
> [!div class="button"]
> [上一步 >](endpoint-protection-site-role.md)
