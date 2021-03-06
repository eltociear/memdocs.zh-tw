---
title: 引導式案例概觀
titleSuffix: Microsoft Intune
description: 了解 Microsoft 365 裝置管理入口網站中所提供的 Intune 引導式案例。
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 01/09/2020
ms.topic: overview
ms.service: microsoft-intune
ms.localizationpriority: high
ms.technology: ''
ms.reviewer: dagerrit
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 1ad9d641bc59b9fee99abce4d05b3871eb90e189
ms.sourcegitcommit: 302556d3b03f1a4eb9a5a9ce6138b8119d901575
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/27/2020
ms.locfileid: "83984835"
---
# <a name="intune-guided-scenarios-overview"></a>Intune 引導式案例概觀 

引導式案例是以單一端對端使用案例為中心的一系列自訂步驟。 常見案例會以組織中系統管理員、使用者或裝置所扮演的角色為基礎。 這些角色通常需要一組仔細協調的設定檔、設定、應用程式和安全性控制項，以提供最佳的使用者體驗和安全性。    

如果您尚不熟悉實作特定 Intune 案例所需的所有步驟和資源，便可以使用引導式案例作為起點。 引導式案例將會自動組合原則、應用程式、指派及其他管理設定。 此外，引導式案例可能會刻意省略針對指定案例不適用或不常見的特定選項。 

引導式案例並非與 Intune 一般工作流程不同的管理空間。 這些工作流程是設計來與 Intune 現有的設定檔、應用程式及原則工作流程搭配使用。 在完成引導式案例之後，於未來對該案例進行的所有管理，都必須在適用於原則、應用程式及設定檔的現有功能表中進行。 引導式案例不會儲存「引導式案例」資源類型，或追蹤未來對資源進行的變更。 由引導式案例所建立的每個資源，都會出現在其相對應的工作負載中。 所有選項 (即便是那些在引導式案例中省略的選項) 都可在現有的功能表中進行編輯。  

## <a name="types-of-guided-scenarios"></a>引導式案例的類型 

基於簡化目的，所有引導式案例都會省略複雜的範圍設定功能，例如範圍標籤、排除群組，以及虛擬群組指派。 由引導式案例所建立的所有資源，都會繼承完成該案例之系統管理員的每個範圍標籤。 特定案例會針對一般設定提供某種程度的自訂，以涵蓋密切相關的案例。 這些案例只會針對包含群組支援群組指派。 針對其他引導式案例，整個案例都會透過不提供任何自訂並自動產生新的群組以接收所有指派，來保證單一的一致性體驗。 在引導式案例完成之後，您便可以自行透過現有的原則、應用程式及設定檔工作負載來使用更複雜的指派。  

下列為引導式的案例： 
- 部署適用於行動裝置的 Microsoft Edge 
- 嘗試由雲端管理的電腦
- 保護 Microsoft Office for Mobile 

## <a name="guided-scenario-functionality"></a>引導式案例功能 

引導式案例能提供特定的功能。 下列詳細資料能協助說明您在遵循引導式案例時可以及不能執行的動作。

### <a name="launching"></a>啟動  

您可以在 **[裝置管理入口網站](https://endpoint.microsoft.com)**  > [疑難排解 + 支援]   > [引導式案例]  中找到所有引導式案例。 

引導式案例會以說明該案例用途的簡介，以及完成設定所需的任何必要條件作為開始。 此時，系統會檢查您的系統管理員權限，以確認您具備完成該案例所需的所有必要權限。  

在所有必要條件檢查都通過之後，該案例會提供適當的自訂設定。 引導式案例的目的是要讓使用者只需輸入最少數量的設定，並隱藏不常用或進階的設定，直到需要它們或是發生特殊情況為止。 每個引導式案例都會連結至能提供其他詳細資料的文件。 

在輸入所有強制設定之後，引導式案例會顯示所輸入的設定，以及該案例所需之資源的摘要。 此時系統並不會儲存任何內容 (除非明確註明)。

下一步是部署該案例。 部署案例會建立並儲存所有必要的資源和選取的設定。 完成部署所需的時間會依案例而有所不同。 在部署完成之後，引導式案例會顯示所建立資源的清單，其中包含每個資源之管理檢視的連結、該資源的一般工作負載，以及相關文件。 

> [!IMPORTANT]
> 系統並不會儲存在引導式案例結尾所顯示的清單，且該清單只可以在開啟該引導式案例時檢視。  
如果在部署案例時發生錯誤，系統會還原所有變更。 

### <a name="editing"></a>編輯 

引導式案例無法用來編輯現有資源。 建立之後，所有的資源、群組及指派都必須使用現有工作負載來編輯。

### <a name="monitoring"></a>監視 

除了初始建立程序之外，引導式案例無法用來監視現有資源。 建立之後，所有的資源、群組及指派都必須使用現有工作負載來監視。 

### <a name="retiring"></a>淘汰 

除了在初始部署期間發生錯誤時所執行的自動清理之外，引導式案例無法用來淘汰現有資源。 建立之後，所有的資源、群組及指派都必須使用現有工作負載來淘汰。 

### <a name="updating"></a>更新

隨著技術的演進，Intune 可能會不時更新引導式案例，以改善使用者體驗、安全性或是案例的其他層面。 此更新只會影響引導式案例所進行的新部署。 Intune 不會更新引導式案例先前所產生的現有資源，來使它們符合新的最佳作法或建議。  

## <a name="next-steps"></a>後續步驟

若要快速在 Microsoft Intune 上開始執行，請逐步執行 Intune 引導式案例。 如果您不熟悉 Intune，請遵循[免費試用快速入門](free-trial-sign-up.md)來設定您的 Intune 租用戶。
