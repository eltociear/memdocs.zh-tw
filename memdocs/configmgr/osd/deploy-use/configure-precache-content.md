---
title: 設定預先快取內容
titleSuffix: Configuration Manager
description: 了解用戶端如何在使用者安裝工作順序之前下載 OS 部署內容。
ms.date: 02/26/2020
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 9d1e8252-99e3-48aa-bfa5-0cf4cd6637b2
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: ec465f3dee33ca311aec120e74a2994a81a90ec9
ms.sourcegitcommit: 0b30c8eb2f5ec2d60661a5e6055fdca8705b4e36
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/05/2020
ms.locfileid: "84455220"
---
# <a name="configure-pre-cache-content-for-task-sequences"></a>設定工作順序的預先快取內容

適用於：Configuration Manager (最新分支)

<!--1021244-->
工作順序之可用部署的預先快取功能，可讓用戶端在使用者安裝工作順序之前下載相關內容。 用戶端可以預先快取[升級 OS](create-a-task-sequence-to-upgrade-an-operating-system.md) 或[安裝 OS 映像](create-a-task-sequence-to-install-an-operating-system.md)的工作順序內容。

> [!Note]  
> 在 1910 版中，Configuration Manager 預設會啟用此功能。 在 1906 版或更早版本中，Configuration Manager 預設不會啟用此選擇性功能。 您必須先先啟用這項功能才能使用它。 如需詳細資訊，請參閱[從更新啟用選擇性功能](../../core/servers/manage/install-in-console-updates.md#bkmk_options)。<!--505213-->  

例如，您只想要適用於所有使用者的單一就地升級工作順序，而且具有許多架構和語言。 在舊版中，使用者從軟體中心安裝可用的工作順序部署時，就會開始下載內容。 此延遲會增加準備開始安裝之前的額外時間。 工作順序中參考的所有內容均可下載。 此內容包含所有語言和架構的 OS 升級套件。 如果每個升級套件的大小大約是 3 GB，則總內容十分龐大。

預先快取的內容可讓您選擇讓用戶端在一收到部署時，只下載適用的內容以及所有其他參考內容。 當使用者在軟體中心按一下 [安裝] 時，內容已就緒。 因為內容是位在本機硬碟機上，所以安裝會快速啟動。

在 Configuration Manager 1902 版和更早版本中，此行為僅適用於「OS 升級套件」。 該套件是您在其中指定相符架構或語言的唯一內容。 例如，如果工作順序也會參考多個驅動程式套件，用戶端會將它們全部下載。 工作順序引擎會在工作順序執行時評估步驟的條件，而不會預先評估。 用戶端會使用套件內容上的標記來判斷要預先快取的內容。

從 1906 版開始，<!--4224642--> 您可以使用預先快取來降低下列內容類型的頻寬使用量：

- OS 升級套件
- OS 映像
- 驅動程式套件
- 套件

## <a name="configure-pre-caching"></a>設定預先快取

設定預先快取功能有三個步驟：

1. [建立並設定套件](#bkmk_createpkg)
2. [建立含有條件式步驟的工作順序](#bkmk_createts)
3. [部署工作順序並啟用預先快取](#bkmk_deploy)


### <a name="1-create-and-configure-the-packages"></a><a name="bkmk_createpkg"></a> 1.建立並設定套件

用戶端會評估套件的屬性，以判斷在預先快取期間所下載的內容。  

#### <a name="os-upgrade-package"></a>OS 升級套件

建立適用於特定架構和語言的 [OS 升級套件](../get-started/manage-operating-system-upgrade-packages.md)。 在其內容的 [資料來源] 索引標籤中指定 [架構] 和 [語言]。

#### <a name="os-image"></a>作業系統映像

建立適用於特定架構和語言的 [OS 映像](../get-started/manage-operating-system-images.md)。 在其內容的 [資料來源] 索引標籤中指定 [架構] 和 [語言]。

#### <a name="driver-package"></a>驅動程式套件

針對特定硬體型號建立[驅動程式套件](../get-started/manage-drivers.md#BKMK_ManagingDriverPackages)。 在其屬性的 [一般] 索引標籤上指定 [型號]。

為判斷它在預先快取期間下載哪個驅動程式套件，用戶端會針對 **Win32_ComputerSystemProduct** WMI 類別的 **Name** 屬性評估模型。

> [!TIP]
> 實際查詢會使用具有萬用字元的 `LIKE` 陳述式：`select * from win32_computersystemproduct where name like "%yourstring%"`。 例如，如果您將 `Surface` 指定為型號，則查詢會比對包含該字串的所有型號。<!-- 6315551 -->

#### <a name="package"></a>套件

建立適用於特定架構和語言的[套件](../../apps/deploy-use/packages-and-programs.md)。 在其內容的 [一般] 索引標籤中指定 [架構] 和 [語言]。


### <a name="2-create-a-task-sequence"></a><a name="bkmk_createts"></a> 2.建立工作順序

針對不同語言和架構建立含有條件式步驟的工作順序，或針對驅動程式套件建立包含不同硬體型號的工作順序。

|Content|步驟|
|---------|---------|
|OS 升級套件|[升級 OS](../understand/task-sequence-steps.md#BKMK_UpgradeOS)|
|作業系統映像|[套用 OS 映像](../understand/task-sequence-steps.md#BKMK_ApplyOperatingSystemImage)|
|驅動程式套件|[套用驅動程式套件](../understand/task-sequence-steps.md#BKMK_ApplyDriverPackage)|
|套件|[安裝套件](../understand/task-sequence-steps.md#BKMK_InstallPackage)|

例如，以下**升級 OS** 步驟使用英文版本：  

![工作順序編輯器，其中顯示適用於 ENU、DEU 和 JPN 的多個升級 OS 步驟](../media/precacheproperties2.png)

![工作順序編輯器 的 [選項] 索引標籤，其中顯示適用於地區設定和 OSArchitecture 的 WMI WQL 查詢](../media/precacheoptions2.png)  

> [!Tip]
> 針對英文 (美國) OS 和 64 位元架構，建議使用下列 WMI 查詢：
>
> ```WMI
> SELECT * FROM Win32_OperatingSystem WHERE OSArchitecture LIKE '%64%' AND OSLanguage='1033'
> ```
>
> 請先選取**作業系統語言**條件來新增語言。 然後編輯 WMI 查詢來包含架構子句。

### <a name="3-deploy-the-task-sequence"></a><a name="bkmk_deploy"></a> 3.部署工作順序

[部署工作順序](deploy-a-task-sequence.md)。 針對預先快取功能，進行下列設定：  

- 在 [一般] 索引標籤上，選取 「Pre-download content for this task sequence」 (此工作順序的下載前內容)。  

- 在 [部署設定] 索引標籤上，將工作順序設定為 [可用]。  

- 在 [排程] 索引標籤上，針對 [排程此部署的可用時間] 設定，選擇設定目前選取的時間。 用戶端會在部署可用時間開始預先快取內容。 目標用戶端收到這個原則時，可用時間會是過去時間，因此會立即開始預先快取下載。 如果用戶端收到此原則，但可用時間是未來時間，則除非有可用的時間，否則用戶端無法開始預先快取內容。  

- 在 [發佈點] 索引標籤上，設定 [部署選項] 設定。 如果未在使用者開始安裝之前預先快取內容，用戶端就會使用這些設定。  

    > [!Important]  
    > 針對安裝 OS 映像的工作順序，請勿使用 [視執行工作順序所需，將內容下載到本機] 的部署選項。 當工作順序在套用 OS 映像之前抹除磁碟時，將會移除用戶端快取。 由於內容已消失，因此工作順序會失敗。<!-- SCCMDocs-PR #1338 --> 這些部署選項會根據您為部署選取的其他選項而變動。 如需詳細資訊，請參閱 [Deploy a task sequence](deploy-a-task-sequence.md#bkmk_deploy-options)。<!-- MEMDocs#328, SCCMDocs#2114 -->

## <a name="user-experience"></a>使用者經驗

- 當用戶端收到部署原則時，就會在部署的可用時間之後開始預先快取內容。 此內容包括所有參考的套件，但僅包含符合套件上之架構和語言屬性的 OS 升級套件。  

- 當用戶端提供使用者可以使用的部署時，即會顯示通知，告知使用者有新的部署。 現在會在軟體中心顯示工作順序。 使用者可以前往軟體中心，然後按一下 [安裝] 開始安裝。  

- 如果使用者安裝工作順序時用戶端未完全預先快取內容，則用戶端會使用您在部署之 [部署選項] 索引標籤上指定的設定。  

## <a name="see-also"></a>請參閱

- [建立工作順序以升級 OS](create-a-task-sequence-to-upgrade-an-operating-system.md)
- [將 Windows 升級至最新版本的案例](upgrade-windows-to-the-latest-version.md)
