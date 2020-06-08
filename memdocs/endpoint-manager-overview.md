---
title: Microsoft 端點管理員概觀 - Azure | Microsoft Docs
description: 「端點管理員」包含 Intune、Configuration Manager、共同管理、「電腦分析」、Windows Autopilot 及系統管理中心，用以管理所有裝置，包括內部部署。
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 05/21/2020
ms.topic: overview
ms.service: microsoft-intune
ms.subservice: ''
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: dougeby
ms.suite: ems
search.appverid: MET150
ms.custom: get-started
ms.collection: M365-identity-device-management
ms.openlocfilehash: d9e3d03211907f31008b31d68c4ed5cd11ae1a6e
ms.sourcegitcommit: fb77170957f50aa386ff825fb4183b4fd9e3e488
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/22/2020
ms.locfileid: "83791735"
---
# <a name="microsoft-endpoint-manager-overview"></a>Microsoft 端點管理員概觀

「Microsoft 端點管理員」可協助提供現代化工作場所和現代化管理，讓您的資料不論是在雲端還是內部部署都保持安全。 「端點管理員」包含您用來管理和監視行動裝置、桌上型電腦、虛擬機器、內嵌裝置及伺服器的服務與工具。

「端點管理員」結合了您可能知道且已在使用的服務，包括 Microsoft Intune、Configuration Manager、「電腦分析」、共同管理及 Windows Autopilot。 這些服務是 Microsoft 365 堆疊的一部分，可協助保護存取、保護資料，以及回應和管理風險。

首先，請觀看下列由 Microsoft 公司副總裁 Brad Anderson 針對 Microsoft 365 提供的兩分鐘影片：

