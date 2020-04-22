---
title: Microsoft 連線快取
titleSuffix: Configuration Manager
description: 使用 Configuration Manager 發佈點作為傳遞最佳化的本機快取伺服器
ms.date: 03/20/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: c5cb5753-5728-4f81-b830-a6fd1a3e105c
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: e718e62f097a9fec20d7b29deb9f03453931188a
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81696206"
---
# <a name="microsoft-connected-cache-in-configuration-manager"></a>Configuration Manager 中的 Microsoft 連線快取

適用於：  Configuration Manager (最新分支)

<!--3555764-->

從 1906 版開始，您可以在發佈點上安裝 Microsoft 連線快取伺服器。 藉由快取此內部部署內容，您的用戶端就可以受益於傳遞最佳化功能，但您可以協助保護 WAN 連結。

> [!NOTE]
> 從 1910 版開始，這項功能現在稱為 **Microsoft 連線快取**。 先前稱為傳遞最佳化網路內快取 (DOINC)。

此快取伺服器可視需要以透明方式快取傳遞最佳化所下載的內容。 使用用戶端設定可確保只將此伺服器提供給本機 Configuration Manager 界限群組的成員。

此快取不同於 Configuration Manager 的發佈點內容。 如果您選擇與發佈點角色相同的磁碟機，則會另外儲存內容。

> [!Note]  
> 連線快取伺服器是安裝在 Windows Server 上的應用程式。 此應用程式仍在開發中。

## <a name="how-it-works"></a>運作方式

當您將用戶端設定為使用連線快取伺服器時，就不會再向網際網路要求 Microsoft 雲端管理的內容。 用戶端會向安裝在發佈點上的快取伺服器要求此內容。 內部部署伺服器會使用應用程式要求路由 (ARR) 的 IIS 功能來快取此內容。 接著，快取伺服器可以快速回應相同內容的任何未來要求。 如果連線快取伺服器無法使用，或尚未快取內容，則用戶端就會從網際網路下載內容。 用戶端也會使用傳遞最佳化，因此請從其網路中的對等，下載部分內容。

![連線快取運作方式的圖表](media/3555764-microsoft-connected-cache.png)

1. 用戶端會檢查更新，並取得內容傳遞網路 (CDN) 的位址。

2. Configuration Manager 會在用戶端上設定傳遞最佳化 (DO) 設定，包括快取伺服器名稱。

3. 用戶端 A 會向 DO 快取伺服器要求內容。

4. 如果快取不包含此內容，則 DO 快取伺服器會從 CDN 取得它。

5. 如果快取伺服器無法回應，用戶端會從 CDN 下載內容。

6. 用戶端會使用 DO 來取得來自對等的內容片段。

## <a name="prerequisites-and-limitations"></a>必要條件和限制

