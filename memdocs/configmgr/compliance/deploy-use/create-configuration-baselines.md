---
title: 建立設定基準
titleSuffix: Configuration Manager
description: 在可部署至集合的 Configuration Manager 中建立設定基準。
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-compliance
ms.topic: conceptual
ms.assetid: 678c9622-c61b-47d1-ba25-690616e431c7
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: 2028974c166e060f445b255db6c5af707725a3f4
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81693286"
---
# <a name="create-configuration-baselines-in-configuration-manager"></a>在 Configuration Manager 中建立設定基準

適用於：  Configuration Manager (最新分支)


Configuration Manager 中的設定基準包含預先定義的設定項目和 (選擇性) 其他設定基準。 建立組態基準之後，您可以將它部署至集合，讓該集合中的裝置下載組態基準，並以此評估合規性。  

## <a name="configuration-baselines"></a>設定基準

 Configuration Manager 中的設定基準可以包含特定的設定項目修訂，或者可以設定為一律使用最新版的設定項目。 如需設定項目修訂的詳細資訊，請參閱[設定資料的管理工作](../../compliance/deploy-use/management-tasks-for-configuration-data.md)。  

 有兩種方法可以用來建立設定基準：  

- 從檔案匯入組態資料。 若要啟動 [匯入組態資料精靈]  ，請在 [資產與相容性]  工作區的 [設定項目]  或 [組態基準]  節點中，按一下 [匯入組態資料]  。 如需詳細資訊，請參閱[匯入設定資料](import-configuration-data.md)。

- 使用 [建立組態基準]  對話方塊建立新的組態基準。  

## <a name="create-a-configuration-baseline"></a>建立組態基準

若要使用 [建立設定基準]  對話方塊來建立設定基準，請使用下列程序：  

1. 在 Configuration Manager 主控台中，按一下 [資產與相容性]   > [相容性設定]   > [設定基準]  。  

2. 在 [常用]  索引標籤上，按一下 [建立]  群組中的 [建立組態基準]  。  

3. 在 [建立組態基準]  對話方塊中，輸入組態基準的唯一名稱和描述。 名稱最多可以使用 255 個字元，描述最多可以使用 512 個字元。  

4. [組態資料]  清單會顯示隨附於這個組態基準的所有組態項目或組態基準。 按一下 [新增]  將新的組態項目或組態基準加入清單中。 您可以從下列項目中選擇：  

   - <bpt id="p1">**</bpt>Configuration Items<ept id="p1">**</ept>  

   - **軟體更新**  

   - <bpt id="p1">**</bpt>Configuration Baselines<ept id="p1">**</ept>  
     > [!IMPORTANT]
     > 您必須將每個設定基準限制成不超過 1000 個軟體更新。
5. 使用 [變更目的]  清單來指定您在 [設定資料]  清單中選取的設定項目行為。 您可以從下列項目中選取：  

   -   **必要**：如果用戶端裝置上偵測不到設定項目，則設定基準會評估為不符合規範。 如果偵測到，就會評估相容性  

   -   **選擇性**：如果用戶端電腦上找到它所參考的應用程式，則設定項目只會評估合規性。 如果找不到應用程式，設定基準不會標示為不相容 (僅適用於應用程式設定項目)。  

   -   **禁止**：如果用戶端電腦上偵測到設定項目，則設定基準會評估為不符合規範 (僅適用於應用程式設定項目)。  

   > [!NOTE]
   >  只有當您在 [建立設定項目精靈]  的 [一般]  頁面上按一下 [此設定項目包含應用程式設定]  選項時，才能使用 [變更目的]  清單。  

6. 使用 [變更修訂]  清單來選取特定或最新的組態項目修訂，評估用戶端裝置的相容性，或選取 [永遠使用最新版本]  一律使用最新的修訂。 如需設定項目修訂的詳細資訊，請參閱[設定資料的管理工作](../../compliance/deploy-use/management-tasks-for-configuration-data.md)。  

7. 若要從設定基準移除設定項目，請選取設定項目，然後按一下 [移除]  。  

8. 從 1806 版開始，選擇您是否想要 [一律為共同管理的用戶端套用此基準]  。 核取後，此基準會套到甚至是 Intune 所管理的用戶端上。  這個例外狀況可能會用來配置您的組織會用到，但 Intune 目前還沒有的設定。

9. (選擇性) 按一 下 [類別]  ，將類別指派給用於搜尋和篩選的基準。 

10. 按一下 [確定]  關閉 [建立組態基準]  對話方塊並建立組態基準。  

>[!NOTE]
> 修改現有的基準 (例如，[一律為共同管理的用戶端套用此基準]  設定) 會遞增基準內容的版本。 用戶端必須評估新的版本，以更新基準報告。

## <a name="include-custom-configuration-baselines-as-part-of-compliance-policy-assessment"></a><a name="bkmk_CAbaselines"></a> 在合規性政策評定中納入自訂設定基準
<!--3608345-->
(於 1910 版推出) 

從 1910 版開始，您可以將自訂設定基準的評估新增為合規性政策評定規則。 當您建立或編輯設定基準時，您可以選擇 [在合規性政策評定期間評估此基準]  。 當新增或編輯合規性政策規則時，您會有一個稱為 [在合規性政策評定中納入已設定的基準]  的條件。 針對共同管理的裝置，以及當設定 Intune 以將 Configuration Manager 合規性評估結果作為整體合規性狀態的一部分時，此資訊將會傳送至 Azure AD。 您接著即可將其用於 Office 365 資源的條件式存取。 如需詳細資訊，請參閱[搭配共同管理的條件式存取](../../comanage/quickstart-conditional-access.md)。

