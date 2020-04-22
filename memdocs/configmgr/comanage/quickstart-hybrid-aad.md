---
title: 使用 Azure AD 進行共同管理
titleSuffix: Configuration Manager
description: 透過 Azure AD，您可以同時在雲端與內部部署環境中善用已提升的使用者生產力與資源安全性
ms.date: 01/14/2019
ms.prod: configuration-manager
ms.technology: configmgr-comanage
ms.topic: conceptual
ms.assetid: 2af37410-d04c-4059-801c-9edb8bf72d89
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: a84247482ddece88208e83fec545afc5e953a070
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81691286"
---
# <a name="use-azure-ad-for-co-management"></a>使用 Azure AD 進行共同管理

身分識別是雲端的新控制平面。 Azure Active Directory (Azure AD) 可讓您在雲端和內部部署環境間連結使用者、裝置與應用程式。 向 Azure AD 註冊裝置，讓您能夠提升使用者的生產力與資源的安全性。 在 Azure AD 中具有裝置，是共同管理與裝置型條件式存取的基礎。

如需有關裝置型條件式存取的詳細資訊，請參閱[操作說明：需要受控裝置以使用條件式存取來存取雲端應用程式](https://docs.microsoft.com/azure/active-directory/conditional-access/require-managed-devices) \(機器翻譯\)。

在下列影片中，資深程式經理 Sandeep Deo 與產品行銷經理 Adam Harbour 正在討論和示範如何使用 Azure AD 進行共同管理：

> [!VIDEO https://channel9.msdn.com/Series/Endpoint-Zone/Embedding-Co-management-With-Azure-Active-Directory/player]

Azure AD 會針對公司擁有的裝置提供兩個選項以符合組織需求：  

- **已加入 Azure AD 的裝置**：將 Windows 10 裝置加入至 Azure AD，而不需將其加入至您的內部部署 Active Directory  

  - 支援 Windows 10

  - 在不需對您的內部部署環境任何額外設定的情況下進行設定  

  - 透過啟用 Azure AD 中的一些設定，您可以讓使用者透過 Windows 安裝體驗 (OOBE) 來將裝置加入至 Azure AD  

  - 如需詳細資訊，請參閱[如何：。規劃 Azure AD 加入實作](https://docs.microsoft.com/azure/active-directory/devices/azureadjoin-plan) \(機器翻譯\)  

- **已加入混合式 Azure AD 的裝置**：將您已加入網域的現有裝置加入至 Azure AD  

  - 支援 Windows 10、Windows 8.1 與 Windows 7

  - 使用 AD FS 宣告或 Azure AD Connect 進行設定  

  - 針對 Windows 10，加入會在機器內容中進行，因此使用者不需採取額外步驟  

  - 如需詳細資訊，請參閱[如何規劃您的混合式 Azure Active Directory 加入實作](https://docs.microsoft.com/azure/active-directory/devices/hybrid-azuread-join-plan) \(機器翻譯\)  

這兩個選項均會為使用者提供類似功能。 它讓您能夠根據需求彈性選擇其中一個。 例如，您可以從已加入 Azure AD 的機器[存取內部部署資源](https://docs.microsoft.com/azure/active-directory/devices/azuread-join-sso) \(機器翻譯\)，即使它們並未加入至 Active Directory 也可以。

您可以在各種環境中將裝置加入至 Azure AD，而不論您的[驗證方法](https://docs.microsoft.com/azure/active-directory/hybrid/choose-ad-authn) \(機器翻譯\) 為何。 例如，同盟驗證或雲端驗證。

如果您已經有內部部署 Active Directory，則可直接設定其中一個選項。

## <a name="benefits"></a>優點

將裝置加入至 Azure AD，可為貴組織提供下列優點：

### <a name="single-sign-on-to-cloud-resources"></a>單一登入至雲端資源

在加入至 Azure AD 的裝置上，您可以取得存取任何雲端或內部部署資源的整合式體驗。 一旦您登入已加入至 Azure AD 的 Windows 機器之後，您就會單一登入至所有應用程式，而不需要任何額外的登入提示。  

### <a name="windows-hello-for-business"></a>Windows Hello 企業版

Windows Hello 企業版為 Windows 10 帶來強大的無密碼驗證。 將您的裝置加入至 Azure AD，您就能針對雲端和內部部署資源，在您的使用者群體間啟用 Windows Hello 企業版。 Windows Hello 企業版可排除記住複雜密碼或不小心將其公開的問題。 其登入程序是簡單且安全的。

如需詳細資訊，請參閱 [Windows Hello 企業版](https://docs.microsoft.com/windows/security/identity-protection/hello-for-business/hello-identity-verification)。  

### <a name="device-based-conditional-access"></a>裝置型條件式存取

根據裝置狀態啟用條件式存取，進一步保護組織的資料。 裝置型條件式存取需要一個受控裝置。 此裝置必須是符合規範的裝置或加入混合式 Azure AD 的裝置。 針對已加入 Azure AD 的裝置，您需要 Intune 將裝置標示為符合規範。 但是，針對已加入混合式 Azure AD 的裝置，裝置狀態本身可用來評估條件式存取。 共同管理會透過 Intune 評估已加入混合式 Azure AD 裝置的合規性來提供額外優點。 此功能確保裝置設定會保持不變。

如需有關裝置型條件式存取的詳細資訊，請參閱[操作說明：需要受控裝置以使用條件式存取來存取雲端應用程式](https://docs.microsoft.com/azure/active-directory/conditional-access/require-managed-devices) \(機器翻譯\)。  

### <a name="automatic-device-licensing"></a>自動裝置授權

所有已加入 Azure AD 的 Windows 10 裝置都會通過授權檢查。 這些檢查可讓您透過 Microsoft 雲端自動將它們從專業版升級為企業版。 當您從使用者移除相關的訂用帳戶時，裝置就會自動將其授權降級。 此功能可提供單一控制窗格來管理 Windows 授權，而不需任何複雜的流程或內部部署系統。

### <a name="self-service-functionality"></a>自助式功能

自助式功能包括自助式密碼重設與 BitLocker 修復金鑰。 Azure AD 也會為您提供直接選項，來重設密碼或存取 BitLocker 修復金鑰。 您可以使用 Azure AD，直接從 Windows 鎖定畫面重設密碼，而不是從網頁瀏覽器。 這些功能可減少使用者的摩擦，有助於降低組織的技術服務人員成本。  

如需詳細資訊，請參閱[教學課程：讓使用者使用 Azure Active Directory 自助式密碼重設來解除鎖定其帳戶或重設密碼](https://docs.microsoft.com/azure/active-directory/authentication/tutorial-enable-sspr)。

### <a name="enterprise-state-roaming"></a>企業狀態漫遊

所有已加入至 Azure AD 的裝置都可以將其設定同步到雲端。 使用者登入的所有裝置都會同步處理其所有設定，以取得更具生產力的體驗。  

## <a name="value-proposition"></a>價值主張

透過這其中任一種方法來將裝置加入至 Azure AD，可加速數位轉型。 它會啟用更多 Microsoft 365 所提供的功能。 您將具有更佳體驗，而您的資料將具有更高的安全性。

Azure AD 提供數個選項來減輕您的工作負載，例如：

- 從單一位置管理貴組織的所有裝置身分識別  

- 啟用自助式密碼重設，以降低技術服務人員成本。 接著，您的使用者可以隨時在您的裝置上，重設 Windows 10 鎖定畫面的密碼。  

## <a name="configure"></a>設定

如果您已經具有內部部署 Active Directory 環境，而且想要將已加入網域的裝置加入至 Azure AD，請設定已加入混合式 Azure AD 的裝置。 如需詳細資訊，請參閱[如何：規劃混合式 Azure Active Directory 加入實作](https://docs.microsoft.com/azure/active-directory/devices/hybrid-azuread-join-plan) (機器翻譯)。

Configuration Manager 提供一個用戶端設定，[自動向 Azure AD 註冊新加入 Windows 10 網域的裝置](../core/clients/deploy/about-client-settings.md#automatically-register-new-windows-10-domain-joined-devices-with-azure-active-directory)。 如需如何設定用戶端設定的詳細資訊，請參閱[如何設定用戶端設定](../core/clients/deploy/configure-client-settings.md)。

如果您想要為裝置設定 Azure AD 加入，而不要將它們加入至您的內部部署網域，請檢閱對環境中 Azure AD 加入的考量。 一旦決定使用 Azure AD 加入，即可根據組織需求利用許多選項部署。 如需詳細資訊，請參閱下列文章：

- [如何：規劃 Azure AD 加入實作](https://docs.microsoft.com/azure/active-directory/devices/azureadjoin-plan) \(機器翻譯\)  
- [了解您的佈建選項](https://docs.microsoft.com/azure/active-directory/devices/azureadjoin-plan#understand-your-provisioning-options) \(機器翻譯\)  
