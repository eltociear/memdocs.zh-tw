---
title: 連結使用者和裝置與使用者裝置親和性
titleSuffix: Configuration Manager
description: 使用使用者裝置親和性連結使用者和裝置，並自動將應用程式部署到與使用者相關聯的所有裝置。
ms.date: 07/26/2019
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 5b30b0d5-722d-4d4b-9ed7-5a43de315461
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 2e74f969016d79254ceb8e8323b6e3914969ecc7
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81689266"
---
# <a name="link-users-and-devices-with-user-device-affinity-in-configuration-manager"></a>在 Configuration Manager 中透過使用者裝置親和性連結使用者與裝置

適用於：  Configuration Manager (最新分支)

Configuration Manager 中的使用者裝置親和性可建立使用者與一或多部裝置的關聯。 此行為不需要知道使用者裝置的名稱，也可為使用者部署應用程式。 不需要將應用程式部署至該使用者的每部裝置，而是部署給該使用者。 接著，使用者裝置親和性會自動確定該應用程式是否已安裝在與該使用者相關聯的所有裝置上。  

定義使用者每天用來執行工作的主要裝置。 在使用者和裝置之間建立親和性時，可以獲得更多應用程式部署選項。 例如，如果使用者需要 Microsoft Visio，您可以使用 Windows Installer 部署將它安裝在該使用者的主要裝置上。 不過，在非主要裝置上，您可以將 Visio 部署為虛擬應用程式。 您也可以使用使用者裝置親和性，在使用者未登入時，預先將軟體部署到使用者的裝置上。 然後，當使用者登入時，應用程式已經安裝並準備好執行。  

您只需要管理電腦的使用者裝置親和性資訊。 Configuration Manager 會自動管理使用者裝置與其所註冊之行動裝置的親和性。  

## <a name="manually-set-up-user-device-affinity"></a>手動設定使用者裝置親和性  

1. 在 Configuration Manager 主控台中，移至 [資產與合規性]  工作區，然後選取 [裝置]  節點。  

1. 選取一個裝置。 在功能區的 [常用]  索引標籤的 [裝置]  群組中，選擇 [編輯主要使用者]  。  

1. 在 [編輯主要使用者]  對話方塊中，搜尋並選取要新增為所選裝置之主要使用者的使用者。 選擇 [新增]  。  

    > [!NOTE]  
    > [主要使用者]  清單會顯示哪些使用者已經是此裝置的主要使用者，以及用於指派每個使用者-裝置關聯性的方法。  

## <a name="set-up-primary-devices-for-a-user"></a>設定使用者的主要裝置  

1. 在 Configuration Manager 主控台中，移至 [資產與合規性]  工作區，然後選取 [使用者]  節點。  

1. 選取使用者。 在功能區的 [裝置]  索引標籤上，選擇 [編輯主要裝置]  。  

1. 在 [編輯主要裝置]  對話方塊中，搜尋並選取裝置以將其新增為所選使用者的主要裝置。 選擇 [新增]  。  

    > [!NOTE]  
    > [主要裝置]  清單會顯示哪些裝置已設為此使用者的主要裝置，以及用於指派每個使用者-裝置關聯性的方法。  

## <a name="automatically-create-user-device-affinities-windows-pcs-only"></a>自動建立使用者裝置親和性 (僅限 Windows 電腦)

Configuration Manager 會從 Windows 事件記錄檔讀取使用者登入事件相關資料。 若要自動建立使用者裝置親和性，您必須在用戶端電腦的本機安全性原則中開啟這兩個選項，將登入事件儲存在 Windows 事件記錄檔中：  

- **稽核帳戶登入事件**  
- **稽核登入事件**  

若要進行這些設定，請使用 Windows 群組原則。  

> [!IMPORTANT]  
> 如果錯誤導致 Windows 事件記錄檔產生大量項目，可能會建立新的事件記錄檔。 若發生此行為，Configuration Manager 可能無法使用現有的登入事件。  

### <a name="set-up-the-site-to-automatically-create-user-device-affinities"></a>設定站台自動建立使用者裝置親和性  

1. 在 Configuration Manager 主控台中，移至 [系統管理]  工作區，然後選取 [用戶端設定]  節點。  

1. 若要修改預設用戶端設定，請選取 [預設用戶端設定]  。 在功能區 [常用]  索引標籤的 [內容]  群組中，選擇 [內容]  。

    若要建立自訂用戶端代理程式設定，請在功能區 [首頁]  索引標籤的 [建立]  群組中，選擇 [建立自訂用戶端裝置設定]  。

    > [!NOTE]  
    > 如果修改預設用戶端設定，網站會將這些設定部署至階層中的所有電腦。 如需詳細資訊，請參閱[如何設定用戶端設定](../../core/clients/deploy/configure-client-settings.md)。  

1. 在 [使用者和裝置親和性]  群組中，設定下列設定：  

    - **使用者裝置親和性閾值 (分鐘)** ：設定在網站建立使用者裝置親和性之前的裝置使用分鐘數。  

    - **使用者裝置親和性閾值 (天)** ：設定站台衡量使用親和性閾值的天數。  

    - **從使用資料自動設定使用者裝置親和性**：選取 **True** 讓網站自動建立使用者裝置親和性。 如果您選取 [False]  ，則必須核准所有使用者裝置親和性指派。  

    > [!TIP]  
    > 例如，若您將 [使用者裝置親和性閾值 (分鐘)]  設定為 **60** 分鐘，並將 [使用者裝置親和性閾值 (天)]  設定為 **5** 天，則使用者在 5 天內至少必須使用該裝置 60 分鐘，才會自動建立使用者裝置親和性。  

