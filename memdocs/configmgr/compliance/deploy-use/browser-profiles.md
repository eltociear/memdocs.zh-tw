---
title: 設定 Microsoft Edge 設定
titleSuffix: Configuration Manager
description: 在 Windows 10 用戶端上設定 Microsoft Edge 網頁瀏覽器的設定
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 07/30/2018
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-compliance
ms.assetid: 76477b4d-df41-4b25-8318-7d18d46ca2c6
ms.openlocfilehash: 4ed49ed3623b34bfb51fd66fafa858ae3951a5af
ms.sourcegitcommit: 214fb11771b61008271c6f21e17ef4d45353788f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/07/2020
ms.locfileid: "82906350"
---
# <a name="configure-microsoft-edge-settings-in-configuration-manager"></a>在 Configuration Manager 中設定 Microsoft Edge 設定

適用於：  Configuration Manager (最新分支)

<!-- 1357310 -->
從 1802 版開始，針對在 Windows 10 用戶端上使用 [Microsoft Edge](https://www.microsoft.com/itpro/microsoft-edge) 網頁瀏覽器的客戶，會建立 Configuration Manager 合規性設定原則來設定數個 Microsoft Edge 設定。 

此原則僅適用於 Windows 10 (1703 版或更新版本) 上的用戶端。 <!--511552-->


## <a name="policy-settings"></a>原則設定
此原則目前包含下列設定：
- **將 Microsoft Edge 瀏覽器設為預設值**：將適用於網頁瀏覽器的 Windows 10 預設應用程式設定設為 Microsoft Edge
- **允許網址列下拉式清單**：需要 Windows 10 (1703 版或更新版本)。 如需詳細資訊，請參閱 [AllowAddressBarDropdown 瀏覽器原則](/windows/client-management/mdm/policy-csp-browser#browser-allowaddressbardropdown)。
- **允許同步 Microsoft 瀏覽器之間的我的最愛**：需要 Windows 10 (1703 版或更新版本)。 如需詳細資訊，請參閱 [SyncFavoritesBetweenIEAndMicrosoftEdge 瀏覽器原則](/windows/client-management/mdm/policy-csp-browser#browser-syncfavoritesbetweenieandmicrosoftedge)。
- **允許在結束時清除瀏覽資料**：需要 Windows 10 (1703 版或更新版本)。 如需詳細資訊，請參閱 [ClearBrowsingDataOnExit 瀏覽器原則](/windows/client-management/mdm/policy-csp-browser#browser-clearbrowsingdataonexit)。
- **允許「不要追蹤」標頭**：如需詳細資訊，請參閱 [AllowDoNotTrack 瀏覽器原則](/windows/client-management/mdm/policy-csp-browser#browser-allowdonottrack)。
- **允許自動填入**：如需詳細資訊，請參閱 [AllowAutofill 瀏覽器原則](/windows/client-management/mdm/policy-csp-browser#browser-allowautofill)。
- **允許 Cookie**：如需詳細資訊，請參閱 [AllowCookies 瀏覽器原則](/windows/client-management/mdm/policy-csp-browser#browser-allowcookies)。
- **允許快顯封鎖程式**：如需詳細資訊，請參閱 [AllowPopups 瀏覽器原則](/windows/client-management/mdm/policy-csp-browser#browser-allowpopups)。
- **允許網址列的搜尋建議**：如需詳細資訊，請參閱 [AllowSearchSuggestionsinAddressBar 瀏覽器原則](/windows/client-management/mdm/policy-csp-browser#browser-allowsearchsuggestionsinaddressbar)。
- **允許將內部網路流量傳送到 Internet Explorer**：如需詳細資訊，請參閱 [SendIntranetTraffictoInternetExplorer 瀏覽器原則](/windows/client-management/mdm/policy-csp-browser#browser-sendintranettraffictointernetexplorer)。
- **允許密碼管理員**：如需詳細資訊，請參閱 [AllowPasswordManager 瀏覽器原則](/windows/client-management/mdm/policy-csp-browser#browser-allowpasswordmanager)。
- **允許開發人員工具**：如需詳細資訊，請參閱 [AllowDeveloperTools 瀏覽器原則](/windows/client-management/mdm/policy-csp-browser#browser-allowdevelopertools)。
- **允許延伸模組**：如需詳細資訊，請參閱 [AllowExtensions 瀏覽器原則](/windows/client-management/mdm/policy-csp-browser#browser-allowextensions)。


### <a name="configure-windows-defender-smartscreen-settings-for-microsoft-edge"></a>設定 Microsoft Edge 的 Windows Defender SmartScreen 設定
<!--1353701-->
從 1806 版開始，此原則會新增三項 [Windows Defender SmartScreen](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-smartscreen/microsoft-defender-smartscreen-overview) 設定。 此原則目前在 [SmartScreen 設定]  頁面中包含下列額外設定：

- **允許 SmartScreen**：指定是否允許 Windows Defender SmartScreen。 如需詳細資訊，請參閱 [AllowSmartScreen 瀏覽器原則](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-allowsmartscreen)。
- **使用者可以覆寫站台的 SmartScreen 提示**：指定使用者是否可覆寫 Windows Defender SmartScreen 篩選工具有關潛在惡意網站的警告。 如需詳細資訊，請參閱 [PreventSmartScreenPromptOverride 瀏覽器原則](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-preventsmartscreenpromptoverride)。
- **使用者可以覆寫檔案的 SmartScreen 提示**：指定使用者是否可覆寫 Windows Defender SmartScreen 篩選工具有關下載未驗證檔案的警告。 如需詳細資訊，請參閱 [PreventSmartScreenPromptOverrideForFiles 瀏覽器原則](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-preventsmartscreenpromptoverrideforfiles)。



## <a name="create-the-microsoft-edge-browser-profile"></a>建立 Microsoft Edge 瀏覽器設定檔

1. 在 Configuration Manager 主控台中，移至 [資產與合規性]  工作區。 展開 [合規性設定]  ，然後選取 [Microsoft Edge 瀏覽器設定檔]  節點。 按一下功能區選項以**建立 Microsoft Edge 設定檔**。
2. 指定原則的**名稱**、選擇性地輸入**描述**，然後按一下 [下一步]  。
3. 在 [一般設定]  頁面上，針對要包含在此原則中的設定來將值變更為 [已設定]  ，然後按一下 [下一步]  。 您必須設定 [將 Edge 瀏覽器設為預設]  設定，才能繼續。
4. 在 1806 版和更新版本中，設定 [SmartScreen 設定]  頁面上的設定，然後按一下 [下一步]  。 
5. 在 [支援的平台]  頁面上，選取要套用此原則的 OS 版本和架構，然後按一下 [下一步]  。 
6. 完成精靈。



## <a name="deploy-the-policy"></a>部署原則

1. 選取您的原則，然後按一下功能區選項以**部署**。
2. 按一下 [瀏覽]  ，以選取要部署原則的使用者或裝置集合。 
3. 視需要選取其他選項。  
     a. 當原則不符合規範時產生警示。  
     b. 設定用戶端使用此原則來評估裝置合規性的排程。 
4. 按一下 [確定]  以建立部署。



## <a name="next-steps"></a>後續步驟

就像任何合規性設定原則，用戶端會按照您指定的排程來修復設定。 在 Configuration Manager 主控台中[監視和報告裝置合規性](monitor-compliance-settings.md)。
