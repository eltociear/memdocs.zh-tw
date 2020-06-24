---
title: 使用 Windows Autopilot 註冊裝置
titleSuffix: Microsoft Intune
description: 了解如何使用 Windows Autopilot 來註冊 Windows 10 裝置。
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 05/15/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.technology: ''
ms.assetid: a2dc5594-a373-48dc-ba3d-27aff0c3f944
ms.reviewer: spshumwa
ms.suite: ems
search.appverid: MET150
ms.custom: seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: 5c4b06e8c81e04e067156929dfe7637cf04fb9d1
ms.sourcegitcommit: bc8c9d957dac46d95070c433d3a83408e5e48d82
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/23/2020
ms.locfileid: "85289456"
---
# <a name="enroll-windows-devices-in-intune-by-using-the-windows-autopilot"></a>使用 Windows Autopilot 在 Intune 中註冊 Windows 裝置  
Windows Autopilot 簡化了在 Intune 中註冊裝置的程序。 建置和維護自訂的作業系統映像需要許多時間。 您也可能會花時間將這些自訂的作業系統映像套用至新的裝置，以在送交使用者之前，先將它們做好使用的準備。 使用 Microsoft Intune 和 Autopilot，您可以將新的裝置提供給使用者而不需要建置、維護及套用自訂作業系統映像至裝置。 當您使用 Intune 來管理 Autopilot 裝置時，可以在裝置註冊之後管理原則、設定檔、應用程式等。 如需優點、案例和必要條件的概觀，請參閱 [Windows Autopilot 概觀](https://docs.microsoft.com/windows/deployment/windows-autopilot/windows-10-autopilot)。

Autopilot 部署類型有四種：

- [自我部署模式](https://docs.microsoft.com/windows/deployment/windows-autopilot/self-deploying)適用於 kiosk、數位告示板或共用裝置
- [白手套](https://docs.microsoft.com/windows/deployment/windows-autopilot/white-glove)可讓合作夥伴或 IT 人員預先佈建 Windows 10 電腦，使其能夠完整設定並可供企業使用
- [適用於現有裝置的 Autopilot](https://docs.microsoft.com/windows/deployment/windows-autopilot/existing-devices) (機器翻譯) 可讓您輕鬆地將最新版本的 Windows 10 部署到現有裝置
- [使用者驅動模式](https://docs.microsoft.com/windows/deployment/windows-autopilot/user-driven)適用於傳統使用者。

本文說明如何設定 Windows 電腦的 Autopilot。 如需 Autopilot 與 HoloLens 的詳細資訊，請參閱[適用於 HoloLens 2 的 Windows Autopilot](https://docs.microsoft.com/hololens/hololens2-autopilot)。

## <a name="prerequisites"></a>先決條件

- [Intune 訂用帳戶](../fundamentals/licenses.md)
- [已啟用 Windows 自動註冊](windows-enroll.md#enable-windows-10-automatic-enrollment)
- [Azure Active Directory Premium 訂用帳戶](https://docs.microsoft.com/azure/active-directory/active-directory-get-started-premium) <!--&#40;[trial subscription](https://go.microsoft.com/fwlink/?LinkID=816845)&#41;-->

## <a name="how-to-get-the-csv-for-import-in-intune"></a>如何在 Intune 中取得 CSV 以進行匯入

如需詳細資訊，請參閱＜了解 PowerShell Cmdlet＞。

- [Get-WindowsAutoPilotInfo](https://www.powershellgallery.com/packages/Get-WindowsAutoPilotInfo)

## <a name="add-devices"></a>新增裝置

您可以藉由匯入含 Windows Autopilot 裝置資訊的 CSV 檔案來新增它們。

1. 在 [Microsoft Endpoint Manager 系統管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)內，選擇 [裝置] > [Windows] > [Windows 註冊] > [裝置] (在 [Windows AutoPilot Deployment Program] > [匯入] 底下)。

    ![Windows Autopilot 裝置的螢幕擷取畫面](./media/enrollment-autopilot/autopilot-import-device.png)

2. 在 [新增 Windows Autopilot 裝置] 下，瀏覽至列出所要新增裝置的 CSV 檔案。 該 CSV 檔案應列出序號、Windows 產品識別碼、硬體雜湊、選擇性群組標籤與選擇性指派的使用者。 您最多可在清單中建立 500 個資料列。 如需如何取得裝置資訊的相關資訊，請參閱[將裝置新增至 Windows Autopilot](https://docs.microsoft.com/windows/deployment/windows-autopilot/add-devices#device-identification) \(部分機器翻譯\)。 使用下面顯示的標題和行格式：

    `Device Serial Number,Windows Product ID,Hardware Hash,Group Tag,Assigned User`</br>
    `<serialNumber>,<ProductID>,<hardwareHash>,<optionalGroupTag>,<optionalAssignedUser>`

    ![新增 Windows Autopilot 裝置的螢幕擷取畫面](./media/enrollment-autopilot/autopilot-import-device2.png)

    >[!IMPORTANT]
    > 當您使用 CSV 上傳來指派使用者時，請確定您已指派有效的 UPN。 如果您指派了無效的 UPN (不正確的使用者名稱)，則在移除無效的指派之前，您的裝置可能無法存取。 在 CSV 上傳期間，我們在 [指派的使用者] 欄上執行的唯一驗證是檢查網域名稱是否有效。 我們無法執行個別 UPN 驗證，以確保您指派的是現有或正確的使用者。

3. 選擇 [匯入] 開始匯入裝置資訊。 匯入可能需要幾分鐘的時間。

4. 匯入完成之後，選擇 [裝置] > [Windows] > [Windows 註冊] > [裝置] \(在 [Windows AutoPilot Deployment Program] 底下\) > [同步]。訊息會顯示正在進行同步處理。 程序可能需要幾分鐘才能完成，取決於有多少裝置正在進行同步處理。

5. 重新整理檢視可查看新的裝置。

## <a name="create-an-autopilot-device-group"></a>建立 Autopilot 裝置群組

1. 在 [Microsoft Endpoint Manager 系統管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)內，選擇 [群組] > [新增群組]。
2. 在 [群組] 刀鋒視窗中：
    1. 針對 [群組類型]，請選擇 [安全性]。
    2. 輸入**群組名稱**與**群組描述**。
    3. 針對 [成員資格類型]，選擇 [已指派] 或是 [動態裝置]。
3. 如果您在上一步中針對 [成員資格類型] 選擇 [已指派] ，請在 [群組] 刀鋒視窗中選擇 [成員] 並將 Autopilot 裝置新增至群組。
    尚未註冊的 Autopilot 裝置為裝置名稱與序號相同的裝置。
4. 如果針對上述的 [成員資格類型] 選擇 [動態裝置]，請在 [群組] 刀鋒視窗中選擇 [動態裝置成員] ，然後在 [進階規則] 方塊中輸入下列任意一項代碼。 這些規則只會收集 Autopilot 裝置，因為其目標屬性僅由 Autopilot 裝置所擁有。 根據非 Autopilot 屬性建立群組，並無法保證包含在該群組中的裝置實際上會註冊至 Autopilot。
    - 若要建立包含您所有 Autopilot 裝置的群組，請輸入：`(device.devicePhysicalIDs -any (_ -contains "[ZTDId]"))`
    - Intune 的群組標籤欄位會對應至 Azure AD 裝置上的 OrderID 屬性。 若要建立包含具特定群組標籤 (Azure AD 裝置 OrderID) 之所有 Autopilot 裝置的群組，您必須輸入：`(device.devicePhysicalIds -any _ -eq "[OrderID]:179887111881")`
    - 若建立的群組要包含具有特定採購單識別碼的所有 Autopilot 裝置，請鍵入：`(device.devicePhysicalIds -any _ -eq "[PurchaseOrderId]:76222342342")`
    
    新增 [進階規則] 代碼後，選擇 [儲存]。
5. 選擇 **[建立]** 。  

## <a name="create-an-autopilot-deployment-profile"></a>建立 Autopilot 部署設定檔
Autopilot 部署設定檔會用來設定 Autopilot 裝置。 您可以為每個租用戶建立最多 350 個設定檔。
1. 在 [Microsoft 端點管理員系統管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)中，選擇 [裝置] > [Windows] > [Windows 註冊] > [部署設定檔] > [建立設定檔] > [Windows 電腦] 或 [HoloLens]。 本文說明如何設定 Windows 電腦的 Autopilot。 如需 Autopilot 與 HoloLens 的詳細資訊，請參閱[適用於 HoloLens 2 的 Windows Autopilot](https://docs.microsoft.com/hololens/hololens2-autopilot)。
2. 在 [基本] 頁面上，輸入**名稱**和選擇性的**描述**。

    ![[基本] 頁面的螢幕擷取畫面](./media/enrollment-autopilot/create-profile-basics.png)

3. 若您想指派群組中所有的裝置自動轉換至 Autopilot，請將 [將所有目標裝置轉換至 Autopilot] 設為 [是]。 指派群組中所有屬公司擁有的非 Autopilot 裝置都會向 Autopilot 部署服務註冊。 個人擁有的裝置將不會轉換成 Autopilot。 等候 48 小時讓註冊處理完畢。 當裝置取消註冊並重設時，Autopilot 將會自動註冊它。 在裝置使用此方式註冊完畢後，停用此選項或是移除設定檔指派也不會從 Autopilot 部署服務移除裝置。 您必須改為[直接移除裝置](enrollment-autopilot.md#delete-autopilot-devices)。
4. 選取 [下一步]。
5. 在 [首次體驗 (OOBE)] 頁面上，針對 [部署模式] 選擇這兩個選項的其中一個：
    - **使用者驅動**：具有此設定檔的裝置會與註冊裝置的使用者相關聯。 需有使用者認證，才能註冊裝置。
    - **自我部署 (預覽)** ：(需要 Windows 10 1809 版或更新版本) 具有此設定檔的裝置不會與註冊裝置的使用者建立關聯。 不需要使用者認證，也能註冊裝置。 當裝置沒有與其建立關聯的使用者時，則不會套用以使用者為基礎的合規性政策。 使用自我部署模式時，只會套用以裝置為目標的合規性政策。

    ![[OOBE] 頁面的螢幕擷取畫面](./media/enrollment-autopilot/create-profile-outofbox.png)

   > [!NOTE]
   > 選取的部署模式目前不支援變暗或呈現陰影的選項。

6. 在 [加入Azure AD] 方塊中，選擇 [已加入 Azure AD]。
7. 設定下列選項：
    - **使用者授權合約 (EULA)** ：(Windows 10，版本 1709 或更新版本) 選擇是否要向使用者顯示授權合約。
    - **隱私權設定**：選擇是否要向使用者顯示隱私權設定。
    >[!IMPORTANT]
    >[診斷資料] 設定的預設值在 Windows 版本之間各有不同。 就執行 Windows 10 1903 版的裝置而言，在全新體驗期間，預設值會設定為 [完整]。 如需詳細資訊，請參閱 [Windows 診斷資料](https://docs.microsoft.com/windows/privacy/windows-diagnostic-data) <br>
    
    - **隱藏變更帳戶選項 (需要 Windows 10 1809 版或更新版本)** ：選擇 [隱藏] 以防止在公司登入和網域錯誤頁面上顯示變更帳戶選項。 此選項需要[在 Azure Active Directory 中設定公司商標](https://docs.microsoft.com/azure/active-directory/fundamentals/customize-branding)。
    - **使用者帳戶類型**：選擇使用者的帳戶類型 ([系統管理員] 或 [標準] 使用者)。 我們藉由將裝置加入本機系統管理員群組，讓使用者能夠將其加入本機系統管理員。 我們不會讓使用者成為裝置上的預設系統管理員。
    - **允許 White Glove OOBE** (需要 Windows 10 1903 版或更新版本；[其他實體需求](https://docs.microsoft.com/windows/deployment/windows-autopilot/white-glove#prerequisites) \(部分機器翻譯\))：選擇 [是] 以允許 White Glove 支援。
    - **套用裝置名稱範本** (需要 Windows 10 1809 版或更新版本，以及 Azure AD 聯結類型)：選擇 [是] 以建立要在註冊期間命名裝置時使用的範本。 名稱必須是 15 個字元或更少，而且可以包含字母、數字和連字號。 名稱不可以全部為數字。 使用 [%SERIAL% 巨集](https://docs.microsoft.com/windows/client-management/mdm/accounts-csp)新增硬體特定序號。 或者，使用 [%RAND:x% 巨集](https://docs.microsoft.com/windows/client-management/mdm/accounts-csp)新增隨機數字字串，其中 x 等於要新增的位數。 您只能在[網域加入設定檔](windows-autopilot-hybrid.md#create-and-assign-a-domain-join-profile)中，為混合式裝置提供預先修正。 
    - **語言 (地區)** \*：選擇要為裝置使用的語言。 僅當您針對 [部署模式] 選擇 [自我部署] 時，此選項才可使用。
    - **自動設定鍵盤**\*：如果選取了 [語言 (區域)]，請選擇 [是] 跳過鍵盤選取頁面。 僅當您針對 [部署模式] 選擇 [自我部署] 時，此選項才可使用。
8. 選取 [下一步]。
9. 在 [範圍標籤] 頁面上，您可以選擇新增您想要套用到此設定檔的範圍標籤。 如需範圍標籤的詳細資訊，請參閱[針對分散式 IT 使用角色型存取控制和範圍標籤](../fundamentals/scope-tags.md)。
10. 選取 [下一步]。
11. 在 [指派] 頁面上，針對 [指派至] 選擇 [選取的群組]。

    ![[指派] 頁面的螢幕擷取畫面](./media/enrollment-autopilot/create-profile-assignments.png)

12. 選擇 [選取要納入的群組]，然後選擇您要納入此設定檔的群組。
13. 如果您想要排除任何群組，請選擇 [選取要排除的群組]，然後選擇要排除的群組。
14. 選取 [下一步]。
15. 在 [檢閱 + 建立] 頁面上，選擇 [建立] 以建立設定檔。

    ![[檢閱] 頁面的螢幕擷取畫面](./media/enrollment-autopilot/create-profile-review.png)

> [!NOTE]
> Intune 將會定期檢查指派的群組中是否有新裝置，然後開始將設定檔指派給這些裝置的程序。 此程序可能需要幾分鐘的時間才能完成。 部署裝置之前，請確定此程序已完成。  您可以在 [裝置] > [Windows] > [Windows 註冊] > [裝置] \(在 [Windows Autopilot Deployment Program] 底下\) 下檢查，您應該會看到設定檔狀態從 [未指派] 變更為 [指派中]，最後變更為 [已指派]。

## <a name="edit-an-autopilot-deployment-profile"></a>編輯 Autopilot 部署設定檔
建立 Autopilot 部署設定檔之後，您可以編輯部署設定檔的某些部分。   

1. 在 [Microsoft Endpoint Manager 系統管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)內，選擇 [裝置] > [Windows] > [Windows 註冊] > [部署設定檔]。
2. 選取您想要編輯的設定檔。
3. 選取左邊的 [屬性]，變更部署設定檔的名稱或描述。 進行變更之後請按一下 [儲存]。
5. 按一下 [設定] 以變更 OOBE 設定。 進行變更之後請按一下 [儲存]。

> [!NOTE]
> 設定檔的變更會套用至指派給該設定檔的裝置。 不過，更新的設定檔不會套用到已在 Intune 註冊的裝置，直到裝置已重設並重新註冊為止。

## <a name="edit-autopilot-device-attributes"></a>編輯 Autopilot 裝置屬性
上傳 Autopilot 裝置之後，您可以編輯裝置的特定屬性。

1. 在 [Microsoft Endpoint Manager 系統管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)內，選取 [裝置] > [Windows] > [Windows 註冊] > [裝置] (在 [Windows AutoPilot Deployment Program] 底下)。
2. 選取您要編輯的裝置。
3. 在畫面右邊的窗格中，您可以編輯裝置名稱、群組標籤或使用者易記名稱 (如果您已指派使用者)。
4. 選取 [儲存]。

> [!NOTE]
> 可以針對所有裝置設定裝置名稱，但會在已加入混合式 Azure AD 部署中予以忽略。 裝置名稱仍然是來自混合式 Azure AD 裝置的網域加入設定檔。

## <a name="alerts-for-windows-autopilot-unassigned-devices-----163236---"></a>Windows Autopilot 未指派裝置的警示  <!-- 163236 -->  

警示會顯示有多少 Autopilot 程式裝置沒有 Autopilot 部署設定檔。 您可以使用警示中的資訊來建立設定檔，並加以指派至未指派的裝置。 當您按一下警示時，會看到 Windows Autopilot 裝置的完整清單，以及這些裝置的詳細資訊。

若要查看未指派裝置的警示，請在 [Microsoft Endpoint Manager 系統管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)內，選擇 [裝置] > [概觀] > [註冊警示] > [未指派的裝置]。  

## <a name="autopilot-deployments-report"></a>Autopilot 部署報告
您可以查看透過 Windows Autopilot 部署之每個裝置的詳細資料。
若要查看報告，請移至 [Microsoft Endpoint Manager 系統管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)，選擇 [裝置] > [監視器] > [Autopilot 部署]。
該資料會在部署後的 30 天內提供使用。

此報告為預覽狀態。 目前只有新的 Intune 註冊事件才會觸發裝置部署記錄。 這表示此報告不會選擇任何不會觸發新的 Intune 註冊的部署。 這包括維護註冊的任何一種重設，以及 Autopilot 服務周全方式的使用者部分。

## <a name="assign-a-user-to-a-specific-autopilot-device"></a>將使用者指派給特定 Autopilot 裝置

您可以將使用者指派給特定 Autopilot 裝置。 此指派會在 Windows 安裝期間，[公司自創的](https://docs.microsoft.com/azure/active-directory/fundamentals/customize-branding)登入頁面上，預先填入 Azure Active Directory 中的使用者。 它也可讓您設定自訂問候語名稱。 它不會預先填入或修改 Windows 登入。 只有具授權的 Intune 使用者可以透過此方式指派。

必要條件：已設定 Azure Active Directory 公司入口網站，並具有 Windows 10 1809 版或更新版本。

> [!NOTE]
> 如果您使用 ADFS，則無法將使用者指派給特定的 Autopilot 裝置。

1. 在 [Microsoft Endpoint Manager 系統管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)內，選擇 [裝置] > [Windows] > [Windows 註冊] > [裝置] (在 [Windows AutoPilot Deployment Program] 底下) > 選擇裝置 > [指派使用者]。

    ![指派使用者的螢幕擷取畫面](./media/enrollment-autopilot/assign-user.png)

2. 選擇授權使用 Intune 的 Azure 使用者並選擇 [選取]。

    ![選取使用者的螢幕擷取畫面](./media/enrollment-autopilot/select-user.png)

3. 在 [User Friendly Name] \(使用者易記名稱\) 方塊中，鍵入易記名稱或直接接受預設值。 此字串是使用者在 Windows 安裝期間登入時顯示的易記名稱。

    ![易記名稱的螢幕擷取畫面](./media/enrollment-autopilot/friendly-name.png)

4. 選擇 [確定]。


## <a name="delete-autopilot-devices"></a>刪除 Autopilot 裝置

您可以刪除未向 Intune 註冊的 Windows Autopilot 裝置：

- 將裝置從 Windows Autopilot 刪除，位置在 [裝置] > [Windows] > [Windows 註冊] > [裝置] \(在 [Windows AutoPilot Deployment Program] 底下\)。 選擇您要刪除的裝置，然後選擇 [刪除]。 刪除 Windows Autopilot 裝置可能需要幾分鐘的時間才會完成。

您必須刪除 Intune 裝置、Azure Active Directory 裝置及 Windows Autopilot 裝置記錄，才能將裝置完全從您的租用戶移除。 這全都可以從 Intune 執行：

1. 如果裝置已在 Intune 中註冊，則必須先[從 Intune [所有裝置] 刀鋒視窗刪除](../remote-actions/devices-wipe.md#delete-devices-from-the-azure-active-directory-portal)。

2. 若要刪除 Azure Active Directory 裝置中的裝置，請前往 [裝置] > [Azure AD 裝置]。

3. 將裝置從 Windows Autopilot 刪除，位置在 [裝置] > [Windows] > [Windows 註冊] > [裝置] \(在 [Windows AutoPilot Deployment Program] 底下\)。 選擇您要刪除的裝置，然後選擇 [刪除]。 刪除 Windows Autopilot 裝置可能需要幾分鐘的時間才會完成。

## <a name="using-autopilot-in-other-portals"></a>在其他入口網站中使用 Autopilot
如果您對行動裝置管理不感興趣，則可以在其他入口網站中使用 Autopilot。 雖然可以選擇使用其他入口網站，我們建議您只使用 Intune 來管理 Autopilot 部署。 如果您使用 Intune 與另一個入口網站，Intune 將無法：  

- 顯示在 Intune 中建立但在另一個入口網站中編輯的設定檔變更
- 同步處理在另一個入口網站中建立的設定檔
- 顯示在另一個入口網站中進行的設定檔指派變更
- 同步處理在另一個入口網站中進行的設定檔指派
- 顯示在另一個入口網站中完成的裝置清單變更

## <a name="windows-autopilot-for-existing-devices"></a>適用於現有裝置的 Windows Autopilot

您可以在透過 Configuration Manager 使用[適用於現有裝置的 Autopilot](https://techcommunity.microsoft.com/t5/Windows-IT-Pro-Blog/New-Windows-Autopilot-capabilities-and-expanded-partner-support/ba-p/260430)註冊時，以交互識別碼來將 Windows 裝置分組
。 交互識別碼是 Autopilot 設定檔的參數。 [Azure AD 裝置屬性 enrollmentProfileName](https://docs.microsoft.com/azure/active-directory/users-groups-roles/groups-dynamic-membership#rules-for-devices) 會自動設為相等的 "OfflineAutopilotprofile-\<correlator ID\>correlator ID"。 這會允許使用 enrollmentprofileName 屬性，根據交互識別碼建立任意 Azure AD 動態群組。

>[!WARNING] 
> 因為交互識別碼並未在 Intune 中預先列出，裝置可能會回報任何其希望的交互識別碼。 若使用者建立與 Autopilot 或 Apple ADE 設定檔名稱相符的交互識別碼，則裝置會新增至任何根據 enrollmentProfileName 屬性的動態 Azure AD 裝置群組。 若要避免此衝突：
> - 一律建立與「整個」enrollmentProfileName 值比對的動態群組規則
> - 永遠不要將 Autopilot 或 Apple ADE 設定檔命名為開頭是 "OfflineAutopilotprofile-" 的名稱。

## <a name="next-steps"></a>後續步驟
您為已註冊的 Windows 10 裝置設定 Windows Autopilot 之後，請了解如何管理這些裝置。 如需詳細資訊，請參閱[什麼是 Microsoft Intune 裝置管理？](../remote-actions/device-management.md)
