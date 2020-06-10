---
title: 使用 Intune 搭配 FileVault 磁碟加密來加密 macOS 裝置
titleSuffix: Microsoft Intune
description: 使用內建加密方法 FileVault 來加密 macOS 裝置，並在 Intune 入口網站管理這些已加密裝置的修復金鑰。
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 04/17/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: annovich
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.openlocfilehash: 99facc87d068239962ab0d40874aa081f5e19189
ms.sourcegitcommit: 302556d3b03f1a4eb9a5a9ce6138b8119d901575
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/27/2020
ms.locfileid: "83989684"
---
# <a name="use-filevault-disk-encryption-for--macos-with-intune"></a>搭配 Intune 使用 macOS 的 FileVault 磁碟加密

Intune 支援 macOS FileVault 磁碟加密。 FileVault 是隨附於 macOS 的完整磁碟加密程式。 您可以使用 Intune，在執行 **macOS 10.13 或更新版本**的裝置上設定 FileVault。

使用下列其中一項原則類型，在您管理的裝置設定 FileVault：

- **[macOS FileVault 的端點安全性原則](#create-an-endpoint-security-policy-for-filevault)** 。 「端點安全性」 中的 FileVault 設定檔是專用於設定 FileVault 的一組設定。

  檢視[磁碟加密原則設定檔中提供的 FileVault 設定](../protect/endpoint-security-disk-encryption-profile-settings.md)。

- **[macOS FileVault 的 Endpoint Protection 裝置設定檔](#create-an-endpoint-security-policy-for-filevault)** 。 FileVault 設定是 macOS Endpoint Protection 其中一項可用的設定類別。 如需使用裝置組態設定檔的詳細資訊，請參閱[在 Inunte 中建立裝置設定檔](../configuration/device-profile-create.md)。

  檢視[裝置設定原則之 Endpoint Protection 設定檔中提供的 FileVault 設定](../protect/endpoint-protection-macos.md#filevault)。

若要管理 Windows 10 的 BitLocker，請參閱[管理 BitLocker 原則](../protect/encrypt-devices.md)。

> [!TIP]
> 顯示涵蓋所有受控裝置之裝置加密狀態詳細資料的[加密報告](encryption-monitor.md)。

當您使用 FileVault 建立加密裝置的原則後，原則會以兩階段套用至裝置。 首先，裝置已準備好讓 Intune 擷取和備份修復金鑰。 此動作稱為委付。 委付金鑰之後，磁碟加密就可以啟動。

若要讓 FileVault 在裝置上運作，則需要使用者核准的裝置註冊。 使用者必須從系統偏好設定中手動核准管理設定檔，系統才會將註冊視為使用者核准。

## <a name="permissions-to-manage-filevault"></a>管理 FileVault 的權限

若要在 Intune 中管理 FileVault，您的帳戶必須具有適用的 Intune [角色型存取控制](../fundamentals/role-based-access-control.md) (RBAC) 權限。

下列為 FileVault 權限，其為 [遠端工作] 類別的一部分，以及授與權限的內建 RBAC 角色：

- **取得 FileVault 金鑰**：
  - 技術服務人員
  - 端點安全性管理員

- **輪替 FileVault 金鑰**
  - 技術服務人員

## <a name="create-and-deploy-policy"></a>建立並部署原則

### <a name="create-an-endpoint-security-policy-for-filevault"></a>建立 FileVault 的端點安全性原則

1. 登入 [Microsoft Endpoint Manager 系統管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)。

2. 選取 [端點安全性] > [磁碟加密] > [建立原則]。

3. 在 [基本] 頁面上輸入下列屬性，然後選擇 [下一步]。
   1. **平台**：macOS
   2. **設定檔**：FileVault

   ![選取 FileVault 設定檔](./media/encrypt-devices-filevault/select-macos-filevault-es.png)

4. 在 [設定] 頁面上：
   1. 將 [啟用 FileVault] 設為 [是]。
   2. 針對 [修復金鑰類型]，只支援 [個人修復金鑰]。
   3. 設定其他設定以符合您的需求。

   請考慮新增一則訊息來協助引導使用者擷取其裝置的修復金鑰。 當您使用個人修復金鑰輪替的設定時，這項資訊對您的使用者會很有幫助，其可以自動為裝置定期產生新的修復金鑰。

   例如：若要擷取遺失或最近輪替的修復金鑰，請從任何裝置登入 Intune 公司入口網站。 在入口網站中，前往 [裝置] 並選取已啟用 FileVault 的裝置，然後選取 [取得修復金鑰]。 目前的修復金鑰會隨即顯示。

5. 當完成設定時，請選取 [下一步]。

6. 在 [範圍 (標籤)] 頁面上，選擇 [選取範圍標籤] 以開啟 [選取標籤] 窗格，並將範圍標籤指派至設定檔。

   選取 [下一步] 以繼續進行操作。

7. 在 [指派] 頁面上，選取將接收此設定檔的群組。 如需指派設定檔的詳細資訊，請參閱＜指派使用者和裝置設定檔＞。
選取 [下一步]。

8. 在 [檢閱 + 建立] 頁面上，當您完成操作時，請選擇 [建立]。 當您為自己建立的設定檔選取原則類型時，新的設定檔就會顯示在清單中。

### <a name="create-a-device-configuration-policy-for-filevault"></a>建立 FileVault 的裝置設定原則

1. 登入 [Microsoft Endpoint Manager 系統管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)。

2. 選取 [裝置] > [組態設定檔] > [建立設定檔]。

3. 設定下列選項：
   1. **平台**：macOS
   2. **設定檔**：Endpoint Protection

   ![選取 FileVault 設定檔](./media/encrypt-devices-filevault/select-macos-filevault-dc.png)

4. 選取 [設定] > [FileVault]。

   ![FileVault 設定](./media/encrypt-devices-filevault/filevault-settings.png)

5. 針對 [FileVault]，選取 [啟用]。

6. 針對 [修復金鑰類型]，只支援 [個人金鑰]。

   請考慮新增一則訊息來協助引導使用者擷取其裝置的修復金鑰。 當您使用個人修復金鑰輪替的設定時，這項資訊對您的使用者會很有幫助，其可以自動為裝置定期產生新的修復金鑰。

   例如：若要擷取遺失或最近輪替的修復金鑰，請從任何裝置登入 Intune 公司入口網站。 在入口網站中，前往 [裝置] 並選取已啟用 FileVault 的裝置，然後選取 [取得修復金鑰]。 目前的修復金鑰會隨即顯示。

7. 完成其餘 [FileVault 設定](endpoint-protection-macos.md#filevault)以符合您的商務需求，然後選取 [確定]。

8. 完成其他組態設定，然後儲存設定檔。

## <a name="manage-filevault"></a>管理 FileVault

若要檢視接收 FileVault 原則的裝置相關資訊，請參閱[監視磁碟加密](../protect/encryption-monitor.md)。

當 Intune 第一次使用 FileVault 加密 macOS 裝置時，會建立個人修復金鑰。 加密後，裝置只會向裝置使用者顯示一次個人金鑰。

針對受控裝置，Intune 可以委付個人修復金鑰的複本。 金鑰委付可讓 Intune 管理員輪替金鑰以協助保護裝置，並讓使用者復原遺失或輪替的個人修復金鑰。

在 Intune 使用 FileVault 來加密 macOS 裝置後：

- 系統管理員可以使用 Intune 加密報告來檢視及管理 FileVault 修復金鑰。
- 使用者可以在裝置上從 Web 公司入口網站檢視裝置的個人修復金鑰。 從 Web 公司入口網站內，選擇已加密的 macOS 裝置，然後選擇 [取得修復金鑰] 作為遠端裝置動作。

> [!IMPORTANT]
> 由使用者 (而非 Intune) 加密的裝置無法由 Intune 管理。 這表示 Intune 無法委付這些裝置的個人修復，也無法管理修復金鑰的輪替。 使用者必須先解密其裝置，再讓 Intune 加密裝置，Intune 才能管理 FileVault 和裝置的修復金鑰。

### <a name="retrieve-personal-recovery-key"></a>擷取個人修復金鑰

針對由 Intune 加密的 macOS 裝置，終端使用者可以使用 iOS 公司入口網站應用程式、Android 公司入口網站應用程式，或透過 Android Intune 應用程式，擷取其個人修復金鑰 (FileVault 金鑰)。

具有個人修復金鑰的裝置必須向 Intune 註冊，並透過 Intune 以 FileVault 加密。 使用 iOS 公司入口網站應用程式、Android 公司入口網站應用程式、Android Intune 應用程式或公司入口網站網站，使用者就可以看到存取其 Mac 裝置所需的 **FileVault** 復原金鑰。

裝置使用者可以選取 [裝置] > *已加密且已註冊的 macOS 裝置* > [取得修復金鑰]。 瀏覽器將會顯示 Web 公司入口網站並顯示修復金鑰。

### <a name="rotate-recovery-keys"></a>輪替修復金鑰

Intune 支援輪替和復原個人修復金鑰的多個選項。 輪替金鑰的一個原因是如果目前的個人金鑰遺失，或者認為有風險。

- **自動輪替**：身為管理員，您可以將 FileVault 設定中的 [個人修復金鑰輪替] 設定為自動定期產生新的修復金鑰。 為裝置產生新的金鑰之後，並不會向使用者顯示該金鑰。 相反地，使用者必須向管理員或使用公司入口網站應用程式取得金鑰。

- **手動輪替**：身為管理員，您可以檢視以 Intune 管理並以 FileVault 加密之裝置的資訊。 然後，您可以選擇手動輪替公司裝置的修復金鑰。 您無法輪替個人裝置的修復金鑰。

  若要輪替修復金鑰：

  1. 登入 [Microsoft Endpoint Manager 系統管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)。

  2. 選取 [裝置] > [所有裝置]。

  3. 從裝置清單中選取您想要輪替其金鑰的加密裝置。 然後在 [監視] 下選取 [ **修復金鑰**]。
  
  4. 在 [修復金鑰] 窗格中，選取 [輪替 FileVault 修復金鑰]。

     下一次裝置使用 Intune 簽入時，即會輪替個人金鑰。 如有需要，使用者可以透過公司入口網站取得新的金鑰。

### <a name="recover-recovery-keys"></a>復原修復金鑰

- **管理員**：管理員無法檢視 FileVault 加密裝置的個人修復金鑰。

- **終端使用者**：終端使用者可以從任何裝置使用公司入口網站來檢視其任何受控裝置的目前個人修復金鑰。 您無法從公司入口網站應用程式檢視修復金鑰。

  若要檢視修復金鑰：
  
  1. 從任何裝置登入「Intune 公司入口網站」網站。

  2. 在入口網站中，移至 [裝置]，然後選取使用 FileVault 加密的 macOS 裝置。

  3. 選取 [取得修復金鑰]。 目前的修復金鑰會隨即顯示。

## <a name="next-steps"></a>後續步驟

[管理 BitLocker 原則](../protect/encrypt-devices.md)

[監視磁碟加密](../protect/encryption-monitor.md)
