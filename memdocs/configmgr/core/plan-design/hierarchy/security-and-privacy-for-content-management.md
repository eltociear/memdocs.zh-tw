---
title: 內容管理的安全性和隱私權
titleSuffix: Configuration Manager
description: 最佳化 Configuration Manager 中內容的安全性和隱私權。
ms.date: 10/26/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 5f38b726-dc00-433a-ba05-5b7dbb0d8e99
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 067922149ef268aeb6cd562816aaa4971e184fab
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81704476"
---
# <a name="security-and-privacy-for-content-management-in-configuration-manager"></a>Configuration Manager 中內容管理的安全性和隱私權

適用於：  Configuration Manager (最新分支)

本文包含 Configuration Manager 中內容管理的安全性和隱私權資訊。 



##  <a name="security-best-practices-for-content-management"></a><a name="BKMK_Security_ContentManagement"></a> 內容管理的安全性最佳做法  


#### <a name="advantages-and-disadvantages-of-https-or-http-for-intranet-distribution-points"></a>針對內部網路發佈點使用 HTTPS 和 HTTP 的優缺點
針對內部網路上的發佈點，請考慮使用 HTTPS 和 HTTP 的優缺點。 在大部分案例中，與使用具加密但沒有授權的 HTTPS 相較之下，使用 HTTP 和套件存取帳戶進行授權可提供更高的安全性。 不過，如果您的內容中包含機密資料，而您想要在傳送時加密資料，請使用 HTTPS。  

-   **當您針對發佈點使用 HTTPS 時**，Configuration Manager 不會使用套件存取帳戶以授權內容存取，但內容透過網路傳送時會經過加密。  

-   **當您針對發佈點使用 HTTP 時**，可以使用套件存取帳戶進行授權，但內容透過網路傳送時不會經過加密。  

從 1806 版開始，請考慮為站台啟用 [增強 HTTP]  。 這項功能可讓用戶端使用 Azure Active Directory 驗證來與 HTTP 發佈點進行安全通訊。 如需詳細資訊，請參閱[Enhanced HTTP](enhanced-http.md) (增強 HTTP)。

#### <a name="protect-the-client-authentication-certificate-file"></a>保護用戶端驗證憑證檔案
如果您對發佈點使用 PKI 用戶端驗證憑證，而不是自我簽署的憑證，請用強式密碼保護憑證檔案 (.pfx)。 如果您在網路上儲存檔案，在將檔案匯入 Configuration Manager 時，請保護網路通道的安全。

如果您需要密碼才能匯入其發佈點用來與管理點通訊的用戶端驗證憑證，則這項設定有助於保護憑證不受攻擊者利用。 在網路位置和站台伺服器之間使用伺服器訊息區 (SMB) 簽署或 IPsec，以防止攻擊者竄改憑證檔案。  

#### <a name="remove-the-distribution-point-role-from-the-site-server"></a>從站台伺服器移除發佈點角色
根據預設，Configuration Manager 安裝程式會在站台伺服器上安裝發佈點。 用戶端不需要直接與站台伺服器進行通訊。 若要減少受攻擊面，請將發佈點角色指派給其他站台系統，並從站台伺服器移除它。  

