---
title: 建立遠端連線設定檔
titleSuffix: Configuration Manager
description: 使用 Configuration Manager 遠端連線設定檔，讓使用者遠端連線至工作電腦。
ms.date: 01/06/2020
ms.prod: configuration-manager
ms.technology: configmgr-compliance
ms.topic: conceptual
ms.assetid: 8c6eabc4-5dda-4682-b03e-3a450e6ef65a
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: c9a06e1b7c14cda02a8029925785c2109ea4204b
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81692466"
---
# <a name="remote-connection-profiles-in-configuration-manager"></a>Configuration Manager 中的遠端連線設定檔

適用於：  Configuration Manager (最新分支)

使用 Configuration Manager 遠端連線設定檔，以允許使用者遠端連線至工作電腦。 您可以透過這些設定檔，為階層中的使用者部署遠端桌面連線設定。 使用者可以藉由 VPN 連線，透過遠端桌面存取任何一部他們的主要工作電腦。  

> [!IMPORTANT]  
> 當您使用 Configuration Manager 來指定遠端連線設定檔設定時，用戶端會將設定儲存於 Windows 本機原則中。 這些設定可能會覆寫您以其他應用程式所設定的遠端桌面設定。 此外，如果您使用 Windows 群組原則進行遠端桌面設定，則在群組原則中指定的設定就會覆寫 Configuration Manager 設定。

Configuration Manager 會在用戶端、以及**遠端電腦連線**上建立安全性群組。 當您部署遠端連線設定檔時，用戶端會將該電腦的主要使用者新增到此群組。 本機系統管理員可以手動新增或移除此群組中的使用者，但是 Configuration Manager 在下一次評估設定檔的相容性時，才會更新成員資格。

> [!IMPORTANT]  
> 如果使用者和裝置之間的使用者裝置親和性關係變更，則 Configuration Manager 會停用遠端連線設定檔與 Windows 防火牆設定，以防止連線到該電腦。

## <a name="prerequisites"></a>先決條件  

### <a name="external-dependencies"></a>外部相依性  

