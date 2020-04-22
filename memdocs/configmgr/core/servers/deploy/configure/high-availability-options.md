---
title: 高可用性
titleSuffix: Configuration Manager
description: 了解如何使用維持高可用度服務的選項部署 Configuration Manager。
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 1a38421d-24c1-4fef-bf6c-42fce53109ac
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 32083deb30d3d7345ccad8d31541d3c641eb10c0
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81707266"
---
# <a name="high-availability-options-for-configuration-manager"></a>Configuration Manager 的高可用性選項

適用於：  Configuration Manager (最新分支)

本文描述如何使用維持高可用度服務的選項部署 Configuration Manager。

下列 Configuration Manager 選項支援高可用性：

- 為所有獨立主要站台設定額外的被動模式站台伺服器。  

- 在主要站台和管理中心網站，為站台資料庫設定 SQL Server Always On 可用性群組。

- 站台可支援提供用戶端重要服務的多重站台系統角色執行個體。 例如，管理點及發佈點。  

- 管理中心網站和主要站台皆支援站台資料庫備份。 站台資料庫會儲存網站和用戶端的所有設定。 階層中的網站會共用此設定資料。  

- 內建的站台復原選項可降低伺服器停機時間。 當您在管理中心網站有階層時，這些進階選項可簡化復原程序。  

- 用戶端可以自動補救常見的問題，不需要系統管理員操作。  

- 站台會產生關於用戶端提交最近資料失敗的警示，以警告系統管理員可能有問題發生。  

- Configuration Manager 提供數種內建報表和儀表板。 使用它們能在問題影響到伺服器或用戶端操作之前就識別出問題與趨勢。  

Configuration Manager 包含數項提供近乎即時服務的功能。 如果這些功能是達到您商務需求的關鍵，請規劃並設定您的站台和階層以取得高可用性。 例如：  

- [用戶端通知動作](../../../clients/manage/manage-clients.md)，例如重新啟動、啟動 Windows Defender 掃描或遠端桌面。  

- 監視功能的狀態訊息，例如軟體更新和 Endpoint Protection。

- [指令碼](../../../../apps/deploy-use/create-deploy-scripts.md)

- [CMPivot](../../manage/cmpivot.md)

Configuration Manager 的其他功能不提供即時服務。 這些功能包括但不限於用戶端設定、硬體和軟體清查、軟體部署和合規性設定。 操作時會有一定程度的資料延遲。 多數涉及服務暫時中斷的情形通常不太會變成重大的問題。 若要將停機時間降到最低、維持自主性操作，並且提供高層級服務，請記得設定網站和階層的高可用性。  

例如，Configuration Manager 用戶端通常會使用已知的排程與操作設定進行自主性操作，並且排定將資料提交至站台處理的時程。  

- 當用戶端無法連絡站台時，便會快取待提交的資料，直到連絡上站台。  

- 無法連絡上站台的用戶端會繼續運作。 它們會使用最後一個已知的排程和快取的資訊，直到連絡上站台並接收新的原則。 例如，用戶端得留過去下載之必須執行或安裝的應用程式。

- 站台會監視其站台系統和用戶端的定期狀態更新。 無法註冊這些元件時會產生警示。  

- 內建報告可提供進行中操作、歷史操作與目前趨勢的深入探索。 Configuration Manager 也支援狀態訊息，其提供進行中操作的近即時資訊。  


## <a name="high-availability-for-sites-and-hierarchies"></a><a name="bkmk_snh"></a> 站台和階層的高可用性  

### <a name="use-a-site-server-in-passive-mode"></a>以被動模式使用站台伺服器

為獨立主要站台安裝額外的「被動」  模式站台伺服器。 被動模式的站台伺服器，是您現有「主動」  模式的站台伺服器以外的站台伺服器。 被動模式的站台伺服器可在有需要時立即使用。 如需詳細資訊，請參閱[站台伺服器高可用性](site-server-high-availability.md)。  

### <a name="use-a-remote-content-library"></a>使用遠端內容庫

