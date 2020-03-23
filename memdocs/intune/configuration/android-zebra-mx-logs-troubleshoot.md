---
title: 在 Microsoft Intune 中使用 Android Zebra 裝置上的 StageNow 記錄 - Azure | Microsoft Docs
description: 請參閱在 Android 裝置上使用 StageNow 搭配 Microsoft Intune 時的常見問題和解決方式。 同時也了解如何取得記錄，並查看如何讀取成功或錯誤記錄的範例。
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 03/26/2019
ms.topic: troubleshooting
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: ''
ms.technology: ''
ms.assetid: ''
ms.reviewer: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: d8c7c60b4d9d1831aaabb9886345865234ce6351
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/13/2020
ms.locfileid: "79364613"
---
# <a name="troubleshoot-and-see-potential-issues-on-android-zebra-devices-in-microsoft-intune"></a>在 Microsoft Intune 中查看 Android Zebra 裝置上的潛在問題並進行疑難排解



在 Microsoft Intune 中，您可以使用 [Zebra Mobility Extensions (MX) 來管理 Android Zebra 裝置](android-zebra-mx-overview.md)。 使用 Zebra 裝置時，您將在 StageNow 中建立設定檔以管理設定並上傳至 Intune。 Intune 會使用 StageNow 應用程式將設定套用於裝置上。 StageNow 應用程式也會在用來進行疑難排解的裝置上建立詳細記錄。

本功能適用於：

- Android

例如，您可以在 StageNow 中建立設定檔來設定裝置。 建立 StageNow 設定檔時，最後一個步驟會產生檔案，以供測試設定檔。 您將在裝置上搭配 StageNow 應用程式使用此檔案。

在另一個範例中，您將在 StageNow 中建立並測試設定檔。 在 Intune 中，您將新增 StageNow 設定檔並指派給 Zebra 裝置。 檢查指派設定檔的狀態時，設定檔會顯示概觀狀態。

在這兩個案例中，您都可以從 StageNow 記錄檔獲得更多詳細資料，該記錄檔會在每次套用 StageNow 設定檔時儲存在裝置上。

某些問題與 StageNow 設定檔的內容沒有關聯，且不會反映在記錄中。

本文說明如何讀取 StageNow 記錄，並列出可能不會反映在記錄中的 Zebra 裝置其他潛在問題。

[使用和管理含有 Zebra Mobility Extensions 的 Zebra 裝置](android-zebra-mx-overview.md)提供這項功能的詳細資訊。

## <a name="get-the-logs"></a>取得記錄

