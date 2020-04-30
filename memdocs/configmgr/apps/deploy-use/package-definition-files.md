---
title: 套件定義檔
titleSuffix: Configuration Manager
description: 了解如何在 Configuration Manager 中使用套件定義檔案建立套件和程式
ms.date: 07/26/2019
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 2de963d7-ffb9-43c3-9e1d-fc992b67bebd
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: 0d2d0dcad06c18b13b337185ae1feb768a7ee323
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81689326"
---
# <a name="package-definition-files"></a>套件定義檔

適用於：  Configuration Manager (最新分支)

套件定義檔是指令碼，可協助您在 Configuration Manager 中自動化建立[套件和程式](packages-and-programs.md)。 它們提供 Configuration Manager 建立套件和程式所需要的全部資訊，套件來源檔案的位置除外。

## <a name="about-the-package-definition-file-format"></a>關於套件定義檔的格式

每個套件定義檔都是使用 .ini 檔格式的 ASCII 或 UTF-8 文字檔。 它包含下列區段：  

### <a name="pdf"></a>[PDF]

本章節會將檔案識別封裝定義檔。 它包含下列資訊:  

- **版本**：指定檔案使用的套件定義檔案格式版本。 此版本會對應到寫入的 Configuration Manager 版本。 這是必要項目。  

### <a name="package-definition"></a>[封裝定義]

指定套件和程式的內容。 它提供下列資訊：  

- **名稱**：套件名稱，最多 50 個字元。  

- **版本** (選擇性)：套件版本，最多 32 個字元。  

- **圖示** (選擇性)：包含要用於此套件圖示的檔案。 如果指定，此圖示會取代 Configuration Manager 主控台中的預設套件圖示。

- **發行者**：套件的發行者，最多 32 個字元。

- **語言**：套件的語言版本，最多 32 個字元。

- **註解** (選擇性)：套件的相關註解，不可超過 127 個字元。

- **ContainsNoFiles**：這個項目指出套件是否有任何來源檔案。  

- **程式**：您為此套件定義的程式。 每個程式名稱會對應至 **[程式]** 這個封裝定義檔中的一節。  

    範例：  

    `Programs=Typical, Custom, Uninstall`  

- **MIFFileName**：包含套件狀態的管理資訊格式 (MIF) 檔案名稱，最多 50 個字元。  

- **MIFName**：用於 MIF 比對的套件名稱，最多 50 個字元。  

- **MIFVersion**：用於 MIF 比對的套件版本號碼，最多 32 個字元。  

- **MIFPublisher**：用於 MIF 比對的套件軟體發行者，最多 32 個字元。  

### <a name="program"></a>[程式]

在 [套件定義]  區段中，為您在 [程式]  項目中指定的每個程式，包含 [程式] 區段。 這個區段會定義每個程式。 每個程式區段都會提供以下資訊：  

- **名稱**：程式名稱，最多 50 個字元。 此項目必須是唯一在封裝內。  

- **圖示** (選擇性)：指定包含要用於此程式之圖示的檔案。 此圖示會取代 Configuration Manager 主控台中的預設程式圖示。 當您將程式部署至集合時，用戶端也會顯示此圖示。

- **註解** (選擇性)：程式的相關註解，不可超過 127 個字元。

- **CommandLine**：指定程式的命令列，不可超過 127 個字元。 此命令為相對於套件來源資料夾。

- **StartIn**：指定程式的工作資料夾，不可超過 127 個字元。 這個項目可以是用戶端電腦上的絕對路徑，或套件來源資料夾的相對路徑。

- **執行**：指定程式會執行的程式模式。 您可以指定 **最小化**, ， **最大化**, ，或 **隱藏**。 如果您未包含這個項目，則會以一般模式執行程式。  

- **AfterRunning**：指定在程式順利完成之後發生的任何特殊動作。 可用選項有 **SMSRestart**, ， **ProgramRestart**, ，或 **SMSLogoff**。 如果您未包含這個項目，程式就不執行特殊動作。  

- **EstimatedDiskSpace**：指定軟體程式在電腦上執行所需的磁碟空間量。 預設值為 [未知]  。 您可以將值指定為大於或等於零的整數。 如果您指定值，也要包含值的單位。  

    範例：  

    `EstimatedDiskSpace=38MB`  

- **EstimatedRunTime**：指定您預期程式在用戶端電腦上執行的預估持續時間 (分鐘)。 預設值為 **120**。 您可以將值設定為大於零的整數，或**未知**。  

    範例：  

    `EstimatedRunTime=25`  

- **SupportedClients**：指定這個程式執行所在的處理器和作業系統。 以逗號分隔平台。 如果您未包含這個項目，用戶端就不會檢查此程式的支援平台。  

