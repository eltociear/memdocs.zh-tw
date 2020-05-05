---
title: 如何大量註冊裝置
titleSuffix: Configuration Manager
description: 使用 Configuration Manager 中的內部部署行動裝置管理（MDM），以自動化方式大量註冊裝置。
ms.date: 01/13/2020
ms.prod: configuration-manager
ms.technology: configmgr-mdm
ms.topic: conceptual
ms.assetid: b36f5e4a-2b57-4d18-83f6-197081ac2a0a
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: bfe2d395187f8af86e2d09156a45f7398a5bc670
ms.sourcegitcommit: 578ad1e8088f7065b565e8a4f4619f5a26b94001
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81724612"
---
# <a name="how-to-bulk-enroll-devices-with-on-premises-mdm-in-configuration-manager"></a>如何在 Configuration Manager 中使用內部部署 MDM 大量註冊裝置

適用於：  Configuration Manager (最新分支)

Configuration Manager 內部部署行動裝置管理（MDM）中的大量註冊是註冊裝置的自動化方法。 另一個方法是「使用者註冊」，這會要求使用者輸入其認證以註冊裝置。 大量註冊使用註冊套件在註冊期間驗證裝置。 套件是一個 ppkg 檔案，它也可以包含憑證和 Wi-fi 設定檔，以支援註冊。

## <a name="create-a-certificate-profile"></a><a name="bkmk_createCert"></a> 建立憑證設定檔

包含憑證設定檔，以在裝置上自動安裝受信任的根憑證。 在裝置與內部部署 MDM 所需的網站系統角色之間進行信任通訊時，需要此根憑證。

