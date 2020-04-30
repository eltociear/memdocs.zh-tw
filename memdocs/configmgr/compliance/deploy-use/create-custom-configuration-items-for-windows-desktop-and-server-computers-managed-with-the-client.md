---
title: 建立自訂設定項目
titleSuffix: Configuration Manager
description: 使用 Windows 桌上型電腦與伺服器的自訂設定項目來管理 Windows 電腦與伺服器的設定
ms.date: 04/14/2020
ms.prod: configuration-manager
ms.technology: configmgr-compliance
ms.topic: conceptual
ms.assetid: 1eb2fcaf-acac-4388-9b31-6cccafacaabe
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 63f11066918854d72af0f1160d7d7569a93d7ebe
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81692516"
---
# <a name="create-custom-configuration-items-for-windows-desktop-and-server-computers-managed-with-the-configuration-manager-client"></a>為 Configuration Manager 用戶端所管理的 Windows 桌上型電腦與伺服器電腦建立自訂設定項目

適用於：  Configuration Manager (最新分支)


使用 Configuration Manager **自訂 Windows 桌上型電腦與伺服器**設定項目，管理 Configuration Manager 用戶端所管理之 Windows 電腦與伺服器的設定。  



## <a name="start-the-wizard"></a>啟動精靈

1. 在 Configuration Manager 主控台中，移至 [資產與合規性]  工作區，展開 [合規性設定]  ，然後選取 [設定項目]  節點。  

2. 在功能區 [常用]  索引標籤上的 [建立]  群組中，選取 [建立設定項目]  。  

3. 在 [建立設定項目精靈]  的 [一般]  頁面上，指定設定項目的名稱和選擇性描述。  

4. 在 [指定您要建立的組態項目類型]  下，選取 [Windows 桌上型電腦和伺服器 (自訂)]  。  

    > [!TIP]  
    > 如果您要提供偵測方法設定以檢查是否有應用程式，請選取 [此組態檔案包含應用程式設定]  。  

5. 為協助您在 Configuration Manager 主控台中搜尋及篩選設定項目，請選取 [類別]  以建立及指派類別。  



## <a name="detection-methods"></a>偵測方法  

您可以使用這個程序，來提供組態項目的偵測方法資訊。  

> [!NOTE]  
> 只有當您選取精靈 [一般]  頁面上的 [此設定項目包含應用程式設定]  時，此資訊才適用。  

Configuration Manager 中的偵測方法包含用來偵測電腦上是否安裝應用程式的規則。 這項偵測會在用戶端評定設定項目的合規性之前進行。 若要偵測是否已安裝應用程式，您可以偵測應用程式的 Windows Installer 檔案是否存在，使用自訂指令碼，或選取 **一律假設應用程式安裝** 評估不論是否已安裝應用程式的合規性的組態項目。  


### <a name="to-detect-an-application-installation-by-using-the-windows-installer-file"></a>使用 Windows Installer 檔案來偵測應用程式安裝  

1. 在 [建立設定項目精靈]  的 [偵測方法]  頁面上，選取 [使用 Windows Installer 偵測]  選項。  

2. 選取 [開啟]  ，瀏覽到您要偵測的 Windows Installer (.msi) 檔案，然後選取 [開啟]  。  

3. [版本]  欄位會自動填入所選取 Windows Installer 檔案的版本號碼。 如果顯示的值不正確，請在此欄位輸入新的版本號碼。  

4. 若要偵測電腦上的每個使用者設定檔，請選取 [已針對一個或多個使用者安裝此應用程式]  。  


### <a name="to-detect-a-specific-application-and-deployment-type"></a>偵測特定應用程式和部署類型  

1. 在 [建立設定項目精靈]  的 [偵測方法]  頁面上，選取 [偵測特定應用程式和部署類型]  。 選擇 [選取]  。   

2. 在 [指定應用程式]  對話方塊中，選取您要偵測的應用程式和相關聯的部署類型。  


