---
title: 教學課程：啟用現有用戶端的共同管理
titleSuffix: Configuration Manager
description: 在您已使用 Configuration Manager 管理 Windows 10 裝置的情況下，搭配 Microsoft Intune 設定共同管理。
ms.date: 03/12/2020
ms.prod: configuration-manager
ms.technology: configmgr-comanage
ms.topic: tutorial
ms.assetid: 140c522f-d09a-40b6-a4b0-e0d14742834a
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 918df2cded3fad48352fff6a2617b1133540c0eb
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81692576"
---
# <a name="tutorial-enable-co-management-for-existing-configuration-manager-clients"></a>教學課程：針對現有 Configuration Manager 用戶端啟用共同管理

藉由共同管理，您將可保有已妥善建立的程序，以使用 Configuration Manager 來管理您組織中的電腦。 同時，您也會使用 Intune 來投資雲端，以取得安全性和現代化佈建。  

在此教學課程中，您會針對已註冊於 Configuration Manager 中的 Windows 10 裝置設定共同管理。 此教學課程會以您已經使用 Configuration Manager 來管理 Windows 10 裝置作為前提。

在下列情況下，請使用此教學課程：  

- 您已經具有內部部署 Active Directory，並可以混合式 Azure AD 設定的形式將它連線至 Azure Active Directory (Azure AD)。

  如果您無法部署能聯結內部部署 AD 與 Azure AD 的混合式 Azure Active Directory (AD)，建議您遵循我們隨附的教學課程：[為新的網際網路型 Windows 10 裝置啟用共同管理](tutorial-co-manage-new-devices.md)。
- 您有想要連線到雲端的現有 Configuration Manager 用戶端。

**在此教學課程中，您將會：**  
> [!div class="checklist"]
> * 檢閱 Azure 和您內部部署環境的先決條件
> * 設定混合式 Azure AD  
> * 設定 Configuration Manager 用戶端代理程式以向 Azure AD 註冊  
> * 設定 Intune 以自動註冊裝置  
> * 在 Configuration Manager 中啟用共同管理  

## <a name="prerequisites"></a>先決條件  

### <a name="azure-services-and-environment"></a>Azure 服務和環境