若要在合規性政策評定中納入自訂設定基準，請執行下列動作：

- 建立相容性原則，並將其部署至使用者集合，其規則為 [在相容性原則評定中包含已設定的基準  ](#bkmk_CA)。
- 在部署到裝置集合的設定基準中選取 [將此基準評估為相容性原則評定的一部分  ](#bkmk_eval-baseline)。

> [!IMPORTANT]
> 以共同管理的裝置為目標時，請確定您符合[共同管理的必要條件](../../comanage/overview.md#prerequisites)。

### <a name="example-evaluation-scenario"></a>範例評估案例

當使用者屬於以包括規則條件 [在合規性政策評定中納入已設定的基準]  之合規性政策為目標的集合時，任何在 [在合規性政策評定期間評估此基準]  選項已選取的情況下部署到使用者或使用者裝置的基準都會被評估是否符合合規性。 例如：

- `User1` 屬於 `User Collection 1`。
- `User1` 使用 `Device1`，它位於 `Device Collection 1` 與 `Device Collection 2`。
- `Compliance Policy 1` 具有 [在合規性政策評定中納入已設定的基準]  規則條件，且已部署到 `User Collection 1`。
- `Configuration Baseline 1` 已選取 [在合規性政策評定期間評估此基準]  且已部署到 `Device Collection 1`。
- `Configuration Baseline 2` 已選取 [在合規性政策評定期間評估此基準]  且已部署到 `Device Collection 2`。

在此案例中，當 `Compliance Policy 1` 使用 `Device1` 針對 `User1` 評估時，也會評估 `Configuration Baseline 1` 與 `Configuration Baseline 2`。

- `User1` 有時候使用 `Device2`。
- `Device2` 是 `Device Collection 2` 與 `Device Collection 3` 的成員。
- `Device Collection 3` 中已部署 `Configuration Baseline 3`，但 [在合規性政策評定期間評估此基準]  未選取。

當 `User1` 使用 `Device2` 時，只有當 `Compliance Policy 1` 評估時才會評估 `Configuration Baseline 2`。

> [!NOTE]
><!--5582516-->
> 若合規性政策評估先前從未在用戶端上評估的新基準，它可能會回報不符合規範。 若評估合規性時，基準評估仍在執行，就會發生此情況。 若要因應此問題，請按一下 [軟體中心]  中的 [檢查合規性]  。

### <a name="create-and-deploy-a-compliance-policy-with-a-rule-for-baseline-compliance-policy-assessment"></a><a name="bkmk_CA"></a> 建立及部署具有基準合規性政策評定規則的合規性政策

1. 在 [資產與合規性]  工作區中，展開 [合規性設定]  ，然後選取 [合規性政策]  節點。
1. 按一下功能區中的 [建立合規性政策]  以顯示 [建立合規性政策精靈]  。 
1. 在 [一般]  頁面上，選取 [使用 Configuration Manager 用戶端管理之裝置的合規性規則]  。
   - 裝置必須由 Configuration Manager 用戶端管理以在合規性政策評定期間納入自訂設定基準。
1. 在 [支援的平台]  頁面上選取您的平台。
1. 在 [規則]  頁面上，選取 [名稱]  ，然後選取 [在合規性政策評定中納入已設定的基準]  條件。

   ![在合規性政策評定中納入已設定的基準條件](./media/3608345-create-compliance-policy-rule.png)

1. 按一下 [確定]  ，然後按一下 [下一步]  以移至 [摘要]  頁面。
1. 確認您的選取，然後按一下 [確定]  ，再按一下 [關閉]  。
1. 在 [合規性政策]  節點中，以滑鼠右鍵按一您建立的政策，然後選取 [部署]  。
1. 選擇警示的集合、警示產生設定，以及您的合規性評估排程。
1. 按一下 [確定]  以部署合規性政策。

### <a name="select-a-configuration-baseline-and-check-evaluate-this-baseline-as-part-of-compliance-policy-assessment"></a><a name="bkmk_eval-baseline"></a> 選取設定基準並核取 [在合規性原則評定中評估此基準]

1. 在 [資產與合規性]  工作區中，展開 [合規性設定]  ，然後選取 [設定基準]  節點。
1. 以滑鼠右鍵按一下已部署到裝置集合的現有基準，然後選取 [屬性]  。 如有需要，您可以建立新的基準。
   - 基準必須部署到裝置集合，而非使用者集合。
1. 啟用 [在合規性政策評定期間評估此基準]  設定。
   - 針對以 Intune 作為 [裝置設定]  授權單位的共同管理裝置，請確定也選取了 [即使用是共同管理的用戶端也一律套用此基準]  。
1. 按一下 [確定]  以儲存您對設定基準所做的變更。

   ![[設定基準屬性] 對話方塊](./media/3608345-configuration-baseline-properties.png)

### <a name="log-files-for-custom-configuration-baselines-as-part-of-compliance-policy-assessment"></a>合規性政策評定中的自訂設定基準記錄檔

- ComplianceHandler.log
- SettingsAgent.log
- DCMAgent.log
- CIAgent.log

## <a name="next-steps"></a>後續步驟

[匯入設定資料](import-configuration-data.md)