### <a name="use-the-stagenow-app-on-the-device"></a>在裝置上使用 StageNow 應用程式
當使用電腦上的 StageNow 來直接測試設定檔，而不是使用 [Intune 來部署設定檔](android-zebra-mx-overview.md#step-4-create-a-device-management-profile-in-stagenow)時，裝置上的 StageNow 應用程式會儲存測試記錄。 若要取得記錄檔，請在裝置上的 StageNow 應用程式中使用 [其他 (...)]  選項。

### <a name="get-logs-using-android-debug-bridge"></a>使用 Android Debug Bridge 取得記錄
若要在使用 Intune 部署設定檔後取得記錄，請將裝置連線至具有 [Android Debug Bridge (adb)](https://developer.android.com/studio/command-line/adb) (會開啟 Android 的網站) 的電腦。

記錄儲存在裝置上的 `/sdcard/Android/data/com.microsoft.windowsintune.companyportal/files`

### <a name="get-logs-from-email"></a>從電子郵件取得記錄
若要在使用 Intune 部署設定檔後取得記錄，終端使用者可以使用裝置上的電子郵件應用程式，以透過電子郵件傳送記錄給您。 在 Zebra 裝置上開啟公司入口網站應用程式，然後[傳送記錄](https://docs.microsoft.com/user-help/send-logs-to-your-it-admin-by-email-android)。 使用傳送記錄功能也會建立 PowerLift 事件識別碼，如果您要連絡 Microsoft 支援服務，就可以參考此識別碼。

## <a name="read-the-logs"></a>讀取記錄

查看記錄檔時若看到 `<characteristic-error>` 標籤，代表發生錯誤。 錯誤詳細資料會寫入 `<parm-error>` 標籤 > `desc` 屬性。

## <a name="error-types"></a>錯誤類型

Zebra 裝置包含不同的錯誤報告層級：

- 裝置不支援 CSP。 例如，裝置並非行動電話裝置，也沒有行動電話管理員。
- MX 或 OSX 版本不符。 每個 CSP 都已設定版本。 如需完整的支援矩陣，請參閱 [Zebra 的文件](http://techdocs.zebra.com/mx/) (會開啟 Zebra 的網站)。
- 裝置回報另一個問題或錯誤。

## <a name="examples"></a>範例

例如，假設您有下列輸入設定檔：

```xml
<wap-provisioningdoc>
    <characteristic type="Clock">
        <parm name="AutoTime" value="false"/>
        <parm name="TimeZone" value="GMT-5"/>
        <parm name="Date" value="2014-12-03"/>
        <parm name="Time" value="11:11:11"/>
    </characteristic>
</wap-provisioningdoc>
```

在記錄中，XML 與輸入相同。 此相符的輸出代表設定檔已成功套用至裝置，且未發生錯誤：

```xml
<wap-provisioningdoc>
    <characteristic type="Clock" version="6.0">
        <parm name="AutoTime" value="false"/>
        <parm name="TimeZone" value="GMT-5"/>
        <parm name="Date" value="2014-12-03"/>
        <parm name="Time" value="11:11:11"/>
    </characteristic>
</wap-provisioningdoc>
```

在另一個範例中，假設您有下列輸入：

```xml
<wap-provisioningdoc>
    <characteristic type="XmlMgr" version="4.2" >
        <parm name="ProcessingMode" value="1"/>
    </characteristic>
    <characteristic type="AppMgr" version="4.2" >
        <parm name="Action" value="Install"/>
        <parm name="APK" value="/sdcard/test.apk"/>
    </characteristic>
</wap-provisioningdoc>
```

記錄顯示錯誤，因為其包含 `<characteristic-error>` 標籤。 在此案例中，設定檔嘗試安裝的 Android 套件 (APK) 不存在於指定路徑中：

```xml
<wap-provisioningdoc>
    <characteristic type="XmlMgr" version="4.2">
        <parm name="ProcessingMode" value="1"/>
    </characteristic>
    <characteristic-error type="AppMgr" version="5.1" desc="missing">
        <parm-error name="Action" value="Install" desc="apk doesnot exist in the path"/>
        <parm name="APK" value="/sdcard/test.apk"/>
    </characteristic-error>
</wap-provisioningdoc>
```

## <a name="other-potential-issues-with-zebra-devices"></a>Zebra 裝置的其他潛在問題

本節列出以裝置管理員身分使用 Zebra 裝置時，可能會看到的其他潛在問題。 這些問題不會在 StageNow 記錄中回報。

### <a name="android-system-webview-is-out-of-date"></a>Android System WebView 已過期

較舊的裝置使用公司入口網站應用程式登入時，使用者可能會看到訊息指出 System WebView 元件已過期，並需要升級。 如果裝置已安裝 Google Play，請將其連線到網際網路，然後檢查是否有更新。 如果裝置未安裝 Google Play，請取得元件的更新版本並套用至裝置。 或更新至 Zebra 所發行的最新裝置 OS。

### <a name="management-actions-take-a-long-time"></a>管理動作耗費很長時間

如果無法使用 Google Play，則某些工作需要最多 8 小時才能完成。 [適用於 Android 的 Intune 公司入口網站應用程式限制](https://support.microsoft.com/help/3211588/limitations-of-intune-company-portal-app-for-android-in-china) (會開啟另一個 Microsoft 網站) 可能是對您有幫助的資源。

### <a name="device-spoofing-suspected-shows-in-intune"></a>Intune 中顯示「懷疑裝置存在詐騙」

此錯誤代表 Intune 懷疑非 Zebra 的 Android 裝置將其型號和製造商報告為 Zebra 裝置。

### <a name="company-portal-app-is-older-than-minimum-required-version"></a>公司入口網站應用程式比最小必要版本還舊

Intune 可能會更新公司入口網站應用程式的最小必要版本。 如果裝置未安裝 Google Play，則公司入口網站應用程式就不會自動更新。 如果最小必要版本比安裝的版本更新，則公司入口網站應用程式會停止運作。 使用 [Zebra 裝置上的側載](android-zebra-mx-overview.md#sideload-the-company-portal-app)，更新至最新的公司入口網站應用程式。

## <a name="next-steps"></a>後續步驟

[Zebra 討論區](https://developer.zebra.com/community/home/discussions) (會開啟 Zebra 的網站)

[在 Intune 中使用 Zebra 行動性延伸模組使用及管理 Zebra 裝置](android-zebra-mx-overview.md)
