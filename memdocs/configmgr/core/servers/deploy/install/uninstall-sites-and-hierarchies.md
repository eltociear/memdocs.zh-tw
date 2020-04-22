---
title: 解除安裝站台
titleSuffix: Configuration Manager
description: 移除角色及解除安裝站台與階層的指南
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: d466edd2-97f0-44c1-a73e-d71abbdbf4a8
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: a90d6f34370b8c3167272bce1a0a673cc5074094
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81700526"
---
# <a name="uninstall-roles-sites-and-hierarchies-in-configuration-manager"></a>在 Configuration Manager 中解除安裝角色、站台和階層

適用於：  Configuration Manager (最新分支)

使用本文作為指南，可解除安裝 Configuration Manager 站台系統角色、站台或階層。

從 2002 版開始，也可從階層移除管理中心網站 (CAS)，但保留主要站台。

## <a name="site-system-role"></a><a name="bkmk_role"></a> 站台系統角色

基於下列原因，建議從站台系統伺服器移除角色：

- 更廣泛的基礎結構變更，例如網路或實體位置
- 解除委任基礎伺服器
- 合併角色以降低成本和複雜性
- 重新設定或重新設計站台角色
- 停止使用角色支援的功能

當決定需要移除角色時，請先考慮下列問題的答案：

- 仍然需要站台中的角色嗎？ 若是如此，其他站台系統是否已具備此角色？

- 其他具備此角色的站台系統是否具有適當大小，可支援效能和可用性的商務需求？

- 所有用戶端都已重新設定為使用另一個角色嗎？ 是否會依賴預設的用戶端行為來回復或探索另一部伺服器？

### <a name="procedure-to-remove-a-site-system-role"></a>移除站台系統角色的程序

使用下列程序來移除角色：

1. 在 **Configuration Manager** 主控台中，移至 [系統管理]  工作區。 展開 [站台設定]  ，然後選取 [伺服器和站台系統角色]  節點。

1. 選取具有所要移除角色的站台系統伺服器。 在 [站台系統角色]  詳細資料窗格中，選取目標角色。

1. 在功能區內 [站台角色]  索引標籤的 [站台角色]  群組中，選取 [移除角色]  。 確認想要移除該角色。

### <a name="additional-information-for-specific-roles"></a>特定角色的其他資訊

某些角色可能會有額外的步驟和考量。

#### <a name="software-update-point"></a>軟體更新點

移除軟體更新點之後，Configuration Manager 會更新用戶端原則，以從清單中移除軟體更新點。 當移除站台上的最後一個軟體更新點時，軟體更新點清單不會包含任何軟體更新點。 在沒有可用角色的情況下，基本上會在站台停用軟體更新管理。

當主要站台上有超過一個軟體更新點，且移除屬於同步處理來源的軟體更新點時，請在站台上選擇另一個軟體更新點作為新的同步處理來源。

## <a name="secondary-site"></a><a name="bkmk_secondary"></a> 次要站台  

