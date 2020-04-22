---
title: '適用於設定基準的一般工作 '
titleSuffix: Configuration Manager
description: 了解如何建立與部署 Configuration Manager 設定基準。
ms.date: 07/12/2017
ms.prod: configuration-manager
ms.technology: configmgr-compliance
ms.topic: conceptual
ms.assetid: 4bb6afeb-d267-4f9b-ade2-26e5400c223b
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 52e83639029db9eeb4ef64657e70e3dc11aab8f2
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81692256"
---
# <a name="common-tasks-for-creating-and-deploying-configuration-baselines-with-configuration-manager"></a>以 Configuration Manager 建立及部署設定基準的一般工作

適用於：  Configuration Manager (最新分支)

此主題包含常見的案例，協助您了解如何建立及部署 Configuration Manager 設定基準。  

 如果您已經熟悉合規性設定，則可在[建立設定基準](../../compliance/deploy-use/create-configuration-baselines.md)和[部署設定基準](../../compliance/deploy-use/deploy-configuration-baselines.md)主題中找到所用全部功能的詳細資訊文件。  

 開始之前，請參閱[開始使用相容性設定](../../compliance/get-started/get-started-with-compliance-settings.md)，了解相容性設定的一些基本概念，另請參閱[規劃及設定相容性設定](../../compliance/plan-design/plan-for-and-configure-compliance-settings.md)，實作任何必要條件。  

## <a name="create-a-configuration-baseline"></a>建立組態基準  
 在這個範例中，您只為執行 Configuration Manager 用戶端的 Windows 10 電腦建立了設定項目。  

 這個組態項目會在 Windows 10 電腦上強制執行至少 6 個字元的必要密碼。 組態項目的名稱是 **Windows 10 密碼強化**。  

使用下列程序來學習如何將這個設定項目加入設定基準中以進行部署。  

1. 在 Configuration Manager 主控台中，按一下 [資產與相容性]   > [相容性設定]   > [設定基準]  。  

2. 在 [常用]  索引標籤上，按一下 [建立]  群組中的 [建立組態基準]  。  

3. 在 [建立設定基準]  對話方塊中，設定下列各項設定：  

   -   **名稱** - 輸入 **Windows 10 密碼** (或您選擇的另一個名稱)  

4. 按一下 [新增]   >   。  

5. 在 [新增設定項目]  對話方塊中，選取之前建立的 [Windows 10 密碼強化]  設定項目，然後按一下 [新增]  。  

6. 按一下 [確定]，關閉 [新增設定項目]  對話方塊並返回 [建立設定基準]  對話方塊。

7. 按一下 [確定]  關閉 [建立組態基準]  對話方塊。  

   您現在可以看到 Configuration Manager 主控台 [設定基準]  節點中的設定基準。  

## <a name="deploy-the-configuration-baseline"></a>部署設定基準  
 在這個範例中，您要將在上一個程序中建立的設定基準部署到電腦集合。  

1. 在 Configuration Manager 主控台中，按一下 [資產與相容性]   > [相容性設定]   > [設定基準]  。  

2. 從組態基準清單中，選取 [Windows 10 密碼]  。  

3. 在 [首頁]  索引標籤的 [部署]  群組中，按一下 [部署]  。  

4. 在 [部署設定基準]  對話方塊中，設定下列各項設定：  

   -   **選取的組態基準**：確定 **Windows 10 密碼** 組態基準已自動加入到這份清單中。  

   -   **支援時補救不符合要求的規則**：選取這個方塊，確保當目標裝置沒有正確的設定時，Configuration Manager 會進行補救。  

   -   **集合**：按一下 [瀏覽]  來選擇電腦集合，以評估及補救設定基準的合規性。 在這個範例中，組態基準已部署至內建的 [所有桌面和伺服器用戶端]  集合。  

       > [!TIP]  
       >  如果您選擇的集合中有不執行 Windows 10 的電腦或裝置，請別擔心。 只要您在建立的設定項目中設定了支援的平台，就只會評估 Windows 10 電腦的合規性。  

   -   必要時，請設定評估設定基準的排程。 否則，請保留 **7 天**的預設值。  

5. 按一下 [確定]  關閉 [部署組態基準]  對話方塊並建立部署。  

   如果想要快速瀏覽這項部署的相容性統計資料，請在 [監視]  工作區中按一下 [部署]  。 在畫面底部，您會看到 [合規性統計資料]  圖表。  

## <a name="next-steps"></a>後續步驟 

如需如何監視設定基準的詳細資訊，請參閱[監視合規性設定](../../compliance/deploy-use/monitor-compliance-settings.md)。  
