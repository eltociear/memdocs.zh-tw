---
title: 軟體更新的必要條件
titleSuffix: Configuration Manager
description: 了解在 Configuration Manager 中進行軟體更新的先決條件。
author: mestew
ms.author: mstewart
manager: dougeby
ms.date: 08/22/2019
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: fdf05118-162a-411e-b72e-386b9dc9a5e1
ms.openlocfilehash: a870d2bf18b9e7f064e914f450aee0f5e3e2e545
ms.sourcegitcommit: 214fb11771b61008271c6f21e17ef4d45353788f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/07/2020
ms.locfileid: "82906709"
---
# <a name="prerequisites-for-software-updates-in-configuration-manager"></a>在 Configuration Manager 中進行軟體更新的先決條件

適用於：  Configuration Manager (最新分支)

此文章列出 Configuration Manager 中軟體更新的先決條件。 每項必要條件的內、外部相依性會分列於不同的表格之中。  

## <a name="software-update-dependencies-that-are-external-to-configuration-manager"></a>Configuration Manager 外部的軟體更新相依性  
 下列各節列出軟體更新的外部相依性。  

### <a name="internet-information-services"></a>Internet Information Services  
 網站系統伺服器上必須安裝 Internet Information Services (IIS)，才能執行軟體更新點、管理點與發佈點。 如需詳細資訊，請參閱[站台系統角色的必要條件](../../core/plan-design/configs/site-and-site-system-prerequisites.md)。  

### <a name="windows-server-update-services"></a>Windows Server Update Services  
 Windows Server Update Services (WSUS) 是用戶端軟體更新同步及軟體更新適用性掃描的必要條件。 必須在建立軟體更新點角色之前安裝 WSUS 伺服器。 下列版本的 WSUS 支援軟體更新點：  

