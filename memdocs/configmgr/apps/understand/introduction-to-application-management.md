---
title: 應用程式管理簡介
titleSuffix: Configuration Manager
description: 探索在 Configuration Manager 中管理和部署應用程式所需的基本資訊。
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 08f711ba-83bf-4b5f-9520-a0778c6ae7eb
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: d3cd21fe4b1d53ecbb0bc60818405cb795a4f289
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81690216"
---
# <a name="introduction-to-application-management-in-configuration-manager"></a>介紹 Configuration Manager 中的應用程式管理

適用於：  Configuration Manager (最新分支)

在本文中，您將了解基本概念，再開始使用 Configuration Manager 應用程式。  

> [!TIP]  
> 如果您已熟悉如何在 Configuration Manager 中管理應用程式，請略過本文。 繼續建立範例應用程式：[建立和部署應用程式](../get-started/create-and-deploy-an-application.md)。  

## <a name="what-is-an-application"></a>何謂應用程式？

雖然「應用程式」  或 app  是電腦中廣泛使用的術語，但是在 Configuration Manager 中有特定的意義。 請將應用程式視為一個盒子。 這個盒子包含軟體套件的一或多組安裝檔 (稱為 *部署類型*)，以及軟體部署方式的指示。  

當您將應用程式部署至裝置時，**需求**決定 Configuration Manager 在裝置上安裝的部署類型。  

您可以使用應用程式完成更多工作。 透過閱讀本指南，您將會了解這些事項。 下列各節介紹您在深入探索之前需要知道的一些概念：  

### <a name="deployment-type"></a>部署類型

如果「應用程式」  是方塊，則「部署類型」  是方塊中的內容集。 應用程式需要至少一種部署類型，因為它會決定如何安裝應用程式。 若要為相同的應用程式設定不同的內容和安裝程式，請使用多種部署類型。

例如，您的公司具有一個企業營運系統應用程式，稱為 Astoria。 應用程式開發人員提供下列方法來安裝應用程式：

- Windows Installer 套件，以取得 Windows 10 裝置上的完整功能
- App-V 套件，以用於終端機伺服器陣列
- 適用於行動使用者的 Web 應用程式  

您可以在 Configuration Manager 中為 Astoria 建立單一應用程式。 此應用程式會定義有關所有安裝方法與平台共通之應用程式的高階中繼資料。 然後，您可以針對可用的安裝方法建立三種部署類型，並將應用程式部署給所有使用者。 Configuration Manager 會根據部署類型的相關需求和其他設定，決定每個使用案例的正確方法。