### <a name="to-detect-an-application-installation-by-using-a-custom-script"></a>使用自訂指令碼偵測應用程式安裝  

1. 在 [建立設定項目精靈]  的 [偵測方法]  頁面上，選取 [使用自訂指令碼來偵測此應用程式]  選項。  

2. 在清單中選取指令碼的語言。 選擇下列格式：  

    - **VBScript**  

    - **JScript**  

    - **PowerShell**  

        > [!Note]  
        > 從 1810 版開始，當 Windows PowerShell 指令碼以偵測方法的形式執行時，Configuration Manager 用戶端會搭配 `-NoProfile` 參數呼叫 PowerShell。 此選項會啟動 PowerShell，但不含設定檔。 PowerShell 設定檔是在 PowerShell 啟動時執行的指令碼。 <!--3607762-->  

3. 選取 [開啟舊檔]  ，瀏覽至您要使用的指令碼，然後選取 [開啟]  。  



## <a name="specify-supported-platforms"></a>指定支援的平台  

在 [建立設定項目精靈]  的 [支援的平台]  頁面上，選取您要評估設定項目合規性所在的 Windows 版本，或選擇 [全選]  。

您也可以**手動指定 Windows 的版本**。 選取 [新增]  並指定 Windows 組建編號的各個部分。

> [!NOTE]
> 指定 Windows Server 2016 時，`All Windows Server 2016 and higher 64-bit)` 的選項也包含 Windows Server 2019。 若只要指定 Windows Server 2016，請使用**手動指定 Windows 版本**的選項。 <!--5866480-->



##  <a name="configure-settings"></a>進行設定  

您可以使用這個程序，來進行組態項目中的設定。  

設定代表商務或技術可用來評估用戶端裝置上的符合性的條件。 您可以進行新的設定，或瀏覽至參照電腦上現有的設定。  

1. 在 [建立設定項目精靈]  的 [設定]  頁面上，選取 [新增]  。  

