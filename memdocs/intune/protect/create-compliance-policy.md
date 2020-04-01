---
title: 建立 Microsoft Intune 中的裝置合規性原則 - Azure | Microsoft Docs
description: 建立裝置合規性原則、狀態和嚴重性等級的概觀、使用 InGracePeriod 狀態、使用條件式存取、處理沒有已指派原則的裝置，以及 Azure 入口網站與傳統入口網站中的 Microsoft Intune 合規性差異
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 03/20/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.reviewer: samyada
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 67a26a42efb56c75d9538d9e7fcd2d726327d26d
ms.sourcegitcommit: e2567b5beaf6c5bf45a2d493b8ac05d996774cac
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/27/2020
ms.locfileid: "80322997"
---
# <a name="create-a-compliance-policy-in-microsoft-intune"></a>在 Microsoft Intune 中建立合規性政策

裝置合規性政策是使用 Intune 保護您組織資源時的一項重要功能。 在 Intune 中，您可以建立裝置必須符合才能視為符合規範的規則和設定，例如最低作業系統版本。 如果裝置不符合規範，您接著可以使用[條件式存取](conditional-access.md)來封鎖對資料和資源的存取。

您也可以針對不符合規範的裝置採取動作，例如將通知電子郵件傳送給使用者。 如需合規性政策用途及其用法的概觀，請參閱[開始使用裝置合規性](device-compliance-get-started.md)。

這篇文章：

- 列出建立合規性政策的必要條件以及步驟。
- 向您示範如何將政策指派給您的使用者和裝置群組。
- 描述其他功能 (包括範圍標籤) 以「篩選」您的政策，以及您可以針對不符合規範的裝置所採取的步驟。
- 當裝置收到政策更新時，列出簽入重新整理週期時間。

## <a name="before-you-begin"></a>開始之前

若要使用裝置合規性政策，請確定您：

