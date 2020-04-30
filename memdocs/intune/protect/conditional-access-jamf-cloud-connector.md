---
title: 整合Jamf Pro Cloud Connector 與 Microsoft Intune
titleSuffix: Microsoft Intune
description: 使用 Jamf Cloud Connector 搭配具有 Azure Active Directory 條件式存取的 Microsoft Intune 合規性原則，協助整合及保護 Jamf 受控的裝置。
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 04/13/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: arnab
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: f86b418df46069b2a33dd56d06e0e82dbbbf8090
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81538445"
---
# <a name="use-the-jamf-cloud-connector-with-microsoft-intune"></a>使用 Jamf Cloud Connector 搭配 Microsoft Intune

本文可協助您安裝 Jamf Cloud Connector，以整合 Jamf Pro 與 Microsoft Intune。 Cloud Connector 會自動執行您手動設定整合時所需的許多步驟，如[將 Jamf Pro 與 Intune 整合以取得合規性](../protect/conditional-access-integrate-jamf.md)所記載。

當您設定 Cloud Connector 時：

- 設定會自動在 Azure 中建立 Jamf Pro 應用程式，並取代手動設定的需求。
- 您可以整合 Jamf Pro 的多個執行個體與裝載 Intune 訂用帳戶的同一個 Azure 租用戶。

只有當您使用 Cloud Connector 時，才支援使用單一 Azure 租用戶來連線 Jamf Pro 的多個執行個體。 當您使用手動設定的連線時，只有單一 Jamf 執行個體可與 Azure 租用戶整合。

Cloud Connector 的使用是選擇性的：

- 對於尚未與 Jamf 整合的新租用戶，您可選擇如本文所述來設定 Cloud Connector。 或者，您可以手動設定整合，如[將 Jamf Pro 與 Intune 整合以取得合規性](../protect/conditional-access-integrate-jamf.md)所述
- 對於已手動設定的租用戶，您可選擇移除該整合，然後設定 Cloud Connector。 本文會說明如何移除現有整合及設定 Cloud Connector。

如果您打算取代先前與 Jamf Cloud Connector 的整合：

