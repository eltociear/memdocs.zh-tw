---
title: 擴充硬體清查
titleSuffix: Configuration Manager
description: 了解擴充 Configuration Manager 中硬體清查的方法。
ms.date: 03/22/2018
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: d5bfab4f-c55e-4545-877c-5c8db8bc1891
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 380ba550a6edb0f639644280df74c500663e19f4
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81695416"
---
# <a name="how-to-extend-hardware-inventory-in-configuration-manager"></a>如何擴充 Configuration Manager 中的硬體清查

適用於：  Configuration Manager (最新分支)

硬體清查會使用 Windows Management Instrumentation (WMI) 從 Windows 電腦讀取資訊。 WMI 是 Microsoft 的 Web 架構企業管理 (WBEM) 實作，而 WBEM 是一種用於存取企業中管理資訊的業界標準。 在舊版 Configuration Manager 中，您藉由修改站台伺服器上的檔案 sms_def.mof 來擴充硬體清查。 這個檔案包含一份可由硬體清查讀取的 WMI 類別清單。 編輯這個檔案，可以啟用和停用現有類別，也會建立新的類別來進行清查。  

Configuration.mof 檔案用來定義用戶端上要由硬體清查所清查的資料類別，而且從 Configuration Manager 2012 以來不曾變更過。 您可以建立資料類別來清查現有或自訂 WMI 儲存機制資料類別，或用戶端系統上的登錄機碼。  

 Configuration.mof 檔案也會定義並註冊存取硬體清查期間的裝置資訊的 WMI 提供者。 註冊提供者會定義要使用的提供者的類型和提供者支援的類別。  

 當設定管理員用戶端要求原則時，Configuration.mof 會附加至原則本文。 這個檔案是然後下載並編譯的用戶端。 當您新增、 修改或刪除 Configuration.mof 檔案中的資料類別時，用戶端會自動編譯存貨相關的資料類別不會對這些變更。 不需要採取進一步的動作，就可以清查 Configuration Manager 用戶端上的新增或修改過的資料類別。 此檔案位於主要站台伺服器上的  **<CM 安裝位置\>\Inboxes\clifiles.src\hinv\\** 中。  

 在 Configuration Manager 中，您無法再像 Configuration Manager 2007 中一樣編輯 sms_def.mof 檔案。 相反地，您可以啟用和停用 WMI 類別，以及使用用戶端設定來新增硬體清查所收集的新類別。 Configuration Manager 提供下列方法來擴充硬體清查。  

> [!NOTE]  
>  如果您已經手動變更 Configuration.mof 檔案來新增自訂清查類別，這些變更將會在您更新到 1602 版時遭到覆寫。 若要在更新之後繼續使用自訂類別，您必須在更新到 1602 版之後，將這些類別新增到 Configuration.mof 檔案的 "Added extensions" 區段。  
> 不過，您不能修改此區段以外的任何部分，因為這些區段是保留給 Configuration Manager 修改。 您可以在下列目錄中找到您自訂的 Configuration.mof 備份︰  
> **< CM 安裝目錄\>\data\hinvarchive\\** 。  