#### <a name="secure-content-at-the-package-access-level"></a>保護套件存取層級的內容
發佈點共用會允許所有使用者的讀取權限。 若要限制哪些使用者可存取內容，針對 HTTP 設定發佈點時，請使用套件存取帳戶。 這項設定不適用於雲端發佈點，因為其不支援套件存取帳戶。 如需詳細資訊，請參閱[套件存取帳戶](accounts.md#package-access-account)。

#### <a name="configure-iis-on-the-distribution-point-role"></a>在發佈點角色上設定 IIS
當您新增發佈點站台系統角色時，如果 Configuration Manager 安裝 IIS，請在發佈點安裝完成時移除 HTTP 重新導向或 IIS 管理指令碼及工具。 發佈點不需要 HTTP 重新導向或 IIS 管理指令碼及工具。 若要減少受攻擊面，請移除網頁伺服器角色的這些角色服務。  如需發佈點上網頁伺服器角色的角色服務詳細資訊，請參閱[站台與站台系統必要條件](../configs/site-and-site-system-prerequisites.md)。  

#### <a name="set-package-access-permissions-when-you-create-the-package"></a>建立套件時設定套件存取權限
由於對套件檔案上存取帳戶的變更只有在重新發佈套件時才會生效，因此初次建立套件時，務必小心設定套件存取權限。 當套件很大或是會發佈至多個發佈點，且內容發佈的網路頻寬容量有限時，這項設定會很重要。  

#### <a name="implement-access-controls-to-protect-media-that-contains-prestaged-content"></a>實作存取控制以保護包含預先設置內容的媒體
預先設置內容經過壓縮，但未加密。 攻擊者可能會讀取及修改下載到裝置的檔案。 Configuration Manager 用戶端會拒絕遭竄改的內容，但仍會下載它。  

#### <a name="import-prestaged-content-with-extractcontent"></a>使用 ExtractContent 匯入預先設置的內容
使用 ExtractContent.exe 命令列工具，只匯入預先設置的內容。 為避免竄改及提高權限，請只使用 Configuration Manager 隨附的已授權命令列工具。  

#### <a name="secure-the-communication-channel-between-the-site-server-and-the-package-source-location"></a>保護站台伺服器與套件來源位置之間通訊通道的安全
當您建立應用程式和套件時，在站台伺服器與套件來源位置之間使用 IPsec 或 SMB 簽署。 這項設定有助於避免攻擊者竄改來源檔案。  

#### <a name="remove-default-virtual-directories-for-custom-website-with-the-distribution-point-role"></a>移除具有發佈點角色的自訂網站預設虛擬目錄
如果您在安裝發佈點角色之後，將站台設定選項變更為使用自訂網站，而不是預設網站，請移除預設虛擬目錄。 當您從預設網站切換至自訂網站時，Configuration Manager 不會移除舊的虛擬目錄。 請移除 Configuration Manager 原本在預設網站下建立的下列虛擬目錄：  

-   SMS_DP_SMSPKG$  

-   SMS_DP_SMSSIG$  

-   NOCERT_SMS_DP_SMSPKG$  

-   NOCERT_SMS_DP_SMSSIG$  


#### <a name="for-cloud-distribution-points-protect-your-azure-subscription-details-and-certificates"></a>針對雲端發佈點，保護您的 Azure 訂用帳戶詳細資料及憑證
當您使用雲端發佈點時，請保護下列高價值的項目：
- 您 Azure 訂用帳戶的使用者名稱和密碼
- Azure 管理憑證 
- 雲端發佈點服務憑證

請將憑證儲存在安全的地方。 如果設定雲端發佈點時要透過網路瀏覽憑證，請在站台系統伺服器與來源位置之間使用 IPsec 或 SMB 簽署。  

#### <a name="for-service-continuity-monitor-the-expiry-date-of-the-cloud-distribution-point-certificates"></a>為持續提供服務，請監控雲端發佈點憑證的到期日
Configuration Manager 不會在針對雲端發佈點匯入的憑證即將到期時警告您。 您必須在 Configuration Manager 之外另行監控到期日。 確定在到期日之前更新並匯入新憑證。 如果您從外部公用提供者取得伺服器驗證憑證，此動作會很重要，因為您可能需要額外的時間來取得更新的憑證。  

 如果兩個憑證中的任何一個已過期，則雲端服務管理員會產生狀態訊息識別碼 **9425**。 CloudMgr.log 檔案包含項目，指出憑證**處於過期狀態**，並以 UTC 格式記錄到期日。  



## <a name="security-considerations-for-content-management"></a>內容管理的安全性考量  

規劃內容管理時，請考慮下列幾點：  

-   用戶端只會驗證下載的內容。  

     Configuration Manager 用戶端只有在內容下載到其用戶端快取後，才會驗證內容上的雜湊。 如果攻擊者竄改下載的檔案清單或內容本身，則下載程序可能佔用相當大的網路頻寬，這樣只會讓用戶端在遭遇無效的雜湊時捨棄內容。  

-   當您使用雲端發佈點時，存取內容時會自動將範圍限制在您的企業中。 您無法將其進一步限制在選取的使用者或群組中。  

-   當您使用雲端發佈點時，管理點會驗證用戶端，然後使用 Configuration Manager 權杖來存取雲端發佈點。 權杖的有效時間為八個小時。 此行為表示，如果某個用戶端因不再受信任而遭到封鎖，它可繼續從雲端發佈點下載內容，直到此權杖的有效期間到期。 這種情況下，因為用戶端遭到封鎖，所以管理點不會對用戶端發出另一個權杖。  

     若要防止封鎖的用戶端在八小時的時間範圍內下載內容，請停止雲端服務。 在設定管理員主控台中，移至 [系統管理]  工作區，展開 [雲端服務]  ，然後選取 [雲端發佈點]  節點。  



##  <a name="privacy-information-for-content-management"></a><a name="BKMK_Privacy_ContentManagement"></a> 內容管理的隱私權資訊  

 Configuration Manager 不會在內容檔案中包含任何使用者資料，但系統管理使用者可能會選擇執行此動作。  



## <a name="see-also"></a>請參閱

- [內容管理的基本概念](fundamental-concepts-for-content-management.md)  

- [應用程式管理的安全性和隱私權](../../../apps/plan-design/security-and-privacy-for-application-management.md)  

- [軟體更新的安全性和隱私權](../../../sum/plan-design/security-and-privacy-for-software-updates.md)  

- [OS 部署的安全性與隱私權](../../../osd/plan-design/security-and-privacy-for-operating-system-deployment.md)  