- **SupportedClientMinVersionX**、**SupportedClientMaxVersionX**：指定 **SupportedClients** 項目中指定的作業系統版本號碼的開始到結束範圍。  

    範例：  

    ```INI
    SupportedClients=Win NT (I386),Win NT (IA64),Win NT (x64)  
    Win NT (I386) MinVersion1=5.00.2195.4  
    Win NT (I386) MaxVersion1=5.00.2195.4  
    Win NT (I386) MinVersion2=5.10.2600.2  
    Win NT (I386) MaxVersion2=5.10.2600.2  
    Win NT (I386) MinVersion3=5.20.0000.0  
    Win NT (I386) MaxVersion3=5.20.9999.9999  
    Win NT (I386) MinVersion4=5.20.3790.0  
    Win NT (I386) MaxVersion4=5.20.3790.2  
    Win NT (I386) MinVersion5=6.00.0000.0  
    Win NT (I386) MaxVersion5=6.00.9999.9999  
    Win NT (IA64) MinVersion1=5.20.0000.0  
    Win NT (IA64) MaxVersion1=5.20.9999.9999  
    Win NT (x64) MinVersion1=5.20.0000.0  
    Win NT (x64) MaxVersion1=5.20.9999.9999  
    Win NT (x64) MinVersion2=5.20.3790.0  
    Win NT (x64) MaxVersion2=5.20.9999.9999  
    Win NT (x64) MinVersion3=5.20.3790.0  
    Win NT (x64) MaxVersion3=5.20.3790.2  
    Win NT (x64) MinVersion4=6.00.0000.0  
    Win NT (x64) MaxVersion4=6.00.9999.9999
    ```  

- **AdditionalProgramRequirements** (選擇性)：提供用戶端電腦的任何其他資訊或需求，不可超過 127 個字元。

- **CanRunWhen**：指定程式在用戶端電腦上執行所需的使用者狀態。 可用的值為 **UserLoggedOn**, ， **NoUserLoggedOn**, ，或 **AnyUserStatus**。 預設值是 **UserLoggedOn**。  

- **UserInputRequired**：指定程式是否需要與使用者互動。 可用的值為 **True** 或 **False**。 預設值是 **True**。 如果 **CanRunWhen** 未設定為 **UserLoggedOn**，此項目會設定為 **False**。  

- **AdminRightsRequired**：指定程式是否需要電腦上的系統管理認證才能執行。 可用的值為 **True** 或 **False**。 預設值為 **False**。 如果 **CanRunWhen** 未設定為 **UserLoggedOn**，此項目會設定為 **True**。  

- **UseInstallAccount**：指定程式在用戶端電腦上執行時是否使用用戶端軟體安裝帳戶。 根據預設，這個值是 **False**。 此值也是 **False** 如果 **CanRunWhen** 設為 **UserLoggedOn**。  

- **DriveLetterConnection**：指定程式是否需要與發佈點上套件檔案的磁碟機代號連線。 您可以指定 **True** 或 **False**。 預設值為 **False**，可讓程式使用通用命名慣例 (UNC) 連線。 這個值設定為 **True** 時，用戶端會使用下一個可用的磁碟機代號 (從 Z: 開始，並往回處理)。  

- **SpecifyDrive** (選擇性)：指定程式連線到發佈點上套件檔案所需的磁碟機代號。 此設定會強制使用指定的磁碟機代號給用戶端連線到發佈點。

- **ReconnectDriveAtLogon**：指定電腦是否在使用者登入時重新連線到發佈點。 可用的值為 **True** 或 **False**。 預設值為 **False**。  

- **DependentProgram**：指定這個套件中必須在目前程式之前執行的程式。 此項目使用 `DependentProgram=<ProgramName>` 格式，其中 `<ProgramName>` 是套件定義檔中該程式的**名稱**項目。 如果不有任何相依的程式，將此項目保留空白。  

    範例：  

    `DependentProgram=Admin`  
    `DependentProgram=`  

- **指派**：指定如何將程式指派給使用者。 此值可以是：

    - **FirstUser**：只有登入用戶端的第一個使用者可以執行程式
    - **EveryUser**：每個登入的使用者都可以執行程式

    當 **CanRunWhen** 未設定為 **UserLoggedOn** 時，此項目設定為 **FirstUser**。  

- **Disabled**：指定是否可以將此程式部署至用戶端。 可用的值為 **True** 或 **False**。 預設值為 **False**。  


## <a name="use-a-package-definition-file"></a>使用套件定義檔案  

1. 在 Configuration Manager 主控台中，移至 [軟體程式庫]  工作區，展開 [應用程式管理]  ，然後選取 [套件]  節點。  

2. 在功能區的 [首頁]  索引標籤上，選擇 [建立]  群組中的 [從定義建立套件]  。  

3. 在 [從定義建立套件精靈]  的 [套件定義]  頁面上，選擇現有套件定義檔。 若要開啟新的套件定義檔，請選擇 [瀏覽]  。 指定新的套件定義檔之後，請從 [套件定義]  清單中選取。

4. 在 [來源檔案]  頁面上，指定與套件和程式的任何必要來源檔案有關的資訊。  

5. 如果套件需要來源檔案，請在 [來源資料夾]  頁面上指定可以從中取得來源檔案的位置。  

6. 完成精靈。  


## <a name="see-also"></a>請參閱

[套件和程式](packages-and-programs.md)