Configuration Manager 在建立自動使用者裝置親和性之後，會繼續監視使用者裝置親和性閾值。 如果使用者的裝置活動低於您設定的閾值，網站會移除使用者裝置親和性。 將**使用者裝置親和性閾值 (天數)** 設定為至少七天的值。 此設定可避免當使用者未登入時 (例如週末期間)，自動設定使用者親和性可能遺失的情形。  


## <a name="import-user-device-affinities-from-a-file"></a>從檔案匯入使用者裝置親和性

若要一次建立許多關聯性，您可以匯入包含多個使用者裝置親和性詳細資料的檔案。 請確定網站已探索到目標裝置，並以資源的形式存在於 Configuration Manager 資料庫中。  

1. 在 Configuration Manager 主控台中，移至 [資產與合規性]  工作區，然後選取 [使用者]  或 [裝置]  節點。  

1. 在功能區的 [常用]  索引標籤的 [建立]  群組中，選擇 [匯入使用者裝置親和性]  。  

1. 在 [匯入使用者裝置親和性精靈] 的 [選擇對應]  頁面上，設定這項資訊：  

    - **檔案名稱**。 指定逗號分隔值 (CSV) 檔案，其中會列出要相互建立親和性的使用者及裝置。 在此檔案中，每一對使用者和裝置都必須各有其專屬資料列，並以逗號分隔值。 請使用此格式：`<domain>\<username>,<device NetBIOS name>`  

    - **此檔案具有可供參照的欄位標題**。 如果 .csv 檔案具有頂端資料列標頭，請選取這個選項。 網站會在匯入期間忽略標頭資料列。  

1. 如果您匯入的檔案中的每列都有兩個以上的項目，您可以使用 [欄]  與 [指派]  來指定代表使用者與裝置的欄，以及匯入時要忽略的欄。  

1. 完成精靈。  


## <a name="let-users-create-their-own-device-affinities"></a>讓使用者建立其專屬裝置親和性

在軟體中心設定使用者以建立自己的使用者裝置親和性。

### <a name="set-up-the-site-to-allow-user-created-user-device-affinity-requests"></a>設定站台允許使用者建立的使用者裝置親和性要求  

1  在 Configuration Manager 主控台中，移至 [系統管理]  工作區，然後選取 [用戶端設定]  節點。  

1. 若要修改預設用戶端設定，請選取 [預設用戶端設定]  。 在功能區 [常用]  索引標籤的 [內容]  群組中，選擇 [內容]  。

    若要建立自訂用戶端代理程式設定，請在功能區 [首頁]  索引標籤的 [建立]  群組中，選擇 [建立自訂用戶端使用者設定]  。

    > [!NOTE]  
    > 如果修改預設用戶端設定，網站會將這些設定部署至階層中的所有電腦。 如需詳細資訊，請參閱[設定用戶端設定](../../core/clients/deploy/configure-client-settings.md)。  

1. 在 [使用者和裝置親和性]  群組中，啟用 [允許使用者定義其主要裝置]  設定。  

### <a name="set-up-a-user-device-affinity-in-software-center"></a>在軟體中心內設定使用者裝置親和性

從 1902 版開始，請使用軟體中心來設定親和性。

1. 在軟體中心，移至 [選項]  索引標籤。

1. 在 [工作資訊]  區段中，選取 [我經常使用這部電腦工作]  選項。

### <a name="set-up-a-user-device-affinity-in-the-application-catalog"></a>在應用程式目錄中設定使用者裝置親和性

> [!Important]
> 從 1806 最新分支版本開始即不支援應用程式類別目錄的 Silverlight 使用者體驗。 從 1906 版開始，已更新的用戶端會自動使用適用於使用者可用應用程式部署的管理點。 此外，您也無法安裝新的應用程式目錄角色。 1910 版會終止對應用程式類別目錄角色的支援。  
>
> 如需詳細資訊，請參閱下列文章：
>
> - [設定軟體中心](../plan-design/plan-for-software-center.md#bkmk_userex)
> - [已移除和已淘汰的功能](../../core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures.md)  

1. 在應用程式類別目錄中，選擇 [我的系統]  。  

1. 選取 [我經常使用這部電腦工作]  選項。  


## <a name="manage-user-device-affinity-requests-from-users"></a>管理使用者的使用者裝置親和性要求

當您停用用戶端設定 [從使用資料自動設定使用者裝置親和性]  時，您必須手動核准所有使用者裝置親和性指派。  

### <a name="approve-or-reject-a-user-device-affinity-request"></a>核准或拒絕使用者裝置親和性要求  

1. 在 Configuration Manager 主控台中，移至 [資產與合規性]  工作區。  

1. 選取您要管理哪一個使用者或裝置集合的親和性要求。  

1. 在功能區的 [常用]  索引標籤的 [集合]  群組中，選擇 [管理親和性要求]  。  

1. 在 [管理使用者裝置親和性要求]  對話方塊中，選取親和性要求，然後選擇 [核准]  或 [拒絕]  。  


## <a name="next-steps"></a>後續步驟

您也可以使用 Microsoft Intune 來尋找已註冊裝置的主要使用。 如需詳細資訊，請參閱 Intune 文件中的[尋找 Intune 裝置的主要使用者](https://docs.microsoft.com/intune/find-primary-user)。
