---
title: 與 Power BI 報表伺服器整合
titleSuffix: Configuration Manager
description: 整合 Power BI 報表伺服器與 Configuration Manager 報告，實現現代化視覺效果及更佳的效能。
ms.date: 04/08/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 315e2613-dc71-46b1-80cb-26161d08103a
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: f4089f52d912491b3b1396906fe391c5c334e061
ms.sourcegitcommit: 02635469d684d233fef795d2a15615658e62db10
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/16/2020
ms.locfileid: "84814896"
---
# <a name="integrate-with-power-bi-report-server"></a>與 Power BI 報表伺服器整合

適用於：Configuration Manager (最新分支)

<!--3721603-->

從 2002 版開始，可整合 [Power BI 報表伺服器](https://docs.microsoft.com/power-bi/report-server/get-started)與 Configuration Manager 報告。 這項整合為您提供現代化視覺效果和更好的效能。 其新增的 Power BI 報表主控台支援類似 SQL Server Reporting Services 已有的功能。

儲存 Power BI Desktop 報表檔案 (.PBIX) 並將其部署至 Power BI 報表伺服器。 此程序類似 SQL Server Reporting Services 報表檔案 (.RDL)。 您也可以直接從 Configuration Manager 主控台，在瀏覽器中啟動報表。

## <a name="prerequisites"></a>先決條件

- Power BI 報表伺服器授權。 如需詳細資訊，請參閱[授權 Power BI 報表伺服器](https://docs.microsoft.com/power-bi/report-server/get-started#licensing-power-bi-report-server)。

- 下載 [Microsoft Power BI 報表伺服器 - 2019 年 9 月](https://www.microsoft.com/download/details.aspx?id=57270)或更新版本。

    > [!NOTE]
    > 請勿立刻安裝 Power BI 報表伺服器。 如需依據環境進行適當處理，請參閱[設定 Reporting Services 點](#configure-the-reporting-services-point)。

- 下載 [Microsoft Power BI Desktop (針對 Power BI 報表伺服器最佳化 - 2019 年 9 月)](https://www.microsoft.com/download/details.aspx?id=57271) 或更新版本。

    > [!IMPORTANT]
    > - 請只使用 [Microsoft 下載中心](https://www.microsoft.com/download/)提供的 Power BI Desktop 版本，請勿使用 Microsoft Store 提供的版本。
    > - 請只使用[標示**針對 Power BI 報表伺服器最佳化**的 Power BI Desktop 版本](https://docs.microsoft.com/power-bi/report-server/install-powerbi-desktop)。

- Power BI 整合會使用以相同角色為基礎的系統管理來進行報告。
    > [!NOTE]
    > Power BI 報表伺服器不支援已啟用 RBAC 的報表，因此不論報表檢視者的受指派範圍為何，所有檢視者都會看到相同結果。

## <a name="configure-the-reporting-services-point"></a>設定 Reporting Services 點

此程序會隨您在網站中是否具有此角色而異。

### <a name="you-have-a-reporting-services-point"></a>您已經擁有 Reporting Services 點

只有當在站台中已經擁有 Reporting Services 點時，才能使用此流程。 在同一部伺服器上執行此程序的所有步驟：

1. 在**報表伺服器 Configuration Manager** 中備份**加密金鑰**。 如需詳細資訊，請參閱 [SSRS 加密金鑰 - 備份與還原加密金鑰](https://docs.microsoft.com/sql/reporting-services/install-windows/ssrs-encryption-keys-back-up-and-restore-encryption-keys)。

    > [!WARNING]
    > 如果略過此步驟，您將無法存取 SQL Server Reporting Services 中的任何自訂報表。

1. 移除網站中的 Reporting Services 點角色。

1. 解除安裝 SQL Server Reporting Services，但保留資料庫。

1. 安裝 Power BI 報表伺服器。

1. 設定 Power BI 報表伺服器

    1. 使用前報表伺服器資料庫。

    1. 使用**報表伺服器 Configuration Manager** 來還原**加密金鑰**。

1. 在 Configuration Manager 中新增 Reporting Services 點角色。

### <a name="you-dont-have-a-reporting-services-point"></a>您還沒有 Reporting Services 點

只有當在站台中尚未擁有 Reporting Services 點時，才能使用此流程。 在同一部伺服器上執行此程序的所有步驟：

1. 安裝 Power BI 報表伺服器。

2. 在 Configuration Manager 中新增 Reporting Services 點角色。 如需詳細資訊，請參閱[設定報告](configuring-reporting.md)。

## <a name="configure-the-configuration-manager-console"></a>設定 Configuration Manager 主控台

1. 在具有 Configuration Manager 主控台的電腦上，將 Configuration Manager 主控台更新至最新版。

1. 安裝 Power BI Desktop。 確認語言相同。

1. 安裝 Power BI Desktop 後，在開啟 Configuration Manager 主控台前請先至少先啟動一次。

## <a name="create-power-bi-reports"></a>建立 Power BI 報表

1. 在 Configuration Manager 主控台中，移至 [監視] 工作區並展開 [報告]，然後選取新的 [Power BI 報表] 節點。

1. 在功能區中，選取 [建立報表]。 此動作會開啟 Power BI Desktop。

1. 在 Power BI Desktop 中建立報表。

    - 在 Power BI Desktop 中，當連線到資料來源時，請選取 [DirectQuery] 進行連線設定。

    - 請在這些報表中僅使用受支援的 SQL 檢視表。 如需詳細資訊，請參閱[在 Configuration Manager 中使用 SQL Server 檢視建立自訂報表](../../../develop/core/understand/sqlviews/create-custom-reports-using-sql-server-views.md)。

1. 當報表可供儲存時，請移至 [檔案] 功能表，然後選取 [另存新檔]，再選擇 [Power BI 報表伺服器]。

1. 在 [Power BI Report Server Selection] \(Power BI 報表伺服器選項\) 視窗中，輸入 Reporting Services 點的 URL 作為 [新增報表伺服器位址]。 例如 `https://rsp.contoso.com/Reports`。

在 Configuration Manager 主控台中，可於 Power BI 報表清單中看到新的報表。

## <a name="next-steps"></a>後續步驟

建立報表後，請在 Configuration Manager 主控台中執行下列動作：

- **在瀏覽器中執行**：在網頁瀏覽器中開啟 Power BI 報表。 與其他人共用此 URL，例如：`https://rsp.contoso.com/Reports/POWERBI/ConfigMgr_ABC/Windows%2010/Windows10%20Dashboard?rs:embed=true`

    > [!TIP]
    > 您只能在網頁瀏覽器中檢視這些報表。

- **編輯**：在 Power BI Desktop 中變更報表。 針對現有的報表，請使用 [儲存] 選項，將變更內容儲存回報表伺服器。

如需用於報告的記錄檔詳細資訊，請參閱[記錄檔參考 - 報告](../../plan-design/hierarchy/log-files.md#BKMK_ReportLog)。
