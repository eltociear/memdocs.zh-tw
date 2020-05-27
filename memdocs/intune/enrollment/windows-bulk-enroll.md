---
title: Windows 10 的大量註冊
titleSuffix: Microsoft Intune
description: 建立 Microsoft Intune 的大量註冊套件
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 5/21/2018
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 1f39c02a-8d8a-4911-b4e1-e8d014dbce95
ms.reviewer: spshumwa
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: ecbde2f6e6a40379cd37a6ddebe09fa9dab8e3b1
ms.sourcegitcommit: 302556d3b03f1a4eb9a5a9ce6138b8119d901575
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/27/2020
ms.locfileid: "83988930"
---
# <a name="bulk-enrollment-for-windows-devices"></a>Windows 裝置的大量註冊

身為系統管理員，您可以將大量的新 Windows 裝置加入 Azure Active Directory 和 Intune。 若要為您的 Azure AD 租用戶大量註冊裝置，請使用 Windows Configuration Designer (WCD) 應用程式來建立佈建套件。 將佈建套件套用到公司擁有的裝置，就會將裝置加入您的 Azure AD 租用戶，並加以註冊以供 Intune 管理。 套用套件之後，您的 Azure AD 使用者即可登入。

Azure AD 使用者是這些裝置上的標準使用者，並且會接收指派的 Intune 原則和必要應用程式。 使用 Windows 大量註冊在 Intune 中註冊的 Windows 裝置，可以使用公司入口網站應用程式安裝可用的應用程式。 

## <a name="prerequisites-for-windows-devices-bulk-enrollment"></a>Windows 裝置大量註冊的先決條件

- 執行 Windows 10 Creators Update (組建 1709) 或更新版本的裝置
- [Windows 自動註冊](windows-enroll.md#enable-windows-10-automatic-enrollment)

## <a name="create-a-provisioning-package"></a>建立佈建套件

1. 從 Microsoft 網上商店下載 [Windows Configuration Designer (WCD)](https://www.microsoft.com/store/apps/9nblggh4tx22)。
   ![Windows 設定設計工具 Microsoft Store 的螢幕擷取畫面](./media/windows-bulk-enroll/bulk-enroll-store.png)

2. 開啟 **Windows Configuration Designer** 應用程式並選取 [Provision desktop devices (佈建電腦裝置)]  。
   ![在 Windows Configuration Designer 應用程式中選取佈建電腦裝置的螢幕擷取畫面](./media/windows-bulk-enroll/bulk-enroll-select.png)

3. **新專案** 視窗隨即開啟，您可以在其中指定下列資訊：
   - **Name (名稱)** - 專案名稱
   - **Project folder (專案資料夾)** - 專案的儲存位置
   - **Description (描述)** - 專案的選擇性描述 ![在 Windows Configuration Designer 應用程式中指定名稱、專案資料夾和描述的螢幕擷取畫面](./media/windows-bulk-enroll/bulk-enroll-name.png)

4. 輸入您裝置的唯一名稱。 名稱可以包含序號 (%SERIAL%) 或一組隨機字元。 您也可以選擇輸入產品金鑰 (如果您正在升級 Windows 的版本)、將裝置設定為共用，以及移除預先安裝的軟體。
   
   ![在 Windows 設定設計工具應用程式中指定名稱和產品金鑰的螢幕擷取畫面](./media/windows-bulk-enroll/bulk-enroll-device.png)

5. 您可以選擇設定裝置第一次啟動時要連線的 Wi-Fi 網路。  如果未設定網路裝置，則裝置第一次啟動時需要有線網路連線。
   ![在 Windows Configuration Designer 中啟用 Wi-Fi (包含網路 SSID 和網路類型選項) 的螢幕擷取畫面](./media/windows-bulk-enroll/bulk-enroll-network.png)

6. 選取 [Enroll in Azure AD (在 Azure AD 中註冊)]  ，輸入 [Bulk Token Expiry (大量權杖到期)]  日期，然後選取 [Get Bulk Token (取得大量權杖)]  。
   ![Windows 設定設計工具應用程式中帳戶管理的螢幕擷取畫面](./media/windows-bulk-enroll/bulk-enroll-account.png)

7. 提供您的 Azure AD 認證以取得大量權杖。
   ![登入 Windows 設定設計工具應用程式的螢幕擷取畫面](./media/windows-bulk-enroll/bulk-enroll-cred.png)

8. 在 [在此裝置的任何位置使用此帳戶]  頁面上，選取 [僅限此應用程式]  。

9. 成功擷取「大量權杖」  之後，按一下 [Next (下一步)]  。

10. 您可以選擇 [Add applications (新增應用程式)]  和 [Add certificates (新增憑證)]  。 這些應用程式和憑證都佈建在該裝置上。

11. 您可以選擇以密碼保護佈建套件。  按一下 [建立]  。
    ![Windows 設定設計工具應用程式中套件保護的螢幕擷取畫面](./media/windows-bulk-enroll/bulk-enroll-create.png)

## <a name="provision-devices"></a>佈建裝置

1. 存取應用程式所指定 [Project folder (專案資料夾)]  中指定的佈建套件位置。

2. 選擇將佈建套件套用到裝置的方式。  您可以使用下列其中一種方式將佈建套件套用到裝置：
   - 將佈建套件置於 USB 磁碟機，將 USB 磁碟機插入到要大量註冊的裝置，然後在初始安裝期間套用佈建套件
   - 將佈建套件置於網路資料夾，並在初始安裝之後套用佈建套件

   如需套用佈建套件的逐步指示，請參閱[套用佈建套件](https://technet.microsoft.com/itpro/windows/configure/provisioning-apply-package)。

3. 套用套件之後，裝置會在一分鐘後自動重新啟動。
   ![在 Windows Configuration Designer 應用程式中指定名稱、專案資料夾和描述的螢幕擷取畫面](./media/windows-bulk-enroll/bulk-enroll-add.png)

4. 當裝置重新啟動時，它會連線到 Azure Active Directory 並在 Microsoft Intune 中註冊。

## <a name="troubleshooting-windows-bulk-enrollment"></a>針對 Windows 大量註冊進行疑難排解

### <a name="provisioning-issues"></a>佈建問題
佈建是要用於新的 Windows 裝置上。 佈建如果失敗，可能需要進行裝置抹除，或使用開機映像進行裝置復原。 下列例子說明佈建失敗的某些原因：

- 嘗試加入 Active Directory 網域或 Azure Active Directory 租用戶的佈建套件，如果未建立本機帳戶，當沒有網路連線而造成網域加入程序失敗時，會使得裝置無法使用。
- 由佈建套件執行的指令碼是在系統環境中執行。 指令碼可以任意對裝置檔案系統與設定進行變更。 惡意或不良的指令碼可能會使裝置處於某種狀態，而只能透過重新安裝映像或進行抹除才能復原裝置。

您可以在事件檢視器中的 **Provisioning-Diagnostics-Provider** 系統管理記錄檔中，檢查您套件中設定的成功/失敗。

### <a name="bulk-enrollment-with-wi-fi"></a>大量註冊使用 Wi-Fi 

未使用開放式網路時，您必須使用[裝置層級憑證](../protect/certificates-configure.md)來起始連線。 大量註冊的裝置無法使用指派給使用者的憑證來存取網路。 

### <a name="conditional-access"></a>條件式存取
使用大量註冊來註冊的 Windows 裝置無法使用條件式存取。
