---
title: 監視憑證設定檔
titleSuffix: Configuration Manager
description: 了解如何監視 Configuration Manager 憑證設定檔的合規性狀態。
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: 98feaa06-64b1-4e86-a122-93017c97cd4f
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: ee1f43e113aa91f75c09bd264e8b3bc2704220a8
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81706306"
---
# <a name="how-to-monitor-certificate-profiles-in-configuration-manager"></a>如何在 Configuration Manager 中監視憑證設定檔

適用於：  Configuration Manager (最新分支)


##  <a name="view-compliance-results-in-the-configuration-manager-console"></a>在 Configuration Manager 主控台中檢視合規性結果  

若要監視 SCEP 憑證合規性，請不要使用主控台，而改為使用[報告](#view-compliance-results-by-using-reports)。 

1. 在 Configuration Manager 主控台中，選擇 [監視]  >  [部署]  。  

2. 選取感興趣的憑證設定檔部署。  

3. 檢閱主要頁面上的摘要憑證合規性資訊。 如需更更詳細資訊，請選取憑證設定檔，然後在 [首頁]  索引標籤的 [部署]  群組中，選擇 [檢視狀態]  以開啟 [部署狀態]  頁面。  

    [部署狀態]  頁面包含下列索引標籤：  

   -   **符合規範**：根據受影響的資產數目，顯示憑證設定檔的合規性。 您可以按兩下規則，在 [資產與相容性]  工作區的 [使用者]  節點下方建立臨時節點。 這個節點包含與此憑證設定檔相容的所有使用者。 [資產詳細資料]  窗格也顯示與這個設定檔相容的使用者。 如需詳細資訊，請按兩下清單中的使用者。  

       > [!IMPORTANT]  
       >  如果憑證設定檔在用戶端裝置上不適用，就不會進行評估； 不過，仍會傳回為相容。  

   -   **錯誤**：根據受影響的資產數目，顯示一份所選憑證設定檔部署的所有錯誤清單。 您可以按兩下規則，在 [資產與相容性]  工作區的 [使用者]  節點下方建立臨時節點。 這個節點包含因為這個設定檔而產生錯誤的所有使用者。 當您選取使用者時，[資產詳細資料]  窗格會顯示受到所選問題影響的使用者。 按兩下清單中的使用者，以顯示詳細資訊。  

   -   **不符合規範**：根據受影響的資產數目，顯示一份憑證設定檔中所有不相容規則的清單。 您可以按兩下規則，在 [資產與相容性]  工作區的 [使用者]  節點下方建立臨時節點。 這個節點包含與這個設定檔不相容的所有使用者。 當您選取使用者時，[資產詳細資料]  窗格會顯示受到所選問題影響的使用者。 按兩下清單中的使用者以顯示與此問題有關的進一步資訊。  

   -   **未知**：顯示一份未回報所選憑證設定檔部署的合規性，以及裝置目前的用戶端狀態的所有使用者清單。  

4. 在 [部署狀態]  頁面上，檢閱有關部署之憑證設定檔合規性的詳細資訊。 [部署]  節點下方會建立一個臨時節點以協助您更快再找到此資訊。  

    憑證的註冊狀態會以數字顯示。 請使用下表瞭解每個數字代表的意義：  


   | 註冊狀態 |                                                                                                                   說明                                                                                                                   |
   |-------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
   |    0x00000001     |                                                                                         註冊成功，且已發行憑證。                                                                                          |
   |    0x00000002     |                                                                    要求已提出，但註冊尚待處理，或要求已被認定超出訊號範圍。                                                                    |
   |    0x00000004     |                                                                                                          註冊必須延後。                                                                                                           |
   |    0x00000010     |                                                                                                               發生錯誤。                                                                                                                |
   |    0x00000020     |                                                                                                        註冊狀態未知。                                                                                                        |
   |    0x00000040     | 狀態資訊已略過。 如果 HYPERLINK "<https://msdn.microsoft.com/windows/ms721572>" \l "_security_certification_authority_gly" 憑證授權單位無效或尚未被選取進行監視，就可能發生此情況。 |
   |    0x00000100     |                                                                                                           註冊已被拒。                                                                                                           |

##  <a name="view-compliance-results-by-using-reports"></a>使用報告檢視合規性結果

Configuration Manager 中的合規性設定包含內建報告，您可利用這些報告來監視憑證設定檔的相關資訊。 這些報告具有 [相容性和設定管理]  的報告類別。  

> [!IMPORTANT]  
>  當您在相容性設定的報告中使用 [裝置篩選器]  和 [使用者篩選器]  參數時，必須使用萬用字元 (%)。  

若要監視 SCEP 憑證合規性，請使用報告節點 [公司資源存取]  下的這些憑證報告：  

-   憑證發行歷程記錄  
-   憑證即將到期的資產清單  
-   依憑證發行狀態列出的資產清單  



 如需如何在 Configuration Manager 中設定報告的詳細資訊，請參閱[報告簡介](../../core/servers/manage/introduction-to-reporting.md)。  
