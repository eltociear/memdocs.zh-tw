---
title: 使用 Azure AD 安裝用戶端
titleSuffix: Configuration Manager
description: 在使用 Azure Active Directory 進行驗證的 Windows 10 裝置上安裝及指派設定管理員用戶端
ms.date: 06/03/2020
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: a44006eb-8650-49f6-94e1-18fa0ca959ee
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 39d6bf22cb24492a0f4e3f59313184ce522b5d09
ms.sourcegitcommit: 0b30c8eb2f5ec2d60661a5e6055fdca8705b4e36
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/05/2020
ms.locfileid: "84454999"
---
# <a name="install-and-assign-configuration-manager-windows-10-clients-using-azure-ad-for-authentication"></a>安裝並指派 Configuration Manager Windows 10 用戶端，並使用 Azure AD 進行驗證

若要在使用 Azure AD 驗證的 Windows 10 裝置上安裝設定管理員用戶端，請整合設定管理員與 Azure Active Directory (Azure AD)。 用戶端可以在內部網路上，直接與已啟用 HTTPS 管理點或啟用增強 HTTP 之站台中的任何管理點進行通訊。 也可以是透過 CMG 或使用網際網路型管理點的網際網路型通訊。 這個程序會使用 Azure AD 向 Configuration Manager 站台驗證用戶端。 Azure AD 能取代設定及使用用戶端驗證憑證的需求。

對於某些客戶而言，為憑證型驗證設定公開金鑰基礎結構可能更容易設定 Azure AD。 有功能要求您讓 Azure AD 站台上線，但不一定會要求用戶端加入 Azure AD。<!-- SCCMDocs issue 1259 --> 如需詳細資訊，請參閱下列文章：

