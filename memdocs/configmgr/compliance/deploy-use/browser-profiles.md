---
title: 設定 Microsoft Edge 設定
titleSuffix: Configuration Manager
description: 在 Windows 10 用戶端上設定 Microsoft Edge 舊版網頁瀏覽器的設定
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 06/02/2020
ms.topic: how-to
ms.prod: configuration-manager
ms.technology: configmgr-compliance
ms.assetid: 76477b4d-df41-4b25-8318-7d18d46ca2c6
ms.openlocfilehash: 898d5240046655ca3d13037f74c92e730ab1993e
ms.sourcegitcommit: 7f542c97ac55bbd329f5befda97d671213c24e9a
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/08/2020
ms.locfileid: "84506130"
---
# <a name="configure-microsoft-edge-legacy-settings-in-configuration-manager"></a>在 Configuration Manager 中設定 Microsoft Edge 舊版設定

> [!IMPORTANT]
> 如果您是使用 Microsoft Edge 77 版或更新版本，並正在嘗試開啟 [設定] 窗格，請在瀏覽器網址列中輸入 `edge://settings/profiles`，而非搜尋其位置。 如需詳細資訊，請參閱[認識 Microsoft Edge](https://support.microsoft.com/help/17171/microsoft-edge-get-to-know)。
>
> 此文章適用於使用 Microsoft Endpoint Configuration Manager 管理 Microsoft Edge 舊版設定的 IT 專業人員。

適用於：Configuration Manager (最新分支)

<!-- 1357310 -->
針對在 Windows 10 用戶端上使用 [Microsoft Edge 舊版](https://docs.microsoft.com/microsoft-edge/deploy/) \(部分機器翻譯\) 網頁瀏覽器的客戶，請建立 Configuration Manager 合規性政策來設定瀏覽器設定。

此原則僅適用於使用 Windows 10 1703 版或更新版本，以及 Microsoft Edge 舊版 45 版或更舊版本的用戶端。 <!--511552-->

如需使用 Configuration Manager 管理 Microsoft Edge 77 版或更新版本的詳細資訊，請參閱[部署和更新 Microsoft Edge 77 版與更新版本](../../apps/deploy-use/deploy-edge.md)。 如需針對 Microsoft Edge 77 版或更新版本設定原則的詳細資訊，請參閱 [Microsoft Edge - 原則](https://docs.microsoft.com/DeployEdge/microsoft-edge-policies) \(部分機器翻譯\)。

## <a name="policy-settings"></a>原則設定

此原則目前包含下列設定：

- **將 Microsoft Edge 瀏覽器設為預設值**：將適用於網頁瀏覽器的 Windows 10 預設應用程式設定設為 Microsoft Edge

- **允許網址列下拉式清單**：需要 Windows 10 (1703 版或更新版本)。 如需詳細資訊，請參閱 [AllowAddressBarDropdown 瀏覽器原則](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-allowaddressbardropdown)。

- **允許同步 Microsoft 瀏覽器之間的我的最愛**：需要 Windows 10 (1703 版或更新版本)。 如需詳細資訊，請參閱 [SyncFavoritesBetweenIEAndMicrosoftEdge 瀏覽器原則](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-syncfavoritesbetweenieandmicrosoftedge)。

- **允許在結束時清除瀏覽資料**：需要 Windows 10 (1703 版或更新版本)。 如需詳細資訊，請參閱 [ClearBrowsingDataOnExit 瀏覽器原則](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-clearbrowsingdataonexit)。

- **允許「不要追蹤」標頭**：如需詳細資訊，請參閱 [AllowDoNotTrack 瀏覽器原則](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-allowdonottrack)。

- **允許自動填入**：如需詳細資訊，請參閱 [AllowAutofill 瀏覽器原則](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-allowautofill)。

- **允許 Cookie**：如需詳細資訊，請參閱 [AllowCookies 瀏覽器原則](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-allowcookies)。

- **允許快顯封鎖程式**：如需詳細資訊，請參閱 [AllowPopups 瀏覽器原則](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-allowpopups)。

- **允許網址列的搜尋建議**：如需詳細資訊，請參閱 [AllowSearchSuggestionsinAddressBar 瀏覽器原則](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-allowsearchsuggestionsinaddressbar)。

- **允許將內部網路流量傳送到 Internet Explorer**：如需詳細資訊，請參閱 [SendIntranetTraffictoInternetExplorer 瀏覽器原則](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-sendintranettraffictointernetexplorer)。

- **允許密碼管理員**：如需詳細資訊，請參閱 [AllowPasswordManager 瀏覽器原則](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-allowpasswordmanager)。

- **允許開發人員工具**：如需詳細資訊，請參閱 [AllowDeveloperTools 瀏覽器原則](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-allowdevelopertools)。

- **允許延伸模組**：如需詳細資訊，請參閱 [AllowExtensions 瀏覽器原則](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-allowextensions)。

> [!TIP]
> 如需使用群組原則來設定上述及其他設定的詳細資訊，請參閱 [Microsoft Edge 舊版群組原則](https://docs.microsoft.com/microsoft-edge/deploy/group-policies/) \(部分機器翻譯\)。

### <a name="configure-windows-defender-smartscreen-settings-for-microsoft-edge-legacy"></a>設定 Microsoft Edge 舊版的 Windows Defender SmartScreen 設定
<!--1353701-->
此原則會新增三個 [Windows Defender SmartScreen](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-smartscreen/microsoft-defender-smartscreen-overview) \(部分機器翻譯\) 設定。 此原則目前在 [SmartScreen 設定] 頁面中包含下列額外設定：

- **允許 SmartScreen**：指定是否允許 Windows Defender SmartScreen。 如需詳細資訊，請參閱 [AllowSmartScreen 瀏覽器原則](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-allowsmartscreen)。

- **使用者可以覆寫站台的 SmartScreen 提示**：指定使用者是否可覆寫 Windows Defender SmartScreen 篩選工具有關潛在惡意網站的警告。 如需詳細資訊，請參閱 [PreventSmartScreenPromptOverride 瀏覽器原則](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-preventsmartscreenpromptoverride)。

- **使用者可以覆寫檔案的 SmartScreen 提示**：指定使用者是否可覆寫 Windows Defender SmartScreen 篩選工具有關下載未驗證檔案的警告。 如需詳細資訊，請參閱 [PreventSmartScreenPromptOverrideForFiles 瀏覽器原則](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-preventsmartscreenpromptoverrideforfiles)。

## <a name="create-the-browser-profile"></a>建立瀏覽器設定檔

1. 在 Configuration Manager 主控台中，移至 [資產與合規性] 工作區。 展開 [合規性設定]，然後選取 [Microsoft Edge 瀏覽器設定檔] 節點。 在功能區中，選取 [建立 Microsoft Edge 設定檔]。

2. 指定原則的 [名稱]，選擇性地輸入 [描述]，然後選取 [下一步]。

3. 在 [一般設定] 頁面上，針對要包含在此原則中的設定，將值變更為 [已設定]。 若要繼續執行精靈，請務必將設定設為 [將 Edge 瀏覽器設為預設]。

4. 設定 [SmartScreen 設定] 頁面上的設定。

5. 在 [支援的平台] 頁面上，選取要套用此原則的 OS 版本和架構。

6. 完成精靈。

## <a name="deploy-the-policy"></a>部署原則

1. 選取您的原則，然後在功能區中選取 [部署]。

2. [瀏覽] 以選取要部署原則的使用者或裝置集合。

3. 視需要選取其他選項：

    1. 當原則不符合規範時產生警示。

    2. 設定用戶端使用此原則來評估裝置合規性的排程。

4. 選取 [確定] 以建立部署。

## <a name="next-steps"></a>後續步驟

就像任何合規性設定原則，用戶端會按照您指定的排程來修復設定。 在 Configuration Manager 主控台中[監視和報告裝置合規性](monitor-compliance-settings.md)。
