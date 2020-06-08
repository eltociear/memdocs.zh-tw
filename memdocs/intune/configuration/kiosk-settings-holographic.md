---
title: Microsoft Intune 中 Windows Holographic for Business 的 Kiosk 設定 - Azure | Microsoft Docs
description: 在 Microsoft Intune 中，將您的 Windows Holographic for Business 裝置設定為單一應用程式和多應用程式 kiosk、自訂開始功能表、新增應用程式、顯示工作列，以及設定網頁瀏覽器。
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 05/18/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure; seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: 3d54e02c7bb88354ec59a9a8ce780ff559377466
ms.sourcegitcommit: 169e279ba686c28d9a23bc0a54f0a2a0d20bdee4
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/19/2020
ms.locfileid: "83556093"
---
# <a name="windows-holographic-for-business-device-settings-to-run-as-a-kiosk-in-intune"></a>Intune 中 Kiosk 執行模式的 Windows Holographic for Business 裝置設定

在 Windows Holographic for Business 裝置上，您可以設定這些裝置在單一應用程式 kiosk 模式或多應用程式 kiosk 模式中執行。 Windows Holographic for Business 不支援某些功能。

本文列出並說明您可以在 Windows Holographic for Business 裝置 上控制的各種不同設定。 作為行動裝置管理 (MDM) 解決方案的一部分，請使用這些設定來設定讓您的 Windows Holographic for Business 裝置以 kiosk 模式執行。

身為 Intune 系統管理員，您可以建立這些設定並將其指派給您的裝置。

若要深入了解 Intune 中的 Windows kiosk 功能，請參閱[設定 Kiosk 設定](kiosk-settings.md)。

## <a name="before-you-begin"></a>開始之前

