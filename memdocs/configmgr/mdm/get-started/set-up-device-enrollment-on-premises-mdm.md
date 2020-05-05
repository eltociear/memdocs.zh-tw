---
title: 設定內部部署 MDM 的註冊
titleSuffix: Configuration Manager
description: 授與使用者在 Configuration Manager 中註冊其裝置以進行內部部署行動裝置管理（MDM）的許可權。
ms.date: 01/09/2020
ms.prod: configuration-manager
ms.technology: configmgr-mdm
ms.topic: conceptual
ms.assetid: 9ffaea91-1379-4b86-9953-b25e152f56a9
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 5c8213fac603d69e0f2afd31631e61ad301090f6
ms.sourcegitcommit: 578ad1e8088f7065b565e8a4f4619f5a26b94001
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81724682"
---
# <a name="set-up-device-enrollment-for-on-premises-mdm-in-configuration-manager"></a>在 Configuration Manager 中設定內部部署 MDM 的裝置註冊

適用於：  Configuration Manager (最新分支)

設定內部部署行動裝置管理（MDM）的最後一個步驟是讓使用者註冊其裝置。 使用 Configuration Manager 的用戶端設定，授與使用者在內部部署 MDM 中註冊裝置的許可權。

## <a name="create-an-enrollment-profile"></a><a name="bkmk_createProf"></a> 建立註冊設定檔

若要推送允許使用者註冊行動裝置所需的設定，請將新的註冊設定檔新增至預設用戶端設定。 此設定檔會套用至 Configuration Manager 網站中的所有使用者。

> [!NOTE]
> 此程式會使用**預設用戶端設定**，這會自動套用至所有裝置和使用者。 或者，您可以建立自訂用戶端設定，然後部署至您選擇的集合。 這個替代方法需要至少兩個自訂用戶端設定，一個用於*裝置*設定，另一個用於*使用者*設定。 如需詳細資訊，請參閱[如何設定用戶端設定](../../core/clients/deploy/configure-client-settings.md)。

1. 在 Configuration Manager 主控台中，移至 [系統**管理**] 工作區，然後選取 [**用戶端設定**] 節點。 開啟 [**預設用戶端設定**]，然後選取 [**註冊**] 群組。

1. 在 [裝置設定] 下，指定**新式裝置的輪詢間隔（分鐘）**。 根據預設，此間隔為60分鐘。

1. 在 [使用者設定] 下，啟用 [**允許使用者註冊新式裝置**] 選項。

1. 針對**新式裝置註冊設定檔**，請選取 [**設定設定檔**]。 在 [註冊設定檔] 視窗中，選取 [**建立**]。

1. 在 [建立註冊設定檔] 視窗中，指定下列資訊：

    - 註冊設定檔的唯一描述性**名稱**。

    - 選擇性的**描述**，以提供設定檔的其他相關資訊。

    - 選擇包含裝置管理點的 [**管理網站] 代碼**。 選取 **[確定]** 以儲存並關閉。

## <a name="configure-additional-client-settings"></a><a name="bkmk_addClient"></a>設定其他用戶端設定

在註冊裝置之後，還有其他用戶端設定可進行設定。 如需更多一般資訊，請參閱[如何設定用戶端設定](../../core/clients/deploy/configure-client-settings.md)。

Configuration Manager 支援下列適用于內部部署 MDM 的用戶端設定：

- **用戶端原則**：這些設定會指定下載用戶端原則到裝置的頻率。 您也可以啟用使用者原則的設定。 如需詳細資訊，請參閱[關於用戶端設定-用戶端原則](../../core/clients/deploy/about-client-settings.md#client-policy)。

- **軟體部署**：設定評估軟體部署的間隔。 如需詳細資訊，請參閱[關於用戶端設定-軟體部署](../../core/clients/deploy/about-client-settings.md#software-deployment)。

    > [!NOTE]
    > 針對內部部署 MDM，軟體部署設定只能用來做為預設用戶端設定。

## <a name="discover-users"></a><a name="bkmk_enableUsers"></a>探索使用者

若要讓使用者使用內部部署 MDM 的註冊設定檔來接收用戶端設定，網站會在 Active Directory 中探索他們的使用者帳戶。 為確保每個需要註冊設定檔的使用者皆可取得它，請執行 Active Directory 使用者探索。 如需詳細資訊，請參閱[Active Directory 使用者探索](../../core/servers/deploy/configure/about-discovery-methods.md#bkmk_aboutUser)。

## <a name="install-the-trusted-root-certificate"></a><a name="bkmk_storeCert"></a>安裝受信任的根憑證

已加入網域的裝置會取得信任的根憑證，以便與裝載網站系統角色的伺服器進行受信任的通訊。 Active Directory 憑證服務會自動散發受信任的根憑證。 未加入網域的電腦和行動裝置需要透過其他方式安裝此憑證，以允許註冊。

> [!NOTE]
> 如果 web 伺服器憑證是由公開憑證授權單位單位所發行，大部分的裝置都已經信任這些 Ca。 如果您的設計包括使用其中一個公用 Ca，則不需要執行此步驟。

[匯出受信任的根憑證](set-up-certificates-on-premises-mdm.md#bkmk_exportCert)之後，您必須將它安裝在需要註冊的裝置上。 例如，未加入網域，且無法從 Active Directory 自動取得的裝置。 您所使用的程式將視下列因素而定：

- 特定裝置類型和技術功能
- OS 版本
- 您的商務、安全性和使用者經驗需求

下列清單包含一些在裝置上傳遞和安裝受信任的根憑證的範例方法：

- 檔案共用

- 電子郵件附件

- 記憶卡

- 行動網卡

- 雲端存放裝置 (例如 OneDrive)

- 近距離無線通訊 (NFC) 連線

- 條碼掃描器

- 全新體驗 (OOBE) 佈建套件

### <a name="manually-install-the-trusted-root-certificate-in-windows"></a>在 Windows 中手動安裝受信任的根憑證

1. 在要註冊的裝置上，在 [檔案瀏覽器] 中流覽至受信任的根憑證檔案（.cer），然後將它**開啟**。

1. 在 [憑證] 視窗中，選取 [**安裝憑證**]。

1. 在 [憑證匯入嚮導] 中，選取 [**本機電腦**]，然後選取 **[下一步]** 以系統管理員身分繼續。

1. 在 [憑證存放區] 頁面上，選取 **[將所有憑證放入下列存放區**]，然後選取 **[流覽]**。

1. 在 [選取證書存儲] 視窗中，選取 [**信任的根憑證授權**單位]，然後選取 **[確定]**。

1. 完成和 wizard。

## <a name="next-step"></a>後續步驟

> [!div class="nextstepaction"]
> [註冊裝置](../deploy-use/enroll-devices-on-premises-mdm.md)
