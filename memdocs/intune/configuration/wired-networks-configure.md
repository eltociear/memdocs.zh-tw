---
title: 在 Microsoft Intune 中設定 macOS 裝置的 802.1x 有線網路設定 - Azure | Microsoft Docs
titleSuffix: ''
description: 建立或新增適用於 macOS 桌上型電腦裝置的有線網路裝置組態設定檔。 查看不同的設定、新增憑證、選擇 EAP 類型，以及在 Microsoft Intune 中選取驗證方法。
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 06/11/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.reviewer: tycast
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: f237daa5e95cb5428e707828f0104c697e338718
ms.sourcegitcommit: 387706b2304451e548d6d9c68f18e4764a466a2b
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2020
ms.locfileid: "85095749"
---
# <a name="add-and-use-wired-networks-settings-on-your-macos-devices-in-microsoft-intune"></a>在 Microsoft Intune 中的 macOS 裝置上新增及使用有線網路設定

許多組織會使用有線網路，將網路存取權授與桌上型電腦。 Microsoft Intune 可包含能部署到您組織中 macOS 使用者與裝置的內建設定。 這組設定稱為「設定檔」。 您可在設定檔中包含一般設定，例如網路介面、已接受的 EAP 類型與伺服器信任設定。

當設定檔就緒時，可以指派給不同的使用者與群組。 指派之後，您的使用者即可在無須自行設定的情況下，存取您組織的有線網路。

作為行動裝置管理 (MDM) 解決方案的一部分，請使用這項功能來建立 802.1x 設定檔，以管理有線網路。 接著，將這些有線網路部署至您的 macOS 裝置。

本功能適用於：

- macOS

例如，您有一個名為 **Contoso 有線網路**的有線網路。 您要將所有 macOS 桌上型電腦都設定為連線到此網路。 程序如下︰

1. 建立包含可連線到 **Contoso 有線網路**之設定的有線網路設定檔。
2. 將設定檔指派給包含所有使用者 macOS 桌上型電腦的群組。 如需使用群組類型的建議，請參閱[使用者群組與裝置群組的比較](device-profile-assign.md#user-groups-vs-device-groups)。
3. 使用者會在其桌上型電腦的網路清單中找到 **Contoso 有線網路**。 然後他們可以使用您選擇的驗證方法連線到網路。

本文會列出建立有線網路設定檔的步驟。 並且包含描述不同設定的連結。

## <a name="create-the-profile"></a>建立設定檔

1. 登入 [Microsoft Endpoint Manager 系統管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)。
2. 選取 [裝置] > [組態設定檔] > [建立設定檔]。
3. 輸入下列內容：

    - **平台**：選取 [macOS]。
    - **設定檔**：選取 [有線網路]。

4. 選取 [建立]。
5. 在 [基本資訊] 中，輸入下列內容：

    - **名稱**：為設定檔輸入描述性名稱。 命名您的設定檔，以方便之後能輕鬆識別。 例如，良好的設定檔名稱為**整個公司在 macOS 裝置上的有線網路設定檔**。
    - **描述**：輸入設定檔的描述。 這是選擇性設定，但建議執行。

6. 選取 [下一步]。
7. 選取 [組態設定] 中網路的網路介面，然後選擇可延伸的驗證通訊協定 (EAP) 類型。 如需所有設定的清單及其用途，請參閱：

    - [macOS](wired-network-settings-macos.md)

8. 選取 [下一步]。
9. 選取 [指派] 中將接收您設定檔的使用者群組或裝置群組。 如需指派設定檔的詳細資訊，請參閱[指派使用者和裝置設定檔](device-profile-assign.md)。

    選取 [下一步]。

10. 在 [檢閱 + 建立] 中，檢閱您的設定。 當您選取 [建立] 時，系統會儲存您的變更，然後指派設定檔。 原則也會顯示在設定檔清單中。

> [!TIP]
> 您的有線網路設定檔如果使用憑證式驗證，請將有線網路設定檔、憑證設定檔及信任的根設定檔部署至相同的群組。 此指派可確定每部裝置都能辨識您憑證授權單位的合法性。 如需詳細資訊，請參閱[使用 Microsoft Intune 設定憑證](../protect/certificates-configure.md)。

## <a name="next-steps"></a>後續步驟

設定檔建立後，不一定會執行任何動作。 請務必[指派此設定檔](device-profile-assign.md)並[監視其狀態](device-profile-monitor.md)。
