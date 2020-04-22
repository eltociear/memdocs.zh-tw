---
author: mestew
ms.author: mstewart
ms.prod: configuration-manager
ms.technology: configmgr-comanage
ms.topic: include
ms.date: 03/12/2020
ms.openlocfilehash: 37376d137409b06816d4c5dff5a0909f57531443
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81690406"
---
<!--3555750 FKA 1357954 --Don't apply H2/H3 in this include file since they are context driven by article-->
1. 在 Configuration Manager 主控台中，移至 [系統管理]  工作區，展開 [雲端服務]  ，然後選取 [共同管理]  節點。 按一下功能區的 [設定共同管理]  以開啟 [共同管理設定精靈]  。

2. 在精靈的 [訂用帳戶]  頁面上，設定下列設定：

    - 要使用的 **Azure 環境**。 例如，Azure 公用雲端或 Azure 美國政府雲端。<!--4075452-->  

    - 選取 [登入]  。 以 Azure 全域系統管理員身分登入，然後選取 [下一步]  。  

        > [!TIP]
        > 您將針對此精靈的目的登入一次。 這些認證不會在其他位置儲存或重複使用。

3. 在 [啟用]  頁面上，選擇下列設定：

   - **自動註冊到 Intune**：為現有的 Configuration Manager 用戶端在 Intune 中啟用自動用戶端註冊。 此選項可讓您在用戶端子集上啟用共同管理，初步測試共同管理，並推出使用分段方法的共同管理。 如果使用者將裝置取消註冊，則該裝置會在下一次評估原則時重新註冊。 <!--3330596-->

      - **試驗**：只有為 **Intune 自動註冊**集合成員的 Configuration Manager 用戶端會在 Intune 中自動註冊。
      - **全部**：針對所有 Windows 10 1709 版或更新版本用戶端啟用自動註冊。

   - **Intune 自動註冊**：此集合應包含所有要上架到共同管理的用戶端。 其就本質上而言，是其他暫存集合的超集。

   ![指定 Intune 自動註冊集合 ](../media/3555750-co-management-onboarding-enablement.png)

      > [!Note]  
      > 從 1806 版開始，不是所有的用戶端都會自動註冊。 這個行為有助於大型環境的大規模註冊。 Configuration Manager 根據用戶端數目隨機化註冊。 例如，如果您的環境有 100,000 個用戶端，則當您啟用此設定時，註冊會在數天之間進行。<!--1358003-->  
      >
      > 從 1906 版開始：
      >
      > - 新的共同管理裝置現在會根據其 Azure Active Directory (Azure AD)「裝置」  權杖自動註冊到 Microsoft Intune 服務。 不需要等待使用者登入裝置以啟動自動註冊。 此變更有助於減少註冊狀態為「擱置使用者登入」  的裝置數目。<!-- 4454491 --> 若要支援此行為，裝置需要執行 Windows 10 1803 版或更新版本。 如需詳細資訊，請參閱[共同管理註冊狀態](../how-to-monitor.md#co-management-enrollment-status)。
      >
      > - 如果您已將裝置註冊到共同管理，新的裝置現在會在符合[必要條件](../overview.md#prerequisites)之後立即註冊。<!--4321130-->

4. 針對已在 Intune 中註冊的網際網路型裝置，請複製 [啟用]  頁面上的命令列並加以儲存。 您可以使用此命令列，將 Configuration Manager 用戶端安裝為 Intune 中的應用程式，以供網際網路型裝置使用。 如果您現在不儲存此命令列，則可隨時檢閱共同管理設定來取得此命令列。

5. 在 [工作負載]  頁面上，針對每個工作負載選擇要移動以使用 Intune 進行管理的裝置群組。 如需詳細資訊，請參閱[工作負載](../workloads.md)。 如果您只想要啟用共同管理，則不需要現在切換工作負載。 您可以稍後再切換工作負載。 如需詳細資訊，請參閱[如何切換工作負載](../how-to-switch-workloads.md)。  

    - **試驗 Intune**：只會針對您將在 [暫存]  頁面上設定之試驗集合中的裝置，切換相關聯的工作負載。 每個工作負載都可以有不同的試驗集合。
    - **Intune** - 會針對所有共同管理的 Windows 10 裝置切換相關工作負載。  

    > [!Important]
    > 切換任何工作負載之前，請確定您已正確地設定及部署 Intune 中對應的工作負載。 請確保工作負載一律受您裝置的其中一項管理工具所管理。  

6. 在 [暫存]  頁面上，針對每個設為 [試驗 Intune]  的工作負載指定試驗集合。

   ![指定 Intune 自動註冊集合 ](../media/3555750-co-management-onboarding-staging.png)

7. 若要啟用共同管理，請完成精靈。
