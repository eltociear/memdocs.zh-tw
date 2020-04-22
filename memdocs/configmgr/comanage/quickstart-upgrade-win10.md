---
title: 升級 Windows 10
titleSuffix: Configuration Manager
description: 將裝置升級到 Windows 10 1709 版或更新版本 (共同管理所需)
ms.date: 01/14/2019
ms.prod: configuration-manager
ms.technology: configmgr-comanage
ms.topic: conceptual
ms.assetid: 561eb5b6-f90c-485a-91c2-e45bb0ce7877
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: e11a6130fb9f7d86b7d3377cc4120d4e61c43d2d
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81691196"
---
# <a name="upgrade-windows-10-for-co-management"></a>升級 Windows 10 以進行共同管理

當您在為組織準備共同管理時，取得最新版本對於某些客戶是一大障礙。 共同管理需要 [Windows 10 1709 版](https://docs.microsoft.com/windows/whats-new/whats-new-windows-10-version-1709)或更新版本。 更新 Windows 並設定自動註冊之後，您的用戶端會自動註冊共同管理。

在下列影片中，資深專案經理 Rob York 與產品行銷經理 Locky Ainley 討論並示範如何為進行共同管理升級至 Windows 10：

> [!VIDEO https://channel9.msdn.com/Series/Endpoint-Zone/Upgrading-to-Windows-10-to-Enable-Co-Management/player]



## <a name="why-upgrade"></a>為何要升級？

除了平台其他方面的改進，Windows 10 1709 版和更新版本還支援自動註冊。 此行為讓裝置在加入 Azure Active Directory (Azure AD) 時，會自動向 Intune 註冊。 

如需詳細資訊，請參閱[啟用 Windows 10 自動註冊](https://docs.microsoft.com/intune/windows-enroll#enable-windows-10-automatic-enrollment)。


## <a name="how-to-do-it"></a>如何進行

以下是我們在協助數千個客戶取得最新版時所學到的祕訣：

- 使用階段式部署將此升級在正確的時間推出給正確的人員。 如需詳細資訊，請參閱[建立階段式部署](../osd/deploy-use/create-phased-deployment-for-task-sequence.md)。  

- 使用預先快取，以減少使用者等候時間。 如需詳細資訊，請參閱[設定預先快取內容](../osd/deploy-use/configure-precache-content.md)。  

- 使用預設的就地升級工作順序範本。 然後設定您的升級前和升級後步驟，以及任何失敗時的動作。 如需詳細資訊，請參閱[建議的後續處理工作順序步驟](../osd/deploy-use/create-a-task-sequence-to-upgrade-an-operating-system.md#recommended-task-sequence-steps-for-post-processing)。  

- 如果您的環境有高機動性員工，Configuration Manager 支援透過雲端管理閘道 (CMG) 的就地升級。 此功能可讓您升級以網際網路為基礎的 Windows 10 用戶端。 如需 CMG 的詳細資訊，請參閱[透過 CMG 部署 Windows 10 就地升級](../osd/deploy-use/deploy-a-task-sequence.md#deploy-windows-10-in-place-upgrade-via-cmg)。  

- 為想要成為早期採用者的使用者提供選擇加入共同管理的選項。 此方法可加速初始採用。 藉由事先識別這些人員，您可確保早期推出有良好的涵蓋範圍。 您也會從喜歡變更且有興趣頻繁變更的使用者收到驗證和意見反應。 早期採用計畫可刺激對新技術的興趣，且人數會隨時間增加。  


## <a name="case-studies"></a>案例研究

Microsoft IT 將 Windows 10 部署到 96,000 個在 Microsoft 的分散使用者。 該部署包括遠端用者與公司網路上的使用者。 該部署在九週內完成。 如需其經驗的詳細資訊，請參閱[在 Microsoft 以就地升級方式部署 Windows 10](https://www.microsoft.com/itshowcase/deploying-windows-10-at-microsoft-as-an-in-place-upgrade) \(英文\)。  

一間大型歐洲軟體製造商成功地使用早期採用者群組。 在初始測試和試驗群組之後，大約有 2,000 個員工收到第一次更新、升級與軟體。 此群組包含 IT 人員與選擇加入的志願者。 達到此程度的使用者參與，讓他們在測試時更有信心，而且在開始大量推出時會更可靠。



## <a name="contact-fasttrack"></a>連絡 FastTrack

如果您在 Windows 10 升級程序中的任何時刻需要協助，請移至 [Microsoft FastTrack](https://Microsoft.com/FastTrack/)，登入並要求提供協助。 

如需詳細資訊，請參閱[從 FastTrack 取得協助](quickstart-fasttrack.md)。 