當您準備內部部署 MDM 的網站時，您會匯出受信任的根憑證。 在註冊套件的憑證設定檔中使用此憑證。 如需如何取得受信任根憑證的詳細資訊，請參閱[匯出受信任的根憑證](../get-started/set-up-certificates-on-premises-mdm.md#bkmk_exportCert)。

使用匯出的憑證來建立憑證設定檔。 如需詳細資訊，請參閱[如何建立憑證設定檔](../../protect/deploy-use/create-certificate-profiles.md)。

## <a name="create-a-wi-fi-profile"></a><a name="CreateWifi"></a> 建立 Wi-Fi 設定檔

大量註冊套件的另一個元件是 Wi-fi 設定檔。 此設定檔可確保裝置具有可支援註冊的網路連線能力。

如需有關如何在 Configuration Manager 中建立 Wi-fi 設定檔的詳細資訊，請參閱[如何建立 wi-fi 設定檔](../../protect/deploy-use/create-wifi-profiles.md)。

### <a name="wi-fi-profile-limitations"></a>Wi-fi 設定檔限制

當您建立用於內部部署 MDM 大量註冊的 Wi-fi 設定檔時，請參閱下列限制。

#### <a name="wi-fi-security-configurations-for-on-premises-mdm"></a>適用于內部部署 MDM 的 wi-fi 安全性設定

Configuration Manager 的最新分支只支援下列適用于內部部署 MDM 的 Wi-fi 安全性設定：

- 安全性類型： **WPA2 Enterprise** 或 **WPA2 Personal**

- 加密類型： **AES** 或 **TKIP**

- EAP 類型： **智慧卡或其他憑證** 或 **PEAP**

#### <a name="proxy-server"></a>Proxy 伺服器

雖然 Configuration Manager 在 Wi-fi 設定檔中有 proxy 伺服器資訊的設定，但它不會在裝置註冊時設定 proxy。 如果您需要在大量註冊的裝置上設定 proxy 伺服器：

- 在裝置註冊之後，使用設定專案部署設定。

- 使用 Windows 映像和設定設計工具（ICD）建立第二個套件，然後將它與大量註冊套件一起部署。

## <a name="create-an-enrollment-profile"></a><a name="bkmk_createEnroll"></a> 建立註冊設定檔

註冊設定檔可讓您指定裝置註冊所需的設定。 這些設定包括[憑證設定檔](#bkmk_createCert)和[wi-fi 設定檔](#CreateWifi)。

1. 在 Configuration Manager 主控台中，移至 [**資產與相容性**] 工作區，展開 [**所有公司擁有的裝置**]，展開 [ **Windows**]，然後選取 [**註冊設定檔**] 節點。

1. 在功能區中，選取 [**建立註冊設定檔**]。

1. 在 [建立註冊設定檔] 的 [**一般**] 頁面上，指定下列資訊：

    - **名稱**：用來識別設定檔的唯一名稱

    - **描述**：可進一步描述設定檔的選擇性欄位

    - **管理授權**單位：只選取 [內部**部署**]

1. 在 [**網站指派**] 頁面上，選取 [使用裝置管理點的**管理網站碼**]。

1. 在 [**選取註冊 Proxy 點**] 頁面上，選取 [**僅限內部**網路]，然後選取一個或多個註冊 Proxy 點。 裝置會使用這些伺服器來啟動註冊程式。

1. 在 [**選取受信任的根憑證**] 頁面上，選取包含受信任根憑證的憑證設定檔。

1. 在 [ **wi-fi 設定檔**] 頁面上，選取包含裝置要連線之必要網路設定的 wi-fi 設定檔。

    > [!TIP]
    > 如果您的註冊套件不使用 Wi-fi 設定檔，請略過此步驟。

1. 完成精靈。

## <a name="create-an-enrollment-package"></a><a name="bkmk_createPpkg"></a>建立註冊套件

註冊套件（ppkg）是您用來為內部部署 MDM 大量註冊裝置的檔案。 使用 Configuration Manager 建立此檔案。 雖然您可以使用 Windows ICD 建立類似類型的套件，但只有您在 Configuration Manager 中建立的套件可以用來為內部部署 MDM 註冊裝置。 您使用 Windows ICD 建立的套件只能提供註冊所需的使用者主要名稱（UPN），而無法啟動實際的註冊程式。

在 Windows 10 建立註冊套件的程序需要 Windows 評定及部署工具套件 (ADK)。 在執行 Configuration Manager 主控台的電腦上，安裝最新版的 Windows ADK。 選取 [**映射和設定設計工具（ICD）** ] 功能和任何相依性。 （此版本不需要符合 Configuration Manager 網站用於 OS 部署的版本。）如需詳細資訊，請參閱[下載適用于 windows 10 的 WINDOWS ADK](https://docs.microsoft.com/windows-hardware/get-started/adk-install)。

1. 在 Configuration Manager 主控台中，移至 [**資產與相容性**] 工作區，展開 [**所有公司擁有的裝置**]，展開 [ **Windows**]，然後選取 [**註冊設定檔**] 節點。

1. 選取現有的註冊設定檔。 在功能區中，選取 [**匯出**]。

1. 在 [匯出註冊套件] 視窗中，指定下列資訊：

    - **有效期間（天）**：根據預設，Configuration Manager 會將註冊套件設定為在兩周內過期（14天）。 在有效期間到期後，您就無法使用套件進行裝置註冊。 請輸入介於1到30之間的整數。

    - **封裝**檔案：指定 ppkg 檔案的本機或網路檔案路徑和名稱。

    - **加密套件**：啟用此選項可保護封裝的密碼。 匯出封裝之後，Configuration Manager 會顯示產生的密碼。 將密碼複製並儲存在安全的位置。 您無法在沒有密碼的情況下使用匯出的註冊套件。

        > [!IMPORTANT]
        > Configuration Manager 不會儲存密碼，而且您無法加以自訂或變更。 一旦您關閉顯示密碼的視窗，就無法取得密碼。

1. 選取 [匯出]  。 Configuration Manager 會使用 Windows ADK 來建立註冊套件。

Configuration Manager 會持續追蹤有效的註冊套件。 在主控台中，展開 [**註冊設定檔**] 節點，然後選取 [**匯出的封裝**]。

> [!TIP]
> 如果您從 Configuration Manager 主控台移除註冊套件，就無法使用它來註冊裝置。 使用此方法來管理您不想讓其他人用來進行大量註冊的註冊套件。

## <a name="bulk-enroll-a-device"></a><a name="bkmk_getPpkg"></a>大量註冊裝置

您可以在裝置的全新體驗（OOBE）程式之前或之後，使用套件來註冊裝置。 註冊套件也可以包含為原始設備製造商（OEM）布建套件的一部分。

若要使用大量註冊的封裝，您必須實際將它傳遞至裝置。 視您的需求而定，有各種不同的方法，例如：

- 從檔案系統複製

- 附加至電子郵件

- 跨近距離無線通訊（NFC）連線複製

- 從記憶卡複製

- 掃描條碼

- 從有行動網卡的裝置複製

- 包含在 OEM 布建套件中

### <a name="enroll-a-device-with-bulk-enrollment-package"></a>使用大量註冊套件註冊裝置

1. 在裝置上，開啟 ppkg 檔案。 如有必要，請以系統管理員身分執行。

1. Windows 詢問封裝是否來自信任的來源，請選取 **[是]**。

註冊程式隨即啟動。

## <a name="verify-enrollment"></a><a name="bkmk_verifyEnroll"></a>確認註冊

### <a name="verify-bulk-enrollment-on-the-device"></a>確認裝置上的大量註冊

1. 在裝置上開啟 [**設定**]。

1. 選取 [**帳戶**]，然後選取 [**存取公司或學校**]。 註冊成功時，您會在 [ **[]**] 下看到一個帳戶。

1. 選取帳戶，然後選取 [**同步**處理]。此動作會開始使用 Configuration Manager 進行管理。

### <a name="verify-enrollment-in-the-console"></a>驗證主控台中的註冊

使用 Configuration Manager 主控台確認已成功註冊裝置。 在 Configuration Manager 主控台中，移至 [資產與合規性]**** 工作區，然後選取 [裝置]****。 流覽或搜尋裝置清單中已註冊的裝置。
