---
title: 在 Microsoft Intune 中將自訂設定新增至 macOS 裝置 - Azure | Microsoft Docs
titleSuffix: ''
description: 從 Apple Configurator 或 Apple Profile Manager 工具匯出 macOS 設定，然後將這些設定匯入 Microsoft Intune。 這些設定可以建立、使用及控制 macOS 裝置上的自訂設定和功能。 此自訂設定檔可接著指派或散發到您組織中的 macOS 裝置，以建立基準或標準。
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 03/24/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.reviewer: kakyker
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 2e900252392f1e6f057561d8d07f6e764dc0aafc
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "80359361"
---
# <a name="use-custom-settings-for-macos-devices-in-microsoft-intune"></a>在 Microsoft Intune 中使用 macOS 裝置的自訂設定

透過 Microsoft Intune，您可以使用「自訂設定檔」新增或建立 macOS 裝置的自訂設定。 自訂設定檔是 Intune 中的功能。 其設計目的是為了新增 Intune 中未內建的裝置設定和功能。

使用 macOS 裝置時，您可以透過兩種方式將自訂設定匯入 Intune：

- [Apple Configurator](https://itunes.apple.com/app/apple-configurator-2/id1037126344?mt=12)
- [Apple Profile Manager](https://support.apple.com/profile-manager)

您可以使用這些工具，將設定匯出至組態設定檔。 在 Intune 中，您可以匯入此檔案，然後將設定檔指派給您的 macOS 使用者和裝置。 指派之後，系統便會散發設定。 其也會針對您組織中的 macOS 建立基準或標準。

此文章提供使用 Apple Configurator 與 Apple Profile Manager 的一些指導方針，並描述您可以設定的屬性。

## <a name="before-you-begin"></a>開始之前

[建立設定檔](custom-settings-configure.md)。

## <a name="what-you-need-to-know"></a>您必須知道的事項

- 使用 **Apple Configurator** 建立組態設定檔時，請確定您所匯出的設定與裝置上的 macOS 版本相容。 如需解決不相容設定的資訊，請在 **Apple Developer** (Apple 開發人員) 網站上搜尋 **Configuration Profile Reference** (組態設定檔參考) 和 [Mobile Device Management Protocol Reference](https://developer.apple.com/) (行動裝置管理通訊協定參考)。

- 使用 **Apple Profile Manager** 時，請確定：

  - 在 Profile Manager 中啟用[行動裝置管理](https://help.apple.com/serverapp/mac/5.7/#/apd05B9B761-D390-4A75-9251-E9AD29A61D0C)。
  - 在 Profile Manager 中新增 [macOS 裝置](https://help.apple.com/profilemanager/mac/5.7/#/pm9onzap1984)。
  - 在 Profile Manager 中新增裝置之後，請移至 [Under the Library] \(在程式庫下\)   > [Devices] \(裝置\)  > 選取您的裝置 > [Settings] \(設定\)  。 輸入裝置的一般、安全性、隱私權、目錄和憑證設定。

    下載並儲存此檔案。 您將在 Intune 設定檔中輸入此檔案。 

  - 確定您從 Apple Profile Manager 匯出的設定與裝置上的 macOS 版本相容。 如需解決不相容設定的資訊，請在 **Apple Developer** (Apple 開發人員) 網站上搜尋 **Configuration Profile Reference** (組態設定檔參考) 和 [Mobile Device Management Protocol Reference](https://developer.apple.com/) (行動裝置管理通訊協定參考)。

## <a name="custom-configuration-profile-settings"></a>自訂組態設定檔設定

- **自訂組態設定檔名稱**：輸入原則的名稱。 此名稱會在裝置上和 Intune 狀態中顯示。
- **組態設定檔**：瀏覽至使用 Apple Configurator 或 Apple Profile Manager 所建立的組態設定檔。 您匯入的檔案會顯示在 [檔案內容]  區域中。

  您也可以將裝置權杖新增到您的 `.mobileconfig` 檔案。 裝置權杖是用來新增裝置特定資訊。 例如，若要顯示序號，請輸入 `{{serialnumber}}`。 在裝置上，會顯示類似 `123456789ABC` 的文字，而且每部裝置都不重複。 輸入變數時，請務必使用大括弧 `{{ }}`。 [應用程式設定權杖](../apps/app-configuration-policies-use-ios.md#tokens-used-in-the-property-list)包含可以使用的變數清單。 您也可以使用 `deviceid` 或任何其他的裝置特定值。

  > [!NOTE]
  > 變數不會在 UI 中驗證，而且會區分大小寫。 因此，您可能會看到儲存之設定檔含有不正確的輸入。 例如，如果輸入 `{{DeviceID}}` 而非 `{{deviceid}}`，則會顯示常值字串而非裝置的唯一識別碼。 請務必輸入正確的資訊。

## <a name="next-steps"></a>後續步驟

雖然設定檔已建立，但它可能還不會執行任何動作。 接下來，[指派設定檔](device-profile-assign.md)並[監視其狀態](device-profile-monitor.md)。

[在 iOS/iPadOS 裝置上建立自訂設定檔](custom-settings-ios.md)。
