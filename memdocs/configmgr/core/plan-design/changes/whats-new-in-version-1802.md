---
title: 新版本 1802
titleSuffix: Configuration Manager
description: 取得 Configuration Manager 1802 版中變更和所引進新功能的詳細資料。
ms.date: 10/09/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 5bd637b1-d7a1-411b-877a-c7aae9741173
author: mestew
ms.author: mstewart
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: 11066470347db0f3ffbfadda9897aed92baa645b
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2020
ms.locfileid: "82073597"
---
# <a name="whats-new-in-version-1802-of-configuration-manager"></a>Configuration Manager 1802 版中的新功能

適用於：  Configuration Manager (最新分支)

Configuration Manager 最新分支的 1802 更新可以主控台內更新的方式取得。 在執行 1702、1706 或 1710 版的站台上套用此更新。 <!-- baseline only statement: -->在安裝新站台時，也可以基準版本的形式取得。

除了新功能之外，此版本也包含錯誤修正等其他變更。 如需詳細資訊，請參閱 [Configuration Manager 最新分支 1802 版中變更的摘要](https://support.microsoft.com/help/4101375) \(機器翻譯\)。

下列針對此版本的其他變更也已可供使用：
- [適用於 Configuration Manager 最新分支 1802 版的更新彙總套件](https://support.microsoft.com/help/4163547) \(機器翻譯\)

> [!TIP]  
> 若要安裝新的站台，您必須使用 Configuration Manager 的基準版本。  
>
> 深入了解：    
> - [安裝新的站台](../../servers/deploy/install/installing-sites.md)  
> - [在站台安裝更新](../../servers/manage/updates.md)  
> - [基準和更新版本](../../servers/manage/updates.md#bkmk_Baselines)

以下各節提供 Configuration Manager 1802 版中的變更和新功能的詳細資料。  

<!--
## Deprecated features and operating systems
Learn about support changes before they are implemented in [removed and deprecated items](deprecated/removed-and-deprecated.md).

Version 1802 drops support for the following products:
-->


## <a name="site-infrastructure"></a>站台基礎結構

### <a name="reassign-distribution-point"></a>重新指派發佈點
<!-- 1306937 -->
許多客戶擁有大型的 Configuration Manager 基礎結構，並會減少主要或次要站台，以簡化其環境。 他們仍然需要保留分公司位置的發佈點，以提供內容給受控的用戶端。 這些發佈點通常包含數 TB 以上的內容。 此內容在散發到這些遠端伺服器時會耗用大量時間和網路頻寬。 這項功能可讓您將發佈點重新指派給其他主要站台，而不需要重新發佈內容。 此動作會更新站台系統指派，同時保存伺服器上的所有內容。 如需詳細資訊，請參閱[重新指派發佈點](../../servers/deploy/configure/install-and-configure-distribution-points.md#bkmk_reassign)。

### <a name="configure-windows-delivery-optimization-to-use-configuration-manager-boundary-groups"></a>設定 Windows 傳遞最佳化以使用 Configuration Manager 界限群組
<!-- 1324696 -->
您可以使用 Configuration Manager 界限群組，來定義和規範在您的公司網路上以及到遠端辦公室的內容發佈。 [Windows 傳遞最佳化](/windows/deployment/update/waas-delivery-optimization)是一種雲端式點對點技術，可在 Windows 10 裝置之間共用內容。 從這個版本開始，設定傳遞最佳化，以便在同儕節點之間共用內容時使用界限群組。 新的用戶端設定會套用界限群組識別碼，以作為用戶端上的傳遞最佳化群組識別碼。 當用戶端與傳遞最佳化雲端服務進行通訊時，它會使用此識別碼來尋找含有所需內容的同儕節點。 如需詳細資訊，請參閱[內容管理的基本概念](../hierarchy/fundamental-concepts-for-content-management.md#delivery-optimization)。

### <a name="support-for-windows-10-arm64-devices"></a>支援 Windows 10 ARM64 裝置
<!-- 1353704 -->
從這個版本開始，Windows 10 ARM64 裝置上便支援 Configuration Manager 用戶端。 現有的用戶端管理功能應該可以使用這些新的裝置來運作。 例如，硬體和軟體清查、軟體更新以及應用程式管理。 目前不支援作業系統部署。 

### <a name="improved-support-for-cng-certificates"></a>已改善對 CNG 憑證的支援
<!-- 1357314 -->
Configuration Manager (最新分支) 1710 版支援[密碼編譯：新一代 (CNG) 憑證](../network/cng-certificates-overview.md)。 1710 版會在數種案例中限制對用戶端憑證的支援。 

從這個版本開始，請針對以下啟用 HTTPS 的伺服器角色使用 CNG 憑證：
- 管理點
- 發佈點
- 軟體更新點
- 狀態移轉點  


### <a name="boundary-group-fallback-for-management-points"></a>管理點的界限群組後援
<!-- 1324594 -->
針對[界限群組](../../servers/deploy/configure/boundary-groups.md)之間的管理點來設定後援關聯性。 此行為可為用戶端使用的管理點提供更好的控制。 如需詳細資訊，請參閱[設定界限群組](../../servers/deploy/configure/boundary-groups.md#management-points)。


### <a name="cloud-distribution-point-site-affinity"></a>雲端發佈點站台親和性
<!--503719-->
此功能對於使用雲端發佈點且具有多個站台、地理位置分散階層的客戶非常有用。 當網際網路型用戶端搜尋內容時，之前用戶端接收到的雲端發佈點清單並沒有排序。 此行為可能導致網際網路型用戶端接收到來自遠方地理位置雲端發佈點的內容。 從遠方伺服器下載內容通常比從距離近伺服器下載來得慢。
 
使用雲端發佈點站台親和性之後，網際網路型用戶端會收到已排序的清單。 此清單會針對用戶端指派的站台，為雲端發佈點設定優先順序。 此行為可讓系統管理員維持其內容從站台資源下載的設計目的。
 

## <a name="management-insights"></a>Management Insights
<!-- 1353967 -->
Configuration Manager 中的管理見解提供您環境目前狀態的相關資訊。 此資訊是以站台資料庫的資料分析為基礎。 深入解析可協助您進一步了解您的環境，並據以採取行動。 如需詳細資訊，請參閱[管理深入解析](../../servers/manage/management-insights.md)

Configuration Manager 1802 中提供以下深入解析：
- 應用程式：
    - 沒有部署的應用程式
- 雲端服務： <!--1356412-->
    - 評估共同管理整備程度 
    - 讓您的裝置能夠加入混合式 Azure Active Directory
    - 將您的身分識別與存取基礎結構現代化
    -  將您的用戶端升級到 Windows 10 (1709 版或更新版本) 
- 集合：
    - 空集合
- 簡化的管理：  <!--1355148-->
    - 已淘汰的用戶端版本  
- 軟體中心： 
    - 將使用者導向到軟體中心，而不是應用程式類別目錄  
    - 使用新版的軟體中心 
- Windows 10： <!--1357421-->
    - 設定 Windows 遙測和商用識別碼金鑰 
    - 將 Configuration Manager 連線至更新整備小幫手 
   
<!-- ## Migration  -->



## <a name="client-management"></a>用戶端管理

### <a name="cloud-management-gateway-support-for-azure-resource-manager"></a>Azure Resource Manager 的雲端管理閘道支援
<!-- 1324735 -->
建立[雲端管理閘道](../../clients/manage/cmg/plan-cloud-management-gateway.md) (CMG) 的執行個體時，精靈現在會提供選項來建立 **Azure Resource Manager 部署**。 [Azure Resource Manager](/azure/azure-resource-manager/resource-group-overview) 是可將所有解決方案資源當作單一實體 (稱為[資源群組](/azure/azure-resource-manager/resource-group-overview#resource-groups)) 來管理的新式平台。 使用 Azure Resource Manager 部署 CMG 時，站台會使用 Azure Active Directory (Azure AD) 來驗證並建立必要的雲端資源。 這個現代化的部署不需要傳統的 Azure 管理憑證。 如需詳細資訊，請參閱 [CMG 拓樸設計](../../clients/manage/cmg/plan-cloud-management-gateway.md#azure-resource-manager)。

> [!IMPORTANT]
> 此功能不會啟用對 Azure 雲端服務提供者 (CSP) 的支援。 含 Azure Resource Manager 的 CMG 部署會繼續使用 CSP 不支援的傳統雲端服務。 如需詳細資訊，請參閱 [Azure CSP 中可用的 Azure 服務](/azure/cloud-solution-provider/overview/azure-csp-available-services)。  

### <a name="improvements-to-cloud-management-gateway"></a>雲端管理閘道的改進  

- 從這個版本開始，**雲端管理閘道**已不再是發行前版本功能。  

- 該功能的文件已修改並增強。 如需詳細資訊，請參閱下列文章：
    - [規劃雲端管理閘道](../../clients/manage/cmg/plan-cloud-management-gateway.md)
    - [雲端管理閘道的大小和規模數量](../configs/size-and-scale-numbers.md#bkmk_cmg)
    - [雲端管理閘道器的安全性和隱私權](../../clients/manage/cmg/security-and-privacy-for-cloud-management-gateway.md)
    - [雲端管理閘道的相關常見問題集](../../clients/manage/cmg/cloud-management-gateway-faq.md)
    - [雲端管理閘道的憑證](../../clients/manage/cmg/certificates-for-cloud-management-gateway.md)
    - [設定雲端管理閘道](../../clients/manage/cmg/setup-cloud-management-gateway.md)  


### <a name="configure-hardware-inventory-to-collect-strings-larger-than-255-characters"></a>將硬體清查設定成收集大於 255 個字元的字串
<!-- 1357389 -->
您可以針對硬體清查屬性，將字串的長度設定為大於 255 個字元。 此變更只會套用到新加入的類別，以及不是索引鍵的硬體清查屬性。 如需詳細資訊，請參閱[擴充硬體清查](../../clients/manage/inventory/extend-hardware-inventory.md#bkmk_GreaterThan255)一文。 

 ### <a name="deprecation-announcement-for-linux-and-unix-client-support"></a>Linux 和 Unix 用戶端支援的淘汰通知
 <!--510139-->
Microsoft 將在一年左右淘汰 Configuration Manager 中的 Linux 和 UNIX 用戶端支援，因此這些用戶端將不會包含在 2019 年初推出的 1902 版中。 Configuration Manager 1810 版 (2018 年後期) 將是包含 Linux 和 UNIX 用戶端的最後一個版本，而且在完整的 Configuration Manager 1810 生命週期內都會受到支援。 在 Configuration Manager 1810 之後，客戶應考慮以 Microsoft Azure 管理來管理 Linux 伺服器。 Azure 解決方案具有廣泛的 Linux 支援，在大部分情況下都超越 Configuration Manager 的功能性，包括 Linux 的完整修補程式管理。

### <a name="surface-device-dashboard"></a>Surface 裝置儀表板
<!--1355788-->
Surface 裝置儀表板提供在您的環境中找到的 Surface 裝置相關資訊。 在主控台中，移至 [監視]   > [Surface Devices] \(Surface 裝置)  。 您可以檢視以下項目：
- Surface 百分比
- Surface 模型的百分比
- 前五個韌體版本

如需詳細資訊，請參閱 [Surface 儀表板](../../clients/manage/surface-device-dashboard.md)一文。

### <a name="change-in-the-configuration-manager-client-install"></a>Configuration Manager 用戶端安裝中的變更
<!--1356195-->
從這個版本開始，將不再於用戶端裝置上自動安裝 Silverlight。 如需詳細資訊，請參閱[將用戶端部署到 Windows 電腦的必要條件](../../clients/deploy/prerequisites-for-deploying-clients-to-windows-computers.md#bkmk_ExternalDependencies)

## <a name="co-management"></a>共同管理

### <a name="transition-endpoint-protection-workload-to-intune-using-co-management"></a>使用共同管理將 Endpoint Protection 工作負載轉換至 Intune
<!-- 1357365 -->
 啟用共同管理之後，可將 Endpoint Protection 工作負載轉換到 Intune。 若要轉換 Endpoint Protection 工作負載，移至共同管理內容頁面，然後將滑動軸從 Configuration Manager 移至 [試驗]  或 [全部]  。 如需有關工作負載的詳細資料，請參閱[共同管理工作負載](../../../comanage/workloads.md)。 如需共同管理的詳細資訊，請參閱 [Windows 10 裝置的共同管理](../../../comanage/overview.md)。
 
### <a name="co-management-dashboard-in-configuration-manager"></a>Configuration Manager 中的共同管理儀表板
<!--1356648-->
從這個版本開始，您可以檢視含有共同管理相關資訊的儀表板。 該儀表板可協助您檢閱在環境中共同管理的機器。 圖形有助於識別可能需要注意的裝置。 如需詳細資訊，請參閱[共同管理儀表板](../../../comanage/how-to-monitor.md#co-management-dashboard)一文。 


## <a name="compliance-settings"></a>相容性設定

### <a name="microsoft-edge-browser-policies"></a>Microsoft Edge 瀏覽器原則
<!-- 1357310 -->
針對在 Windows 10 用戶端上使用 [Microsoft Edge](https://technet.microsoft.com/microsoft-edge/bb265256) 網頁瀏覽器的客戶，請建立 Configuration Manager 合規性設定原則來設定數個 Microsoft Edge 設定。 如需詳細資訊，請參閱[建立 Microsoft Edge 瀏覽器的設定檔](../../../compliance/deploy-use/browser-profiles.md)。 



## <a name="application-management"></a>應用程式管理

### <a name="allow-user-interaction-when-installing-an-application"></a>在安裝應用程式時允許使用者互動
<!-- 1356976 -->
允許使用者在工作順序執行其間與應用程式安裝互動。 例如，執行安裝程序，以向終端使用者提示各種選項。 某些應用程式安裝程式無法轉為無使用者提示，或者安裝流程可能需要只有使用者才知道的特定設定值。 這項功能可讓您處理這些安裝案例。 如需詳細資訊，請參閱[針對部署類型指定使用者體驗選項](../../../apps/deploy-use/create-applications.md#bkmk_dt-ux)。

### <a name="do-not-automatically-upgrade-superseded-applications"></a>不會自動升級已取代的應用程式
<!-- 1351266 -->
設定一個不會自動升級任何已被取代之版本的應用程式部署。 現在在建立部署時，在 [部署軟體精靈]  的 [部署設定]  頁面中，基於**可用**安裝目的，您可以啟用或停用 [自動升級此應用程式的任何已取代版本]  選項。 如需詳細資訊，請參閱[指定部署設定](../../../apps/deploy-use/deploy-applications.md#bkmk_deploy-settings)。

### <a name="approve-application-requests-for-users-per-device"></a>針對每個裝置的使用者核准應用程式要求
<!-- 1357015 -->
從這個版本開始，當使用者要求需要核准的應用程式時，特定的裝置名稱現在為要求的一部分。 如果系統管理員核准要求，使用者就只能在該裝置上安裝應用程式。 使用者必須提交其他要求，才能在其他裝置上安裝應用程式。 如需詳細資訊，請參閱[指定部署設定](../../../apps/deploy-use/deploy-applications.md#bkmk_deploy-settings)。

 > [!Note]  
 > 這是選擇性的功能。 如需詳細資訊，請參閱[從更新啟用選擇性功能](../../servers/manage/install-in-console-updates.md#bkmk_options)。  


### <a name="run-scripts-improvements"></a>執行指令碼的改進 
<!-- 1236459 -->
 從這個版本開始，**執行指令碼**不再是發行前版本功能。 指令碼輸出現在會使用 JSON 格式來傳回。 如需詳細資訊，請參閱[從 Configuration Manager 主控台建立及執行 PowerShell 指令碼](../../../apps/deploy-use/create-deploy-scripts.md)。


## <a name="operating-system-deployment"></a>作業系統部署

### <a name="windows-10-in-place-upgrade-task-sequence-via-cloud-management-gateway"></a>透過雲端管理閘道的 Windows 10 就地升級工作順序
<!-- 1357149 -->
Windows 10 [就地升級工作順序](../../../osd/deploy-use/upgrade-windows-to-the-latest-version.md)現在支援部署到以網際網路為基礎且透過[雲端管理閘道](../../clients/manage/cmg/plan-cloud-management-gateway.md)管理的用戶端。 此功能讓遠端使用者可以更輕鬆地升級到 Windows 10，而不需連線到公司網路。 如需詳細資訊，請參閱 [Deploy a task sequence](../../../osd/deploy-use/deploy-a-task-sequence.md)。

### <a name="improvements-to-windows-10-in-place-upgrade-task-sequence"></a>Windows 10 就地升級工作順序的改善
<!-- 1357425 -->
Windows 10 就地升級的預設工作順序範本現在包含其他群組，其中具有要在升級程序前後新增的建議動作。 這些動作在許多已順利升級到 Windows 10 裝置的客戶之間是通用的。 如需詳細資訊，請參閱[建立工作順序以升級作業系統](../../../osd/deploy-use/create-a-task-sequence-to-upgrade-an-operating-system.md#recommended-task-sequence-steps-to-prepare-for-upgrade)。

### <a name="improvements-to-operating-system-deployment"></a>作業系統部署增強功能
此版本包含作業系統部署的下列改善︰
- 在 Windows PE 中，當啟動 cmtrace.exe 時，不會再提示您選擇是否要將此程式設定為預設的記錄檔檢視器。 <!-- SMS 500897 -->
- 將開機映像新增到[下載套件內容](../../../osd/understand/task-sequence-steps.md#BKMK_DownloadPackageContent)工作順序步驟中。
- [執行工作順序](../../../osd/understand/task-sequence-steps.md#child-task-sequence)步驟的改進： <!-- 1261338 -->   
  - 軟體中心、PXE 和媒體中的所有作業系統部署案例支援。
  - 改善主控台動作，例如複製、匯入、匯出，以及物件刪除期間的警告。
  - 支援[建立預先設置的內容檔案](../hierarchy/manage-network-bandwidth.md#BKMK_PrestagingContent)精靈。
  - 與部署驗證的整合。 如需詳細資訊，請參閱[高風險工作順序部署](../../../osd/deploy-use/deploy-a-task-sequence.md)。 
  - 執行工作順序步驟現在可以跨多層的工作順序使用，而不只是單一父子式關聯性。 多層關聯性會增加複雜度，因此請謹慎使用。 仍然會檢查這些關聯性的循環參考。

### <a name="deployment-templates-for-task-sequences"></a>工作順序的部署範本
<!-- 1357391 -->
[工作順序的部署精靈](../../../osd/deploy-use/deploy-a-task-sequence.md)現在可以建立部署範本。 該部署範本可以儲存並套用到現有或新的工作順序來建立部署。 

### <a name="phased-deployments-for-task-sequences"></a>工作順序的分階段部署
<!--1356837-->
 分階段部署是[發行前版本功能](../../servers/manage/pre-release-features.md)。 分階段部署可跨越多個集合，自動化協調循序的工作順序推出。 您可以使用預設的兩個階段，或手動設定多個階段來[建立分階段部署](../../../osd/deploy-use/create-phased-deployment-for-task-sequence.md)。 工作順序的階段式部署不支援 PXE 或媒體安裝。




## <a name="software-center"></a>軟體中心

### <a name="install-multiple-applications-in-software-center"></a>在軟體中心安裝多個應用程式
<!-- 1357126 -->
如果使用者或桌面電腦技術人員需要在裝置上安裝多個應用程式，軟體中心現在支援安裝多個選取的應用程式。 因為不用等待安裝完一項後再開始下一項，所以此行為可以讓使用者更有效率。 如需詳細資訊，請參閱新的軟體中心使用者指南中的[安裝多個應用程式](../../understand/software-center.md#install-multiple-applications)。

### <a name="use-software-center-to-browse-and-install-user-available-applications-on-azure-ad-joined-devices"></a>在已加入 Azure AD的裝置上使用軟體中心瀏覽和安裝使用者可用的應用程式
<!-- 1322613 -->
如果您將可用的應用程式部署至使用者，他們現在就能在 Azure Active Directory (Azure AD) 裝置上，透過軟體中心瀏覽和安裝這些應用程式。 如需詳細資訊，請參閱[在已加入 Azure AD 的裝置上部署使用者可用的應用程式](../../../apps/deploy-use/deploy-applications.md#deploy-user-available-applications-on-azure-ad-joined-devices)。

### <a name="hide-installed-applications-in-software-center"></a>在軟體中心中隱藏已安裝的應用程式
<!--1357592-->
現在可以在軟體中心內隱藏已安裝的應用程式。 當此選項在用戶端設定底下啟用之後，已經安裝的應用程式就不會再顯示於 [應用程式] 索引標籤中。 當您安裝或升級至 Configuration Manager 1802 時，此選項會設定為預設值。  在 [安裝狀態] 索引標籤下，仍然得以檢閱已安裝的應用程式。[在軟體中心中隱藏已安裝的應用程式](../../clients/deploy/about-client-settings.md#bkmk_HideInstalled)具有其他詳細資料。   

### <a name="hide-unapproved-applications-in-software-center"></a>在軟體中心中隱藏未核准的應用程式
 <!--1355146-->
當啟用此用戶端設定選項時，針對使用者可用的應用程式，軟體中心會隱藏需要核准的應用程式。  [在軟體中心中隱藏未核准的應用程式](../../clients/deploy/about-client-settings.md#bkmk_HideUnapproved)具有其他詳細資訊。  

### <a name="software-center-shows-user-additional-compliance-information"></a>軟體中心會向使用者顯示其他合規性資訊
<!-- 1235616 -->
 當使用裝置健康情況證明狀態當作對公司資源進行條件存取的合規性政策時，軟體中心現在會顯示不合規的裝置健康情況證明設定。


 ## <a name="software-updates"></a>軟體更新 

### <a name="schedule-automatic-deployment-rule-evaluation-to-be-offset-from-a-base-day"></a>排程自動部署規則評估從基準日算起的偏移。 
<!--1357133-->
可以排程自動部署規則，以評估從基準日算起的偏移。 也就是說，如果星期二的修補程式實際上落在星期三，評估排程可以設為該月份的第二個星期二再偏移一天。 如需詳細資訊，請參閱[自動部署軟體更新](../../../sum/deploy-use/automatically-deploy-software-updates.md#BKMK_CreateAutomaticDeploymentRule)。 



## <a name="reporting"></a>報告

### <a name="report-for-default-browser-counts"></a>報告預設瀏覽器計數
<!-- 1357830 -->
現在有一份新報表，可顯示使用特定網頁瀏覽器作為 Windows 預設值之用戶端的計數。 請參閱 [軟體 - 公司與產品]  報表群組中的 [預設瀏覽器計數]  報表。 如需詳細資訊，請參閱[報表清單](../../servers/manage/list-of-reports.md#software---companies-and-products)。

### <a name="report-on-windows-autopilot-device-information"></a>Windows Autopilot 裝置資訊報告
<!-- 1351442 -->
Windows Autopilot 是使用新式方法讓新的 Windows 10 裝置上線並加以設定的解決方案。 如需詳細資訊，請參閱 [Windows Autopilot 概觀](https://docs.microsoft.com/windows/deployment/windows-autopilot/windows-10-autopilot)。 向 Windows Autopilot 註冊現有裝置的方法之一是，將裝置資訊上傳至商務用和教育用的 Microsoft Store。 此資訊包括裝置序號、Windows 產品識別碼及硬體識別碼。 使用 Configuration Manager 的 [硬體 - 一般]  報表節點中的新報表 [Windows Autopilot 裝置資訊]  來收集並報告此裝置資訊。 如需詳細資訊，請參閱[如何準備網路型裝置進行共同管理](../../../comanage/how-to-prepare-Win10.md#windows-autopilot)來準備進行共同管理。

### <a name="report-on-windows-10-servicing-details-for-a-specific-collection"></a>針對特定集合報告 Windows 10 服務的詳細資料
<!--1357653-->
[特定集合的 Windows 10 服務詳細資料]  報表會顯示有關特定集合的 Windows 10 服務一般資訊。 此報表會顯示資源識別碼、NetBIOS 名稱、OS 名稱、OS 版本名稱、組建、OS 分支，以及 Windows 10 裝置的服務狀態。 如需詳細資訊，請參閱[報表清單](../../servers/manage/list-of-reports.md#operating-system)



<!-- ## Inventory  -->



<!-- ## Mobile device management -->



 ## <a name="protect-devices"></a>保護裝置

### <a name="improvements-to-configuration-manager-policies-for-windows-defender-exploit-guard"></a>適用於 Windows Defender 惡意探索防護之 Configuration Manager 原則的改善
<!-- 1356220 -->
針對 [Windows Defender 惡意探索防護](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/configure-attack-surface-reduction)，已在 Configuration Manager 中新增適用於[攻擊面縮減](../../../protect/deploy-use/create-deploy-exploit-guard-policy.md#bkmk_ASR)和[受控資料夾存取權](../../../protect/deploy-use/create-deploy-exploit-guard-policy.md#bkmk_CFA)元件的額外原則設定。

### <a name="new-host-interaction-settings-for-windows-defender-application-guard"></a>Windows Defender 應用程式防護的新主機互動設定
<!-- 1356256 -->
對於 Windows 10 1709 版和更新版本的裝置，[Windows Defender 應用程式防護](../../../protect/deploy-use/create-deploy-application-guard-policy.md#bkmk_HIS)有兩個新的主機互動設定： 
- 網站可獲授與主機虛擬圖形處理器的存取權。 
- 容器內下載的檔案就可保存在主機上。 




## <a name="configuration-manager-console"></a>Configuration Manager 主控台

### <a name="improvements-to-the-configuration-manager-console"></a>Configuration Manager 主控台的改善 
此版本包含對 Configuration Manager 主控台的以下改進。
- [資產與合規性]、[裝置] 底下列出的裝置，現在預設會顯示主要使用者。 此欄只會在 [裝置] 節點中顯示。 最後登入的使用者也會新增為選擇性資料行。<!-- 1357280 --> 啟用[使用者和裝置親和性](../../clients/deploy/about-client-settings.md#user-and-device-affinity)用戶端設定，可讓站台建立主要使用者和裝置之間的關聯性。
- 如果集合是另一個集合的成員且重新命名時，會依成員資格規則來更新新名稱。<!--1357282--> 
- 在用戶端上使用遠端控制時，若用戶端具有多個不同 DPI 縮放比例的監視器，滑鼠游標現在會正確地對應不同的監視器。 <!--433170-->
- 當選取圖形區段時，[Office 365 用戶端管理儀表板](../../../sum/deploy-use/office-365-dashboard.md)會顯示相關裝置的清單。 <!--1357281 --> 



## <a name="next-steps"></a>後續步驟
當您已準備好要安裝此版本時，請參閱 [Configuration Manager 的更新](../../servers/manage/updates.md)。
