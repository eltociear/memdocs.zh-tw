---
title: 搭配共同管理的 Windows Autopilot
titleSuffix: Configuration Manager
description: 使用 Windows Autopilot 搭配 Configuration Manager 中的共同管理來簡化新 Windows 10 裝置的設定。
ms.date: 02/21/2019
ms.prod: configuration-manager
ms.technology: configmgr-comanage
ms.topic: conceptual
ms.assetid: e3e3c97f-5945-49ab-a622-9f6fe6b9737e
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: b97f9bb6be00129e0b88dc3943af1de166a801d4
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81690946"
---
# <a name="windows-autopilot-with-co-management"></a>搭配共同管理的 Windows Autopilot

收到新的 Windows 10 裝置很令人興奮。 但是，設定所有設定和應用程式以便提高工作效率可能需要一段時間。 共同管理透過 Windows Autopilot 解決了此裝置佈建問題。

在下列情況下，Autopilot 為您和您的使用者提供簡化的體驗：
- 設定及預先設定新的 Windows 10 裝置  
- 重設、回收及復原現有的裝置  

Autopilot 減少了與部署、管理及淘汰裝置相關的時間、資源與複雜度。 同時，您的使用者體驗也得到了簡化，並且在第一次開機時也很容易。

Windows Autopilot 支援多種案例，所有案例都透過共同管理實現最大化：

- 使用者可以將自己的新裝置部署推動到混合式 Azure AD Join 的 Active Directory 或 Azure Active Directory (Azure AD) 中  

- 您可以為 Azure AD 中的共用裝置和 Kiosk 設定自我部署新裝置部署  

- 利用適用於現有裝置的 Windows Autopilot，使用 Configuration Manager 將現有裝置從 Windows 7 與 Active Directory 移轉至 Windows 10 與 Azure AD  

在下列影片中，資深方案經理 Danny Guillory 與首席方案經理 Andrew McMurray 正在討論並示範使用共同管理的 Windows Autopilot：

> [!VIDEO https://channel9.msdn.com/Series/Endpoint-Zone/Using-Windows-Autopilot-with-Co-Management/player]



## <a name="benefits"></a>優點

當您同時使用共同管理和 Autopilot 時，您可以確保進入網路的新裝置最終會在相同的管理狀態。 在此設定中，裝置會在 Intune 中註冊並具有 Configuration Manager 用戶端。  它允許您使用新的 Windows 10 佈建模型，並協助您消除建立、維護及更新自訂 OS 映像的需求。 

在所有這些案例中，您可以自動[啟用 Intune 的共同管理](how-to-prepare-Win10.md)。 這個自動化有助於佈建程序，並可持續管理裝置。

使用 Autopilot，您不需要擔心映像和驅動程式。 透過共同管理使用 Intune 和 Configuration Manager，以此自動化程序專注於佈建裝置。


以下是一起使用共同管理和 Autopilot 可以協助您的方式：

#### <a name="reduce-time-costs-and-complexity"></a>減少時間、成本與複雜度
Windows Autopilot 使用已預先安裝在裝置上的 Windows 10 OEM 最佳化版本。 此設定為組織節省了必須為所使用的每種裝置型號維護自訂映像與驅動程式的工作。 將現有的 Windows 10 安裝轉換為「商務就緒」狀態，而不是裝置重新安裝映像。 它會套用設定與原則、安裝應用程式，以及變更 Windows 10 的版本。 例如，從 Windows 10 專業版升級到 Windows 10 企業版，以便您可以支援進階功能。

#### <a name="improve-the-user-experience"></a>改善使用者體驗
最佳使用者體驗可減少中斷情況，並可幫助他們重新專注於他們的工作。 Windows Autopilot 提供了一種簡單的方法，讓使用者只需簡單按幾下並提供其 Azure AD 認證，即可協助他們快速設定。 對於許多擁有大量遠端員工的組織來說，請使用 Windows Autopilot 直接從製造商提供新的裝置。

#### <a name="use-autopilot-and-configuration-manager-to-migrate-existing-windows-7-devices-to-windows-10"></a>使用 Autopilot 與 Configuration Manager 將現有的 Windows 7 裝置移轉至 Windows 10
使用適用於現有裝置的 Windows Autopilot，您可以建立設定檔並使用 Configuration Manager 工作順序部署它。 此程序可輕鬆地將現有裝置從 Windows 7 移轉到 Windows 10。 您在 Configuration Manager 中使用簽章 Windows 10 映像，然後將它套用到具有 Autopilot 設定的現有 Windows 7 裝置。 當使用者啟動裝置時，他們會使用 Autopilot 使用者驅動的上線程序。

以下是適用於現有裝置之 Autopilot 的步驟：

![適用於現有裝置之 Windows Autopilot 的程序概觀](media/autopilot-for-existing-devices.png)

1. 部署群組原則，將已知的資料夾重新導向到 OneDrive
2. 產生 Autopilot 設定檔
3. 部署工作順序以升級到 Windows 10
4. Windows 10 電腦在第一次開機時完成 Autopilot 程序

#### <a name="modernizing-device-provisioning-for-all-types-of-workers"></a>針對所有類型員工的現代化裝置佈建
利用 Autopilot，您現在可以使用自我部署模式針對非受控裝置或共用裝置提供無操作 OS 部署。 此設定符合您所有不同類型之員工的需求。 此外，Windows Autopilot 重設功能可確保將裝置重新佈建給新的使用者既簡單又容易。 當您有季節性員工或約聘員工時，此程序簡化了長久以來一個困難的工作。 



## <a name="case-study"></a>案例研究

德國物流與鐵路貨運公司 DB Shenker 使用 Autopilot 來提升員工產能，並使其 IT 團隊免於處理日常的支援工作。 Shenker 已經放棄傳統的映像處理，並以透過雲端進行佈建來取代。 他們現在使用 Azure AD Join 與 Intune 來設定新裝置並讓它開始執行。 

Shenker 現在使用 Windows Autopilot，而不是讓他們的遠端員工浪費時間前往有 IT 服務的位置。 他們將員工的硬體直接從製造商運送到當地的現場辦公室。 員工將新裝置連線到網際網路，然後使用 Azure AD 認證登入。 然後，裝置將連線到 Schenker IT 部門指派給使用者的個別設定檔的應用程式與服務。

如需詳細資訊，請參閱[全球物流公司集中 IT，將員工與現代數位工作場所聯繫在一起](https://customers.microsoft.com/story/db-schenker-travel-transportation-windows-10) \(英文\)。



## <a name="value-proposition"></a>價值主張

透過為使用者建立更好的使用者體驗，在您的組織中建立滿意度。 使用 Windows Autopilot 來降低成本。 騰出時間專注於其他專案，為您的組織帶來更多價值與影響力。



## <a name="configure"></a>設定

如需詳細資訊，請參閱下列文章：

[使用 Intune 建立 Windows Autopilot 設定檔](https://docs.microsoft.com/intune/enrollment-autopilot)

[適用於現有裝置的 Windows Autopilot 工作順序](../osd/deploy-use/windows-autopilot-for-existing-devices.md)