|方法|更多資訊|  
|------------|----------------------|  
|啟用或停用現有的庫存類別|啟用或停用預設清查類別，或建立自訂用戶端設定，讓您可從指定集合的用戶端收集不同的硬體清查類別。 請參閱本文中的[啟用或停用現有清查類別](#BKMK_Enable)程序。|  
|加入新的庫存類別|從另一部裝置的 WMI 命名空間新增清查類別。 請參閱本文中的[新增清查類別](#BKMK_Add)程序。|  
|匯入和匯出硬體清查類別|從 Configuration Manager 主控台匯入和匯出其中包含清查類別的管理物件格式 (MOF) 檔案。 請參閱本文中的[匯入硬體清查類別](#BKMK_Import)和[匯出硬體清查類別](#BKMK_Export)程序。|  
|建立 NOIDMIF 檔案|使用 NOIDMIF 檔案收集 Configuration Manager 無法清查的用戶端裝置相關資訊。 例如，您可能要收集裝置的資產數字資訊存在於只要在裝置上的標籤。 NOIDMIF 清查會自動關聯於它所收集從用戶端裝置。 請參閱本文中的[建立 NOIDMIF 檔案](#BKMK_NOIDMIF)。|  
|建立 IDMIF 檔案|您可使用 IDMIF 檔案，來收集組織中尚未與 Configuration Manager 用戶端建立關聯之資產的資訊，例如投影機、 影印機及網路印表機。 請參閱本文中的[建立 IDMIF 檔案](#BKMK_IDMIF)。|  

## <a name="procedures-to-extend-hardware-inventory"></a>擴充硬體清查的程序  
這些程序可協助您設定硬體清查的預設用戶端設定並套用至您的階層中的所有用戶端。 如果您只想要將這些設定套用至部分用戶端，請建立自訂用戶端裝置設定，並將它指派給特定用戶端集合。 請參閱[如何設定用戶端設定](../../../../core/clients/deploy/configure-client-settings.md)。  

###  <a name="to-enable-or-disable-existing-inventory-classes"></a><a name="BKMK_Enable"></a> 啟用或停用現有清查類別  

1.  在 Configuration Manager 主控台中，選擇 [系統管理]   > [用戶端設定]   > [預設用戶端設定]  。  

4.  在 [首頁]  索引標籤的 [內容]  群組中，選擇 [內容]  。  

5.  在 [預設用戶端設定]  對話方塊中，選擇 [硬體清查]  。  

6.  在 **裝置設定** 清單中，按一下 **設定類別**。  

7.  在 **硬體清查類別**  對話方塊中，選取或清除的類別和要收集的硬體清查類別屬性。 您可以展開以選取或清除該類別中的個別屬性的類別。 使用 **清查類別搜尋** 欄位搜尋個別類別。  

    > [!IMPORTANT]  
    >  將新的類別新增至 Configuration Manager 硬體清查時，收集並傳送到站台伺服器的清查檔案大小將會增加。 這可能會對網路和 Configuration Manager 站台的效能造成負面影響。 啟用只想要收集的清查類別。  


###  <a name="to-add-a-new-inventory-class"></a><a name="BKMK_Add"></a> 新增清查類別  

您只能修改預設的用戶端設定，從階層的最上層伺服器新增清查類別。 此選項無法使用。 當您建立自訂的裝置設定

1. 在 Configuration Manager 主控台中，選擇 [系統管理]   > [用戶端設定]   > [預設用戶端設定]  。  

2. 在 [首頁]  索引標籤的 [內容]  群組中，選擇 [內容]  。  

3. 在 [預設用戶端設定]  對話方塊中，選擇 [硬體清查]  。  

4. 在 [裝置設定]  清單中，選擇 [設定類別]  。  

5. 在 [硬體清查類別]  對話方塊中，選擇 [新增]  。  

6. 在 **加入硬體清查類別**  對話方塊中按一下 **連接**。  

7. 在 **連線到 Windows Management Instrumentation (WMI)**  對話方塊中，指定您將從中擷取 WMI 類別以及要用來擷取類別的 WMI 命名空間的電腦名稱。 如果您想要擷取您所指定的 WMI 命名空間底下的所有類別、 按一下 **遞迴**。 如果您要連接到電腦不是本機電腦，提供有權存取 WMI 遠端電腦上的帳戶登入認證。  

8. 選擇 [連線]  。  

9. 在 [新增硬體清查類別]  對話方塊的 [清查類別]  清單中，選取您想要新增至 Configuration Manager 硬體清查的 WMI 類別。  

10. 如果您想要編輯所選取 WMI 類別的相關資訊，請選擇 [編輯]  ，然後在 [類別限定詞]  對話方塊中提供下列資訊：  

    - **顯示名稱** - 此名稱將會顯示在資源總管中。  

    - **內容** – 指定將用來顯示 WMI 類別之每個內容的單位。  

      您也可以指定屬性做為索引鍵屬性來唯一識別每個類別的執行個體。 如果此類別定義任何索引鍵和多個執行個體的類別會報告從用戶端，只有最新發現的執行個體儲存在資料庫中。  

      完成內容的設定之後，請按一下 [確定]  關閉 [類別限定詞]  對話方塊和其他開啟的對話方塊。 

###  <a name="to-import-hardware-inventory-classes"></a><a name="BKMK_Import"></a> 匯入硬體清查類別  

當您修改預設的用戶端設定時您可以只匯入清查類別。 不過，您可以使用自訂用戶端設定匯入不包含結構描述變更的資訊，例如將現有類別的屬性從 **True** 變更為 **False**。  

1.  在 Configuration Manager 主控台中，選擇 [系統管理]   >  [用戶端設定]   > [預設用戶端設定]  。  

4.  在 [首頁]  索引標籤的 [內容]  群組中，選擇 [內容]  。  

5.  在 [預設用戶端設定]  對話方塊中，選擇 [硬體清查]  。  

6.  在 [裝置設定]  清單中，選擇 [設定類別]  。  

7.  在 [硬體清查類別]  對話方塊中，選擇 [匯入]  。  

8.  在 [匯入]  對話方塊中，選取您要匯入的管理物件格式 (MOF) 檔案，然後選擇 [確定]  。 檢閱將匯入的項目，然後按一下 [匯入]  。  

###  <a name="to-export-hardware-inventory-classes"></a><a name="BKMK_Export"></a> 匯出硬體清查類別  

1.  在 Configuration Manager 主控台中，選擇 [系統管理]   > [用戶端設定]   > [預設用戶端設定]  。  

4.  在 [首頁]  索引標籤的 [內容]  群組中，選擇 [內容]  。  

5.  在 [預設用戶端設定]  對話方塊中，選擇 [硬體清查]  。  

6.  在 [裝置設定]  清單中，選擇 [設定類別]  。  

7.  在 [硬體清查類別]  對話方塊中，選擇 [匯出]  。  

    > [!NOTE]  
    >  當您匯出類別時時就會匯出所有目前選取的類別。  

8.  在 [匯出]  對話方塊中，指定您要將類別匯出至其中的管理物件格式 (MOF) 檔案，然後選擇 [儲存]  。  

### <a name="configure-hardware-inventory-to-collect-strings-larger-than-255-characters"></a><a name="bkmk_GreaterThan255"></a> 將硬體清查設定成收集大於 255 個字元的字串
從 Configuration Manager 1802 版開始，您可以針對硬體清查屬性，將字串的長度指定為大於 255 個字元。 此變更只會套用到新加入的類別，以及不是索引鍵的硬體清查屬性。 <!-- 1357389 -->

1. 在 [系統管理]  工作區中，按一下 [用戶端設定]  反白顯示要編輯的用戶端裝置設定，按一下滑鼠右鍵後選取 [屬性]  。

2. 選取 [硬體清查]  ，然後選取 [設定類別]  和 [新增]  。

3. 按一下 [連線]  按鈕。

4. 填寫 [電腦名稱]  、[WMI 命名空間]  ，視需要選取 [遞迴]  。 提供連線所需的認證。 按一下 [連線]  以檢視命名空間類別。

5. 選取新的類別，然後按一下 [編輯]  。

6. 將屬於字串 (索引鍵除外) 之屬性的 [長度]  變更為大於 255。 按一下 [確定]  。 

7. 確定已針對 [新增硬體清查類別]  選取編輯的屬性，然後按一下 [確定]  。 


## <a name="how-to-use-management-information-files-mif-files-to-extend-hardware-inventory"></a>如何使用管理資訊檔案 (MIF 檔案) 來擴充硬體清查  
 使用管理資訊格式 (MIF) 檔案，來延伸透過 Configuration Manager 從用戶端收集到的硬體清查資訊。 硬體清查期間 MIF 檔案中儲存的資訊加入至用戶端清查報告，並儲存在網站資料庫，您可以在其中使用您使用預設用戶端清查資料的相同方式中的資料。 有兩種類型的 MIF 檔案：NOIDMIF 和 IDMIF。

> [!IMPORTANT]  
>  將資訊從 MIF 檔案新增至 Configuration Manager 資料庫之前，您必須建立或匯入其類別資訊。 如需詳細資訊，請參閱本文中的[新增清查類別](#BKMK_Add)和[匯入硬體清查類別](#BKMK_Import)小節。  

###  <a name="to-create-noidmif-files"></a><a name="BKMK_NOIDMIF"></a> 建立 NOIDMIF 檔案  
 NOIDMIF 檔案可以用來將資訊新增至 Configuration Manager 通常無法收集且與特定用戶端裝置相關聯的用戶端硬體清查。 例如，許多公司都會使用資產編號來標示組織中的每部電腦，然後手動將這些編號編成目錄。 當您建立 NOIDMIF 檔案時，這項資訊可以新增至 Configuration Manager 資料庫並用於查詢和報告。 如需建立 NOIDMIF 檔案的相關資訊，請參閱 Configuration Manager SDK 文件。  

> [!IMPORTANT]  
>  當您建立 NOIDMIF 檔案時，必須將其儲存為 ANSI 編碼格式。 Configuration Manager 無法讀取以 UTF-8 編碼格式儲存的 NOIDMIF 檔案。  

 建立 NOIDMIF 檔案之後，請將其儲存至每個用戶端上的 _%Windir%_ **\CCM\Inventory\Noidmifs** 資料夾。 在下次排程的硬體清查週期，Configuration Manager 會從這個資料夾中的 NODMIF 檔案收集資訊。  

###  <a name="to-create-idmif-files"></a><a name="BKMK_IDMIF"></a> 建立 IDMIF 檔案  
 IDMIF 檔案可以用來將資產相關資訊新增至 Configuration Manager 資料庫，而這些資產通常無法透過 Configuration Manager 進行清查而且與特定用戶端裝置不相關。 例如，您可以使用 IDMIFS 收集下列項目的相關資訊：投影機，DVD 播放機、影印機或沒有設定管理員用戶端的其他設備。 如需建立 IDMIF 檔案的相關資訊，請參閱 Configuration Manager SDK 文件。  

 建立 IDMIF 檔案之後，請將其儲存至用戶端電腦上的 _%Windir%_ **\CCM\Inventory\Idmifs** 資料夾。 在下次排程的硬體清查週期，Configuration Manager 會從這個檔案收集資訊。 您必須宣告新類別，藉由新增或匯入這些檔案中包含的資訊。  

> [!NOTE]
> MIF 檔案可能包含大量資料，而且收集這項資料可能會對站台效能造成負面影響。 只在需要時才啟用 MIF 收集，並在硬體清查設定中設定 [自訂 MIF 檔案大小上限 (KB)]  選項。 如需詳細資訊，請參閱[硬體清查簡介](introduction-to-hardware-inventory.md)。
