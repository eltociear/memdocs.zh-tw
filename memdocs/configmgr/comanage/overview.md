---
title: Windows 10 裝置的共同管理
titleSuffix: Configuration Manager
description: 了解如何使用 Configuration Manager 和 Microsoft Intune 同時管理多部 Windows 10 裝置。
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 01/24/2020
ms.topic: overview
ms.prod: configuration-manager
ms.technology: configmgr-comanage
ms.assetid: d6bbc787-83a5-44b4-ad64-016e5da7413f
ms.openlocfilehash: 86bd566e9582c7dd7c83f93c22430edcc8ea0d0d
ms.sourcegitcommit: d498e5eceed299f009337228523d0d4be76a14c2
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/04/2020
ms.locfileid: "84347180"
---
# <a name="what-is-co-management"></a>什麼是共同管理？

<!-- 1350871 -->
共同管理是將您現有的 Configuration Manager 部署附加至 Microsoft 365 雲端其中一種主要方式。 它可協助您解除其他雲端支援功能的鎖定，例如條件式存取。

共同管理可讓您使用 Configuration Manager 與 Microsoft Intune 同時管理多部 Windows 10 裝置。 它可讓您透過加入新的功能，在雲端中附加您在 Configuration Manager 中的現有投資。 透過使用共同管理，您將能擁有使用最適合您組織之技術解決方案的彈性。

當 Windows 10 裝置具有 Configuration Manager 用戶端且註冊至 Intune 時，您便可同時取得這兩個服務的優點。 您可以控制要將哪些工作負載 (如果有) 的授權從 Configuration Manager 切換至 Intune。 Configuration Manager 會繼續管理所有其他工作負載 (包括那些沒有切換到 Intune 的工作負載)，以及共同管理不支援的所有其他 Configuration Manager 功能。

您也可以搭配個別的裝置集合對工作負載進行試驗。 試驗可讓您在切換到更大規模的裝置群組之前，先搭配一部份裝置來測試 Intune 功能。

![共同管理的概觀圖表](media/co-management-overview.svg)

[檢視完整大小的圖表](media/co-management-overview.svg)

