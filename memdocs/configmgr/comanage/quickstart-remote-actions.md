---
title: 透過共同管理的遠端動作
titleSuffix: Configuration Manager
description: 從 Intune 針對共同管理的裝置執行遠端動作
ms.date: 01/14/2019
ms.prod: configuration-manager
ms.technology: configmgr-comanage
ms.topic: conceptual
ms.assetid: 4a877bed-f6c4-4048-9421-507dc848af5c
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 0ca37a4e15f5da63ed743b541eeabc43708b0be1
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2020
ms.locfileid: "82075314"
---
# <a name="remote-actions-with-co-management"></a>透過共同管理的遠端動作

您需要確定所管理的每個裝置均可連線，而不論其位於何處、何時連線。 您也需要為每個使用者提供保有生產力所需的一切，同時保護應用程式和資料。 透過 Intune 所支援的裝置動作，您可以從遠端解決這些重要功能。

在下列影片中，首席方案經理 Heidi Cheng 與資深方案經理 Danny Guillory 正在討論並示範透過共同管理的遠端動作：

> [!VIDEO https://channel9.msdn.com/Series/Endpoint-Zone/Using-Co-Management-to-Execute-Remote-Actions/player]



## <a name="benefits"></a>優點

遠端裝置動作可以為您提供裝置上的管理控制，而不會干擾個人資料。 這些遠端裝置動作可讓您： 
- 刪除遺失或遭竊裝置上的公司資料  
- 重新命名裝置  
- 重新啟動裝置  
- 檢閱裝置清查  
- 遠端控制裝置  
- 透過「全新開始」重新啟動來抹除預先安裝的 OEM 應用程式  
- 在任何 Windows 10 裝置上進行出廠重設  

這些功能為重要且簡單的方式，可用於保護這些裝置上所儲存的公司資料，而不論其位於電子郵件或 OneDrive。

如需這些動作的詳細資訊，請參閱[可用的遠端動作](#available-remote-actions)。 



## <a name="case-studies"></a>案例研究

全球顧問公司 Avanade 會定期使用遠端動作，來管理其 30,000 個員工所使用的裝置。 Avanade 的 CIO 在[近期部落格文章](https://www.microsoft.com/microsoft-365/blog/2018/02/07/the-future-is-on-the-other-side-of-this-bridge/)中表示：

> 擁有 Intune 功能所帶給我們的立即優勢是能夠以遠端方式在機器上重設 Windows。  這對我們遺失或遭竊的機器來說非常重要，這對於具有高度行動力的行動員工而言更為普遍。
> 這是我們必須在自訂 ConfigMgr 封裝中建置並維護的功能。 

如需如何使用這些遠端動作的詳細資訊，請參閱[可用的裝置動作](../../intune/remote-actions/device-management.md#available-device-actions)。


## <a name="value-proposition"></a>價值主張

共同管理 Configuration Manager 裝置時，它會立即新增這些 Configuration Manager 原本就不需要的功能。 現在，您可以立即進行 Intune 所支援的任何遠端動作。 

透過共同管理，Configuration Manager 裝置現在就如同任何其他受 Intune 管理的裝置。 例如，它們完全存在於雲端，只要它們具有網際網路存取權，您就可以連線到它們。 您可以執行所有這些動作，而不需採取任何額外的步驟 (但啟用共同管理除外)。

由於使用者不會察覺自動註冊程序，因此不會對其生產力產生影響。 使用者不需要執行任何動作。


### <a name="available-remote-actions"></a>可用的遠端動作

一旦您在 Configuration Manager 中[啟用共同管理](how-to-enable.md)之後，即可從 Intune 使用這些遠端動作。

#### <a name="remove-devices"></a>移除裝置
- **淘汰**：這個動作會移除受控應用程式和資料 (如果適用)、設定，以及已指派給該裝置的電子郵件設定檔。 接著從 Intune 管理移除裝置。 此流程會在下一次裝置簽入並接收遠端淘汰動作時發生。 淘汰動作會將使用者的個人資料保留在裝置上。  

- **抹除**：此動作會將裝置還原為其出廠預設值。 如果您選擇**保留註冊狀態及使用者帳戶**的選項，則會保留使用者資料。 否則會安全地清除磁碟機。  

- **刪除**：如果您想要從 Azure 入口網站的 Intune 移除裝置，請從特定的裝置窗格中刪除它們。 下一次裝置簽入時，它就會移除儲存於其上的所有組織資料。  

如需詳細資訊，請參閱[使用抹除、淘汰或手動取消註冊裝置來移除裝置](../../intune/remote-actions/devices-wipe.md)。

#### <a name="selective-wipe"></a>選擇性抹除
<!--SCCMDocs issue 973-->
當您選擇 [應用程式選擇性抹除]  時，它會移除公司應用程式資料，而不會移除個人資料。 當裝置報告為遺失或遭竊時使用此動作。 

如需詳細資訊，請參閱[如何只抹除 Intune 管理之應用程式中的公司資料](../../intune/apps/apps-selective-wipe.md)。

#### <a name="sync"></a>同步
**同步**裝置動作會強制所選取的裝置立即使用 Intune 簽入。 當裝置簽入時，會立即接收所有擱置動作或已指派給它的原則。

此功能可協助您立即驗證已指派的原則並對其進行疑難排解，而不用等到下次排程的簽入才進行。

如需詳細資訊，請參閱[使用 Intune 同步裝置以取得最新的原則和動作](../../intune/remote-actions/device-sync.md)。

#### <a name="restart"></a>重新啟動
**重新啟動**裝置動作會使得您所選擇的裝置重新啟動。 若有擱置的重新開機，但使用者無法執行它，則此動作非常有用。

如需詳細資訊，請參閱[使用 Intune 從遠端重新啟動裝置](../../intune/remote-actions/device-restart.md)。

#### <a name="fresh-start"></a>全新開始
**全新開始**裝置動作會移除安裝於任何執行 Windows 10 1703 版或更新版本之裝置上的應用程式。 「全新開始」有助於移除新裝置通常會安裝的預先安裝 (OEM) 應用程式。

如果您選擇不要保留使用者資料，裝置就會還原為其立即可用狀態。 它會向 Azure AD 和 MDM 中取消註冊。

如果您預先決定的標準與哪些應用程式應該位於裝置上有關，則此動作會排除不符合您準則的項目。

如需詳細資訊，請參閱[透過 Intune 使用「重新開始」重設 Windows 10 裝置](../../intune/remote-actions/device-fresh-start.md)。 

#### <a name="remote-control"></a>遠端控制
Intune 所管理的裝置可以使用 [TeamViewer](https://www.teamviewer.com/) 從遠端管理。 TeamViewer 是您可個別取得的協力廠商程式。

如需詳細資訊，請參閱[使用 TeamViewer 來遠端管理 Intune 裝置](../../intune/remote-actions/teamviewer-support.md)。



## <a name="configure"></a>設定

除了透過 TeamViewer 進行遠端控制，若要在 Intune 中開始使用這些遠端裝置動作，當您[啟用共同管理](how-to-enable.md)之後就不需要任何額外設定。

如需使用 TeamViewer 進行遠端控制的詳細資訊，請參閱[使用 TeamViewer 來遠端管理 Intune 裝置](../../intune/remote-actions/teamviewer-support.md)。
