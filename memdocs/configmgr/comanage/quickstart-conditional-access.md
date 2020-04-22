---
title: 搭配共同管理的條件式存取
titleSuffix: Configuration Manager
description: 根據來自 Intune 的合規性規則控制使用者對組織資源的存取
ms.date: 05/13/2019
ms.prod: configuration-manager
ms.technology: configmgr-comanage
ms.topic: conceptual
ms.assetid: 4cf640b3-610c-4c3c-b966-c62e9f5654ff
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: d35f36b6578359f62f21b4e2208a70ace22cf0d9
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81691256"
---
# <a name="conditional-access-with-co-management"></a>搭配共同管理的條件式存取

條件式存取可確保只有受信任的使用者能透過受信任裝置上的受信任應用程式存取組織資源。 它是在雲端中從頭建立。 無論您是使用 Intune 來管理裝置，還是搭配共同管理來延伸 Configuration Manager 部署，其運作方式皆相同。

在下列影片中，資深專案經理 Joey Glocke 與產品行銷經理 Locky Ainley 會討論並示範搭配共同管理的條件式存取：

> [!VIDEO https://channel9.msdn.com/Series/Endpoint-Zone/The-Security-Benefits-of-Conditional-Access/player]

搭配共同管理，Intune 會評估網路中的每個裝置以判斷其可信任程度。 它會以下列兩種方式執行此評估：

1. Intune 會確定裝置或應用程式已受管理並安全地設定。 此檢查會依您組織合規性原則的設定方式而有所差異。 例如，確保所有裝置皆已啟用加密且未被破解。  

    - 此評估會在安全性缺口發生前進行，並以設定為基礎  

    - 針對共同管理的裝置，Configuration Manager 也會進行以設定為基礎的評估。 例如要求更新或應用程式合規性。 Intune 會將其自己的評量與此評估結合。  

2. Intune 會偵測裝置上的作用中安全性事件。 會使用 [Microsoft Defender 進階威脅防護](/windows/security/threat-protection/microsoft-defender-atp/microsoft-defender-advanced-threat-protection) (先前稱為 Windows Defender ATP) 與其他[行動裝置威脅防護提供者](https://www.lookout.com/about/partners/microsoft)的智慧型安全性。 這些合作夥伴會在裝置上執行持續的行為分析。 此分析會偵測作用中的事件，然後將此資訊傳遞至 Intune 以進行即時的合規性評估。  

    - 此評估會在安全性缺口發生後進行，並以事件為基礎  

Microsoft 企業副總裁 Brad Anderson 在 Ignite 2018 重點演說期間，搭配即時示範對條件式存取進行深度討論。 

> [!VIDEO https://www.youtube.com/embed/7tDbUhVCX_I?start=1071]

條件式存取也能提供集中式的位置，以查看所有已連線至網路之裝置的健康情況。 您能取得雲端規模的優點，這在測試 Configuration Manager 生產環境執行個體上特別有價值。


## <a name="benefits"></a>優點

所有 IT 團隊皆無比重視網路安全性。 您必須在每個裝置能存取您的網路之前，確定其符合您的安全性與商務需求。 透過條件式存取，您可以決定下列因素： 
- 每個裝置是否皆已加密  
- 是否已安裝惡意程式碼  
- 其設定是否已更新  
- 其是否已越獄或 Root  

條件式存取能結合對組織資料的精確控制，以及能在位於任何位置的任何裝置上最大化員工生產力的使用者體驗。

下列影片示範[進階威脅防護](https://www.microsoft.com/windowsforbusiness/windows-atp) (ATP) 能如何整合至您經常會體驗到的常見案例：

> [!VIDEO https://www.youtube.com/embed/A7IrxAH87wc?start=178]

透過共同管理，Intune 可以納入 Configuration Manager 在評量您針對必要更新或應用程式的安全性標準合規性上的責任。 對於想要繼續使用 Configuration Manager 來進行複雜應用程式和修補程式管理的所有 IT 組織來說，此行為至關重要。

條件式存取也是開發[零信任網路](https://cloudblogs.microsoft.com/microsoftsecure/2018/06/14/building-zero-trust-networks-with-microsoft-365/) \(英文\) 架構的重要元件。 透過條件式存取，符合規範的裝置存取控制會涵蓋零信任網路的基本層。 此功能會在您於未來保護組織的方法中扮演重要的角色。

如需詳細資訊，請參閱關於 [Enhancing conditional access with machine-risk data from Microsoft Defender Advanced Threat Protection](https://techcommunity.microsoft.com/t5/Enterprise-Mobility-Security/Enhancing-conditional-access-with-machine-risk-data-from-Windows/ba-p/250559) (從 Microsoft Defender 進階威脅防護搭配電腦風險資料強化條件式存取) 的部落格文章。



## <a name="case-studies"></a>案例研究

IT 顧問公司 Wipro 使用條件式存取來保護並管理全體 91,000 個員工所使用的裝置。 在近日的案例研究中，Wipro 的 IT 副總裁表示：

> *達成條件式存取是 Wipro 的一大勝利。現在，我們所有員工都可以藉由行動方式隨需存取資訊。* 
> *我們加強了安全性狀態及員工生產力。現在 91,000 名員工可以受益於隨時隨地從任何裝置存取超過 100 個應用程式，且非常安全。*

<!-- waiting for the case study to be public
For more information, see [Wipro drives mobile productivity with Microsoft cloud security tools to improve customer engagements](https://customers.microsoft.com/story/446f72f9-2f50-4697-b688-6d279786e010)
-->

其他範例包括： 

- Nestlé，其將應用程式型的條件式存取用於超過 150,000 名員工  

- 自動化軟體公司 Cadence，其現已確保「只有受控的裝置才能存取如 Teams 等的 Office 365 應用程式，以及公司的內部網路」。 他們也能讓其員工「以更安全的方式存取其他雲端型的應用程式，例如 Workday 和 Salesforce。」 如需 Cadence 的 Intune 使用體驗的詳細資訊，請參閱 [Cadence 透過 Microsoft 365 中的行動裝置共同作業工具提升商務步調](https://customers.microsoft.com/story/cadence-partner-professional-services-microsoft-365)\(英文\)。

Intune 也已和 Cisco ISE、Aruba Clear Pass 與 Citrix NetScaler 等合作夥伴完全整合。 透過這些合作夥伴，您可以根據 Intune 註冊和這些其他平台上的裝置合規性狀態來維持存取控制。

如需詳細資訊，請參閱下列影片：
- [Brad Anderson 詳細示範條件式存取](https://youtu.be/8321obNofgM?t=547) \(英文\)  
- [來自 Endpoint Zone 1805 的額外詳細資料](https://youtu.be/f-ILlEuBFZg?t=196) \(英文\)  


## <a name="value-proposition"></a>價值主張

透過條件式存取和 ATP 整合，您將能強化所有 IT 組織的基礎元件：安全的雲端存取。

在超過 63% 的資料外洩中，攻擊者都是透過脆弱、預設或遭竊的使用者認證來取得組織網路的存取權。 由於條件式存取是專注在保護使用者身分識別上，它能限制對認證的竊取。 條件式存取能管理並保護您的身分識別，無論其是否具有特殊權限。 這是保護裝置及其所保存之資料的最佳方式。

由於條件式存取是 Enterprise Mobility + Security (EMS) 的核心元件，因此不需要任何內部部署設定或架構。 透過 Intune 和 Azure Active Directory (Azure AD)，您可以快速在雲端中設定條件式存取。 如果您正在使用 Configuration Manager，則可以透過共同管理輕鬆地將您的環境延伸至雲端，並立即開始使用。

如需 ATP 整合的詳細資訊，請參閱這篇 [Microsoft Defender ATP device risk score exposes new cyberattack, drives Conditional access to protect networks](https://cloudblogs.microsoft.com/microsoftsecure/2018/11/28/windows-defender-atp-device-risk-score-exposes-new-cyberattack-drives-conditional-access-to-protect-networks/) (Microsoft Defender ATP 裝置風險分數公開新的網路攻擊，並驅動條件式存取以保護網路) 部落格文章。 它會詳述進階駭客群組使用前所未見工具的方式。 Microsoft 雲端之所以能成功偵測並阻止它們，是因為目標使用者擁有條件式存取。 該入侵啟動了該裝置的風險型條件式存取原則。 雖然攻擊者已經成功入侵網路，系統順利地自動限制被入侵的電腦，使其無法存取由 Azure AD 管理的組織服務與資料。



## <a name="configure"></a>設定

當您[啟用共同管理](how-to-enable.md)時，條件式存取非常容易使用。 它需要您將**合規性原則**工作負載移至 Intune。 如需詳細資訊，請參閱[如何將 Configuration Manager 工作負載切換至 Intune](how-to-switch-workloads.md)。 

如需使用條件式存取的詳細資訊，請參閱下列文章： 

- [Azure AD 中的條件式存取](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access-azure-portal)  

- [Intune 裝置合規性原則](https://docs.microsoft.com/intune/device-compliance)  

- [搭配 Intune 使用應用程式型條件式存取](https://docs.microsoft.com/intune/app-based-conditional-access-intune)  

> [!Note]  
> 條件式存取功能可立即供已加入混合式 Azure AD 的裝置使用。 這些功能包括多重要素驗證和混合式 Azure AD Join 存取控制。 此行為是因為它們是以 Azure AD 屬性為基礎。 若要運用來自 Intune 和 Configuration Manager 以設定為基礎的評量，請啟用共同管理。 此設定能讓您直接從 Intune 對合規裝置進行存取控制。 它也能提供 Intune 的合規性原則評估功能。  

