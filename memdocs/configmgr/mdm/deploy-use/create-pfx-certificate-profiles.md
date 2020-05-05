---
title: 建立 PFX 憑證設定檔
titleSuffix: Configuration Manager
description: 瞭解如何在 Configuration Manager 中使用 PFX 檔案，以產生支援加密資料交換的使用者特定憑證。
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: d240a836-c49b-49ab-a920-784c062d6748
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: b45474484629b437f2548fb375075cfe55275ee2
ms.sourcegitcommit: 578ad1e8088f7065b565e8a4f4619f5a26b94001
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81724572"
---
# <a name="create-pfx-certificate-profiles-using-a-certificate-authority"></a>使用憑證授權單位建立 PFX 憑證設定檔

適用於：  Configuration Manager (最新分支)

瞭解如何建立憑證設定檔，以使用認證的憑證授權單位單位。 本文將重點放在關於個人資訊交換（PFX）憑證設定檔的特定資訊。 如需有關如何建立及設定這些設定檔的詳細資訊，請參閱[憑證設定檔](../../protect/deploy-use/introduction-to-certificate-profiles.md)。

Configuration Manager 可讓您使用憑證授權單位單位所發行的認證來建立 PFX 憑證設定檔。 您可以選擇 [Microsoft] 或 [Entrust] 作為您的憑證授權單位單位。 部署到使用者裝置時，PFX 檔案會產生使用者特定憑證，以支援加密的資料交換。

若要從現有的憑證檔案匯入憑證認證，請參閱匯[入 PFX 憑證設定檔](import-pfx-certificate-profiles.md)。

## <a name="prerequisites"></a>先決條件