- [建立 Windows 10 kiosk裝置組態設定檔](kiosk-settings.md#create-the-profile)。

  當您建立 Windows 10 kiosk 裝置組態設定檔時，設定會比本文所列的更多。 Windows Holographic for Business 裝置支援本文中的設定。

- 此 kiosk 設定檔直接與您使用 [Microsoft Edge kiosk 設定](device-restrictions-windows-holographic.md#microsoft-edge-browser)建立的裝置限制設定檔相關。 總括來說：

  1. 建立此 kiosk 設定檔以在 kiosk 模式下執行裝置。
  2. 建立[裝置限制設定檔](device-restrictions-windows-holographic.md#microsoft-edge-browser)，並設定 Microsoft Edge 中允許的特定功能及設定。

> [!IMPORTANT]
> 請務必將此 kiosk 設定檔指派給與您 [Microsoft Edge 設定檔](device-restrictions-windows-holographic.md#microsoft-edge-browser)相同的裝置。

## <a name="single-app-full-screen-kiosk"></a>單一應用程式、全螢幕 kiosk

僅在裝置執行一個應用程式。 當使用者登入時，會啟動特定的應用程式。 此模式也會限制使用者開啟新的應用程式或變更執行中的應用程式。

- **使用者登入類型**：選取執行應用程式的帳戶類型。 選項包括：

  - **自動登入 (Windows 10 1803 版及更新版本)** ：不支援 Windows Holographic for Business。
  - **本機使用者帳戶**：輸入本機 (對裝置而言) 使用者帳戶。 或者，輸入與 kiosk 應用程式建立關聯的 Microsoft 帳戶 (MSA) 帳戶。 您輸入的帳戶會登入 kiosk。

    針對對外公開環境中的 kiosk，應使用具備最低權限的使用者類型。

- **應用程式類型**：選取 [新增市集應用程式]。

  - **要以 kiosk 模式執行的應用程式**：從清單中選取應用程式。

    目前未列出任何應用程式？ 請使用[用戶端應用程式](../apps/apps-add.md)中的步驟新增一些應用程式。

## <a name="multi-app-kiosk"></a>多應用程式 kiosk

此模式下的應用程式可以在 [開始] 功能表中使用。 這些應用程式是使用者唯一能夠開啟的應用程式。 如果應用程式對另一個應用程式具有相依性，則兩者都必須包含在允許的應用程式清單中。

- **以 S 模式的 Windows 10 裝置為目標**：選取 [否]。 Windows Holographic for Business 不支援 S 模式。

- **使用者登入類型**：新增一或多個能夠使用您所新增應用程式的使用者帳戶。 選項包括：

  - **自動登入 (Windows 10 1803 版及更新版本)** ：不支援 Windows Holographic for Business。
  - **本機使用者帳戶**：[新增] 本機 (對裝置而言) 使用者帳戶。 您輸入的帳戶會登入 kiosk。
  - **Azure AD 使用者或群組 (Windows 10 1803 版和更新版本)** ：需要使用者認證才能登入裝置。 選取 [新增] 以從清單中選擇 Azure AD 使用者或群組。 您可以選取多個使用者和群組。 選擇 [選取] 以儲存您的變更。
  - **HoloLens 訪客**：訪客帳戶是來賓帳戶，不需要任何使用者認證或驗證，如 [shared PC mode concepts](https://docs.microsoft.com/windows/configuration/set-up-shared-or-guest-pc#shared-pc-mode-concepts) (共用電腦模式概念) 中所述。

- **瀏覽器及應用程式**：新增要在 kiosk 裝置上執行的應用程式。 請記住，您可以新增數個應用程式。

  - **瀏覽器**
    - **新增 Microsoft Edge**：Microsoft Edge 會新增至應用程式方格，所有的應用程式都可以在此 Kiosk 上執行。 選取 Microsoft Edge kiosk 模式類型：

      - **標準模式 (Microsoft Edge 完整版)** ：執行具備所有瀏覽功能的 Microsoft Edge 完整版本。 使用者資料和狀態會在工作階段之間儲存。
      - **公開瀏覽 (InPrivate)** ：執行 Microsoft Edge InPrivate 的多重索引標籤版本，為在全螢幕模式中所執行 Kiosk 提供量身打造的體驗。

      如需這些選項的詳細資訊，請參閱[部署 Microsoft Edge kiosk 模式](https://docs.microsoft.com/microsoft-edge/deploy/microsoft-edge-kiosk-mode-deploy#supported-configuration-types)。

      > [!NOTE]
      > 此設定可啟用裝置上的 Microsoft Edge 瀏覽器。 若要設定特定於 Microsoft Edge 的設定，請建立裝置限制設定檔 ([裝置設定] > [設定檔] > [建立設定檔] > [Windows 10] 平台 > [裝置限制] > [Microsoft Edge 瀏覽器])。 [Microsoft Edge 瀏覽器](device-restrictions-windows-holographic.md#microsoft-edge-browser)會列出並描述可用的 Holographic for Business 設定。

    - **新增 Kiosk 瀏覽器**：不支援 Windows Holographic for Business。

  - **應用程式**
    - **新增市集應用程式**：選取所新增或部署至 Intune 作為[用戶端應用程式](../apps/apps-add.md)的現有應用程式，包括 LOB 應用程式。 如果未列出任何應用程式，則 Intune 會支援所[新增至 Intune](../apps/store-apps-windows.md) 的許多[應用程式類型](../apps/apps-add.md)。
    - **新增 Win32 應用程式**：Windows Holographic for Business 不支援。
    - **依 AUMID 新增**：使用此選項可新增現成的 Windows 應用程式，例如 [記事本] 或 [小算盤]。 輸入下列內容：

      - **應用程式名稱**：必要。 輸入應用程式的名稱。
      - **應用程式使用者模型識別碼 (AUMID)** ：必要。 輸入 Windows 應用程式的應用程式使用者模型識別碼 (AUMID)。 若要取得此識別碼，請參閱 [find the Application User Model ID of an installed app](https://docs.microsoft.com/windows-hardware/customize/enterprise/find-the-application-user-model-id-of-an-installed-app) (尋找已安裝應用程式的應用程式使用者模型識別碼)。

    - **自動啟動**：選擇性。 在您新增應用程式和瀏覽器後，請選取一個應用程式或瀏覽器，以在使用者登入時自動開啟。 只有一個應用程式或瀏覽器可以自動啟動。
    - **磚大小**：必要。 在您新增應用程式後，請選取小型、中型、寬或大型應用程式磚大小。

- **使用其他開始畫面版面配置**：選取 [是] 以輸入描述應用程式在 [開始] 功能表上如何顯示 (包括應用程式的順序) 的 XML 檔案。 如果您需要在 [開始] 功能表中有更多自訂項目，請使用此選項。 [自訂與匯出 [開始] 配置](https://docs.microsoft.com/hololens/hololens-kiosk#start-layout-for-hololens)提供一些指引，並包含 Windows Holographic for Business 裝置的特定 XML 檔案。

- **Windows 工作列**：不支援 Windows Holographic for Business。
- **允許下載資料夾的存取權**：不支援 Windows Holographic for Business。
- **指定應用程式重新啟動的維護視窗**：不支援 Windows Holographic for Business。

## <a name="next-steps"></a>後續步驟

[指派設定檔](device-profile-assign.md)並[監視其狀態](device-profile-monitor.md)。

您也可以為 [Android](device-restrictions-android.md#kiosk)、[Android 企業](device-restrictions-android-for-work.md#dedicated-devices)及 [Windows 10 和更新版本](kiosk-settings-windows.md) 裝置建立 kiosk 設定檔。