除了[解除委任階層](#bkmk_hierarchy)之外，移除次要站台的主要原因是因為基礎結構的變更 (例如網路或實體位置) 較廣泛。 另請檢閱[選擇次要站台](../../../plan-design/hierarchy/design-a-hierarchy-of-sites.md#BKMK_ChooseSecondary)的原因。

當決定需要移除次要站台時，請先考慮下列問題的答案：

- 是否從站台伺服器移除所有站台系統角色？

- 是否有任何界限或界限群組與次要站台建立關聯？ 請先重新設定界限，再移除站台。

- 是否有任何用戶端仍在該位置？

- 是否已設定[對等快取](../../../plan-design/hierarchy/fundamental-concepts-for-content-management.md#peer-caching-technologies)等其他內容管理選項？

### <a name="options-to-delete-secondary-sites"></a>用來刪除次要站台的選項

您無法將次要站台移至或重新指派給另一個主要站台。 當從其直接父站台移除次要站台時，請選擇是否要將其解除安裝或刪除。

#### <a name="uninstall-the-secondary-site"></a>解除安裝次要站台

使用此選項以移除可從網路存取的正常運作次要站台。 此選項會從次要站台伺服器解除安裝 Configuration Manager。 接著，從 Configuration Manager 站台刪除該站台及其資源的所有資訊。

如果 Configuration Manager 為次要站台安裝了 SQL Server Express，則 Configuration Manager 也會解除安裝 SQL Express。 如果是在安裝次要站台之前安裝 SQL Server Express，則 Configuration Manager 不會解除安裝 SQL Server Express。

#### <a name="delete-the-secondary-site"></a>刪除次要站台

遇到下列狀況時，請使用此選項：

- 次要站台無法安裝

- 解除安裝次要站台之後，Configuration Manager 主控台仍然顯示次要站台

    此選項會從 Configuration Manager 階層中刪除該站台及其資源的所有資訊，但不會在站台伺服器上進行任何變更。

    > [!TIP]
    >  您也可以使用階層維護工具搭配 **/DELSITE** 選項來刪除次要站台。 如需詳細資訊，請參閱[階層維護工具 (Preinst.exe)](../../manage/hierarchy-maintenance-tool-preinst.exe.md)。

### <a name="prerequisites-to-delete-a-secondary-site"></a>刪除次要站台的先決條件

執行 Configuration Manager 安裝程式的系統管理使用者，需要下列安全性權限：

- 次要站台伺服器上的本機**系統管理員**權限

- 如果主要站台資料庫伺服器在主要站台伺服器遠端，則需要主要站台的遠端站台資料庫伺服器上本機**系統管理員**權限。

- 父主要站台上的 [基礎結構系統管理員]  或 [系統高權限管理員]  安全性角色

- 次要站台資料庫的**系統管理員** (Sysadmin) 權限

### <a name="procedure-to-delete-a-secondary-site"></a>刪除次要站台的先決條件

使用下列程序來解除安裝或刪除次要站台：

1. 在 Configuration Manager 主控台中，移至 [系統管理]  工作區，展開 [站台設定]  ，然後選取 [站台]  節點。

1. 選取您要移除的次要站台伺服器。 在功能區內 [常用]  索引標籤的 [站台]  群組中，選取 [刪除]  。

1. 在 [一般]  頁面上，選取要解除安裝或刪除次要站台。

1.  完成精靈。

## <a name="primary-site"></a><a name="bkmk_primary"></a> 主要站台  

基於下列原因，建議從階層中解除安裝主要站台：

- 合併站台以降低成本和複雜性
- 重新設定或重新設計階層的站台

如果子主要站台將[分散式檢視](../../../plan-design/hierarchy/database-replication.md#bkmk_distviews)用於 CAS 的複寫連結，則必須先關閉階層中的分散式檢視，才能解除安裝該站台。 如需詳細資訊，請參閱 [解除安裝以分散式檢視設定的主要站台](#bkmk_distviews)。

### <a name="plan-to-uninstall-a-primary-site"></a><a name="bkmk_pri-plan"></a> 規劃解除安裝主要站台

在解除安裝主要站台之前，請先檢閱下列工作：

- 檢閱界限、界限群組和後援關聯性。 如果將用戶端指派給新站台，但未變更界限，則可能將其視為漫遊。 如需詳細資訊，請參閱[定義站台界限與界限群組](../configure/define-site-boundaries-and-boundary-groups.md)。

- 確定所有作用中用戶端都會重新指派給階層中的另一個主要站台。 否則，在解除安裝站台之後，用戶端將變成非受控。 如需詳細資訊，請參閱[如何將用戶端指派至站台](../../../clients/deploy/assign-clients-to-a-site.md)。

  - 檢閱站台角色清單，確定新站台提供相同層級的服務。

  - 確定已使用其他站台中此角色來正確調整其他站台系統的大小。 這些站台系統必須與其他用戶端一起支援效能和可用性的商務需求。

  - 如果此站台有許多用戶端，請分階段加以重新指派。 當用戶端重新整理完整清查和其他站台特定資料時，請監視資料庫複寫。 如果管理軟體更新，則用戶端將會指派給新的軟體更新點。 此行為會導致完整掃描更新相容性。

  - 用戶端重新指派可能會影響依賴清查資料的報表和查詢，以及以狀態為基礎的相容性。 請考慮在轉換期間暫時調整任何用戶端週期。

  - 檢閱所有用戶端指派方法，以確定沒有方法參考這個主要站台。

- 檢查階層中任何使用中物件是否有站台碼的靜態參考。 例如，集合查詢、工作順序或系統管理指令碼。

- 如果階層使用[後援站台](../configure/boundary-group-procedures.md#bkmk_site-fallback)進行自動站台指派，請確定該階層不會參考這個主要站台。

- 重新設定可能會參考靜態站台碼的任何[用戶端安裝方法](../../../clients/deploy/plan/client-installation-methods.md)。

- 如果這個主要站台有任何站台特定的雲端附加服務，請務必將其移除。 如果仍然需要雲端資源，請將雲端資源移至階層中的另一個主要站台。 將這些雲端資源從所要解除安裝的主要站台中移除，並新增至另一個主要站台。

- 如果這個主要站台具有階層的任何[探索方法](../configure/run-discovery.md)，請將這些方法移至另一個站台。

- 淘汰任何以站台為基礎的 [OS 部署媒體](../../../../osd/deploy-use/create-task-sequence-media.md)。

- 從站台和站台伺服器解除安裝所有站台系統角色。 如需詳細資訊，請參閱[解除安裝站台系統角色](#bkmk_role)。 雖然這不是必要的準備步驟，但是在解除安裝站台之前，其有助於識別任何其他相依性。

- 解除安裝這個主要站台下的任何次要站台。 如需詳細資訊，請參閱[＜次要站台＞](#bkmk_secondary)一節。

### <a name="prerequisites-to-uninstall-a-primary-site"></a><a name="bkmk_pri-prereq"></a> 解除安裝主要站台的先決條件

執行 Configuration Manager 安裝程式的系統管理使用者需要下列安全性權限：

- CAS 伺服器的本機**系統管理員**權限

- 如果 CAS 資料庫伺服器在站台伺服器遠端，則需要 CAS 遠端站台資料庫伺服器的本機**系統管理員**權限。

- CAS 站台資料庫的**系統管理員** (Sysadmin) 權限

- 主要站台伺服器的本機**系統管理員**權限

- 如果主要站台資料庫伺服器在主要站台伺服器遠端，則需要主要站台的遠端站台資料庫伺服器上本機**系統管理員**權限。

- CAS 的**基礎結構系統管理員**或**系統高權限管理員**安全性角色

### <a name="procedure-to-uninstall-a-primary-site"></a><a name="bkmk_pri-process"></a> 解除安裝主要站台的程序

您會執行 Configuration Manager 安裝程式以解除安裝沒有相關聯次要站台的主要站台。 使用下列程序來解除安裝主要站台：

> [!TIP]
> 如果主要站台伺服器已無法使用，請使用 CAS 上的階層維護工具從站台資料庫中刪除主要站台。 如需詳細資訊，請參閱[階層維護工具 (Preinst.exe)](../../manage/hierarchy-maintenance-tool-preinst.exe.md)。

1. 使用下列其中一種方法，在主要站台伺服器上啟動 Configuration Manager 安裝程式：

    - 在 [開始]  功能表上，選取 [Configuration Manager 安裝程式]  。

    - 在 Configuration Manager 的「安裝媒體」  目錄中，開啟 `\SMSSETUP\BIN\X64\setup.exe`。 請確定此版本與站台版本相同。

    - 在 Configuration Manager 的「安裝」  目錄中，開啟 `\BIN\X64\setup.exe`。

1. 檢閱 [開始之前]  頁面上的資訊。

1. 在 [開始使用]  頁面上，選取 [解除安裝 Configuration Manager 站台]  。

    > [!IMPORTANT]  
    >  次要網站連結至主要網站時，您必須先移除次要網站才可解除安裝主要網站。  

1. 在 [解除安裝 Configuration Manager 站台]  頁面上，預設會啟用下列兩個選項：

    - 從主要站台伺服器移除站台資料庫
    - 移除 Configuration Manager 主控台

1. 選取 [是]  以確認解除安裝 Configuration Manager 主要站台。

### <a name="uninstall-a-primary-site-that-uses-distributed-views"></a><a name="bkmk_distviews"></a> 解除安裝使用分散式檢視的主要站台

1. 解除安裝子主要站台之前，請先關閉 CAS 與主要站台之間每個階層連結上的分散式檢視。

1. 關閉每個連結上的分散式檢視之後，請確認來自主要站台的資料已完成 CAS 重新初始化。 若要監視資料的初始化，請參閱[監視複寫](../../manage/monitor-replication.md)。

1. 在透過 CAS 成功將資料重新初始化之後，即可[解除安裝主要站台](#bkmk_pri-process)。

1. 解除安裝主要站台時，可重新設定 CAS 到其他主要站台連結上的分散式檢視。

    > [!IMPORTANT]
    > 如果在關閉每個站台的分散式檢視之前，或在來自主要站台的資料成功在 CAS 重新初始化之前就解除安裝主要站台，資料複寫可能會失敗。

## <a name="decommission-a-hierarchy"></a><a name="bkmk_hierarchy"></a> 解除委任階層

有些組織因為合併、收購、測試環境或其他商務需求而有多個階層。 如果將管理整合到單一階層，則此動作可協助降低成本和複雜性。 解除委任階層的另一個原因是，您正在移轉至僅限雲端的管理服務 (例如 Microsoft Intune)，並準備好移除內部部署基礎結構。

若要解除委任包含多個站台的階層，則移除順序十分重要。 從解除安裝階層底部的站台開始，然後向上進行：

1. 移除連接到主要站台的次要站台。
2. 解除安裝主要站台。
3. 解除安裝所有主要站台之後，即可解除安裝 CAS。

如需詳細資訊，請參閱下列各節：

- [移除次要站台](#bkmk_secondary)
- [解除安裝主要站台](#bkmk_primary)
- [解除安裝 CAS](#bkmk_uninstall-cas)

### <a name="uninstall-the-cas"></a><a name="bkmk_uninstall-cas"></a> 解除安裝 CAS

解除委任階層的最後一個步驟是解除安裝 CAS。 執行 Configuration Manager 安裝程式可解除安裝沒有子主要站台的 CAS。

#### <a name="prerequisites-to-uninstall-the-cas"></a>解除安裝 CAS 的先決條件

執行 Configuration Manager 安裝程式的系統管理使用者需要下列安全性權限：

- CAS 伺服器的本機**系統管理員**權限

- 如果 CAS 資料庫伺服器在站台伺服器遠端，則需要 CAS 遠端站台資料庫伺服器的本機**系統管理員**權限。

#### <a name="procedure-to-uninstall-the-cas"></a>解除安裝 CAS 的程序

1. 使用下列其中一種方法，在 CAS 伺服器上啟動 Configuration Manager 安裝程式：

    - 在 [開始]  功能表上，選取 [Configuration Manager 安裝程式]  。

    - 在 Configuration Manager 的「安裝媒體」  目錄中，開啟 `\SMSSETUP\BIN\X64\setup.exe`。 請確定此版本與站台版本相同。

    - 在 Configuration Manager 的「安裝」  目錄中，開啟 `\BIN\X64\setup.exe`。

1. 檢閱 [開始之前]  頁面上的資訊。

1. 在 [開始使用]  頁面上，選取 [解除安裝 Configuration Manager 站台]  。

    > [!IMPORTANT]  
    >  請先移除所有子主要站台，再解除安裝 CAS。  

1. 在 [解除安裝 Configuration Manager 站台]  頁面上，預設會啟用下列兩個選項：

    - 從 CAS 伺服器移除站台資料庫
    - 移除 Configuration Manager 主控台

1. 選取 [是]  以確認解除安裝 Configuration Manager 管理中心網站 (CAS)。

## <a name="remove-the-cas"></a><a name="bkmk_remove-cas"></a> 移除 CAS

<!-- 3607277 -->

從 2002 版開始，如果階層包含 CAS 和單一子主要站台，則可移除 CAS。 此動作會將 Configuration Manager 基礎結構簡化為單一獨立主要站台。 此動作會將站對站複寫的複雜性簡化，並將管理工作重點放在單一站台上。

如需詳細資訊，請參閱[移除 CAS](remove-central-administration-site.md)。
