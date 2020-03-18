---
title: 註冊 iOS/iPadOS 裝置 - 裝置註冊計劃
titleSuffix: Microsoft Intune
description: 了解如何使用裝置註冊計劃來註冊屬公司擁有的 iOS/iPadOS 裝置。
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 02/04/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 7ddbf360-0c61-11e8-ba89-0ed5f89f718b
ms.reviewer: tisilver
ms.suite: ems
search.appverid: MET150
ms.custom: seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: d40c4f352d3e7b94ef6e6c2f16a28d188c4e9ad1
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/13/2020
ms.locfileid: "79339380"
---
# <a name="automatically-enroll-iosipados-devices-with-apples-device-enrollment-program"></a>使用 Apple 的裝置註冊計劃來自動註冊 iOS/iPadOS 裝置

您可以設定 Intune 來註冊透過 Apple [裝置註冊計劃 (DEP)](https://deploy.apple.com) 購買的 iOS/iPadOS 裝置。 DEP 可讓您註冊大量裝置，而完全不需要接觸它們。 iPhone、iPad 與 MacBook 等裝置可直接交付給使用者。 當使用者開啟裝置電源時，會以預先設定的設定來執行設定助理 (包括 Apple 產品的典型全新體驗)，並註冊裝置以接受管理。

若要啟用 DEP 註冊，您可以同時使用 Intune 與 Apple Business Manager (ABM) 或 Apple School Manager (ASM) 入口網站。 需要序號或採購單編號的清單，以在 ABM/ASM 中將裝置指派給 Intune 進行管理。 您可以在 Intune 中建立 DEP 註冊設定檔，其中包含已在註冊期間套用至裝置的設定。 請注意，DEP 註冊不能與[裝置註冊管理員](device-enrollment-manager-enroll.md)帳戶一起使用。

> [!NOTE]
> DEP 會設定終端使用者無法移除的裝置設定。 因此，在[移轉至 DEP](../fundamentals/migration-guide-considerations.md) 之前，必須先抹除裝置，讓裝置回復為出廠 (全新) 狀態。

## <a name="dep-and-the-company-portal"></a>DEP 與公司入口網站

DEP 註冊與公司入口網站應用程式的 App Store 版本不相容。 您可以為使用者提供 DEP 裝置上公司入口網站應用程式的存取權。 您可以提供此存取權，讓使用者選擇他們要在其裝置上使用的公司應用程式，或使用新式驗證來完成註冊程序。 

若要在註冊期間啟用新式驗證，請使用 DEP 設定檔中的 [使用 VPP 安裝公司入口網站]  將應用程式推送至裝置。 如需詳細資訊，請參閱[使用 Apple 的裝置註冊計劃來自動註冊 iOS/iPadOS 裝置](device-enrollment-program-enroll-ios.md#create-an-apple-enrollment-profile)。

若要讓公司入口網站自動更新，並在已向 DEP 註冊的裝置上提供公司入口網站應用程式，請透過 Intune 將公司入口網站應用程式部署為必要的大量採購方案 (VPP) 應用程式，並套用[應用程式設定原則](../apps/app-configuration-policies-use-ios.md)。

附註：在自動註冊裝置期間，當公司入口網站在單一應用程式模式中執行時，若按一下「深入了解」連結，則會因為單一應用程式模式而出現錯誤訊息。 當註冊完成後，且裝置不再處於單一應用程式模式時，您可以在 CP 中查看更多資訊。 

## <a name="what-is-supervised-mode"></a>何謂受監督模式？

Apple 在 iOS/iPadOS 5 中引進受監管模式。 您可以使用更多控制措施管理受監管模式中的 iOS/iPadOS 裝置，例如封鎖螢幕畫面擷取及封鎖從 App Store 安裝應用程式。 因此，它特別適用於公司擁有的裝置。 Intune 支援針對受監督模式設定裝置，以作為 Apple 裝置註冊方案 (DEP) 的一部分。

iOS/iPadOS 11 中對非監督式 DEP 裝置的支援已淘汰。 在 iOS/iPadOS 11 與更新版本中，應一律監督 DEP 設定裝置。 在未來的 iOS/iPadOS 版本中，將會忽略 DEP is_supervised 旗標。

<!--
**Steps to enable enrollment programs from Apple**
1. [Get an Apple DEP token and assign devices](#get-the-apple-dep-token)
2. [Create an enrollment profile](#create-an-apple-enrollment-profile)
3. [Synchronize DEP-managed devices](#sync-managed-device)
4. [Assign DEP profile to devices](#assign-an-enrollment-profile-to-devices)
5. [Distribute devices to users](#end-user-experience-with-managed-devices)
-->
## <a name="prerequisites"></a>先決條件
- [Apple 的裝置註冊計劃](https://deploy.apple.com)中所購買的裝置
- [行動裝置管理 (MDM) 授權單位](../fundamentals/mdm-authority-set.md)
- [Apple MDM Push Certificate](apple-mdm-push-certificate-get.md)

## <a name="get-an-apple-dep-token"></a>取得 Apple DEP 權杖

您必須先從 Apple 取得 DEP 權杖 (.p7m) 檔案，才能為 iOS/iPadOS 裝置註冊 DEP。 此權杖可讓 Intune 同步貴公司所擁有的 DEP 裝置資訊。 它也允許 Intune 將註冊設定檔上傳至 Apple，並將這些設定檔指派給裝置。

您可以使用 Apple Business Manager 或 Apple School Manager 入口網站來建立權杖。 您也可以使用 ABM/ASM 入口網站將裝置指派給 Intune 進行管理。

> [!NOTE]
> 若在移轉至 Azure 之前從 Intune 傳統入口網站刪除了權杖，Intune 可能會還原已刪除的 Apple DEP 權杖。 您可以從 Azure 入口網站再次刪除該 DEP 權杖。

### <a name="step-1-download-the-intune-public-key-certificate-required-to-create-the-token"></a>步驟 1： 下載建立權杖所需的 Intune 公開金鑰憑證。

1. 在 [Microsoft 端點管理員系統管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)中，選擇 [裝置]   > [iOS]   > [iOS 註冊]   > [註冊方案權杖]   > [新增]  。

    ![取得註冊計劃權杖。](./media/device-enrollment-program-enroll-ios/image01.png)

2. 藉由選取 [我同意]  來將權限授與 Microsoft，以將使用者和裝置資訊傳送給 Apple。

> [!NOTE]
> 當您在步驟 2 之後下載 Intune 公開金鑰憑證後，請勿關閉精靈或巡覽出這個頁面。 這麼做會讓您下載的憑證失效，而必須重複此程序。 如果遇到此狀況，則您通常會注意到 [檢閱 + 建立] 索引標籤上的 [建立] 按鈕呈現灰色，而無法完成此程序。

   ![[Apple 憑證] 工作區中 [註冊計劃權杖] 窗格下載公開金鑰的螢幕擷取畫面。](./media/device-enrollment-program-enroll-ios/add-enrollment-program-token-pane.png)

3. 選擇 [下載您的公開金鑰]  ，在本機下載並儲存加密金鑰 (.pem) 檔案。 這個 .pem 檔案會用於向 Apple 裝置註冊程式入口網站要求信任關係憑證。


### <a name="step-2-use-your-key-to-download-a-token-from-apple"></a>步驟 2： 使用您的金鑰，下載來自 Apple 的權杖。

1. 選擇 [建立 Apple 裝置註冊計劃的權杖]  以開啟 Apple 的部署計劃入口網站，並使用您的公司 Apple ID 登入。 您可以使用此 Apple ID 來更新 DEP 權杖。
2. 在 Apple 的[部署計劃入口網站](https://deploy.apple.com)，針對 [裝置註冊計劃]  選擇 [開始使用]  。

3. 在 [管理伺服器]  頁面上，選擇 [新增 MDM 伺服器]  。
4. 輸入 [MDM 伺服器名稱]  ，然後選擇 [下一步]  。 您可參考這個伺服器名稱，以識別行動裝置管理 (MDM) 伺服器， 但它不是 Microsoft Intune 伺服器的名稱或 URL。

5. [新增 &lt;服器名稱&gt;]  對話方塊隨即開啟，指出**上傳您的公用金鑰**。 選取 [選擇檔案]  以上傳 .pem 檔案，然後選擇 [下一步]  。

6. 移至 [部署計劃]  &gt; [裝置註冊計劃]  &gt; [管理裝置]  。
7. 在 [選擇裝置依據]  下，指定識別裝置的方式：
    - **序號**
    - **訂單號碼**
    - **上傳 CSV 檔案**。

   ![指定依據序號選擇裝置、將選擇的動作設定為 [指派給伺服器]，然後選取伺服器名稱的螢幕擷取畫面。](./media/device-enrollment-program-enroll-ios/enrollment-program-token-specify-serial.png)

8. 針對 [選擇動作]  選擇 [Assign to Server] (指派給伺服器))  ，然後選擇指定給 Microsoft Intune 的 &lt;伺服器名稱&gt;，再選擇 [確定]  。 Apple 入口網站會將指定的裝置指派給 Intune 伺服器以便管理 ，然後顯示 [指派完成]  。

   在 Apple 入口網站中，移至 [部署計劃]  &gt; [裝置註冊計劃]  &gt; [檢視指派歷程記錄]  以查看裝置與其 MDM 伺服器指派的清單。

### <a name="step-3-save-the-apple-id-used-to-create-this-token"></a>步驟 3： 儲存用以建立此權杖的 Apple ID。

在 [Microsoft Endpoint Manager 系統管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)內，提供 Apple ID 供日後參考。

![指定要用於建立註冊計劃權杖的 Apple 識別碼，並瀏覽至註冊計劃權杖的螢幕擷取畫面。](./media/device-enrollment-program-enroll-ios/image03.png)

### <a name="step-4-upload-your-token-and-choose-scope-tags"></a>步驟 4： 上傳權杖，然後選擇範圍標籤。

1. 在 [Apple 權杖]  方塊中，瀏覽至憑證 (.pem) 檔案，選擇 [開啟]  。
2. 如果您想要將[範圍標籤](../fundamentals/scope-tags.md)套用到這個 DEP 權杖中，請選擇 [範圍 (標籤)]  ，然後選取您想要的範圍標籤。 新增到此權杖的設定檔和裝置會繼承套用到權杖的範圍標籤。
3. 選擇 **[建立]** 。

使用推播憑證，透過將原則推送到已註冊的行動裝置，Intune 即可註冊及管理 iOS/iPadOS 裝置。 Intune 會自動與 Apple 同步處理，以查看您的註冊計劃帳戶。

## <a name="create-an-apple-enrollment-profile"></a>建立 Apple 註冊設定檔

安裝權杖之後，您可以為 DEP 裝置建立註冊設定檔。 裝置註冊設定檔會定義要在註冊期間套用至裝置群組的設定。 每個 DEP 權杖都有 100 個註冊設定檔的限制。

> [!NOTE]
> 如果 VPP 權杖沒有足夠的公司入口網站授權，或如果權杖已過期，將會封鎖裝置。 當權杖即將到期或授權偏低時，Intune 將會顯示警示。
 

1. 在 [Microsoft 端點管理員系統管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)中，選擇 [裝置]   > [iOS]   > [iOS 註冊]   > [註冊方案權杖]  。
2. 選取權杖、選擇 [設定檔]   > [建立設定檔]   > [iOS]  。

    ![[建立設定檔] 螢幕擷取畫面。](./media/device-enrollment-program-enroll-ios/image04.png)

3. 在 [基本]  頁面上，為設定檔輸入系統管理用的**名稱**與**描述**。 使用者看不到這些詳細資料。 您可以使用此 [名稱]  欄位，在 Azure Active Directory 中建立動態群組。 設定檔名稱可用來定義 enrollmentProfileName 參數，以註冊具備此註冊設定檔的裝置。 深入了解 [Azure Active Directory 動態群組](https://docs.microsoft.com/azure/active-directory/users-groups-roles/groups-dynamic-membership#rules-for-devices)。

    ![設定檔名稱與描述。](./media/device-enrollment-program-enroll-ios/image05.png)

4. 選取 [下一步:  裝置管理設定]。

5. 針對 [使用者親和性]  ，為具備此設定檔的裝置選擇需要或不需要由指派的使用者來進行註冊。
    - **搭配使用者親和性進行註冊** - 針對屬於使用者的裝置，以及想要使用公司入口網站進行像是安裝應用程式等服務的裝置，選擇此選項。 如果使用 ADFS，而且註冊設定檔將 [不向設定輔助程式驗證，而向公司入口網站驗證]  設定為 [否]  ，則需要 [WS-Trust 1.3 使用者名稱/混合端點](https://technet.microsoft.com/library/adfs2-help-endpoints) [深入了解](https://technet.microsoft.com/itpro/powershell/windows/adfs/get-adfsendpoint)。

    - **不搭配使用者親和性進行註冊** - 針對未與任何使用者相關的裝置選擇此選項。 針對不會存取本機使用者資料的裝置，請使用此選項。 公司入口網站應用程式類的應用程式無法運作。

5. 如果您選擇 [搭配使用者親和性進行註冊]  ，則可以讓使用者使用公司入口網站進行驗證，而不是 Apple 設定輔助程式。

    ![使用公司入口網站進行驗證。](./media/device-enrollment-program-enroll-ios/authenticatewithcompanyportal.png)

    > [!NOTE]
    > 如果您想要執行下列任何一項，請將 [選取使用者在何處必須進行驗證]  設定為 [公司入口網站]  。
    >    - 使用多重要素驗證
    >    - 提示第一次登入時必須變更密碼的使用者
    >    - 提示使用者在註冊期間重設其過期密碼
    >
    > 使用 Apple 設定輔助程式進行驗證時，不支援這些功能。

6. 如果您針對 [選取使用者在何處必須進行驗證]  選擇 [公司入口網站]  ，則可以使用 VPP 權杖自動在裝置上安裝公司入口網站。 在此情況下，使用者不需要提供 Apple ID。 若要使用 VPP 安裝公司入口網站，請在 [使用 VPP 安裝公司入口網站]  下選擇權杖。 要求已將公司入口網站新增至 VPP 權杖。 為確保公司入口網站應用程式在註冊後會繼續更新，請確定已在 Intune 中設定應用程式部署 ([Intune] > [用戶端應用程式])。 如此即不需要使用者互動。您很可能希望公司入口網站能像 iOS/iPadOS VPP 應用程式一樣、將其設為必要應用程式，並使用裝置授權進行指派。 請確定權杖未過期，而且您有足夠的公司入口網站應用程式裝置授權。 如果權杖過期或授權不足，則 Intune 會改為安裝 App Store 公司入口網站，並提示您輸入 Apple ID。 

    > [!NOTE]
    > 當 [選取使用者在何處必須進行驗證]  是 [公司入口網站]  時，請確定裝置註冊程序會在公司入口網站下載至 DEP 裝置的前 24 小時內執行。 否則註冊可能會失敗，而且需要重設成出廠預設值才能註冊裝置。
    
    ![[使用 VPP 安裝公司入口網站] 的螢幕擷取畫面。](./media/device-enrollment-program-enroll-ios/install-cp-with-vpp.png)

7. 如果您為 [選取使用者在何處必須進行驗證]  選擇 [設定輔助程式]  ，但您也想要使用條件式存取或在裝置上部署公司應用程式，您必須在裝置上安裝公司入口網站。 若要這樣做，請為 [安裝公司入口網站]  選擇 [是]  。  如果您想要讓使用者接收公司入口網站，而不需要向 App Store 進行驗證，請選擇 [使用 VPP 安裝公司入口網站]  並選取 VPP 權杖。 請確定權杖未過期，而且您有足夠的公司入口網站應用程式裝置授權來正確部署。

8. 如果您為 [使用 VPP 安裝公司入口網站]  選擇權杖，您可以在設定輔助程式完成之後，立即以單一應用程式模式 (具體來說就是公司入口網站應用程式) 鎖定裝置。 在 [Run Company Portal in Single App Mode until authentication] \(驗證前以單一應用程式模式執行公司入口網站\)  選擇 [是]  ，設定此選項。 若要使用裝置，使用者必須先使用公司入口網站登入進行驗證。

    在鎖定於單一應用程式模式的單一裝置上，不支援多重要素驗證。 此限制存在的原因是，裝置無法切換至不同的應用程式以完成第二個驗證要素。 因此，如果您想要在單一應用程式模式裝置上進行多重要素驗證，第二個要素必須位於不同的裝置上。

    iOS/iPadOS 11.3.1 與更新版本才支援此功能。

   ![單一應用程式模式的螢幕擷取畫面。](./media/device-enrollment-program-enroll-ios/single-app-mode.png)

9. 如果您想要監督使用此設定檔的裝置，請為 [受監督]  選擇 [是]  。

    ![裝置管理設定螢幕擷取畫面。](./media/device-enrollment-program-enroll-ios/supervisedmode.png)

    **受監督**裝置可提供您更多管理選項，並且預設會停用 [啟用鎖定]。 Microsoft 建議使用 DEP 作為啟用受監管模式的機制，尤其是您在部署大量的 iOS/iPadOS 裝置時。

    有兩種方式可通知使用者其裝置收到監督：

   - 鎖定畫面顯示：「此 iPhone 受 Contoso 管理。」
   - [設定]   > [一般]   > [關於]  畫面顯示：「此 iPhone 受監督。 Contoso 可以監視您的網際網路流量並找到此裝置。」

     > [!NOTE]
     > 註冊為不受監督的裝置，僅可透過使用 Apple Configurator 重設為受監督。 以這種方式將裝置重設，需要使用 USB 纜線將 iOS/iPadOS 裝置連接至 Mac。 在 [Apple Configurator 文件](http://help.apple.com/configurator/mac/2.3)上，深入了解這項作業。

10. 選擇您是否想要針對使用此設定檔的裝置鎖定註冊。 **鎖定的註冊**會停用可將管理設定檔從 [設定]  功能表中移除的 iOS/iPadOS 設定。 註冊裝置之後，必須抹除裝置才能變更此設定。 這類裝置必須將**受監督**管理模式設為 [是]  。 

11. 選擇您是否想要讓使用此設定檔的裝置**與電腦同步**。 若選擇 [依據憑證允許 Apple Configurator]  ，則必須在 [Apple Configurator 憑證]  下選擇憑證。

12. 若您在前一個步驟中選擇 [依據憑證允許 Apple Configurator]  ，則請選擇要匯入的 Apple Configurator 憑證。

13. 您可以指定裝置的命名格式，以在其註冊時和每次後續簽入時自動套用。 若要建立命名範本，請在 [套用裝置名稱範本]  下選取 [是]  。 然後，在 [裝置名稱範本]  方塊中，輸入要用於使用此設定檔之名稱的範本。 您可以指定包括裝置類型與序號的範本格式。 

14. 選擇 [下一步:  設定助理自訂]。

15. 在 [設定助理自訂]  頁面上，設定下列設定檔設定：![設定助理自訂。](./media/device-enrollment-program-enroll-ios/setupassistantcustom.png)


    | 部門設定 | 說明 |
    |---|---|
    | <strong>部門名稱</strong> | 使用者在啟用期間點選 [關於設定] 時顯示。 |
    |    <strong>部門電話</strong>     | 在使用者在啟用期間按一下 [需要協助] 按鈕時顯示。 |

    在使用者安裝期間，您可以選擇隱藏裝置上的 [設定助理] 畫面。
    - 如果您選擇 [隱藏]  ，則不會在設定期間顯示畫面。 設定好裝置之後，使用者仍然可以進入 [設定]  功能表來設定此功能。
    - 如果您選擇 [顯示]  ，將會在設定期間顯示畫面。 使用者有時可以跳過畫面而不採取動作。 但是他們隨後可以進入裝置的 [設定]  功能表來設定此功能。 


    | 設定助理畫面設定 | 如果您選擇 [顯示]  ，裝置會在設定期間... |
    |------------------------------------------|------------------------------------------|
    | <strong>密碼</strong> | 提示使用者輸入密碼。 除非以其他方式控制存取 (例如，將裝置限制為單一應用程式的 Kiosk 模式)，否則未受到保護的裝置一律需要密碼。 |
    | <strong>位置服務</strong> | 提示使用者輸入其位置。 |
    | <strong>還原</strong> | 顯示 [應用程式與資料] 畫面。 此畫面可讓使用者選擇在設定裝置時，要從 iCloud 備份還原或傳送資料。 |
    | <strong>iCloud 與 Apple ID</strong> | 提供讓使用者選擇使用其 Apple ID 登入並使用 iCloud 的選項。                         |
    | <strong>條款和條件</strong> | 需要使用者接受 Apple 的條款及條件。 |
    | <strong>Touch ID</strong> | 可讓使用者選擇設定裝置的指紋識別。 |
    | <strong>Apple Pay</strong> | 可讓使用者選擇在裝置上設定 Apple Pay。 |
    | <strong>縮放</strong> | 可讓使用者選擇在設定裝置時縮放顯示畫面。 |
    | <strong>Siri</strong> | 可讓使用者選擇設定 Siri。 |
    | <strong>診斷資料</strong> | 向使用者顯示 [診斷] 畫面。 此畫面可讓使用者選擇將診斷資料傳送給 Apple。 |
    | <strong>顯示色調</strong> | 可讓使用者選擇開啟 [顯示色調]。 |
    | <strong>隱私權</strong> | 向使用者顯示 [隱私權] 畫面。 |
    | <strong>Android 移轉</strong> | 可讓使用者選擇從 Android 裝置移轉日期。 |
    | <strong>iMessage 和 FaceTime</strong> | 提供使用者選擇設定 iMessage 與 FaceTime 的選項。 |
    | <strong>入門訓練</strong> | 顯示用於使用者教育的入門訓練資訊畫面，例如封面頁及多工和控制中心。 |
    | <strong>Watch 移轉</strong> | 可讓使用者選擇從監看式裝置移轉資料。 |
    | <strong>螢幕使用時間</strong> | 顯示 [螢幕使用時間] 畫面。 |
    | <strong>軟體更新</strong> | 顯示強制軟體更新畫面。 |
    | <strong>SIM 卡設定</strong> | 可讓使用者選擇新增行動電話通訊方案。 |
    | <strong>外觀</strong> | 向使用者顯示 [外觀] 畫面。 |
    | <strong>快速語言</strong>| 向使用者顯示 [快速語言] 畫面。 |
    | <strong>慣用語言</strong> | 提供使用者選擇其**慣用語言**的選項。 |
    | <strong>裝置到裝置的移轉</strong> | 提供使用者將資料從舊裝置移轉到此裝置的選項。|
    

16. 選擇 [下一步]  以移至 [檢閱 + 建立]  頁面。

17. 若要儲存該設定檔，請選擇 [建立]  。

## <a name="sync-managed-devices"></a>同步受管理裝置
由於 Intune 有管理您裝置的權限，您可以同步處理 Intune 與 Apple，以在 Azure 入口網站的 Intune 中查看受管理裝置。

1. 在 [Microsoft 端點管理員系統管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)中，選擇 [裝置]  > [iOS]  > **[iOS 註冊]** > [註冊方案權杖]  > 選擇清單中的權杖 > [裝置]  > [同步]  。![[註冊計劃裝置] 節點與 [同步] 連結的螢幕擷取畫面。](./media/device-enrollment-program-enroll-ios/image06.png)

   為遵循 Apple 條款內所規定的註冊計劃流量，Intune 具有下列限制︰
   - 完整同步處理每 7 天只能執行一次。 在完整同步期間，Intune 會擷取指派至已連線 Intune 之 Apple MDM 伺服器的序號完整更新清單。 如果從 Intune 入口網站刪除 DEP 裝置，則應該從 DEP 入口網站中的 Apple MDM 伺服器取消指派 DEP 裝置。 如果未解除指派，則在執行完整同步之前，不會將它重新匯入至 Intune。   
   - 同步會每 24 小時自動執行一次。 您也可以按一下 [同步]  按鈕來進行同步 (請勿在 15 分鐘內重複點選)。 所有同步要求都必須在 15 分鐘內完成。 [同步]  按鈕在同步完成前都會處於停用狀態。 此同步會重新整理現有的裝置狀態，以及匯入指派至 Apple MDM 伺服器的新裝置。   


## <a name="assign-an-enrollment-profile-to-devices"></a>將註冊設定檔指派給裝置
必須先將註冊計劃設定檔指派至裝置，裝置才能註冊。

>[!NOTE]
>您也可以從 [Apple 序號]  刀鋒視窗中，將序號指派給設定檔。

1. 在 [Microsoft 端點管理員系統管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)中，選擇 [裝置]   > [iOS]   > [iOS 註冊]   > [註冊方案權杖]  > 在清單中選擇權杖。
2. 選擇 [裝置]  > 選擇清單中的裝置 > [指派設定檔]  。
3. 在 [指派設定檔]  下，選擇裝置的設定檔 > [指派]  。

### <a name="assign-a-default-profile"></a>指派預設設定檔

您可以針對使用特定權杖註冊的所有裝置，挑選要套用的預設設定檔。

1. 在 [Microsoft 端點管理員系統管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)中，選擇 [裝置]   > [iOS]   > [iOS 註冊]   > [註冊方案權杖]  > 在清單中選擇權杖。
2. 選擇 [設定預設設定檔]  、在下拉式清單中選擇設定檔，然後選擇 [儲存]  。 此設定檔將套用到使用該權杖註冊的所有裝置。

## <a name="distribute-devices"></a>散發裝置
您已啟用 Apple 與 Intune 之間的管理和同步，並指派設定檔以供您的 DEP 裝置註冊。 您現在可以將裝置散發給使用者。 具有使用者親和性的裝置會需要為每個使用者指派 Intune 授權。 沒有使用者親和性的裝置需要裝置授權。 在抹除裝置前，已啟用的裝置無法套用註冊設定檔。

請參閱[以裝置註冊計劃在 Intune 註冊 iOS/iPadOS 裝置](../user-help/enroll-your-device-dep-ios.md)。

## <a name="renew-a-dep-token"></a>更新 DEP 權杖  
1. 前往 deploy.apple.com。  
2. 在 [管理伺服器]  下，選擇與您所欲更新之權杖檔案相關的 MDM 伺服器。
3. 選擇 [產生新權杖]  。

    ![產生新權杖的螢幕擷取畫面。](./media/device-enrollment-program-enroll-ios/generatenewtoken.png)

4. 選擇 [您的伺服器權杖]  。  
5. 在 [Microsoft 端點管理員系統管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)中，選擇 [裝置]   > [iOS]   > [iOS 註冊]   > [註冊方案權杖]  > 選擇權杖。
    ![註冊計劃權杖的螢幕擷取畫面。](./media/device-enrollment-program-enroll-ios/enrollmentprogramtokens.png)

6. 選擇 [更新權杖]**Renew token**，然後輸入用於建立原始權杖的 Apple ID。  
    ![產生新權杖的螢幕擷取畫面。](./media/device-enrollment-program-enroll-ios/renewtoken.png)

8. 上傳新下載的權杖。  
9. 選擇 [更新權杖]  。 您會看到權杖已更新的確認。   
    ![確認的螢幕擷取畫面。](./media/device-enrollment-program-enroll-ios/confirmation.png)
