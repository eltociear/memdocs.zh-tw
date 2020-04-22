---
title: 在 Microsoft Intune 中設定 Windows 8.1 裝置的 VPN 設定 - Azure | Microsoft Docs
description: 使用虛擬私人網路 (VPN) 組態設定新增或建立 VPN 設定檔，包括執行 Windows 8.1 裝置上 Microsoft Intune 中的連線詳細資料、包含 IP 或 FQDN 位址的 Proxy 設定，以及 TCP 連接埠。
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
ms.openlocfilehash: 2c80bf57b195d7e97308ba423c9e5b53f7e29c74
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "80086460"
---
# <a name="add-vpn-settings-on-windows-81-devices-in-microsoft-intune"></a>在 Microsoft Intune 中新增 Windows 8.1 裝置的 VPN 設定

本文說明可用於設定執行 Windows 8.1 之裝置上 VPN 連線的 Intune 設定。

下列清單中的值並非全部都能設定，須取決於您選擇的設定。

## <a name="before-you-begin"></a>開始之前

[建立裝置組態設定檔](vpn-settings-configure.md)。

## <a name="base-vpn-settings"></a>基本 VPN 設定

- **僅將所有設定套用至 Windows 8.1**：在傳統 Intune 入口網站中進行此設定。 這項設定無法在 Microsoft 端點管理員系統管理中心內變更。 當設定為 [已設定]  時，則所有設定將只會套用到 Windows 8.1 裝置。 當設定為 [未設定]  時，則這些設定也會套用到 Windows 10 裝置。
- **連線名稱**：輸入此連線的名稱。 使用者瀏覽其裝置的可用 VPN 連線清單時，會看到此名稱。
- **伺服器**：新增裝置要連線的一或多部 VPN 伺服器。
  - **新增**：開啟 [新增資料列]  頁面指定下列資訊︰
    - **描述**：為伺服器指定描述性名稱，例如 **Contoso VPN 伺服器**。
    - **IP 位址或 FQDN**：提供裝置要連線之 VPN 伺服器的 IP 位址或完整網域名稱。 範例：**192.168.1.1**、**vpn.contoso.com**。
    - **預設伺服器**：啟用此伺服器作為裝置用來建立連線的預設伺服器。 您只可設定一部預設伺服器。
  - **匯入**：瀏覽至內含伺服器清單並以逗點分隔的檔案 (格式為：描述, IP 位址或 FQDN, 預設伺服器)。 選擇 [確定]  ，以將這些伺服器匯入**伺服器**清單。
  - [匯出]  ：將伺服器清單匯出成逗點分隔值 (csv) 檔案。

- **連線類型**：從下列廠商清單中選取 VPN 連線類型︰
  - **Check Point Capsule VPN**
  - **SonicWall Mobile Connect**
  - **F5 Edge Client**
  - **Pulse Secure**

<!--- **Fingerprint** (Check Point Capsule VPN only): Specify a string (for example, "Contoso Fingerprint Code") that will be used to verify that the VPN server can be trusted. A fingerprint can be sent to the client so it knows to trust any server that presents the same fingerprint when connecting. If the device doesn't already have the fingerprint, it will prompt the user to trust the VPN server that they are connecting to while showing the fingerprint. (The user manually verifies the fingerprint and chooses **trust** to connect.) --->

- **登入群組或網域** (僅限 SonicWall Mobile Connect)：指定您想要連線之登入群組或網域的名稱。

- **角色** (僅限 Pulse Secure)：指定有權存取此連線之使用者角色的名稱。 使用者角色定義個人設定和選項，以及啟用或停用某些存取功能。

- **領域** (僅限 Pulse Secure)：指定您想要使用之驗證領域的名稱。 驗證領域就是 Pulse Secure 連線類型使用的驗證資源群組。

- **自訂 XML**：指定可設定 VPN 連線的任何自訂 XML 命令。

  **Pulse Secure 範例**：

  ```xml
  <pulse-schema><isSingleSignOnCredential>true</isSingleSignOnCredential></pulse-schema>
  ```

  **CheckPoint Mobile VPN 範例**：

  ```xml
  <CheckPointVPN port="443" name="CheckPointSelfhost" sso="true" debug="3" />
  ```

  **SonicWall Mobile Connect 範例**：

  ```xml
  <MobileConnect><Compression>false</Compression><debugLogging>True</debugLogging><packetCapture>False</packetCapture></MobileConnect>
  ```

  **F5 Edge Client 範例**：

  ```xml
  <f5-vpn-conf><single-sign-on-credential /></f5-vpn-conf>
  ```

  如需撰寫自訂 XML 命令的詳細資訊，請參閱製造商的 VPN 文件。

- **分割通道**：[啟用]  可讓裝置依據流量決定要使用的連線。 例如，旅館中的使用者使用 VPN 連線存取工作檔案，但使用旅館的標準網路進行一般的網頁瀏覽。 如果您想要在 VPN 連線為使用中時強制所有流量使用 VPN 通道，則設定為 [停用]  。

## <a name="proxy-settings"></a>Proxy 設定

- **自動偵測 Proxy 設定**：如果您的 VPN 伺服器進行連線時需要 Proxy 伺服器，請指定是否要裝置自動偵測連線設定。
- **自動設定指令碼**：使用檔案設定 Proxy 伺服器。 輸入包含設定檔的 [Proxy 伺服器 URL]  。 例如，輸入 `http://proxy.contoso.com`。
- **使用 Proxy 伺服器**：若要手動輸入 Proxy 伺服器設定，可啟用此選項。
  - **位址**：輸入 Proxy 伺服器位址 (例如 IP 位址)。
  - **連接埠號碼**：輸入與 Proxy 伺服器相關聯的連接埠號碼。
- **本機位址不使用 Proxy**：如果您的 VPN 伺服器進行連線時需要 Proxy 伺服器，且您不想要使用您所輸入之本機位址的 Proxy 伺服器，則請選取此選項。

## <a name="next-steps"></a>後續步驟

設定檔已建立，但還不會執行任何動作。 接下來，[指派設定檔](device-profile-assign.md)並[監視其狀態](device-profile-monitor.md)。

在 [Android](vpn-settings-android.md)、[Android Enterprise](vpn-settings-android-enterprise.md)、[macOS](vpn-settings-macos.md) 與 [Windows 10](vpn-settings-windows-10.md) 裝置上設定 VPN 設定。
