---
title: 在 Microsoft Intune 中使用 Microsoft Defender ATP - Azure | Microsoft Docs
description: 搭配 Intune 使用 Microsoft Defender 進階威脅防護 (Microsoft Defender ATP)，包括安裝及設定、使用 ATP 讓您的 Intune 裝置上線，然後搭配您的 Intune 裝置相容性與條件式存取原則使用裝置 ATP 風險評量來保護網路資源。
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 06/17/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.reviewer: shpate
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 1141879a282219cdac72273e47c84b51df172d04
ms.sourcegitcommit: 397ec824f1368dcf06c3870c89f52347852062bd
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/23/2020
ms.locfileid: "85264051"
---
# <a name="enforce-compliance-for-microsoft-defender-atp-with-conditional-access-in-intune"></a>在 Intune 中使用條件式存取強制執行 Microsoft Defender ATP 的合規性

您可以將 Microsoft Defender 進階威脅防護 (Microsoft Defender ATP) 與 Microsoft Intune 整合，作為 Mobile Threat Defense 解決方案。 整合可以協助防止安全性缺口，並協助限制因缺口而在組織內所造成的影響。 Microsoft Defender ATP 適用於執行 Windows 10 或更新版本的裝置以及 Android 裝置。

若要成功，必須使用下列設定：

- **Intune 與 Microsoft Defender ATP 之間建立服務對服務連線**。 此連線可讓 Microsoft Defender ATP 從您以 Intune 管理的受支援裝置，收集機器風險的相關資料。
- **使用裝置組態設定檔將裝置上線至 Microsoft Defender ATP**。 您會將裝置上線，將其設定為與 Microsoft Defender ATP 通訊，以及提供有助於評估其風險層級的資料。
- **使用裝置合規性政策來設定您想要允許的風險層級**。 風險層級是由 Microsoft Defender ATP 回報。 超過允許風險等級的裝置會被識別為不符合規範。
- **使用條件式存取原則**禁止使用者從不符合規範的裝置存取公司資源。

當您整合 Intune 與 Microsoft Defender (ATP) 時，可以利用 Microsoft Defender ATP 的威脅與弱點管理 (TVM)，並[使用 Intune 補救 TVM 找到的端點弱點](atp-manage-vulnerabilities.md)。

## <a name="example-of-using-microsoft-defender-atp-with-intune"></a>搭配 Intune 使用 Microsoft Defender ATP 的範例

下列範例會協助說明這些解決方案如何搭配使用，來協助保護您的組織。 在此範例中，Microsoft Defender ATP 與 Intune 已整合。

考慮有人傳送具有內嵌惡意程式碼的 Word 附件給組織內使用者的事件。

- 使用者開啟該附件並啟用內容。
- 權限提升的攻擊將會展開，而來自遠端電腦的攻擊者將會擁有受害者裝置的系統管理員權限。
- 攻擊者接著會從遠端存取該使用者的其他裝置。 此安全性缺口可能會影響整個組織。

Microsoft Defender ATP 有助於解決此類安全性事件。

