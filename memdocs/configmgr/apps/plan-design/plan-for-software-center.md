---
title: 針對軟體中心進行規劃
titleSuffix: Configuration Manager
description: 決定要如何對軟體中心進行設定並設定其商標，來讓使用者與 Configuration Manager 互動。
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: c6826794-aa19-469d-ae47-1a0db68a1ff1
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 15da90b12504fdaf7a4dd0a36704391eead877cd
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81689026"
---
# <a name="plan-for-software-center"></a>針對軟體中心進行規劃

適用於：  Configuration Manager (最新分支)

使用者會從軟體中心變更設定、瀏覽應用程式，以及安裝應用程式。 當您在 Windows 裝置上安裝 Configuration Manager 用戶端時，它也會自動安裝軟體中心。

如需軟體中心其他功能的詳細資訊，請參閱[軟體中心使用者指南](../../core/understand/software-center.md)。  

## <a name="configure-software-center"></a><a name="bkmk_userex"></a> 設定軟體中心  

將 Configuration Manager 站台與用戶端更新至 1906 版或更新版本，以體驗最新的功能改善。

請檢閱下列對於軟體中心的改進：

> [!Important]  
> 這些軟體中心和管理點的反覆式改善是為了淘汰應用程式類別目錄角色。
>
> - 最新分支版本 1806 不支援 Silverlight 使用者體驗。
> - 從 1906 版開始，已更新的用戶端會自動使用適用於使用者可用應用程式部署的管理點。 此外，您也無法安裝新的應用程式目錄角色。
> - 1910 版會終止對應用程式類別目錄角色的支援。  

### <a name="starting-in-version-1802"></a>從 1802 版開始

- 預設會在 [電腦代理程式]  群組中啟用 [使用新的軟體中心]  用戶端設定。 不再支援舊版軟體中心。 如需詳細資訊，請參閱[已移除和已淘汰的功能](../../core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures.md)。  

