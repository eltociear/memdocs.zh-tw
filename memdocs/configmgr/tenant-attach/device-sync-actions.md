---
title: Microsoft 端點管理員租用戶附加
titleSuffix: Configuration Manager
description: 將您的 Configuration Manager 裝置上傳至雲端服務，並從系統管理中心採取動作。
ms.date: 04/10/2020
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: 7a597d9e-a878-48d0-a7ce-56a1dbfd0e5c
manager: dougeby
author: mestew
ms.author: mstewart
ms.openlocfilehash: be1c938cfcf332edb37e24e4094567f88f363560
ms.sourcegitcommit: c333fc6627f5577cde9d2fa8f59e642202a7027b
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/16/2020
ms.locfileid: "84795613"
---
# <a name="microsoft-endpoint-manager-tenant-attach-device-sync-and-device-actions"></a><a name="bkmk_attach"></a>Microsoft Endpoint Manager 租使用者附加：裝置同步和裝置動作
<!--3555758 live 3/4/2020-->
適用於：Configuration Manager (最新分支)

Microsoft Endpoint Manager 是一個整合的解決方案，可用於管理您的所有裝置。 Microsoft 將 Configuration Manager 和 Intune 整合到稱為 **Microsoft 端點管理員系統管理中心**的單一主控台。

從 Configuration Manager 版本2002開始，您可以將您的 Configuration Manager 裝置上傳至雲端服務，並從系統管理中心的 [**裝置**] 分頁中採取動作。

## <a name="prerequisites"></a>必要條件