- 使用下列訂用帳戶：

  - Intune
  - 如果您使用條件式存取，則需要有 Azure Active Directory (AD) Premium 版本。 [Azure Active Directory 定價](https://azure.microsoft.com/pricing/details/active-directory/)會列出不同版本的功能。 Intune 合規性並不需要 Azure AD。

- 使用支援的平台：

  - Android 裝置管理員
  - Android 企業
  - iOS
  - macOS
  - Windows 10
  - Windows 8.1
  - Windows Phone 8.1

- 在 Intune 中註冊裝置 (查看合規性狀態所必需)

- 向一位使用者註冊裝置，或者在沒有主要使用者的情況下進行註冊。 不支援向多位使用者註冊裝置。

## <a name="create-the-policy"></a>建立政策

1. 登入 [Microsoft Endpoint Manager 系統管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)。

2. 選取 [裝置]   > [合規性政策]   > [政策]   > [建立政策]  。

3. 從下列選項中，選取此原則的 [平台]  ：
   - *Android 裝置系統管理員*
   - *Android Enterprise*
   - *iOS/iPadOS*
   - *macOS*
   - *Windows Phone 8.1*
   - *Windows 8.1 及更新版本*
   - *Windows 10 及以上版本*

    針對 [Android 企業]  ，您也可以選取 [原則類型]  ：
     - *Android 裝置擁有者合規性原則*
     - *Android 公司設定檔合規性原則*

    接著，選取 [建立]  以開啟 [建立原則]  設定視窗。

4. 在 [基本]  索引標籤上，指定可協助您之後識別的 [名稱]  。 例如，**將 iOS/iPadOS 越獄裝置標記為不符合規範**是一個不錯的政策名稱。

   您也可以選擇指定 [描述]  。
  
5. 在 [合規性設定]  索引標籤上，展開可用的類別，並設定原則的設定。  下列文章會描述每個平台的設定︰
   - [Android 裝置系統管理員](compliance-policy-create-android.md)
   - [Android Enterprise](compliance-policy-create-android-for-work.md)
   - [iOS/iPadOS](compliance-policy-create-ios.md)
   - [macOS](compliance-policy-create-mac-os.md)
   - [Windows Phone 8.1，Windows 8.1 和更新版本](compliance-policy-create-windows-8-1.md)
   - [Windows 10 及以上版本](compliance-policy-create-windows.md)  

6. 在 [位置]  索引標籤上，您可以根據裝置的位置，強制執行合規性。 從現有的位置中選擇。 如果您還沒有可用的位置，請參閱[使用位置 (網路柵欄)](use-network-locations.md) 以取得指引。
   > [!TIP]
   > [位置]  僅適用於 [Android 裝置系統管理員]  平台。

7. 在 [因不符合規範而採取的動作]  索引標籤上，指定要自動套用至不符合此合規性政策之裝置的動作順序。

   您可以新增多個動作，並設定一些動作的排程和其他詳細資料。 例如，您可能會將預設動作 [標記裝置不合規]  的排程變更為一天後發生。 接著，您可以新增動作，以便在裝置不符合規範時，傳送電子郵件給使用者，以警告他們該狀態。 您也可以新增能夠鎖定或淘汰不符合規範之裝置的動作。

   如需您可以設定之動作的相關資訊，請參閱[為不符合規範的裝置新增動作](actions-for-noncompliance.md)，包括如何建立要傳送給使用者的通知電子郵件。

   另一個範例包括使用位置，其中至少要將一個位置新增至合規性政策。 在此情況下，當您選取至少一個位置時，則會套用不符合規範的預設動作。 如果裝置未連線到所選取的任何位置，則會視為不符合規範。 您可以設定排程以提供使用者寬限期，例如一天。

8. 在 [範圍標籤]  索引標籤上，選取標籤以協助篩選特定群組的原則，例如 `US-NC IT Team` 或 `JohnGlenn_ITDepartment`。 新增設定之後，您也可以將範圍標籤新增至合規性政策。 

   如需有關使用範圍標籤的詳細資訊，請參閱[使用範圍標籤篩選原則](../fundamentals/scope-tags.md)。

9. 在 [指派]  索引標籤上，將原則指派給您的群組。  

   選取 [+ 選取要納入的群組]  ，然後將原則指派給一或多個群組。 當您在下一個步驟之後儲存原則時，該原則會套用到這些群組。 

10. 在 [檢閱 + 建立]  索引標籤上，檢閱設定，並在準備好儲存合規性政策時，選取 [建立]  。  

    當您的原則設為目標的使用者或裝置使用 Intune 簽入時，會評估其合規性。

<!-- Evaluate option  - pending details as to its fate with this new Full Screen UI udpate  

### Evaluate how many users are targeted

When you assign the policy, you can also **Evaluate** how many users are affected. This feature calculates users; it doesn't calculate devices.

1. In Intune, select **Devices** > **Compliance policies** > **Policies**.

2. Select a *policy* > **Assignments** > **Evaluate**. A message shows you how many users are targeted by this policy.

If the **Evaluate** button is grayed out, make sure the policy is assigned to one or more groups.
-->

## <a name="refresh-cycle-times"></a>重新整理週期時間

Intune 會使用各種重新整理循環來檢查合規性原則的更新。 如果裝置是最近註冊的，則簽入的執行頻率會更加頻繁。 [原則和設定檔重新整理循環](../configuration/device-profile-troubleshoot.md#how-long-does-it-take-for-devices-to-get-a-policy-profile-or-app-after-they-are-assigned)列出預估的重新整理時間。

使用者隨時都能開啟公司入口網站應用程式並同步處理裝置，以立即檢查是否有原則更新。

### <a name="assign-an-ingraceperiod-status"></a>指派 InGracePeriod 狀態

合規性原則的 InGracePeriod 狀態是一個值。 此值取決於裝置寬限期與裝置對該合規性政策之實際狀態的組合。

具體來說，若裝置的已指派合規性政策為 NonCompliant 狀態，且：

- 未針對裝置指派寬限期，則針對合規性原則所指派的值會是 NonCompliant
- 裝置的寬限期已過，則針對合規性原則所指派的值會是 NonCompliant
- 裝置的寬限期未到，則針對合規性原則所指派的值會是 InGracePeriod

下表摘要說明這些選項：

|實際合規性狀態|指派的寬限期值|有效合規性狀態|
|---------|---------|---------|
|NonCompliant |未指派任何寬限期 |NonCompliant |
|NonCompliant |昨天的日期|NonCompliant|
|NonCompliant |明天的日期|InGracePeriod|

如需有關監視裝置合規性政策的詳細資訊，請參閱[監視 Intune 裝置合規性政策](compliance-policy-monitor.md)。

### <a name="assign-a-resulting-compliance-policy-status"></a>指派最終合規性規則狀態

如果裝置有多個合規性原則，且裝置的兩個或更多個已指派的合規性原則具有不同的合規性狀態，系統就會指派單一的最終合規性狀態。 此指派會以指派至各合規性狀態的概念嚴重性等級為準。 每個合規性狀態均具下列嚴重性等級：

|狀態  |嚴重性  |
|---------|---------|
|Unknown     |1|
|NotApplicable     |2|
|符合標準|3|
|InGracePeriod|4|
|NonCompliant|5|
|錯誤|6|

當裝置具有多個合規性原則時，系統就會將所有原則的最高嚴重性等級指派給該裝置。

例如，有一個裝置獲指派三個合規性政策，分別是：Unknown 狀態 (嚴重性 = 1)、Compliant 狀態 (嚴重性 = 3)、InGracePeriod 狀態 (嚴重性 = 4)。 InGracePeriod 狀態的嚴重性層級最高。 因此，全部三個政策都有 InGracePeriod 合規性狀態。

## <a name="next-steps"></a>後續步驟

[監視您的原則](compliance-policy-monitor.md)。