在您開始建立憑證設定檔之前，請先確定必要的必要條件已就緒。 如需詳細資訊，請參閱[憑證設定檔的必要條件](../../protect/plan-design/prerequisites-for-certificate-profiles.md)。 例如，針對 PFX 憑證設定檔，您需要[憑證登錄點](../../protect/deploy-use/certificate-infrastructure.md#step-2---install-and-configure-the-certificate-registration-point)網站系統角色。

## <a name="create-a-profile"></a>建立設定檔  

1. 在 Configuration Manager 主控台中，移至 [**資產與相容性**] 工作區，展開 [**相容性設定**]，展開 [**公司資源存取**]，然後選取 [**憑證設定檔**]。

1. 在功能區 [常用]**** 索引標籤的 [建立]**** 群組中，選取 [建立憑證設定檔]****。

1. 在 [**建立憑證設定檔]** 的 [**一般**] 頁面上，指定下列資訊：  

    - **名稱**：輸入憑證設定檔的唯一名稱。 您最多可以使用 256 個字元。  

    - **描述**：提供可協助您在 Configuration Manager 主控台中識別憑證設定檔的說明。 您最多可以使用 256 個字元。  

1. 選取 [**個人資訊交換-PKCS #12 （PFX）設定-建立**]。 此選項會代表使用者從已連線的內部部署憑證授權單位單位（CA）要求憑證。 選擇您的憑證授權單位單位： **Microsoft**或**Entrust Datacard**。

    > [!NOTE]
    > [匯**入**] 選項會從現有憑證取得資訊，以建立憑證設定檔。 如需詳細資訊，請參閱[匯入 PFX 憑證設定檔](import-pfx-certificate-profiles.md)。

1. 在 [**支援的平臺**] 頁面上，選取此憑證設定檔支援的作業系統版本。 如需您的 Configuration Manager 版本所支援作業系統版本的詳細資訊，請參閱[支援的用戶端和裝置作業系統版本](../../core/plan-design/configs/supported-operating-systems-for-clients-and-devices.md)。

1. 在 [**憑證授權單位**單位] 頁面上，選擇要處理 PFX 憑證的憑證登錄點（CRP）：

    1. **主要網站**：選擇包含 CA 之 CRP 角色的伺服器。
    1. **憑證授權單位**單位：選取相關的 CA。

    如需詳細資訊，請參閱[憑證基礎結構](../../protect/deploy-use/certificate-infrastructure.md)。

[ **PFX 憑證**] 頁面上的設定會視 [**一般**] 頁面上選取的 CA 而有所不同：

- [Microsoft CA](#bkmk_microsoft)
- [Entrust Datacard CA](#bkmk_entrust)

### <a name="configure-pfx-certificate-settings-for-microsoft-ca"></a><a name="bkmk_microsoft"></a>設定 Microsoft CA 的**PFX 憑證**設定

1. 在 [**憑證範本名稱**] 中，選擇 [憑證範本]。

1. 若要使用憑證設定檔進行 S/MIME 簽署或加密，請啟用**憑證使用**方式。

    當您啟用此選項時，它會將與目標使用者相關聯的所有 PFX 憑證，傳遞至其所有裝置。 如果您未啟用此選項，每個裝置都會收到唯一的憑證。  

1. 將 [主體名稱格式]**** 設為 [一般名稱]**** 或 [完整的辨別名稱]****。 如果您不確定要使用哪一個，請洽詢您的 CA 系統管理員。

1. 針對 [**主體別名**]，視需要為您的 CA 啟用 [**電子郵件地址**] 和 **[使用者主體名稱（UPN）** ]。

1. **更新閾值**：根據到期前的剩餘時間百分比，決定是否自動更新憑證。

1. 將 [憑證有效期間]**** 設為憑證的存留期。

1. 當憑證登錄點指定 Active Directory 認證時，請啟用**Active Directory 發佈**。

1. 如果您已選取一或多個 Windows 10 支援的平臺：

    1. 將 [ **Windows 憑證存放區**] 設定為 [**使用者**]。 （[**本機電腦**] 選項不會部署憑證，因此請不要加以選擇）。

    1. 選取下列其中一個**金鑰儲存提供者（KSP）**：

        - **安裝至信賴平台模組 (TPM) (若存在)**  
        - **安裝至信賴平臺模組（TPM）否則會失敗**
        - **安裝至 Windows Hello 企業版否則會失敗**
        - **安裝至軟體金鑰儲存提供者**

1. 完成精靈。

### <a name="configure-pfx-certificate-settings-for-entrust-datacard-ca"></a><a name="bkmk_entrust"></a>設定 Entrust Datacard CA 的**PFX 憑證**設定

1. 針對 [**數位識別碼**設定]，選擇 [設定設定檔]。 Entrust 系統管理員會建立數位識別碼設定選項。

1. 若要使用憑證設定檔進行 S/MIME 簽署或加密，請啟用**憑證使用**方式。

    當您啟用此選項時，它會將與目標使用者相關聯的所有 PFX 憑證，傳遞至其所有裝置。 如果您未啟用此選項，每個裝置都會收到唯一的憑證。  

1. 若要將 Entrust 的**主體名稱格式**標記對應至 Configuration Manager 欄位，請選取 [**格式**]。

    [憑證名稱格式]**** 對話方塊會列出 Entrust 數位識別碼設定變數。 針對每個 Entrust 變數，選擇適當的 Configuration Manager 欄位。

1. 若要將 Entrust**主體別名**權杖對應至支援的 LDAP 變數，請選取 [**格式**]。

    [憑證名稱格式]**** 對話方塊會列出 Entrust 數位識別碼設定變數。 針對每個 Entrust 變數，選擇適當的 LDAP 變數。

1. **更新閾值**：根據到期前的剩餘時間百分比，決定是否自動更新憑證。

1. 將 [憑證有效期間]**** 設為憑證的存留期。

1. 當憑證登錄點指定 Active Directory 認證時，請啟用**Active Directory 發佈**。

1. 如果您已選取一或多個 Windows 10 支援的平臺：

    1. 將 [ **Windows 憑證存放區**] 設定為 [**使用者**]。 （[**本機電腦**] 選項不會部署憑證，因此請不要加以選擇）。

    1. 選取下列其中一個**金鑰儲存提供者（KSP）**：

        - **安裝至信賴平台模組 (TPM) (若存在)**  
        - **安裝至信賴平臺模組（TPM）否則會失敗**
        - **安裝至 Windows Hello 企業版否則會失敗**
        - **安裝至軟體金鑰儲存提供者**

1. 完成精靈。

## <a name="deploy-the-profile"></a>部署設定檔

建立憑證設定檔之後，它現在可以在 [**憑證設定檔**] 節點中使用。 如需有關如何部署它的詳細資訊，請參閱[部署資源存取設定檔](../../protect/deploy-use/deploy-wifi-vpn-email-cert-profiles.md)。

## <a name="see-also"></a>請參閱

[建立新的憑證設定檔](../../protect/deploy-use/create-certificate-profiles.md)

[匯入 PFX 憑證設定檔](import-pfx-certificate-profiles.md)

[部署 Wi-Fi、VPN、電子郵件和憑證設定檔](../../protect/deploy-use/deploy-wifi-vpn-email-cert-profiles.md)