- 如果您想要讓使用者可以從網際網路連線，請安裝並設定遠端桌面閘道伺服器。 如需要如何安裝和設定遠端桌面閘道伺服器的詳細資訊，請參閱[遠端桌面服務 - 隨處存取](https://docs.microsoft.com/windows-server/remote/remote-desktop-services/rds-plan-access-from-anywhere)。

- 如果用戶端執行主機型防火牆，則必須啟用 mstsc.exe 程式。 當您設定遠端連線設定檔時，您必須啟用 [允許在 Windows 網域和私人網路上連線的 Windows 防火牆例外狀況]  設定。 這項設定可讓 Configuration Manager 自動設定 Windows 防火牆。

    > [!TIP]
    > 用於設定 Windows 防火牆的群組原則設定可以覆寫您在 Configuration Manager 中指定的設定。 如果您使用群組原則來設定 Windows 防火牆，請確定群組原則設定不會封鎖 mstsc.exe。

    如果用戶端執行不同的主機型防火牆，請手動設定此防火牆相依性。  

### <a name="configuration-manager-dependencies"></a>Configuration Manager 相依性  

- 若要讓使用者連線至工作電腦，該電腦必須為該使用者的主要裝置。 如需詳細資訊，請參閱[透過使用者裝置親和性連結使用者和裝置](../../apps/deploy-use/link-users-and-devices-with-user-device-affinity.md)。

- 若要管理遠端連線設定檔，您的使用者帳戶需要 Configuration Manager 中的特定權限。 **合規性設定管理員**內建角色包含管理這些設定檔所需的權限。 如需詳細資訊，請參閱[設定以角色為基礎的系統管理](../../core/servers/deploy/configure/configure-role-based-administration.md)。

## <a name="security-and-privacy-considerations"></a>安全性和隱私權考量

### <a name="security-considerations"></a>安全性考量  

- 手動指定使用者裝置親和性，而不是讓使用者識別自己的主要裝置。 請勿啟用以使用方式為基礎的設定。

  - 在您可以部署遠端連線設定檔之前，您必須啟用 [允許讓工作電腦的所有主要使用者從遠端連線]  選項。 使用此設定時，您應該一律手動指定使用者裝置親和性。 請勿信任 Configuration Manager 從使用者或裝置收集到的資訊。 如果您部署設定檔，且信任的系統管理使用者未指定使用者裝置親和性，則未授權的使用者則可能會獲得較高權限，並可從遠端連線到電腦。

  - Configuration Manager 會透過狀態訊息收集以使用量為基礎的資訊，這是一種快速但不安全的通訊通道。 若要降低此威脅，請在用戶端電腦和管理點之間使用伺服器訊息區 (SMB) 簽署或網際網路通訊協定安全性 (IPsec)。

- 限制網站伺服器電腦上的本機系統管理權限。 站台伺服器上本機系統管理員可以手動新增成員至 Configuration Manager 自動建立及維護的**遠端電腦連線**安全性群組。 此動作可能會導致權限提高，因為成員會獲得遠端桌面權限。

### <a name="privacy-considerations"></a>隱私權考量  

當使用者從遠端連線到工作電腦時，其會下載 .wsrdp 檔案。 這個檔案包含裝置名稱與遠端桌面閘道伺服器名稱。 使用者需要這些值才能建立遠端桌面工作階段。 .wsrdp 檔案會從本機下載並且自動儲存於本機。 此檔案會在使用者下次執行遠端桌面工作階段時覆寫。  

## <a name="create-a-profile"></a>建立設定檔

1. 在 Configuration Manager 主控台中，移至 [資產與合規性]  工作區，展開 [合規性設定]  ，然後選取 [遠端連線設定檔]  。  

1. 在功能區 [首頁]  索引標籤的 [建立]  群組中，選取 [建立遠端連線設定檔]  。  

1. 在 [建立遠端連線設定檔精靈]  的 [一般]  頁面上，指定設定檔的名稱與選擇性描述。 這兩個值的最大限制為 256 個字元。  

1. 在 [設定檔設定]  頁面上，指定下列設定：  

    - **遠端桌面閘道伺服器的完整名稱與連接埠 (選用)** ：指定用於連線的遠端桌面閘道伺服器名稱。 此值具有下列需求：

        - 伺服器名稱的長度不能超過 256 個字元。
        - 該名稱可以包含大寫、小寫和數字字元。
        - 除了區段之間的句點 (`.`)，與連接埠前面的冒號 (`:`) 之外，特殊字元僅能為破折號(`–`) 與底線 (`_`)。
        - Configuration Manager 不支援使用國際化網域名稱來取得此值。

    - **僅允許來自透過網路層級驗證執行遠端桌面的電腦進行連線**：預設為啟用，此設定會為連線增加更高的安全層級。 如需詳細資訊，請參閱[授與遠端桌面存取](https://docs.microsoft.com/windows-server/remote/remote-desktop-services/clients/remote-desktop-allow-access#why-allow-connections-only-with-network-level-authentication)。

    - 啟用下列連線設定：

        - **允許遠端連線到工作電腦**

        - **允許工作電腦的所有主要使用者從遠端連線**

        - **允許 Windows 網域及私人網路連線的 Windows 防火牆例外**

        > [!IMPORTANT]  
        > 這三項設定都必須相同才能繼續進行。

        只有在您部署設定檔以關閉遠端連線時，才停用這些設定。

1. 完成精靈。

新設定檔會顯示在 [資產與相容性]  工作區的 [遠端連線設定檔]  節點中。  

## <a name="deploy"></a>部署

1. 在 Configuration Manager 主控台中，移至 [資產與合規性]  工作區，展開 [合規性設定]  ，然後選取 [遠端連線設定檔]  。

1. 在 [遠端連線設定檔]  清單中，選取您想要部署的設定檔。 在功能區 [首頁]  索引標籤的 [部署]  群組中，選取 [部署]  。  

1. 在 [部署遠端連線設定檔]  視窗中，指定下列資訊：

    - **集合**：瀏覽以選取您要部署設定檔的裝置集合。

    - **支援時補救不符合規範的規則**：啟用此設定，可在裝置上的設定檔設定不符合規範時自動進行補救。 當設定檔不存在時，則可能不符合規範。

    - **允許在維護期間以外補救**：如果想為要部署設定檔的集合設定維護視窗，請啟用此選項，讓 Configuration Manager 在維護視窗之外補救設定檔設定。 如需詳細資訊，請參閱[如何使用維護期間](../../core/clients/manage/collections/use-maintenance-windows.md)。

    - **產生警示**：啟用此選項可設定合規性警示。

    - **指定此設定基準的合規性評估排程**：指定用戶端用來評估設定檔的簡易或自訂排程。

1. 選取 [確定]  以關閉視窗並建立部署。

### <a name="client-evaluation"></a>用戶端評估

用戶端會在使用者登入時評估設定檔。

如果裝置離開您要部署遠端連線設定檔的集合，則 Configuration Manager 會停用該裝置上的設定。 不過，若要正確執行此程序，您必須至少已部署一個設定項目或含有站台設定項目的設定基準。

### <a name="conflict-resolution"></a>衝突解決

請勿將一個以上具有衝突設定的遠端連線設定檔部署到相同裝置。 例如，您將具有不同設定的兩個設定檔部署到相同集合。 您只設定一個設定檔部署，以**在支援時補救不符合規範的規則**， 這項部署可能會覆寫另一個設定檔中的設定。 Configuration Manager 不支援這種類型的遠端連線設定檔部署。

## <a name="monitor"></a>監視

前往 Configuration Manager 主控台中的 [監視]  工作區，然後選取 [部署]  。 在 [部署]  清單中，選取 [遠端連線設定檔部署]。

您可以在主頁面檢閱有關遠端連線設定檔部署相容性的摘要資訊。 若要查看更詳細的資訊，請選取 [設定檔部署]。 在功能區 [首頁]  索引標籤上的 [部署]  群組中，選取 [查看狀態]  。 此動作會開啟 [部署狀態]  頁面。  

[部署狀態]  頁面包含下列索引標籤：  

- **符合規範**：根據受影響的資產數目，顯示遠端連線設定檔的合規性。

    > [!IMPORTANT]  
    > 用戶端不會評估遠端連線設定檔 (如果不適用)。 不過，其仍會回報為符合規範。

- **錯誤**：根據受影響的資產數目，顯示一份所選遠端連線設定檔部署的所有錯誤清單。

- **不符合規範**：根據受影響的資產數目，顯示一份遠端連線設定檔中所有不符合規範規則的清單。

- **未知**：顯示一份清單，該清單包含未針對所選遠端連線設定檔部署回報合規性的所有裝置，以及這些裝置目前的用戶端狀態。

在任何索引標籤上，開啟規則，以在 [資產與相容性]  工作區的 [使用者]  節點底下建立臨時子節點。 此子節點包含所有裝置，其具有所選索引標籤的合規性狀態。

[資產詳細資料]  窗格會顯示此設定檔中，所選合規性狀態的裝置。 開啟清單中的裝置以顯示其他資訊。

## <a name="reports"></a>報告

Configuration Manager 包含內建報告，您可利用這些報告來監視遠端連線設定檔的相關資訊。 這些報告具有 [相容性和設定管理]  的報告類別。  

> [!IMPORTANT]  
> 當您在合規性設定的報告中使用 [裝置篩選器]  和 [使用者篩選器]  參數時，必須使用萬用字元 (`%`)。  

如需如何在 Configuration Manager 中設定報告的詳細資訊，請參閱[報告簡介](../../core/servers/manage/introduction-to-reporting.md)。  