將站台的內容庫移至遠端位置，其提供高度可用的儲存體。 這項功能是站台伺服器高可用性的需求。 如需詳細資訊，請參閱[內容庫](../../../plan-design/hierarchy/the-content-library.md#bkmk_remote)。

### <a name="centralize-content-sources"></a>集中內容的來源

Configuration Manager 中的所有軟體內容都需要有網路上的套件來源位置。 使用集中式的高度可用儲存體來裝載所有內容的常見套件來源位置。

### <a name="use-a-sql-server-always-on-availability-group-to-host-the-site-database"></a>使用 SQL Server Always On 可用性群組裝載站台資料庫

在 SQL Server Always On 可用性群組的主要站台和管理中心網站，裝載站台資料庫。 如需詳細資訊，請參閱[適用於高可用性站台資料庫的 SQL Server Always On](sql-server-alwayson-for-a-highly-available-site-database.md)。  

### <a name="use-a-sql-server-cluster-to-host-the-site-database"></a>使用 SQL Server 叢集裝載站台資料庫

當您將 SQL Server 叢集用於管理中心網站或次要站台的資料庫時，便會使用 SQL Server 內建的容錯轉移支援。  

次要站台無法使用 SQL Server 叢集，並且不支援站台資料庫的備份或還原。 從父主要站台重新安裝次要站台，以復原次要站台。  

### <a name="deploy-a-hierarchy-of-sites-with-a-central-administration-site-and-one-or-more-child-primary-sites"></a>使用管理中心網站及一個或多個子主要站台部署站台的階層

此設定可在您的站台管理網路的重疊區段時，提供容錯功能。 它也提供其他的復原選項，如此才能使用其他站台可用的共用資料庫資訊，藉以在復原的站台重建站台資料庫。 請使用此選項取代失敗或無法使用的失敗站台資料庫備份。  

### <a name="create-regular-backups-at-central-administration-sites-and-primary-sites"></a>在管理中心網站及主要站台建立標準備份

當您建立和測試定期站台備份時，這可確保您擁有復原站台的必要資料。 您也要練習在最短的時間內復原站台。  

### <a name="install-multiple-instances-of-site-system-roles"></a>安裝多重站台系統角色執行個體

當您安裝重要站台系統角色的多個執行個體時，您要提供用戶端的備援連絡點。 例如，多個管理點和發佈點可於特定伺服器離線時，提供備援服務。  

### <a name="install-multiple-instances-of-the-sms-provider-at-a-site"></a>在站台安裝多重 SMS 提供者執行個體

SMS 提供者會為一或多個 Configuration Manager 主控台提供系統管理連絡點。 請安裝多重 SMS 提供者，以提供備援連絡點管理您的站台和階層。  


## <a name="high-availability-for-site-system-roles"></a><a name="bkmk_ssr"></a> 站台系統角色的高可用性

在各個站台，您可以部署站台系統角色以提供您要用戶端在該站台使用的服務。 站台資料庫中包含站台與所有用戶端的設定資訊。 使用一個或多個可用選項，提供站台資料庫的高可用性，如有必要也可提供站台與站台資料庫的復原。  

### <a name="redundancy-for-important-site-system-roles"></a>重要站台系統角色的複本

- 應用程式類別目錄 Web 服務點  

- 應用程式類別目錄網站點  

- 發佈點  

- 管理點  

- 軟體更新點  

- 狀態移轉點  

請安裝多個 Reporting Services 點的執行個體，以為站台和用戶端上的報告提供備援。

如需軟體更新點的容錯移轉支援，請使用 Windows PowerShell 將此角色安裝在 Windows 網路負載平衡 (NLB) 叢集上。  

### <a name="built-in-site-backup"></a>內建站台備份

Configuration Manager 包含內建的備份工作，可協助您依定期排程備份站台及重要資訊。 此外，Configuration Manager 安裝精靈支援站台還原動作，協助您將網站還原作業。  

### <a name="publishing-to-active-directory-domain-services-and-dns"></a>發佈至 Active Directory 網域服務及 DNS

設定每個站台都要將站台資料發佈至 Active Directory 網域服務和 DNS。 此發佈可讓用戶端找到網路上最容易存取的伺服器。 用戶端也可以使用它找到提供重要服務的可用新站台系統伺服器，例如管理點。  

### <a name="sms-provider-and-configuration-manager-console"></a>SMS 提供者與 Configuration Manager 主控台

Configuration Manager 支援在不同的伺服器上安裝多個 SMS 提供者，當成主控台的多個存取點。 如果某個 SMS 提供者伺服器離線，您仍然可以檢視與管理網站和用戶端。  

當 Configuration Manager 主控台連線至站台時，它會連線至該站台的 SMS 提供者的執行個體。 隨機選取 SMS 提供者的執行個體。 如果選取的 SMS 提供者無法使用，下列選項可供您選擇：  

- 將主控台重新連線至站台。 每個新連線要求的 SMS 提供者執行個體都是隨機指派。 新的連線有可能獲指派可用的執行個體。  

- 將主控台連線到不同的 Configuration Manager 站台，並從該連線管理設定。 此選項會使設定變更稍微延遲幾分鐘。 在站台的 SMS 提供者上線後，請直接將 Configuration Manager 主控台重新連線至您要管理的站台。  

請在多部電腦上安裝 Configuration Manager 主控台，以供系統管理員使用。 各個 SMS 提供者皆支援來自多重主控台的連線。  

### <a name="management-point"></a>管理點

在各個主要站台上安裝多個管理點，並且使站台將站台資料發佈至 Active Directory 基礎結構及 DNS。  

多個管理點有助於平衡多用戶端使用單一管理點時的負載。 亦請考慮為管理點安裝一或多個資料庫複本。 此設定可減少管理點的處理器密集作業。 它也會提高此重要站台系統角色的可用性。  

次要站台只支援安裝一個管理點，它必須位在次要站台伺服器上。 次要站台上的管理點不被認為具有高可用設定。  

> [!NOTE]  
> 內部部署行動裝置管理所管理的裝置只能連接到主要站台的一個管理點。 管理點是由 Configuration Manager 在註冊期間指派至行動裝置，不會變更。 當您安裝多個管理點，並且啟用一個以上的行動裝置時，指派至行動裝置用戶端的管理點不具有確定性。  
>
> 如果行動裝置所使用的管理點變成無法使用，您必須解決該管理點的問題，或是清除行動裝置並重新註冊行動裝置，以便它可以重新指派至針對行動裝置啟用的操作管理點。  

### <a name="distribution-point"></a>發佈點

安裝多個發佈點，並將內容部署至多個發佈點。 每個界限群組新增一個以上的發佈點，可確保用戶端在其內容要求中取得數個選項。 設定界限群組關聯性，以便它們對另一個界限群組或雲端發佈點有可預測的後援行為。 如需詳細資訊，請參閱[設定界限群組](boundary-groups.md)。  

### <a name="application-catalog-web-service-point-and-application-catalog-website-point"></a>應用程式類別目錄 Web 服務點與應用程式類別目錄網站點

> [!Important]
> 從 1806 最新分支版本開始即不支援應用程式類別目錄的 Silverlight 使用者體驗。 從 1906 版開始，已更新的用戶端會自動使用適用於使用者可用應用程式部署的管理點。 此外，您也無法安裝新的應用程式目錄角色。 1910 版會終止對應用程式類別目錄角色的支援。  
>
> 如需詳細資訊，請參閱下列文章：
>
> - [設定軟體中心](../../../../apps/plan-design/plan-for-software-center.md#bkmk_userex)
> - [已移除和已淘汰的功能](../../../plan-design/changes/deprecated/removed-and-deprecated-cmfeatures.md)  

每個站台系統角色安裝一個以上的執行個體。 請在相同的站台系統伺服器每種部署一個，以達到最佳效能。  

不論此角色在階層中的位置為何，每個應用程式類別目錄站台系統角色提供的資訊都與該角色的其他執行個體相同。 當用戶端要求應用程式類別目錄，而您已經設定用戶端自動偵測預設的應用程式類別目錄網站點時，用戶端會導向至可用的執行個體。 用戶端根據其目前的網路位置，慣用本機應用程式類別目錄執行個體。  

如需有關此用戶端設定與自動偵測運作方式的詳細資訊，請參閱[電腦代理程式](../../../clients/deploy/about-client-settings.md#computer-agent)用戶端設定。  


## <a name="high-availability-for-clients"></a><a name="bkmk_client"></a> 用戶端的高可用性  

### <a name="client-operations-are-autonomous"></a>用戶端作業是自主性的

Configuration Manager 用戶端自主性包括下列行為︰  

- 用戶端不會要求持續與任何特定站台系統伺服器連絡。 用戶端會使用已知設定，按照排程執行預先設定的動作。  

- 用戶端可以使用任何可用的站台系統角色執行個體，向用戶端提供服務。 它們會嘗試連絡已知的伺服器，直到找到可用的伺服器為止。  

- 用戶端可以執行清查、軟體部署以及類似的排程動作，不需要直接與站台系統伺服器連絡。  

- 設定為使用後援狀態點的用戶端，可以在無法與管理點通訊時，將詳細資料提交給後援狀態點。  

### <a name="clients-can-repair-themselves"></a>用戶端能夠自行修復

用戶端可以自動補救多數常見的問題，不需要系統管理者直接操作。  

- 用戶端會定期自我評估狀態。 它們會使用補救步驟的本機快取以及需修復的來源檔案，進行常見問題的補救動作。  

- 當用戶端無法提交狀態資訊至其站台時，站台會產生警示。 接收這些警示的系統管理使用者，可以立即採取動作，以還原用戶端的正常操作。  

### <a name="clients-cache-information-to-use-in-the-future"></a>未來使用的用戶端快取資訊

當用戶端與管理點通訊時，用戶端可以取得並快取以下資訊：  

- 用戶端設計  

- 用戶端排程  

- 針對此動作設定部署時，有關軟體部署與用戶端排定安裝之軟體下載的資訊。  

當用戶端無法連絡管理點時，用戶端會在本機快取狀態、狀況，以及對站台報告的用戶端資訊。 用戶端會在與管理點建立連絡之後，傳送此資料。  

### <a name="client-can-submit-status-to-a-fallback-status-point"></a>用戶端可以將狀態提交至後援狀態點

當您將用戶端設定為使用後援狀態點時，便會提供額外的連絡點讓用戶端提交有關其操作的重要詳細資料。 即使在用戶端無法與管理點通訊時，設定為使用後援狀態點的用戶端也會持續傳送有關其操作的狀態至其站台系統角色。  

### <a name="central-management-of-client-data-and-client-identity"></a>用戶端資料與用戶端識別身分的中央管理

站台資料庫 (而非個別用戶端) 會保留有關各個用戶端識別身分的資訊，並且為該資料與特定電腦或使用者建立關聯性。  

- 電腦上的用戶端來源檔案可以解除安裝與重新安裝，完全不會影響用戶端安裝所在電腦的歷程記錄。  

- 用戶端電腦的失敗並不影響資料庫中所儲存的資訊完整性。 此資訊仍可供報告使用。  


## <a name="options-for-sites-and-site-system-roles-that-arent-highly-available"></a><a name="bkmk_nonHAoptions"></a> 不具高度可用性的站台與站台系統角色的選項

某些站台系統並不支援站台或階層內的多個執行個體。 此資訊可協助您準備這些要離線的站台系統。  

### <a name="asset-intelligence-synchronization-point-hierarchy"></a>Asset Intelligence 同步處理點 (階層)

此站台角色並非關鍵角色，而且提供 Configuration Manager 中的選用功能。 如果此站台系統離線，請使用下列其中一個選項：  

- 解析站台系統離線的原因。  

- 從目前伺服器解除安裝角色，並且在新伺服器上安裝角色。  

### <a name="endpoint-protection-point-hierarchy"></a>Endpoint Protection 點 (階層)

此站台角色並非關鍵角色，而且提供 Configuration Manager 中的選用功能。 如果此站台系統離線，請使用下列其中一個選項：  

- 解析站台系統離線的原因。  

- 從目前伺服器解除安裝角色，並且在新伺服器上安裝角色。  

### <a name="enrollment-point-site"></a>註冊點 (站台)

此站台角色並非關鍵角色，而且提供 Configuration Manager 中的選用功能。 如果此站台系統離線，請使用下列其中一個選項：  

- 解析站台系統離線的原因。  

- 從目前伺服器解除安裝角色，並且在新伺服器上安裝角色。  

### <a name="enrollment-proxy-point-site"></a>註冊 Proxy 點 (站台)

此站台角色並非關鍵角色，而且提供 Configuration Manager 中的選用功能。 但是，您可以在一個站台以及階層中的多個站台安裝此站台系統角色的多個執行個體。 如果此站台系統離線，請使用下列其中一個選項：  

- 解析站台系統離線的原因。  

- 從目前伺服器解除安裝角色，並且在新伺服器上安裝角色。  

站台中有一個以上的註冊 Proxy 伺服器時，伺服器名稱請使用 DNS 別名。 如果您使用此設定，DNS 循環配置資源會在使用者註冊其行動裝置時，提供部分容錯與負載平衡。  

### <a name="fallback-status-point-site-or-hierarchy"></a>後援狀態點 (站台或階層)

此站台角色並非關鍵角色，而且提供 Configuration Manager 中的選用功能。 如果此站台系統離線，請使用下列其中一個選項：  

- 解析站台系統離線的原因。  

- 從目前伺服器解除安裝角色，並且在新伺服器上安裝角色。 由於用戶端在用戶端安裝期間已接受後援狀態點的指派，因此您必須修改現有用戶端以使用新的站台系統伺服器。  

### <a name="service-connection-point-hierarchy"></a>服務連線點設定 (階層)

雖然此站台系統角色對將 Configuration Manager 最新分支保持在最新狀態至關重要，但它一般很少使用。 如果此系統離線，請使用下列其中一個選項：

- 解析站台系統離線的原因。  

- 從目前伺服器解除安裝角色，並且在新伺服器上安裝角色。  


## <a name="see-also"></a>請參閱

- [支援的設定](../../../plan-design/configs/supported-configurations.md)  

- [建議的硬體](../../../plan-design/configs/recommended-hardware.md)  

- [支援的站台系統伺服器作業系統](../../../plan-design/configs/supported-operating-systems-for-site-system-servers.md)

- [站台和站台系統必要條件](../../../plan-design/configs/site-and-site-system-prerequisites.md)  

- [站台失敗影響](../../manage/site-failure-impacts.md)  
