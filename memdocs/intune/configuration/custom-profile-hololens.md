---
title: 在 Microsoft Intune 中的 HoloLens 2 裝置上使用 Windows Defender 應用程式控制 - Azure | Microsoft Docs
description: 設定 Windows Defender 應用程式控制 (WDAC) CSP，以在 Microsoft Intune 中的 HoloLens 2 裝置上，允許或封鎖開啟應用程式。 使用 PowerShell 和自訂的組態設定檔。
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 05/20/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 6d2d19b03253725bde7b0ee27f3c94b42adb5917
ms.sourcegitcommit: 302556d3b03f1a4eb9a5a9ce6138b8119d901575
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/27/2020
ms.locfileid: "83990122"
---
# <a name="use-wdac-and-windows-powershell-to-allow-or-blocks-apps-on-hololens-2-devices-with-microsoft-intune"></a>使用 WDAC 和 Windows PowerShell 在使用 Microsoft Intune 的 HoloLens 2 裝置上允許或封鎖應用程式

Microsoft HoloLens 2 裝置支援 [Windows Defender 應用程式控制 (WDAC) CSP](https://docs.microsoft.com/windows/client-management/mdm/applicationcontrol-csp)，這會取代 [AppLocker CSP](https://docs.microsoft.com/windows/client-management/mdm/applocker-csp) (機器翻譯)。

使用 Windows PowerShell 和 Microsoft Intune，您就可以使用 WDAC CSP 在 Microsoft HoloLens 2 裝置上允許或封鎖開啟特定的應用程式。 例如，您可能想要在您組織中的 HoloLens 2 裝置上，允許或阻止開啟 Cortana 應用程式。

本功能適用於：

- 執行 Windows Holographic for Business 的 HoloLens 2 裝置

WDAC CSP 是以 [Windows Defender 應用程式控制 (WDAC) 功能](https://docs.microsoft.com/windows/security/threat-protection/windows-defender-application-control/windows-defender-application-control)為基礎。 您也可以[使用多個 WDAC 原則](https://docs.microsoft.com/windows/security/threat-protection/windows-defender-application-control/deploy-multiple-windows-defender-application-control-policies) (機器翻譯)。

本文將示範下列項目的作法：

1. 使用 Windows PowerShell 建立 WDAC 原則。
2. 使用 Windows PowerShell 將 WDAC 原則規則轉換成 XML、更新 XML，然後將 XML 轉換成二進位檔案。
3. 在 Microsoft Intune 中，建立[自訂裝置組態設定檔](custom-settings-windows-holographic.md)、新增此 WDAC 原則二進位檔案，然後將此原則套用至您的 HoloLens 2 裝置。

在 Intune 中，您必須建立自訂的組態設定檔，才能使用 Windows Defender 應用程式控制 (WDAC) CSP。 

使用本文中的步驟為範本，在 HoloLens 2 裝置上允許或拒絕開啟特定的應用程式。

## <a name="prerequisites"></a>先決條件

- 熟悉 Windows PowerShell。
- 以下列成員身分登入 Intune：

  - **原則和設定檔管理員**或 **Intune 角色系統管理員** 的 Intune 角色

    或

  - **全域管理員**或 **Intune 服務管理員**的 Azure AD 角色

  如需詳細資訊，請參閱[使用 Intune 的角色型存取控制 (RBAC)](../fundamentals/role-based-access-control.md)。

- 建立具有 HoloLens 2 裝置的使用者群組或裝置群組。 如需相關資訊，請參閱[使用者群組與裝置群組的比較](device-profile-assign.md#user-groups-vs-device-groups)。

## <a name="example"></a>範例

這個範例會使用 Windows PowerShell 建立 Windows Defender 應用程式控制 (WDAC) 原則。 原則會阻止開啟特定的應用程式。 然後，使用 Intune 將原則部署至 HoloLens 2 裝置。

1. 在您的桌上型電腦上，開啟 **Windows PowerShell** 應用程式。
2. 取得桌上型電腦上已安裝的應用程式套件相關資訊：

    ```powershell
    $package1 = Get-AppxPackage -name *<applicationname>*
    ```

    例如，輸入：

    ```powershell
    $package1 = Get-AppxPackage -name *cortana*
    ```

    接下來，確認套件具有應用程式屬性：

    ```powershell
    $package1
    ```

    您會看到類似下列應用程式詳細資料的屬性：

    ```powershell
    Name              : Microsoft.Windows.Cortana
    Publisher         : CN=Microsoft Windows, O=Microsoft Corporation, L=Redmond, S=Washington, C=US
    Architecture      : Neutral
    ResourceId        : neutral
    Version           : 1.13.0.18362
    PackageFullName   : Microsoft.Windows.Cortana_1.13.0.18362_neutral_neutral_cw5n1h2txyewy
    InstallLocation   : C:\Windows\SystemApps\Microsoft.Windows.Cortana_cw5n1h2txyewy
    IsFramework       : False
    PackageFamilyName : Microsoft.Windows.Cortana_cw5n1h2txyewy
    PublisherId       : cw5n1h2txyewy
    IsResourcePackage : False
    IsBundle          : False
    IsDevelopmentMode : False
    NonRemovable      : True
    IsPartiallyStaged : False
    SignatureKind     : System
    Status            : Ok
    ```

3. 建立 WDAC 原則，並將應用程式套件新增至「拒絕」規則：

    ```powershell
    $rule = New-CIPolicyRule -Package $package1 -Deny
    ```

4. 針對您想要拒絕的任何其他應用程式，重複步驟 2 和步驟 3：

    ```powershell
    $rule += New-CIPolicyRule -Package $package<2..n> -Deny
    ```

    例如，輸入：

    ```powershell
    $package2 = Get-AppxPackage -name *windowsstore*
    $rule += New-CIPolicyRule -Package $package<2..n>  -Deny
    ```

5. 將 WDAC 原則轉換成 **newPolicy.xml**：

    ```powershell
    New-CIPolicy -rules $rule -f .\newPolicy.xml -UserPEs
    ```

    若要以應用程式的所有版本為目標，請確定在 newPolicy.xml 中，`PackageVersion="65535.65535.65535.65535"` 位在 [拒絕] 節點中：

    ```xml
    <Deny ID="ID_DENY_D_1" FriendlyName="Microsoft.WindowsStore_8wekyb3d8bbwe FileRule" PackageFamilyName="Microsoft.WindowsStore_8wekyb3d8bbwe" PackageVersion="65535.65535.65535.65535" />
    ```

    您可以為 `PackageFamilyNameRules` 使用下列版本：

    - **允許**：輸入 `PackageVersion, 0.0.0.0`，這表示「允許此版本和更新版本」。
    - **拒絕**：輸入 `PackageVersion, 65535.65535.65535.65535`，這表示「拒絕此版本和較舊版本」。

6. 合併 **newPolicy.xml** 與您桌上型電腦中的預設原則。 此步驟會建立 **mergedPolicy.xml**。 例如，允許 Windows、WHQL 簽署的驅動程式，以及市集簽署的應用程式執行：

    ```powershell
    Merge-CIPolicy -PolicyPaths .\newPolicy.xml,C:\Windows\Schemas\codeintegrity\examplepolicies\DefaultWindows_Audit.xml -o mergedPolicy.xml
    ```

7. 停用 **mergedPolicy.xml** 中的 **Audit mode** 規則。 當您合併時，會自動開啟稽核模式：

    ```powershell
    Set-RuleOption -o 3 -Delete .\mergedPolicy.xml
    ```

8. 啟用 **mergedPolicy.xml** 中的 **InvalidateEAs on a reboot** 規則：

    ```powershell
    Set-RuleOption -o 15 .\mergedPolicy.xml
    ```

    如需這些規則的詳細資訊，請參閱[了解 WDAC 原則規則和檔案規則](https://docs.microsoft.com/windows/security/threat-protection/windows-defender-application-control/select-types-of-rules-to-create) (機器翻譯)。

9. 將 **mergedPolicy.xml** 轉換成二進位格式。 此步驟會建立 **compiledPolicy.bin**。 您會將這個 **compiledPolicy.bin** 二進位檔案新增至 Intune。

    ```powershell
    ConvertFrom-CIPolicy .\mergedPolicy.xml .\compiledPolicy.bin
    ```

10. 在 Intune 中，建立自訂的裝置組態設定檔：

    1. 在 [Microsoft Endpoint Manager 系統管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)，建立 Windows 10 自訂裝置組態設定檔。

        如需特定步驟，請參閱[在 Intune 中使用 OMA-URI 建立自訂設定檔](custom-settings-configure.md)。

    2. 當您建立設定檔時，請輸入下列設定：

      - **OMA-URI**：輸入 `./Vendor/MSFT/ApplicationControl/Policies/<PolicyGUID>`。 使用您在步驟 6 所建立之 **mergedPolicy.xml** 檔案中的 PolicyTypeID 節點取代 `<PolicyGUID>`。

        使用我們的範例，輸入 `./Vendor/MSFT/ApplicationControl/Policies/A244370E-44C9-4C06-B551-F6016E563076`。

        原則 GUID **必須符合** (步驟 6 所建立之) **mergedPolicy.xml** 檔案中的 PolicyTypeID 節點。

      - **資料類型**：設為 **Base64 檔案**。 這會自動將檔案從 bin 轉換成 base64。
      - **憑證檔案**：上傳 **compiledPolicy.bin** 二進位檔案 (在步驟 9 中建立)。

      您的設定會看起來類似下列設定：

      :::image type="content" source="./media/custom-profile-hololens/custom-applicationcontrol-omauri.png" alt-text="新增自訂的 OMA-URI 以在 Microsoft Intune 中設定 ApplicationControl CSP。":::

11. 當設定檔[指派給](device-profile-assign.md)您的 HoloLens 2 群組後，請檢查設定檔狀態。 成功套用設定檔之後，請重新開機 HoloLens 2 裝置。

## <a name="next-steps"></a>後續步驟

[指派設定檔](device-profile-assign.md)並[監視其狀態](device-profile-monitor.md)。

[深入了解 Intune 中的自訂設定檔](custom-settings-configure.md)。
