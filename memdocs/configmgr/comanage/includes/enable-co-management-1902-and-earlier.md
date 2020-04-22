---
author: mestew
ms.author: mstewart
ms.prod: configuration-manager
ms.technology: configmgr-comanage
ms.topic: include
ms.date: 08/23/2019
ms.openlocfilehash: d8eaaa403bd1dd97214b4eff82be79d5c2a6566e
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81690396"
---
<!--Don't apply H2/H3 in this include file since they are context driven by article-->
1. 在 Configuration Manager 主控台中，移至 [系統管理]  工作區，展開 [雲端服務]  ，然後選取 [共同管理]  節點。 按一下功能區的 [設定共同管理]  以開啟 [共同管理設定精靈]  。

2. 在精靈的 [訂閱]  頁面上，選取 [登入]  。 登入您的 Intune 租用戶，然後選取 [下一步]  。  

3. 在 [啟用]  頁面上，選擇您的 [自動註冊到 Intune]  設定 ([試驗]  或 [全部]  )。 如果使用者將裝置取消註冊，則該裝置會在下一次評估原則時重新註冊。 <!--3330596--> 

    此動作可為現有 Configuration Manager 用戶端在 Intune 中啟用自動用戶端註冊。 當您選擇 [試驗]  時，只有為試驗集合成員的 Configuration Manager 用戶端會在 Intune 中自動註冊。 此選項可讓您在用戶端子集上啟用共同管理，初步測試共同管理，並推出使用分段方法的共同管理。 

    > [!Note]  
    > 從 1806 版開始，不是所有的用戶端都會自動註冊。 這個行為有助於大型環境的大規模註冊。 Configuration Manager 根據用戶端數目隨機化註冊。 例如，如果您的環境有 100,000 個用戶端，則當您啟用此設定時，註冊會在數天之間進行。<!--1358003-->  

4. 針對已在 Intune 中註冊的網際網路型裝置，請複製 [啟用]  頁面上的命令列並加以儲存。 您可以使用此命令列將 Configuration Manager 用戶端作為 Intune 中的應用程式來安裝。 如果您現在不儲存此命令列，則可隨時檢閱共同管理設定來取得此命令列。

5. 在 [工作負載]  頁面上，針對每個工作負載選擇要移動以使用 Intune 進行管理的裝置群組。 如需詳細資訊，請參閱[工作負載](../workloads.md)。  

    如果您只想要啟用共同管理，則不需要現在切換工作負載。 您可以稍後再切換工作負載。 如需詳細資訊，請參閱[如何切換工作負載](../how-to-switch-workloads.md)。  

    **試驗 Intune** 設定只會切換試驗集合裝置的相關工作負載。 **Intune** 設定會切換所有共同管理的 Windows 10 裝置的相關工作負載。  

    > [!Important]
    > 切換任何工作負載之前，請確定您已正確地設定及部署 Intune 中對應的工作負載。 請確保工作負載一律受您裝置的其中一項管理工具所管理。  

6. 在 [預備]  頁面上，設定下列設定：  

    - **試驗**：試驗群組包含一或多個您選取的集合。 使用此群組作為共同管理分段推出的一部分。 從小型的測試集合開始，當向更多使用者與裝置推出共同管理時，再新增更多的集合到試驗群組。 您可以隨時變更試驗群組中的集合。  

    - **生產**：設定具有一或多個集合的**排除群組**。 凡是此群組中任何集合成員的裝置，都會從使用共同管理中排除。  

7. 若要啟用共同管理，請完成精靈。  
