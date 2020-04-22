---
title: 移除 CAS
titleSuffix: Configuration Manager
description: 移除管理中心網站 (CAS) 會將 Configuration Manager 基礎結構簡化為單一獨立主要站台。
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 16975644-8dfa-4f22-b45a-c54a9250dbd2
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 6704075d707306f55a50a937185c9bdd28b18cc5
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81700616"
---
# <a name="remove-the-central-administration-site"></a>移除管理中心網站

適用於：  Configuration Manager (最新分支)

<!-- 3607277 -->

從 2002 版開始，如果階層包含管理中心網站 (CAS) 和單一子主要站台，則可移除 CAS。 此動作會將 Configuration Manager 基礎結構簡化為單一獨立主要站台。 此動作會將站對站複寫的複雜性簡化，並將管理工作重點放在單一站台上。

> [!IMPORTANT]
> 在此版本的 Configuration Manager 中，這項功能是發行前版本，預設不會啟用。 這項功能目前可供 Microsoft Premier 客戶使用。
>
> 若要啟用這項功能，請洽詢技術支援專案經理以取得協助：
>
> - TAM 會開啟一個諮詢案例，這會使用 Microsoft Premier 時數。
> - 無法變更案例的嚴重性。
> - Microsoft 支援服務將在平常的工作日上班時間內為這些諮詢案例提供協助。

## <a name="plan"></a>方案

