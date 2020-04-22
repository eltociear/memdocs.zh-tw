---
title: 切換共同管理工作負載
titleSuffix: Configuration Manager
description: 了解如何將目前受 Configuration Manager 管理的工作負載切換至 Microsoft intune。
ms.prod: configuration-manager
ms.technology: configmgr-comanage
author: mestew
ms.author: mstewart
manager: dougeby
ms.date: 09/06/2019
ms.topic: conceptual
ms.assetid: 60e2022f-a4f9-40dd-af01-9ecb37b43878
ms.openlocfilehash: 4874d12149f213351740c9e5b300bf04fc536571
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81691056"
---
# <a name="how-to-switch-configuration-manager-workloads-to-intune"></a>如何將 Configuration Manager 工作負載切換至 Intune

共同管理的好處之一是將 Configuration Manager 工作負載切換至 Microsoft Intune。 當 Windows 10 裝置具有 Configuration Manager 用戶端且註個冊至 Intune 時，您可取得這兩服務的優點。 您可以控制要將哪些工作負載 (如果有) 的授權從 Configuration Manager 切換至 Intune。 Configuration Manager 會繼續管理所有其他工作負載 (包括那些沒有切換到 Intune 的工作負載)，以及共同管理不支援的所有其他 Configuration Manager 功能。

如果您將工作負載切換到 Intune，但之後又改變主意，您可以將它切換回 Configuration Manager。

如需所支援工作負載的詳細資訊，請參閱[工作負載](workloads.md)。

## <a name="switch-workloads-starting-in-version-1906"></a>從 1906 版開始切換工作負載
<!--3555750 FKA 1357954 -->
從 1906 版開始，您現在可以為每個共同管理工作負載設定不同的試驗集合。 使用不同的試驗集合，可讓您在轉移工作負載時採取更細微的方法。 您可以在啟用共同管理時切換工作負載，或等您稍後準備好時再切換。 如果您尚未啟用共同管理，請先將它啟用。 如需詳細資訊，請參閱[如何啟用共同管理](how-to-enable.md)。 啟用共同管理之後，請修改共同管理內容中的設定。

1. 在 Configuration Manager 主控台中，移至 [系統管理]  工作區，展開 [雲端服務]  ，然後選取 [共同管理]  節點。  
2. 選取共同管理物件，然後在功能區中選擇 [屬性]  。  
3. 切換到 [工作負載]  索引標籤。根據預設，所有工作負載都設定為 [Configuration Manager]  設定。 若要切換工作負載，請將該工作負載的滑桿控制項移動至所需的設定。  

    ![共同管理內容頁面上 [工作負載] 索引標籤的螢幕擷取畫面](media/3555750-co-management-workloads-tab.png)

    - **Configuration Manager**：Configuration Manager 會繼續管理此工作負載。  

    - **試驗 Intune**：只會為試驗群組中的裝置切換此工作負載。 您可以在共同管理屬性頁面的 [暫存]  索引標籤上變更**試驗集合**。  

    - **Intune**：為註冊到共同管理中的所有 Windows 10 裝置切換此工作負載。  

4. 移至 [暫存]  索引標籤，並視需要變更任何工作負載的**試驗集合**。
  
   ![共同管理內容頁面上 [工作負載] 索引標籤的螢幕擷取畫面](media/3555750-co-management-staging-tab.png)

> [!Important]  
> - 切換任何工作負載之前，請確定您已正確地設定及部署 Intune 中對應的工作負載。 請確保工作負載一律受您裝置的其中一項管理工具所管理。
> - 從 Configuration Manager 1806 版開始，當您切換共同管理工作負載時，共同管理裝置就會從 Microsoft Intune 自動同步 MDM 原則。 當您在 Configuration Manager 主控台中從用戶端通知起始 [下載電腦原則]  動作時，也會進行這項同步處理作業。 如需詳細資訊，請參閱[使用用戶端通知起始用戶端原則擷取](../core/clients/manage/manage-clients.md#BKMK_PolicyRetrieval)。 <!--1357377-->

## <a name="switch-workloads-in-version-1902-and-earlier"></a>1902 版和更早版本中的交換器工作負載

您可以在啟用共同管理時切換工作負載，或等您稍後準備好時再切換。 如果您尚未啟用共同管理，請先將它啟用。 如需詳細資訊，請參閱[如何啟用共同管理](how-to-enable.md)。 啟用共同管理之後，請修改共同管理內容中的設定。

1. 在 Configuration Manager 主控台中，移至 [系統管理]  工作區，展開 [雲端服務]  ，然後選取 [共同管理]  節點。  

2. 選取共同管理物件，然後在功能區中選擇 [屬性]  。
   - 系統會提示您登入 Azure AD。 該提示不會阻止您更新您的上線。 不過，系統會在您每次開啟 [屬性]  頁面時顯示提示，直到您登入為止。

3. 切換到 [工作負載]  索引標籤。根據預設，所有工作負載都設定為 [Configuration Manager]  設定。 若要切換工作負載，請將該工作負載的滑桿控制項移動至所需的設定。  

    ![共同管理內容頁面上 [工作負載] 索引標籤的螢幕擷取畫面](media/properties-workloads.png)

    - **Configuration Manager**：Configuration Manager 會繼續管理此工作負載。  

    - **試驗 Intune**：只會為試驗群組中的裝置切換此工作負載。 您可以在共同管理內容頁面上的 [準備]  索引標籤變更 [試驗集合]  。  

    - **Intune**：為註冊到共同管理中的所有 Windows 10 裝置切換此工作負載。  

4. 在共同管理屬性頁面的 [暫存]  索引標籤上，視需要變更您工作負載的**試驗集合**。

5. 按一下 [確定]  以儲存並結束共同管理屬性。

> [!Important]  
> - 切換任何工作負載之前，請確定您已正確地設定及部署 Intune 中對應的工作負載。 請確保工作負載一律受您裝置的其中一項管理工具所管理。 
> - 從 Configuration Manager 1806 版開始，當您切換共同管理工作負載時，共同管理裝置就會從 Microsoft Intune 自動同步 MDM 原則。 當您在 Configuration Manager 主控台中從用戶端通知起始 [下載電腦原則]  動作時，也會進行這項同步處理作業。 如需詳細資訊，請參閱[使用用戶端通知起始用戶端原則擷取](../core/clients/manage/manage-clients.md#BKMK_PolicyRetrieval)。 <!--1357377-->

## <a name="next-steps"></a>後續步驟

[監視共同管理](how-to-monitor.md)
