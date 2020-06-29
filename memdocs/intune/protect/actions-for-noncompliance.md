---
title: Microsoft Intune - Azure 中不符合規範的訊息與動作 | Microsoft Docs
description: 建立電子郵件通知，並傳送到不符合規範的裝置。 新增動作，以套用至不符合合規性原則的裝置。 動作可包括取得符合規範的寬限期、禁止存取網路資源，或淘汰不符合規範的裝置。
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 06/19/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.reviewer: samyada
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 330dd566599d6bdb1fa667d8797878ea8c92f098
ms.sourcegitcommit: 387706b2304451e548d6d9c68f18e4764a466a2b
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2020
ms.locfileid: "85093715"
---
# <a name="configure-actions-for-noncompliant-devices-in-intune"></a>在 Intune 中為不符合規範的裝置設定動作

針對不符合合規性政策或規則的裝置，您可以新增 [不符合規範時所採取的動作]。 這項功能會設定按時間排序的一連串動作，例如傳送電子郵件給終端使用者等。

## <a name="overview"></a>概觀

根據預設，每個合規性原則都包含不符合規範時 [將裝置標示為不符合規範] 的動作，且排程為零天 (**0**)。 此預設值的結果是當 Intune 偵測到不符合規範的裝置時，Intune 就會立即將此裝置標示為不符合規範。 在裝置被標示為不符合規範之後，Azure Active Directory (AD) [條件式存取](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access-azure-portal)就可以封鎖該裝置。

設定 [不符合規範時的動作]，您可彈性地決定如何處理不符合規範的裝置，以及何時執行。 例如，您可選擇不要立即封鎖裝置，然後給予使用者可變得符合規範的寬限期。

針對所設定的每個動作，您可以設定排程，以判斷該動作何時會生效。 排程會規定裝置將在幾天後被標示為不符合規範。 您也可設定某個動作的多個執行個體。 當您在原則中設定某個動作的多個執行個體時，如果裝置仍不符合規範，該動作會在該排程時間之後再次執行。

並非所有動作都適用於所有平台。

## <a name="available-actions-for-noncompliance"></a>不符合規範時可用的動作

以下是不符合規範時可用的動作。 除非另有指示，否則每個動作都適用於 Intune 支援的所有平台：

- **將裝置標記為不符合規範**：根據預設，系統會針對每個合規性原則設定此動作，且排程為零 (**0**) 天，也就是立即將裝置標示為不符合規範。

  當您變更預設排程時，您可提供寬限期，讓使用者能在不被標示為不符合規範的情況下，修補問題或變得符合規範。

