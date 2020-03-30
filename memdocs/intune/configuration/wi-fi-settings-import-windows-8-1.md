---
title: 在 Microsoft Intune 中為 Windows 裝置匯入 Wi-Fi 設定 - Azure | Microsoft Docs
description: 使用 netsh wlan，從 Windows 裝置將 Wi-Fi 設定匯出成 XML 檔案。 接著再將此檔案匯入 Intune，為執行 Windows 8.1、Windows 10 及 Windows Holographic for Business 的裝置匯入 Wi-Fi 設定檔。
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 03/19/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: ef2c4593ad9809614b7e0d497745065fef12df69
ms.sourcegitcommit: 017b93345d8d8de962debfe3db5fc1bda7719079
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/21/2020
ms.locfileid: "80086379"
---
# <a name="import-wi-fi-settings-for-windows-devices-in-intune"></a>在 Intune 中，為 Windows 裝置匯入 Wi-Fi 設定

對於執行 Windows 的裝置，您可以匯入先前匯出到檔案的 Wi-Fi 設定檔。 **對於 Windows 10 及更新版本的裝置，您也可以直接在 Intune 中[建立 Wi-Fi 設定檔](wi-fi-settings-windows.md)** 。

適用於：  
- Windows 8.1 及更新版本
- Windows 10 及更新版本
- Windows 10 Desktop 或行動裝置版
- Windows Holographic for Business

## <a name="before-you-begin"></a>開始之前

[建立裝置設定檔](wi-fi-settings-configure.md)。 設定檔名稱**必須**與 Wi-Fi 設定檔 XML 中的名稱屬性相同。 否則，就會發生失敗。

## <a name="import-the-wi-fi-settings-into-intune"></a>將 Wi-Fi 設定匯入 Intune

- **連線名稱**：輸入 Wi-Fi 連線的名稱。 當使用者瀏覽可用的 Wi-Fi 網路時，即會看到此名稱。
- **設定檔 XML**：選取瀏覽按鈕，然後選取包含您想匯入之 Wi-Fi 設定檔設定的 XML 檔案。
- **檔案內容**：顯示您所選取組態設定檔的 XML 程式碼。

## <a name="export-wi-fi-settings-from-a-windows-device"></a>從 Windows 裝置匯出 Wi-Fi 設定

在 Windows 中，您可以使用 `netsh wlan`，將現有的 Wi-Fi 設定檔匯出成 Intune 能夠讀取的 XML 檔案。 必須以純文字格式匯出金鑰，才能順利使用設定檔。

在已安裝必要 WiFi 設定檔的 Windows 電腦上，請使用下列步驟：

1. 為匯出的 Wi-Fi 設定檔建立本機資料夾，例如 **c:\WiFi**。
2. 以系統管理員身分開啟命令提示字元。
3. 執行 `netsh wlan show profiles` 命令。 記下所要匯出的設定檔名稱。 在此範例中，設定檔名稱是 **WiFiName**。
4. 執行 `netsh wlan export profile name="ProfileName" folder=c:\Wifi` 命令。 此命令會在目標資料夾中建立名為 **Wi-Fi-WiFiName.xml** 的 Wi-Fi 設定檔。

> [!IMPORTANT]
> - 如果您要匯出包含預先共用金鑰的 Wi-Fi 設定檔，就**必須**將 `key=clear` 新增至命令中。 例如，輸入：`netsh wlan export profile name="ProfileName" key=clear folder=c:\Wifi`
> - 搭配 Windows 10 使用預先共用金鑰會導致在 Intune 中顯示補救錯誤。 發生這種情況時，系統會將 Wi-Fi 設定檔適當地指派給裝置，而該設定檔將如預期般運作。
> - 如果您要匯出包含預先共用金鑰的 Wi-Fi 設定檔，請確定該檔案受到保護。 該金鑰會採用存文字格式，因此您需負責保護該金鑰。

## <a name="next-steps"></a>後續步驟

設定檔已建立，但它不會執行任何動作。 接下來，[指派設定檔](device-profile-assign.md)並[監視其狀態](device-profile-monitor.md)。

請參閱 [Wi-Fi 設定概觀](wi-fi-settings-configure.md)，包括其他可用平台。