- 使用者可以在已加入 Azure Active Directory (Azure AD) 的裝置上，瀏覽和安裝使用者可用的應用程式。 如需詳細資訊，請參閱[在已加入 Azure AD 的裝置上部署使用者可用的應用程式](../deploy-use/deploy-applications.md#deploy-user-available-applications-on-azure-ad-joined-devices)。  

### <a name="starting-in-version-1806"></a>從 1806 版開始

- 指定是否要在軟體中心的 [安裝狀態]  索引標籤上顯示應用程式類別目錄網站連結。 如需詳細資訊，請參閱[軟體中心](../../core/clients/deploy/about-client-settings.md#software-center)用戶端設定。  

- 不再需要應用程式類別目錄角色，就能在軟體中心顯示使用者可用的應用程式。 這項變更可協助您減少將應用程式傳遞給使用者所需的伺服器基礎結構。 軟體中心現在依賴管理點來取得這項資訊，這可透過將更大型的環境指派給[界限群組](../../core/servers/deploy/configure/boundary-groups.md#management-points)，協助這些環境更適當地調整大小。<!--1358309-->  

    > [!Note]  
    > 如果您目前正在使用應用程式類別目錄，並將 Configuration Manager 更新為 1806 版，則它會繼續運作。 不再「需要」  但仍「支援」  應用程式類別目錄網站點和 Web 服務點角色。 不再支援應用程式類別目錄「網站點」  的 **Silverlight 使用者體驗**。 如需詳細資訊，請參閱[已移除和已淘汰的功能](../../core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures.md)。
    >
    > 開始規劃未來要從您的基礎結構移除的應用程式類別目錄角色。 充分利用軟體中心的改進來使用管理點，並簡化您的 Configuration Manager 環境。  

### <a name="starting-in-version-1902"></a>從 1902 版開始

- 設定使用者裝置親和性。 如需詳細資訊，請參閱[透過使用者裝置親和性連結使用者和裝置](../deploy-use/link-users-and-devices-with-user-device-affinity.md)。

### <a name="starting-in-version-1906"></a>從 1906 版開始

- 軟體中心現在會與使用者可使用之目標應用程式的管理點通訊。 它不會再使用應用程式類別目錄。 這項變更可讓您更輕鬆地從站台中移除應用程式類別目錄。

- 先前，軟體中心會從可用伺服器清單中挑選第一個管理點。 從此版本開始，它會使用用戶端所使用的相同管理點。 這項變更允許軟體中心從指派的主要站台，使用與用戶端所使用的相同的管理點。

- 管理點具有軟體中心端點，可支援這些新功能。 管理點現在每隔五分鐘就會檢查這些端點的健全狀況。 它會透過 SMS_MP_CONTROL_MANAGER 站台元件的狀態訊息報告任何問題。

- 您無法將新的應用程式類別目錄角色新增至站台。 現有的角色會繼續工作。 只有現有用戶端會使用應用程式類別目錄來進行使用者可用的部署。 已更新用戶端會自動使用所有部署的管理點。

- 您最多可以將 5 個自訂索引標籤新增至軟體中心。 如需詳細資訊，請參閱[軟體中心用戶端設定](../../core/clients/deploy/about-client-settings.md#software-center)。 <!--4063773-->

### <a name="summary-of-infrastructure-requirements-per-version"></a>每個版本的基礎結構需求摘要

使用下表，協助您根據特定版本的 Configuration Manager 了解軟體中心需求：

| 裝置類型 | 站台版本 | 基礎結構 |
|-----------------|--------------|----------------|
| 已加入 Azure AD 的裝置<br>(或「已加入雲端網域」) | 1802 或 1806 | 適用於所有應用程式部署的管理點 |
| 網際網路上[已加入 Azure AD 的混合式](https://docs.microsoft.com/azure/active-directory/device-management-hybrid-azuread-joined-devices-setup)裝置 | 1802 或 1806 | 適用於所有應用程式部署的雲端管理閘道和管理點 |
| 已加入 Active Directory 網域的內部部署裝置 | 1802 | 透過軟體中心提供使用者可用應用程式所需的應用程式類別目錄 |
| 已加入 Active Directory 網域的內部部署裝置 | 1806 | 適用於所有應用程式部署的管理點 |

> [!Important]  
> 若要利用 Configuration Manager 的新功能，請先將用戶端更新為最新版本。 雖然當您更新主控台和站台時，Configuration Manager 主控台中會出現新功能，但要等到用戶端版本也是最新版，才能完整運作。


## <a name="replace-toast-notifications-with-dialog-window"></a><a name="bkmk_impact"></a> 以對話視窗取代快顯通知

<!--3555947-->
有時使用者會看不到有關重新啟動或必要部署的 Windows 快顯通知。 然後他們就會看不到可將提醒延遲的體驗。 此行為可能導致在用戶端達到期限時，使用者無法獲得良好的體驗。

從 1902 版開始，當[需要進行軟體變更](#software-changes-are-required)或[需要重新啟動](#restart-required)部署時，您可以選擇使用更具提示效果的對話視窗。

### <a name="software-changes-are-required"></a>需要軟體變更

當您基於未來期限的需求而[部署應用程式](../deploy-use/deploy-applications.md)時，請在 [部署軟體精靈] 的 [使用者體驗]  頁面上選取下列使用者通知選項：

- **顯示在軟體中心中並顯示所有通知**
- **必須進行軟體變更時，將對使用者顯示快顯通知改為顯示對話視窗**

設定此部署設定會變更此案例的使用者體驗。

從下列快顯通知：

![[需要軟體變更] 的快顯通知](media/3555947-required-toast.png)  

變更為下對話視窗：

![[需要軟體變更] 的對話視窗](media/3555947-required-dialog.png)


### <a name="restart-required"></a>需要重新啟動

在用戶端設定的[電腦重新啟動](../../core/clients/deploy/about-client-settings.md#computer-restart)群組中，啟用下列選項：[部署必須重新啟動時，將對使用者顯示快顯通知改為顯示對話視窗]  。  

設定此用戶端設定會將所有需要下列重新啟動類型之所有必要部署的使用者體驗：

- [應用程式](../deploy-use/deploy-applications.md)
- [工作順序](../../osd/deploy-use/manage-task-sequences-to-automate-tasks.md#BKMK_DeployTS)
- [軟體更新](../../sum/deploy-use/deploy-software-updates.md)

從下列快顯通知：

![[需要重新啟動] 的快顯通知](media/3555947-restart-toast.png)  

變更為下對話視窗：

![[重新啟動您的電腦] 的對話視窗](media/3555947-restart-dialog.png)

> [!IMPORTANT]
> 在 Configuration Manager 1902 中，在某些情況下，對話方塊將不會取代快顯通知。 若要解決此問題，請安裝 [Configuration Manager 1902 的更新彙總套件](https://support.microsoft.com/help/4500571/update-rollup-for-configuration-manager-current-branch-1902)。 <!--4404715-->

## <a name="branding-software-center"></a>設定軟體中心商標

變更軟體中心的外觀，使其符合貴組織的商標需求。 此設定有助於讓使用者信任軟體中心。

### <a name="configure-software-center-branding"></a>設定軟體中心商標

<!-- 1351224 -->
新增組織的商標元素並指定要顯示的索引標籤，藉以自訂軟體中心的外觀。

如需詳細資訊，請參閱下列文章：

- 用戶端設定的[軟體中心](../../core/clients/deploy/about-client-settings.md#software-center)群組  
- [如何設定用戶端設定](../../core/clients/deploy/configure-client-settings.md)  

### <a name="branding-priorities"></a>商標優先順序

Configuration Manager 會根據下列優先順序來套用軟體中心的自訂商標：  

1. [軟體中心]  用戶端設定。 如需詳細資訊，請參閱[關於用戶端設定](../../core/clients/deploy/about-client-settings.md#software-center)。  

2. [電腦代理程式]  群組中的 [組織名稱]  用戶端設定。 如需詳細資訊，請參閱[關於用戶端設定](../../core/clients/deploy/about-client-settings.md#computer-agent)。  

#### <a name="application-catalog-branding-priorities"></a>應用程式類別目錄商標優先順序

> [!Important]
> 從 1806 最新分支版本開始即不支援應用程式類別目錄的 Silverlight 使用者體驗。 從 1906 版開始，已更新的用戶端會自動使用適用於使用者可用應用程式部署的管理點。 此外，您也無法安裝新的應用程式目錄角色。 1910 版會終止對應用程式類別目錄角色的支援。  

如果您使用應用程式類別目錄，則商標會遵循下列優先順序：  

1. [軟體中心]  用戶端設定。 如需詳細資訊，請參閱[關於用戶端設定](../../core/clients/deploy/about-client-settings.md#software-center)。  

2. 您在應用程式類別目錄網站點內容中指定的「組織名稱」  和「色彩」  。 如需詳細資訊，請參閱[應用程式類別目錄網站點的設定選項](../../core/servers/deploy/configure/configuration-options-for-site-system-roles.md#BKMK_ApplicationCatalog_Website)。  

3. [電腦代理程式]  群組中的 [組織名稱]  用戶端設定。 如需詳細資訊，請參閱[關於用戶端設定](../../core/clients/deploy/about-client-settings.md#computer-agent)。  


## <a name="see-also"></a>請參閱

- [軟體中心使用者指南](../../core/understand/software-center.md)
- [規劃和設定應用程式管理](plan-for-and-configure-application-management.md)