- 階層必須由 CAS 和單一子主要站台組成。 主要站台可以具有次要站台。 若要從階層移除其他子主要站台，請檢閱[解除安裝主要站台](uninstall-sites-and-hierarchies.md#bkmk_primary)的規劃步驟和先決條件。

- 請確認子主要站台符合[獨立主要站台](../../../plan-design/configs/size-and-scale-numbers.md#bkmk_pri)大小和規模需求。

- 在 CAS 上移動或淘汰任何網站角色 (服務連接點和軟體更新點除外)。 當移除 CAS 時，Configuration Manager 安裝程式會處理這兩個角色。

  下列角色在必須淘汰或移至主要站台的 CAS 中最常見：

  - Asset Intelligence 同步處理點
  - Endpoint Protection 點
  - Reporting Services 點
  - 資料倉儲服務點
  - 雲端管理閘道 (CMG)

    > [!NOTE]
    > 如果已啟用內容的 CMG，請在主要站台上重新建立 CMG 之後規劃轉散布內容。<!-- 6608659 -->

- 關閉分散式檢視

- Configuration Manager 會自動處理內建套件的套件來源位置，例如 Configuration Manager 用戶端。 請檢閱所有其他內容來源位置，以確保其並未在 CAS 上使用共用。

- 停止任何作用中移轉作業，並移除移轉的所有設定。 如需詳細資訊，請參閱[停止來自另一個階層的作用中移轉](prerequisites-for-installing-sites.md#stop-active-migration-from-another-hierarchy)。

- 如果針對軟體更新使用自動部署規則，請在子主要站台上重新建立這些規則。

- 如果使用 Configuration Manager 或 System Center Updates Publisher 來管理[協力廠商軟體更新](../../../../sum/deploy-use/third-party-software-updates.md)，請從 CAS 上的軟體更新點匯出 WSUS 簽署憑證。

  - 在移除 CAS 之前，請等候協力廠商軟體更新的任何必要部署期限。 用戶端會預先下載內容以用於必要的部署，當變更軟體更新點時，內容雜湊會隨著軟體更新的「本機發佈」  而變更。 (此行為不會影響其他內容類型，只會在本機發佈協力廠商軟體更新。)如果在這些必要部署仍在進行的情況下移除 CAS，則會在用戶端上發生雜湊不符的錯誤而失敗。

- 檢閱任何可能相依於 CAS 的協力廠商軟體。

## <a name="prerequisites"></a>先決條件

- 執行 Configuration Manager 安裝程式的系統管理使用者，需要下列安全性權限：

  - CAS 伺服器的本機**系統管理員**權限

  - 如果 CAS 資料庫伺服器在站台伺服器遠端，則需要 CAS 遠端站台資料庫伺服器的本機**系統管理員**權限。

  - CAS 站台資料庫的**系統管理員** (Sysadmin) 權限

  - 主要站台伺服器的本機**系統管理員**權限

  - 如果主要站台資料庫伺服器在主要站台伺服器遠端，則需要主要站台的遠端站台資料庫伺服器上本機**系統管理員**權限。

  - 主要站台資料庫上的**系統管理員**權限

  - CAS 和主要站台上的**基礎結構系統管理員**或**系統高權限管理員**安全性角色

- 階層中只有一個子主要站台。 如需詳細資訊，請參閱[解除安裝主要站台](uninstall-sites-and-hierarchies.md#bkmk_primary)。

## <a name="process"></a>程序

1. 使用下列其中一種方法啟動 CAS 伺服器上的 Configuration Manager 安裝程式：

    - 在 [開始]  功能表上，選取 [Configuration Manager 安裝程式]  。

    - 在 Configuration Manager 的「安裝媒體」  目錄中，開啟 `\SMSSETUP\BIN\X64\setup.exe`。 請確定此版本與站台版本相同。

    - 在 Configuration Manager 的「安裝」  目錄中，開啟 `\BIN\X64\setup.exe`。

1. 檢閱 [開始之前]  頁面上的資訊。

1. 在 [開始使用]  頁面上，選取 [執行站台維護或重設此站台]  。

1. 在 [站台維護]  頁面上，選取 [移除管理中心網站]  。 <!-- or is it still "delete"? -->

1. 在 [重新設定現有的站台系統角色]  頁面上：

    - **服務連接點**：在主要站台中輸入站台系統的完整網域名稱，以裝載此必要角色。 如需詳細資訊，請參閱 [About the service connection point](../configure/about-the-service-connection-point.md) (關於服務連接點)。

    - **軟體更新點**：選取主要站台中現有的軟體更新點。 安裝程式會將此軟體更新點設定為與 CAS 設定同步處理。

    安裝程式會檢查指定的伺服器是否滿足先決條件。 準備好繼續進行時，請選取 [開始安裝]  。

如果安裝程式發生問題，請使用精靈來重試程序。

安裝程式完成後，會重設主要站台。 如需詳細資訊，請參閱[執行站台重設](../../manage/modify-your-infrastructure.md#bkmk_reset)。

## <a name="monitor-and-verify"></a>監視與驗證

請在安裝程序中檢閱下列記錄：

- CAS 伺服器上的 `C:\ConfigMgrSetup.log`

- 主要站台伺服器上 Configuration Manager 記錄目錄中的 **hman.log**

使用 [監視]  工作區中的 [站台階層]  節點，將階層的變更視覺化。 例如，下圖顯示 **SHY** CAS、**HAW** 主要站台及 **VWT** 次要站台之前和之後的比較：

| 之前  | 在   |
|---------|---------|
|![CAS、主要站台和次要站台的範例站台階層檢視](media/3607277-cas-primary-secondary.png)|![主要站台和次要站台的範例站台階層檢視](media/3607277-primary-secondary.png)|

## <a name="post-setup-tasks"></a>安裝後的工作

移除 CAS 後，請在下列步驟套用至環境時檢閱這些步驟。

- 手動從主要站台本機群組移除 CAS 伺服器電腦帳戶。

- 受信任的根金鑰已變更，可能需要其他動作：

  - 更新 OS 部署開機映像，以包含最新的 Configuration Manager 二進位檔。

  - 重新建立 [OS 部署媒體](../../../../osd/deploy-use/create-task-sequence-media.md)。

- 如果將 Configuration Manager 與 [Azure 監視器](https://docs.microsoft.com/azure/azure-monitor/platform/collect-sccm?context=configmgr/core/context/core-context)連線，則需要重設連線。 解決任何問題的第一個步驟是[更新祕密金鑰](../configure/azure-services-wizard.md#bkmk_renew)。 如果這樣仍無法解決問題，請重新建立連線。<!-- 5584635 -->

- 在 2002 版中，如果啟用 Surface 驅動程式的同步處理，請在移除 CAS 後重新設定此功能。 如需詳細資訊，請參閱[包含 Microsoft Surface 驅動程式與韌體更新](../../../../sum/get-started/configure-classifications-and-products.md#bkmk_Surface)。<!-- 5728727 -->

- 如果管理協力廠商軟體更新：

  1. 從 CAS 上的軟體更新點匯出 WSUS 簽署憑證 (如果尚未這麼做)。

  1. 在建立任何新的部署之前，請先從任何現有的部署和軟體更新套件中移除更新。

  1. 若要將軟體更新中繼資料復原到可用的狀態，請重新同步處理已訂閱的目錄。 您也可以等候 Configuration Manager 自動重新同步處理。

  1. 開始 (或等待) 一般軟體更新同步程序來將 Configuration Manager 更新為 WSUS 的目前狀態。 (選擇性) 使用 SCUP 或 WSUS PowerShell Cmdlet 來刪除並重新新增更新。

  1. 重新發佈所需部署的更新內容。
