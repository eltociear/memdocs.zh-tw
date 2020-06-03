---
title: 使用 Intune App Wrapping Tool 包裝 Android 應用程式
description: 了解如何包裝 Android 應用程式，而不需要變更應用程式本身的程式碼。 準備應用程式，以便您可以套用行動裝置應用程式管理原則。
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 05/27/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: developer
ms.localizationpriority: medium
ms.technology: ''
ms.assetid: e9c349c8-51ae-4d73-b74a-6173728a520b
ms.reviewer: aanavath
ms.suite: ems
search.appverid: MET150
ms.custom: intune-classic
ms.collection: M365-identity-device-management
ms.openlocfilehash: 69a694ab9da7987271214bc6919cd3b676f9814e
ms.sourcegitcommit: 118587ddb31ce26b27801839db9b3b59f1177f0f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/29/2020
ms.locfileid: "84166054"
---
# <a name="prepare-android-apps-for-app-protection-policies-with-the-intune-app-wrapping-tool"></a>使用 Intune App Wrapping Tool 準備應用程式保護原則的 Android 應用程式

使用 Microsoft Intune App Wrapping Tool for Android 變更內部 Android 應用程式的行為，讓您限制應用程式的功能，而不需變更應用程式本身的程式碼。

此工具是一個 Windows 命令列應用程式，可在 PowerShell 中執行並在您的 Android 應用程式周圍建立包裝函式。 包裝好應用程式後，您便可以透過在 Intune 中設定[行動應用程式管理原則](../apps/app-protection-policies.md)，以變更應用程式的功能。