- WSUS 10.0.14393 (Windows Server 2016 中的角色)
- WSUS 10.0.17763 (Windows Server 2019 中的角色) (需要 Configuration Manager 1810 或更新版本)
- WSUS 6.2 和 6.3 (Windows Server 2012 和 Windows Server 2012 R2 中的角色)
  - 如果您部署 Windows 10 升級，則 WSUS 6.2 和 6.3 需要 [KB 3095113 和 KB 3159706 (或同等更新)](#BKMK_wsus2012)。

> [!NOTE]
> - 一個站台上有多個軟體更新點時，請確認所有更新點均執行相同版本的 WSUS。

### <a name="wsus-administration-console"></a>WSUS 管理主控台  
如果軟體更新點位於遠端站台系統伺服器上，且站台伺服器尚未安裝 WSUS，則必須在 Configuration Manager 站台伺服器上安裝 WSUS 管理主控台。  

> [!IMPORTANT]  
> - 站台伺服器和軟體更新點必須執行相同版本的 WSUS。
> - 請不要使用 WSUS 管理主控台進行 WSUS 設定。 Configuration Manager 會連線至軟體更新點上執行的 WSUS 執行個體，並進行適當地設定。  


### <a name="windows-update-agent"></a>Windows Update 代理程式  
 用戶端上需要有 Windows Update Agent (WUA) 用戶端，才能連線至 WSUS 伺服器。 WUA 會擷取必須進行相容性掃描的軟體更新清單。  

 安裝 Configuration Manager 時，會下載最新版的 WUA。 接下來，當您安裝 Configuration Manager 用戶端時，會在必要時升級 WUA。 若安裝失敗，便須使用其他方法升級 WUA。  

## <a name="software-update-dependencies-that-are-internal-to-configuration-manager"></a>Configuration Manager 內部的軟體更新相依性  
 下列各節列出 Configuration Manager 中軟體更新的內部相依性。  

### <a name="management-points"></a>管理點  
 管理點會在用戶端電腦和 Configuration Manager 站台之間傳送資訊。 管理點是軟體更新的必要條件。  

### <a name="software-update-points"></a>軟體更新點  
 您必須在 WSUS 伺服器上安裝軟體更新點，才能在 Configuration Manager 中部署軟體更新。 如需詳細資訊，請參閱[安裝和設定軟體更新點](../get-started/install-a-software-update-point.md)。

### <a name="distribution-points"></a>發佈點  
 必須要有發佈點，才能儲存軟體更新的內容。 如需安裝發佈點及管理內容之方式的詳細資訊，請參閱[管理內容與內容基礎結構](../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md)。  

### <a name="client-settings-for-software-updates"></a>軟體更新的用戶端設定  
根據預設，用戶端會啟用軟體更新。 另有其他設定可以控制用戶端評估軟體更新相容性的方式和時間，以及控制軟體更新的安裝方式。  

 如需詳細資訊，請參閱下列文章：  

- [軟體更新的用戶端設定](../get-started/manage-settings-for-software-updates.md#BKMK_ClientSettings)   

- [軟體更新用戶端設定](../../core/clients/deploy/about-client-settings.md#software-updates)  

### <a name="reporting-services-points"></a>Reporting Services 點  
 Reporting Services 點站台系統角色可以顯示軟體更新的報告。 這個角色是選用項目，但建議使用。 如需如何建立 Reporting Services 點的詳細資訊，請參閱[設定報告](../../core/servers/manage/configuring-reporting.md)。  

## <a name="which-updates-are-required-on-wsus-62-and-63"></a><a name="BKMK_wsus2012"></a> WSUS 6.2 和 6.3 需要哪些更新？

在 WSUS 6.2 和 6.3 中同步 [升級]  分類，需要兩項更新。 有時候，如果在安裝 KB3095113 和 KB3159706 之前先同步處理下載或部署升級，可能會發生下載或部署升級錯誤。 下一節將說明可能問題的相關資訊。  

- 您必須在您的軟體更新點與網站伺服器上，安裝 2015 年 10 月發行的 [KB 3095113](https://support.microsoft.com/kb/3095113)，才能同步**升級**分類。
  - 此更新會啟用 [升級]  分類。
- 若要服務 Windows 10 1607 版及更新版本，您必須安裝並設定 [KB 3159706](https://support.microsoft.com/help/3159706)。 KB 3159706 已於 2016 年 5 月發行。
  - 此更新可讓 WSUS 以原生方式來解密用於升級 Windows 10 1607 版及更新版本的檔案。

>[!IMPORTANT]
> 從 2017 年 7 月開始，**安全性每月品質彙總**包含了 KB 3095113 和 KB 3159706。 這表示您可能不會看到 KB 3095113 和 KB 3159706 顯示為已安裝的更新，因為這兩項更新可能已隨彙總套件一起安裝。 不過，如果需要其中一項更新，建議您安裝 2017 年 10 月之後發行的**安全性每月品質彙總**，因為這些彙總包含額外的 WSUS 更新，可降低 WSUS clientwebservice 的記憶體使用率。

## <a name="download-of-windows-10-upgrades-fails-with-error-invalid-certificate-signature-or-0xc1800118"></a><a name="BKMK_RecoverUpgrades"></a> 下載 Windows 10 升級失敗，出現「錯誤：不正確的憑證簽章」或 0xc1800118

本節所述的更新和問題，僅適用於在 Windows Server 2012 或 Windows Server 2012 R2 電腦上執行的 WSUS (WSUS 6.2 和 6.3)。 一般而言，如果在 2017 年 7 月之前安裝 WSUS，且最近才啟用 [升級]  分類，您才會看到本節中所述的問題。 不過，在其他情況下也有可能看到這些問題。

### <a name="historical-information-about-kb-3095113"></a>KB 3095113 的歷程記錄資訊

 [KB 3095113](https://support.microsoft.com/kb/3095113) 於 2015 年 10 月[發行為 Hotfix](https://docs.microsoft.com/archive/blogs/wsus/important-update-for-wsus-4-0-kb-3095113)，以將 Windows 10 升級的支援新增至 WSUS。 此更新可讓 WSUS 在 Windows 10 的 [升級]  分類中同步處理及發佈更新。

若未先安裝 [Hotfix 3095113](https://support.microsoft.com/kb/3095113)，即同步任何升級，將會在 WSUS 資料庫 (SUSDB) 中填入無法使用的資料。 必須先清除該資料，才能正確地部署升級。 無法使用 [下載軟體更新精靈] 來下載此狀態中的 Windows 10 升級。

類似下列的錯誤，出現在 [下載軟體更新精靈] 的 [完成] 頁面上：

``` Output
Error: Upgrade to Windows 10 Pro, version 1511, 10586
Failed to download content id {content_id}. Error: Invalid certificate signature
```

此外，類似下列的錯誤會記錄在 PatchDownloader.log 檔案中：

``` Log
Download http://wsus.ds.b1.download.windowsupdate.com/d/upgr/2015/12/10586.0.151029-1700.th2_release_...esd...
Authentication of file C:\Users\{username}\AppData\Local\Temp\2\{temporary_filename}.tmp failed, error 0x800b0004
ERROR: DownloadContentFiles() failed with hr=0x80073633
# This log is truncated for readability.
```

在過去，當發生這些錯誤時，可藉由執行 [WSUS 解決步驟](https://docs.microsoft.com/archive/blogs/wsus/how-to-delete-upgrades-in-wsus)的修改版本來解決這些錯誤。 由於這些步驟類似於在安裝 KB 3159706 後不執行所需手動步驟的解決方案，所以我們將這兩組步驟結合成下一節中的單一解決方案：

- [安裝 KB 3095113 或 KB 3159706 之前，先將同步升級復原](#bkmk_fix-upgrades)。

### <a name="historical-information-about-kb-3159706"></a>KB 3159706 的歷程記錄資訊

KB 3148812 最初於 2016 年 4 月發行，讓 WSUS 以原生方式來解密用於升級 Windows 10 套件的 .esd 檔案。 [KB 3148812 造成了部分客戶的問題](https://docs.microsoft.com/archive/blogs/wsus/the-long-term-fix-for-kb3148812-issues)，並已取代為 [KB 3159706](https://support.microsoft.com/help/3159706)。 您必須先在所有軟體更新點和站台伺服器上安裝 KB 3159706，才能服務 Windows 10 1607 版和更新版本的裝置。 不過，如果您不知道在安裝 KB 之後需要進行下列手動步驟，就可能會發生問題：

1. 從提高權限的命令提示下，執行 `"C:\Program Files\Update Services\Tools\wsusutil.exe" postinstall /servicing`。
1. 重新啟動所有 WSUS 伺服器上的 WSUS 服務。

如果您不知道 KB 3159706 在安裝後有手動步驟，或在安裝 KB 3159706 之前已同步處理 Windows 10 1607，則在連線至 WSUS 主控台並分別部署升級時會遇到問題。 當用戶端下載升級檔案時，會收到 [**0xC1800118**錯誤碼](https://support.microsoft.com/help/3194588/0xc1800118-error-when-you-push-windows-10-version-1607-by-using-wsus)。

由於解決方案步驟類似於在安裝 KB 3095113 之前同步處理升級的解決方案，所以我們將這兩組步驟結合成下一節中的單一解決方案。
 

### <a name="to-recover-from-synchronizing-the-upgrades-before-you-install-kb-3095113-or-kb-3159706"></a><a name="bkmk_fix-upgrades"></a> 安裝 KB 3095113 或 KB 3159706 之前，先將同步升級復原

請依照下方步驟來解決 0xc1800118 錯誤和「錯誤：不正確的憑證簽章」：

1. 在 WSUS 和 Configuration Manager 兩者中停用 [升級]  分類。 在指示要您同步處理前，請勿進行同步處理。  
   - 取消核取頂層網站上，軟體更新點元件屬性中的**升級**分類。
     - 如需詳細資訊，請參閱[設定分類和產品](../get-started/configure-classifications-and-products.md)。
   - 從 WSUS [選項  ](https://docs.microsoft.com/windows-server/administration/windows-server-update-services/manage/setting-up-update-synchronizations) 頁面的 [產品和分類]  下方，取消選取 [升級]  分類，或使用以系統管理員身分執行的 PowerShell ISE。
      ```PowerShell
      Get-WsusClassification | Where-Object -FilterScript {$_.Classification.Title -Eq "Upgrades"} | Set-WsusClassification -Disable
      ```  
     - 如果您在多個 WSUS 伺服器之間共用 WSUS 資料庫，則只需要針對每個資料庫取消選取 [升級]  一次。  
1. 在每部 WSUS 伺服器上，從提高權限的命令提示字元執行：`"C:\Program Files\Update Services\Tools\wsusutil.exe" postinstall /servicing`。 然後，重新啟動所有 WSUS 伺服器上的 WSUS 服務。
   -  WSUS 會先將資料庫設定為[單一使用者模式](https://docs.microsoft.com/sql/relational-databases/databases/set-a-database-to-single-user-mode)，再檢查是否需要服務。 服務是否會執行取決於檢查結果。 然後，資料庫會設定回多使用者模式。 
   - 如果您在多個 WSUS 伺服器之間共用 WSUS 資料庫，則只需要針對每個資料庫執行一次這項服務。
1. 使用以系統管理員身分執行的 PowerShell ISE，從每個 WSUS 資料庫刪除所有 Windows 10 升級。
   ```PowerShell
   [reflection.assembly]::LoadWithPartialName("Microsoft.UpdateServices.Administration")
   $wsus = [Microsoft.UpdateServices.Administration.AdminProxy]::GetUpdateServer();
   $wsus.GetUpdates() | Where {$_.UpdateClassificationTitle -eq 'Upgrades' -and $_.Title -match 'Windows 10'} `
   | ForEach-Object {$wsus.DeleteUpdate($_.Id.UpdateId.ToString()); Write-Host $_.Title removed}
   ```
1. 從軟體更新點使用的每個 WSUS 資料庫中，刪除 tbFile 資料表中的檔案。 在 WSUS 資料庫上，從 SQL Server Management Studio 執行下列命令：
   ```SQL
   declare @NotNeededFiles table (FileDigest binary(20) UNIQUE)
   insert into @NotNeededFiles(FileDigest) (select FileDigest from tbFile where FileName like '%.esd%'  except select FileDigest from tbFileForRevision)
   delete from tbFileOnServer where FileDigest in (select FileDigest from @NotNeededFiles)
   delete from tbFile where FileDigest in (select FileDigest from @NotNeededFiles)
   ```
1. 在 Configuration Manager 的最上層站台啟動軟體更新同步處理，並等候其完成。 由於我們已在移除 [升級]  時變更了分類 Configuration Manager，所以會進行完整同步處理。 (如需詳細資訊，請參閱[同步軟體更新](../get-started/synchronize-software-updates.md)。
1. 選取軟體更新點元件屬性中的**升級**分類。 接下來，啟動另一個軟體更新同步處理，讓 [升級]  返回 WSUS 和 Configuration Manager。 您不需要在 WSUS 中啟用 [升級]  分類，因為 Configuration Manager 會為您執行這項操作。
1. 如果您的用戶端在下載升級時收到 **0xC1800118** 錯誤碼，則必須刪除 Windows Update 代理程式所使用的資料存放區。 您也可能必須刪除裝置上隱藏的 ~BT 資料夾。 用戶端下次掃描時，將對 WSUS 伺服器而非差異進行完整掃描，。 您可以使用類似下列範例指令碼的 PowerShell 指令碼：  
   ```PowerShell
   stop-service wuauserv
   remove-item -path c:\windows\softwaredistribution\datastore -recurse -force
   # If the device has a hidden ~BT folder on the c drive, delete it too by uncommenting the next line.
   # remove-item -path c:\~BT -recurse -force
   start-service wuauserv
   ```

## <a name="next-steps"></a>後續步驟
[準備軟體更新管理](../get-started/prepare-for-software-updates-management.md)
