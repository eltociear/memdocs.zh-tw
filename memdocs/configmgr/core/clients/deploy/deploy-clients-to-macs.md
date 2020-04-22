---
title: 部署 Mac 用戶端
titleSuffix: Configuration Manager
description: 了解如何在 Configuration Manager 中將用戶端部署至 Mac 電腦。
ms.date: 12/10/2018
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: e46ad501-5d73-44ac-92de-0de14ef72b83
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 8993f4c05b7156f3aecf6fcc9c8ea3790e49e98d
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81694026"
---
# <a name="how-to-deploy-clients-to-macs"></a>如何將用戶端部署至 Mac

適用於：  Configuration Manager (最新分支)

本文描述如何在 Mac 電腦上部署和維護 Configuration Manager 用戶端。 若要了解您必須先進行何種設定，再將用戶端部署到 Mac 電腦，請參閱[準備將用戶端軟體部署到 Mac](prepare-to-deploy-mac-clients.md)。

為 Mac 電腦安裝新的用戶端時，您可能必須同時安裝 Configuration Manager 更新，以反映 Configuration Manager 主控台中的新用戶端資訊。

在這些程序中，您有兩個選項可以安裝用戶端憑證。 在[準備將用戶端軟體部署到 Mac](prepare-to-deploy-mac-clients.md#certificate-requirements) 中，深入了解 Mac 的用戶端憑證。  

- 利用 [CMEnroll 工具](#bkmk_enroll)使用 Configuration Manager 註冊。 註冊程序不支援自動憑證更新。 請在已安裝的憑證到期之前重新註冊 Mac 電腦。    

- [使用與 Configuration Manager 無關的憑證要求和安裝方法](#bkmk_external)。  

> [!IMPORTANT]  
> 若要將用戶端部署到執行 macOS Sierra 的裝置上，請正確設定管理點憑證的**主體名稱**。 例如，使用管理點伺服器的 FQDN。



## <a name="configure-client-settings"></a>設定用戶端設定  

使用[預設用戶端設定](about-client-settings.md)來設定 Mac 電腦的註冊。 您無法使用自訂用戶端設定。 若要要求及安裝憑證，Configuration Manager Mac 用戶端需要使用預設用戶端設定。  

1. 在 Configuration Manager 主控台中，移至 [系統管理]  工作區。 選取 [用戶端設定]  節點，然後選取 [預設用戶端設定]  。  

2. 在功能區 [常用]  索引標籤的 [內容]  群組中，選擇 [內容]  。  

3. 選取 [註冊]  區段，然後進行下列設定：  

    1. **允許使用者註冊行動裝置和 Mac 電腦**：**是**  

    2. **註冊設定檔：** 按一下 [設定設定檔]  。  

4. 在 [行動裝置註冊設定檔]  對話方塊中，選擇 [建立]  。  

5. 在 [建立註冊設定檔]  對話方塊中，輸入此註冊設定檔的名稱。 然後設定 [管理站台碼]  。 選取包含用於這些 Mac 電腦管理點的 Configuration Manager 主要站台。  

    > [!NOTE]  
    >  如果您無法選取站台，請確認站台內至少有一個管理點設定為支援行動裝置。  

6. 選擇 [新增]  。  

7. 在 [新增行動裝置的憑證授權單位]  視窗中，選取負責簽發憑證給 Mac 電腦的憑證授權單位伺服器。  

8. 於 [建立註冊設定檔]  對話方塊中，選取您先前建立的 Mac 電腦憑證範本。  

9. 選取 [確定]  關閉 [註冊設定檔]  對話方塊，然後按一下 [預設用戶端設定]  對話方塊。  

    > [!TIP]  
    > 若要變更用戶端原則間隔，請使用 [用戶端原則]  用戶端設定群組中的 [用戶端原則輪詢間隔]  。  

裝置下一次下載用戶端原則時，Configuration Manager 會為所有使用者套用這些設定。 若要起始單一用戶端的原則抓取，請參閱[起始 Configuration Manager 用戶端的原則抓取](../manage/manage-clients.md#BKMK_PolicyRetrieval)。  

除了註冊用戶端設定之外，也請確認您已設定下列用戶端裝置設定︰  

- **硬體清查**：啟用並設定此功能，從 Mac 和 Windows 用戶端電腦收集硬體清查。 如需詳細資訊，請參閱[如何擴充硬體清查](../manage/inventory/extend-hardware-inventory.md)。  

- **合規性設定**：啟用並設定此功能，以在 Mac 和 Windows 用戶端電腦上評估和補救設定。 如需詳細資訊，請參閱[規劃和設定合規性設定](../../../compliance/plan-design/plan-for-and-configure-compliance-settings.md)。  

如需詳細資訊，請參閱[如何設定用戶端設定](configure-client-settings.md)。  



## <a name="download-the-client-for-macos"></a><a name="bkmk_download"></a> 下載適用於 macOS 的用戶端

1. 下載 macOS 用戶端檔案套件：[Microsoft Endpoint Configuration Manager - macOS 用戶端 (64 位元)](https://www.microsoft.com/download/details.aspx?id=100850) \(英文\)。 將 **ConfigmgrMacClient.msi** 儲存至執行 Windows 的電腦。 Configuration Manager 安裝媒體並未提供這個檔案。  

2. 在 Windows 電腦上執行安裝程式。 將 Mac 用戶端套件 **Macclient.dmg** 解壓縮至本機磁碟上的資料夾。 預設路徑為 `C:\Program Files\Microsoft\System Center Configuration Manager for Mac client`。  

3. 將 **Macclient.dmg** 檔案複製到 Mac 電腦上的資料夾。  

4. 在 Mac 電腦上執行 **Macclient.dmg**，將檔案解壓縮至本機磁碟機的資料夾。  

5. 在資料夾中，確認其包含下列檔案： 

    - **Ccmsetup**：使用 **CMClient.pkg** 在您的 Mac 電腦上安裝 Configuration Manager 用戶端  

    - **CMDiagnostics**：在 Mac 電腦上收集與 Configuration Manager 用戶端相關的診斷資訊  

    - **CMUninstall**：從 Mac 電腦解除安裝用戶端  

    - **CMAppUtil**：將 Apple 應用程式套件轉換成可部署為 Configuration Manager 應用程式的格式  

    - **CMEnroll**：要求並安裝 Mac 電腦的用戶端憑證，以便您安裝 Configuration Manager 用戶端  



## <a name="enroll-the-mac-client"></a><a name="bkmk_enroll"></a> 註冊 Mac 用戶端  

使用 [Mac 電腦註冊精靈](#enroll-the-client-with-the-mac-computer-enrollment-wizard) 註冊個別用戶端。

若要將多個用戶端的註冊自動化，請使用 [CMEnroll 工具](#client-and-certificate-automation-with-cmenroll)。   


### <a name="enroll-the-client-with-the-mac-computer-enrollment-wizard"></a>使用 [Mac 電腦註冊精靈] 註冊用戶端  

1. 安裝用戶端後，[電腦註冊精靈] 隨即開啟。 若要以手動方式啟動精靈，請從 [Configuration Manager]  喜好設定頁面選取 [註冊]  。  

2. 在精靈的第二個頁面上，提供下列資訊︰  

   - **使用者名稱**：使用者名稱的格式可以如下︰  

     - `domain\name`。 例如：`contoso\mnorth`  

     - `user@domain`。 例如：`mnorth@contoso.com`  

         > [!IMPORTANT]  
         >  當您使用電子郵件地址填入 [使用者名稱]  欄位時，Configuration Manager 會自動填入 [伺服器名稱]  欄位。 會使用註冊 Proxy 點伺服器的預設名稱，以及電子郵件地址的網域名稱。 如果這些名稱不符合註冊 Proxy 點伺服器的名稱，請在註冊期間修正 [伺服器名稱]  。  

       使用者名稱和對應密碼必須符合 Active Directory 使用者帳戶，並具有 Mac 用戶端憑證範本的**讀取**和**註冊**權限。  

   - **伺服器名稱**：註冊 Proxy 點伺服器的名稱。  


### <a name="client-and-certificate-automation-with-cmenroll"></a>使用 CMEnroll 的用戶端和憑證自動化  

使用此程序來自動化用戶端安裝，以及使用 CMEnroll 工具來要求和註冊用戶端憑證。 若要執行此工具，您必須擁有 Active Directory 使用者帳戶。

1. 在 Mac 電腦上，巡覽至 **Macclient.dmg** 檔案內容解壓縮所在的資料夾。  

2. 輸入下列命令：`sudo ./ccmsetup`  

3. 請等候直至您看見 [已完成安裝]  訊息。 雖然安裝程式會顯示必須立即重新啟動的訊息，但請不要重新啟動，並繼續下一個步驟。  

4. 在 Mac 電腦的**工具**資料夾中鍵入下列命令︰`sudo ./CMEnroll -s <enrollment_proxy_server_name> -ignorecertchainvalidation -u '<user_name>'`  

    用戶端安裝之後，Mac [電腦註冊精靈] 便會開啟以協助您註冊 Mac 電腦。 如需詳細資訊，請參閱[使用 Mac 電腦註冊精靈註冊用戶端](#bkmk_enroll)。  

     範例：如果註冊 Proxy 點伺服器命名為 **server02.contoso.com**，且 **contoso\mnorth** 已取得 Mac 用戶端憑證範本的權限，請鍵入下列命令︰`sudo ./CMEnroll -s server02.contoso.com -ignorecertchainvalidation -u 'contoso\mnorth'`  

    > [!NOTE]  
    > 如果使用者名稱包含任何下列字元，註冊便會失敗：`<>"+=,`。 請使用不包含這些字元的使用者名稱來使用頻外憑證。  
    >  
    > 為了提供更順暢的使用者體驗，請編寫安裝步驟。 如此一來，使用者只需要提供其使用者名稱和密碼。  

5. 輸入 Active Directory 使用者帳戶的密碼。 當您輸入此命令時，會提示輸入兩個密碼。 第一個密碼是針對執行命令的進階使用者帳戶。 第二個提示是針對 Active Directory 使用者帳戶。 提示外觀看似相同，所以請確認是否以正確順序輸入密碼。  

6. 請等候直至您看見 [已順利註冊]  訊息。  

7. 若要將註冊的憑證限制到 Configuration Manager，請在 Mac 電腦上開啟終端機視窗，並進行下列變更︰  

    1. 輸入命令 `sudo /Applications/Utilities/Keychain Access.app/Contents/MacOS/Keychain Access`  

    2. 在 [金鑰鏈存取]  視窗的 [金鑰鏈]  區段中，選擇 [系統]  。 然後在 [類別]  區段中選擇 [金鑰]  。  

    3. 展開金鑰以檢視用戶端憑證。 使用已安裝的私密金鑰來尋找憑證，並開啟金鑰。  

    4. 在 [存取控制]  索引標籤上，選擇 「Confirm before allowing access」 (允許存取前先確認)  。  

    5. 瀏覽至 **/Library/Application Support/Microsoft/CCM**，選取 [CCMClient]  ，然後選擇 [新增]  。  

    6. 選擇 [儲存變更]  並關閉 [金鑰鏈存取]  對話方塊。  

8. 重新啟動 Mac 電腦。  

若要驗證用戶端安裝是否已順利完成，請在 Mac 電腦的 [系統喜好設定]  開啟 [Configuration Manager]  項目。 也請在 Configuration Manager 主控台中更新並檢視 [所有系統]  集合。 請確認 Mac 電腦作為受控用戶端顯示在此集合中。  

> [!TIP]  
> 若要協助 Mac 用戶端進行疑難排解，請使用 Mac 用戶端套件所包含的 **CMDiagnostics** 工具。 您可以將其用於收集下列診斷資訊：  
>   
> - 執行中處理程序清單  
> - Mac OS X 作業系統版本  
> - 與 Configuration Manager 用戶端相關的 Mac OS X 當機報告 (其中包含 **CCM\*.crash** 和 **System Preference.crash**)。  
> - 由 Configuration Manager 用戶端安裝所建立的用料表 (BOM) 檔案和內容清單 (.plist) 檔案。  
> - 資料夾 **/Library/Application Support/Microsoft/CCM/Logs** 的內容。  
>   
> 系統會將 CmDiagnostics 收集的資訊新增至 ZIP 檔案，並儲存於電腦桌面上，且命名為 `cmdiag-<hostname>-<datetime>.zip`。



## <a name="manage-certificates-external-to-configuration-manager"></a><a name="bkmk_external"></a> 管理 Configuration Manager 外部的憑證

您可以使用獨立於 Configuration Manager 的憑證要求和安裝方法。 使用相同的一般程序，但包含下列額外步驟： 

- 安裝 Configuration Manager 用戶端時，請使用 **MP** 和 **SubjectName** 命令列選項。 輸入下列命令：`sudo ./ccmsetup -MP <management point internet FQDN> -SubjectName <certificate subject name>`。 憑證主體名稱區分大小寫，請依憑證詳細資料中所顯示正確鍵入。  

     範例：管理點的網際網路 FQDN 為 **server03.contoso.com**。 Mac 用戶端憑證具有 **mac12.contoso.com** 的 FQDN，作為憑證主體的一般名稱。 使用下列命令：`sudo ./ccmsetup -MP server03.contoso.com -SubjectName mac12.contoso.com`  

- 如果您有多個憑證含有相同的主體值，請指定要用於 Configuration Manager 用戶端的憑證序號。 使用下列命令：`sudo defaults write com.microsoft.ccmclient SerialNumber -data "<serial number>"`。  

     例如：`sudo defaults write com.microsoft.ccmclient SerialNumber -data "17D4391A00000003DB"`  



## <a name="renew-the-mac-client-certificate"></a>更新 Mac 用戶端憑證  

此程序會移除 SMSID。 Mac 的 Configuration Manager 用戶端需要新的識別碼，以使用新或更新的憑證。  

> [!IMPORTANT]  
> 取代用戶端 SMSID 後，從 Configuration Manager 主控台刪除較舊資源時，您也可以刪除任何已儲存的用戶端歷程記錄。 例如該用戶端的硬體清查歷程記錄。  


1. 針對必須更新電腦憑證的 Mac 電腦建立並填入一個裝置集合。  

2. 在 [資產與相容性]  工作區內，開啟 [建立設定項目精靈]  。  

3. 在精靈的 [一般]  頁面上，指定下列資訊︰  

    - **名稱**：**移除 Mac 的 SMSID**  

    - **類型**：**Mac OS X**  

4. 在 [支援的平台]  頁面上選取所有 Mac OS X 版本。  

5. 在 [設定]  頁面上選取 [新增]  。 在 [建立設定]  視窗中指定下列資訊：  

    - **名稱**：**移除 Mac 的 SMSID**  

    - **設定類型**︰**指令碼**  

    - **資料類型**：**字串**  

6. 在 [建立設定]  視窗中，針對 [探索指令碼]  選取 [新增指令碼]  。 此動作會指定指令碼，探索透過 SMSID 設定的 Mac 電腦。  

7. 在 [編輯探索指令碼]  視窗中，輸入下列殼層指令碼：  

    ``` Shell
    defaults read com.microsoft.ccmclient SMSID  
    ```  

8. 選擇 [確定]  以關閉 [編輯探索指令碼]  視窗。  

9. 在 [建立設定]  視窗中，針對 [補救指令碼 (選擇性)]  ，選擇 [新增指令碼]  。 此動作會指定指令碼，在 Mac 電腦上發現 SMSID 時將其移除。  

10. 在 [建立補救指令碼]  視窗中，輸入下列殼層指令碼：  

    ``` Shell
    defaults delete com.microsoft.ccmclient SMSID  
    ```  

11. 選擇 [確定]  以關閉 [建立補救指令碼]  視窗。  

12. 在 [合規性規則]  頁面上選擇 [新增]  。 然後，在 [建立原則]  視窗中指定下列資訊：  

    - **名稱**：**移除 Mac 的 SMSID**  

    - **選取的設定**︰按一下 [瀏覽]  ，然後選取您先前指定的探索指令碼。  

    - 在**下列值**欄位中： **(com.microsoft.ccmclient SMSID) 的網域/預設組不存在**。  

    - 啟用 [當此設定不符合規範時，執行指定的補救指令碼]  選項。  

13. 完成精靈。  

14. 建立包含此設定項目的設定基準。 將基準部署至目標集合。  

     如需詳細資訊，請參閱[如何建立設定基準](../../../compliance/deploy-use/create-configuration-baselines.md)。  

15. 在已移除 SMSID 的 Mac 電腦上安裝新憑證後，執行下列指令以設定用戶端使用新憑證：  

    ``` Shell
    sudo defaults write com.microsoft.ccmclient SubjectName -string <subject_name_of_new_certificate>  
    ```  



## <a name="see-also"></a>請參閱

[準備將用戶端部署到 Mac](prepare-to-deploy-mac-clients.md)

[維護 Mac 用戶端](../manage/maintain-mac-clients.md)