- **傳送電子郵件給終端使用者**：此動作會將電子郵件通知傳送給使用者。
當您啟用此動作時：

  - 選取此動作傳送的「通知訊息範本」。 您要先[建立通知訊息範本](#create-a-notification-message-template)，才能將其指派給此動作。 當您建立自訂通知時，您可自訂主旨、訊息本文，並可包含公司標誌、公司名稱和其他連絡人資訊。
  - 選取您的一或多個 Azure AD 群組，以將訊息傳送給其他收件者。

當電子郵件送出時，Intune 會在電子郵件通知中包含不符合規範裝置的詳細資料。

- **遠端鎖定不符合規範的裝置**：使用此動作來發出裝置的遠端鎖定。 然後便會提示使用者輸入 PIN 或密碼來解除鎖定裝置。 [遠端鎖定](../remote-actions/device-remote-lock.md)功能的詳細資訊。

  下列平台支援此動作：
  - Android：
    - Android 裝置管理員
    - Android Enterprise 裝置擁有者
    - Android Enterprise 工作設定檔
    - Android 企業 kiosk 裝置
  - iOS/iPadOS
  - macOS
  - Windows 10 Mobile
  - Windows Phone 8.1 和更新版本

- **淘汰不符合規範的裝置**：此動作會從裝置移除所有公司資料，然後從 Intune 管理移除裝置。 為了防止意外抹除裝置，此動作支援的最小排程為 **30** 天。

  下列平台支援此動作：
  - Android：
    - Android 裝置管理員
    - Android Enterprise 裝置擁有者
    - Android Enterprise 工作設定檔
  - iOS/iPadOS
  - macOS
  - Windows 10 Mobile
  - Windows Phone 8.1 和更新版本

  深入了解[淘汰裝置](../remote-actions/devices-wipe.md#retire)。

- **傳送推播通知給終端使用者**：設定此動作，以透過裝置上的公司入口網站應用程式或 Intune 應用程式，將有關不符合規範的推播通知傳送至裝置。

  下列平台支援此動作：
  - Android：
    - Android 裝置管理員
    - Android Enterprise 裝置擁有者
    - Android Enterprise 工作設定檔
  - iOS/iPadOS

  推播通知會在裝置第一次簽入 Intune 且發現其不符合合規性原則時傳送。 當使用者選取通知時，公司入口網站應用程式或 Intune 應用程式會開啟，並顯示為何不符合規範的相關資訊。 使用者可接著採取動作來解決問題。 Intune 會產生不符合規範時的訊息詳細資料，且無法加以自訂。

  > [!IMPORTANT]
  > Intune、公司入口網站應用程式和 Microsoft Intune 應用程式無法保證能傳遞推播通知。 通知可能會在延遲數小時後顯示 (如果有的話)。 這包括使用者關閉推播通知的時間。
  >
  > 請勿依賴此通知方法來處理緊急訊息。

  動作的每個執行個體都只會傳送一次通知。 若要從原則再次傳送相同的通知，請在該原則中設定動作的其他執行個體，每個執行個體都有不同的排程。
  
  例如，您可將第一個動作的排程設為零天，然後為此動作新增設為三天的第二個執行個體。 第二個通知前的此種延遲讓使用者有幾天的時間可解決問題，且避免第二個通知。

  為避免因太多重複郵件造成使用者受垃圾郵件困擾，請檢閱並簡化哪些合規性原則包含不符合規範的推播通知，並檢閱排程，以免經常傳送相同內容的重複通知。

  考量：
  - 若單一原則對於針對同一天所設定的推播通知包含多個執行個體，則當天只會傳送單一通知。

  - 當多個合規性原則包含相同的合規性條件，且包含具有相同排程的推播通知動作時，Intune 會在同一天將多個通知傳送至相同的裝置。

## <a name="before-you-begin"></a>開始之前

當您設定裝置合規性原則時，您可以[新增不符合規範時的動作](#add-actions-for-noncompliance)，或稍後編輯該原則。 您可將其他動作新增至每個原則，以符合您的需求。 請記住，每個合規性原則都會自動包含不符合規範時的預設動作，以將裝置標示為不符合規範，並將排程設定為零天。

若要使用裝置合規性原則來禁止裝置存取公司資源，必須設定 Azure AD 條件式存取。 如需指引，請參閱 [Azure Active Directory 中的條件式存取](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access-azure-portal)或[透過 Intune 使用條件式存取的常見方式](conditional-access-intune-common-ways-use.md)。

若要建立裝置合規性原則，請參閱以下平台專屬指引：

- [Android](compliance-policy-create-android.md)
- [Android 工作設定檔](compliance-policy-create-android-for-work.md)
- [iOS](compliance-policy-create-ios.md)
- [macOS](compliance-policy-create-mac-os.md)
- [Windows](compliance-policy-create-windows.md)

## <a name="create-a-notification-message-template"></a>建立通知訊息範本

若要傳送電子郵件給您的使用者，請建立通知訊息範本。 裝置不符合規範時，您在範本中輸入的詳細資料會顯示在傳送給您使用者的電子郵件裡。

1. 登入 [Microsoft Endpoint Manager 系統管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)。
2. 選取 [端點安全性] > [裝置合規性] > [通知]  > [建立通知]。
3. 在 [基本] 底下，指定下列資訊：

   - **Name**
   - **主旨**
   - **Message**

4. 此外，在 [基本] 底下，為通知設定下列選項：

   - **電子郵件標頭 – 包含公司標誌** (預設 =「啟用」) - 作為公司入口網站商標一部分上傳的標誌，將會用於電子郵件範本。 如需公司入口網站商標的詳細資訊，請參閱[公司識別商標自訂](../apps/company-portal-app.md#customizing-the-user-experience)。
   - **電子郵件頁尾 – 包含公司名稱** (預設 =「啟用」)
   - **電子郵件頁尾 – 包含連絡人資訊** (預設 =「啟用」)
   - **公司入口網站網站連結** (預設 =「停用」) - 當設定為 [啟用] 時，電子郵件會包含公司入口網站的網站連結。

   > [!div class="mx-imgBorder"]
   > ![在 Intune 中符合規範的通知訊息範例](./media/actions-for-noncompliance/actionsfornoncompliance-1.PNG)

   選取 [下一步] 以繼續進行操作。

5. 在 [檢閱 + 建立] 底下檢閱設定，以確保通知訊息範本可供使用。 選取 [建立] 以完成通知的建立。

> [!NOTE]
> 您也可以選取先前建立的現有通知範本，然後 [編輯] 其資訊來更新範本。

## <a name="add-actions-for-noncompliance"></a>新增不符合規範時所採取的動作

當您建立裝置合規性政策時，Intune 會針對不符合規範自動建立動作。 如果裝置不符合合規性政策，此動作會將其標記為不符合規範。 您可以自訂將裝置標記為不符合規範的時間長度。 該動作無法移除。

您也可以在建立合規性原則或更新現有原則時，新增選擇性動作。

1. 登入 [Microsoft Endpoint Manager 系統管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)。

2. 選取 [裝置] > [合規性原則] > [原則]，選取其中一個原則，然後選取 [內容]。

   尚未建立原則嗎？ 您可建立 [Android](compliance-policy-create-android.md)、[iOS](compliance-policy-create-ios.md)、[Windows](compliance-policy-create-windows.md) 或其他平台的原則。

   > [!NOTE]
   > JAMF 裝置和裝置群組目標的裝置目前無法接收合規性動作。

3. 選取 [不符合規範時所採取的動作] > [新增]。

4. 選取您的 [動作]：

   - **傳送電子郵件給終端使用者**：裝置不符合規範時，選擇傳送電子郵件給使用者。 此外：
     - 選擇您先前建立的 [訊息範本]
     - 選取群組來輸入任何 [其他收件者]

   - **遠端鎖定不符合規範的裝置**：裝置不符合規範時，鎖定裝置。 此動作會強制使用者輸入 PIN 或密碼來解除鎖定裝置。

   - **淘汰不符合規範的裝置**：裝置不符合規範時，從裝置移除所有公司資料，然後從 Intune 管理移除裝置。

   - **傳送推播通知給終端使用者**：設定此動作，以透過裝置上的公司入口網站應用程式或 Intune 應用程式，將有關不符合規範的推播通知傳送至裝置。

5. 設定 [排程]：輸入不符合規範之後在使用者裝置觸發動作的天數 (0 到 365)。 (*淘汰不符合規範的裝置*最少支援 30 天)。在此寬限期間之後，您可以強制執行[條件式存取](conditional-access-intune-common-ways-use.md)原則。 如果您輸入 **0** (零) 天，則條件式存取會**立即**生效。 例如，如果裝置不符合規範，請使用條件式存取來立即封鎖對電子郵件、SharePoint 與其他組織資源的存取。

   當您建立合規性政策時，會自動建立 [標記裝置不合規] 動作，並自動設定為 **0** 天 (立即)。 使用此動作時，當裝置簽入時，裝置會立即評估為不符合規範。 如果也使用條件式存取，則條件式存取會立即啟動。 如果您想要允許寬限期，請在 [標記裝置不合規] 動作上變更 [排程]。

   例如，在您的合規性政策中，您也會想要通知使用者。 您可以新增 [傳送電子郵件給使用者] 動作。 在此 [傳送電子郵件] 動作中，您將 [排程] 設定為兩天。 如果裝置或終端使用者在第二天仍被評估為不符合規範，則會在第二天傳送您的電子郵件。 如果您想要在不符合規範的第五天再次傳送電子郵件給使用者，請新增另一個動作，並將 [排程] 設定為五天。

   如需有關合規性與內建動作的詳細資訊，請參閱[合規性概觀](device-compliance-get-started.md)。

6. 完成後，請選取 [新增] > [確定]以儲存變更。

## <a name="next-steps"></a>後續步驟

[監視您的原則](compliance-policy-monitor.md)。