- [規劃 Azure Active Directory](../../plan-design/security/plan-for-security.md#bkmk_planazuread)
- [使用 Azure AD 進行共同管理](../../../comanage/quickstart-hybrid-aad.md)

## <a name="before-you-begin"></a>開始之前

- Azure AD 租用戶為必要條件  

- 裝置需求：  

  - Windows 10  

  - 加入 Azure AD，加入單純雲端網域或加入混合式 Azure AD  

- 使用者需求：  

  - 登入的使用者必須是 Azure AD 身分識別。

  - 如果使用者是同盟或同步處理身分識別，請設定 Configuration Manager [Active Directory 使用者探索](../../servers/deploy/configure/about-discovery-methods.md#bkmk_aboutUser)與 [Azure AD 使用者探索](../../servers/deploy/configure/about-discovery-methods.md#azureaddisc)。 如需混合式身分識別的詳細資訊，請參閱[定義混合式身分識別採用策略](https://docs.microsoft.com/azure/active-directory/hybrid/plan-hybrid-identity-design-considerations-identity-adoption-strategy)。<!--497750-->

- 除了管理點站台系統角色的[現有必要條件](../../plan-design/configs/site-and-site-system-prerequisites.md#bkmk_2012MPpreq)之外，也要在這部伺服器上啟用 **ASP.NET 4.5**。 包括在啟用 ASP.NET 4.5 時會自動選取的其他任何選項。  

- 判斷您的管理點是否需要 HTTPS。 如需詳細資訊，請參閱[啟用 HTTPS 的管理點](../manage/cmg/certificates-for-cloud-management-gateway.md#bkmk_mphttps)。  

- 選擇性設定[雲端管理閘道](../manage/cmg/plan-cloud-management-gateway.md) (CMG) 來部署以網際網路為基礎的用戶端。 針對使用 Azure AD 進行驗證的內部部署用戶端，您不需要 CMG。  

> [!TIP]
> 從 2002 版開始，<!--5686290--> Configuration Manager 已可支援不常連線至內部網路、無法加入 Azure Active Directory (Azure AD)，且沒有方法可安裝 PKI 發行憑證等的裝置。 如需詳細資訊，請參閱 [CMG 的權杖型驗證](deploy-clients-cmg-token.md)。

## <a name="configure-azure-services-for-cloud-management"></a>設定 Azure 服務以進行雲端管理

第一個步驟是將您的 Configuration Manager 站台連線到 Azure AD。 如需此程序的詳細資訊，請參閱[設定 Azure 服務](../../servers/deploy/configure/azure-services-wizard.md)。 建立與**雲端管理**服務的連線。

在**雲端管理**上線時啟用 [Azure AD 使用者探索](../../servers/deploy/configure/configure-discovery-methods.md#azureaadisc)。

完成這些動作之後，您的 Configuration Manager 站台就會連線到 Azure AD。

## <a name="configure-client-settings"></a>設定用戶端設定

這些用戶端設定可協助將 Windows 10 裝置設定為混合式加入。 它們也可以啟用以網際網路為基礎的用戶端，來使用 CMG 和雲端發佈點。

1. 在 [雲端服務] 群組中設定下列用戶端設定。 如需詳細資訊，請參閱[如何設定用戶端設定](configure-client-settings.md)。

    - **允許存取雲端發佈點**：啟用此設定來協助網際網路型裝置取得安裝設定管理員用戶端的必要內容。 如果無法從雲端發佈點取得內容，裝置可以從 CMG 擷取內容。 用戶端安裝啟動程序會在容錯回復到 CMG 之前，重試雲端發佈點四個小時。<!--495533-->  

    - **自動以 Azure Active Directory 註冊已加入新 Windows 10 網域的裝置**：設定為 [是] 或 [否]。 預設值為 [是]。 這個行為也是 Windows 10 1709 版的預設值。

        > [!TIP]
        > 混合式加入裝置會加入內部部署 Active Directory 網域，並向 Azure AD 註冊。 如需詳細資訊，請參閱[混合式 Azure AD 加入裝置](https://docs.microsoft.com/azure/active-directory/devices/concept-azure-ad-join-hybrid) \(部分機器翻譯\)。<!-- MEMDocs#325 -->

    - **允許用戶端使用雲端管理閘道**：設定為 [是] (預設值)，或 [否]。  

2. 將用戶端設定部署至所需的裝置集合。 不要將這些設定部署到使用者集合。

若要確認裝置為混合式加入，請在命令提示字元中執行 `dsregcmd.exe /status`。 如果裝置已加入 Azure AD 或為混合式加入，結果中的 **AzureAdjoined** 欄位會顯示**是**。 如需詳細資訊，請參閱 [dsregcmd 命令 - 裝置狀態](https://docs.microsoft.com/azure/active-directory/devices/troubleshoot-device-dsregcmd) \(部分機器翻譯\)。

## <a name="install-and-register-the-client-using-azure-ad-identity"></a>使用 Azure AD 身分識別安裝及註冊用戶端

若要使用 Azure AD 身分識別來手動安裝用戶端，首先請檢閱[如何手動安裝用戶端](deploy-clients-to-windows-computers.md#BKMK_Manual)上的一般流程。

> [!Note]  
> 裝置需要網際網路的存取權才能夠與 Azure AD 連絡，但是不需要是以網際網路為基礎。

以下範例示範命令列的一般結構：`ccmsetup.exe /mp:<source management point> CCMHOSTNAME=<internet-based management point> SMSSiteCode=<site code> SMSMP=<initial management point> AADTENANTID=<Azure AD tenant identifier> AADCLIENTAPPID=<Azure AD client app identifier> AADRESOURCEURI=<Azure AD server app identifier>`

如需詳細資訊，請參閱[用戶端安裝屬性](about-client-installation-properties.md)。

視案例而定， **/mp** 參數和 **CCMHOSTNAME** 屬性會指定下列其中一項：

- 內部部署管理點。 僅指定 **/mp** 參數。 不需要 **CCMHOSTNAME** 屬性。
- 雲端管理閘道
- 以網際網路為基礎的管理點

**SMSMP** 屬性會指定內部部署管理點。 這不是必要項目。 建議已加入 Azure AD 且漫遊至內部網路的裝置使用，讓其可以找到內部部署管理點。

這個範例使用雲端管理閘道。 其會取代範例值：`ccmsetup.exe /mp:https://CONTOSO.CLOUDAPP.NET/CCM_Proxy_MutualAuth/72186325152220500 CCMHOSTNAME=CONTOSO.CLOUDAPP.NET/CCM_Proxy_MutualAuth/72186325152220500 SMSSiteCode=ABC SMSMP=https://mp1.contoso.com AADTENANTID=daf4a1c2-3a0c-401b-966f-0b855d3abd1a AADCLIENTAPPID=7506ee10-f7ec-415a-b415-cd3d58790d97 AADRESOURCEURI=https://contososerver`

此站台會將額外的 Azure AD 資訊發佈至雲端管理閘道 (CMG)。 已加入 Azure AD 的用戶端會在 ccmsetup 過程中從 CMG 取得此資訊 (使用它所加入的同一租用戶)。 在具有多個 Azure AD 租用戶的環境中，此行為可進一步簡化用戶端安裝作業。 唯二必要的 ccmsetup 屬性分別為 **CCMHOSTNAME** 和 **SMSSiteCode**。<!--3607731-->

若要使用 Azure AD 身分識別，透過 Microsoft Intune 將用戶端安裝自動化，請參閱[如何準備網路型裝置進行共同管理](../../../comanage/how-to-prepare-Win10.md#install-the-configuration-manager-client)。

## <a name="next-steps"></a>後續步驟

完成後，您可以繼續[監視及管理用戶端](../manage/monitor-clients.md)。
