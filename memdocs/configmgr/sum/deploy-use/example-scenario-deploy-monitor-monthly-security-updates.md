---
title: 部署及監視更新的範例案例
titleSuffix: Configuration Manager
description: 如何在 Configuration Manager 中使用軟體更新來部署和監視每月軟體更新。
ms.date: 10/21/2019
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: c32f757a-02da-43f2-b055-5cfd097d8c43
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: ea654c4ec13b95b78a65c85d9d36ce576619854e
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81696126"
---
# <a name="example-scenario-to-deploy-and-monitor-monthly-software-updates"></a>部署及監視每月安全性更新的範例案例

適用於：  Configuration Manager (最新分支)

此主題提供的示範案例說明如何在 Configuration Manager 中使用軟體更新部署及監視 Microsoft 每月發行的安全性軟體更新。  

 在此案例中，我們遵循 Woodgrove Bank Configuration Manager 系統管理員的動作。 系統管理員必須依照下列條件與需求建立軟體更新部署策略：  

- 每月第二個星期二 Mircrosoft 發行安全性軟體更新，一個星期後進行作用中軟體更新部署。 此事件通常稱為 Patch Tuesday (周二修補日)。  

- 發佈點會下載並設置軟體更新， 接著 ConfigMgr 系統管理員會在用戶端子集中測試部署，之後才在生產環境中完全部署軟體更新。  

- 系統管理員必須能夠逐月或逐年監視軟體更新的合規性。  

  此案例假設軟體更新點的基礎結構已實作完成。 請運用下列資訊規劃及設定 Configuration Manager中的軟體更新。  

|程序|參考|  
|-------------|---------------|  
|檢閱軟體更新的重要概念。|[軟體更新簡介](../understand/software-updates-introduction.md)|  
|規劃軟體更新。 這項資訊協助您規劃容量考量、判斷軟體更新點基礎結構、軟體更新點安裝作業、同步處理設定，以及軟體更新的用戶端設定。|[規劃軟體更新](../plan-design/plan-for-software-updates.md)|  
|設定軟體更新。 這項資訊協助您在階層中安裝及設定軟體更新點，並且有助於設定及同步處理軟體更新。<br /><br /> 在此案例中，ConfigMgr 系統管理員會設定在每個月的第二個星期三同步處理軟體更新，確保能接收 Microsoft 提供的最新安全性軟體更新。|[同步處理軟體更新](../get-started/synchronize-software-updates.md)|  

 本主題中的下列案例提供一些範例步驟，協助您部署及監視組織中的 Configuration Manager 安全性軟體更新。

##  <a name="step-1-create-a-software-update-group-for-yearly-compliance"></a><a name="BKMK_Step1"></a> 步驟 1：建立年度合規性軟體更新群組  
 Configuration Manager 系統管理員會建立一個軟體更新群組，用於監視 2016 年所發行所有安全性軟體更新的合規性。 系統管理員會執行下表中的步驟。  

|程序|參考|  
|-------------|---------------|  
|Configuration Manager 系統管理員會從 Configuration Manager 主控台中的 [所有軟體更新]  節點新增準則，只顯示在 2015 年發行或修改且符合下列準則的安全性軟體更新：<br /><br /><ul><li>**準則**：發行或修改日期</li><li>**條件**：晚於或等於特定日期<br />**值**：1/1/2015</li><li>**準則**：更新分類<br />**值**：安全性更新</li><li>**準則**：已過期 <br />**值**：否</li></ul>|沒有其他資訊|
|ConfigMgr 系統管理員會篩選出來的軟體更新全數新增到新的軟體更新群組，需求如下：<br /><br /><ul><li>**名稱**：合規性群組 - Microsoft 安全性更新 2015</li><li>**描述**：軟體更新|[將軟體更新新增至更新群組](add-software-updates-to-an-update-group.md)|  

##  <a name="step-2-create-an-automatic-deployment-rule-for-the-current-month"></a><a name="BKMK_Step2"></a> 步驟 2：建立當月自動部署規則  
 Configuration Manager 系統管理員會針對 Microsoft 當月發行的安全性軟體更新建立自動部署規則。 系統管理員會執行下表中的步驟。  

