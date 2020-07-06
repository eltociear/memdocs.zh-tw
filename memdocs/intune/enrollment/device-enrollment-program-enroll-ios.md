---
title: 註冊 iOS/iPadOS 裝置 - 自動裝置註冊
titleSuffix: Microsoft Intune
description: 了解如何使用自動裝置註冊來註冊公司擁有的 iOS/iPadOS 裝置。
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 02/04/2020
ms.topic: how-to
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
ms.openlocfilehash: 8fe0b1748a40858bca55cc66b250c96725bfd9f1
ms.sourcegitcommit: 411e9d93cbafc7585f5a0f9a05097fe589de804f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/24/2020
ms.locfileid: "85332876"
---
# <a name="automatically-enroll-iosipados-devices-with-apples-automated-device-enrollment"></a>使用 Apple 的自動裝置註冊來自動註冊 iOS/iPadOS 裝置

> [!IMPORTANT]
> Apple 在最近將 Apple 裝置註冊計劃 (DEP) 變更為 Apple 自動裝置註冊 (ADE)。 Intune 正在更新 Intune 使用者介面以應對這項變更。 在變更完成之前，您仍會繼續在 Intune 入口網站中看到「裝置註冊計劃」。 無論顯示的名稱為何，您現在所使用的皆為「自動裝置註冊」。