如需詳細資訊，請參閱[建立應用程式的部署類型](../deploy-use/create-applications.md#bkmk_create-dt)。

### <a name="requirements"></a>需求

在舊版的 Configuration Manager 中，您會建立要部署應用程式的目標裝置集合。 雖然您仍然可以建立集合，但使用「需求」  可為應用程式部署指定更詳細的準則。

例如，指定應用程式只能安裝在執行 Windows 10 的裝置上。 當您將應用程式部署至您所有的裝置時，它就只會安裝在執行 Windows 10 的裝置上。

Configuration Manager 會評估需求，以判斷是否要安裝應用程式及其任何部署類型。 然後會判斷可套用來安裝應用程式的正確部署類型。 根據預設，Configuration Manager 用戶端會每 7 天根據用戶端設定 [排程部署的重新評估]  重新評估需求規則，確保其合規性。

如需詳細資訊，請參閱[建立和部署應用程式](../get-started/create-and-deploy-an-application.md)及[部署類型需求](../deploy-use/create-applications.md#bkmk_dt-require)。

### <a name="global-conditions"></a>全域條件

雖然您會搭配單一應用程式中的特定部署類型來使用需求，但您也可以建立「全域條件」  。 這些條件是預先定義的需求庫，您可以與任何應用程式和部署類型搭配使用。 Configuration Manager 包含一組內建全域條件，或者您可以建立專屬的全域條件。

如需詳細資訊，請參閱[建立全域條件](../deploy-use/create-global-conditions.md)。

### <a name="simulated-deployment"></a>模擬部署

「模擬部署」  會評估應用程式的需求、偵測方法及相依性。 用戶端會報告結果，而不會實際安裝應用程式。

如需詳細資訊，請參閱[模擬應用程式部署](../deploy-use/simulate-application-deployments.md)。  

### <a name="deployment-action"></a>部署動作

「部署動作」  指定要安裝或解除安裝正在部署的應用程式。 並非所有部署類型都支援解除安裝動作。

如需詳細資訊，請參閱[部署應用程式](../deploy-use/deploy-applications.md)。  

### <a name="deployment-purpose"></a>部署目的

「部署目的」  指定部署應用程式是 [必要]  或 [可用]  ：  

- 用戶端會根據您設定的排程自動安裝「必要」  部署。 如果未隱藏應用程式，使用者可以追蹤其部署狀態。 他們也可以使用軟體中心，在期限前安裝應用程式。  

- 如果您部署給使用者的應用程式為「可用」  ，其會在軟體中心看到該應用程式，並可視需求要求應用程式。  

如需詳細資訊，請參閱[部署應用程式](../deploy-use/deploy-applications.md)。  

### <a name="revisions"></a>修訂

當您針對應用程式或部署類型進行「修訂」  時，Configuration Manager 會建立新的應用程式版本。 在 Configuration Manager 主控台中執行下列動作：

- 顯示每個應用程式修訂的歷程記錄
- 檢視其內容
- 還原先前的應用程式版本
- 刪除舊版本

如需詳細資訊，請參閱[更新和淘汰應用程式](../deploy-use/update-and-retire-applications.md)。  

### <a name="detection-method"></a>偵測方法

使用「偵測方法」  探索裝置是否已安裝應用程式。 如果偵測方法表示已安裝應用程式，則 Configuration Manager 不會嘗試再次安裝。

如需詳細資訊，請參閱[部署類型的偵測方法選項](../deploy-use/create-applications.md#bkmk_dt-detect)。

### <a name="dependencies"></a>相依性

「相依性」  會從用戶端安裝此部署類型之前必須先行安裝的其他應用程式中，定義一或多個部署類型。

如需詳細資訊，請參閱[部署類型的相依性](../deploy-use/create-applications.md#bkmk_dt-depend)。  

### <a name="supersedence"></a>取代

Configuration Manager 可讓您使用「取代」  關聯性來升級或取代現有應用程式。 當您取代應用程式時，您會指定新的部署類型來取代被取代應用程式的部署類型。 您也可以決定要升級被取代的應用程式，或將它解除安裝再由用戶端安裝取代的應用程式。

如需詳細資訊，請參閱[應用程式取代](../deploy-use/revise-and-supersede-applications.md#application-supersedence)。  

### <a name="user-centric-management"></a>使用者為中心的管理

Configuration Manager 應用程式支援「以使用者為中心的管理」  ，讓您可以建立特定使用者與特定裝置的關聯。 您不需要記住使用者裝置的名稱，就可以將應用程式部署給使用者和裝置。 這項功能可協助您確保使用者的每部裝置上一律有最重要的應用程式。 若使用者獲得一部新電腦，Configuration Manager　會在使用者登入前，自動將其應用程式安裝到裝置上。

如需詳細資訊，請參閱[透過使用者裝置親和性連結使用者和裝置](../deploy-use/link-users-and-devices-with-user-device-affinity.md)。  

### <a name="application-group"></a>應用程式群組

從 1906 版開始，建立您可以作為單一部署傳送給使用者或裝置集合的應用程式群組。 您所指定應用程式群組相關中繼資料會顯示為軟體中心內的單一實體。 您可以排序群組中的應用程式，讓用戶端依特定順序來安裝這些應用程式。

如需詳細資訊，請參閱[建立應用程式群組](../deploy-use/create-app-groups.md)。

## <a name="what-application-types-can-you-deploy"></a>您可以部署的應用程式類型為何？

Configuration Manager 可讓您部署下列應用程式類型：  

- Windows Installer (msi)  

- Windows 應用程式套件和應用程式套件組合 (appx、appxbundle、msix、msixbundle)  

- Microsoft Store 中的 Windows 應用程式套件  

- 協力廠商安裝程式和指令碼包裝函式的指令碼安裝程式

- Microsoft App-V v4 和 v5  

- macOS  

- 複雜應用程式的非 OS 部署工作順序

此外，當您透過 Configuration Manager [內部部署裝置管理](../../mdm/understand/manage-mobile-devices-with-on-premises-infrastructure.md)功能來管理裝置時，可以進一步管理下列應用程式類型：  

- Windows Phone 應用程式套件 (xap)  

- Microsoft Store 中的 Windows Phone 應用程式套件  

- 透過 MDM 的 Windows Installer (msi)  

- Web 應用程式

## <a name="state-based-applications"></a>狀態型應用程式  

Configuration Manager 應用程式會使用狀態式監視功能。 您可以追蹤使用者和裝置最近的應用程式部署狀態。 狀態訊息會顯示有關個別裝置的資訊。 例如，如果您將應用程式部署至使用者集合，您可以在 Configuration Manager 主控台中檢視部署與部署目的的合規性狀態。 從 Configuration Manager 主控台中的 [監視]  工作區，監視所有軟體的部署。 如需詳細資訊，請參閱[監視應用程式](../deploy-use/monitor-applications-from-the-console.md)。  

Configuration Manager 用戶端會定期重新評估應用程式部署。 例如：  

- 使用者解除安裝已部署的應用程式。 在下一個評估週期中，Configuration Manager 偵測到應用程式不存在。 用戶端接著會自動重新安裝應用程式。  

- Configuration Manager 未在裝置上安裝應用程式，因為它不符合需求。 稍後，裝置會進行變更，因此現在已符合需求。 Configuration Manager 偵測到此變更，而且用戶端會安裝應用程式。  

您可以設定應用程式部署的重新評估間隔。 請使用 [軟體部署]  群組中的 [排程部署的重新評估]  用戶端設定。 如需詳細資訊，請參閱[關於用戶端設定](../../core/clients/deploy/about-client-settings.md#software-deployment)。  

## <a name="get-started-creating-an-application"></a>開始建立應用程式  

如果您想要直接建立應用程式，可以在[建立和部署應用程式](../get-started/create-and-deploy-an-application.md)一文中找到逐步解說。  

如果您已熟悉基本概念，但需要所有可用選項的更詳細參考資訊，請開始[建立應用程式](../deploy-use/create-applications.md)。  

## <a name="software-center"></a>軟體中心  

軟體中心是與 Configuration Manager 用戶端一起安裝的 Windows 應用程式。 可用來執行下列動作：  

- 瀏覽並要求部署至裝置或使用者的應用程式
- 安裝並排程軟體安裝
- 檢視應用程式、軟體更新和作業系統的安裝狀態
- 設定遠端控制設定
- 設定電源管理

如需詳細資訊，請參閱下列文章：  

- [規劃和設定應用程式管理](../plan-design/plan-for-and-configure-application-management.md)
- [針對軟體中心進行規劃](../plan-design/plan-for-software-center.md)
- [軟體中心使用者指南](../../core/understand/software-center.md)

> [!Note]  
> 1910 版會終止對應用程式類別目錄角色的支援。 如需詳細資訊，請參閱[移除應用程式類別目錄](../plan-design/plan-for-and-configure-application-management.md#bkmk_remove-appcat)。  

## <a name="packages-and-programs"></a>封裝和程式  

Configuration Manager 會持續支援產品舊版本中所使用的套件和程式。

如需詳細資訊，請參閱[套件和程式](../deploy-use/packages-and-programs.md)。  

## <a name="next-steps"></a>後續步驟

現在，您了解 Configuration Manager 中之應用程式管理的基本概念，請繼續閱讀下列文章：

- [建立和部署範例應用程式](../get-started/create-and-deploy-an-application.md)
- [規劃和設定應用程式管理](../plan-design/plan-for-and-configure-application-management.md)
- [建立應用程式](../deploy-use/create-applications.md)
