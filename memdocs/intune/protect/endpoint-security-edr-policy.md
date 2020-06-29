---
title: 在 Microsoft Intune 中使用端點安全性原則管理端點端點偵測及回應設定 | Microsoft Docs
description: 使用 Microsoft 端點管理員中的端點安全性端點偵測及回應原則，為您管理的裝置設定及部署原則。
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 05/29/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.reviewer: mattsha
ms.openlocfilehash: ae95fb48296f778fb98affa2270ba763d79fb766
ms.sourcegitcommit: 97f150f8ba8be8746aa32ebc9b909bb47e22121c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/17/2020
ms.locfileid: "84879680"
---
# <a name="endpoint-detection-and-response-policy-for-endpoint-security-in-intune"></a>Intune 中端點安全性的端點偵測及回應原則

當將 Microsoft Defender 進階威脅防護 (Microsoft Defender ATP) 與 Intune 整合時，您可使用端點偵測及回應 (EDR) 的端點安全性原則來管理 EDR 設定，並讓裝置在 Microsoft Defender ATP 上線。

Microsoft Defender ATP 端點偵測及回應功能可提供接近即時且可採取動作的進階攻擊偵測。 安全性分析師可以有效地優先處理警示、查看缺口的完整範圍，並採取回應動作來補救威脅。

EDR 原則包含平台專用的設定檔，可用來管理 EDR 的設定。 設定檔會自動包含 Microsoft Defender ATP 的「上線套件」。 上線套件會設定裝置與 Microsoft Defender ATP 搭配使用的方式。 在裝置上線後，您便可以開始使用該裝置的威脅資料。

EDR 原則會部署到您使用 Intune 在 Azure Active Directory (Azure AD) 中管理的裝置群組，以及您使用 Configuration Manager 管理的內部部署裝置 (包含 Windows 伺服器)。 不同管理路徑的 EDR 原則需要不同的上線套件。 因此，您需要為您管理的不同裝置類型建立個別的 EDR 原則。

> [!TIP]
> 對於使用 Configuration Manager 管理的裝置，其支援目前處於「公開預覽」階段。

