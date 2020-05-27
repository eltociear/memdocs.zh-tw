---
title: 如何針對 Intune 應用程式保護原則部署進行疑難排解
description: 討論如何針對部署 Intune 應用程式保護原則時可能遇到的問題進行疑難排解。
author: simonxjx
manager: dcscontentpm
localization_priority: Normal
search.appverid:
- MET150
audience: ITPro
ms.date: 4/17/2020
ms.service: microsoft-intune
ms.topic: troubleshooting
ms.author: v-six
ms.custom: CSSTroubleshoot
appliesto:
- Intune
ms.openlocfilehash: 8443ca01a0ca1647e8069fdccf1d71aef74c23d8
ms.sourcegitcommit: 302556d3b03f1a4eb9a5a9ce6138b8119d901575
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/27/2020
ms.locfileid: "83989462"
---
# <a name="troubleshooting-app-protection-policy-deployment-in-intune"></a>針對 Intune 中的應用程式保護原則部署進行疑難排解

## <a name="introduction"></a>簡介

本文可協助您了解並在 Microsoft Intune 中套用應用程式保護原則時的問題，並且進行疑難排解。 請遵循適用於您情況的章節。

## <a name="basic-steps"></a>基本步驟

### <a name="collect-initial-data"></a>收集起始資料

開始進行疑難排解之前，您應該先收集一些基本資訊，協助您更加了解問題，並減少尋找解決方案的時間。

收集下列資訊：

- 哪些原則設定不適用？ 是否已套用任何原則？
- 使用者體驗為何？ 使用者是否已安裝及啟動目標應用程式？
- 問題何時開始發生？ 應用程式保護是否曾經有作用？
- 哪個平台 (Android 或 iOS) 有問題？
- 有多少使用者受到影響？ 所有裝置或只有部分裝置受到影響？
- 有多少裝置受到影響？ 所有裝置或只有部分裝置受到影響？
- 雖然 Intune 應用程式保護原則不需要行動裝置管理 (MDM) 服務，但是使用 Intune 或第三方 EMM 的使用者是否會受到影響？
- 所有受控應用程式或只有特定應用程式會受到影響？ 例如，具有 [Intune App SDK](../developer/app-sdk-get-started.md) 的 LOB 應用程式受到影響，但是市集應用程式不會受到影響？

現在，您可以根據這些問題的答案開始進行疑難排解。

### <a name="verify-prerequisites"></a>確認必要條件

疑難排解的下一步是檢查是否符合所有必要條件。

雖然您可以使用與任何 MDM 解決方案無關的 Intune 應用程式保護原則，但是必須符合下列必要條件：