|程序|參考|  
|-------------|---------------|  
|ConfigMgr 系統管理員會建立符合下列需求的自動部署規則：<br /><br /><ol><li>在 [一般]  索引標籤中，Configuration Manager 系統管理員會進行下列設定：<br /> <ul><li>指定名稱為 **Monthly Security Updates**。</li><li>選取含有限用戶端的測試集合。</li><li>選取 [建立新的軟體更新群組]  。</li><li>確認未選取 [在執行此規則後啟用部署]  。</li></ul></li><li>在 [部署設定]  索引標籤中，Configuration Manager 系統管理員會選取預設設定。</li><li>在 [軟體更新]  頁面中，ConfigMgr 系統管理員會擷取下列內容篩選器和搜尋準則：<br /><ul><li>發行或修改日期是 [過去 1 個月]  。</li><li>更新分類是 [安全性更新]  。</li></ul></li><li>在 [評估]  頁面中，ConfigMgr 系統管理員會啟用根據每**月** **第二個星期四**的排程執行規則。  此外，ConfigMgr 系統管理員也會確認同步處理排程設為在每**月**的**第二個星期三**執行。</li><li>ConfigMgr 系統管理員會使用 [部署排程]、[使用者經驗]、[警示] 及 [下載設定] 頁面中的預設設定。</li><li>在 [部署套件]  頁面中，Configuration Manager 系統管理員會指定新的部署套件。</li><li>ConfigMgr 系統管理員會在 [下載位置] 與 [語言選擇] 頁面中使用預設設定。</li></ol>|[自動部署軟體更新](automatically-deploy-software-updates.md)|  

##  <a name="step-3-verify-that-software-updates-are-ready-to-deploy"></a><a name="BKMK_Step3"></a> 步驟 3：確認是否準妥部署軟體更新  
 在每個月的第二個星期二，ConfigMgr 系統管理員會確認是否已準備好部署軟體更新。 系統管理員會執行下列步驟。  

|程序|參考|  
|-------------|---------------|  
|ConfigMgr 系統管理員會確認軟體更新同步處理是否已順利完成。|[軟體更新同步處理狀態](monitor-software-updates.md#BKMK_SUSyncStatus)|  

##  <a name="step-4-deploy-the-software-update-group"></a><a name="BKMK_Step4"></a> 步驟 4：部署軟體更新群組  
 在 Configuration Manager 系統管理員確認已準備好部署軟體更新之後，他們會部署軟體更新。 系統管理員會執行下表中的步驟。  

|程序|參考|  
|-------------|---------------|  
|ConfigMgr 系統管理員會針對新的軟體更新群組建立兩個測試部署。 系統管理員會考量每個部署的下列環境：<br /><br /> **工作站測試部署**：ConfigMgr 系統管理員會考量工作站測試部署的下列事項：<br /><br /><ul><li>指定一個部署集合，其中包含用於驗證部署的工作站用戶端子集。</li><li>根據環境中的工作站用戶端設定適合的部署設定。</li></ul><br />**伺服器測試部署**：ConfigMgr 系統管理員會考量伺服器測試部署的下列事項：<br /><br /><ul><li>指定一個部署集合，其中包含用於驗證部署的伺服器用戶端子集。</li><li>根據環境中的伺服器用戶端設定適合的部署設定。</li></ul>|[部署軟體更新](deploy-software-updates.md)|  
|ConfigMgr 系統管理員會確認測試部署是否順利完成。|[軟體更新部署狀態](monitor-software-updates.md#BKMK_SUDeployStatus)|  
|ConfigMgr 系統管理員會將兩個部署更新為包含生產工作站和伺服器的新集合。|沒有其他資訊|  

##  <a name="step-5-monitor-compliance-for-deployed-software-updates"></a><a name="BKMK_Step5"></a> 步驟 5：監視所部署之軟體更新的合規性  
 Configuration Manager 系統管理員會監視軟體更新部署的合規性。 系統管理員會執行下表中的步驟。  

|程序|參考|  
|-------------|---------------|  
|ConfigMgr 系統管理員會在 Configuration Manager 主控台中監視軟體更新部署狀態，並且檢查主控台提供的軟體更新部署報告。|[監視軟體更新](../../sum/deploy-use/monitor-software-updates.md)|  

##  <a name="step-6-add-monthly-software-updates-to-the-yearly-update-group"></a><a name="BKMK_Step6"></a> 步驟 6：在年度更新群組中新增每月軟體更新  
 ConfigMgr 系統管理員會在年度軟體更新群組中新增每月軟體更新群組的軟體更新。 系統管理員會執行下表中的步驟。  

|程序|參考|  
|-------------|---------------|  
|ConfigMgr 系統管理員會從每月軟體更新群組中選取軟體更新，然後新增軟體更新到建立的年度合規性軟體更新群組中。 系統管理員會追蹤軟體更新合規性，並建立各種管理報告。|[將軟體更新新增至已部署的更新群組](add-software-updates-to-an-update-group.md)|  

ConfigMgr 系統管理員已順利完成每月的安全性軟體更新部署。 ConfigMgr 系統管理員會繼續監視並報告軟體更新合規性，確保環境中的用戶端皆符合可接受的合規性等級。  

##  <a name="recurring-monthly-process-to-deploy-software-updates"></a><a name="BKMK_MonthlyProcess"></a> 每月部署軟體更新定期程序  
 ConfigMgr 系統管理員部署軟體更新的第一個月過後，系統管理員會執行步驟三到步驟六，以部署 Microsoft 發行的每月安全性軟體更新。  
