---
title: 註冊 macOS 裝置 - Apple Business Manager 或 Apple School Manager
titleSuffix: ''
description: 了解如何註冊公司擁有的 macOS 裝置。
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 12/06/2018
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: tisilver
ms.suite: ems
search.appverid: MET150
ms.custom: seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: 196fc4f551596a6146513d25166b1b167aa44186
ms.sourcegitcommit: 302556d3b03f1a4eb9a5a9ce6138b8119d901575
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/27/2020
ms.locfileid: "83986682"
---
# <a name="automatically-enroll-macos-devices-with-the-apple-business-manager-or-apple-school-manager"></a>使用 Apple Business Manager 或 Apple School Manager 自動註冊 macOS 裝置

> [!IMPORTANT]
> Apple 在最近將 Apple 裝置註冊計劃 (DEP) 變更為 Apple 自動裝置註冊 (ADE)。 Intune 正在更新 Intune 使用者介面以應對這項變更。 在變更完成之前，您仍會繼續在 Intune 入口網站中看到「裝置註冊計劃」  。 無論顯示的名稱為何，您現在所使用的皆為「自動裝置註冊」。

您可以為透過 Apple [Apple Business Manager](https://business.apple.com/) 或 [Apple School Manager](https://school.apple.com/) 購買的 macOS 裝置設定 Intune 註冊。 針對大量裝置，這兩種註冊您都可以使用，且不需要實際取得裝置。 您可以將 macOS 裝置直接寄送給使用者。 當使用者開啟裝置電源時，會以預先設定的設定來執行設定助理，並註冊裝置以接受 Intune 管理。

若要設定註冊，請使用 Intune 和 Apple 入口網站。 您可以建立註冊設定檔，其中包含在註冊期間套用至裝置的設定。

Apple Businesss Manager 註冊或 Apple School Manager 註冊都無法搭配[裝置註冊管理員](device-enrollment-manager-enroll.md)運作。

<!--
**Steps to enable enrollment programs from Apple**
1. [Get an Apple DEP token and assign devices](#get-the-apple-dep-token)
2. [Create an enrollment profile](#create-an-apple-enrollment-profile)
3. [Synchronize DEP-managed devices](#sync-managed-device)
4. [Assign DEP profile to devices](#assign-an-enrollment-profile-to-devices)
5. [Distribute devices to users](#end-user-experience-with-managed-devices)
-->
## <a name="prerequisites"></a>先決條件

- 在 [Apple School Manager](https://school.apple.com/) 或 [Apple 的裝置註冊計劃](http://deploy.apple.com)中購買的裝置
- 序號或採購單號碼的清單。
- [MDM 授權單位](../fundamentals/mdm-authority-set.md)
- [Apple MDM Push Certificate](../enrollment/apple-mdm-push-certificate-get.md)

## <a name="get-an-apple-ade-token"></a>取得 Apple ADE 權杖

您需要 Apple 的 權杖 (.p7m) 檔案，才能使用 ADE 或 Apple School Manager 來註冊 macOS 裝置。 此權杖可讓 Intune 同步處理您組織所擁有的裝置相關資訊。 它也讓 Intune 得以將註冊設定檔上傳至 Apple，並將這些設定檔指定給裝置。

您會使用 Apple 入口網站來建立權杖。 您也可以使用 Apple 入口網站將裝置指派給 Intune 進行管理。

> [!NOTE]
> 若在移轉至 Azure 之前從 Intune 傳統入口網站刪除了權杖，Intune 可能會還原已刪除的 Apple 權杖。 您可以從 Azure 入口網站再次刪除該權杖。

### <a name="step-1-download-the-intune-public-key-certificate-required-to-create-the-token"></a>步驟 1： 下載建立權杖所需的 Intune 公開金鑰憑證

1. 在 [Microsoft 端點管理員系統管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)內，選擇 [裝置]   > [macOS]   > [macOS 註冊]   > [註冊方案權杖]   > [新增]  。

    ![取得註冊計劃權杖。](./media/device-enrollment-program-enroll-macos/image01.png)

2. 藉由選取 [我同意]  來將權限授與 Microsoft，以將使用者和裝置資訊傳送給 Apple。

   ![[Apple 憑證] 工作區中 [註冊計劃權杖] 窗格下載公開金鑰的螢幕擷取畫面。](./media/device-enrollment-program-enroll-macos/add-enrollment-program-token-pane.png)

3. 選擇 [下載您的公開金鑰]  ，在本機下載並儲存加密金鑰 (.pem) 檔案。 這個 .pem 檔案會用於向 Apple 入口網站要求信任關係憑證。

### <a name="step-2-use-your-key-to-download-a-token-from-apple"></a>步驟 2： 使用您的金鑰，下載來自 Apple 的權杖

1. 選擇 [建立 Apple 的裝置註冊計畫的權杖]  或 [透過 Apple School Manager 建立權杖]  來開啟適當的 Apple 入口網站，並使用您的公司 Apple ID 登入。 您可以使用此 Apple ID 來更新您的權杖。
2. 對於 DEP，在 Apple 入口網站中，對於 [裝置註冊計劃]  選擇 [開始使用]   > [管理伺服器]   > [新增 MDM 伺服器]  。
3. 對於 Apple School Manage，在 Apple 入口網站中，選擇 [MDM 伺服器]   > [新增 MDM 伺服器]  。
4. 輸入 [MDM 伺服器名稱]  ，然後選擇 [下一步]  。 您可參考這個伺服器名稱，以識別行動裝置管理 (MDM) 伺服器， 但它不是 Microsoft Intune 伺服器的名稱或 URL。

5. [新增 &lt;服器名稱&gt;]  對話方塊隨即開啟，指出**上傳您的公用金鑰**。 選擇 [選擇檔案...]  以上傳 .pem 檔案，然後選擇 [下一步]  。

6. 移至 [部署計劃]  &gt; [裝置註冊計劃]  &gt; [管理裝置]  。
7. 在 [選擇裝置依據]  下，指定識別裝置的方式：
    - **序號**
    - **訂單號碼**
    - **上傳 CSV 檔案**。

   ![指定依據序號選擇裝置、將選擇的動作設定為 [指派給伺服器]，然後選取伺服器名稱的螢幕擷取畫面。](./media/device-enrollment-program-enroll-macos/enrollment-program-token-specify-serial.png)

8. 針對 [選擇動作]  選擇 [Assign to Server] (指派給伺服器))  ，然後選擇指定給 Microsoft Intune 的 &lt;伺服器名稱&gt;，再選擇 [確定]  。 Apple 入口網站會將指定的裝置指派給 Intune 伺服器以便管理 ，然後顯示 [指派完成]  。

### <a name="step-3-save-the-apple-id-used-to-create-this-token"></a>步驟 3： 儲存用以建立此權杖的 Apple ID

在 [Microsoft 端點管理員系統管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)內，提供 Apple ID 供日後參考。

![指定要用於建立註冊計劃權杖的 Apple 識別碼，並瀏覽至註冊計劃權杖的螢幕擷取畫面。](./media/device-enrollment-program-enroll-macos/image03.png)

### <a name="step-4-upload-your-token"></a>步驟 4： 上傳權杖
在 [Apple 權杖]  方塊中，瀏覽至憑證 (.pem) 檔案，選擇 [開啟]  ，然後選擇 [建立]  。 使用推播憑證，透過將原則推送到已註冊的裝置，Intune 即可註冊及管理 macOS 裝置。 Intune 會自動與 Apple 同步處理，以查看您的註冊計劃帳戶。

## <a name="create-an-apple-enrollment-profile"></a>建立 Apple 註冊設定檔

安裝權杖之後，您可以為裝置建立註冊設定檔。 裝置註冊設定檔會定義要在註冊期間套用至裝置群組的設定。

1. 在 [Microsoft 端點管理員系統管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)內，選擇 [裝置]   > [macOS]   > [macOS 註冊]   > [註冊方案權杖]  。
2. 選取權杖，選擇 [設定檔]  ，然後選擇 [建立設定檔]  。

    ![[建立設定檔] 螢幕擷取畫面。](./media/device-enrollment-program-enroll-macos/image04.png)

3. 在 [建立設定檔]  下，為設定檔輸入系統管理用的**名稱**以及**描述**。 使用者看不到這些詳細資料。 您可以使用此 [名稱]  欄位，在 Azure Active Directory 中建立動態群組。 設定檔名稱可用來定義 enrollmentProfileName 參數，以註冊具備此註冊設定檔的裝置。 深入了解 [Azure Active Directory 動態群組](https://docs.microsoft.com/azure/active-directory/users-groups-roles/groups-dynamic-membership#rules-for-devices)。

    ![設定檔名稱與描述。](./media/device-enrollment-program-enroll-macos/createprofile.png)

4. 針對 [平台]  ，選擇 [macOS]  。

5. 針對 [使用者親和性]  ，為具備此設定檔的裝置選擇需要或不需要由指派的使用者來進行註冊。
    - **搭配使用者親和性進行註冊** - 針對屬於使用者且想要使用公司入口網站 App 進行像是安裝應用程式等服務的裝置，選擇此選項。 若使用 ADFS，則使用者親和性需要 [WS-Trust 1.3 使用者名稱/混合端點](https://technet.microsoft.com/library/adfs2-help-endpoints)。 [深入了解](https://technet.microsoft.com/itpro/powershell/windows/adfs/get-adfsendpoint)。具有使用者親和性的 macOS ADE 裝置不支援多重要素驗證。

    - **不搭配使用者親和性進行註冊** - 針對未與任何使用者相關的裝置選擇此選項。 針對執行工作而不需存取本機使用者資料的裝置使用此選項。 公司入口網站應用程式類的應用程式無法運作。

6. 選擇 [裝置管理設定]  ，並選擇您是否想要針對使用此設定檔的裝置鎖定註冊。 **鎖定的註冊**會停用可將管理設定檔從 [系統喜好設定]  功能表中或透過 [終端機]  移除的 macOS 設定。 註冊裝置之後，必須抹除裝置才能變更此設定。

    ![裝置管理設定螢幕擷取畫面。](./media/device-enrollment-program-enroll-macos/devicemanagementsettingsblade-macos.png)

7. 選擇 [確定]  。

8. 選擇 [設定助理設定]  ，對下列設定檔進行設定：![設定助理自訂。](./media/device-enrollment-program-enroll-macos/setupassistantcustom-macos.png)

    | 部門設定 | 說明 |
    |---|---|
    | <strong>部門名稱</strong> | 使用者在啟用期間點選 [關於設定] 時顯示。 |
    | <strong>部門電話</strong> | 在使用者在啟用期間按一下 [需要協助] 按鈕時顯示。 |

    您可以選擇當使用者設定裝置時，要在裝置上顯示或隱藏各種不同的設定助理畫面。
    - 如果您選擇 [隱藏]  ，則不會在設定期間顯示畫面。 設定好裝置之後，使用者仍然可以進入 [設定]  功能表來設定此功能。
    - 如果您選擇 [顯示]  ，將會在設定期間顯示畫面。 使用者有時可以跳過畫面而不採取動作。 但是他們隨後可以進入裝置的 [設定]  功能表來設定此功能。 

    | 設定助理畫面設定 | 如果您選擇 [顯示]  ，裝置會在設定期間... |
    |------------------------------------------|------------------------------------------|
    | <strong>密碼</strong> | 提示使用者輸入密碼。 除非裝置受到保護，或以其他方式控制存取 (例如，將裝置限制為單一應用程式的 Kiosk 模式)，否則一律需要密碼。 |
    | <strong>位置服務</strong> | 提示使用者輸入其位置。 |
    | <strong>還原</strong> | 顯示 [應用程式與資料] 畫面。 此畫面可讓使用者選擇在設定裝置時，要從 iCloud 備份還原或傳送資料。 |
    | <strong>iCloud 與 Apple ID</strong> | 可讓使用者選擇使用其 **Apple ID** 登入並使用 **iCloud**。                         |
    | <strong>條款和條件</strong> | 需要使用者接受 Apple 的條款及條件。 |
    | <strong>Touch ID</strong> | 可讓使用者選擇設定裝置的指紋識別。 |
    | <strong>Apple Pay</strong> | 可讓使用者選擇在裝置上設定 Apple Pay。 |
    | <strong>縮放</strong> | 可讓使用者選擇在設定裝置時縮放顯示畫面。 |
    | <strong>Siri</strong> | 可讓使用者選擇設定 Siri。 |
    | <strong>診斷資料</strong> | 向使用者顯示 [診斷] 畫面。 此畫面可讓使用者選擇將診斷資料傳送給 Apple。 |
    | <strong>FileVault</strong> | 可讓使用者選擇設定 FileVault 加密。 |
    | <strong>iCloud 診斷</strong> | 可讓使用者選擇將 iCloud 診斷資料傳送給 Apple。 |
    | <strong>iCloud 儲存空間</strong> | 讓使用者能夠選擇使用 iCloud 儲存空間。 |    
    | <strong>顯示色調</strong> | 可讓使用者選擇開啟 [顯示色調]。 |
    | <strong>外觀</strong> | 向使用者顯示 [外觀] 畫面。 |
    | <strong>註冊</strong>| 要求使用者註冊裝置。 |
    | <strong>隱私權</strong>| 向使用者顯示 [隱私權] 畫面。 |
    | <strong>螢幕使用時間</strong>| 向使用者顯示 [螢幕使用時間] 畫面。 |

9. 選擇 [確定]  。

10. 若要儲存該設定檔，請選擇 [建立]  。

## <a name="sync-managed-devices"></a>同步受管理裝置

由於 Intune 有管理您裝置的權限，您可以同步處理 Intune 與 Apple，以在 Azure 入口網站的 Intune 中查看受管理裝置。

1. 在 [Microsoft 端點管理員系統管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)內，選擇 [裝置]  > [macOS]  > **[macOS 註冊]** > [註冊方案權杖]  > 選擇清單中的權杖 > [裝置]  > [同步]  。![選取 [註冊計劃裝置] 節點並選擇 [同步] 連結的螢幕擷取畫面。](./media/device-enrollment-program-enroll-macos/image06.png)

   為了符合 Apple 規定的可接受註冊計劃流量，Intune 具有下列限制︰
   - 完整同步處理每 7 天只能執行一次。 在完整同步期間，Intune 會擷取指派至已連線 Intune 之 Apple MDM 伺服器的序號完整更新清單。 若註冊計劃裝置從 Intune 入口網站刪除，但未從 Apple 入口網站中的 Apple MDM 伺服器解除指派，則在執行完整同步之前，該裝置都不會重新匯入 Intune。   
   - 同步會每 24 小時自動執行一次。 您也可以按一下 [同步]  按鈕來進行同步 (請勿在 15 分鐘內重複點選)。 所有同步要求都必須在 15 分鐘內完成。 [同步]  按鈕在同步完成前都會處於停用狀態。 此同步會重新整理現有的裝置狀態，以及匯入指派至 Apple MDM 伺服器的新裝置。

## <a name="assign-an-enrollment-profile-to-devices"></a>將註冊設定檔指派給裝置

必須先將註冊計劃設定檔指派至裝置，裝置才能註冊。

1. 在 [Microsoft 端點管理員系統管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)內，選擇 [裝置]   > [macOS]   > [macOS 註冊]   > [註冊方案權杖]  > 在清單中選擇權杖。
2. 選擇 [裝置]  > 選擇清單中的裝置 > [指派設定檔]  。
3. 在 [指派設定檔]  下，選擇裝置的設定檔 > [指派]  。

### <a name="assign-a-default-profile"></a>指派預設設定檔

您可以針對使用特定權杖註冊的所有裝置，挑選要套用的預設 macOS 與 iOS/iPadOS 設定檔。 

1. 在 [Microsoft 端點管理員系統管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)內，選擇 [裝置]   > [macOS]   > [macOS 註冊]   > [註冊方案權杖]  > 在清單中選擇權杖。
2. 選擇 [設定預設設定檔]  、在下拉式清單中選擇設定檔，然後選擇 [儲存]  。 此設定檔將套用到使用該權杖註冊的所有裝置。

## <a name="distribute-devices"></a>散發裝置

您已啟用 Apple 與 Intune 之間的管理和同步，並指派設定檔以供您的裝置註冊。 您現在可以將裝置散發給使用者。 具有使用者親和性的裝置會需要為每個使用者指派 Intune 授權。 沒有使用者親和性的裝置需要裝置授權。 在抹除裝置前，已啟動的裝置無法套用註冊設定檔。

## <a name="renew-an-ade-token"></a>更新 ADE 權杖

1. 前往 deploy.apple.com。  
2. 在 [管理伺服器]  下，選擇與您所欲更新之權杖檔案相關的 MDM 伺服器。
3. 選擇 [產生新權杖]  。

    ![產生新權杖的螢幕擷取畫面。](./media/device-enrollment-program-enroll-macos/generatenewtoken.png)

4. 選擇 [您的伺服器權杖]  。  
5. 在 [Microsoft Endpoint Manager 系統管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)內，選擇 [裝置註冊]   > [Apple 註冊]   > [註冊方案權杖]  > 選擇權杖。
    ![註冊計劃權杖的螢幕擷取畫面。](./media/device-enrollment-program-enroll-macos/enrollmentprogramtokens.png)

6. 選擇 [更新權杖]**Renew token**，然後輸入用於建立原始權杖的 Apple ID。  
    ![產生新權杖的螢幕擷取畫面。](./media/device-enrollment-program-enroll-macos/renewtoken.png)

7. 上傳新下載的權杖。  
8. 選擇 [更新權杖]  。 您會看到權杖已更新的確認。
    ![確認的螢幕擷取畫面。](./media/device-enrollment-program-enroll-macos/confirmation.png)

## <a name="next-steps"></a>後續步驟

註冊 macOS 裝置後，您可以開始[管理它們](../remote-actions/device-management.md)。