- Azure 訂用帳戶 ([免費試用](https://azure.microsoft.com/free))
- Azure Active Directory Premium
- Microsoft Intune 訂閱
  > [!TIP]  
  > Enterprise Mobility + Security (EMS) 訂用帳戶同時包括 Azure Active Directory Premium 和 Microsoft Intune。 EMS 訂用帳戶 ([免費試用](https://www.microsoft.com/cloud-platform/enterprise-mobility-security-trial))。  

如果其尚未存在於您的環境，在此教學課程期間您將會：

- 在您的內部部署 Active Directory 與 Azure Active Directory (AD) 租用戶之間設定 [Azure AD Connect](https://docs.microsoft.com/azure/active-directory/hybrid/how-to-connect-install-select-installation) \(部分機器翻譯\)。

> [!TIP]
> 您不再需要購買並指派個別的 Intune 或 EMS 授權給使用者。 如需詳細資訊，請參閱[產品與授權常見問題集](../core/understand/product-and-licensing-faq.md#bkmk_mem)。

### <a name="on-premises-infrastructure"></a>內部部署基礎結構

- Configuration Manager 最新分支的[支援版本](../core/servers/manage/updates.md#supported-versions)
- 行動裝置管理 (MDM) 授權單位必須設定為 Intune。  

### <a name="permissions"></a>權限

在此教學課程的整個過程中，請使用下列權限來完成工作：

- 在 Azure Active Directory (Azure AD) 中為「全域管理員」  帳戶 
- 在您內部部署基礎結構上為「網域管理員」  的帳戶  
- 在 Configuration Manager 中為「所有」  範圍之「系統高權限管理員」  的帳戶

## <a name="set-up-hybrid-azure-ad"></a>設定混合式 Azure AD

當您設定混合式 Azure AD 時，您實際上是使用 Azure AD Connect 和 Active Directory Federated Services (ADFS) 設定內部部署 AD 與 Azure AD 的整合。 設定成功之後，您的員工便能使用其內部部署 AD 認證順暢地登入外部系統。

> [!IMPORTANT]  
> 此教學課程會詳述針對受控網域設定混合式 Azure AD 的極簡程序。 我們建議您熟悉該程序，且不要仰賴此教學課程作為了解及部署混合式 Azure AD 的指南。
>
> 如需混合式 Azure AD 的詳細資訊，請以下列來自 Azure Active Directory 文件中的文章作為開始：
>
> - [規劃 Azure AD Join 實作](https://docs.microsoft.com/azure/active-directory/devices/azureadjoin-plan)
> - [規劃混合式 Azure AD Join 實作](https://docs.microsoft.com/azure/active-directory/devices/hybrid-azuread-join-plan)
> - [控制裝置的混合式 Azure AD Join](https://docs.microsoft.com/azure/active-directory/devices/hybrid-azuread-join-control)
> - [設定適用於同盟網域的混合式 Azure AD Join](https://docs.microsoft.com/azure/active-directory/devices/hybrid-azuread-join-federated-domains)  

### <a name="set-up-azure-ad-connect"></a>設定 Azure AD Connect

混合式 Azure AD 需要設定 Azure AD Connect，以確保內部部署 Active Directory (AD) 中的電腦帳戶以及 Azure AD 中的裝置物件能保持同步。

從 1.1.819.0 版開始，Azure AD Connect 能提供設定混合式 Azure AD Join 的精靈。 使用該精靈將能簡化設定程序。  

若要設定 Azure AD Connect，則需要 Azure AD 的全域系統管理員認證。  

> [!TIP]  
> 下列程序不應該被當作設定 Azure AD Connect 的正當作法，在此提供它的原因是為了協助簡化 Intune 和 Configuration Manager 之間的共同管理設定。 如需此主題的正當內容，以及設定 Azure AD 的相關程序，請參閱 Azure AD 文件中的[設定適用於受控網域的混合式 Azure AD Join](https://docs.microsoft.com/azure/active-directory/devices/hybrid-azuread-join-managed-domains)。  

#### <a name="configure-a-hybrid-azure-ad-join-using-azure-ad-connect"></a>使用 Azure AD Connect 設定混合式 Azure AD Join

1. 取得並安裝[最新版本的 Azure AD Connect](https://www.microsoft.com/download/details.aspx?id=47594) \(英文\) (1.1.819.0 或更高版本)。  
2. 啟動 Azure AD Connect，然後選取 [設定]  。
3. 在 [其他工作]  頁面上，選取 [設定裝置選項]  ，然後選取 [下一步]  。
4. 在 [概觀]  頁面上，選取 [下一步]  。
5. 在 [連線到 Azure AD]  頁面中，輸入 Azure AD 的全域系統管理員認證。
6. 在 [裝置選項]  頁面上，選取 [設定混合式 Azure AD Join]  ，然後選取 [下一步]  。
7. 在 [裝置作業系統]  頁面上，選取您 Active Directory 環境中裝置所使用的作業系統，然後選取 [下一步]  。  

   您可以選取支援 Windows 舊版已加入網域裝置的選項，但請牢記裝置的共同管理僅支援 Windows 10。
8. 在 [SCP]  頁面上，針對您想要 Azure AD Connect 設定服務連接點 (SCP) 的每個內部部署樹系執行下列步驟，然後選取 [下一步]  ：  
   1. 選取樹系。  
   2. 選取驗證服務。  如果您有同盟的網域，請選取 AD FS 伺服器，除非您的組織只具有 Windows 10 用戶端且您已設定電腦/裝置同步，或是您的組織是使用 [SeamlessSSO](https://docs.microsoft.com/azure/active-directory/hybrid/how-to-connect-sso)。  
   3. 按一下 [新增]  以輸入企業系統管理員認證。  
9. 如果您有受控網域，請略過此步驟。  

   在 [同盟設定]  頁面上，輸入 AD FS 系統管理員的認證，然後選取 [下一步]  。
10. 在 [準備設定]  頁面上，選取 [設定]  。
11. 在 [設定完成]  頁面上，選取 [結束]  。

如果您在針對已加入網域的 Windows 裝置完成混合式 Azure AD Join 時遇到問題，請參閱[針對 Windows 目前裝置進行混合式 Azure AD Join 的疑難排解](https://docs.microsoft.com/azure/active-directory/devices/troubleshoot-hybrid-join-windows-current)。

## <a name="configure-client-settings-to-direct-clients-to-register-with-azure-ad"></a>設定 [用戶端設定] 指示用戶端向 Azure AD 註冊

使用 [用戶端設定] 來設定讓 Configuration Manager 用戶端自動向 Azure AD 註冊。  

1. 開啟 [Configuration Manager 主控台]   > [系統管理]   > [概觀]   > [用戶端設定]  ，然後編輯 [預設用戶端設定]  。  

2. 選取 [雲端服務]  。  

3. 在 [預設設定]  頁面上，將 [自動向 Azure Active Directory 註冊新加入 Windows 10 網域的裝置]  設定為 [是]  。  

4. 按一下 [確定]  儲存這項設定。  

## <a name="configure-auto-enrollment-of-devices-to-intune"></a>設定針對 Intune 自動註冊裝置

接下來，我們將搭配 Intune 設定裝置自動註冊。 透過自動註冊，您使用 Configuration Manager 管理的裝置都會自動向 Intune 註冊。

自動註冊也能讓使用者向 Intune 註冊其 Windows 10 裝置。 裝置會在使用者將其公司帳戶新增到其個人擁有的裝置，或在公司擁有的裝置加入 Azure Active Directory 時註冊。  

1. 登入 [Azure 入口網站](https://portal.azure.com/)，然後選取 [Azure Active Directory]   > [行動性 (MDM 與 MAM)]   > [Microsoft Intune]  。  

2. 設定 [MDM 使用者範圍]  。 指定下列其中一個，以設定有哪些使用者的裝置是由 Microsoft Intune 管理，然後接受 URL 值的預設值。  

   - **部分**：選取可以自動註冊其 Windows 10 裝置的 [群組]   

   - **全部**：所有使用者都可以自動註冊其 Windows 10 裝置

   - **無**：停用 MDM 自動註冊

   > [!IMPORTANT]  
   > 如果同時針對某個群組啟用 [MAM 使用者範圍]  和自動 MDM 註冊 ([MDM 使用者範圍]  )，則只會啟用 MAM。 當該群組中的使用者將個人裝置加入工作場所網路時，系統只會針對他們新增行動應用程式管理 (MAM)。 裝置不會自動進行 MDM 註冊。  

3. 選取 [儲存]  以完成自動註冊的設定。  

4. 返回 [行動性 (MDM 與 MAM)]  並選取 [Microsoft Intune 註冊]  。  

    > [!NOTE]
    > 某些租用戶可能無法設定這些選項。<!-- SCCMDocs#1230 -->
    >
    > **Microsoft Intune** 是為 Azure AD 設定 MDM 應用程式的方式。 **Microsoft Intune 註冊**是當針對 iOS 和 Android 註冊套用多重要素驗證原則時所建立的特定 Azure AD 應用程式。 如需詳細資訊，請參閱[需要 Intune 裝置註冊的多重要素驗證](https://docs.microsoft.com/intune/enrollment/multi-factor-authentication) (英文)。

5. 針對 MDM 使用者範圍，請選取 [全部]  ，然後選取 [儲存]  。  

## <a name="enable-co-management-in-configuration-manager"></a>在 Configuration Manager 中啟用共同管理

設定混合式 Azure AD 並備妥 Configuration Manager 用戶端設定之後，您便已準備好啟用 Windows 10 裝置的共同管理。  

> [!TIP]
> - 當您啟用共同管理時，將會指派一個集合作為「試驗群組」  。 這是一個包含少量用戶端的群組，以用來測試共同管理設定。 建議您先建立一個適當的集合，再開始進行此程序。 如此一來，您無需結束此程序，即可選取該集合。
> - 從 Configuration Manager 1906 版開始，您可能需要多個集合，因為您可以為每個工作負載指派不同的「試驗群組」  。

### <a name="enable-co-management-starting-in-version-1906"></a>從 1906 版開始啟用共同管理

若要從 Configuration Manager 1906 版開始啟用共同管理，請遵循下列指示：

[!INCLUDE [Enable Co-management in version 1906 and later](includes/enable-co-management-1906-and-higher.md)]

### <a name="enable-co-management-in-version-1902-and-earlier"></a>在 1902 版和更早版本中啟用共同管理

若要針對 Configuration Manager 1902 版和更早版本啟用共同管理，請遵循下列指示：

[!INCLUDE [Enable Co-management in version 1902 and earlier](includes/enable-co-management-1902-and-earlier.md)]

## <a name="next-steps"></a>後續步驟

- 使用[共同管理儀表板](how-to-monitor.md)來檢閱共同管理裝置的狀態
- 開始從共同管理取得[立即性的價值](quickstarts.md#immediate-value)
- 使用[條件式存取](quickstart-conditional-access.md)和 Intune 合規性規則來管理使用者對公司資源的存取
