---
title: Windows Hello 企業版設定
titleSuffix: Configuration Manager
description: 了解如何將 Windows Hello 企業版與 Configuration Manager 整合。
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: a95bc292-af10-4beb-ab56-2a815fc69304
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: c60f30e306c6ff52849cfcdd4696d67a7d26f395
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81706216"
---
# <a name="windows-hello-for-business-settings-in-configuration-manager"></a>Configuration Manager 中的 Windows Hello 企業版設定

適用於：  Configuration Manager (最新分支)

<!--1245704-->
Configuration Manager 與 Windows Hello 企業版整合。 (這項功能先前稱為 Microsoft Passport for Work)。Windows Hello 企業版是適用於 Windows 10 裝置的替代登入方法。 Windows Hello 企業版使用 Active Directory 或 Azure Active Directory (Azure AD) 帳戶來取代密碼、智慧卡或虛擬智慧卡。 Hello 企業版可讓您藉由「使用者手勢」  登入，而不使用密碼。 使用者手勢可能是 PIN、生物識別驗證或外部裝置 (例如指紋辨識器)。

> [!Important]  
> 從 1910 版開始，Configuration Manager 就不支援搭配使用憑證式驗證與 Windows Hello 企業版設定。 如需詳細資訊，請參閱[已淘汰的功能](../../core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures.md)。 金鑰式驗證仍然有效。
>
> Active Directory 同盟服務登錄授權單位 (ADFS RA) 部署比較簡單、提供較好的使用者經驗，且有更決定性的憑證註冊體驗。 請使用 ADFS RA 來向 Windows Hello 企業版進行憑證式驗證。
>
> 針對共同管理的裝置，請考慮將[**資源存取原則**工作負載](../../comanage/workloads.md#resource-access-policies)移至 Intune。 然後使用 Intune 原則來管理這些憑證。 如需詳細資訊，請參閱[如何切換工作負載](../../comanage/how-to-switch-workloads.md)。

如需詳細資訊，請參閱 [Windows Hello 企業版](https://docs.microsoft.com/windows/security/identity-protection/hello-for-business/hello-identity-verification)。

> [!Note]  
> 根據預設，Configuration Manager 不會啟用此選擇性功能。 您必須先先啟用這項功能才能使用它。 如需詳細資訊，請參閱[從更新啟用選擇性功能](../../core/servers/manage/install-in-console-updates.md#bkmk_options)。<!--505213-->  

Configuration Manager 與 Windows Hello 企業版整合的方法如下：  

- 控制使用者所能用來登入和無法用來登入的筆勢。  

- 將驗證憑證儲存在 Windows Hello 企業版金鑰儲存提供者 (KSP) 中。 如需詳細資訊，請參閱[憑證設定檔](introduction-to-certificate-profiles.md)。  

- 建立及部署 Windows Hello 企業版設定檔，以在執行 Configuration Manager 用戶端的已加入網域 Windows 10 裝置上控制其設定。 從 1910 版開始，您已無法使用憑證式驗證。 使用金鑰式驗證時，您不需要部署憑證設定檔。

## <a name="configure-a-profile"></a>設定設定檔  

1. 在 Configuration Manager 主控台中，移至 [資產與合規性]  工作區。 展開 [合規性設定]  、展開 [公司資源存取]  ，然後選取 [Windows Hello 企業版設定檔]  節點。

1. 在功能區中，選取 [建立 Windows Hello 企業版設定檔]  以啟動設定檔精靈。

1. 在 [一般]  頁面上，指定此設定檔的名稱和選擇性說明。

1. 在 [支援的平台]  頁面上，選取應套用此設定檔的 OS 版本。

1. 在 [設定]  頁面上，指定下列設定：

    - **設定 Windows Hello 企業版**：指定此設定檔會啟用、停用還是不設定 Hello 企業版。

    - **使用信賴平台模組 (TPM)** ：TPM 提供額外一層資料安全性。 選擇下列其中一個值：  

      - **必要**：只有能存取 TPM 的裝置可以佈建 Windows Hello 企業版。  

      - **慣用**：第一次嘗試使用 TPM 的裝置。 如果無法使用此值，則可以使用軟體加密。

    - **驗證方法**：將此選項設定為 [未設定]  或 [金鑰型]  。

        > [!NOTE]
        > 從 1910 版開始，Configuration Manager 就不支援搭配使用憑證式驗證與 Windows Hello 企業版設定。

    - **設定最小 PIN 長度**：如果您想要要求使用者的 PIN 必須有最小長度，請啟用此選項並指定值。 啟用時，預設值為 `4`。

    - **設定最大 PIN 長度**：如果您想要要求使用者的 PIN 必須有最大長度，請啟用此選項並指定值。 啟用時，預設值為 `127`。

    - **需要 PIN 到期 (天數)** ：指定使用者必須變更裝置 PIN 之前的天數。

    - **防止重複使用先前的 PIN**：不允許使用者使用先前使用過的 PIN。

    - **PIN 中需要有大寫字母**：指定使用者是否必須在 Windows Hello 企業版的 PIN 中包含大寫字母。 從下列選項進行選擇：  

      - **允許**：使用者可以在 PIN 中使用大寫字元，但非必要。

      - **必要**：使用者必須在 PIN 中包含至少一個大寫字元。  

      - **不允許**：使用者無法在 PIN 中使用大寫字元。  

    - **PIN 中需要有小寫字母**：指定使用者是否必須在 Windows Hello 企業版的 PIN 中包含小寫字母。 從下列選項進行選擇：  

      - **允許**：使用者可以在 PIN 中使用小寫字元，但非必要。

      - **必要**：使用者必須在 PIN 中包含至少一個小寫字元。  

      - **不允許**：使用者無法在 PIN 中使用小寫字元。  

    - **設定特殊字元**：指定在 PIN 使用特殊字元的方式。 從下列選項進行選擇：  

        > [!NOTE]
        > 特殊字元包括下列集合：
        >
        > ``` characters
        > ! " # $ % & ' ( ) * + , - . / : ; < = > ? @ [ \ ] ^ _ ` { | } ~
        > ```

      - **允許**：使用者可以在 PIN 中使用特殊字元，但非必要。  

      - **必要**：使用者必須在 PIN 中包含至少一個特殊字元。  

      - **不允許**：使用者無法在 PIN 中使用特殊字元。 如果此設定為 [未設定]  ，則也會有此行為。  

    - **設定 PIN 中的數字使用**：指定 PIN 中的數字使用。 從下列選項進行選擇：

      - **允許**：使用者可以在其 PIN 中使用數字，但並非必要。  

      - **必要**：使用者必須在其 PIN 中包含至少一個數字。  

      - **不允許**：使用者不能在其 PIN 中使用數字。

    - **啟用生物識別手勢**：使用生物識別驗證 (例如臉部辨識或指紋)。 這些模式可替代 Windows Hello 企業版的 PIN。 使用者仍然必須設定 PIN 以免生物識別驗證失敗。  

      若設為 [是]  ，Windows Hello 企業版即允許生物識別驗證。 若設為 [否]  ，Windows Hello 企業版會防止生物識別驗證 (針對所有帳戶類型)。  

    - **使用增強的防詐騙功能**：在支援增強式防詐騙功能的裝置上設定此功能。 若設為 [是]  ，Windows 即要求所有使用者在支援的情況下，使用臉部特徵防詐騙。  

    - **使用電話登入**：設定行動電話的雙重要素驗證。

1. 完成精靈。

下列螢幕擷取畫面是 Windows Hello 企業版設定檔設定的範例：  

![Windows Hello 企業版原則精靈，顯示可用設定的清單](../media/hello-for-business-settings.png)

## <a name="configure-permissions"></a>設定權限

1. 身為網域系統管理員或對等的認證，請登入已安裝下列選用功能且安全無虞的系統管理工作站：RSAT：Active Directory Domain Services 和輕量目錄服務工具。

1. 開啟 [Active Directory 使用者和電腦]  主控台。

1. 選取 [網域]、移至 [執行]  功能表，然後選取 [屬性]  。

1. 切換至 [安全性]  索引標籤，然後選取 [進階]  。

    > [!TIP]
    > 如果您沒有看到 [安全性]  索引標籤，請關閉 [屬性] 視窗。 移至 [檢視]  功能表，然後選取 [進階功能]  。

1. 選取 [新增]  。

1. 選擇 [選取主體]  ，然後輸入 `Key Admins`。

1. 在 [套用至]  清單中，選取 [子系使用者物件]  。

1. 在頁面底部，選取 [全部清除]  。

1. 在 [屬性]  區段中，選取 [讀取 msDS-KeyCredentialLink]  。

1. 選取 [確定]  以儲存您的變更並關閉所有視窗。

## <a name="next-steps"></a>後續步驟

[憑證設定檔](introduction-to-certificate-profiles.md)