- 使用[移除目前設定的程序](#remove-the-jamf-pro-integration-for-a-previously-configured-tenant)，包括刪除 Jamf Pro 的企業應用程式，以及停用手動整合。 接著，您可使用[設定 Cloud Connector 的程序](#configure-the-cloud-connector-for-a-new-tenant)。
- 您不需要重新註冊裝置。 已經註冊的裝置不需額外設定，即可使用 Cloud Connecto。
- 請務必在 24 小時內設定 Cloud Connector 移除您的手動整合，以確保已註冊的裝置可以繼續報告其狀態。

如需 Jamf Cloud Connector 的詳細資訊，請參閱 docs.jamf.com 上的[使用 Cloud Connector 設定 macOS Intune 整合](https://docs.jamf.com/technical-papers/jamf-pro/microsoft-intune/10.17.0/Configuring_the_macOS_Intune_Integration_using_the_Cloud_Connector.html)。

## <a name="prerequisites"></a>先決條件

**產品與服務**：  
- Jamf Pro 10.18 或更新版本
- 具有條件式存取權限的 Jamf Pro 使用者帳戶  
- Microsoft Intune
- Microsoft Azure AD Premium
- [macOS 版公司入口網站應用程式](https://aka.ms/macoscompanyportal)
- 具有 OS X 10.12 Yosemite 或更新版本的 macOS 裝置

**網路**：  
必須能夠存取下列連接埠和端點，才能正確地整合 Jamf 與 Intune：

- **Intune**：連接埠 443
- **Apple**：連接埠 2195、2196 和 5223 (將通知推播至 Intune)
- **Jamf**：連接埠 80 和 5223

- 端點：
  - login.microsoftonline.com
  - graph.windows.net  
  - *.manage.microsoft.com  

若要讓 APNS 能在網路上正確運作，您也必須啟用連出連線，以及從下列連接埠重新導向：

- 來自所用戶端的 Apple 17.0.0.0/8 區塊 (在 TCP 連接埠 5223 與 443)。
- 來自 Jamf Pro 伺服器的連接埠 2195 與 2196。

如需有關這些連接埠的詳細資訊，請參閱下列文章：

- [Intune 網路設定需求與頻寬](../fundamentals/network-bandwidth-use.md)。
- jamf.com 上 [Jamf Pro 使用的網路連接埠](https://www.jamf.com/jamf-nation/articles/34/network-ports-used-by-jamf-pro) \(英文\)。
- support.apple.com 網站上的 [Apple 軟體產品使用的 TCP 和 UDP 連接埠](https://support.apple.com/HT202944)

**帳戶**：  
本文中的程序需要使用具有下列權限的帳戶：

- **Jamf Pro 主控台**：有權管理 Jamf Pro 的帳戶
- **Microsoft 端點管理系統管理中心**：全域管理員
- **Azure 入口網站**：全域管理員

## <a name="remove-the-jamf-pro-integration-for-a-previously-configured-tenant"></a>為先前設定的租用戶移除 Jamf Pro 整合

使用下列程序，「先」  從您的 Azure 租用戶中移除手動設定的 Jamf Pro 整合，您才能設定 Cloud Connector。

如果您先前尚未設定 Jamf Pro 與 Intune 之間的連線，或如果您有一或多個已使用 Cloud Connector 的連線，請略過此程序並從[為新的租用戶設定 Cloud Connector](#configure-the-cloud-connector-for-a-new-tenant) 著手。

### <a name="remove-a-manually-configured-jamf-pro-integration"></a>移除手動設定的 Jamf Pro 整合

1. 登入 Jamf Pro 主控台。

2. 選取 [設定]  (右上角的齒輪圖示)，然後移至 [全域管理]   > [條件式存取]  。

   ![導覽至條件式存取](./media/conditional-access-jamf-cloud-connector/navigate-jamf-console-1.png)

3. 選取 [編輯]  。

4. 取消選取 [啟用 macOS 的 Intune 整合]  核取方塊。

   取消選取此設定時，您會停用連線，但會儲存設定。

5. 登入 [Microsoft 端點管理員系統管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)，並移至 [租用戶系統管理]   > [合作夥伴裝置管理]  。

   在 [合作夥伴裝置管理]  節點上，刪除 [指定 Jamf 的 Azure Active Directory 應用程式識別碼]  欄位中的 [應用程式識別碼]  ，然後選取 [儲存]  。

   當您設定 Jamf Pro 的手動整合時，應用程式識別碼就是在 Azure 中所建立 Azure 企業應用程式的識別碼。

6. 使用具有全域系統管理員權限的帳戶登入 [Azure 入口網站](https://portal.azure.com/)，並移至 [Azure Active Directory]   > [企業應用程式]  。

   找出兩個 Jamf 應用程式並予以刪除。 當您在下一個程序中設定 Jamf Cloud Connector 時，系統將會自動建立新的應用程式。

   ![選取要刪除的 Jamf 應用程式](./media/conditional-access-jamf-cloud-connector/delete-jamf-apps.png)

   在 Jamf Pro 中停用整合並刪除企業應用程式之後，[合作夥伴裝置管理]  節點會顯示 [已終止]  連線狀態。

   ![終止的連線狀態](./media/conditional-access-jamf-cloud-connector/terminated-connection-status.png)

既然您已成功移除 Jamf Pro 整合的手動設定，即可使用 Cloud Connector 來設定整合。 若要這麼做，請參閱本文中的[為新的租用戶設定 Cloud Connector](#configure-the-cloud-connector-for-a-new-tenant)。

## <a name="configure-the-cloud-connector-for-a-new-tenant"></a>為新的租用戶設定 Cloud Connector

使用下列程序，將 Jamf Cloud Connector 設定為在下列情況下整合 Jamf Pro 與 Microsoft Intune：

- 您並未針對 Azure 租用戶在 Jamf Pro 與 Intune 之間設定任何整合。
- 您已在 Azure 租用戶中的 Jamf Pro 與 Intune 之間設定 Cloud Connector，並想要整合額外的 Jamf 執行個體與您的訂用帳戶。

如果您目前在 Intune 與 Jamf Pro 之間有手動設定的整合，請參閱本文中的[為先前設定的租用戶移除 Jamf Pro 整合](#remove-the-jamf-pro-integration-for-a-previously-configured-tenant)來移除該整合，再繼續執行。 您必須先移除手動設定的整合，才能成功地設定 Jamf Cloud Connector。

### <a name="create-a-new-connection"></a>建立新的連線

1. 登入 Jamf Pro 主控台。

2. 選取 [設定]  (右上角的齒輪圖示)，然後移至 [全域管理]   > [條件式存取]  。

   ![導覽至條件式存取](./media/conditional-access-jamf-cloud-connector/navigate-jamf-console-1.png)

3. 選取 [編輯]  。

4. 選取 [啟用 macOS 的 Intune 整合]  核取方塊。
   - 選取此設定，讓 Jamf Pro 將清查更新傳送至 Microsoft Intune。
   - 您可以取消選取此設定來停用連線，但會儲存設定。

   > [!IMPORTANT]
   > 如果已選取 [啟用 macOS 的 Intune 整合]  ，且 [連線類型]  已設定為 [手動]  ，您就必須先移除該整合，才能繼續執行。 繼續執行之前，請參閱本文中的[為先前設定的租用戶移除 Jamf Pro 整合](#remove-the-jamf-pro-integration-for-a-previously-configured-tenant)。

5. 在 [連線類型]  底下，選取 [Cloud Connector]  。

   ![在 Jamf Pro 主控台中選取 Cloud Connector](./media/conditional-access-jamf-cloud-connector/select-cloud-connector.png)

6. 從 [主權雲端]  快顯功能表，選取 Microsoft 中您的主權雲端位置。

7. 對於 Microsoft Azure 無法辨識的電腦，選取下列其中一個登陸頁面選項：
   - **預設 Jamf Pro 裝置註冊頁面**：視 macOS 裝置的狀態而定，此選項會將使用者重新導向至 Jamf Pro 裝置註冊入口網站 (以向 Jamf Pro 註冊) 或 Intune 公司入口網站應用程式 (以向 Azure AD 註冊)。
   - **拒絕存取頁面**
   - **自訂 URL**

8. 選取 [連線]  。 系統會將您重新導向以在 Azure 中註冊 Jamf Pro 應用程式。

   出現提示時，請指定您的 Microsoft Azure 認證，並遵循畫面上的指示來授與所要求的權限。 您將授與 [Cloud Connector]  的權限，然後再次授與 [Cloud Connector 使用者註冊應用程式]  的權限。 這兩個應用程式都會在 Azure 中註冊為企業應用程式。

   授與這兩個應用程式的權限之後，[應用程式識別碼]  頁面隨即開啟。

9. 在 [應用程式識別碼]  頁面上，選取 [複製並開啟 Intune]  。

   ![應用程式識別碼](./media/conditional-access-jamf-cloud-connector/copy-application-id.png)

   [應用程式識別碼]  會複製到系統剪貼簿，以供下一個步驟使用，而 [Microsoft 端點管理員系統管理中心]  中的 [合作夥伴裝置管理]  節點會開啟。 ([租用戶管理]   > [合作夥伴裝置管理]  )。

10. 在 [合作夥伴裝置管理]  節點上，將 [應用程式識別碼]  貼到  [指定 Jamf 的 Azure Active Directory 應用程式識別碼]  欄位中，然後選取 [儲存]  。

    ![設定合作夥伴裝置管理](./media/conditional-access-jamf-cloud-connector/partner-device-management.png)

11. 返回 Jamf Pro 中的 [應用程式識別碼] 頁面，然後選取 [確認]  。

12. Jamf Pro 會完成並測試設定，而且在 [條件式存取設定] 頁面上顯示連線成功或失敗。 下圖為成功範例：

    ![已在 Jamf Pro 中確認設定成功](./media/conditional-access-jamf-cloud-connector/successful-configuration.png)

13. 在 Microsoft 端點管理員系統管理中心，重新整理 [合作夥伴裝置管理]  節點。 連線現在應該會顯示為 [作用中]  ：

    ![連線狀態為作用中](./media/conditional-access-jamf-cloud-connector/active-connection-status.png)

成功建立 Jamf Pro 與 Microsoft Intune 之間的連線時，Jamf Pro 會針對已向 Azure AD 註冊的每部電腦 (向 Azure AD 註冊是終端使用者工作流程)，將清查資訊傳送至 Microsoft Intune。 您可以在 Jamf Pro 中電腦清查資訊的 [本機使用者帳戶] 類別中，檢視使用者和電腦的條件式存取清查狀態。

使用 Jamf Cloud Connector 整合 Jamf Pro 的一個執行個體之後，您可使用此相同程序，在您的 Azure 租用戶中設定具有相同 Intune 訂用帳戶的 Jamf Pro 額外執行個體。  

## <a name="set-up-compliance-policies-and-register-devices"></a>設定合規性原則並註冊裝置

設定 Intune 和 Jamf 之間的整合後，您需要[將合規性政策套用至 Jamf 受控裝置](../protect/conditional-access-assign-jamf.md)。

## <a name="disconnect-jamf-pro-and-intune"></a>中斷 Jamf Pro 和 Intune 的連線

如果您需要移除 Jamf Pro 與 Intune 的整合，請使用下列步驟，從 Jamf Pro 主控台內移除連線。此資訊適用於 Cloud Connector 和手動設定的整合。

1. 在 Jamf Pro 中，移至 [全域管理]   > [條件式存取]  。 在 [macOS Intune 整合]  索引標籤上，選取 [編輯]  。

2. 清除 [啟用 macOS 的 Intune 整合]  核取方塊。

3. 選取 [儲存]  。 Jamf Pro 會將您的設定傳送至 Intune 並終止整合。

4. 登入 [Microsoft Endpoint Manager 系統管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)。

5. 選取 [租用戶系統管理]   > [連接器與權杖]   > [夥伴裝置管理]  ，以驗證狀態現為 [已終止]  。

   > [!NOTE]
   > 您組織的 Mac 裝置將會在主控台中顯示的日期 (3 個月) 移除。

## <a name="get-support-for-the-cloud-connector"></a>取得 Cloud Connector 的支援

由於 Cloud Connector 會自動建立整合所需的 Azure 企業應用程式，因此第一個支援聯繫點應該是 **Jamf**。 這些選項包括：

- 傳送電子郵件給支援小組 (`support@jamf.com`)
- 使用 Jamf Nation 的支援入口網站： https://www.jamf.com/support/ 


聯繫支援小組之前：

- 檢閱必要條件，例如您使用的連接埠和產品版本。
- 確認尚未修改在 Azure 中建立的下列兩個 Jamf Pro 應用程式的權限。 Intune 不支援變更應用程式權限，因為這可能會導致整合失敗。

  **Cloud Connector 使用者註冊應用程式**：
  - API 名稱：Microsoft Graph
    - 權限：登入和讀取使用者設定檔
    - 類型：已委派
    - 授與管道：系統管理員同意
    - 授與者：系統管理員

  **Cloud Connector 應用程式**：
  - API 名稱：Microsoft Graph (執行個體 1)
    - 權限：登入和讀取使用者設定檔
    - 類型：已委派
    - 授與管道：系統管理員同意
    - 授與者：系統管理員

  - API 名稱：Microsoft Graph (執行個體 2)
    - 權限：讀取目錄資料
    - 類型：應用程式
    - 授與管道：系統管理員同意
    - 授與者：系統管理員

  - API 名稱：Intune API
    - 權限：將裝置屬性傳送至 Microsoft Intune
    - 類型：應用程式
    - 授與管道：系統管理員同意
    - 授與者：系統管理員

## <a name="common-questions-about-the-jamf-cloud-connector"></a>Jamf Cloud Connector 的相關常見問題

### <a name="what-data-is-shared-via-the-cloud-connector"></a>哪些資料會透過 Cloud Connector 共用？

Cloud Connector 會向 Microsoft Azure 進行驗證，並將裝置清查資料從 Jamf Pro 傳送至 Azure。 此外，Cloud Connector 會在 Azure 中管理服務探索、權杖交換、通訊錯誤和災害復原。

### <a name="where-is-device-inventory-data-stored"></a>裝置清查資料會儲存在哪裡？

裝置清查資料會儲存在 Jamf Pro 資料庫中。

### <a name="what-credentials-are-stored"></a>已儲存哪些認證？

未儲存任何認證。 設定 Cloud Connector 時，系統管理員必須同意將 Jamf 多租用戶應用程式和原生 macOS 連接器應用程式新增至其 Azure AD 租用戶。 新增多租用戶應用程式後，Cloud Connector 會要求存取權杖，以便與 Azure API 進行互動。 您可隨時在 Microsoft Azure 中撤銷應用程式存取權，以限制存取權。

### <a name="how-is-data-encrypted"></a>資料如何加密？

Cloud Connector 會使用傳輸層安全性 (TLS) 在 Jamf Pro 與 Microsoft Azure 之間傳送資料。

### <a name="how-does-jamf-know-which-device-is-associated-with-which-instance-of-jamf-pro"></a>Jamf 如何知道哪個裝置與 Jamf Pro 的哪個執行個體相關聯？

Jamf Pro 會使用 AWS 中的微服務，將裝置資訊正確地路由傳送至正確的執行個體。

### <a name="can-i-switch-from-using-the-cloud-connector-to-the-manual-connection-type"></a>我可以從使用 Cloud Connector 切換到手動連線類型嗎？

是。 您可以將連線類型變回手動，並依照步驟進行手動設定。 如有任何問題，應將其導向至 Jamf 尋求協助。

### <a name="permissions-were-modified-on-one-or-both-required-apps-cloud-connector-and-cloud-connector-user-registration-app-and-registration-is-not-working-is-this-supported"></a>已在一或兩個必要的應用程式 ([Cloud Connector]  和 [loud Connector 使用者註冊應用程式]  ) 上修改權限，而註冊無法運作，可支援此作業嗎？

不支援修改應用程式的權限。

## <a name="next-steps"></a>後續步驟

- [將合規性原則套用至受 Jamf 管理的裝置](../protect/conditional-access-assign-jamf.md)
- [Jamf 傳送至 Intune 的資料](../protect/data-jamf-sends-to-intune.md)
