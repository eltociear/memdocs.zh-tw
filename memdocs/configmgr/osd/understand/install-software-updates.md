---
title: 安裝軟體更新
titleSuffix: Configuration Manager
description: 在 Configuration Manager 中使用工作順序步驟「安裝軟體更新」的建議。
ms.date: 05/28/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 72d1ccd5-3763-4f88-9273-e1a73e8f4286
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 6528e979222bc6ecea2a57a003ff5266b5c096c5
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81703306"
---
# <a name="install-software-updates"></a>安裝軟體更新

適用於：  Configuration Manager (最新分支)

**安裝軟體更新**步驟常用於 Configuration Manager 工作順序中。 安裝或更新 OS 時，它會觸發軟體更新元件來進行掃描及部署更新。 此步驟可能會對某些客戶形成挑戰，例如，很長的逾時延遲或遺漏更新。 使用此文章中的資訊，以協助減少此步驟的常見問題，並在發生錯誤時進行更好的排解疑難。

如需步驟的詳細資訊，請參閱[安裝軟體更新](task-sequence-steps.md#BKMK_InstallSoftwareUpdates)



## <a name="recommendations"></a>建議

為了協助此流程成功，請使用下列建議：

- [使用離線服務](#use-offline-servicing)
- [單一索引](#single-index)
- [減少映像大小](#bkmk_resetbase)

### <a name="use-offline-servicing"></a>使用離線服務

使用 Configuration Manager，定期將適用的軟體更新安裝至您的映像檔案。 這種做法接著能減少您需要在工作順序期間安裝的更新數目。

如需詳細資訊，請參閱[將軟體更新套用至映像](../get-started/manage-operating-system-images.md#BKMK_OSImagesApplyUpdates)。

### <a name="single-index"></a>單一索引

許多映像檔案都包含多個索引，例如，針對不同版本的 Windows。 將映像檔案減少為您所需的單一索引。 這種做法可減少將軟體更新套用至映像的時間量。 它也會讓下一個建議能夠減少映像大小。

從 1902 版開始，當您將 OS 映像新增至站台時，即會將此程序自動化。 如需詳細資訊，請參閱[新增 OS 映像](../get-started/manage-operating-system-images.md#BKMK_AddOSImages)。<!--3719699-->

### <a name="reduce-image-size"></a><a name="bkmk_resetbase"></a> 減少映像大小

當您將軟體更新套用至映像時，請移除任何已取代的更新來將輸出最佳化。 使用 DISM 命令列工具，例如：

``` Command
dism /Mount-Image /ImageFile:C:\Data\install.wim /MountDir:C:\Mountdir
dism /Image:C:\Mountdir /Cleanup-Image /StartComponentCleanup /ResetBase
dism /Unmount-Image /MountDir:C:\Mountdir /Commit  
```

從 1902 版開始，有一個新選項可將此程序自動化。 如需詳細資訊，請參閱[最佳化的映像服務](../get-started/manage-operating-system-images.md#bkmk_resetbase)。<!--3555951-->


## <a name="image-engineering-decisions"></a>映像工程決策

當您設計映像處理流程時，有數個可能影響軟體更新安裝的選項：

- [定期重新擷取映像](#bkmk_goldimage)  
- [使用離線服務](#bkmk_offline)  
- [只使用預設映像](#bkmk_installwim)

### <a name="periodically-recapture-the-image"></a><a name="bkmk_goldimage"></a> 定期重新擷取映像

您必須有一個自動化流程可定期排程來擷取自訂的 OS 映像。 此擷取工作順序會安裝最新的軟體更新。 這些更新可以包括累積、非累積和其他重大更新，例如，服務堆疊更新 (SSU)。 部署工作順序會安裝自擷取之後的任何其他更新。

如需此流程的詳細資訊，請參閱[建立工作順序以擷取 OS](../deploy-use/create-a-task-sequence-to-capture-an-operating-system.md)。

#### <a name="advantages"></a>優點

- 每個用戶端上要在部署期間套用的更新較少，可在部署期間節省時間與頻寬
- 擔心會導致重新啟動的更新較少
- 適用於組織的自訂映像
- 部署階段的變數較少

#### <a name="disadvantages"></a>缺點

- 需要建立和擷取映像的時間，即使它大部分會自動進行
- 將映像發佈至發佈點的時間增加，這可視為使用中部署的中斷
- 透過進入生產階段前的環境進行測試的時間可能比 OS 修補週期更長，這可能使得更新的映像變成無關


### <a name="use-offline-servicing"></a><a name="bkmk_offline"></a> 使用離線服務

排程 Configuration Manager 軟體以將更新套用至映像。

如需詳細資訊，請參閱[將軟體更新套用至映像](../get-started/manage-operating-system-images.md#BKMK_OSImagesApplyUpdates)。

#### <a name="advantages"></a>優點

- 每個用戶端上要在部署期間套用的更新較少，可在部署期間節省時間與頻寬
- 擔心會導致重新啟動的更新較少
- 您可以在站台上排程服務流程

#### <a name="disadvantages"></a>缺點

- 手動選取更新
- 將映像發佈至發佈點的時間增加
- 僅支援以 CBS 為基礎的更新。 無法套用 Office 更新

> [!Tip]  
> 您可以使用 PowerShell 自動選取軟體更新。 使用 [Get-CMSoftwareUpdate](https://docs.microsoft.com/powershell/module/configurationmanager/get-cmsoftwareupdate?view=sccm-ps) Cmdlet 來取得更新清單。 然後使用 [New-CMOperatingSystemImageUpdateSchedule](https://docs.microsoft.com/powershell/module/configurationmanager/new-cmoperatingsystemimageupdateschedule?view=sccm-ps) Cmdlet 來建立離線服務排程。 下列範例示範一個可自動執行此動作的方法：
>
> ```PowerShell
> # Get the OS image
> $Win10Image = Get-CMOperatingSystemImage -Name "Windows 10 Enterprise"
>
> # Get the latest cumulative update for Windows 10 1809
> $OSBuild = "1809"
> $LatestUpdate = Get-CMSoftwareUpdate -Fast | Where {$_.LocalizedDisplayName -Like "*Cumulative Update for Windows 10 Version $OSBuild for x64*" -and $_.LocalizedDisplayName -notlike "*Dynamic*"} | Sort-Object ArticleID -Descending | Select -First 1
> Write-Host "Latest update for Windows 10 build" $OSBuild "is" $LatestUpdate.LocalizedDisplayName
>
> # Create a new update schedule to apply the latest update
> New-CMOperatingSystemImageUpdateSchedule -Name $Win10Image.Name -SoftwareUpdate $LatestUpdate -RunNow -ContinueOnError $True
> ```


### <a name="use-default-image-only"></a><a name="bkmk_installwim"></a> 只使用預設映像

在您的部署工作順序中，使用預設的 Windows install.wim 映像檔案。

#### <a name="advantages"></a>優點

- 已知良好的來源，可減少映像損毀成為潛在問題的風險
- 使修改映像不會成為潛在問題

#### <a name="disadvantages"></a>缺點

- 可能在部署期間進行大量更新
- 每部裝置的部署時間增加
- 可能沒有所需的自訂，需要額外的工作順序步驟來自訂



## <a name="flowchart"></a>流程圖

此流程圖顯示當您在工作順序中包含「安裝軟體更新」步驟時的流程。

[檢視完整大小的圖表](media/ts-step-install-software-updates.svg)

![適用於「安裝軟體更新」工作順序步驟的流程圖](media/ts-step-install-software-updates.svg)  

1. **在用戶端上啟動流程**：用戶端上執行的工作順序包含「安裝軟體更新」步驟。
2. **編譯和評估原則**：用戶端會將所有軟體更新原則編譯至 WMI RequestedConfigs 命名空間。 (CIAgent.log)
3. *這個執行個體是第一次呼叫嗎？*  
    1. **是**：移至「完整掃描」   
    2. **否**：此步驟會將選項設定為 [[從快取掃描結果評估軟體更新](task-sequence-steps.md#evaluate-software-updates-from-cached-scan-results)] 嗎？ 
        1. **是**：移至「從快取的結果掃描」 
        2. **否**：移至「完整掃描」 
4. 掃描流程：完整掃描或從快取的結果掃描，與監視流程同時進行。
    1. **完整掃描**：工作順序引擎會透過更新掃描 API 來呼叫軟體更新代理程式，以進行「完整」  掃描。 (WUAHandler.log、ScanAgent.log)  
        1. **SUM 代理程式掃描 - 完整**：透過 Windows Update 代理程式 (WUA) 的標準掃描流程，與執行 WSUS 的軟體更新點進行通訊。 它會在本機更新存放區中新增任何適用的更新。 (WindowsUpdate.log、UpdateStore.log)
    2. **從快取的結果掃描**：工作順序引擎會透過更新掃描 API 來呼叫軟體更新代理程式，以根據已快取的中繼資料進行掃描。 (WUAHandler.log、ScanAgent.log)
        1. **SUM 代理程式掃描 - 已快取**：Windows Update 代理程式 (WUA) 會針對已經快取於本機更新存放區中的更新進行檢查。 (WindowsUpdate.log、UpdateStore.log)
    3. **啟動掃描計時器**：工作順序引擎會啟動計時器並進行等候。 (此流程會與完整掃描或從已快取的結果流程中進行掃描同時發生)。
        1. **監視**：工作順序引擎會監視 SUM 代理程式以取得狀態。
        2. 來自 SUM 代理程式的回應是什麼？ 
            - **進行中**：計時器是否已達到工作順序變數 [SMSTSSoftwareUpdateScanTimeout](task-sequence-variables.md#SMSTSSoftwareUpdateScanTimeout) 中的值？ (預設值為 1 小時)
                - **是**：步驟失敗。
                - **否**：移至「監視」 
            - **失敗**：步驟失敗。
            - **完成**：移至「列舉更新清單」 
5. **列舉更新清單**：SUM 代理程式會列舉掃描所傳回的更新清單，以判斷更新為可用或必要。
6. 掃描結果清單中是否有任何更新？ 
    - **是**：移至「安裝更新」 
    - **否**：不需安裝任何項目，步驟已順利完成。
7. 部署流程：安裝更新流程會與部署監視流程同時發生。
    1. **安裝更新**：工作順序引擎會透過更新部署 API 來呼叫 SUM 代理程式，以安裝所有可用更新或僅安裝強制更新。 此行為會以步驟的設定為基礎：您選取的是 [安裝必備 - 僅限強制軟體更新]  或 [可供安裝 - 所有軟體更新]  。 您也可以使用 [SMSInstallUpdateTarget](task-sequence-variables.md#SMSInstallUpdateTarget) 變數來指定此行為。
        1. **SUM 代理程式安裝**：透過標準內容下載，使用現有已快取之更新清單的標準安裝流程。 透過 Windows Update 代理程式 (WUA) 安裝更新。 (UpdatesDeployment.log、UpdatesHandler.log、WuaHandler.log、WindowsUpdate.log)
    2. **開始部署計時器並顯示進度**：工作順序引擎會啟動安裝計時器，在 TS 進度 UI 中以 10% 時間間隔來顯示子進度，然後等候。
        1. **監視**：工作順序引擎會輪詢 SUM 代理程式以取得狀態。
        2. 來自 SUM 代理程式的回應是什麼？ 
            - **進行中**：安裝流程是否已有 8 小時處於非使用中狀態？ 
                - **是**：步驟失敗。
                - **否**：移至「監視」 
            - **失敗**：步驟失敗。
            - **完成**：移至「此步驟會將選項設定為 [從快取掃描結果評估軟體更新]  嗎？」 


### <a name="timeouts"></a>逾時

此圖表包含兩個適用於此步驟的逾時變數。 有其他來自可能影響此流程之其他元件的標準計時器。

- 更新掃描逾時：1 小時 (smsts.log)  
- 位置要求逾時：1 小時 (LocationServices.log、CAS.log)  
- 內容下載逾時：1 小時 (DTS.log)  
- 非使用中的發佈點逾時：1 小時 (LocationServices.log、CAS.log)  
- 安裝非使用中逾時總計：8 小時 (smsts.log)  



## <a name="troubleshooting"></a>疑難排解

使用下列資源和其他資訊，以協助您針對此步驟的問題進行疑難排解：

- 請務必將軟體更新部署的目標設定為與工作順序部署相同的集合。  

- 請務必在界限群組中包含軟體更新點。 如需詳細資訊，請參閱這篇 [Microsoft 支援服務文章](https://support.microsoft.com/help/4041012/1702-clients-do-not-get-software-updates-from-configuration-manager) \(機器翻譯\)。  

- 為了協助您進行軟體更新管理流程的疑難排解，請參閱[軟體更新管理疑難排解](https://support.microsoft.com/help/10680/software-update-management-troubleshooting-in-configuration-manager) \(機器翻譯\)。  

- 若要協助改善整體效能，請降低軟體更新類別目錄的大小。 例如：  

    - 移除不必要的分類、產品和語言。 如需詳細資訊，請參閱[設定要同步處理的分類和產品](../../sum/get-started/configure-classifications-and-products.md)。  

    - 為站台資料庫重新建立索引並重建統計資料。 如需詳細資訊，請參閱 [Configuration Manager 的效能與調整指導方針白皮書](https://gallery.technet.microsoft.com/Configuration-Manager-ba55428e) \(英文\)。  

    - 拒絕不必要的更新，例如：
        - 已取代 (從 1810 版開始，Configuration Manager 會為您執行此動作。 如需詳細資訊，請參閱[從 1810 版開始的 WSUS 清理行為](../../sum/deploy-use/software-updates-maintenance.md#wsus-cleanup-behavior-starting-in-version-1810))。
        - Itanium
        - 搶鮮版 (Beta)
        - Version Next
        - ARM
        - 您未部署的 Windows 版本
