---
title: 語言套件
titleSuffix: Configuration Manager
description: 了解 Configuration Manager 中可用的語言支援。
ms.date: 06/29/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: cd74e5f5-33f6-4566-8c9d-d6a93bfe71ed
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 53aa7e932e782254f63b422526b315f3ce91f397
ms.sourcegitcommit: 214fb11771b61008271c6f21e17ef4d45353788f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/07/2020
ms.locfileid: "82906162"
---
# <a name="language-packs-in-configuration-manager"></a>Configuration Manager 中的語言套件

適用於：  Configuration Manager (最新分支)

本文提供關於 Configuration Manager 中語言支援的技術詳細資料。 Configuration Manager 站台伺服器和用戶端被視為非語言相關的。 在管理中心網站和主要站台上安裝**伺服器語言套件**或**用戶端語言套件**，即可新增對顯示語言的支援。 在站台安裝程序期間，您可以從可用的語言套件檔案中選取要在該站台支援的伺服器和用戶端語言。
 
在每個站台上安裝多種語言。 您只需安裝要使用的語言。  

- 每個站台均針對 Configuration Manager 主控台支援多種語言。  

- 在每個站台上安裝個別的用戶端語言套件，只針對您想要支援的用戶端語言新增支援。  

當您安裝與下列元件相符的語言支援時：  

- 電腦的顯示語言：在該電腦上執行的 Configuration Manager 主控台和用戶端使用者介面都會以該語言顯示資訊。  

- 電腦之網頁瀏覽器所使用的語言喜好設定：與 Web 型資訊的連線 (包括應用程式類別目錄或 SQL Server Reporting Services) 會以該語言顯示。  


當您執行 Configuration Manager 安裝程式時，它會下載語言套件檔案作為必要條件和可轉散發檔案的一部分。 您也可以先使用[安裝程式下載程式](setup-downloader.md)來下載這些檔案，然後再執行安裝程式。   



## <a name="server-languages"></a>伺服器語言  

使用下表來將地區設定識別碼對應到您想要在伺服器上支援的語言。 如需地區設定識別碼的詳細資訊，請參閱 [Microsoft 指派的地區設定識別碼](https://docs.microsoft.com/openspecs/windows_protocols/ms-lcid/a9eac961-e77d-41a6-90a5-ce1a8b0cdb9c)。  

|伺服器語言|地區設定識別碼 (LCID)|三個字母的代碼|  
|---------------------|------------------------|-----------------------|  
|英文 (預設值)|0409|ENU|  
|中文 (簡體)|0804|CHS|  
|中文 (繁體，台灣)|0404|CHT|  
|捷克文|0405|CSY|  
|荷蘭文 - 荷蘭|0413|NLD|  
|法文|040c|FRA|  
|德文|0407|DEU|  
|匈牙利文|040e|HUN|  
|義大利文 - 義大利|0410|ITA|  
|日文|0411|JPN|  
|韓文|0412|KOR|  
|波蘭文|0415|PLK|  
|葡萄牙文 - 巴西|0416|PTB|  
|葡萄牙文 - 葡萄牙|0816|PTG|  
|俄文|0419|RUS|  
|西班牙文 - 西班牙|0c0a|ESN|  
|瑞典文|041d|SVE|  
|土耳其文|041f|TRK|  



## <a name="client-languages"></a>用戶端語言  

使用下表來將地區設定識別碼對應到您想要在用戶端電腦上支援的語言。 如需地區設定識別碼的詳細資訊，請參閱 [Microsoft 指派的地區設定識別碼](https://docs.microsoft.com/openspecs/windows_protocols/ms-lcid/a9eac961-e77d-41a6-90a5-ce1a8b0cdb9c)。  

|用戶端語言|地區設定識別碼 (LCID)|三個字母的代碼|  
|---------------------|------------------------|-----------------------|  
|英文 (預設值)|0409|ENG|  
|中文 - 簡體|0804|CHS|  
|中文 (繁體，台灣)|0404|CHT|  
|捷克文|0405|CSY|  
|丹麥文|0406|DAN|  
|荷蘭文 - 荷蘭|0413|NLD|  
|芬蘭文|040b|FIN|  
|法文|040c|FRA|  
|德文|0407|DEU|  
|希臘文|0408|ELL|  
|匈牙利文|040e|HUN|  
|義大利文 - 義大利|0410|ITA|  
|日文|0411|JPN|  
|韓文|0412|KOR|  
|挪威文|0414|NOR|  
|波蘭文|0415|PLK|  
|葡萄牙文 (巴西)|0416|PTB|  
|葡萄牙文 (葡萄牙)|0816|PTG|  
|俄文|0419|RUS|  
|西班牙文 - 西班牙|0c0a|ESN|  
|瑞典文|041d|SVE|  
|土耳其文|041f|TRK|  


### <a name="mobile-device-client-languages"></a>行動裝置用戶端語言  
新增行動裝置語言支援時，所有支援的行動裝置用戶端語言皆包含在內。 您不能針對行動裝置支援選取個別語言套件。  



## <a name="identify-installed-language-packs"></a>識別已安裝的語言套件  
若要識別 Configuration Manager 用戶端執行電腦所安裝的語言套件，請在電腦登錄中尋找已安裝語言套件的地區設定識別碼 (LCID)。 此資訊可在下列登錄路徑上取得：  

`HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\CCMSetup\InstalledLangs`  

自訂硬體清查來收集此資訊。 接著建置自訂報告來檢視語言詳細資料。 如需收集自訂硬體清查的詳細資訊，請參閱[如何設定硬體清查](../../../clients/manage/inventory/configure-hardware-inventory.md)。 如需詳細資訊，請參閱[建立報表](../../manage/operations-and-maintenance-for-reporting.md#create-reports)。