- 使用者必須獲得 Intune 授權指派。
- 使用者必須隸屬於由應用程式保護原則設為目標的安全性群組。 相同的應用程式保護原則必須將已使用的特定應用程式設為目標。
- 針對 Android 裝置，必須有公司入口網站應用程式，才能接收應用程式保護原則。
- 如果您使用 [Word、Excel 或 PowerPoint](https://products.office.com/business/office) 應用程式，則必須符合下列其他需求：
    - 使用者必須擁有連結到其 Azure Active Directory (Azure AD) 帳戶的 [Microsoft 365 Apps 商務版或企業版](https://products.office.com/business/compare-more-office-365-for-business-plans)授權。 訂用帳戶必須包括行動裝置版 Office 應用程式，而且可以包括[商務用 OneDrive](https://onedrive.live.com/about/business/) 的雲端儲存體帳戶。 Office 365 授權可在 [Microsoft 365 系統管理中心](https://admin.microsoft.com)內根據[這些指示](https://support.office.com/article/Assign-or-remove-licenses-for-Office-365-for-business-997596b5-4173-4627-b915-36abac6786dc) (部分機器翻譯) 指派。
    - 使用者必須擁有使用細微 [另存新檔]  功能所設定的受控位置。 此命令位於**儲存組織資料的複本**應用程式保護原則設定之下。 例如，若受控位置是 OneDrive，則 [OneDrive](https://onedrive.live.com/about/) 應用程式應該在使用者的 Word、Excel 或 PowerPoint 應用程式中設定。
    - 若受控位置是 OneDrive，則應用程式必須是部署到使用者的應用程式保護原則目標。

  > [!NOTE]
  > Office 行動裝置應用程式目前僅支援 SharePoint Online，不支援 SharePoint 內部部署。

- 如果您搭配使用 Intune 應用程式保護原則和內部部署資源 (Microsoft 商務用 Skype 和 Microsoft Exchange Server)，您必須啟用[適用於商務用 Skype 和 Exchange 的混合式新式驗證 (HMA)](https://docs.microsoft.com/office365/enterprise/hybrid-modern-auth-overview) (部分機器翻譯)。

Intune 應用程式保護原則需要使用者的身分識別在應用程式和 [Intune App SDK](../developer/app-sdk-get-started.md) 之間保持一致。 保證一致的唯一方式是透過新式驗證。 在某些情況下，應用程式可能會在沒有新式驗證的內部部署設定中運作。 不過，結果會不一致或不保證。

如需如何針對商務用 Skype 混合式和內部部署設定啟用 HMA 的詳細資訊，請參閱下列文章：

- **混合式**<br>
[適用於 SfB 和 Exchange goes GA 的混合式新式驗證](https://techcommunity.microsoft.com/t5/Skype-for-Business-Blog/Hybrid-Modern-Auth-for-SfB-and-Exchange-goes-GA/ba-p/134756) (英文)

- **內部部署**<br>
[適用於 SfB 內部部署與 AAD 的新式驗證](https://techcommunity.microsoft.com/t5/Skype-for-Business-Blog/Modern-Auth-for-SfB-OnPrem-with-AAD/ba-p/180910) (英文)

### <a name="check-app-protection-policy-status"></a>檢查應用程式保護原則狀態

若要檢查您的應用程式保護狀態，請遵循下列步驟：

1. 登入 [Microsoft Endpoint Manager 系統管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)。
2. 選取 [應用程式]   > [監視器]   > [應用程式保護狀態]  ，然後選取 [指派的使用者]  磚。
3. 在 [應用程式報告]  頁面上，選取 [選取使用者]  以顯示使用者與群組清單。
4. 從清單中搜尋並選取其中一個受影響的使用者，然後選取 [選取使用者]  。 在 [應用程式報告] 窗格頂端，您可以看到使用者是否具備應用程式保護的授權，以及是否具備 O365 的授權。 您也可以查看所有使用者裝置的應用程式狀態。
5. 記下目標應用程式、裝置類型、原則、裝置簽入狀態和上次同步時間等重要資訊。

> [!NOTE]
> 只有在應用程式用於工作內容時，才會套用應用程式保護原則。 例如，當使用者使用公司帳戶來存取應用程式時。

如需詳細資訊，請參閱[如何在 Microsoft Intune 中驗證您的應用程式保護原則設定](../apps/app-protection-policies-validate.md)。

### <a name="verify-that-user-identity-is-consistent-between-app-and-intune-app-sdk"></a>驗證應用程式與 Intune App SDK 之間的使用者身分識別一致

在大部分案例中，使用者使用其使用者主體名稱 (UPN) 登入其帳戶。 不過，在某些環境中 (例如內部部署案例)，使用者可能會使用其他形式的登入認證。 在這些情況下，您會發現在應用程式中使用的 UPN 與 Azure AD 中的 UPN 物件不相符。 發生此問題時，應用程式保護原則不會如預期般套用。

Microsoft 建議的最佳做法是將 UPN 與主要 SMTP 位址進行比對。 這種做法可讓使用者藉由使用一致的身分識別來登入受控應用程式、Intune 應用程式保護和其他 Azure AD 資源。 如需詳細資訊，請參閱 [Azure AD UserPrincipalName 填入](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect-userprincipalname) (部分機器翻譯)。

如果您的環境需要替代登入方法，請參閱[設定替代登入識別碼](https://docs.microsoft.com/windows-server/identity/ad-fs/operations/configuring-alternate-login-id) (部分機器翻譯)，特別是[具有替代識別碼的混合式新式驗證](https://docs.microsoft.com/windows-server/identity/ad-fs/operations/configuring-alternate-login-id#hybrid-modern-authentication-with-alternate-id) (部分機器翻譯)。

### <a name="verify-that-the-user-is-targeted"></a>確認使用者為目標

Intune 應用程式保護原則必須以使用者為目標。 如果您未將應用程式保護原則指派給使用者或使用者群組，則不會套用原則。

若要驗證原則是否已套用至目標使用者，請遵循下列步驟：

1. 登入 [Microsoft Endpoint Manager 系統管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)。
2. 選取 [應用程式]   >  [監視]   >  [應用程式保護狀態]  ，然後選取 [使用者狀態]  磚 (根據裝置作業系統平台)。
在開啟的 [應用程式報告]  窗格上，選取 [選取使用者]  來搜尋使用者。
3. 從清單中選取一個使用者。 您可以查看該使用者的詳細資料。

當您將原則指派給使用者群組時，請確定使用者在使用者群組中。 若要執行此動作，請依照下列步驟執行：

1. 登入 [Microsoft Endpoint Manager 系統管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)。
2. 選取 [群組] > [所有群組]  ，然後搜尋並選取用於您應用程式保護原則指派的群組。
3. 在 [管理]  區段底下，選取 [成員]  。
4. 如果未列出受影響的使用者，請檢閱[使用 Azure Active Directory 群組來管理應用程式和資源存取權](https://docs.microsoft.com/azure/active-directory/fundamentals/active-directory-manage-groups) (部分機器翻譯) 和群組成員資格規則。 請確定受影響的使用者已包含在群組中。
5. 請確定受影響的使用者不在任何原則排除群組中。

> [!IMPORTANT]
> - Intune 應用程式保護原則必須指派給使用者群組，而不是裝置群組。
> - 如果受影響的裝置使用 Apple 裝置註冊計劃 (DEP)，請確定已啟用 [使用者親和性]  。 需要在 DEP 下進行使用者驗證的任何應用程式都需要有使用者親和性。
> - 如果受影響的裝置使用 Android Enterprise，只有公司設定檔支援應用程式保護原則。


### <a name="verify-that-the-managed-app-is-targeted"></a>確認受控應用程式已設為目標

當您設定 Intune 應用程式保護原則時，目標應用程式必須使用 [Intune App SDK](../developer/app-sdk-get-started.md)。 否則，應用程式保護原則可能無法正確運作。

請確定目標應用程式已列在[受 Microsoft Intune 保護的應用程式](../apps/apps-supported-intune-apps.md)中。 針對 LOB 或自訂應用程式，請確認應用程式使用最新版的 [Intune App SDK](../developer/app-sdk-get-started.md)。 注意下列事項：

針對 iOS，這個做法很重要，因為每個版本都包含會影響這些原則套用方式以及運作方式的修正程式。 如需詳細資訊，請參閱 [Intune App SDK iOS 版本](https://github.com/msintuneappsdk/ms-intune-app-sdk-ios/releases) (英文)。
針對 Android，這個做法並不重要。 不過，使用者必須安裝最新版的公司入口網站應用程式，因為公司入口網站應用程式會以原則訊息代理程式的形式運作。

> [!NOTE]
> 從 2019 年 9 月開始，Intune 開始支援使用 Intune App SDK 8.1.1 及更新版本的 iOS 應用程式。 使用 8.1.1 以前版本 SDK 所建置的應用程式不再受到支援。 

## <a name="more-information"></a>更多資訊

### <a name="special-requirements-for-intune-mdm-managed-devices"></a>Intune MDM 受控裝置的特殊需求

當您建立應用程式保護原則時，您可以將其目標設為所有應用程式類型或下列應用程式類型：

- 非受控裝置上的應用程式
- Intune 受控裝置上的應用程式
- Android 公司設定檔中的應用程式

> [!NOTE] 
> 若要指定應用程式類型，請將 [以所有應用程式類型為目標]  設定為 [否]  ，然後從 [應用程式類型]  清單中選取。

針對 iOS，需要下列額外的[應用程式組態設定](../apps/app-configuration-policies-use-ios.md)，才能將應用程式保護原則 (APP) 設定目標設為 Intune 已註冊裝置上的應用程式：

- **IntuneMAMUPN** 必須針對所有 MDM (Intune 或第三方 EMM) 受控應用程式進行設定。 如需詳細資訊，請參閱設定 Microsoft Intune 或第三方 EMM 的使用者 UPN 設定。
- **IntuneMAMDeviceID** 必須針對所有第三方及 LOB MDM 受控應用程式進行設定。
- **IntuneMAMDeviceID** 必須設為裝置識別碼權杖。 例如，索引鍵=IntuneMAMDeviceID，值={{deviceID}}。 如需詳細資訊，請參閱[為受控 iOS 裝置新增應用程式設定原則](../apps/app-configuration-policies-use-ios.md)。
- 若只有設定 **IntuneMAMDeviceID** 值，則 Intune 應用程式會將裝置視為非受控。

### <a name="scenario-policy-changes-are-not-working"></a>案例：原則變更不作用
[Intune App SDK](../developer/app-sdk-get-started.md) 會定期檢查原則變更。 不過，此程序可能會因為下列任何原因而延遲：

- 應用程式未與服務一起簽入。
- 從裝置移除公司入口網站應用程式。

Intune 應用程式保護原則依賴使用者身分識別。 因此，在應用程式中使用公司或學校帳戶的有效登入，以及與服務的一致連線都是必要的。 如果使用者未登入應用程式，或者已從裝置移除公司入口網站應用程式，則不會套用原則更新。

此外，套用應用程式保護原則的變更與更新最多需要 8 個小時。 如果適用，關閉所有應用程式並重新啟動裝置通常會強制原則更新更快套用。

若要檢查應用程式保護狀態，請遵循下列步驟：

1. 登入 [Microsoft Endpoint Manager 系統管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)。
2. 選取 [應用程式]   > [監視器]   > [應用程式保護狀態]  ，然後選取 [指派的使用者]  磚。
3. 在 [應用程式報告] 頁面上，選取 [選取使用者]  以開啟使用者與群組的清單。
4. 從清單中搜尋並選取其中一個受影響的使用者，然後選取 [選取使用者]  。
5. 檢閱目前套用的原則，包括狀態和上次同步時間。
6. 如果狀態是 [未簽入]  ，或是顯示指出最近未同步處理，請檢查使用者是否具有一致的網路連線。 針對 Android 使用者，請確定已安裝最新版本的公司入口網站應用程式。

> [!IMPORTANT]
> [Intune App SDK](../developer/app-sdk-get-started.md) 會每 30 分鐘檢查選擇性抹除。 不過，已登入使用者的現有原則變更可能不會出現長達 8 小時。 若要加速此程序，請使用者登出應用程式然後重新登入，或者重新啟動其裝置。

Intune 應用程式保護原則包含多重身分識別支援。 Intune 只能將應用程式保護原則套用至已登入應用程式的公司或學校帳戶。 不過，每個裝置只支援一個公司或學校帳戶。

### <a name="scenario-the-policy-is-applied-but-ios-users-can-still-transfer-work-files-to-unmanaged-apps"></a>案例：已套用原則，但是 iOS 使用者仍然可以將工作檔案傳送到未受控應用程式
iOS 裝置適用的**開啟位置管理** (![開啟位置按鈕](media/troubleshoot-app-protection/troubleshoot-app-protection.jpg)) 功能可以限制透過 MDM 通道部署的應用程式之間的檔案傳輸。 視設定而定，使用者可能可以將工作檔案從受控位置 (例如 OneDrive 和 Exchange) 轉移到未受控應用程式或位置。 iOS **開啟位置管理**功能可在其他資料傳輸方法之外運作。 因此，不會受到**另存新檔**和**複製/貼上**設定的影響。

您可以搭配 iOS **開啟位置管理**功能使用 Intune 應用程式保護原則，以透過下列方式保護公司資料︰

- **員工擁有但未交由 MDM 解決方案管理的裝置**：您可以將應用程式防護原則設定設為 [Allow app to transfer data to only Policy Managed apps] \(只允許應用程式將資料傳送至受原則管理的應用程式\)  。 以這種方式設定，原則受控應用程式中的**開啟位置**行為只會將其他原則受控應用程式提供為共用選項。 例如，如果使用者嘗試在原生郵件應用程式中從 OneDrive 將受保護的檔案作為附件傳送，該檔案將無法讀取。

- **由 MDM 解決方案管理的裝置**：針對註冊至 Intune 或第三方 MDM 解決方案的裝置，在使用應用程式保護原則的應用程式與透過 MDM 所部署其他受控 iOS 應用程式之間的資料共用，是由 Intune 應用程式和 iOS **開啟位置管理**功能所控制。<br/><br/>
若要確認您使用 MDM 解決方案部署的應用程式也會與您的 Intune 應用程式保護原則建立關聯，請依[設定使用者 UPN 設定](../apps/data-transfer-between-apps-manage-ios.md#configure-user-upn-setting-for-microsoft-intune-or-third-party-emm)的說明，來設定使用者 UPN 設定。<br/><br/>若要指定您想允許資料傳輸至其他應用程式的方式，請啟用 [將組織資料傳送至其他應用程式]  ，然後選取您偏好的共用層級。<br/><br/>若要指定您想允許應用程式接收其他應用程式傳送資料的方式，請啟用 [接收其他應用程式的資料]  ，然後選取您偏好的接收資料層級。

如需如何接收和共用應用程式資料的詳細資訊，請參閱[資料重新配置設定](../apps/app-protection-policy-settings-ios.md#data-protection)。

如需詳細資訊，請參閱[如何使用 Microsoft Intune 管理 iOS 應用程式之間的資料傳輸](../apps/data-transfer-between-apps-manage-ios.md)。

## <a name="references"></a>參考

如果您仍在尋找相關問題的解決方案或 Intune 詳細資訊，請在我們的 [Microsoft Intune 論壇](https://social.technet.microsoft.com/Forums/en-US/home?category=microsoftintune&filter=alltypes&sort=lastpostdesc) (英文) 中張貼問題。 許多支援工程師、MVP 和開發小組成員都會造訪論壇。 因此，您很有可能會發現具有您所需資訊的人員。

若要開啟 Microsoft Intune 產品支援小組的支援要求，請參閱[如何取得 Microsoft Intune 支援](../fundamentals/get-support.md)。

如需 Intune 應用程式保護原則的詳細資訊，請參閱下列文章：

- [行動應用程式管理疑難排解](../apps/troubleshoot-mam.md)
- [MAM 和應用程式保護常見問題集](../apps/mam-faq.md)
- [支援提示：使用本機裝置上的記錄檔針對 Intune 應用程式保護原則進行疑難排解](https://techcommunity.microsoft.com/t5/Intune-Customer-Success/Support-Tip-Troubleshooting-Intune-app-protection-policy-using/ba-p/330372) (英文)

如需所有最新消息、資訊和技術秘訣，請移至我們的官方部落格：

- [Microsoft Intune 支援小組部落格](https://techcommunity.microsoft.com/t5/Intune-Customer-Success/bg-p/IntuneCustomerSuccess) (英文)
- [Microsoft Enterprise Mobility 與安全性部落格](https://cloudblogs.microsoft.com/enterprisemobility) (英文)

## <a name="next-steps"></a>後續步驟

- 如需其他 Intune 疑難排解資訊，請參閱[使用疑難排解入口網站來協助公司的使用者](../fundamentals/help-desk-operators.md)。 
- 深入了解 Microsoft Intune 的任何已知問題。 如需詳細資訊，請參閱 [Intune Customer Success](https://techcommunity.microsoft.com/t5/Intune-Customer-Success/bg-p/IntuneCustomerSuccess) (Intune 客戶成功)。
- 需要額外說明嗎？ 請參閱[如何取得 Microsoft Intune 支援](../fundamentals/get-support.md)。
