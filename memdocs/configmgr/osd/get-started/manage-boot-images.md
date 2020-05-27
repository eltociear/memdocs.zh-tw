---
title: 管理開機映像
titleSuffix: Configuration Manager
description: 在 Configuration Manager 中，了解如何管理 OS 部署期間所使用的 Windows PE 開機映像。
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 97f2d81a-2c58-442c-88bc-defd5a1cd48f
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 4403c8d0c57fba8fb63e3df729fb8a48ff123362
ms.sourcegitcommit: d8dc05476ecd5db7ecb36dc649b566b349ba263d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/21/2020
ms.locfileid: "83732868"
---
# <a name="manage-boot-images-with-configuration-manager"></a>使用 Configuration Manager 管理開機映像

適用於：Configuration Manager (最新分支)

Configuration Manager 中的開機映像是 OS 部署期間所使用的 [Windows PE](https://docs.microsoft.com/windows-hardware/manufacture/desktop/winpe-intro) \(英文\) (WinPE) 映像。 開機映像可用來啟動 WinPE 中的電腦。 這個基本的 OS 包含有限的元件和服務。 Configuration Manager 會使用 WinPE 來準備要安裝 Windows 的目的地電腦。

## <a name="default-boot-images"></a><a name="BKMK_BootImageDefault"></a> 預設開機映像

Configuration Manager 提供兩種預設開機映像：一種支援 x86 平台，另一種支援 x64 平台。 這些映像均儲存於站台伺服器上下列共用的 *x64* 或 *i386* 資料夾中：`\\<SiteServerName>\SMS_<sitecode>\osd\boot\`。 預設開機映像會根據您所採取的動作更新或重新產生。

對於任何針對預設開機映像描述的動作，請考慮下列行為：

- 來源驅動程式物件必須有效。 這些物件包括驅動程式來源檔案。 如果物件無效，站台就不會將驅動程式新增至開機映像。  

- 開機映像若非以預設開機映像為基礎，則即使它們使用相同的 Windows PE 版本，也不會進行修改。  

- 將已修改的開機映像重新發佈至發佈點。  

- 重新建立任何使用已修改開機映像的媒體。  

- 如果您不想自動更新自訂/預設開機映像，請勿將它們儲存於預設位置。  

> [!NOTE]
> Configuration Manager 記錄工具 (**CMTrace**) 會新增至**軟體程式庫**中的所有開機映像。 當您位於 Windows PE 時，從命令提示字元輸入 `cmtrace` 來啟動此工具。
>
> CMTrace 是 Windows PE 中記錄檔的預設檢視器。

### <a name="use-updates-and-servicing-to-install-the-latest-version-of-configuration-manager"></a>使用 [更新與服務] 來安裝最新版本的 Configuration Manager

在您升級 Windows 評定及部署套件 (ADK) 版本，然後使用 [更新與服務] 來安裝最新的 Configuration Manager 版本時，站台會重新產生預設開機映像。 此更新包括來自已更新之 Windows ADK 的新 WinPE 版本、新版 Configuration Manager 用戶端、驅動程式及自訂。 站台不會修改自訂開機映像。

### <a name="upgrade-from-configuration-manager-2012-to-current-branch"></a>從 Configuration Manager 2012 升級至最新分支

當您將 Configuration Manager 2012 升級至最新分支時，站台會重新產生預設開機映像。 此更新包括來自已更新之 Windows ADK 的新 WinPE 版本，以及新版 Configuration Manager 用戶端。 所有開機映像自訂都保持不變。 站台不會修改自訂開機映像。

### <a name="update-distribution-points-with-the-boot-image"></a>使用開機映像更新發佈點

當您在主控台中從 [開機映像] 節點使用 [更新發佈點] 動作時，站台會使用用戶端元件、驅動程式及自訂來更新目標開機映像。

您可以從 Windows ADK 安裝目錄重新載入具有最新 WinPE 版本的開機映像。 「更新發佈點」精靈的 [一般] 頁面會提供下列資訊：

- 站台伺服器上目前安裝的 Windows ADK 版本
- 目前的生產環境用戶端版本
- 開機映像中 WinPE 的 Windows ADK 版本
- 開機映像中的 Configuration Manager 用戶端版本

如果開機映像中的版本過時，請使用 [從 Windows ADK 重新載入具備目前 Windows PE 版本的此開機映像] 的選項。

> [!Important]  
> 此動作適用於預設和自訂開機映像。 在這個重新載入開機映像的流程中，站台不會保留任何在 Configuration Manager 以外手動進行的自訂。 這些自訂包括協力廠商延伸模組。 此選項會使用最新的 WinPE 版本和最新的用戶端版本來重建開機映像。 系統只會重新套用您在開機映像屬性中指定的設定。 <!--SCCMDocs issue #1283-->

[開機映像] 節點也包括一個新的 (**用戶端版本**) 資料行。 您可以使用此資料行來快速檢視每個開機映像中的 Configuration Manager 用戶端版本。

## <a name="customize-a-boot-image"></a><a name="BKMK_BootImageCustom"></a> 自訂開機映像  

如果開機映像是以來自所支援 Windows ADK 版本的 WinPE 版本為基礎，您可以從主控台自訂或[修改開機映像](#BKMK_ModifyBootImages)。 當您升級站台並安裝新的 Windows ADK 版本時，不會使用新的 Windows ADK 版本來更新自訂開機映像。 發生這種情況時，您並無法在 Configuration Manager 主控台中自訂開機映像。 不過，它們將依照升級前一樣的方式繼續運作。  

當開機映像是以站台上所安裝的不同 Windows ADK 版本為基礎時，您必須自訂開機映像。 請使用另一個方法來自訂這些開機映像，例如使用「部署映像服務與管理」(DISM) 命令列工具。 DISM 是 Windows ADK 的一部分。 如需詳細資訊，請參閱[自訂開機映像](customize-boot-images.md)。  

## <a name="add-a-boot-image"></a><a name="BKMK_AddBootImages"></a> 新增開機映像  

在站台安裝期間，Configuration Manager 會自動新增以支援的 Windows ADK 版本中的 WinPE 版本為基礎的開機映像。 依據 Configuration Manager 的版本而定，您可以根據來自 Windows ADK 支援版本的不同 WinPE 版本來新增開機映像。 當您嘗試新增包含不支援之 WinPE 版本的開機映像時，會發生錯誤。 以下清單是目前支援的 Windows ADK 和 WinPE 版本：

|  |  |
|---------|---------|
| Windows ADK 版本 | Windows ADK for Windows 10 |
| 可從 Configuration Manager 主控台自訂之開機映像的 Windows PE 版本 | Windows PE 10 |
| 「無法」從 Configuration Manager 主控台自訂的開機映像所支援的 Windows PE 版本 | - Windows PE 3.1<sup>[附註 1](#bkmk_note1)</sup> <br> - Windows PE 5 |

例如，使用 Configuration Manager 主控台來根據 Windows PE 10 (來自適用於 Windows 10 的 Windows ADK) 自訂開機映像。 針對以 Windows PE 5 為基礎的開機映像，請使用來自適用於 Windows 8 之 Windows ADK 的 DISM 版本，從不同電腦來自訂它。 接著，將自訂的開機映像新增到 Configuration Manager 主控台。 如需詳細資訊，請參閱下列文章：

- [自訂開機映像](customize-boot-images.md)
- [支援 Windows 10 ADK](../../core/plan-design/configs/support-for-windows-10.md#windows-10-adk)
- [DISM 支援的平台](https://docs.microsoft.com/windows-hardware/manufacture/desktop/dism-supported-platforms) \(英文\)

<a name="bkmk_note1"></a>

> [!NOTE]
> **附註 1：支援 Windows PE 3.1**
>
> 只會根據 Windows PE「3.1 版」，將開機映像新增至 Configuration Manager。 請使用適用於 Windows 7 SP1 的 Windows AIK 補充元件 (以 Windows PE 3.1 為基礎) 來升級適用於 Windows 7 的 Windows AIK (以 Windows PE 3.0 為基礎)。 請從 [Microsoft 下載中心](https://www.microsoft.com/download/details.aspx?id=5188)下載適用於 Windows 7 SP1 的 Windows AIK 補充元件。  

1. 在 Configuration Manager 主控台中，前往 [軟體程式庫] 工作區，展開 [作業系統]，然後選取 [開機映像] 節點。  

2. 在功能區 [常用] 索引標籤上的 [建立] 群組中，選取 [新增開機映像]。 此動作會啟動 [新增開機映像精靈]。  

3. 在 [資料來源] 頁面上，指定下列選項：  

    - 在 [路徑]  方塊中，指定開機映像 WIM 檔案的路徑。 指定的路徑必須是使用 UNC 格式的有效網路路徑。 例如：`\\ServerName\ShareName\BootImageName.wim`

    - 從 [開機映像]  下拉式清單選取開機映像。 如果 WIM 檔案包含多個開機映像，請選取適當的映像。  

4. 在 [一般] 頁面上，指定下列選項：  

    - 在 [名稱]  方塊中，為開機映像指定唯一的名稱。  

    - 在 [版本]  方塊中，指定開機映像的版本號碼。  

    - 在 [註解] 方塊中，指定您如何使用開機映像的簡單描述。  

5. 完成精靈。  

開機映像現在會列在 [開機映像] 節點中。 使用開機映像部署 OS 之前，先將開機映像發佈至發佈點。

> [!Tip]  
> 在主控台的 [開機映像] 節點中，[大小 (KB)] 欄會顯示每個開機映像解壓縮後的大小。 當站台透過網路傳送開機映像時，會傳送已壓縮的複本。 此複本通常小於 [大小 (KB)] 欄中所列的大小。  

## <a name="distribute-boot-images"></a><a name="BKMK_DistributeBootImages"></a> 發佈開機映像  

開機映像發佈至發佈點的方式，與您發佈其他內容的方式相同。 部署 OS 或建立媒體之前，先將開機映像至少發佈到一個發佈點。

如需如何發佈開機映像的詳細資訊，請參閱[發佈內容](../../core/servers/deploy/configure/deploy-and-manage-content.md#bkmk_distribute)。  

若要使用 PXE 部署 OS，在發佈開機映像之前，先考量下列數點：  

- 將發佈點設定成接受 PXE 要求。  
- 將支援 x86 PXE 和支援 x64 PXE 的開機映像發佈到至少一個支援 PXE 的發佈點。  
- Configuration Manager 會將開機映像發佈到支援 PXE 之發佈點上的 **RemoteInstall** 資料夾。  
  
如需如何使用 PXE 部署作業系統的詳細資訊，請參閱[使用 PXE 透過網路部署 Windows](../deploy-use/use-pxe-to-deploy-windows-over-the-network.md)。  

## <a name="modify-a-boot-image"></a><a name="BKMK_ModifyBootImages"></a> 修改開機映像  

新增或移除映像的裝置驅動程式，或編輯開機映像的屬性。 您新增或移除的裝置驅動程式可能會包含網路或存放裝置驅動程式。 修改開機映像時，請考慮下列因素：  

- 將驅動程式新增至開機映像之前，請在裝置驅動程式類別目錄中匯入並啟用它們。  

- 當您修改開機映像時，該開機映像不會變更開機映像所參考的任何相關聯套件。  

- 對開機映像進行變更之後，請**更新** 已有該開機映像之發佈點上的開機映像。 此程序可為用戶端提供最新版的開機映像。 如需詳細資訊，請參閱[管理已發佈的內容](../../core/servers/deploy/configure/deploy-and-manage-content.md#bkmk_manage)。  

### <a name="modify-the-properties-of-a-boot-image"></a>修改開機映像的屬性  

1. 在 Configuration Manager 主控台中，前往 [軟體程式庫] 工作區，展開 [作業系統]，然後選取 [開機映像] 節點。  

2. 選取要修改的開機映像。  

3. 在功能區 [常用] 索引標籤的 [內容] 群組中，選取 [內容]。  

4. 設定下列其中一個設定以變更開機映像的行為：  

#### <a name="images"></a>映像

在 [映像] 索引標籤上，如果您使用外部工具來變更開機映像屬性，請選取 [重新載入]。  

#### <a name="drivers"></a>驅動程式

在 [驅動程式] 索引標籤上，新增啟動 WinPE 所需的 Windows 裝置驅動程式。 新增裝置驅動程式時，請考量下列幾點：  

- 確定您新增到開機映像中的驅動程式符合開機映像的架構。  

- 若只要顯示適用於開機映像架構的驅動程式，請選取 [隱藏不符合開機映像架構的驅動程式]。 驅動程式的架構會以製造商在 INF 中所回報的架構為準。  

- WinPE 已經隨附許多內建的驅動程式。 只需新增 WinPE 中未包括的網路和存放裝置驅動程式。  

- 除非 WinPE 中需要其他驅動程式，否則，只需在開機映像中新增網路和存放裝置驅動程式。  

- 若只要顯示存放裝置和網路驅動程式，請選取 [隱藏不在儲存體或網路類別中的驅動程式 (針對開機映像)]。 此選項也會隱藏開機映像通常不需要的其他驅動程式，例如影片或數據機驅動程式。  

- 若要隱藏未具有效數位簽章的驅動程式，請選取 [隱藏未數位簽署的驅動程式]。  

> [!NOTE]  
> 先將裝置驅動程式匯入至驅動程式類別目錄，然後才能將它們新增至開機映像。 如需如何匯入裝置驅動程式的相關資訊，請參閱[管理驅動程式](manage-drivers.md)。  

#### <a name="customization"></a>自訂

在 [自訂]  索引標籤上，選取下列其中一項設定：  

- 選取 [啟用啟動前置命令] 選項，以指定要在工作順序執行前執行的命令。 啟用此選項時，請一併指定命令列來執行命令所需的任何支援檔案。  

    > [!WARNING]  
    > 在命令列的開頭加上 `cmd /c`。 如果未指定 `cmd /c`，則命令就不會在執行之後關閉。 部署會繼續等待命令完成，而不會開始執行任何其他已設定的命令或動作。  

    > [!TIP]  
    > 在工作順序媒體建立期間，精靈會將套件識別碼和啟動前置命令列寫入至 **CreateTSMedia.log** 檔案。 此資訊包含所有工作順序變數的值。 此記錄檔位於執行 Configuration Manager 主控台的電腦上。 檢閱這個記錄檔來驗證工作順序變數的值。  

- 設定 [Windows PE 背景]  設定，指定是否要使用預設的 WinPE 背景，或使用自訂背景。  

- 設定 **Windows PE 臨時空間 (MB)** ，這是由 WinPE 使用的暫存位置 (RAM 磁碟機)。 例如，當應用程式在 WinPE 中執行且需要寫入暫存檔案時，WinPE 會將檔案重新導向到記憶體的臨時空間，以模擬實際的硬碟。 根據預設，對於含有 RAM 超過 1 GB 的裝置，此數量為 512 MB，否則預設值為 32 MB。  

- 選取 [啟用命令支援 (僅限測試)]  ，以在部署開機映像時，使用 **F8** 鍵開啟命令提示字元。 如果要在測試部署時進行疑難排解，此選項相當有用。 基於安全性考量，不建議在生產環境部署中使用此設定。  

- **設定 WinPE 中的預設鍵盤配置**： <!--4910348-->從 1910 版開始，請設定開機映像的預設鍵盤配置。 如果您選取 en-us 以外的語言，Configuration Manager 仍會在可用的輸入地區設定中包含 en-us。 在裝置上，初始鍵盤配置是選取的地區設定，但使用者可以視需要將裝置切換為 en-us。

> [!Tip]
> 使用 [Set-CMBootImage](https://docs.microsoft.com/powershell/module/configurationmanager/set-cmbootimage?view=sccm-ps) PowerShell Cmdlet 從指令碼中進行這些設定。

#### <a name="optional-components"></a>選擇性元件

在 [選用元件] 索引標籤上，指定已新增至 Windows PE 以搭配 Configuration Manager 使用的元件。 如需可用選用元件的詳細資訊，請參閱 [WinPE:Add packages (Optional Components Reference)](https://docs.microsoft.com/windows-hardware/manufacture/desktop/winpe-add-packages--optional-components-reference) (WinPE：新增套件 (選用元件參考))。  

下列元件均為 Configuration Manager 的必要項，一律會新增到開機映像：

- 指令碼 (WinPE-Scripting)
- 啟動 (WinPE-SecureStartup)
- 網路 (WinPE-WDS-Tools)
- 指令碼 (WinPE-WMI)

[元件] 清單會顯示其他已新增至此開機映像的項目。 若要新增更多元件，請選取金色星號。 若要移除元件，從清單中選取它，然後選取紅色的 X。

客戶通常會使用下列元件：

- Microsoft .NET (WinPE-NetFX)：此元件是 PowerShell 的先決條件。 它是較大型選擇性元件之一。  
- Windows PowerShell (WinPE-PowerShell)：此元件需要 .NET，並新增有限的 PowerShell 支援。 如果您在工作順序的 WinPE 階段期間執行自訂的 PowerShell 指令碼，請新增此元件。 有其他可能需要其他 PowerShell Cmdlet 的元件。
- HTML (WinPE-HTA)：如果您在工作順序的 WinPE 階段期間執行自訂的 HTML 應用程式，請新增此元件。

如需新增語言的詳細資訊，請參閱[設定多個語言](#BKMK_BootImageLanguage)。

#### <a name="data-source"></a>資料來源

在 [資料來源]  索引標籤上，更新下列其中一項設定：  

- 若要變更開機映像的來源檔案，請設定 [映像路徑] 和 [映像索引]。  

- 若要建立站台更新開機映像的排程，請選取 [按照排程更新發佈點]。  

- 如果不想要讓此套件的內容在用戶端快取中因到期而被清除以將空間騰出給其他內容使用，請選取 [將內容保存在用戶端快取中]。  

- 若要指定站台在更新發佈點上的開機映像套件時只發佈已變更的檔案，請選取 [啟用二進位差異複寫] (BDR)。 此設定可將站台間的網路流量降到最低。 當開機映像套件很大而變更相對較小時，BDR 特別有用。  

- 如果您是在支援 PXE 的部署中使用開機映像，請選取 [從支援 PXE 的發佈點部署此開機映像]。 如需詳細資訊，請參閱[使用 PXE 透過網路部署 Windows](../deploy-use/use-pxe-to-deploy-windows-over-the-network.md)。  

#### <a name="data-access"></a>資料存取

在 [資料存取] 索引標籤上，您可以設定套件共用設定。 如果您的環境中需要，請將選項設定為 [將此套件中的內容複製到發佈點上的套件共用]。 您接著會有 [針對套件共用使用自訂名稱] 的其他選項，並指定自訂的**共用名稱**。 當您啟用此選項時，發佈點上需要額外的磁碟空間。 它適用於所有接收此開機映像的發佈點。

#### <a name="distribution-settings"></a>發佈設定

在 [發佈設定]  索引標籤上，選取下列其中一項設定：  

- 在 [發佈優先順序] 清單中，指定優先順序層級。 當站台將多個套件發佈至相同的發佈點時，Configuration Manager 會使用此優先順序清單。  

- 如果您想要對慣用發佈點啟用隨選內容發佈，請選取 [啟用隨選發佈]。 啟用此設定時，如果用戶端要求套件的內容，而所有發佈點上都沒有該內容時，則管理點會發佈該內容。 如需詳細資訊，請參閱[依需求散發內容](../../core/plan-design/hierarchy/fundamental-concepts-for-content-management.md#on-demand-content-distribution)。  

- 若要指定要讓站台如何將開機映像發佈至已針對預先設置的內容啟用的發佈點，請設定 [預先設置的發佈點設定]。 如需預先設置內容的詳細資訊，請參閱 [Prestage content](../../core/servers/deploy/configure/deploy-and-manage-content.md#bkmk_prestage)。  

#### <a name="content-locations"></a>內容位置

在 [內容位置] 索引標籤上，選取發佈點或發佈點群組，並執行下列動作：  

- **驗證**：檢查所選取的發佈點或發佈點群組上開機映像套件的完整性。  

- **重新發佈**：將開機映像再次發佈到所選取的發佈點或發佈點群組。  

- **移除**：從所選取的發佈點或發佈點群組中刪除開機映像。  

#### <a name="security"></a>安全性

在 [安全性] 索引標籤上，檢視具備此物件權限的系統管理使用者。

## <a name="configure-a-boot-image-for-pxe"></a><a name="BKMK_BootImagePXE"></a> 設定適用於 PXE 的開機映像  

您需要設定開機映像以從支援 PXE 的發佈點進行部署，才能使用開機映像進行支援 PXE 的部署。  

1. 在 Configuration Manager 主控台中，前往 [軟體程式庫] 工作區，展開 [作業系統]，然後選取 [開機映像] 節點。  

2. 選取要修改的開機映像。  

3. 在功能區 [常用] 索引標籤的 [內容] 群組中，選取 [內容]。  

4. 在 [資料來源]  索引標籤上，選取 [從支援 PXE 的發佈點部署此開機映像] 。 如需詳細資訊，請參閱[使用 PXE 透過網路部署 Windows](../deploy-use/use-pxe-to-deploy-windows-over-the-network.md)。  

## <a name="configure-multiple-languages"></a><a name="BKMK_BootImageLanguage"></a> 設定多個語言

> [!TIP]
> 從 1910 版開始，請在開機映像的屬性上設定預設鍵盤配置。 如需詳細資訊，請參閱[自訂](#customization)。<!--4910348-->

開機映像與語言無關。 此功能可讓您在 WinPE 中時，使用一個開機映像以多種語言顯示工作順序文字。 請從開機映像 [選用元件] 索引標籤，納入適當的語言支援。接著，設定適當的工作順序變數以包含要顯示的語言。 所部署 OS 的語言不會受到 WinPE 中的語言所影響。 WinPE 向使用者顯示的語言取決於下列因素：  

- 當使用者從現有 OS 執行工作順序時，Configuration Manager 會自動使用為該使用者所設定的語言。 當工作順序因為強制部署期限的結果而自動執行時，Configuration Manager 會使用 OS 的語言。  

- 針對使用 PXE 或媒體的 OS 部署，在 **SMSTSLanguageFolder** 變數中設定語言識別碼值，以作為啟動前置命令的一部分。 電腦開機至 WinPE 時，會以您在變數中指定的語言來顯示訊息。 如果存取指定資料夾內的語言資源檔案發生錯誤，或您未設定變數，WinPE 就會以預設語言顯示訊息。  

    > [!NOTE]  
    > 當您使用密碼保護媒體時，提示使用者輸入密碼的文字一律會以 WinPE 語言來顯示。  

使用下列程序，來設定適用於 PXE 或媒體初始之 OS 部署的 WinPE 語言。  

### <a name="set-the-windows-pe-language-for-a-pxe-or-media-initiated-os-deployment"></a>設定適用於 PXE 或媒體初始之 OS 部署的 Windows PE 語言  

1. 更新開機映像之前，請確認站台伺服器上對應的語言資料夾中有適當的工作順序資源檔 (tsres.dll)。 例如，英文資源檔位於下列位置：`<ConfigMgrInstallationFolder>\OSD\bin\x64\00000409\tsres.dll`  

2. 在啟動前置命令中，將 **SMSTSLanguageFolder** 環境變數設為適當的語言識別碼。 語言識別碼必須使用十進位而不是十六進位格式來指定。 例如，若要將語言識別碼設為英文，請指定十進位值 **1033**，而不是資料夾名稱的十六進位值 00000409。  