- 在我們的範例中，Microsoft Defender ATP 會偵測到裝置執行不正常的程式碼、發生處理序權限提升、被插入惡意程式碼，並發出可疑遠端殼層。
- 根據來自裝置的這些動作，Microsoft Defender ATP [會將裝置分類為高風險](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/alerts-queue#severity)，並在 Microsoft Defender 資訊安全中心入口網站中包含可疑活動的詳細報告。

因為您使用 Intune 裝置合規性原則，將「中」或「高」風險的裝置分類為不符合規範，所以遭到入侵的裝置會被分類為不符合規範。 此分類可讓您的條件式存取原則開始介入，並防止該裝置存取您的公司資源。

您也可以使用 Intune 原則，在 Android 上修改 Microsoft Defender ATP 的某些設定。 如需詳細資訊，請參閱本文稍後的[在執行 Android 的裝置上設定 Web 防護](#configure-web-protection-on-devices-that-run-android)。

## <a name="prerequisites"></a>先決條件

若要搭配 Intune 使用 Microsoft Defender ATP，請確認下列項目已設定且可供使用：

- 適用於 Enterprise Mobility + Security E3 和 Windows E5 (或 Microsoft 365 企業版 E5) 的授權租用戶
- Microsoft Intune 環境，搭配已加入 Azure AD 且[受 Intune 管理的](../enrollment/windows-enroll.md) Windows 10 或 Android 裝置
- [Microsoft Defender ATP](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/microsoft-defender-advanced-threat-protection) 和 Microsoft Defender 資訊安全中心 (ATP 入口網站) 的存取權

> [!NOTE]
> iOS/iPadOS 和 Android 的 Intune 應用程式保護原則不支援 Microsoft Defender ATP。

## <a name="enable-microsoft-defender-atp-in-intune"></a>在 Intune 中啟用 Microsoft Defender ATP

您必須執行的第一個步驟是在 Intune 與 Microsoft Defender ATP 之間設定服務對服務連線。 這需要對 Microsoft Defender 資訊安全中心與 Intune 的存取權。

### <a name="to-enable-microsoft-defender-atp"></a>啟用 Microsoft Defender ATP

每個租用戶只需要啟用一次 Microsoft Defender ATP。

1. 登入 [Microsoft Endpoint Manager 系統管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)。

2. 選取 [端點安全性] > [Microsoft Defender ATP]，然後選取 [開啟 Microsoft Defender 資訊安全中心]。

   ![選取以開啟 [Microsoft Defender 資訊安全中心]](./media/advanced-threat-protection/atp-device-compliance-open-microsoft-defender.png)

3. 在 **Microsoft Defender 資訊安全中心**中：
   1. 選取 [設定] > [進階功能]。
   2. 針對 [Microsoft Intune 連線]，選擇 [開啟]：

      ![啟用 Intune 的連線](./media/advanced-threat-protection/atp-security-center-intune-toggle.png)

   3. 選取 [儲存喜好設定]。

4. 返回 Microsoft 端點管理員系統管理中心內的 [Microsoft Defender ATP]。 根據您組織的需求，在 [MDM 相容性原則設定] 之下：
   - 將 [將 10.0.15063 版及更新版本的 Windows 裝置連線到 Microsoft Defender ATP] 設定為 [開啟]
   - 將 [將 6.0.0 版及更新版本的 Android 裝置連線到 Microsoft Defender ATP] 設定為 [開啟]

5. 選取 [儲存]。

> [!TIP]
> 當您將新的應用程式整合到 Intune Mobile Threat Defense 並啟用 Intune 連線時，Intune 會在 Azure Active Directory 中建立傳統條件式存取原則。 您整合的每個 MTD 應用程式 (包括 [Microsoft Defender ATP](advanced-threat-protection.md) 或任何其他 [MTD 合作夥伴](mobile-threat-defense.md#mobile-threat-defense-partners))，都會建立新的傳統條件式存取原則。 這些原則可以忽略，但不應編輯、刪除或停用。
>
> 如已刪除傳統原則，則將需要刪除負責建立該原則的 Intune 連線，然後再次設定。 這會重新建立此傳統原則。 不支援將 MTD 應用程式傳統原則移轉至條件式存取的新原則類型。
>
> 適用於 MTD 應用程式的傳統條件式存取原則：
>
> - 由 Intune MTD 用於要求裝置必須在 Azure AD 中註冊，以便它們與 MTD 合作夥伴通訊之前擁有裝置識別碼。 此識別碼為必要，以便裝置成功向 Intune 報告其狀態。
> - 不會影響任何其他雲端應用程式或資源。
> - 不同於您可能會建立用來協助管理 MTD 的條件式存取原則。
> - 根據預設，不會與用於評估的其他條件式存取原則互動。
>
> 若要檢視傳統條件式存取原則，請前往 [Azure](https://portal.azure.com/#home) 中的 [Azure Active Directory] > [條件式存取] > [傳統原則]。

## <a name="onboard-windows-devices-by-using-a-configuration-profile"></a>使用組態設定檔將 Windows 裝置上線

對於 Windows 平台，在 Intune 與 Microsoft Defender ATP 之間建立服務對服務的連線之後，將由 Intune 管理的裝置上線到 Microsoft Defender ATP，以便收集及使用其風險層級相關資料。 若要讓裝置上線，您必須使用 Microsoft Defender ATP 的裝置組態設定檔。

當您建立與 Microsoft Defender ATP 的連線之後，Intune 會從 Microsoft Defender ATP 收到 Microsoft Defender ATP 上線組態套件。 此套件會使用裝置組態設定檔部署到裝置。 該組態套件會設定裝置，使其與 [Microsoft Defender ATP 服務](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/microsoft-defender-advanced-threat-protection)通訊，以掃描檔案、偵測威脅，以及向 Microsoft Defender ATP 回報風險。 當您使用組態套件將裝置上線之後，您不需要再次執行此動作。 您也可以使用[群組原則或 Microsoft Endpoint Configuration Manager](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/configure-endpoints) \(部分機器翻譯\) 來將裝置上線。

### <a name="create-the-device-configuration-profile"></a>建立裝置組態設定檔

1. 登入 [Microsoft Endpoint Manager 系統管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)。
2. 選取 [裝置] > [組態設定檔] > [建立設定檔]。
3. 輸入 [名稱] 和 [描述]。
4. 針對 [平台]，選取 [Windows 10 及更新版本]
5. 針對 [設定檔類型]，選取 [Microsoft Defender ATP (Windows 10 Desktop)]。
6. 設定這些設定：

   - **Microsoft Defender ATP 用戶端設定套件類型**：選取 [上架] 以將新的設定套件新增至設定檔。 選取 [下架] 可從設定檔移除設定套件。
  
     > [!NOTE]
     > 如果您已經正確建立與 Microsoft Defender ATP 的連線，Intune 會自動為您將組態設定檔**上線**，且 [Microsoft Defender ATP 用戶端設定套件類型] 設定將無法使用。
  
   - **所有檔案的範例共用**：[啟用] 可收集樣本並與 Microsoft Defender ATP 共用。 例如，如果您看到可疑檔案，可將它提交至 Microsoft Defender ATP 以進行深入分析。 [尚未設定] 不與 Microsoft Defender ATP 共用任何樣本。
   - **加快遙測回報頻率**：針對高風險的裝置 [啟用] 此設定，系統會更頻繁地將遙測回報給 Microsoft Defender ATP 服務。

     [使用 Microsoft Endpoint Configuration Manager 將 Windows 10 電腦上線](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/configure-endpoints-sccm) \(部分機器翻譯\) 中有這些 Microsoft Defender ATP 設定的更多詳細資料。

7. 選取 [確定]，然後選取 [建立] 以儲存您的變更，這會建立設定檔。
8. [指派裝置組態設定檔](../configuration/device-profile-assign.md)給您要使用 Microsoft Defender ATP 評估的裝置。

## <a name="onboard-android-devices"></a>上線 Android 裝置
在 Intune 與 Microsoft Defender ATP 之間建立服務對服務的連線之後，您必須將受控裝置上線到 Microsoft Defender ATP，以便收集及使用其風險層級相關資料。

如需上線 Android 裝置的詳細指示 (包括使用者與系統管理員的必要條件)，請參閱 Microsoft Defender ATP 文件的 [Android 版 Microsoft Defender 進階威脅防護](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/microsoft-defender-atp-android) (機器翻譯)。

## <a name="create-and-assign-compliance-policy-to-set-device-risk-level"></a>建立及指派合規性原則，以設定裝置風險等級

對於 Windows 和 Android 裝置，合規性原則會決定您視為可接受的裝置風險層級。

若不熟悉如何建立合規性原則，請參閱＜在 Microsoft Intune 中建立合規性原則＞一文中的[建立原則](../protect/create-compliance-policy.md#create-the-policy)程序。 下列資訊僅供在合規性原則中設定 Microsoft Defender ATP 使用。

1. 登入 [Microsoft Endpoint Manager 系統管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)。

2. 選取 [裝置] > [合規性政策] > [政策] > [建立政策]。

3. 針對 [平台]，使用下拉式方塊來選取下列其中一個選項：
   - **Windows 10 及以上版本**
   - **Android 裝置系統管理員**
   - **Android Enterprise**

   接著，選取 [建立] 以開啟 [建立原則] 設定視窗。

4. 指定以後可協助您識別此原則的 [名稱]。 您也可以選擇指定 [描述]。
  
5. 在 [合規性設定] 索引標籤上，展開 [Microsoft Defender ATP] 群組，然後將 [要求裝置等於或低於電腦風險分數] 設定為您偏好的等級。

   威脅等級分類是[由 Windows Defender ATP 所決定的](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/alerts-queue) \(部分機器翻譯\)。

   - **清除**：這個層級最安全。 裝置不能在具有任何現有威脅的情況下，繼續存取公司資源。 發現任何威脅時，即會將裝置評估為不相容。 (Microsoft Defender ATP 使用值*安全*)。
   - **低**：裝置只有在僅存在低層級威脅的情況下才能符合規範。 具有中或高威脅等級的裝置不符合規範。
   - **中等**：如果在裝置上發現的威脅為低或中層級，則會將裝置評估為符合規範。 如果偵測到高層級的威脅，則會將裝置判斷為不相容。
   - **高**：這個層級最不安全，且會允許所有威脅層級。 具有高、中或低威脅等級的裝置都會被視為符合規範。

6. 完成原則的設定，包括將原則指派給適用的群組。

## <a name="configure-web-protection-on-devices-that-run-android"></a>在執行 Android 的裝置上設定 Web 防護

根據預設，Android 版的 Microsoft Defender ATP 包含及啟用 Web 防護功能。 [Web 防護](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/web-protection-overview) (機器翻譯) 有助於保護裝置免遭 Web 威脅，以及保護使用者免遭網路釣魚攻擊。

雖然預設為啟用，但在某些 Android 裝置上仍有停用此防護的正當理由。 例如，您可以選擇只使用 Microsoft Defender ATP 應用程式掃描功能，或防止 Web 防護在掃描有害的 URL 時使用您的 VPN。

Intune 支援關閉全部或部分的 Web 防護功能。 您所使用的方法與您可以停用的功能，視 Android 裝置向 Intune 註冊的方式而定：

- **Android 裝置系統管理員**：使用組態設定檔來設定裝置上的自訂 OMA-URI 設定，以停用整個 Web 防護功能，或只停止使用 VPN。 如需 Android 裝置自訂設定的一般資訊，請參閱[自訂設定](../configuration/custom-settings-android.md)。

- **Android Enterprise 工作設定檔**：使用應用程式組態設定檔與「設定設計工具」來停用 Web 防護。 這個方法與註冊類型支援停用所有的 Web 防護功能，但不支援只停止使用 VPN。 如需應用程式設定原則的一般資訊，請參閱[使用設定設計工具](../apps/app-configuration-policies-use-android.md#use-the-configuration-designer)。

若要在裝置上設定 Web 防護，請使用下列程序來建立及部署適用的設定。

### <a name="disable-web-protection-for-android-device-administrator"></a>停用 Android 裝置系統管理員的 Web 防護

1. 登入 [Microsoft Endpoint Manager 系統管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)。

2. 選取 [裝置] > [組態設定檔] > [建立設定檔]。

3. 輸入下列設定：

   - **平台**：選取 [Android 裝置系統管理員]
   - **設定檔**：選取 [自訂]

   選取 [建立]。

4. 在 [基本] 中，輸入下列詳細資訊：

   - **名稱**：為設定檔輸入描述性名稱。 命名您的設定檔，以方便之後能輕鬆識別。 例如，「適用於 Microsoft Defender ATP Web 防護的 Android 自訂設定檔」
   - **描述**：輸入設定檔的描述。 這是選擇性設定，但建議執行。

5. 選取 [組態設定] 中的 [新增]。

   指定您想要部署的組態設定：

   - **停用 Web 防護**：
     - **名稱**：為此 OMA-URI 設定輸入唯一名稱，使其易於尋找。 例如，「停用 Microsoft Defender ATP Web 防護」
     - **描述**：(選擇性) 輸入描述以概述該設定及其他重要的詳細資料。
     - **OMA-URI**：輸入 **./Vendor/MSFT/DefenderATP/AntiPhishing**
     - **資料類型**：使用下拉式選單，然後選取 [整數]
     - **值**：輸入 **0** 停用 Web 防護，包括 VPN 型的掃描。
       > [!NOTE]
       > 輸入 **1** 啟用 Web 防護，這是預設的 Web 防護。

   - **僅停用 Web 防護使用 VPN**：
     - **名稱**：為此 OMA-URI 設定輸入唯一名稱，以便易於尋找。 例如，「停用 Microsoft Defender ATP Web 防護 VPN」
     - **描述**：(選擇性) 輸入描述以概述該設定及其他重要的詳細資料。
     - **OMA-URI**：輸入 **./Vendor/MSFT/DefenderATP/Vpn**
     - **資料類型**：使用下拉式選單，然後選取 [整數]
     - **值**：輸入 **0** 停用 VPN 型的掃描。
       > [!NOTE]
       > 輸入 **1** 啟用 Web 防護，這是預設的 Web 防護。

   選取 [新增] 以儲存 OMA-URI 設定組態，然後選取 [下一步] 繼續。

6. 在 [指派] 上指定將接收此設定檔的群組。 如需指派設定檔的詳細資訊，請參閱[指派使用者和裝置設定檔](../configuration/device-profile-assign.md)。

7. 當您在 [檢閱 + 建立] 完成操作後，請選擇 [建立]。 新的設定檔會在您選取所建立設定檔的原則類型時顯示在清單中。

### <a name="disable-web-protection-for-android-enterprise-work-profile"></a>停用 Android Enterprise 工作設定檔的 Web 防護

1. 登入 [Microsoft Endpoint Manager 系統管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)。

2. 選取 [應用程式] > [應用程式設定原則] > [新增]，然後選取受控裝置。

3. 在 [基本] 中，輸入下列詳細資訊：

   - **名稱**：為設定檔輸入描述性名稱。 命名您的設定檔，以方便之後能輕鬆識別。 例如，「適用於 Microsoft Defender ATP Web 防護的 Android 應用程式設定」。
   - **描述**：輸入設定檔的描述。 這是選擇性設定，但建議執行。
   - **平台**：選取 [Android Enterprise]
   - **設定檔類型**：選取 [僅限工作設定檔]
   - **目標應用程式**：按一下 [選取應用程式]。

4. 在 [相關聯的應用程式] 中，尋找及選取 [Defender ATP]，然後選取 [確定] > [下一步]。

5. 在 [設定] 中使用 [組態設定格式] 的下拉式清單，選取 [使用組態設計工具]，然後按一下 [新增]。 隨即開啟 JSON 編輯器。

6. 尋找及選取 [Web 防護]，然後選取 [確定] 以返回 [設定] 頁面。

7. 針對 [設定值]，輸入 **0** 以停用 Web 防護。

   > [!NOTE]
   > 輸入 **1** 啟用 Web 防護，這是預設的 Web 防護。

   選取 [下一步] 以繼續進行操作。

8. 在 [指派] 上指定將接收此設定檔的群組。 如需指派設定檔的詳細資訊，請參閱[指派使用者和裝置設定檔](../configuration/device-profile-assign.md)。

9. 當您在 [檢閱 + 建立] 完成操作後，請選擇 [建立]。 新的設定檔會在您選取所建立設定檔的原則類型時顯示在清單中。

## <a name="create-a-conditional-access-policy"></a>建立條件式存取原則

條件式存取原則可以使用 Microsoft Defender ATP 的資料，禁止超出威脅等級設定的裝置存取資源。 您可以封鎖裝置，使其無法存取公司資源，例如 SharePoint 或 Exchange Online。

> [!TIP]
> 條件式存取是一項 Azure Active Directory (Azure AD) 技術。 在 Microsoft Endpoint Manager 系統管理中心找到的「條件式存取」節點是來自 *Azure AD* 的節點。

1. 登入 [Microsoft Endpoint Manager 系統管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)。

2. 選取 [端點安全性] > [條件式存取] > [新增原則]。

3. 輸入原則 [名稱]，然後選取 [使用者和群組]。 使用 [包含] 或 [排除] 選項來針對原則新增群組，並選取 [完成]。

4. 選取 [雲端應用程式]，然後選擇要保護哪些應用程式。 例如，選擇 [選取應用程式]，然後選取 [Office 365 SharePoint Online] 和 [Office 365 Exchange Online]。

   按一下 [完成] 以儲存您的變更。

5. 選取 [條件] > [用戶端應用程式] 來將原則套用至應用程式和瀏覽器。 例如，選取 [是]，然後啟用 [瀏覽器] 和 [行動應用程式及桌面用戶端]。

   按一下 [完成] 以儲存您的變更。

6. 選取 [授與]，以根據裝置合規性套用條件式存取。 例如，選取 [授與存取權] > [裝置需要標記為合規]。

    選擇 [選取] 以儲存您的變更。

7. 選取 [啟用原則]，然後選取 [建立] 以儲存變更。

## <a name="monitor-device-compliance"></a>監視裝置合規性

監視具有 Microsoft Defender ATP 合規性原則的裝置狀態。

1. 登入 [Microsoft Endpoint Manager 系統管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)。

2. 選取 [裝置] > [監視] > [原則合規性]。

3. 在清單中尋找您的 Microsoft Defender ATP 政策，並查看有哪些裝置是符合規範或不符合規範。

您也可以使用位於相同位置，適用於不符合規範裝置的「作業」報告：

1. 選取 [裝置] > [監視] > [不合規的裝置]。

如需報告的詳細資訊，請參閱 [Intune 報告](../fundamentals/reports.md)。

## <a name="view-onboarding-status"></a>檢視上線狀態

若要檢視所有受 Intune 管理的裝置上線狀態，您可以前往 [端點安全性] > [Microsoft Defender ATP]。 您也可以在此頁面中開始建立裝置組態設定檔，以便將更多裝置上線至 Microsoft Defender ATP。

## <a name="next-steps"></a>後續步驟

[Microsoft Defender ATP 條件式存取](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/conditional-access) \(部分機器翻譯\)

[Microsoft Defender ATP 風險儀表板](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/security-operations-dashboard) \(部分機器翻譯\)

[搭配 ATP 弱點管理使用安全性工作來補救裝置上的問題](atp-manage-vulnerabilities.md)。

[裝置合規性原則入門](device-compliance-get-started.md)