您可以設定 Intune 註冊透過 Apple [自動裝置註冊 (ADE)](https://deploy.apple.com) 購買的 iOS/iPadOS 裝置。 自動裝置註冊能夠自動地幫助您註冊大量裝置。 iPhone、iPad 與 MacBook 等裝置可直接交付給使用者。 當使用者開啟裝置電源時，會以預先設定的設定來執行設定助理 (包括 Apple 產品的典型全新體驗)，並註冊裝置以接受管理。

若要啟用 ADE，您可同時使用 Intune 與 [Apple Business Manager (ABM)](https://business.apple.com/) 或 [Apple School Manager (ASM)](https://school.apple.com/) 入口網站。 您需要序號或採購單編號的清單，才能在上述任一個 Apple 入口網站中將裝置指派給 Intune 進行管理。 您可在 Intune 中建立 ADE 註冊設定檔，其中包含已在註冊期間套用至裝置的設定。 ADE 無法與[裝置註冊管理員](device-enrollment-manager-enroll.md)帳戶一起使用。

> [!NOTE]
> ADE 會設定終端使用者無法移除的裝置設定。 因此，在[移轉至 ADE](../fundamentals/migration-guide-considerations.md) 之前，必須先抹除裝置，讓裝置回復為出廠 (全新) 狀態。

## <a name="automated-device-enrollment-and-the-company-portal"></a>自動裝置註冊與公司入口網站

ADE 註冊與公司入口網站應用程式的 App Store 版本不相容。 您可為使用者提供 ADE 裝置上公司入口網站應用程式的存取權。 您可以提供此存取權，讓使用者選擇他們要在其裝置上使用的公司應用程式，或使用新式驗證來完成註冊程序。 

若要在註冊期間啟用新式驗證，請使用 ADE 設定檔中的 [使用 VPP 安裝公司入口網站] 將應用程式推送至裝置。 如需詳細資訊，請參閱[使用 Apple 的 ADE 來自動註冊 iOS/iPadOS 裝置](device-enrollment-program-enroll-ios.md#create-an-apple-enrollment-profile)。

若要讓公司入口網站自動更新，並在已向 ADE 註冊的裝置上提供公司入口網站應用程式，請透過 Intune 將公司入口網站應用程式部署為必要的大量採購方案 (VPP) 應用程式，並套用[應用程式設定原則](../apps/app-configuration-policies-use-ios.md)。

## <a name="what-is-supervised-mode"></a>何謂受監督模式？

Apple 在 iOS/iPadOS 5 中引進受監管模式。 您可以使用更多控制措施管理受監管模式中的 iOS/iPadOS 裝置，例如封鎖螢幕畫面擷取及封鎖從 App Store 安裝應用程式。 因此，它特別適用於公司擁有的裝置。 Intune 支援針對受監督模式設定裝置，以作為 ADE 的一部分。

iOS/iPadOS 11 中對非監督式 ADE 裝置的支援已淘汰。 在 iOS/iPadOS 11 與更新版本中，應一律監督 ADE 設定裝置。 使用 iOS/iPadOS 13.0 和更新版本時，將會忽略 ADE *is_supervised* 旗標。 使用自動裝置註冊進行註冊時，會自動監督所有使用 13.0 版和更新版本的 iOS/iPadOS 裝置。 

<!--
**Steps to enable enrollment programs from Apple**
1. [Get an Apple DEP token and assign devices](#get-the-apple-dep-token)
2. [Create an enrollment profile](#create-an-apple-enrollment-profile)
3. [Synchronize DEP-managed devices](#sync-managed-device)
4. [Assign DEP profile to devices](#assign-an-enrollment-profile-to-devices)
5. [Distribute devices to users](#end-user-experience-with-managed-devices)
-->
## <a name="prerequisites"></a>先決條件
- 在 [Apple 的 ADE](https://deploy.apple.com) 中購買的裝置
- [行動裝置管理 (MDM) 授權單位](../fundamentals/mdm-authority-set.md)
- [Apple MDM Push Certificate](apple-mdm-push-certificate-get.md)

## <a name="supported-volume"></a>支援的磁碟區

- 每個權杖的註冊設定檔上限：1,000  
- 每個設定檔的 Automated Device Enrollment 裝置上限：無限制 (在每個權杖的裝置數目上限內)
- 每個 Intune 帳戶的 Automated Device Enrollment 權杖上限：2,000
- 每個權杖的 Automated Device Enrollment 裝置數目上限：第一次同步的限制為 75,000 到 80,000 個裝置。 Intune 將會每隔 12 小時簽入來持續與 ABM 或 ASM 同步，且每次都會新增額外 80,000 個裝置。 手動同步也會再度新增額外 80,000 個裝置。 同步將會持續發生，且裝置將會持續以 75,000 到 80,000 個裝置的批次從 ABM/ASM 同步到 Intune。 

## <a name="get-an-apple-ade-token"></a>取得 Apple ADE 權杖

您必須先從 Apple 取得 ADE 權杖 (.p7m) 檔案，才能使用 ADE 註冊 iOS/iPadOS 裝置。 此權杖可讓 Intune 同步公司所擁有的 ADE 裝置資訊。 它也允許 Intune 將註冊設定檔上傳至 Apple，並將這些設定檔指派給裝置。

您可使用 [Apple Business Manager (ABM)](https://business.apple.com/) 或 [Apple School Manager (ASM)](https://school.apple.com/) 入口網站來建立權杖。 您也可以使用 ABM/ASM 入口網站將裝置指派給 Intune 進行管理。

> [!NOTE]
> 若在移轉至 Azure 之前從 Intune 傳統入口網站刪除了權杖，則 Intune 可能會還原已刪除的 Apple ADE 權杖。 您可從 Azure 入口網站再次刪除該 ADE 權杖。

### <a name="step-1-download-the-intune-public-key-certificate-required-to-create-the-token"></a>步驟 1： 下載建立權杖所需的 Intune 公開金鑰憑證。

1. 在 [Microsoft Endpoint Manager 系統管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)中，選擇 [裝置] > [iOS/iPadOS] > [iOS/iPadOS 註冊]。

    ![取得註冊計劃權杖。](./media/device-enrollment-program-enroll-ios/ios-enroll.png)

2. 選擇 [註冊方案權杖] > [新增]。

3. 藉由選取 [我同意] 來將權限授與 Microsoft，以將使用者和裝置資訊傳送給 Apple。

   > [!NOTE]
   > 當您在步驟 2 之後下載 Intune 公開金鑰憑證後，請勿關閉精靈或巡覽出這個頁面。 這麼做會讓您下載的憑證失效，而必須重複此程序。 如果遇到此狀況，則您通常會注意到 [檢閱 + 建立] 索引標籤上的 [建立] 按鈕呈現灰色，而無法完成此程序。

   ![[Apple 憑證] 工作區中 [註冊計劃權杖] 窗格下載公開金鑰的螢幕擷取畫面。](./media/device-enrollment-program-enroll-ios/add-enrollment-program-token-pane.png)

4. 選擇 [下載您的公開金鑰]，在本機下載並儲存加密金鑰 (.pem) 檔案。 這個 .pem 檔案會用於向 Apple 入口網站要求信任關係憑證。


### <a name="step-2-use-your-key-to-download-a-token-from-apple"></a>步驟 2： 使用您的金鑰，下載來自 Apple 的權杖。

1. 選擇 [Create a token for via Apple Business Manager] \(透過 Apple Business Manager 建立權杖\)，開啟 Apple 的商業入口網站，並使用公司 Apple ID 登入。 您可使用此 Apple ID 來更新 ADE 權杖。
2. 在 Apple 的[商業入口網站](https://business.apple.com)內，選擇 [裝置註冊計劃] 中的 [開始使用]。

3. 在 [管理伺服器] 頁面上，選擇 [新增 MDM 伺服器]。
4. 輸入 [MDM 伺服器名稱]，然後選擇 [下一步] 。 您可參考這個伺服器名稱，以識別行動裝置管理 (MDM) 伺服器， 但它不是 Microsoft Intune 伺服器的名稱或 URL。

5. [新增 &lt;服器名稱&gt;] 對話方塊隨即開啟，指出**上傳您的公用金鑰**。 選取 [選擇檔案] 以上傳 .pem 檔案，然後選擇 [下一步]。

6. 移至 [部署計劃] &gt; [裝置註冊計劃] &gt; [管理裝置]。
7. 在 [選擇裝置依據] 下，指定識別裝置的方式：
    - **序號**
    - **訂單號碼**
    - **上傳 CSV 檔案**。

   ![指定依據序號選擇裝置、將選擇的動作設定為 [指派給伺服器]，然後選取伺服器名稱的螢幕擷取畫面。](./media/device-enrollment-program-enroll-ios/enrollment-program-token-specify-serial.png)

8. 針對 [選擇動作] 選擇 [Assign to Server] (指派給伺服器))，然後選擇指定給 Microsoft Intune 的 &lt;伺服器名稱&gt;，再選擇 [確定]。 Apple 入口網站會將指定的裝置指派給 Intune 伺服器以便管理 ，然後顯示 [指派完成]。

   在 Apple 入口網站中，移至 [部署計劃] &gt; [裝置註冊計劃] &gt; [檢視指派歷程記錄] 以查看裝置與其 MDM 伺服器指派的清單。

### <a name="step-3-save-the-apple-id-used-to-create-this-token"></a>步驟 3： 儲存用以建立此權杖的 Apple ID。

在 [Microsoft Endpoint Manager 系統管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)內，提供 Apple ID 供日後參考。

![指定要用於建立註冊計劃權杖的 Apple 識別碼，並瀏覽至註冊計劃權杖的螢幕擷取畫面。](./media/device-enrollment-program-enroll-ios/image03.png)

### <a name="step-4-upload-your-token-and-choose-scope-tags"></a>步驟 4： 上傳權杖，然後選擇範圍標籤。

1. 在 [Apple 權杖] 方塊中，瀏覽至憑證 (.p7m) 檔案，選擇 [開啟]。
2. 如果您想要將[範圍標籤](../fundamentals/scope-tags.md)套用到這個 DEP 權杖中，請選擇 [範圍 (標籤)]，然後選取您想要的範圍標籤。 新增到此權杖的設定檔和裝置會繼承套用到權杖的範圍標籤。
3. 選擇 **[建立]** 。

使用推播憑證，透過將原則推送到已註冊的行動裝置，Intune 即可註冊及管理 iOS/iPadOS 裝置。 Intune 會自動與 Apple 同步處理，以查看您的註冊計劃帳戶。

## <a name="create-an-apple-enrollment-profile"></a>建立 Apple 註冊設定檔

安裝權杖之後，即可為 ADE 裝置建立註冊設定檔。 裝置註冊設定檔會定義要在註冊期間套用至裝置群組的設定。 每個 ADE 權杖只能擁有最多 100 個註冊設定檔。

> [!NOTE]
> 如果 VPP 權杖沒有足夠的公司入口網站授權，或如果權杖已過期，將會封鎖裝置。 當權杖即將到期或授權偏低時，Intune 將會顯示警示。
 

1. 在 [Microsoft Endpoint Manager 系統管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)中，選擇 [裝置] > [iOS/iPadOS] > [iOS/iPadOS 註冊] > [註冊方案權杖]。
2. 選取權杖，選擇 [設定檔] > [建立設定檔] > [iOS/iPadOS]。

    ![[建立設定檔] 螢幕擷取畫面。](./media/device-enrollment-program-enroll-ios/image04.png)

3. 在 [基本] 頁面上，為設定檔輸入系統管理用的**名稱**與**描述**。 使用者看不到這些詳細資料。 

    ![設定檔名稱與描述。](./media/device-enrollment-program-enroll-ios/image05.png)

4. 選取 [下一步:裝置管理設定]。

5. 針對 [使用者親和性]，為具備此設定檔的裝置選擇需要或不需要由指派的使用者來進行註冊。
    - **搭配使用者親和性進行註冊** - 針對屬於使用者的裝置，以及想要使用公司入口網站進行像是安裝應用程式等服務的裝置，選擇此選項。 如果您使用 ADFS 且使用 [設定助理] 來進行驗證，[WS-Trust 1.3 使用者名稱/混合端點](https://technet.microsoft.com/library/adfs2-help-endpoints) [(深入了解)](https://technet.microsoft.com/itpro/powershell/windows/adfs/get-adfsendpoint) 是必要的。

    - **不搭配使用者親和性進行註冊** - 針對未與任何使用者相關的裝置選擇此選項。 對於不會存取本機使用者資料與 Apple Shared iPad for Business 裝置的裝置，請使用此選項。 公司入口網站應用程式類的應用程式無法運作。

6. 如果您選擇 [搭配使用者親和性進行註冊]，則可以讓使用者使用公司入口網站進行驗證，而不是 Apple 設定輔助程式。

    ![使用公司入口網站進行驗證。](./media/device-enrollment-program-enroll-ios/authenticatewithcompanyportal.png)

    > [!NOTE]
    > 如果您想要執行下列任何一項，請將 [選取使用者在何處必須進行驗證] 設定為 [公司入口網站]。
    >    - 使用多重要素驗證
    >    - 提示第一次登入時必須變更密碼的使用者
    >    - 提示使用者在註冊期間重設其過期密碼
    >
    > 使用 Apple 設定輔助程式進行驗證時，不支援這些功能。

7. 如果您針對 [選取使用者在何處必須進行驗證] 選擇 [公司入口網站]，則可以使用 VPP 權杖自動在裝置上安裝公司入口網站。 在此情況下，使用者不需要提供 Apple ID。 若要使用 VPP 安裝公司入口網站，請在 [使用 VPP 安裝公司入口網站] 下選擇權杖。 要求已將公司入口網站新增至 VPP 權杖。 為確保公司入口網站應用程式在註冊後會繼續更新，請確定已在 Intune 中設定應用程式部署 ([Intune] > [用戶端應用程式])。 如此即不需要使用者互動。您很可能希望公司入口網站能像 iOS/iPadOS VPP 應用程式一樣、將其設為必要應用程式，並使用裝置授權進行指派。 請確定權杖未過期，而且您有足夠的公司入口網站應用程式裝置授權。 如果權杖過期或授權不足，則 Intune 會改為安裝 App Store 公司入口網站，並提示您輸入 Apple ID。 

    > [!NOTE]
    > 當 [選取使用者在何處必須進行驗證] 是 [公司入口網站] 時，請確定裝置註冊程序會在公司入口網站下載至 ADE 裝置的前 24 小時內執行。 否則註冊可能會失敗，而且需要重設成出廠預設值才能註冊裝置。
    
    ![[使用 VPP 安裝公司入口網站] 的螢幕擷取畫面。](./media/device-enrollment-program-enroll-ios/install-cp-with-vpp.png)

8. 如果您為 [選取使用者在何處必須進行驗證] 選擇 [設定輔助程式]，但您也想要使用條件式存取或在裝置上部署公司應用程式，您必須在裝置上安裝公司入口網站。 若要這樣做，請為 [安裝公司入口網站] 選擇 [是]。  如果您想要讓使用者接收公司入口網站，而不需要向 App Store 進行驗證，請選擇 [使用 VPP 安裝公司入口網站] 並選取 VPP 權杖。 請確定權杖未過期，而且您有足夠的公司入口網站應用程式裝置授權來正確部署。

9. 如果您為 [使用 VPP 安裝公司入口網站] 選擇權杖，您可以在設定輔助程式完成之後，立即以單一應用程式模式 (具體來說就是公司入口網站應用程式) 鎖定裝置。 在 [Run Company Portal in Single App Mode until authentication] \(驗證前以單一應用程式模式執行公司入口網站\) 選擇 [是]，設定此選項。 若要使用裝置，使用者必須先使用公司入口網站登入進行驗證。

    在鎖定於單一應用程式模式的單一裝置上，不支援多重要素驗證。 此限制存在的原因是，裝置無法切換至不同的應用程式以完成第二個驗證要素。 因此，如果您想要在單一應用程式模式裝置上進行多重要素驗證，第二個要素必須位於不同的裝置上。

    iOS/iPadOS 11.3.1 與更新版本才支援此功能。

   ![單一應用程式模式的螢幕擷取畫面。](./media/device-enrollment-program-enroll-ios/single-app-mode.png)

10. 如果您想要監督使用此設定檔的裝置，請為 [受監督] 選擇 [是]。

    ![裝置管理設定螢幕擷取畫面。](./media/device-enrollment-program-enroll-ios/supervisedmode.png)

    **受監督**裝置可提供您更多管理選項，並且預設會停用 [啟用鎖定]。 Microsoft 建議使用 ADE 作為啟用受監管模式的機制，尤其是在部署大量的 iOS/iPadOS 裝置時。 Apple Shared iPad for Business 裝置必須受到監督。

    有兩種方式可通知使用者其裝置收到監督：

   - 鎖定畫面顯示：「此 iPhone 受 Contoso 管理。」
   - [設定] > [一般] > [關於] 畫面顯示：「此 iPhone 受監督。 Contoso 可以監視您的網際網路流量並找到此裝置。」

     > [!NOTE]
     > 註冊為不受監督的裝置，僅可透過使用 Apple Configurator 重設為受監督。 以這種方式將裝置重設，需要使用 USB 纜線將 iOS/iPadOS 裝置連接至 Mac。 在 [Apple Configurator 文件](http://help.apple.com/configurator/mac/2.3)上，深入了解這項作業。

11. 選擇您是否想要針對使用此設定檔的裝置鎖定註冊。 **鎖定的註冊**會停用可將管理設定檔從 [設定] 功能表中移除的 iOS/iPadOS 設定。 註冊裝置之後，必須抹除裝置才能變更此設定。 這類裝置必須將**受監督**管理模式設為 [是]。 

    > [!NOTE]
    > 使用 [鎖定註冊] 註冊裝置之後，使用者將無法在公司入口網站應用程式中使用 [移除裝置] 或 [恢復出廠預設值]。 使用者將無法使用這些選項。 使用者也無法在公司入口網站 (https://portal.manage.microsoft.com) 中移除裝置。
    > 此外，如果 BYOD 裝置已轉換為 Apple Automated Device Enrollment 裝置，並使用已啟用 [鎖定註冊] 的設定檔進行註冊，則使用者將可使用 [移除裝置] 和 [恢復出廠預設值] 30 天，然後這些選項就會停用或無法使用。 參考： https://help.apple.com/configurator/mac/2.8/#/cad99bc2a859 。

12. 若您選擇 [不使用使用者親和性註冊] 與 [受監督]，您必須決定是否要將裝置設定為 [Apple Shared iPad for Business 裝置](https://support.apple.com/guide/mdm/shared-ipad-overview-cad7e2e0cf56/web)。 透過針對 [Shared iPad] 選擇 [是]，多個使用者將能夠登入相同的裝置。 使用者會使用其受控 Apple ID 與同盟驗證帳戶，或透過暫時工作階段 (亦即來賓帳戶) 來進行驗證。 此選項需要 iOS/iPadOS 13.4 或更新版本。

    若您選擇將裝置設定為 Apple Shared iPad for Business 裝置，您必須設定 [快取的使用者人數上限]。 將此值設定為您預期會使用 Shared iPad 的使用者數目。 在 32 GB 或 64 GB 的裝置上，您最多可快取 24 位使用者。 若您選擇非常低的數目，在登入之後，您的使用者資料可能需要一些時間才能進入裝置。 若您選擇非常高的數目，您的使用者可能沒有足夠的磁碟空間。  

    > [!NOTE]
    > 若您要設定 Apple Shared iPad for Business，請設定下列各項： 
    > - [使用者親和性] = [不使用使用者親和性註冊]。 
    > - [受監督] = [是]。 
    > - [Shared iPad] = [是]****。
    > 根據預設，會啟用暫時工作階段，並允許您的使用者不使用受控 Apple ID 帳戶登入 Shared iPad。 您可以透過設定 iOS/iPadOS Shared iPad [裝置限制設定](../configuration/device-restrictions-ios.md)，停用 Shared iPad 的暫時工作階段。  

13. 選擇您是否想要讓使用此設定檔的裝置**與電腦同步**。 若選擇 [依據憑證允許 Apple Configurator]，則必須在 [Apple Configurator 憑證] 下選擇憑證。

     > [!NOTE]
     > 如果 [與電腦同步] 設定為 [全部拒絕]，則連接埠將會在 iOS 和 iPadOS 裝置上受到限制。 連接埠只能用於充電，而沒有其他用途。 連接埠將遭到封鎖，而無法使用 iTunes 或 Apple Configurator 2。
     如果 [與電腦同步] 設定為 [依憑證允許 Apple Configurator]，請確認您有憑證的本機複本，以便稍後存取。 您無法對上傳的複本進行變更，因此請務必保留此憑證以供日後存取。 若要從 macOS 裝置或電腦連線到 iOS/iPadOS 裝置，您必須在裝置上安裝相同的憑證，才能連線到已透過此設定與憑證向自動裝置註冊設定檔註冊的 iOS/iPadOS 裝置。

14. 若您在前一個步驟中選擇 [依據憑證允許 Apple Configurator]，則請選擇要匯入的 Apple Configurator 憑證。

15. 您可以指定裝置的命名格式，以在其註冊時和每次後續簽入時自動套用。 若要建立命名範本，請在 [套用裝置名稱範本] 下選取 [是]。 然後，在 [裝置名稱範本] 方塊中，輸入要用於使用此設定檔之名稱的範本。 您可以指定包括裝置類型與序號的範本格式。 

16. 選擇 [下一步:設定助理自訂]。

17. 在 [設定助理自訂] 頁面上，設定下列設定檔設定：![設定助理自訂。](./media/device-enrollment-program-enroll-ios/setupassistantcustom.png)


    | 部門設定 | 說明 |
    |---|---|
    | <strong>部門名稱</strong> | 使用者在啟用期間點選 [關於設定] 時顯示。 |
    |    <strong>部門電話</strong>     | 在使用者在啟用期間按一下 [需要協助] 按鈕時顯示。 |

    在使用者安裝期間，您可以選擇隱藏裝置上的 [設定助理] 畫面。
    - 如果您選擇 [隱藏]，則不會在設定期間顯示畫面。 設定好裝置之後，使用者仍然可以進入 [設定] 功能表來設定此功能。
    - 如果您選擇 [顯示]，將會在設定期間顯示畫面。 使用者有時可以跳過畫面而不採取動作。 但是他們隨後可以進入裝置的 [設定] 功能表來設定此功能。 


    | 設定助理畫面設定 | 如果您選擇 [顯示]，裝置會在設定期間... |
    |------------------------------------------|------------------------------------------|
    | <strong>密碼</strong> | 提示使用者輸入密碼。 除非以其他方式控制存取 (例如，將裝置限制為單一應用程式的 Kiosk 模式)，否則未受到保護的裝置一律需要密碼。 適用於 iOS/iPadOS 7.0 與更新版本。 |
    | <strong>位置服務</strong> | 提示使用者輸入其位置。 適用於 macOS 10.11 與更新版本，以及 iOS/iPadOS 7.0 與更新版本。 |
    | <strong>還原</strong> | 顯示 [應用程式與資料] 畫面。 此畫面可讓使用者選擇在設定裝置時，要從 iCloud 備份還原或傳送資料。 適用於 macOS 10.9 與更新版本，以及 iOS/iPadOS 7.0 與更新版本。 |
    | <strong>iCloud 與 Apple ID</strong> | 提供讓使用者選擇使用其 Apple ID 登入並使用 iCloud 的選項。 適用於 macOS 10.9 與更新版本，以及 iOS/iPadOS 7.0 與更新版本。   |
    | <strong>條款和條件</strong> | 需要使用者接受 Apple 的條款及條件。 適用於 macOS 10.9 與更新版本，以及 iOS/iPadOS 7.0 與更新版本。 |
    | <strong>Touch ID</strong> | 可讓使用者選擇設定裝置的指紋識別。 適用於 macOS 10.12.4 與更新版本，以及 iOS/iPadOS 8.1 與更新版本。 |
    | <strong>Apple Pay</strong> | 可讓使用者選擇在裝置上設定 Apple Pay。 適用於 macOS 10.12.4 與更新版本，以及 iOS/iPadOS 7.0 與更新版本。 |
    | <strong>縮放</strong> | 可讓使用者選擇在設定裝置時縮放顯示畫面。 適用於 iOS/iPadOS 8.3 與更新版本。 |
    | <strong>Siri</strong> | 可讓使用者選擇設定 Siri。 適用於 macOS 10.12 與更新版本，以及 iOS/iPadOS 7.0 與更新版本。 |
    | <strong>診斷資料</strong> | 向使用者顯示 [診斷] 畫面。 此畫面可讓使用者選擇將診斷資料傳送給 Apple。 適用於 macOS 10.9 與更新版本，以及 iOS/iPadOS 7.0 與更新版本。 |
    | <strong>顯示色調</strong> | 可讓使用者選擇開啟 [顯示色調]。 適用於 macOS 10.13.6 與更新版本，以及 iOS/iPadOS 9.3.2 與更新版本。 |
    | <strong>隱私權</strong> | 向使用者顯示 [隱私權] 畫面。 適用於 macOS 10.13.4 與更新版本，以及 iOS/iPadOS 11.3 與更新版本。 |
    | <strong>Android 移轉</strong> | 可讓使用者選擇從 Android 裝置移轉日期。 適用於 iOS/iPadOS 9.0 與更新版本。|
    | <strong>iMessage 和 FaceTime</strong> | 提供使用者選擇設定 iMessage 與 FaceTime 的選項。 適用於 iOS/iPadOS 9.0 與更新版本。 |
    | <strong>入門訓練</strong> | 顯示用於使用者教育的入門訓練資訊畫面，例如封面頁及多工和控制中心。 適用於 iOS/iPadOS 11.0 與更新版本。 |
    | <strong>Watch 移轉</strong> | 可讓使用者選擇從監看式裝置移轉資料。 適用於 iOS/iPadOS 11.0 與更新版本。|
    | <strong>螢幕使用時間</strong> | 顯示 [螢幕使用時間] 畫面。 適用於 macOS 10.15 與更新版本，以及 iOS/iPadOS 12.0 與更新版本。 |
    | <strong>軟體更新</strong> | 顯示強制軟體更新畫面。 適用於 iOS/iPadOS 12.0 與更新版本。 |
    | <strong>SIM 卡設定</strong> | 可讓使用者選擇新增行動電話通訊方案。 適用於 iOS/iPadOS 12.0 與更新版本。 |
    | <strong>外觀</strong> | 向使用者顯示 [外觀] 畫面。 適用於 macOS 10.14 與更新版本，以及 iOS/iPadOS 13.0 與更新版本。 |
    | <strong>快速語言</strong>| 向使用者顯示 [快速語言] 畫面。 |
    | <strong>慣用語言</strong> | 提供使用者選擇其**慣用語言**的選項。 |
    | <strong>裝置到裝置的移轉</strong> | 提供使用者將資料從舊裝置移轉到此裝置的選項。 適用於 iOS/iPadOS 13.0 與更新版本。 |
    | <strong>註冊</strong> | 向使用者顯示註冊畫面。 適用於 macOS 10.9 與更新版本。 |
    | <strong>FileVault</strong> | 向使用者顯示 FileVault 2 加密畫面。 適用於 macOS 10.10 與更新版本。 |
    | <strong>iCloud 診斷</strong> | 向使用者顯示 iCloud 分析畫面。 適用於 macOS 10.12.4 與更新版本。 |
    | <strong>iCloud 儲存空間</strong> | 向使用者顯示 iCloud 文件及桌面畫面。 適用於 macOS 10.13.4 與更新版本。 |
    

18. 選擇 [下一步] 以移至 [檢閱 + 建立] 頁面。

19. 若要儲存該設定檔，請選擇 [建立]。

### <a name="dynamic-groups-in-azure-active-directory"></a>Azure Active Directory 中的動態群組

您可以使用註冊 [名稱] 欄位，在 Azure Active Directory 中建立動態群組。 如需詳細資訊，請參閱 [Azure Active Directory 動態群組](/azure/active-directory/users-groups-roles/groups-dynamic-membership)。

您可以使用設定檔名稱來定義 [enrollmentProfileName 參數](/azure/active-directory/users-groups-roles/groups-dynamic-membership#rules-for-devices)，以註冊具備此註冊設定檔的裝置。

若要在具備使用者親和性的 ADE 裝置上取得最快的原則傳遞，請確定註冊的使用者在裝置設定之前已經是 AAD 使用者群組的成員。 

將動態群組指派至註冊設定檔，可能會在註冊後將應用程式與原則傳遞至裝置時導致些許延遲。


## <a name="sync-managed-devices"></a>同步受管理裝置
由於 Intune 有管理您裝置的權限，您可以同步處理 Intune 與 Apple，以在 Azure 入口網站的 Intune 中查看受管理裝置。

1. 在 [Microsoft Endpoint Manager 系統管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)中，選擇 [裝置] > [iOS/iPadOS] > [iOS/iPadOS 註冊] > [註冊方案權杖]。

2. 在清單中選擇權杖 > [裝置]>[同步]。![[註冊計劃裝置] 節點與 [同步] 連結的螢幕擷取畫面。](./media/device-enrollment-program-enroll-ios/image06.png)

   為遵循 Apple 條款內所規定的註冊計劃流量，Intune 具有下列限制︰
   - 完整同步處理每 7 天只能執行一次。 在完整同步期間，Intune 會擷取指派至已連線 Intune 之 Apple MDM 伺服器的序號完整更新清單。 如果從 Intune 入口網站刪除 ADE 裝置，則應該從 ADE 入口網站中的 Apple MDM 伺服器取消指派 ADE 裝置。 如果未解除指派，則在執行完整同步之前，不會將它重新匯入至 Intune。   
   - 每 12 小時會自動同步一次。 您也可以按一下 [同步] 按鈕來進行同步 (請勿在 15 分鐘內重複點選)。 所有同步要求都必須在 15 分鐘內完成。 [同步] 按鈕在同步完成前都會處於停用狀態。 此同步會重新整理現有的裝置狀態，以及匯入指派至 Apple MDM 伺服器的新裝置。   


## <a name="assign-an-enrollment-profile-to-devices"></a>將註冊設定檔指派給裝置
必須先將註冊計劃設定檔指派至裝置，裝置才能註冊。

>[!NOTE]
>您也可以從 [Apple 序號] 刀鋒視窗中，將序號指派給設定檔。

1. 在 [Microsoft Endpoint Manager 系統管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)中，選擇 [裝置] > [iOS/iPadOS] > [iOS/iPadOS 註冊] > [註冊方案權杖] > 在清單中選擇權杖。
2. 選擇 [裝置] > 選擇清單中的裝置 > [指派設定檔]。
3. 在 [指派設定檔] 下，選擇裝置的設定檔 > [指派]。

### <a name="assign-a-default-profile"></a>指派預設設定檔

您可以針對使用特定權杖註冊的所有裝置，挑選要套用的預設設定檔。

1. 在 [Microsoft Endpoint Manager 系統管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)中，選擇 [裝置] > [iOS/iPadOS] > [iOS/iPadOS 註冊] > [註冊方案權杖] > 在清單中選擇權杖。
2. 選擇 [設定預設設定檔]、在下拉式清單中選擇設定檔，然後選擇 [儲存]。 此設定檔將套用到使用該權杖註冊的所有裝置。

## <a name="distribute-devices"></a>散發裝置
您已啟用 Apple 與 Intune 之間的管理和同步，並指派設定檔以供 ADE 裝置註冊。 您現在可以將裝置散發給使用者。 具有使用者親和性的裝置會需要為每個使用者指派 Intune 授權。 沒有使用者親和性的裝置需要裝置授權。 在抹除裝置前，已啟用的裝置無法套用註冊設定檔。

請參閱[以裝置註冊計劃在 Intune 註冊 iOS/iPadOS 裝置](../user-help/enroll-your-device-dep-ios.md)。

## <a name="renew-an-ade-token"></a>更新 ADE 權杖  

> [!NOTE]
> 除了每年更新 ADE 權杖之外，當在 Apple Business Manager 中設定權杖的使用者變更 Managed Apple ID 密碼時，或該使用者離開 Apple Business Manager 組織時，您也必須在 Intune 和 Apple Business Manager 中更新註冊計劃權杖。

1. 前往 business.apple.com。  
2. 在 [管理伺服器] 下，選擇與您所欲更新之權杖檔案相關的 MDM 伺服器。
3. 選擇 [產生新權杖]。

    ![產生新權杖的螢幕擷取畫面。](./media/device-enrollment-program-enroll-ios/generatenewtoken.png)

4. 選擇 [您的伺服器權杖]。  
5. 在 [Microsoft Endpoint Manager 系統管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)中，選擇 [裝置] > [iOS/iPadOS] > [iOS/iPadOS 註冊] > [註冊方案權杖] > 選擇權杖。
    ![註冊計劃權杖的螢幕擷取畫面。](./media/device-enrollment-program-enroll-ios/enrollmentprogramtokens.png)

6. 選擇 [更新權杖]**Renew token**，然後輸入用於建立原始權杖的 Apple ID。  
    ![產生新權杖的螢幕擷取畫面。](./media/device-enrollment-program-enroll-ios/renewtoken.png)

7. 選取 [下一步]，以移至 [範圍標籤] 頁面，並視需要指派範圍標籤。

8. 選取 [下一步] 並上傳新下載的權杖。  
9. 選擇 [更新權杖]。 您會看到權杖已更新的確認。   
    ![確認的螢幕擷取畫面。](./media/device-enrollment-program-enroll-ios/confirmation.png)

## <a name="delete-an-ade-token-from-intune"></a>從 Intune 刪除 ADE 權杖

您可以從 Intune 刪除註冊設定檔權杖，只要
- 未將任何裝置指派給權杖
- 未將任何裝置指派給預設設定檔

1. 在 [Microsoft 端點管理員系統管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)內，選擇 [裝置] > [iOS/macOS] > [iOS/macOS 註冊] > [註冊計劃權杖] > 選擇權杖 > [裝置]。
2. 刪除已指派給權杖的所有裝置。
3. 移至 [裝置] > [iOS/macOS] > [iOS/macOS 註冊] > [註冊計劃權杖] > 選擇權杖 > [設定檔]。
4. 如有預設設定檔，請予以刪除。
5. 移至 [裝置] > [iOS/macOS] > [iOS/macOS 註冊] > [註冊計劃權杖] > 選擇權杖 > [刪除]。
