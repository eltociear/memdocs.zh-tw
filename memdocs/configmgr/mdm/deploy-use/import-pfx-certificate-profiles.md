---
title: 匯入 PFX 憑證設定檔
titleSuffix: Configuration Manager
description: 瞭解如何在 Configuration Manager 中使用 PFX 檔案，以產生支援加密資料交換的使用者特定憑證。
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: e3bb3e13-3037-4122-93bc-504bfd080a4d
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 7f72dcba7e7f1e3af0bf168ca83deb958094879a
ms.sourcegitcommit: 578ad1e8088f7065b565e8a4f4619f5a26b94001
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81724592"
---
# <a name="import-pfx-certificate-profiles"></a>匯入 PFX 憑證設定檔

適用於：  Configuration Manager (最新分支)

瞭解如何從外部憑證匯入認證來建立憑證設定檔。 本文將重點放在關於個人資訊交換（PFX）憑證設定檔的特定資訊。 如需有關如何建立及設定這些設定檔的詳細資訊，請參閱[憑證設定檔](../../protect/deploy-use/introduction-to-certificate-profiles.md)。

Configuration Manager 針對不同的裝置和作業系統版本支援不同類型的憑證存放區。 例如，Windows 10 和 Windows 10 Mobile。 如需詳細資訊，請參閱[憑證設定檔必要條件](../../protect/plan-design/prerequisites-for-certificate-profiles.md)。

使用 Configuration Manager 匯入憑證認證，然後將 PFX 檔案布建到裝置。 您可以使用這些檔案來產生使用者特定憑證，以支援加密的資料交換。

> [!TIP]  
> 如需此程式的逐步解說，請參閱[建立和部署 PFX 憑證設定檔 Configuration Manager 中](https://blogs.technet.microsoft.com/karanrustagi/2015/09/01/how-to-create-and-deploy-pfx-certificate-profiles-in-configuration-manager/)的 blog 文章。  

## <a name="create-a-profile"></a>建立設定檔

1. 在 Configuration Manager 主控台中，移至 [**資產與相容性**] 工作區，展開 [**相容性設定**]，展開 [**公司資源存取**]，然後選取 [**憑證設定檔**]。

1. 在功能區 [常用]**** 索引標籤的 [建立]**** 群組中，選取 [建立憑證設定檔]****。

1. 在 [**建立憑證設定檔]** 的 [**一般**] 頁面上，指定下列資訊：  

    - **名稱**：輸入憑證設定檔的唯一名稱。 您最多可以使用 256 個字元。  

    - **描述**：提供可協助您在 Configuration Manager 主控台中識別憑證設定檔的說明。 您最多可以使用 256 個字元。  

1. 選取 [**個人資訊交換-PKCS #12 （PFX）設定-匯入**]。 此選項會從現有憑證匯入資訊，以建立憑證設定檔。

    > [!NOTE]
    > [**建立**] 選項會代表使用者從已連線的內部部署憑證授權單位單位（CA）要求憑證。 此程式接著會安全地將憑證以 PFX 檔案形式傳遞給用戶端。 如需詳細資訊，請參閱[使用憑證授權單位單位建立 PFX 憑證設定檔](create-pfx-certificate-profiles.md)。

1. 在 [**建立憑證設定檔]** 的 [ **PFX 憑證**] 頁面上，指定裝置金鑰儲存提供者（KSP）：

    - **安裝至信賴平台模組 (TPM) (若存在)**  
    - **安裝至信賴平臺模組（TPM）否則會失敗**
    - **安裝至 Windows Hello 企業版否則會失敗**
    - **安裝至軟體金鑰儲存提供者**

1. 在 [**支援的平臺**] 頁面上，選擇支援的裝置平臺。

1. 完成精靈。

## <a name="deploy-the-profile"></a>部署設定檔

建立並布建憑證設定檔之後，它現在會出現在 [**憑證設定檔**] 節點中。 如需有關如何部署它的詳細資訊，請參閱[部署資源存取設定檔](../../protect/deploy-use/deploy-wifi-vpn-email-cert-profiles.md)。

## <a name="assign-primary-users"></a>指派主要使用者

在您需要安裝 PFX 憑證的 Windows 10 裝置上，將目標使用者指派為主要使用者。 如需詳細資訊，請參閱[使用者裝置親和性](../../apps/deploy-use/link-users-and-devices-with-user-device-affinity.md)。

## <a name="provision-a-create-pfx-script"></a>布建建立 PFX 腳本

若要匯入 PFX 憑證，請使用下列 Configuration Manager PowerShell Cmdlet 來布建「建立 PFX」腳本：

- [CMClientCertificatePfx](https://docs.microsoft.com/powershell/module/configurationmanager/get-cmclientcertificatepfx?view=sccm-ps)
- [匯入-CMClientCertificatePfx](https://docs.microsoft.com/powershell/module/configurationmanager/import-cmclientcertificatepfx?view=sccm-ps)
- [移除-CMClientCertificatePfx](https://docs.microsoft.com/powershell/module/configurationmanager/remove-cmclientcertificatepfx?view=sccm-ps)

### <a name="example-script"></a>範例指令碼

若要將 PFX 檔案布建到使用者的憑證設定檔，請在具有 Configuration Manager 主控台的電腦上開啟 PowerShell。 使用您環境中的值來變更變數。

``` PowerShell
# The display name of your PFX Import certificate profile
$PfxProfileDisplayName = "ImportPFX"

# The password you used to protect/encrypt the external PFX file that was created/exported from your certificate storage provider
# If you omit this password, PowerShell will securely prompt you for it. You can specify it as a parameter for process automation.
$password = ""

# The username of the user who will receive this PFX certificate on their device
$user = "Melissa"

# The full path to the PFX file you exported from the certificate store
$pfxfile = "c:\p1.pfx"

# If the target user isn't in the same domain as the user running this script, specify a different domain
Import-CMClientCertificatePfx -UserName "$env:USERDOMAIN\$user" -Password (ConvertTo-SecureString -String $password -AsPlainText -Force) -CertificateProfilePfx (Get-CMCertificateProfilePfx -Fast -Name $PfxProfileDisplayName) -Path $pfxfile
```

## <a name="see-also"></a>請參閱

[建立新的憑證設定檔](../../protect/deploy-use/create-certificate-profiles.md)

[使用憑證授權單位建立 PFX 憑證設定檔](create-pfx-certificate-profiles.md)

[部署 Wi-Fi、VPN、電子郵件和憑證設定檔](../../protect/deploy-use/deploy-wifi-vpn-email-cert-profiles.md)