2. 在 **一般**  索引標籤 **建立設定**  對話方塊中，提供下列資訊:  

    - **名稱**：輸入設定的唯一名稱。 您最多可以使用 256 個字元。  

    - **描述**：輸入設定的描述。 您最多可以使用 256 個字元。  

    - **設定類型**︰在清單中選擇並設定要用於此項設定的其中一個設定類型：  
        - [Active Directory 查詢](#bkmk_adquery)
        - [組件](#bkmk_assembly)
        - [檔案系統](#bkmk_file)
        - [IIS Metabase](#bkmk_iis)
        - [登錄機碼](#bkmk_regkey)
        - [登錄值](#bkmk_regval)
        - [指令碼](#bkmk_script)
        - [SQL 查詢](#bkmk_sql)
        - [WQL 查詢](#bkmk_wql)
        - [XPath 查詢](#bkmk_xpath)

    - **資料類型**：選擇條件傳回資料所使用的格式，再使用條件來評估設定。 並非所有設定類型都會顯示 [資料類型]  清單。  

        > [!Tip]  
        > **浮點數**資料類型只支援小數點後有三個數字。  

3. 設定此設定下的其他詳細 **類型設定** 清單。 您可以設定的項目會因您所選取的設定類型而異。  

4. 選取 [確定]  以儲存設定，然後關閉 [建立設定]  對話方塊。  


### <a name="active-directory-query"></a><a name="bkmk_adquery"></a> Active Directory 查詢

- **LDAP 首碼**：為 Active Directory 網域服務查詢指定有效的首碼，以評估用戶端電腦上的合規性。 若要執行通用類別目錄搜尋，請使用 `LDAP://` 或 `GC://`。  

- **辨別名稱 (DN)** ：指定評估是否符合用戶端電腦上合規性之 Active Directory 網域服務物件的辨別名稱。  

- **搜尋篩選器**：指定選擇性 LDAP 篩選器以縮小 Active Directory 網域服務查詢的結果搜尋範圍，以評估用戶端電腦上的合規性。 若要從查詢傳回所有結果，請輸入 `(objectclass=*)`。  

- **搜尋範圍**：指定 Active Directory 網域服務中的搜尋範圍  

    - **基本**：僅查詢指定的物件  

    - **單層**：在此 Configuration Manager 版本中不使用此選項  

    - **樹狀子目錄**：查詢指定的物件以及該物件在目錄中的完整樹狀子目錄  

- **屬性**：指定用來評估用戶端電腦上合規性之 Active Directory 網域服務物件的屬性。  

    例如，如果您要查詢 Active Directory 屬性 (儲存使用者不正確輸入密碼的次數)，請在此欄位中輸入 `badPwdCount`。  

- **查詢**：顯示從 [LDAP 首碼]  、[辨別名稱 (DN)]  、[搜尋篩選器]  \(若已指定\) 與 [屬性]  建構的查詢。  


### <a name="assembly"></a><a name="bkmk_assembly"></a> 組件

該組件是可在應用程式間共用的一組代碼。 組件的副檔名可以是 .dll 或 .exe。 全域組件快取是用戶端電腦上的 `%SystemRoot%\Assembly` 資料夾。 此快取是 Windows 儲存所有共用組件的位置。  

- **組件名稱：** 指定您想要搜尋的組件物件名稱。 名稱不能與相同類型的其他組件物件相同。 請先在全域組件快取中註冊名稱， 組件名稱的長度上限為 256 個字元。  


### <a name="file-system"></a><a name="bkmk_file"></a> 檔案系統

- **類型**：在此清單中，選取您要搜尋 [檔案]  或 [資料夾]  。  

- **路徑**：指定用戶端電腦上指定的檔案或資料夾的路徑。 您可以指定系統環境變數和路徑中的 `%USERPROFILE%` 環境變數。  

    > [!NOTE]  
    > 如果在 [路徑]  或 [檔案或資料夾名稱]  方塊中使用 `%USERPROFILE%` 環境變數，則 Configuration Manager 用戶端會搜尋用戶端電腦上的所有使用者設定檔。 此行為可能會導致找到多個檔案或資料夾的執行個體。  
    >   
    > 如果合規性設定無法存取指定的路徑，則會產生探索錯誤。 此外，如果您要搜尋的檔案目前正在使用中，探索會產生錯誤。  

    > [!Tip]  
    > 選取 [瀏覽]  ，以從參照電腦上的值進行設定。   

- **檔案或資料夾名稱**：指定要搜尋之檔案或資料夾物件的名稱。 您可以指定系統環境變數和檔案或資料夾名稱中的 `%USERPROFILE%` 環境變數。 您也可以在檔案名稱中使用萬用字元 `*` 與 `?`。  

    > [!NOTE]  
    > 如果您指定檔案或資料夾名稱並使用萬用字元，此組合這可能會產生大量的結果。 這也可能導致大量耗用用戶端電腦上的資源，而且在向 Configuration Manager 報告結果時會產生相當高的網路流量。  

- **包含子資料夾**：一併搜尋指定路徑下的所有子資料夾。  

- **此檔案或資料夾與 64 位元應用程式建立關聯**：若啟用，則只會搜尋 64 位元的檔案位置，例如 64 位元電腦上的 `%ProgramFiles%`。 若未啟用此選項，則會同時搜尋 64 位元位置和 32 位元位置，例如 `%ProgramFiles(x86)%`。  

    > [!NOTE]  
    > 如果同一部 64 位元電腦上的 64 位元和 32 位元系統檔案位置中同時存在相同的檔案或資料夾，則全域條件會探索多個檔案。  

    [檔案系統]  設定類型不支援在 [路徑]  方塊中將 UNC 路徑指定為網路共用。  


### <a name="iis-metabase"></a><a name="bkmk_iis"></a> IIS Metabase

- **Metabase 路徑**：指定 Internet Information Services (IIS) Metabase 的有效路徑。 例如 `/LM/W3SVC/`。  

- **內容識別碼**：指定 IIS Metabase 設定的數值內容。  


### <a name="registry-key"></a><a name="bkmk_regkey"></a> 登錄機碼

- **登錄區**：選取所要搜尋的登錄區

    > [!Tip]  
    > 選取 [瀏覽]  ，以從參照電腦上的值進行設定。 若要瀏覽至遠端電腦上的登錄機碼，請在該遠端電腦上啟用**遠端登錄**服務。  

- **索引鍵**：指定要搜尋的登錄機碼名稱。 請使用 `key\subkey` 格式。  

- **這個登錄機碼已與 64 位元應用程式相關聯**：除了 32 位元登錄機碼之外，也在執行 64 位元版本 Windows 的用戶端上搜尋 64 位元登錄機碼。  

    > [!NOTE]  
    > 如果同一部 64 位元電腦上的 64 位元和 32 位元登錄位置中同時存在相同的登錄機碼，則全域條件會同時探索這兩個登錄機碼。  


### <a name="registry-value"></a><a name="bkmk_regval"></a> 登錄值

- **登錄區**：選取所要搜尋的登錄區。  

    > [!Tip]  
    > 選取 [瀏覽]  ，以從參照電腦上的值進行設定。 若要瀏覽至遠端電腦上的登錄值，請在該遠端電腦上啟用**遠端登錄**服務。 您也必須具有系統管理員權限，才能存取該遠端電腦。  

- **索引鍵**：指定要搜尋的登錄機碼名稱。 請使用 `key\subkey` 格式。  

- **值**：指定必須包含在所指定登錄機碼內的值。  

- **這個登錄機碼已與 64 位元應用程式相關聯**：除了 32 位元登錄機碼之外，也在執行 64 位元版本 Windows 的用戶端上搜尋 64 位元登錄機碼。  

    > [!NOTE]  
    > 如果同一部 64 位元電腦上的 64 位元和 32 位元登錄位置中同時存在相同的登錄機碼，則全域條件會同時探索這兩個登錄機碼。  


### <a name="script"></a><a name="bkmk_script"></a> 指令碼

指令碼傳回的值可用來評估全域條件的相容性。 例如，使用 VBScript 時，您可以使用命令 **WScript.Echo Result** 將 *Result* 變數值傳回至全域條件。  

- **探索指令碼**：選取 [新增指令碼]  ，然後輸入或瀏覽至指令碼。 此指令碼可用來尋找值。 您可以使用 Windows PowerShell、 VBScript、 或 Microsoft JScript 指令碼。  

- **補救指令碼 (選擇性)** ：選取 [新增指令碼]  ，然後輸入或瀏覽至指令碼。 此指令碼可用來補救不符合規範的設定值。 您可以使用 Windows PowerShell、 VBScript、 或 Microsoft JScript 指令碼。  

- **使用登入的使用者認證來執行指令碼**：若啟用此選項，指令碼會在使用登入使用者認證的用戶端電腦上執行。  

> [!Note]  
> 從 1810 版開始，當使用 Windows PowerShell 作為探索指令碼或時補救指令碼，Configuration Manager 用戶端會使用 `-NoProfile` 參數來呼叫 PowerShell。 此選項會啟動 PowerShell，但不含設定檔。 PowerShell 設定檔是在 PowerShell 啟動時執行的指令碼。 <!--3607762-->  


### <a name="sql-query"></a><a name="bkmk_sql"></a> SQL 查詢

- **SQL Server 執行個體**：選擇要在預設執行個體、所有執行個體還是指定的資料庫執行個體名稱上執行 SQL 查詢。  

    > [!NOTE]  
    > 執行個體名稱必須參考 SQL Server 的本機執行個體。 若要參考叢集 SQL Server 執行個體，您應使用指令碼設定。  

- **資料庫**：指定要執行 SQL 查詢的 Microsoft SQL Server 資料庫名稱。  

- **資料行**：指定用來評估全域條件的合規性的 Transact-SQL 陳述式所傳回的資料行名稱。  

- **Transact-SQL 陳述式**：指定您想要使用全域條件的完整 SQL 查詢。 若要使用現有的 SQL 查詢，請選取 [開啟]  。  

    > [!IMPORTANT]  
    > SQL 查詢設定並不支援任何修改資料庫的 SQL 命令。 您只能使用 SQL 命令從資料庫讀取資訊。  


### <a name="wql-query"></a><a name="bkmk_wql"></a> WQL 查詢

- **命名空間**：指定用於評定用戶端電腦相容性的 WMI 命名空間。 預設值為 `root\cimv2`。  

- **類別**：在上述命名空間中指定目標 WMI 類別。  

- **屬性**：在上述類別中指定目標 WMI 屬性。  

- **WQL 查詢 WHERE 子句**：指定符合條件的子句以限縮結果。 例如，若只要查詢 Win32_Service 類別中的 DHCP 服務，則 WHERE 子句可為 `Name = 'DHCP' and StartMode = 'Auto'`。   


### <a name="xpath-query"></a><a name="bkmk_xpath"></a> XPath 查詢

- **路徑**：指定用於評估合規性之 .xml 檔案在用戶端電腦上的路徑。 Configuration Manager 支援在路徑名稱中使用所有 Windows 系統環境變數和 `%USERPROFILE%` 使用者變數。  

- **XML 檔案名稱**：在上述路徑中指定包含 XML 查詢的檔案名稱。  

- **包含子資料夾**：啟用此選項以搜尋指定路徑下的任何子資料夾。  

- **此檔案與 64 位元應用程式建立關聯**：在執行 Windows 64 位元版本的 Configuration Manager 用戶端上除了搜尋 32 位元系統檔案位置 `%Windir%\Syswow64` 以外，也一併搜尋 64 位元系統檔案位置 `%Windir%\System32`。  

- **XPath 查詢**：指定有效的完整 XML 路徑語言 (XPath) 查詢。  

- **命名空間**：識別要在 XPath 查詢期間使用的命名空間與首碼。  

如果您嘗試探索加密的 .xml 檔案，合規性設定會找到該檔案，但 XPath 查詢不會產生任何結果。 則 Configuration Manager 用戶端不會產生任何錯誤。  

如果 XPath 查詢無效，此設定會在用戶端電腦上評估為不符合規範。  



##  <a name="configure-compliance-rules"></a>設定相容性規則  

合規性規則指定定義設定項目的合規性的條件。 設定至少必須有一項相容性規則，才能評估其相容性。 WMI、 登錄和指令碼設定可讓您修復不符合找到的值。 您可以建立新的規則或瀏覽至任何組態項目中選取規則中現有的設定。  


### <a name="to-create-a-compliance-rule"></a>若要建立合規性規則  

1. 在 [建立設定項目精靈]  的 [合規性規則]  頁面上，選取 [新增]  。  

2. 在 [建立規則]  對話方塊中，提供下列資訊：  

    - **名稱**：輸入合規性規則的名稱。  

    - **描述**：輸入合規性規則的描述。  

    - **選取的設定**︰選取 [瀏覽]  以開啟 [選取設定]  對話方塊。 選取您要定義規則的設定，或選取 [新增設定]  。 完成之後，選擇 [選取]  。  

        > [!Tip]  
        > 若要檢視目前所選設定的相關資訊，請選取 [屬性]  。  

    - **規則類型**：選取您要使用的合規性規則類型：  

        - **值**：建立規則來比較設定項目所傳回值與您所指定的值。 如需其他設定的詳細資訊，請參閱[值規則](#bkmk_value)。  

        - **存在**：建立規則，以根據設定是否存在於用戶端裝置上，或根據找到設定的次數，來評估設定。 如需其他設定的詳細資訊，請參閱[存在規則](#bkmk_exist)。  

3. 選取 [確定]  以關閉 [建立規則]  對話方塊。  




### <a name="value-rules"></a><a name="bkmk_value"></a> 值規則  

- **屬性**：要檢查的物件屬性會依據所選取設定而有所不同， 可用屬性亦會依據設定的類型而有所不同。 

- **設定必須符合下列項目...** ：可用規則或權限會依據設定的類型而有所不同。

- **支援時補救不符合規範的規則**：如果您要讓 Configuration Manager 自動補救不符合規範的規則，請選取此選項。 Configuration Manager 會使用下列規則類型來支援此動作：  

    - **登錄值**：如果登錄值不符合規範，則用戶端會設定登錄值。 如果登錄值不存在，則用戶端會建立該值。  

    - **指令碼**：用戶端會使用您透過設定所指定的補救指令碼。  

    - **WQL 查詢**  

    > [!IMPORTANT]  
    > 只有在規則運算子設定為 [等於]  時，才能補救不相容的規則。  

- **如果找不到此設定執行個體，即回報不符合規範**：如果在用戶端電腦上找不到這項設定，請啟用此選項，讓設定項目回報不相容。  

- **報告的不符合規範嚴重性**：指定不符合此合規性規則時，要在 Configuration Manager 報告中回報的嚴重性等級。 可用的嚴重性等級如下：  
    - **無**  
    - **資訊**  
    - **警告**  
    - **重大**  
    - **重大事件**：不符合此相容性規則的電腦會回報 [重大]  失敗嚴重性。 此嚴重性層級也會在應用程式事件記錄檔中記錄為 Windows 事件。  


### <a name="existential-rules"></a><a name="bkmk_exist"></a> 存在規則 

> [!NOTE]  
> 所顯示的選項可能會根據您要設定的規則設定類型而有所不同。  

- **設定必須存在於用戶端裝置上**  

- **此設定必須存在於用戶端裝置**  

- **此設定就會發生下列次數:**  

- **報告的不符合規範嚴重性**：指定不符合此合規性規則時，要在 Configuration Manager 報告中回報的嚴重性等級。 可用的嚴重性等級如下：  
    - **無**  
    - **資訊**  
    - **警告**  
    - **重大**  
    - **重大事件**：不符合此相容性規則的電腦會回報 [重大]  失敗嚴重性。 此嚴重性層級也會在應用程式事件記錄檔中記錄為 Windows 事件。  


## <a name="track-configuration-item-remediations"></a><a name="bkmk_track"></a> 追蹤設定項目補救
<!--4261411-->
*(於 2002 版引進)*

從 Configuration Manager 2002 版開始，您可根據設定項目合規性規則，**在支援時追蹤補救歷程**。 啟用此選項時，任何針對設定項目在用戶端上所執行的補救都會產生狀態訊息。 該歷程會儲存於 Configuration Manager 資料庫中。

使用公用檢視 **v_CIRemediationHistory** 來建置自訂報告，以檢視補救歷程。 `RemediationDate` 資料行是用戶端執行補救的時間 (UTC)。 `ResourceID` 可識別裝置。 使用 **v_CIRemediationHistory** 檢視來建置自訂報告，以協助：

- 使用補救指令碼識別可能發生的問題
- 在補救中尋找趨勢，例如，在每個評估週期中始終都不符合規範的用戶端。

### <a name="enable-the-track-remediation-history-when-supported-option"></a>啟用 [Track remediation history when supported] \(在支援時追蹤補救歷程\) 選項

- 針對新的設定項目，當在精靈的 [設定]  頁面上建立新設定時，請於 [合規性規則]  索引標籤中，新增 [Track remediation history when supported] \(在支援時追蹤補救歷程\)  選項。
- 針對現有的設定項目，請於設定項目 [屬性]  中的 [合規性規則]  索引標籤上，新增 [Track remediation history when supported] \(在支援時追蹤補救歷程\)  選項。
[ ![2002 版的 [在支援時追蹤補救歷程]](./media/4261411-remediation-history.png)](./media/4261411-remediation-history.png#lightbox)

## <a name="next-steps"></a>後續步驟

[建立設定基準](create-configuration-baselines.md)