- *內部部署*發佈點，其設定如下：

  - 執行 Windows Server 2012、Windows Server 2012 R2、Windows Server 2016 或 Windows Server 2019

  - 在連接埠 80 上啟用的預設網站

  - 請勿預先安裝 IIS 的 [應用程式要求路由](https://docs.microsoft.com/iis/extensions/planning-for-arr/application-request-routing-version-2-overview) (ARR) 功能。 連線快取會安裝 ARR，並進行其設定。 Microsoft 無法保證連線快取的 ARR 設定不會與伺服器上同時使用此功能的其他應用程式產生衝突。

  - 此發佈點需要 Microsoft 雲端的網際網路存取權限。 特定 URL 可能會依已啟用雲端的特定內容而有所不同。 如需詳細資訊，請參閱[網際網路存取需求](../network/internet-endpoints.md)。

  - 從 2002 版開始，連線快取應用程式可以使用未經驗證的 Proxy 伺服器來存取網際網路。 如需詳細資訊，請參閱[為站台系統伺服器設定 Proxy](../network/proxy-server-support.md#configure-the-proxy-for-a-site-system-server)。<!-- 5856396 -->

- 執行 Windows 10 1709 版或更新版本的用戶端

## <a name="enable-connected-cache"></a>啟用連線快取

1. 在 Configuration Manager 主控台中，移至 [系統管理]  工作區，然後選取 [發佈點]  節點。

1. 選取「內部部署」  發佈點，然後在功能區中選取 [內容]  。

1. 在發佈點角色屬性的 [一般]  索引標籤上，進行下列設定：  

    1. 啟用 [Enable this distribution point to be used as Microsoft Connected Cache server] \(允許將此發佈點用作 Microsoft 連線快取伺服器\)  選項  

        請檢視並接受授權條款。

    2. **要使用的本機磁碟機**：選取用於快取的磁碟。 [自動]  是預設值，會使用可用空間最多的磁碟。<sup>[備註 1](#bkmk_note1)</sup>  

        > [!Note]  
        > 您之後可以變更此磁碟機。 除非您將所有快取的內容都複製到新的磁碟機，否則將會遺失。

    3. **磁碟空間**：選取要保留的磁碟空間量，並以 GB 或總磁碟空間的百分比為單位。 根據預設，此值為 100 GB。

        > [!Note]  
        > 預設快取大小應該足以應付大部分的客戶。 您之後可以調整快取大小。
        >
        > 如果磁碟上快取大小超過配置的空間，則 ARR 會根據其內建啟發學習法移除內容來清除空間。<!-- SCCMDocs#2045 -->

    4. **停用連線快取伺服器時保留快取**：如果您移除快取伺服器並啟用這個選項，伺服器會將快取內容保留在磁碟上。  

1. 在用戶端設定的 [傳遞最佳化]  群組中，設定為 [Enable devices managed by Configuration Manager to use Microsoft Connected Cache servers for content download] \(允許 Configuration Manager 所管理裝置使用 Microsoft 連線快取伺服器來下載內容\)  。  

### <a name="note-1-about-drive-selection"></a><a name="bkmk_note1"></a> 附註 1：關於選取磁碟機

如果您選取 [自動]  ，則當 Configuration Manager 安裝連線快取元件時，會接受 **no_sms_on_drive.sms** 檔案。 例如，發佈點具有 `C:\no_sms_on_drive.sms` 檔案。 即使 C: 磁碟機有最多的可用空間，Configuration Manager 仍會設定連線快取使用其他磁碟機來進行快取。

如果您選取已有 **no_sms_on_drive.sms** 檔案的特定磁碟機，則 Configuration Manager 會忽略此檔案。 設定連線快取使用該磁碟機為明確的意圖。 例如，發佈點具有 `F:\no_sms_on_drive.sms` 檔案。 當明確設定發佈點內容來使用 **F:** 磁碟機時，Configuration Manager 會設定連線快取使用 F: 磁碟機來進行快取。

安裝連線快取後變更磁碟機：

- 手動設定發佈點內容以使用特定的磁碟機代號。

- 如果設為自動，請先建立 **no_sms_on_drive.sms** 檔案。 然後，變更部分發佈點內容，以觸發設定變更。

## <a name="verify"></a>確認

當用戶端下載雲端管理的內容時，他們可以從安裝在您發佈點上的快取伺服器中使用傳遞最佳化。 雲端管理的內容包括下列類型：

- Microsoft Store 應用程式
- 隨選 Windows 功能，例如語言
- 如果您啟用[商務用 Windows Update 原則](../../../sum/deploy-use/integrate-windows-update-for-business-windows-10.md)：Windows 10 功能和品質更新
- 對於[共同管理工作負載](../../../comanage/workloads.md)：
  - 商務用 Windows Update：Windows 10 功能和品質更新
  - Office 隨選即用應用程式：Office 應用程式和更新
  - 用戶端應用程式：Microsoft Store 應用程式和更新
  - Endpoint Protection：Windows Defender 定義更新

在 Windows 10 1809 版或更新版本上，使用 **Get-DeliveryOptimizationStatus** Windows PowerShell Cmdlet 確認此行為。 在 Cmdlet 輸出中，檢閱 **BytesFromCacheServer** 值。 如需詳細資訊，請參閱[監視傳遞最佳化](https://docs.microsoft.com/windows/deployment/update/waas-delivery-optimization-setup#monitor-delivery-optimization)。

如果快取伺服器傳回任何 HTTP 失敗，則傳遞最佳化用戶端會回復為原始雲端來源。

如需詳細資訊，請參閱[在 Configuration Manager 中針對 Microsoft 連線快取進行疑難排解](../../servers/deploy/configure/troubleshoot-microsoft-connected-cache.md)。

## <a name="support-for-intune-win32-apps"></a><a name="bkmk_intune"></a> Intune Win32 應用程式的支援

<!--5032900-->

從 1910 版開始，當在 Configuration Manager 發佈點上啟用連線快取時，這些發佈點可以將 Microsoft Intune Win32 應用程式提供給共同管理的用戶端。

### <a name="prerequisites"></a>先決條件

#### <a name="client"></a>用戶端

- 請將用戶端更新為最新版本。

- 用戶端裝置必須至少擁有 4 GB 的記憶體。

    > [!TIP]
    > 使用下列群組原則設定：[電腦設定] > [系統管理範本] > [Windows 元件] > [傳遞最佳化] > [啟用對等快取所需的最小 (含) RAM 容量 (以 GB 為單位)]  。

#### <a name="site"></a>網站

- 啟用發佈點上的已連線快取。 如需詳細資訊，請參閱 [Microsoft 連線快取](microsoft-connected-cache.md)。

- 藉由用戶端和已連線快取所啟用的發佈點必須位於相同界限群組中。

- 在[**傳遞最佳化**](../../clients/deploy/about-client-settings.md#delivery-optimization)群組中啟用下列用戶端設定：

  - **針對傳遞最佳化群組識別碼使用 Configuration Manager 界限群組**
  - **允許 Configuration Manager 管理的裝置使用 Microsoft 已連線快取伺服器來下載內容**

- 啟用發行前版本功能**共同管理裝置的用戶端應用程式**。 如需詳細資訊，請參閱[發行前版本功能](../../servers/manage/pre-release-features.md)。

- 啟用共同管理，並將**用戶端應用程式**的工作負載切換至**試驗 Intune** 或 **Intune**。 如需詳細資訊，請參閱下列文章：

  - [工作負載 - 用戶端應用程式](../../../comanage/workloads.md#client-apps)
  - [如何啟用共同管理](../../../comanage/how-to-enable.md)
  - [將工作負載切換至 Intune](../../../comanage/how-to-switch-workloads.md)

    如果在試驗中，則請將用戶端新增至用戶端應用程式的試驗集合。

#### <a name="intune"></a>Intune

- 這項功能僅支援 Intune Win32 應用程式類型。

  - 基於此目的，在 Intune 中建立並指派 (部署) 新的應用程式。 (在 Intune 1811 版之前建立的應用程式無法使用。)如需詳細資訊，請參閱 [Intune Win32 應用程式管理](https://docs.microsoft.com/intune/apps/apps-win32-app-management)。

  - 應用程式的大小必須至少為 100 MB。
  
    > [!TIP]
    > 使用下列群組原則設定：[電腦設定] > [系統管理範本] > [Windows 元件] > [傳遞最佳化] > [最小對等快取內容檔案大小 (以 MB 為單位)]  。

## <a name="see-also"></a>請參閱

[透過傳遞最佳化將 Windows 10 更新最佳化](../../../sum/deploy-use/optimize-windows-10-update-delivery.md)

[在 Configuration Manager 中針對 Microsoft 連線快取進行疑難排解](../../servers/deploy/configure/troubleshoot-microsoft-connected-cache.md)