- 套用此變更時，用來登入的*全域管理員*帳戶。 如需詳細資訊，請參閱[Azure Active Directory （Azure AD）系統管理員角色](https://docs.microsoft.com/azure/role-based-access-control/rbac-and-directory-admin-roles#azure-ad-administrator-roles)。
   - 上架會在您的 Azure AD 租使用者中建立協力廠商應用程式和第一方服務主體。
- Azure 公用雲端環境。
- 觸發裝置動作的使用者帳戶具有下列必要條件：
   - 已探索[Azure Active Directory 的使用者探索](../core/servers/deploy/configure/about-discovery-methods.md#azureaddisc)和[Active Directory 使用者探索](../core/servers/deploy/configure/about-discovery-methods.md#bkmk_aboutUser)。
      - 這表示在 Azure AD 中，使用者帳戶必須是已同步處理的使用者物件。
   - Microsoft Endpoint Manager 系統管理中心的 [**遠端**工作] 底下的 [**起始 Configuration Manager 動作**] 許可權。


## <a name="internet-endpoints"></a>網際網路端點

- `https://aka.ms/configmgrgateway`
- `https://*.manage.microsoft.com` <!--7424742-->

## <a name="enable-device-upload"></a>啟用裝置上傳

- 如果您目前已啟用共同管理，請[編輯共同管理屬性](#bkmk_edit)以啟用裝置上傳。
- 如果您未啟用共同管理，請[使用**設定共同管理**嚮導](#bkmk_config)來啟用裝置上傳。
   - 您可以上傳您的裝置，而不需啟用自動註冊以進行共同管理，或將工作負載切換至 Intune。
- 在 [**用戶端**] 資料行中具有 **[是]** Configuration Manager 所管理的所有裝置都將會上傳。 如有需要，您可以將上傳限制為單一裝置集合。

### <a name="edit-co-management-properties-to-enable-device-upload"></a><a name="bkmk_edit"></a>編輯共同管理屬性以啟用裝置上傳

如果您目前已啟用共同管理，請使用下列指示編輯共同管理屬性，以啟用裝置上傳：

1. 在 Configuration Manager 管理主控台中，移至 [系統管理] > [概觀] > [雲端服務] > [共同管理]。
1. 以滑鼠右鍵按一下共同管理設定，然後選取 [屬性]。
1. 在 [設定上傳] 索引標籤中，選取 [上傳至 Microsoft 端點管理員系統管理中心]。 按一下 [套用] 。
   - 裝置上傳的預設設定是 [All my devices managed by Microsoft Endpoint Configuration Manager] \(所有我由 Microsoft Endpoint Configuration Manager 管理的裝置\)。 如有需要，您可以將上傳限制為單一裝置集合。

   [![共同管理設定向導](./media/3555758-configure-upload.png)](./media/3555758-configure-upload.png#lightbox)
1. 當出現提示時，請使用「全域管理員」帳戶登入。
1. 按一下 [是] 以接受 [建立 AAD 應用程式] 通知。 此動作會佈建服務主體並建立 Azure AD 應用程式註冊，以加速同步作業。
1. 當完成變更後，請按一下 [確定] 結束共同管理屬性。


### <a name="use-the-configure-co-management-wizard-to-enable-device-upload"></a><a name="bkmk_config"></a>使用設定共同管理嚮導來啟用裝置上傳
如果您未啟用共同管理，請使用**設定共同管理**嚮導來啟用裝置上傳。 您可以上傳您的裝置，而不需啟用自動註冊以進行共同管理，或將工作負載切換至 Intune。 使用下列指示啟用裝置上傳：

1. 在 Configuration Manager 管理主控台中，移至 [系統管理] > [概觀] > [雲端服務] > [共同管理]。
1. 在功能區中，按一下 [設定共同管理] 來開啟精靈。
1. 在 [租用戶上線] 頁面上，針對環境選取 [AzurePublicCloud]。 不支援 Azure Government 雲端。
1. 按一下 [登入]。 使用「全域管理員」帳戶進行登入。
1. 確定已在 [**租**使用者登入] 頁面上選取 [**上傳至 Microsoft Endpoint Manager 系統管理中心**] 選項。
   - 如果您不想要立即啟用共同管理，請確定未核取 [**為共同管理啟用自動用戶端註冊**] 選項。 如果您想要啟用共同管理，請選取此選項。
   - 如果您啟用共同管理以及裝置上傳，您會在嚮導中提供其他頁面來完成。 如需詳細資訊，請參閱[啟用共同管理](../comanage/how-to-enable.md)。

   [![共同管理設定向導](./media/3555758-comanagement-wizard.png)](./media/3555758-comanagement-wizard.png#lightbox)
1. 依序按一下 [下一步] 和 [是]，以接受 [建立 AAD 應用程式] 通知。 此動作會佈建服務主體並建立 Azure AD 應用程式註冊，以加速同步作業。
1. 在 [**設定上傳**] 頁面上，針對 [我的**所有受 Microsoft 端點管理的裝置] Configuration Manager**選取 [建議的裝置上傳] 設定。 如有需要，您可以將上傳限制為單一裝置集合。
1. 按一下 [摘要] 以檢閱您的選擇，然後按一下 [下一步]。
1. 完成精靈後，按一下 [關閉]。  


## <a name="review-your-upload"></a><a name="bkmk_review"></a>檢查您的上傳

1. 從**CMGatewaySyncUploadWorker.log** &lt; ConfigMgr 安裝目錄開啟 CMGatewaySyncUploadWorker> \logs
1. 下一個同步處理時間是由類似于的記錄專案所記錄 `Next run time will be at approximately: 02/28/2020 16:35:31` 。
1. 針對裝置上傳，尋找類似的記錄專案 `Batching N records` 。 **N**是上傳至雲端的裝置數目。 
1. 每隔15分鐘就會進行上傳，以進行變更。 上傳變更之後，可能需要額外的5至10分鐘，用戶端變更才會出現在**Microsoft Endpoint Manager 系統管理中心**。

## <a name="perform-device-actions"></a>執行裝置動作

1. 在瀏覽器中，流覽至`endpoint.microsoft.com`
1. 選取 [**裝置**] [**所有裝置**]，以查看已上傳的裝置。 您會在所上傳裝置的 [受**管理者**] 資料行中看到**ConfigMgr** 。
   [![Microsoft Endpoint Manager 系統管理中心內的所有裝置](./media/3555758-all-devices.png)](./media/3555758-all-devices.png#lightbox)
1. 按一下裝置以載入其 **[總覽**] 頁面。
1. 按一下下列任一動作：
   - **同步處理電腦原則**
   - **同步處理使用者原則**
   - **應用程式評估週期**

   [![Microsoft Endpoint Manager 系統管理中心的裝置總覽](./media/3555758-device-overview-actions.png)](./media/3555758-device-overview-actions.png#lightbox)

## <a name="known-issues"></a>已知問題

### <a name="specific-devices-dont-synchronize"></a>特定裝置不會同步處理

<!--7099564-->
Configuration Manager 用戶端的特定裝置可能不會上傳至服務。

**受影響的裝置：** 如果裝置是針對發佈點功能和其用戶端代理程式使用相同 PKI 憑證的發佈點，則裝置將不會包含在租使用者連結裝置同步中。

**行為：** 在上線階段執行租使用者連接時，會第一次執行完整同步處理。 後續的同步處理週期為差異同步處理。 受影響裝置的任何更新都會使裝置從同步中移除。

## <a name="log-files"></a>記錄檔
使用位於服務連接點上的下列記錄：

- **CMGatewaySyncUploadWorker .log**
- **CMGatewayNotificationWorker .log**

## <a name="next-steps"></a>後續步驟

如需租使用者附加記錄檔的詳細資訊，請參閱針對[租使用者附加進行疑難排解](technical-reference.md)。