> [!VIDEO https://www.youtube.com/embed/GS7oNPInFuw]

## <a name="what-you-get"></a>您會獲得的服務

「端點管理員」包含下列服務：

- **Microsoft Intune**：Intune 是適用於您應用程式與裝置的 100% 雲端式行動裝置管理 (MDM) 和行動應用程式管理 (MAM) 提供者。 它可讓您控制 Android、Android Enterprise、iOS/iPadOS、macOS 及 Windows 10 裝置上的功能與設定。 它與其他服務整合，包括 Azure Active Directory (AD)、行動威脅防禦工具、ADMX 範本、Win32 及自訂 LOB 應用程式等等。

  如果您有內部部署基礎結構 (例如 Exchange 或 Active Directory)，則也可以使用 Intune 連接器：

  - 「適用於 Active Directory 的 Intune 連接器」會針對使用 Windows Autopilot 註冊的電腦，將項目新增至您的內部部署 Active Directory 網域。 如需詳細資訊，請參閱[部署已加入混合式 Azure AD 的裝置](/mem/intune/enrollment/windows-autopilot-hybrid)。
  - 如果裝置已在 Intune 中註冊且符合您的原則規範，則 **Intune Exchange 連接器**會允許 (或封鎖) 裝置存取您的 Exchange 伺服器。 如需詳細資訊，請參閱[安裝內部部署 Intune Exchange 連接器](/mem/intune/protect/exchange-connector-install)。
  - 「Intune 憑證連接器」會處理來自使用憑證進行驗證和 S/MIME 電子郵件加密之裝置的憑證要求。 如需詳細資訊，請參閱[使用憑證進行驗證](/mem/intune/protect/certificates-configure)。

  作為「端點管理員」的一部分，使用 Intune 來建立及檢查合規性，然後使用雲端將應用程式、功能及設定部署到您的裝置。

  如需詳細資訊，請參閱[什麼是 Microsoft Intune](https://docs.microsoft.com/intune/fundamentals/what-is-intune)。

- **Configuration Manager**：Configuration Manager 是一個內部部署管理解決方案，可管理網路或網際網路上的桌上型電腦、伺服器及膝上型電腦。 您可以啟用其雲端功能來與 Intune、Azure Active Directory (AD)、Microsoft Defender ATP 及其他雲端服務進行整合。 使用 Configuration Manager 來部署應用程式、軟體更新及作業系統。 您也可以監視合規性、即時查詢用戶端並對其進行操作等等。

  作為「端點管理員」的一部分，繼續使用 Configuration Manager，如您一直所做的一樣。 如果您已經準備好將一些工作移至雲端，請考慮使用[共同管理](https://docs.microsoft.com/configmgr/comanage/)。

  如需詳細資訊，請參閱[什麼是 Configuration Manager？](https://docs.microsoft.com/configmgr/core/understand/introduction)

- **共同管理**：共同管理會使用 Intune 及其他 Microsoft 365 雲端服務，將您現有的內部部署 Configuration Manager 投資與雲端結合。 您可以選擇是要讓 Configuration Manager 還是 Intune 成為七個不同工作負載群組的管理授權單位。

  作為「端點管理員」的一部分，共同管理會使用雲端功能，包括條件式存取。 您會將部分工作保留在內部部署環境中，同時又使用 Intune 在雲端中執行其他工作。

  如需詳細資訊，請參閱[什麼是共同管理？](https://docs.microsoft.com/configmgr/comanage/overview)。

- **電腦分析**：電腦分析是與 Configuration Manager 整合的雲端式服務。 它可以提供見解與情報，讓您為您的 Windows 用戶端更新整備做出更明智的決策。 此服務結合了來自您組織的資料，以及從連線到 Microsoft 雲端的數百萬部裝置彙總而成的資料。 它會提供您組織中安全性更新、應用程式及裝置的相關資訊，並識別應用程式和驅動程式的相容性問題。 請針對最有可能為您組織中各項資產提供最佳見解的裝置建立試驗。

  作為「端點管理員」的一部分，使用由雲端提供技術支援的「電腦分析」見解，讓 Windows 10 裝置保持在最新狀態。

  如需詳細資訊，請參閱[什麼是電腦分析？](https://docs.microsoft.com/configmgr/desktop-analytics/overview)

- **Windows Autopilot**：Windows Autopilot 會安裝並預先設定新的裝置，將它們準備好以供使用。 其設計目的是要為 IT 和終端使用者，簡化 Windows 裝置從初始部署到生命週期結束的生命週期。

  作為「端點管理員」的一部分，使用 Autopilot 來預先設定裝置，並在 Intune 中自動註冊裝置。 您也可以將 Autopilot 與 Configuration Manager 和共同管理整合，以進行更複雜的裝置設定 (預覽階段)。

  如需詳細資訊，請參閱 [Windows Autopilot 概觀](https://docs.microsoft.com/windows/deployment/windows-autopilot/windows-autopilot) \(部分機器翻譯\) 和[在 Intune 中註冊 Windows 裝置](/mem/intune/enrollment/enrollment-autopilot)。

- **Azure Active Directory (AD)** ：Azure AD 由端點管理員用來進行裝置、使用者、群組和多重要素驗證 (MFA) 的身分識別。 **Azure AD Premium** (可能會是額外成本) 具有[額外的功能](https://azure.microsoft.com/pricing/details/active-directory/)，可協助保護裝置、應用程式和資料，包括動態群組、自動註冊和條件式存取。

  如需詳細資訊，請參閱[新增使用者](/mem/intune/fundamentals/users-add)、[設定自動註冊](/mem/intune/enrollment/windows-enroll)，以及[關於條件式存取 ](/mem/intune/protect/conditional-access)。

- **端點管理員系統管理中心**：[系統管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)是一個可建立原則並管理裝置的一站式網站。 其中插入了其他重要的裝置管理服務，包括群組、安全性、條件式存取及報告。 此系統管理中心也會顯示由 Configuration Manager 和 Intune 管理的裝置 (預覽階段)。

## <a name="choose-whats-right-for-you"></a>選擇適合您的選項

有幾個方法可判斷適合您組織的選項。 您接下來的步驟取決於您組織所執行的工作。 請思考一下您要嘗試達成的目的。

例如：

- 如果您經常佈建新裝置，則請從 Windows Autopilot 開始著手。
- 如果您要為使用者、應用程式及裝置新增規則和控制設定，則請從 Intune 開始著手。
- 如果您目前使用 Configuration Manager 來部署應用程式，而想要根據安全性需求使用條件式存取，則請從共同管理開始著手。
- 如果您目前使用 Configuration Manager，且負責讓 Windows 10 裝置保持在最新狀態，則請從「電腦分析」開始著手。
- 如果您正開始使用 MDM 和 MAM，或使用 ADMX 範本來控制 Office、Microsoft Edge 及 Windows 設定，則請從 Intune 開始著手。

您也可以將「端點管理員」分成三部分來思考：雲端、內部部署，以及雲端 + 內部部署：

- **雲端**：所有資料都儲存在 Azure 中。 因此，不再有資料中心。 這個方法為您帶來了雲端的行動優勢，以及 Azure 的安全性優勢。

- **內部部署**：如果您的內部部署基礎結構包含 Configuration Manager，或尚未做好使用雲端的準備，則您可以保留現有的系統。

- **雲端 + 內部部署**：許多環境都是混合的，而且使用雲端連結方法。 這表示它們使用雲端與內部部署的組合。 針對新裝置，請使用 Intune 的優點來存取和保護資料。 如果您使用 Configuration Manager，請連線到雲端以取得額外的功能和分析。 如果您想要將部分工作負載移至雲端，則共同管理是個理想選項。

## <a name="what-you-need-to-get-started"></a>開始使用的必要條件

Microsoft 端點管理員是統一數種技術的解決方案平台。 這不是新的授權。 服務的授權方式會依據其個別授權條款。 如需詳細資訊，請參閱[產品授權條款](https://www.microsoft.com/licensing/product-licensing/products)。

如果您目前使用 Configuration Manager，您也會取得 Microsoft Intune 來共同管理您的 Windows 裝置。 針對 iOS/iPadOS 和 Android 等其他平台，則需要個別的 Intune 授權。

在大多數情況下，Microsoft 365 可能是最佳選項，因為它可提供您「端點管理員」和 Office 365。 如需詳細資訊，請參閱 [Microsoft 365](https://www.microsoft.com/licensing/product-licensing/microsoft-365-enterprise)。

## <a name="next-steps"></a>後續步驟

[使用雲端智慧的強大功能來簡化和加速 IT 並移至現代化工作場所](https://www.microsoft.com/microsoft-365/blog/2019/11/04/use-the-power-of-cloud-intelligence-to-simplify-and-accelerate-it-and-the-move-to-a-modern-workplace/) \(英文\)

[Microsoft 端點管理員](https://www.microsoft.com/microsoft-365/microsoft-endpoint-manager)

[教學課程：逐步解說 Microsoft 端點管理員中的 Intune](/intune/fundamentals/tutorial-walkthrough-endpoint-manager)

[什麼是 Microsoft 365？Learn 課程模組](https://docs.microsoft.com/learn/modules/what-is-m365/index)