EDR 的端點安全性原則位於 [Microsoft 端點管理員系統管理中心](https://go.microsoft.com/fwlink/?linkid=2109431) [端點安全性] 節點中的 [管理] 下方。

檢視[端點偵測及回應設定檔的設定](endpoint-security-edr-profile-settings.md)。

## <a name="prerequisites-for-edr-policies"></a>EDR 原則的必要條件

**一般**：

- **Microsoft Defender 進階威脅防護租用戶** – Microsoft Defender ATP 租用戶必須與 Microsoft 端點管理員租用戶 (Intune 訂閱) 整合，您才能建立 EDR 原則。 請參閱 Intune 文件中的[使用 Microsoft Defender ATP](advanced-threat-protection.md)。

**支援來自 Configuration Manager 的裝置**：

若要支援搭配 Configuration Manager 裝置使用 EDR 原則，您的 Configuration Manager 環境需要下列額外設定。 本文提供[設定指導](#set-up-configuration-manager-to-support-edr-policy)：

- **Configuration Manager 版本 2002 或更新版本** ‒ 您的網站必須執行 Configuration Manager 2002 或更新版本。

- **安裝 Configuration Manager 更新** - 若要啟用 Configuration Manager 2002 中的支援，以在 Microsoft 端點管理員系統管理中心使用您建立的 EDR 原則，請從 Configuration Manager 主控台安裝以下更新：
  - **Configuration Manager 2002 Hotfix (KB4563473)**

- **設定租用戶附加** - 租用戶附加可以讓您將 Configuration Manager 中的裝置集合同步到 Microsoft 端點管理員系統管理中心。 您接著便可以使用系統管理中心來將 EDR 原則部署到這些集合。

  租用戶附加通常與共同管理一併設定，但您也可以單獨設定租用戶附加。

- **同步 Configuration Manager 集合** ‒ 當您設定租用戶附加時，您可以選取要和 Microsoft 端點管理員系統管理中心同步的 Configuration Manager 裝置集合。 您也可以稍後回來修改要同步的裝置集合。Configuration Manager 裝置的 EDR 原則只能指派給您已同步的集合。

  在選取要同步的集合後，您必須啟用這些集合以搭配 Microsoft Defender ATP 使用。

- **Azure AD 的權限** - 若要完成租用戶附加的設定，並設定要與 Microsoft 端點管理員系統管理中心同步的 Configuration Manager 集合，您必須有具備 Azure 訂用帳戶全域管理員權限的帳戶。

## <a name="edr-profiles"></a>EDR 設定檔

檢視您可以為下列平台及設定檔進行的[設定](endpoint-security-edr-profile-settings.md)。

**Intune** ‒ 以下適用於您使用 Intune 管理的裝置：

- 平台：**Windows 10 及更新版本** - Intune 會將原則部署到您 Azure AD 群組中的裝置。
- 設定檔：**端點偵測及回應 (MDM)**

**Configuration Manager** (預覽) - 以下適用於您使用 Configuration Manager 管理的裝置：

- 平台：**Windows 10 和 Windows Server** - Configuration Manager 會將原則部署到您 Configuration Manager 集合中的裝置。
- 設定檔：**端點偵測及回應 (ConfigMgr) (預覽)**

## <a name="set-up-configuration-manager-to-support-edr-policy"></a>設定 Configuration Manager 以支援 EDR 原則

在您將 EDR 原則部署到 Configuration Manager 裝置前，請完成下列各節中詳細描述的設定。

這些設定會在 Configuration Manager 主控台中進行，並用於 Configuration Manager 部署。 若您不熟悉 Configuration Manager，請安排與 Configuration Manager 系統管理員協力完成這些工作。  

下列各節涵蓋必要的工作：

1. [安裝 Configuration Manager 的更新](#task-1-install-the-update-for-configuration-manager)
2. [啟用租用戶附加](#task-2-configure-tenant-attach-and-synchronize-collections)  
3. [選取要同步的集合](#task-3-select-collections-to-synchronize)
4. [為 Microsoft Defender ATP 啟用集合](#task-4-enable-collections-for-microsoft-defender-atp)

> [!TIP]
> 若要深入了解如何搭配 Configuration Manager 使用 Microsoft Defender ATP，請參閱 Configuration Manager 內容中的下列文章：
>
> - [透過 Microsoft 端點管理員系統管理中心，將 Configuration Manager 用戶端上線至 Microsoft Defender ATP](../../configmgr/core/get-started/2020/technical-preview-2003.md#bkmk_atp)
> - [Microsoft 端點管理員租用戶附加：裝置同步及裝置動作](../../configmgr/core/get-started/2020/technical-preview-2002-2.md#bkmk_attach)

### <a name="task-1-install-the-update-for-configuration-manager"></a>工作 1：安裝 Configuration Manager 的更新

Configuration Manager 版本 2002 需要更新，才支援使用您從 Microsoft 端點管理員系統管理中心部署的端點偵測及回應原則。

**更新詳細資料**：

- **Configuration Manager 2002 Hotfix (KB4563473)**

您將會發現這項更新是 Configuration Manager 2002 的「主控台內更新」。

若要安裝此更新，請遵循 Configuration Manager 文件中[安裝主控台內更新](../../configmgr/core/servers/manage/install-in-console-updates.md)的指導。

在安裝更新後，返回此處以繼續設定您的環境，使其支援來自 Microsoft 端點管理員系統管理中心的 EDR 原則。

### <a name="task-2-configure-tenant-attach-and-synchronize-collections"></a>工作 2：設定租用戶附加和同步集合

若先前已啟用共同管理，則租用戶附加已設定完成；您可以直接跳到[工作 3](#task-3-select-collections-to-synchronize)。

透過租用戶附加，您可以指定 Configuration Manager 部署中要和 Microsoft 端點管理員系統管理中心同步的裝置集合。 在同步集合後，請使用系統管理中心來檢視這些裝置的資訊，並從 Intune 部署 EDR 原則到這些裝置。  

如需租用戶附加案例的詳細資訊，請參閱 Configuration Manager 內容中的[啟用租用戶附加](../../configmgr/tenant-attach/device-sync-actions.md)。

#### <a name="enable-tenant-attach-when-co-management-hasnt-been-enabled"></a>在尚未啟用共同管理時啟用租用戶附加

> [!TIP]
> 您可以使用 Configuration Manager 主控台的**共同管理設定精靈**啟用租用戶附加，但不啟用共同管理。

若您打算啟用共同管理，請先熟悉共同管理、其必要條件及如何管理工作負載，再繼續進行。 請參閱 Configuration Manager 文件中的[什麼是共同管理？](../../configmgr/comanage/overview.md)。

1. 在 Configuration Manager 管理主控台中，移至 [系統管理] > [概觀] > [雲端服務] > [共同管理]。
2. 在功能區中，按一下 [設定共同管理] 來開啟精靈。
3. 在 [租用戶上線] 頁面上，針對環境選取 [AzurePublicCloud]。 不支援 Azure Government 雲端。
   1. 按一下 [登入]。 使用「全域管理員」帳戶進行登入。

   2. 確定已在 [租用戶上線] 頁面上選取 [上傳至 Microsoft 端底管理員系統管理中心]。

   3. 取消選取 [啟用自動用戶端註冊以進行共同管理]。

      選取此選項時，精靈會顯示額外頁面來完成共同管理的設定。 如需詳細資訊，請參閱 Configuration Manager 內容中的[啟用共同管理](../../configmgr/comanage/how-to-enable.md)。

     ![設定租用戶附加](media/endpoint-security-edr-policy/tenant-onboarding.png)

4. 依序按一下 [下一步] 和 [是]，以接受 [建立 AAD 應用程式] 通知。 此動作會佈建服務主體並建立 Azure AD 應用程式註冊，來加速將集合同步至 Microsoft 端點管理員系統管理中心的過程。

5. 在 [設定上傳] 頁面上，設定您要同步的集合。您可以將您的設定限制在一或數個裝置集合，或是使用 [所有由 Microsoft 端點管理員系統管理中心管理的裝置] 的建議裝置上傳設定。

6. 按一下 [摘要] 以檢閱您的選擇，然後按一下 [下一步]。

7. 完成精靈後，按一下 [關閉]。

   現在您已完成租用戶附加設定，並選取了要同步至 Microsoft 端點管理員系統管理中心的集合。

#### <a name="enable-tenant-attach-when-you-use-co-management"></a>在您使用共同管理時啟用租用戶附加

1. 在 Configuration Manager 管理主控台中，移至 [系統管理] > [概觀] > [雲端服務] > [共同管理]。

2. 以滑鼠右鍵按一下共同管理設定，然後選取 [屬性]。

3. 在 [設定上傳] 索引標籤中，選取 [上傳至 Microsoft 端點管理員系統管理中心]。 按一下 [套用] 。
   - 裝置上傳的預設設定是 [All my devices managed by Microsoft Endpoint Configuration Manager] \(所有我由 Microsoft Endpoint Configuration Manager 管理的裝置\)。 您也可以選擇將您的設定限制在一或數個裝置集合。

     ![檢視共同管理屬性索引標籤](media/endpoint-security-edr-policy/configure-upload.png)

4. 當出現提示時，請使用「全域管理員」帳戶登入。

5. 按一下 [是] 以接受 [建立 AAD 應用程式] 通知。 此動作會佈建服務主體並建立 Azure AD 應用程式註冊，以加速同步作業。

6. 當完成變更後，請按一下 [確定] 結束共同管理屬性。

   現在您已完成租用戶附加設定，並選取了要同步至 Microsoft 端點管理員系統管理中心的集合。

### <a name="task-3-select-collections-to-synchronize"></a>工作 3：選取要同步的集合

設定租用戶附加後，您便可以選取要同步的集合。若您尚未同步集合，或需要重新設定要同步的集合，可以在 Configuration Manager 主控台編輯共同管理的屬性來進行此操作。

#### <a name="select-collections"></a>選取集合

1. 在 Configuration Manager 管理主控台中，移至 [系統管理] > [概觀] > [雲端服務] > [共同管理]。

2. 以滑鼠右鍵按一下共同管理設定，然後選取 [屬性]。

3. 在 [設定上傳] 索引標籤中，選取 [上傳至 Microsoft 端點管理員系統管理中心]。 按一下 [套用] 。

   裝置上傳的預設設定是 [All my devices managed by Microsoft Endpoint Configuration Manager] \(所有我由 Microsoft Endpoint Configuration Manager 管理的裝置\)。 您也可以選擇將您的設定限制在一或數個裝置集合。

### <a name="task-4-enable-collections-for-microsoft-defender-atp"></a>工作 4：為 Microsoft Defender ATP 啟用集合

在您設定要同步至 Microsoft 端點管理員系統管理中心的集合後，這些集合還必須經過啟用，才能上線及使用 Microsoft Defender ATP 原則。  若要執行此操作，請在 Configuration Manager 主控台編輯各個集合的屬性。

#### <a name="enable-collections-for-use-with-advanced-threat-protection"></a>啟用集合以搭配進階威脅防護使用

1. 從連線到您頂層網站的 Configuration Manager 主控台中，以滑鼠右鍵按一下您要同步至 Microsoft 端點管理員系統管理中心的裝置集合，然後選取 [屬性]。

2. 在 [Cloud Sync] \(雲端同步\) 索引標籤中，啟用 [Make this collection available to assign Microsoft Defender ATP policies in Intune] \(提供此集合以在 Intune 中指派 Microsoft Defender ATP 原則\) 選項。

   - 若您的 Configuration Manager 階層尚未附加租用戶，您便無法選取此選項。
  
   ![設定雲端同步](media/endpoint-security-edr-policy/cloud-sync.png)

3. 選取 [確定] 儲存設定。

   此集合中的裝置現在可以接收 Microsoft Defender ATP 原則。

## <a name="create-and-deploy-edr-policies"></a>建立及部署 EDR 原則

當您的 Microsoft Defender ATP 訂用帳戶與 Intune 整合時，您便可以建立和部署 EDR 原則。 您可以建立兩種相異的 EDR 原則類型。 其中一個原則類型適用於您透過 MDM 使用 Intune 管理的裝置。 第二種類型則適用於您使用 Configuration Manager 管理的裝置。

建立新的 EDR 原則時，您會在為原則選擇平台的階段選擇要建立的原則類型。

在將原則部署到 Configuration Manager 管理的裝置前，請在 Microsoft 端點管理員系統管理中心中[設定 Configuration Manager 以支援 EDR 原則](#set-up-configuration-manager-to-support-edr-policy)。

### <a name="create-edr-policies"></a>建立 EDR 原則

1. 登入 [Microsoft Endpoint Manager 系統管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)。

2. 選取 [端點安全性] > [端點偵測及回應] > [建立原則]。

3. 選取原則的平台和設定檔。 以下資訊會決定您的選項：

   - Intune - Intune 會將原則部署到您 Azure AD 群組中的裝置。 建立原則時，請選取：
     - 平台：**Windows 10 及以上版本**
     - 設定檔：**端點偵測及回應 (MDM)**

   - Configuration Manager - Configuration Manager 會將原則部署到您 Configuration Manager 集合中的裝置。 建立原則時，請選取：
     - 平台：**Windows 10 和 Windows Server**
     - 設定檔：**端點偵測及回應 (ConfigMgr) (預覽)**

4. 選取 [建立]。

5. 在 [基本] 頁面上，輸入新設定檔的名稱與描述，然後選擇 [下一步]。

6. 在 [組態設定] 頁面上，設定您要透過此設定檔管理的設定。 上線套件會自動包含在其中，並且您無法對其進行設定。

   當完成設定時，請選取 [下一步]。

7. 此步驟僅適用於**端點偵測及回應 (MDM)** 設定檔：  

   在 [範圍標籤] 頁面上，選擇 [選取範圍標籤] 來開啟 [選取標籤] 窗格，以將範圍標籤指派給設定檔。
  
   選取 [下一步] 以繼續進行操作。

8. 在 [指派] 頁面上，選取將接收此原則的群組或集合。 選項取決於您選取的平台和設定檔：

   - 若是 Intune，請選取來自 Azure AD 的群組。
   - 若是 Configuration Manager，請選取已同步到 Microsoft 端點管理員系統管理中心，且已為 Microsoft Defender ATP 原則啟用的 Configuration Manager 集合。

   您此時可以選擇不要指派群組或集合，並在稍後編輯原則來新增指派。

   在您準備好繼續時，請選取 [下一步]。

9. 在 [檢閱 + 建立] 頁面上，當您完成操作時，請選擇 [建立]。

   新的設定檔會在您選取所建立設定檔的原則類型時顯示在清單中。

## <a name="edr-policy-reports"></a>EDR 原則報告

您可以在 Microsoft 端點管理員系統管理中心內檢視您所部署 EDR 原則的詳細資料。 若要檢視詳細資料，請前往 [端點安全性] > [端點部署和回應]，然後選取您要檢視其合規性詳細資料的原則：

- 針對以 **Windows 10 及更新版本**平台 (Intune) 為目標的原則，您將會看到原則的合規性概觀。 您也可以選取圖表來檢視接收原則的裝置清單，並鑽研個別裝置以取得詳細資料。

  **具有 ATP 感應器的裝置**圖表只會顯示已透過使用 **Windows 10 及更新版本**設定檔，成功上線至 Microsoft Defender ATP 的裝置。 為了確保您的裝置在此圖表中完整呈現，請將上線設定檔部署到所有裝置。 以外部方式 (例如群組原則或 PowerShell) 上線至 Microsoft Defender ATP 的裝置，會視為**沒有 ATP 感應器的裝置**。

- 針對以 **Windows 10 和 Windows Server** 平台 (Configuration Manager) 為目標的原則，您將會看到原則的合規性概觀，但無法鑽研以檢視其他詳細資料。 此檢視會受到限制，因為系統管理中心只會從負責管理 Configuration Manager 裝置原則部署的 Configuration Manager 收到有限的狀態詳細資料。


檢視您可以為平台和設定檔進行的[設定](endpoint-security-edr-profile-settings.md)。

## <a name="next-steps"></a>後續步驟

- [設定端點安全性原則](endpoint-security-policy.md#create-an-endpoint-security-policy)
- 深入了解 Microsoft Defender ATP 文件中的[端點偵測及回應](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/overview-endpoint-detection-response)。