> [!Note]  
> 當您同時使用 Configuration Manager 和 Microsoft Intune 來管理 Windows 10 裝置時，此設定被稱為「共同管理」。 當您使用 Configuration Manager 來管理裝置，並註冊至第三方 MDM 服務時，此設定被稱為「共存」。 當您針對單一裝置具備兩個管理授權單位，且沒有在兩者之間取得適當協調的情況下，可能會帶來許多挑戰性。 在使用共同管理的情況下，Configuration Manager 和 Intune 會平衡[工作負載](#workloads)，以確保不會發生衝突。 在使用第三方服務的情況下，由於此互動並不存在，使得共存具備有限的管理能力。 如需詳細資訊，請參閱[搭配 Configuration Manager 的第三方 MDM 共存](coexistence.md)。

## <a name="paths-to-co-management"></a>共同管理的路徑

連上共同管理有兩條主要路徑：  

- **現有 Configuration Manager 用戶端**：您有已經是 Configuration Manager 用戶端的 Windows 10 裝置。 您會設定混合式 Azure AD，並將它們註冊至 Intune。  

- **新網際網路型裝置**：您有已加入 Azure AD 並自動註冊至 Intune 的新 Windows 10 裝置。 您會安裝 Configuration Manager 用戶端以達到共同管理狀態。  

如需路徑的詳細資訊，請參閱[共同管理的路徑](quickstart-paths.md)。

## <a name="benefits"></a>優點

當您將現有的 Configuration Manager 用戶端註冊至共同管理時，您將能立即獲得下列價值：  

- 搭配裝置合規性的條件式存取  

- 以 Intune 為基礎的遠端動作，例如重新啟動、遠端控制或恢復出廠預設值

- 裝置健康情況的集中式可見度  

- 搭配 Azure Active Directory (Azure AD) 連結使用者、裝置與應用程式  

- 搭配 Windows Autopilot 進行新式佈建  

- 遠端動作

如需共同管理所提供之立即價值的詳細資訊，請參閱針對[搭配共同管理的雲端連線](quickstarts.md)的快速入門系列。

共同管理也可讓您針對數個工作負載搭配 Intune 進行協調。 如需詳細資訊，請參閱[工作負載](#workloads)一節。

## <a name="prerequisites"></a>先決條件

共同管理在下列領域中具有這些先決條件：

- [授權](#licensing)  
- [Configuration Manager](#configuration-manager)  
- [Azure Active Directory](#azure-ad) (Azure AD)  
- [Microsoft Intune](#intune)  
- [Windows 10](#windows-10)  
- [權限與角色](#permissions-and-roles)  

### <a name="licensing"></a>授權

- Azure AD Premium

    > [!Note]  
    > Enterprise Mobility + Security (EMS) 訂用帳戶同時包括 Azure Active Directory Premium 與 Microsoft Intune。

- 至少有一個 Intune 授權可讓您以系統管理員身分存取 Intune 入口網站。

    > [!Tip]
    > 請務必將 Intune 授權指派給您用來登入租用戶的帳戶。 否則登入將會失敗，並顯示錯誤訊息「無法辨識的使用者」。
    >
    > 您不再需要購買並指派個別的 Intune 或 EMS 授權給使用者。 如需詳細資訊，請參閱[產品與授權常見問題集](../core/understand/product-and-licensing-faq.md#bkmk_mem)。

### <a name="configuration-manager"></a>Configuration Manager

共同管理需要 Configuration Manager 1710 版或更新版本。

從 Configuration Manager 1806 版開始，您可以將多個 Configuration Manager 執行個體連線到單一 Intune 租用戶。 <!--1357944-->  

啟用共同管理本身並不需要您搭配 Azure AD 將網站上線。 針對[第二條路徑的案例](#paths-to-co-management)，網際網路型的 Configuration Manager 用戶端會需要[雲端管理閘道](../core/clients/manage/cmg/plan-cloud-management-gateway.md) (CMG)。 CMG 需要網站[已上線至 Azure AD 以進行雲端管理](../core/servers/deploy/configure/azure-services-wizard.md)。

### <a name="azure-ad"></a>Azure AD

- Windows 10 裝置必須連線至 Azure AD。 它們可以是下列任一類型：  

  - [已加入混合式 Azure AD](https://docs.microsoft.com/azure/active-directory/devices/concept-azure-ad-join-hybrid)，其中裝置已加入您的內部部署 Active Directory，並會向 Azure Active Directory 註冊。

  - 僅限[已加入 Azure AD](https://docs.microsoft.com/azure/active-directory/devices/azureadjoin-plan)。 (此類型有時稱為「已加入雲端網域」)<!--SCCMDocs issue 605-->  

### <a name="intune"></a>Intune

- [設定 Intune](https://docs.microsoft.com/intune/setup-steps)  

- [啟用 Windows 10 自動註冊](https://docs.microsoft.com/intune/windows-enroll#enable-windows-10-automatic-enrollment)  

### <a name="windows-10"></a>Windows 10

將裝置升級至 Windows 10 1709 版或更新版本。 如需詳細資訊，請參閱[採用 Windows 即服務](../core/understand/configuration-manager-and-windows-as-service.md#key-articles-about-adopting-windows-as-a-service)。

> [!IMPORTANT]
> Windows 10 行動裝置不支援共同管理。

### <a name="permissions-and-roles"></a>權限與角色

<!--SCCMDocs issue #667-->
| 動作 | 所需的角色 |
|----|----|
| 在 Configuration Manager 中設定雲端管理閘道 | Azure **訂用帳戶管理員** |
| 從 Configuration Manager 建立 Azure AD 應用程式 | Azure AD **全域管理員** |
| 在 Configuration Manager 中匯入 Azure 應用程式 | Configuration Manager **系統高權限管理員**<br>不需要其他 Azure 角色 |
| 在 Configuration Manager 中啟用共同管理 | Azure AD 使用者<br>具有**所有**範圍權限的 Configuration Manager **系統高權限管理員**。<!--SCCMDoc issue 626--> |

如需 Azure 角色的詳細資訊，請參閱[了解不同的角色](https://docs.microsoft.com/azure/role-based-access-control/rbac-and-directory-admin-roles)。

如需有關 Configuration Manager 角色的詳細資訊，請參閱[以角色為基礎之系統管理的基礎](../core/understand/fundamentals-of-role-based-administration.md)。

## <a name="workloads"></a>工作負載

您不需要切換工作負載，您也可以在準備好時再個別切換它們。 Configuration Manager 會繼續管理所有其他工作負載 (包括那些沒有切換到 Intune 的工作負載)，以及共同管理不支援的所有其他 Configuration Manager 功能。

共同管理支援下列工作負載：

- 相容性原則  

- Windows Update 原則  

- 資源存取原則  

- Endpoint Protection  

- 裝置設定  

- Office 隨選即用應用程式  

- 用戶端應用程式  

如需詳細資訊，請參閱[工作負載](workloads.md)。

## <a name="monitor-co-management"></a>監視共同管理

共同管理儀表板可協助您檢閱在環境中被共同管理的電腦。 圖形有助於識別可能需要注意的裝置。

![共同管理儀表板的螢幕擷取畫面](media/co-management-dashboard.png)

如需詳細資訊，請參閱[如何監視共同管理](how-to-monitor.md)。

## <a name="next-steps"></a>後續步驟

- [深入了解立即價值並開始使用共同管理](quickstarts.md)  

- [教學課程：針對現有 Configuration Manager 用戶端啟用共同管理](tutorial-co-manage-clients.md)  
