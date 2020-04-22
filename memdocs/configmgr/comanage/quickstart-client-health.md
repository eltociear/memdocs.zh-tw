---
title: 搭配共同管理的用戶端健康情況
titleSuffix: Configuration Manager
description: 在 Azure 入口網站中從 Intune 維持對 Configuration Manager 用戶端健康情況的可見度
ms.date: 01/14/2019
ms.prod: configuration-manager
ms.technology: configmgr-comanage
ms.topic: conceptual
ms.assetid: 5b243aac-8a1a-4f14-ba3f-5446bb483e92
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 11fbeaf76737a832afca7351e8587e0d9c4bacac
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81690826"
---
# <a name="client-health-with-co-management"></a>搭配共同管理的用戶端健康情況

您網路的健康情況會與在其中進出之裝置的健康情況直接相關。 Intune 可以與狀況不良的用戶端通訊，即使該用戶端不位於您網路上也一樣。 使用共同管理來將此功能與 Configuration Manager 回報 98% 的已知狀況良好用戶端的能力結合在一起。 然後您便可以即時對所有用戶端進行偵測、評量並提供可見度。 Intune 也會新增對所有已連線用戶端進行合規性升級所需的支援。

在下列影片中，資深專案經理 Rob York 與產品行銷經理 Locky Ainley 會討論並示範搭配共同管理的用戶端健康情況：

> [!VIDEO https://channel9.msdn.com/Series/Endpoint-Zone/Client-Health-Monitoring-with-Co-Management/player]



## <a name="benefits"></a>優點

評量用戶端的健康情況是第一要務。 System Center 2012 Configuration Manager 已新增 **CCMeval**。 此公用程式位於 Configuration Manager 用戶端外部。 它能提供用戶端健康情況監視和自動補救。 不過，此報告功能需仰賴裝置實際或以虛擬方式位於您的內部網路上。 共用管理可協助處理此問題。

透過共同管理，Intune 可以針對用戶端健康情況狀態進行報告。 它能針對資料有效性提供時間戳記資訊。 此資訊能告訴您裝置健康情況是否良好、是否能進行連線、是否能安裝應用程式，或是否能更新至所需的 OS 組建。 

如需此功能的詳細概觀，請參閱這部來自 Ignite 2018 [Configuration Manager 的新功能](https://myignite.techcommunity.microsoft.com/sessions/64591) \(英文\) 講習的影片。

> [!VIDEO https://www.youtube.com/embed/UAW2KBUq7DM?start=518]


當 Configuration Manager 提供用戶端已安裝的裝置狀態，但實際上未安裝時，Intune 可以在無須連線至該用戶端的情況下提供詳細資訊。 Intune 中的裝置健康情況資訊是簡單易懂的。 如果狀態不是「良好」  ，它便會提供建議與後續步驟，以對其進行疑難排解及修復。

> [!Note]  
> 預計於未來版本提供下列優點：
> - Configuration Manager 會將額外功能包含到 CCMeval 中  
> - 這能使在 Configuration Manager 和與 Intune 中識別潛在狀況不良電腦的程序更為簡單  
> - 您可以將 Intune 中的用戶端健康情況資料分組  



## <a name="value-proposition"></a>價值主張

透過此功能，您現在可以搭配 Intune 取得外部資料來源。 它能讓您在對各式各樣的用戶端問題進行疑難排解時決定後續步驟。 現在您不需要建立額外的報告，或使用其他工具來取回用戶端資料。

當您有狀況良好的用戶端時，便已更新修補程式合規性。 更好的修補程式合規性，代表您擁有更好的安全性。



## <a name="configure"></a>設定

若要開始使用此功能，請使用下列步驟：

- 將裝置更新至 Windows 10 1709 版或更新版本  

- [啟用共同管理](how-to-enable.md)  
    - 您不需要將任何工作負載切換至 Intune  

- 將 Configuration Manager 站台與用戶端更新至 *1806* 版或更新版本  


### <a name="review-configuration-manager-client-health-in-intune"></a>在 Intune 中檢閱 Configuration Manager 用戶端健康情況

1. 登入 [Azure 入口網站](https://portal.azure.com/)。  

2. 選擇 [所有服務]   > [Intune]  。 Intune 位於 [Monitoring + Management] (監視 + 管理)  區段。  

3. 在您開啟 [Microsoft Intune]  窗格之後，請在 [說明及支援]  底下的功能表中，移至 [疑難排解]  頁面。  

4. 使用 [選取使用者]  選項，在 [裝置]  清單中找出特定裝置，然後選取它以開啟裝置頁面。  

5. 共同管理資訊會顯示在裝置頁面的底部。 此資訊包含下列針對用戶端健康情況的欄位：  
    - **Configuration Manager 代理程式狀態**  
    - **Configuration Manager 代理程式上次簽入時間**  

> [!Tip]  
> 已註冊至 Intune 的裝置每天會連線至雲端服務三次，連線之間有約八小時的間隔。 
