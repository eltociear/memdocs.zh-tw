---
title: 針對報告進行規劃
titleSuffix: Configuration Manager
description: 從安裝詳細資料到安全性和網路頻寬，請務必規劃 Configuration Manager 中的報告。
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: ff920c84-d5c8-458c-b67f-bc7219b05690
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: 2621a6a364734a1146700aa8eef8fded3a6e58ab
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81694366"
---
# <a name="plan-for-reporting-in-configuration-manager"></a>規劃 Configuration Manager 的報告

適用於：  Configuration Manager (最新分支)

Configuration Manager 的報告會提供一組工具和資源，其有助使用 SQL Server Reporting Services 或 Power BI 報表伺服器的進階報告功能。 下列各節可協助您規劃 Configuration Manager 中的報告功能。

## <a name="where-to-install-the-reporting-services-point"></a>Reporting Services 點的安裝位置

當您在站台中執行 Configuration Manager 報告時，報告即可存取連線站台資料庫中的資訊。 下列章節可協助您判斷 Reporting Services 點的安裝位置，以及應使用的資料來源。

> [!NOTE]
> 如需在 Configuration Manager 中規劃站台系統的詳細資訊，請參閱[新增站台系統角色](../deploy/configure/add-site-system-roles.md)。

### <a name="supported-site-system-servers"></a>支援的站台系統伺服器

您可在管理中心網站 (CAS) 和主要站台安裝 Reporting Services 點。 其適用於站台的多站台系統，以及階層中的其他站台。 Configuration Manager 不支援次要站台的 Reporting Services 點。 站台的第一個 Reporting Services 點會設為預設報告伺服器。 您可在站台中新增多個 Reporting Services 點，但 Configuration Manager 報告會主動使用每個站台的預設報告伺服器。 將 Reporting Services 點安裝在站台伺服器或遠端站台系統。 請在遠端站台系統伺服器上使用 SQL Server Reporting Services，以獲得最佳效能。

### <a name="data-replication-considerations"></a>資料複寫的考量

考量下列因素可以協助您決定 Reporting Services 點的安裝位置：

- 以 CAS 資料庫為報告資料來源的 Reporting Services 點可以存取 Configuration Manager 階層中所有全域和站台資料。 如果需要報表包含階層中多個站台的站台資料，請考慮在 CAS 的站台系統上安裝 Reporting Services 點。 然後使用其資料庫作為報告資料來源。

- 以子主要站台資料庫為報告資料來源的 Reporting Services 點，只能存取本機主要站台和任何子次要站台的全域資料和站台資料。 Configuration Manager 階層中其他主要站台的站台資料不會複寫到此主要站台。 Reporting Services 無法存取其他主要站台的站台資料。 如果需要報表包含特定主要站台的站台資料或全域資料，但不希望使用者從其他主要站台存取站台資料，請將 Reporting Services 點安裝在主要站台的站台系統中。 然後使用主要站台資料庫作為報告資料來源。

如需全域和站台資料的詳細資訊，請參閱[資料類型](../../plan-design/hierarchy/database-replication.md#types-of-data)。

### <a name="network-bandwidth-considerations"></a>網路頻寬考量

視站台的設定方式而定，同一個站台中的站台系統彼此會使用伺服器訊息區 (SMB)、HTTP 或 HTTPS 互相通訊。 Configuration Manager 不會管理此通訊。 在沒有網路頻寬控制的情況下，隨時都可能發生此問題。 請先檢閱可用的網路頻寬，然後在站台系統上安裝 Reporting Services 點角色。

如需規劃站台系統的詳細資訊，請參閱[新增站台系統角色](../deploy/configure/add-site-system-roles.md)。

## <a name="plan-for-role-based-administration"></a>規劃以角色為基礎的系統管理

報告的安全性與 Configuration Manager 中的其他物件類似，您可以指派安全性角色和權限給系統管理使用者。 系統管理使用者只能執行和修改他們擁有相關安全性權限的報告。 若要在 Configuration Manager 主控台中執行報告，使用者必須具有**站台**權限的**讀取**權，以及專為特定物件設定的權限。

不過，與其他 Configuration Manager 物件不同的是，您在 Configuration Manager 主控台中為系統管理員使用者設定的安全性權限，也會在 Reporting Services 中設定。 當您在 Configuration Manager 主控台中設定安全性權限時，Reporting Services 點會連線至 Reporting Services，並且設定適當的報告權限。

例如，**軟體更新管理員**安全性角色擁有**執行報告**和**修改報告**權限。 具有**軟體更新管理員**角色的使用者，只能執行和修改軟體更新報告。 Configuration Manager 主控台不會向此角色顯示其他物件的報告。 一些未與特定 Configuration Manager 安全物件建立關聯的報告則是此行為例外狀況。 就這些報告而言，系統管理員使用者必須擁有 [站台]  的 [讀取]  權限才能執行報告，而要有 [站台]  的 [修改]  權限才能修改報告。  

> [!IMPORTANT]
> 為使 Reporting Servicies 點帳戶以外的不同網域使用者得以成功執行報告，請建立兩個網域間的雙向信任。

針對以角色為基礎的系統管理，已完全啟用報告。 Configuration Manager 會根據報告執行人的使用者權限，以篩選所有內含報告的資料。 具特定角色的使用者，只能檢視針對其角色定義的資訊。

如需報告安全性權限的詳細資訊，請參閱[設定報告](configuring-reporting.md)。

如需 Configuration Manager 中規劃站台系統的詳細資訊，請參閱[設定以角色為基礎的系統管理](../deploy/configure/configure-role-based-administration.md)。

## <a name="reporting-recommendations"></a>報告建議

請考慮下列 Configuration Manager 的報告建議和提示：

- 請在遠端站台系統上安裝 Reporting Services 點，以獲得最佳效能。 雖然可在站台伺服器安裝 Reporting Services 點，但其安裝在遠端站台系統中才能發揮最佳效能。 當此角色執行背景處理時，會與其他角色競爭系統資源。 涉及站台和角色效能時有許多變數要考慮，但一般而言，此設定可改善報告和整體站台的效能。

- 最佳化 SQL Server Reporting Services 查詢。 通常，報告延遲都是因為執行查詢及擷取結果的時間過長所致。 Query Analyzer 和 Profiler 等 Microsoft SQL Server 工具有助最佳化查詢。

- 將報告訂閱處理排定在標準上班時間以外的時間執行。 盡可能在離峰時間處理訂閱，可將 Configuration Manager 站台資料庫伺服器的 CPU 處理降到最低。 此作法也可提高非預期報告要求的可用性。

- 站台更新保留內建報告。 若修改標準報告，則站台更新時會使用底線 (`_`) 作為前置詞來重新命名報告。 此行為可確保站台更新不會覆寫標準報告修改的報告。

## <a name="security-and-privacy"></a>安全性和隱私權

Configuration Manager 報告會顯示於標準 Configuration Manager 管理作業期間所收集的資訊。 例如，可顯示 Configuration Manager 從探索或清查收集的資訊報告。 報告也可以包含用戶端管理作業目前的狀態資訊，例如部署軟體和檢查相容性。

如需會產生可在報告中檢視資料的 Configuration Manager 作業其任何安全性建議和隱私權資訊詳細資訊，請參閱 [Configuration Manager 的安全性與隱私權](../../plan-design/security/security-and-privacy.md)。  

## <a name="next-steps"></a>後續步驟

[報告的先決條件](prerequisites-for-reporting.md)
