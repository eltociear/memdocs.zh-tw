---
title: 如何建立 Wi-Fi 設定檔
titleSuffix: Configuration Manager
description: 了解如何在 Configuration Manager 中使用 Wi-Fi 設定檔，將無線網路設定部署至組織中的使用者。
ms.date: 01/14/2020
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: 321b19b2-a093-4b8f-995f-41f74b886eb5
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 21dffd1201b04846a9fffcdc7cc917465daa5905
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81690226"
---
# <a name="create-wi-fi-profiles"></a>建立 Wi-Fi 設定檔

適用於：  Configuration Manager (最新分支)

在 Configuration Manager 中使用 Wi-Fi 設定檔，將無線網路設定部署至組織中的使用者。 部署這些設定，即可讓使用者更輕鬆地連線至 Wi-Fi。  

例如，您想要讓所有 Windows 膝上型電腦連線到您的 Wi-Fi 網路。 建立 Wi-Fi 設定檔，內含連線到無線網路所需的設定。 然後，將設定檔部署到在您階層中擁有 Windows 膝上型電腦的所有使用者。 這些裝置使用者可在無線網路清單中看見您的網路，且可直接連線至此網路。  

您可以為下列作業系統版本設定 Wi-Fi 設定檔：

- Windows 8.1 (32 位元或 64 位元)

- Windows RT 8.1

- Windows 10 或 Windows 10 行動裝置版

您也可以使用 Configuration Manager，將無線網路設定部署到使用內部部署行動裝置管理 (MDM) 的行動裝置。 如需更多一般資訊，請參閱[什麼是內部部署 MDM](../../mdm/understand/manage-mobile-devices-with-on-premises-infrastructure.md)。

建立 Wi-Fi 設定檔時，您可以加入多種安全性設定。 這些設定包括使用 Configuration Manager 憑證設定檔推送的伺服器驗證憑證和用戶端驗證憑證。 如需憑證設定檔的詳細資訊，請參閱[憑證設定檔](introduction-to-certificate-profiles.md)。

## <a name="create-a-wi-fi-profile"></a>建立 Wi-Fi 設定檔

1. 移至 Configuration Manager 主控台的 [資產與相容性]  工作區，依序展開 [相容性設定]  和 [公司資源存取]  ，然後選取 [Wi-Fi 設定檔]  節點。

1. 在 [常用]  索引標籤的 [建立]  群組中，選擇 [建立 Wi-Fi 設定檔]  。

1. 在 [建立 Wi-Fi 設定檔精靈] 的 [一般]  頁面上，指定下列資訊：

    - **名稱**：輸入在主控台中識別設定檔的唯一名稱。

    - **描述**：選擇性新增提供 Wi-Fi 設定檔進一步資訊的描述。

    - [從檔案匯入現有的 Wi-Fi 設定檔項目]  ：選取此選項可使用另一個 Wi-Fi 設定檔中的設定。 當您選取此選項時，精靈的其餘頁面會簡化為兩個頁面：[匯入 Wi-Fi 設定檔]  和 [支援的平台]  。

        > [!IMPORTANT]
        > 請確定您所匯入 Wi-Fi 設定檔包含 Wi-Fi 設定檔的有效 XML。 當您匯入檔案時，Configuration Manager 不會驗證設定檔。

    - **報告的不符合規範嚴重性**：選擇下列其中一個嚴重性等級，當裝置將 Wi-Fi 設定檔評估為不相容時，就會回報此等級。 例如，若設定檔安裝失敗，則為不相容。

        - **無**：不符合此合規性規則的電腦不會回報 Configuration Manager 報告的失敗嚴重性。

        - **資訊**

        - **警告**

        - **重大**

        - **重大事件**：不符合這項相容性規則的電腦會回報 Configuration Manager 報告的**重大**失敗嚴重性。 裝置也會將不相容狀態記錄為應用程式事件記錄中的 Windows 事件。

1. 在精靈的 [Wi-Fi 設定檔]  頁面上，指定下列資訊：

    - **網路名稱**：提供裝置將顯示的網路名稱。

        > [!IMPORTANT]
        > Configuration Manager 不支援在網路名稱中使用單引號 (`'`) 或逗號 (`,`) 字元。

    - **SSID**：指定無線網路的區分大小寫識別碼。

    - **當這個網路在範圍內時自動連線**
    - **在連線到此網路時，尋找其他無線網路**
    - **在網路未廣播其名稱 (SSID) 時進行連線**

1. 在 [安全性設定]  頁面上指定下列資訊：

    > [!IMPORTANT]
    > 如果您要建立 Wi-Fi 設定檔來進行[內部部署 MDM](../../mdm/understand/manage-mobile-devices-with-on-premises-infrastructure.md)，則 Configuration Manager 的最新分支只支援下列 Wi-Fi 安全性設定：  
    >
    > - 安全性類型：**WPA2 Enterprise** 或 **WPA2 Personal**  
    > - 加密類型：**AES** 或 **TKIP**  
    > - EAP 類型：**智慧卡或其他憑證**或 **PEAP**  

    - **安全性類型**：選取無線網路使用的安全性通訊協定，或在網路不安全時選取 [不驗證 (開放)]  。

    - **加密**：如果安全性類型支援此類型，請設定無線網路的加密方法。

    - **EAP 類型**：選取選定加密方法的驗證通訊協定。

        > [!NOTE]
        > 僅適用於 Windows Phone 裝置：不支援 [LEAP]  和 [EAP-FAST]  的 EAP 類型。

        請選取 [設定]  以指定所選取 EAP 類型的屬性。 此選項不適用於選取的某些 EAP 類型。

        > [!IMPORTANT]
        > EAP 類型設定視窗是來自 Windows。 請確定您在支援所選取 EAP 類型的電腦上執行 Configuration Manager 主控台。

    - **在每次登入時記住使用者認證**：選取此選項可儲存使用者認證，讓使用者不需要在每次登入 Windows 時輸入無線網路認證。

1. 在精靈的 [進階設定]  頁面上，指定 Wi-Fi 設定檔的其他設定。 視您在精靈的 [安全性設定]  頁面上選取的選項而定，進階設定可能無法使用或有所變動。 例如，驗證模式或單一登入選項。

1. 如果您的無線網路使用 Proxy 伺服器，請在 [Proxy 設定]  頁面上，選取 [設定此 Wi-Fi 設定檔的 Proxy 設定]  的選項。 然後提供 Proxy 的設定資訊。

1. 在 [支援的平台]  頁面上，選取此 Wi-Fi 設定檔適用的作業系統版本。

1. 完成精靈。

## <a name="next-step"></a>後續步驟

> [!div class="nextstepaction"]
> [如何部署 Wi-Fi 設定檔](deploy-wifi-vpn-email-cert-profiles.md)