執行此工具之前，請檢閱[執行 App Wrapping Tool 的安全性考量](#security-considerations-for-running-the-app-wrapping-tool)。 若要下載此工具，請前往 GitHub 的 [Microsoft Intune App Wrapping Tool for Android](https://github.com/msintuneappsdk/intune-app-wrapping-tool-android)。

## <a name="fulfill-the-prerequisites-for-using-the-app-wrapping-tool"></a>滿足使用 App Wrapping Tool 的必要條件

- 您必須在執行 Windows 7 或更新版本的 Windows 電腦上執行 App Wrapping Tool。

- 您的輸入應用程式必須是副檔名為 .apk 的有效 Android 應用程式套件，而且：

  - 它無法加密。
  - 它之前未使用 Intune App Wrapping Tool 進行包裝。
  - 它必須是針對 Android 4.0 或更新版本編寫的。

- 該應用程式必須是由貴公司所開發，或針對貴公司所開發。 您無法在下載自 Google Play 商店的應用程式使用這個工具。

- 若要執行 App Wrapping Tool，您必須安裝最新版的 [Java Runtime Environment](https://java.com/download/)，然後確定已在您的 Windows 環境變數中將 Java 路徑變數設為 C:\ProgramData\Oracle\Java\javapath。 如需詳細說明，請參閱 [Java 文件](https://java.com/download/help/)。

    > [!NOTE]
    > 在某些情況下，Java 32 位元版本可能會導致記憶體問題。 您最好安裝 64 位元版本。

- Android 要求所有應用程式套件 (.apk) 均已簽署。 若要**重複使用**現有憑證和整個簽署憑證指引，請參閱[重複使用簽署憑證和包裝應用程式](app-wrapper-prepare-android.md#reusing-signing-certificates-and-wrapping-apps)。 使用 Java 可執行檔 keytool.exe 產生簽署包裝輸出應用程式所需的**新**認證。 任何設定的密碼都必須安全，但請記下密碼，因為執行 App Wrapping Tool 時會需要這些密碼。

    > [!NOTE]
    > Intune App Wrapping Tool d不支援 Google 的 v2 與即將推出的 v3 應用程式簽署配置。 使用 Intune App Wrapping Tool 封裝 .apk 檔案之後，建議使用 [Google 提供的 Apksigner 工具]( https://developer.android.com/studio/command-line/apksigner)。 這將可確保一旦您的應用程式到達使用者裝置，就可由 Android 標準適當地啟動。 

- (選擇性) 應用程式有時可能會達到 Dalvik 可執行檔 (DEX) 大小限制，因為包裝期間新增 Intune MAM SDK 類別。 DEX 檔案是 Android 應用程式編譯的一部分。 Intune App Wrapping Tool 會在最低 API 層級 21 或以上的應用程式包裝期間，自動處理 DEX 檔案溢位 (直至 [v.1.0.2501.1](https://github.com/msintuneappsdk/intune-app-wrapping-tool-android/releases))。 針對最低 API 層級為 < 21 的應用程式，最佳做法是使用包裝函式的 `-UseMinAPILevelForNativeMultiDex` 旗標來提高最低 API 層級。 若客戶無法增加應用程式的最低 API 層級，可使用下列 DEX 溢位因應措施。 在某些組織中，這可能需要與編譯應用程式的人員 (即應用程式建置小組) 合作：

  - 請使用 ProGuard 從應用程式的主要 DEX 檔案排除未使用的類別參考。
  - 針對使用 v 3.1.0 或更高版本 Android Gradle 外掛程式的客戶，請停用 [D8 dexer](https://android-developers.googleblog.com/2018/04/android-studio-switching-to-d8-dexer.html)。  

## <a name="install-the-app-wrapping-tool"></a>安裝應用程式包裝工具

1. 從 [GitHub 儲存機制](https://github.com/msintuneappsdk/intune-app-wrapping-tool-android)將 Intune App Wrapping Tool for Android 的 InstallAWT.exe 安裝檔案下載至 Windows 電腦。 開啟安裝檔案。

2. 接受授權合約，然後完成安裝。

記下您安裝此工具的資料夾。 預設位置為：C:\Program Files (x86)\Microsoft Intune Mobile Application Management\Android\App Wrapping Tool。

## <a name="run-the-app-wrapping-tool"></a>執行應用程式包裝工具

1. 在您安裝應用程式包裝工具的 Windows 電腦上，開啟 PowerShell 視窗。

2. 從安裝此工具的資料夾，匯入 App Wrapping Tool PowerShell 模組：

   ```PowerShell
   Import-Module .\IntuneAppWrappingTool.psm1
   ```

3. 使用 **invoke-AppWrappingTool** 命令執行工具，其使用語法如下：

   ```PowerShell
   Invoke-AppWrappingTool [-InputPath] <String> [-OutputPath] <String> -KeyStorePath <String> -KeyStorePassword <SecureString>
   -KeyAlias <String> -KeyPassword <SecureString> [-SigAlg <String>] [<CommonParameters>]
   ```

   下表詳列 **invoke-AppWrappingTool** 命令的屬性：

|屬性|資訊|範例|
|-------------|--------------------|---------|
|**-InputPath**&lt;String&gt;|來源 Android 應用程式 (.apk) 的路徑。| |
 |**-OutputPath**&lt;String&gt;|輸出的 Android 應用程式路徑。 如果此路徑與 InputPath 的目錄路徑相同，封裝會失敗。| |
|**-KeyStorePath**&lt;String&gt;|包含要簽署之公開/私密金鑰組的金鑰儲存區檔案路徑。|根據預設，金鑰儲存區檔案會儲存在 "C:\Program Files (x86)\Java\jreX.X.X_XX\bin"。 |
|**-KeyStorePassword**&lt;SecureString&gt;|用來解密 keystore 的密碼。 Android 要求所有應用程式套件 (.apk) 均已簽署。 使用 Java keytool 來產生 KeyStorePassword。 在這裡深入了解 Java [金鑰儲存區](https://docs.oracle.com/javase/7/docs/api/java/security/KeyStore.html)。| |
|**-KeyAlias**&lt;String&gt;|要用於簽署的金鑰名稱。| |
|**-KeyPassword**&lt;SecureString&gt;|用來解密簽署用途之私密金鑰的密碼。| |
|**-SigAlg**&lt;SecureString&gt;| (選擇性) 要用於簽署的簽章演算法名稱。 此演算法必須與私密金鑰相容。|範例：SHA256withRSA、SHA1withRSA|
|**-UseMinAPILevelForNativeMultiDex**| 選擇性使用此旗標，將來源 Android 應用程式的最低 API 層級提高到 21。 此旗標會提示進行確認，因為這會限制可能安裝此應用程式的人員。 使用者可以將參數 "-Confirm:$false" 附加至其 PowerShell 命令，以略過確認對話方塊。 此旗標只能供最低 API < 21 的應用程式客戶使用，這些應用程式會因為 DEX 溢位錯誤而無法成功包裝。 | |
| **&lt;CommonParameters&gt;** | (選擇性) 此命令支援 verbose 和 debug 等常用 PowerShell 參數。 |


- 如需常用參數清單，請參閱 [Microsoft 指令碼中心](https://technet.microsoft.com/library/hh847884.aspx)。

- 若要查看工具的詳細使用方式資訊，請輸入命令：

    ```PowerShell
    Help Invoke-AppWrappingTool
    ```

**範例：**

匯入 PowerShell 模組。

```PowerShell
Import-Module "C:\Program Files (x86)\Microsoft Intune Mobile Application Management\Android\App Wrapping Tool\IntuneAppWrappingTool.psm1"
```

在原生應用程式 HelloWorld.apk 執行 App Wrapping Tool。

```PowerShell
invoke-AppWrappingTool -InputPath .\app\HelloWorld.apk -OutputPath .\app_wrapped\HelloWorld_wrapped.apk -KeyStorePath "C:\Program Files (x86)\Java\jre1.8.0_91\bin\mykeystorefile" -keyAlias mykeyalias -SigAlg SHA1withRSA -Verbose
```

系統接著會提示您提供 **KeyStorePassword** 和 **KeyPassword**。 輸入您用以建立金鑰儲存區檔案的認證。

隨即會產生已包裝的應用程式和記錄檔，並儲存於您指定的輸出路徑中。

## <a name="how-often-should-i-rewrap-my-android-application-with-the-intune-app-wrapping-tool"></a>我應該多久一次，用 Intune App Wrapping Tool 來重新包裝我的 Android 應用程式？
會需要重新包裝應用程式的主要案例如下：
* 應用程式本身發行了新版本。 舊版的應用程式已包裝並上傳至 Intune 主控台。
* Intune App Wrapping Tool for Android 發行了新版本，讓關鍵 Bug 獲得修正，或提供新的特定 Intune 應用程式保護原則功能。 這會透過 [Microsoft Intune App Wrapping Tool for Android](https://github.com/msintuneappsdk/intune-app-wrapping-tool-android) 的 GitHub 存放庫，每 6-8 週發生一次。

重新包裝的幾種最佳做法包括： 
* 保留在建置程序中使用的簽署憑證。請參閱[重複使用簽署憑證和包裝應用程式](app-wrapper-prepare-android.md#reusing-signing-certificates-and-wrapping-apps)

## <a name="reusing-signing-certificates-and-wrapping-apps"></a>重複使用簽署憑證和包裝應用程式
Android 要求所有的應用程式都必須以有效的憑證簽署，才能安裝在 Android 裝置上。

已包裝的應用程式可簽署為包裝程序的一部分，或在包裝「之後」  使用現有的簽署工具簽署 (應用程式在包裝前的任何簽署資訊皆予以捨棄)。 可能的話，包裝期間應該使用建置程序期間所用的簽署資訊。 在某些組織中，這可能需要與擁有金鑰存放區資訊的人合作 (即應用程式建置小組)。 

如果無法使用先前的簽署憑證，或者之前並未部署應用程式，您可以遵循 [Android 開發人員指南](https://developer.android.com/studio/publish/app-signing.html#signing-manually)中的指示建立新的簽署憑證。

如果之前已使用不同的簽署憑證來部署應用程式，應用程式在升級之後即無法上傳至 Intune。 如果應用程式的簽署憑證和建置時的憑證不同，應用程式升級案例就會中斷。 因此，應該維持任何新的簽署憑證以用於應用程式升級。 

## <a name="security-considerations-for-running-the-app-wrapping-tool"></a>執行 App Wrapping Tool 的安全性考量
若要防止潛在的詐騙、資訊洩漏和權限提升攻擊：

- 請確定輸入的企業營運 (LOB) 應用程式、輸出應用程式及 Java 金鑰儲存區都位於執行 App Wrapping Tool 的同一部 Windows 電腦上。

- 在執行工具所在的同一部電腦上，將輸出應用程式匯入 Intune。 如需 Java keytool 的詳細資訊，請參閱 [keytool](https://docs.oracle.com/javase/8/docs/technotes/tools/unix/keytool.html)。

- 如果輸出應用程式和工具位於通用命名慣例 (UNC) 路徑上，而您未在同一部電腦上執行工具和輸入檔案，請使用 [網際網路通訊協定安全性 (IPsec)](https://wikipedia.org/wiki/IPsec) 或[伺服器訊息區 (SMB) 簽署](https://support.microsoft.com/kb/887429)，將環境設定為安全的。

- 確認應用程式來自信任的來源。

- 保護包含已包裝應用程式的輸出目錄。 考慮針對輸出使用使用者層級目錄。

## <a name="see-also"></a>請參閱
- [決定如何準備應用程式以使用 Microsoft Intune 進行行動應用程式管理](../developer/apps-prepare-mobile-application-management.md)

- [Microsoft Intune App SDK for Android 開發人員指南](../developer/app-sdk-android.md)
