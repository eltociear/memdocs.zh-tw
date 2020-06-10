---
title: 用戶端安全性和隱私權
titleSuffix: Configuration Manager
description: 了解 Configuration Manager 用戶端的安全性和隱私權。
ms.date: 07/07/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: c1d71899-308f-49d5-adfa-3a3ec0163ed8
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 84ef4e37ddf756f04101c9cdec0ec7a4ed91688d
ms.sourcegitcommit: 1e04fcd0d6c43897cf3993f705d8947cc9be2c25
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/02/2020
ms.locfileid: "84270832"
---
# <a name="security-and-privacy-for-configuration-manager-clients"></a>Configuration Manager 用戶端的安全性和隱私權

適用於：Configuration Manager (最新分支)

本文說明 Configuration Manager 用戶端的安全性和隱私權資訊。 它也包含由 [Exchange Server 連接器](../../../../mdm/deploy-use/manage-mobile-devices-with-exchange-activesync.md)所管理之行動裝置的資訊。  


## <a name="security-best-practices-for-clients"></a><a name="BKMK_Security_Clients"></a> 用戶端的安全性最佳做法  

Configuration Manager 站台接受來自執行 Configuration Manager 用戶端之裝置的資料。 此行為可能會引發用戶端攻擊站台的風險。 例如傳送格式錯誤的清查，或者嘗試使網站系統超載。 因此，只能將 Configuration Manager 用戶端部署至您信任的裝置。 此外，使用以下安全性最佳作法有助於保護網站不受 Rogue 或遭盜用的裝置攻擊：  

### <a name="use-public-key-infrastructure-pki-certificates-for-client-communications-with-site-systems-that-run-iis"></a>使用公開金鑰基礎結構 (PKI) 憑證，以執行 IIS 的站台系統進行用戶端通訊  

- 作為網站內容，針對 [僅 HTTPS]  設定 [網站系統設定] 。  

- 以 `UsePKICert` CCMSetup 內容安裝用戶端。  

- 使用憑證撤銷清單 (CRL)，並且確保用戶端和通訊中的伺服器可以隨時存取憑證撤銷清單。  

行動裝置用戶端及一些以網際網路為基礎的用戶端需要這些憑證。 Microsoft 建議使用這些憑證來進行內部網路上的所有用戶端連線。  

如需 PKI 憑證需求及其如何用來協助保護 Configuration Manager 的詳細資訊，請參閱 [PKI 憑證需求](../../../plan-design/network/pki-certificate-requirements.md)。  

### <a name="automatically-approve-client-computers-from-trusted-domains-and-manually-check-and-approve-other-computers"></a>自動核准來自信任網域的用戶端電腦，並且手動檢查並核准其他電腦。  

當您無法使用 PKI 驗證時，核准時便會將您信任的電腦識別為受 Configuration Manager 管理。 此階層具有以下用來設定用戶端核准的選項：  

- 手動
- 自動 (適用於受信任網域中的電腦)
- 自動 (適用於所有電腦)  

最安全的核准方法是自動核准受信任網域成員的用戶端。 此選項包括來自已連線 Azure Active Directory (Azure AD) 租用戶的雲端網域加入用戶端。<!-- MEMDocs#318 --> 然後手動檢查並核准所有其他電腦。 除非有其他存取控制功能可預防不受信任的電腦存取您的網路，否則不建議自動核准所有用戶端。  

如需如何手動核准電腦的詳細資訊，請參閱[從裝置節點管理用戶端](../../manage/manage-clients.md#BKMK_ManagingClients_DevicesNode)。  

### <a name="dont-rely-on-blocking-to-prevent-clients-from-accessing-the-configuration-manager-hierarchy"></a>請勿依賴以封鎖預防用戶端存取 Configuration Manager 階層  

Configuration Manager 基礎結構會拒絕被封鎖的用戶端。 如果用戶端遭到封鎖，則無法與站台系統通訊來下載原則、上傳清查資料，或是傳送狀態或狀態訊息。

封鎖是專為下列案例所設計：

- 在您部署 OS 至用戶端時，用以封鎖遺失或遭到洩露的開機媒體
- 所有站台系統接受 HTTPS 用戶端連線時

當站台系統接受 HTTP 用戶端連線時，請勿依賴用封鎖來保護 Configuration Manager 階層，以阻擋不信任電腦的存取。 在此案例中，封鎖的用戶端可以用新的自我簽署憑證與硬體識別碼重新加入站台。

憑證撤銷是對應可能遭到洩露之憑證的主要防線。 只有支援的公開金鑰基礎結構 (PKI) 才有憑證撤銷清單 (CRL) 可用。 在 Configuration Manager 中封鎖用戶端是保護階層的第二條防線。  

如需詳細資訊，請參閱[判斷是否要封鎖用戶端](determine-whether-to-block-clients.md)。  

### <a name="use-the-most-secure-client-installation-methods-that-are-practical-for-your-environment"></a>針對您的環境使用最安全實用的用戶端安裝方法  

- 對於網域電腦，群組原則用戶端安裝和以軟體更新為基礎的用戶端安裝方法，皆比用戶端推入安裝更安全。  

- 如果您套用存取控制與變更控制，請使用映像處理與手動安裝方法。  

- 在 1806 版或更新版本中，使用 Kerberos 相互驗證並搭配用戶端推入安裝。  

所有用戶端安裝方法中，最不安全的是用戶端推入安裝，因為其中具有諸多相依性。 這些相依性包括本機系統管理權限、Admin$ 共用及防火牆例外。 這些相依性的數目和類型會增加您的受攻擊面。  

從 1806 版開始，使用用戶端推入時，站台可以藉由在建立連線之前不允許回復為 NTLM 來要求 Kerberos 相互驗證。 此增強功能有助於保護伺服器和用戶端之間的通訊。 如需詳細資訊，請參閱[如何使用用戶端推入來安裝用戶端](../deploy-clients-to-windows-computers.md#BKMK_ClientPush)。<!--1358204-->  

如需不同用戶端安裝方法的詳細資訊，請參閱[用戶端安裝方法](client-installation-methods.md)。  

盡可能選取需要 Configuration Manager 最少安全性權限的用戶端安裝方法。 限制將具有可用於用戶端部署以外用途之權限的安全性角色指派給系統管理使用者。 例如，設定自動用戶端升級需要 [系統高權限管理員] 安全性角色，而此角色會授與系統管理使用者所有的安全性權限。  

如需各用戶端安裝方法所需之相依性和安全性權限的詳細資訊，請參閱[電腦用戶端的必要條件](../prerequisites-for-deploying-clients-to-windows-computers.md#BKMK_prereqs_computers)中的＜安裝方法相依性＞。  

### <a name="if-you-must-use-client-push-installation-take-additional-steps-to-secure-the-client-push-installation-account"></a>如果您必須使用用戶端推入安裝，請採取以下步驟以保護用戶端推入安裝帳戶  

此帳戶必須是安裝 Configuration Manager 用戶端之每部電腦的本機**系統管理員**群組成員。 絕不要將用戶端推入安裝帳戶新增至 **Domain Admins** 群組。 相反地，請建立全域群組，然後將該全域群組新增至您用戶端上的本機**系統管理員**群組。 建立群組原則物件以新增受限群組設定，藉以將用戶端推入安裝帳戶新增至本機**系統管理員**群組。  

如需額外的安全性，請建立多個用戶端推入安裝帳戶，其每一個帳戶對於有限數量電腦皆具有系統管理存取權。 如果一個帳戶遭到洩露，則只有該帳戶可存取的用戶端電腦會遭到洩露。  

### <a name="remove-certificates-before-imaging-clients"></a>製作用戶端映像前移除憑證  

當您使用 OS 映像部署用戶端時，請一律先移除憑證，再擷取映像。 這些憑證包括用於用戶端驗證的 PKI 憑證，以及自我簽署憑證。 如果您未移除這些憑證，用戶端可能會互相模擬。 您無法驗證各用戶端的資料。  

如需詳細資訊，請參閱[建立工作順序以擷取作業系統](../../../../osd/deploy-use/create-a-task-sequence-to-capture-an-operating-system.md)。  

### <a name="ensure-that-the-configuration-manager-computer-clients-get-an-authorized-copy-of-these-certificates"></a>請確定 Configuration Manager 電腦用戶端取得以下憑證的授權複本  

#### <a name="the-configuration-manager-trusted-root-key-certificate"></a>Configuration Manager 受信任的根金鑰憑證  

當下列兩個敘述皆為真時，用戶端會仰賴 Configuration Manager 受信任的根金鑰來驗證有效的管理點：  

- 您尚未擴充 Configuration Manager 的 Active Directory 架構
- 用戶端在與管理點通訊時未使用 PKI 憑證  

在此案例中，除非用戶端使用受信任的根金鑰，否則無法驗證該管理點是否受階層信任。 在沒有受信任的根金鑰時，技術好的攻擊可以將用戶端導向至 Rogue 管理點。  

當用戶端無法從通用類別目錄或藉由使用 PKI 憑證下載 Configuration Manager 受信任的根金鑰時，請以受信任的根金鑰預先佈建用戶端。 此動作可確保用戶端無法導向至 Rogue 管理點。 如需詳細資訊，請參閱[規劃受信任的根金鑰](../../../plan-design/security/plan-for-security.md#BKMK_PlanningForRTK)。  

#### <a name="the-site-server-signing-certificate"></a>網站伺服器簽署憑證  

用戶端會使用此憑證，驗證站台伺服器是否已簽署從管理點下載的原則。 此憑證是由網站伺服器自我簽署，並且發佈至 Active Directory 網域服務。  

當用戶端無法從通用分類目錄下載站台伺服器簽署憑證時，用戶端預設會從管理點下載該憑證。 如果管理點暴露在不受信任的網路 (例如網際網路)，請在用戶端上手動安裝站台伺服器簽署憑證。 此動作可確保用戶端無法從遭到洩露的管理點下載遭篡改的用戶端原則。  

若要手動安裝網站伺服器簽署憑證，請使用 CCMSetup client.msi 內容 **SMSSIGNCERT**。 如需詳細資訊，請參閱[關於用戶端安裝內容](../about-client-installation-properties.md)。  

### <a name="dont-use-automatic-site-assignment-if-the-client-downloads-the-trusted-root-key-from-the-first-management-point-it-contacts"></a>如果用戶端將從第一個接觸的管理點下載受信任的根金鑰，請勿使用自動站台指派  

若要避免新用戶端從 Rogue 管理點下載受信任之根金鑰的風險，請只在下列案例使用自動站台指派：  

- 用戶端可以存取已發佈至 Active Directory Domain Services 的 Configuration Manager 站台資訊。  

- 您以受信任的根金鑰預先佈建用戶端。  

- 您使用來自企業憑證授權單位的 PKI 憑證，在用戶端和管理點之間建立信任。  

如需受信任之根金鑰的詳細資訊，請參閱[規劃受信任的根金鑰](../../../plan-design/security/plan-for-security.md#BKMK_PlanningForRTK)。  

### <a name="install-client-computers-with-the-ccmsetup-clientmsi-option-smsdirectorylookupnowins"></a>使用 CCMSetup Client.msi 選項 SMSDIRECTORYLOOKUP=NoWINS 安裝用戶端電腦  

尋找網站與管理點的最安全服務位置方法為 Active Directory 網域服務。 有時候，在某些環境中無法使用此方法。 例如，因為您無法擴充 Configuration Manager 的 Active Directory 架構，或因為用戶端位於不受信任樹系或工作群組中。 如果無法使用此方法，請使用 DNS 發佈作為替代服務位置方法。 如果這兩種方法都失敗，當管理點未針對 HTTPS 用戶端連線進行設定時，用戶端可能會切換回使用 WINS。  

發佈至 WINS 比其他發佈方法更不安全。 因此，請指定 **SMSDIRECTORYLOOKUP=NoWINS** 將用戶端電腦設定為不切換回使用 WINS。 如果您必須使用 WINS 作為服務位置，請使用 **SMSDIRECTORYLOOKUP=WINSSECURE**。 這是預設設定。 它會使用 Configuration Manager 受信任的根金鑰驗證管理點的自我簽署憑證。  

> [!NOTE]  
> 當您針對 **SMSDIRECTORYLOOKUP=WINSSECURE** 設定用戶端，且它從 WINS 找到管理點時，用戶端會檢查其 WMI 中 Configuration Manager 受信任的根金鑰複本。  
>
> 如果管理點憑證上的簽章符合用戶端上受信任的根金鑰複本，憑證便已通過驗證。 驗證憑證之後，用戶端會開始與透過 WINS 找到的管理點通訊。  
>
> 如果管理點憑證上的簽章不符合用戶端上受信任的根金鑰複本，憑證便會無效。 在此案例中，用戶端不會與透過 WINS 找到的管理點通訊。  

### <a name="make-sure-that-maintenance-windows-are-large-enough-to-deploy-critical-software-updates"></a>請確定維護期間值大到足以部署重要的軟體更新  

裝置集合的維護期間會限制 Configuration Manager 可以在這些裝置上安裝軟體的次數。 如果您將維護期間設定得太小，則用戶端可能無法安裝重大軟體更新。 此行為會導致用戶端容易遭受軟體更新所減輕的任何攻擊。  

### <a name="take-additional-security-precautions-to-reduce-the-attack-surface-on-windows-embedded-devices-with-write-filters"></a>在具有寫入篩選器的 Windows Embedded 裝置上，採取額外的安全預防措施以減少受攻擊面  

當您在 Windows Embedded 裝置上啟用寫入篩選器時，任何軟體安裝或變更只會對重疊執行。 這些變更在裝置重新啟動後不會保存。 如果您使用 Configuration Manager 停用寫入篩選器，在這段期間，內嵌裝置易受所有磁碟區變更的影響。 這些磁碟區包括共用資料夾。  

Configuration Manager 在這段期間會將電腦鎖定，只能由本機系統管理員登入。 請盡可能採取額外的安全預防措施以協助保護電腦。 例如，啟用防火牆的其他限制。  

如果您使用維護期間保存變更，請小心規劃這些期間。 將寫入篩選器的停用時間降到最低，但時間長度仍足以完成軟體安裝與重新啟動。  

### <a name="use-the-latest-client-version-with-software-update-based-client-installation"></a>使用最新的用戶端版本進行以軟體更新為基礎的用戶端安裝

如果您使用以軟體更新為基礎的用戶端安裝，並且在站台上安裝較新版本的用戶端，請更新發佈的軟體更新。 然後，用戶端會從軟體更新點收到最新版本。  

當您更新站台時，已發佈至軟體更新點之用戶端部署的軟體更新不會自動更新。 請將 Configuration Manager 用戶端重新發佈至軟體更新點，並更新版本號碼。  

如需詳細資訊，請參閱[如何使用以軟體更新為基礎的安裝來安裝 Configuration Manager 用戶端](../deploy-clients-to-windows-computers.md#BKMK_ClientSUP)。  

### <a name="only-suspend-bitlocker-pin-entry-on-trusted-and-restricted-access-devices"></a>只在信任並限制存取的裝置上暫停輸入 BitLocker PIN  

請只為您信任並已限制其實際存取權的電腦，將用戶端設定 [重新啟動時暫停輸入 BitLocker PIN] 設定為 [永遠]。

當您將此用戶端設定設為 [永遠] 時，Configuration Manager 會完成軟體的安裝。 此行為可協助安裝重大軟體更新，並且繼續服務。 如果有攻擊者攔截重新啟動程序，則攻擊者可能會控制電腦。 只有在信任電腦並已限制電腦的實際存取權時，才能使用此設定。 例如，此設定可能適合用於資料中心內的伺服器。  

如需此用戶端設定的詳細資訊，請參閱[關於用戶端設定](../about-client-settings.md#suspend-bitlocker-pin-entry-on-restart)。  

### <a name="dont-bypass-powershell-execution-policy"></a>請勿略過 PowerShell 執行原則

如果您將 Configuration Manager 用戶端設定 [PowerShell 執行原則] 設定為 [略過]，則 Windows 會允許執行未簽署的 PowerShell 指令碼。 此行為可能會允許在用戶端電腦上執行惡意程式碼。 當您的組織需要此選項時，請使用自訂用戶端設定。 請只將其指派至必須執行未簽署之 PowerShell 指令碼的用戶端電腦。  

如需此用戶端設定的詳細資訊，請參閱[關於用戶端設定](../about-client-settings.md#powershell-execution-policy)。  


## <a name="security-best-practices-for-mobile-devices"></a><a name="bkmk_mobile"></a> 行動裝置的安全性最佳做法  

### <a name="install-the-enrollment-proxy-point-in-a-perimeter-network-and-the-enrollment-point-in-the-intranet"></a>將註冊 Proxy 點安裝在周邊網路，並將註冊點安裝在內部網路  

針對您以 Configuration Manager 註冊之以網際網路為基礎的的行動裝置，請將註冊 Proxy 點安裝在周邊網路，並將註冊點安裝在內部網路。 此角色隔離有助於保護註冊點不受攻擊。 如果攻擊者洩漏註冊點，則可以取得憑證進行驗證。 攻擊者也可以竊取註冊其行動裝置之使用者的認證。  

### <a name="configure-the-password-settings-to-help-protect-mobile-devices-from-unauthorized-access"></a>設定密碼設定，以協助保護行動裝置並防止未經授權的存取  

針對由 Configuration Manager 註冊的行動裝置：使用行動裝置設定項目將密碼複雜性設定為 PIN。 至少指定預設的密碼最小長度。  

針對沒有安裝 Configuration Manager 用戶端，但由 Exchange Server 連接器管理的行動裝置：設定 Exchange Server 連接器的 [密碼設定]，使密碼複雜性為 PIN。 至少指定預設的密碼最小長度。  

### <a name="only-allow-applications-to-run-that-are-signed-by-companies-that-you-trust"></a>只允許執行信任的公司簽署過的應用程式  

只允許執行信任的公司簽署過的應用程式，如此有助於預防清查資訊與狀態資訊遭到竄改。 不允許裝置安裝未簽署的檔案。  

針對由 Configuration Manager 註冊的行動裝置：使用行動裝置設定項目，將安全性設定 [未簽署的應用程式] 設定為 [禁止]。 將 [未簽署的檔案安裝] 設定為信任的來源。  

針對沒有安裝 Configuration Manager 用戶端，但由 Exchange Server 連接器管理的行動裝置：設定 Exchange Server 連接器的 [應用程式設定]，將 [未簽署的檔案安裝] 與 [未簽署的應用程式] 設定為 [禁止]。  

### <a name="lock-mobile-devices-when-not-in-use"></a>鎖定未使用的行動裝置  

鎖定未使用的行動裝置，有助於預防權限提高攻擊。

針對由 Configuration Manager 註冊的行動裝置：使用行動裝置設定項目，進行密碼設定 [鎖定行動裝置前允許的閒置時間 (分鐘)]。  

針對沒有安裝 Configuration Manager 用戶端，但由 Exchange Server 連接器管理的行動裝置：設定 Exchange Server 連接器的 [密碼設定]，以設定 [鎖定行動裝置前允許的閒置時間 (分鐘)]。  

### <a name="restrict-the-users-who-can-enroll-their-mobile-devices"></a>限制可註冊其行動裝置的使用者  

限制可註冊行動裝置的使用者，有助於防止權限提高。 使用自訂用戶端設定而非預設用戶端設定，只允許已獲得授權的使用者註冊其行動裝置。  

### <a name="user-device-affinity-guidance-for-mobile-devices"></a>適用於行動裝置的使用者裝置親和性指引  

在下列案例中，請勿將應用程式部署至已使用 Configuration Manager 或 Microsoft Intune 註冊行動裝置的使用者：  

- 行動裝置供多人使用。  

- 系統管理員代替使用者註冊裝置。  

- 裝置傳送給他人，而沒有先淘汰再重新註冊裝置。  

裝置註冊會建立使用者裝置親和性關聯性。 此關聯性會將執行註冊的使用者對應到行動裝置。 如果有其他使用者使用行動裝置，則該使用可以執行部署至原始使用者的應用程式，如此可能導致權限提高。 同樣地，如果系統管理員為使用者註冊行動裝置，則不會在行動裝置上安裝部署至使用者的應用程式。 相反地，可能會安裝部署至系統管理員的應用程式。  

有別於 Windows 電腦的使用者裝置親和性，您不能為 Microsoft Intune 所註冊的行動裝置手動定義使用者裝置親和性資訊。  

如果轉移 Intune 所註冊的行動裝置擁有權，請先將行動裝置從 Intune 淘汰。 此動作會移除使用者裝置親和性關聯性。 然後要求目前使用者再次註冊裝置。  

### <a name="make-sure-that-users-enroll-their-own-mobile-devices-for-microsoft-intune"></a>確定使用者使用 Microsoft Intune 註冊他們的行動裝置  

裝置註冊期間會建立使用者裝置親和性關聯性。 此動作會將執行註冊的使用者對應到行動裝置。 如果系統管理員為使用者註冊行動裝置，則不會在行動裝置上安裝部署至使用者的應用程式。 相反地，可能會安裝部署至系統管理員的應用程式。  

### <a name="protect-the-connection-between-the-configuration-manager-site-server-and-the-exchange-server"></a>保護 Configuration Manager 站台伺服器與 Exchange Server 之間的連線

如果是內部部署的 Exchange Server，則使用 IPsec。 託管的 Exchange 會自動使用 SSL 保護連線。  

### <a name="use-the-principle-of-least-privileges-for-the-connector"></a>針對連接器使用最低權限準則  

如需 Exchange Server 連接器所需之基本 Cmdlet 的清單，請參閱[使用 Configuration Manager 和 Exchange 管理行動裝置](../../../../mdm/deploy-use/manage-mobile-devices-with-exchange-activesync.md)。  


## <a name="security-best-practices-for-macs"></a><a name="bkmk_macs"></a> Mac 的安全性最佳做法  

### <a name="store-and-access-the-client-source-files-from-a-secured-location"></a>儲存和存取來自安全位置的用戶端來源檔案  

在 Mac 電腦上安裝或註冊用戶端之前，Configuration Manager 不會確認這些用戶端來源檔案是否已遭竄改。 請從可信任的來源下載這些檔案。 以安全的方式進行儲存和存取。  

### <a name="monitor-and-track-the-validity-period-of-the-certificate"></a>監視並追蹤憑證的有效期限  

為確保業務連續性，請監視並追蹤您用於 Mac 電腦的憑證有效期。 Configuration Manager 不支援此憑證的自動更新，憑證即將到期時也不會對您提出警告。 通常有效期限為一年。  

如需如何更新憑證的詳細資訊，請參閱[手動更新 Mac 用戶端憑證](../deploy-clients-to-macs.md#renew-the-mac-client-certificate)。  

### <a name="configure-the-trusted-root-certificate-for-ssl-only"></a>只設定受信任的根憑證用於 SSL  

為了協助防止權限提高，請設定可信任之根憑證授權單位的憑證，只有在用於 SSL 通訊協定時才信任它。

當您註冊 Mac 電腦時，會自動安裝管理 Configuration Manager 用戶端的使用者憑證。 此使用者憑證包括其信任鏈結中受信任的根憑證。 若要將此根憑證的信任限制在 SSL 通訊協定，請使用下列程序：  

1. 在 Mac 電腦上，開啟終端機視窗。  

2. 輸入下列命令：`sudo /Applications/Utilities/Keychain\ Access.app/Contents/MacOS/Keychain\ Access`  

3. 在 [金鑰鏈存取] 對話方塊的 [金鑰鏈] 區段中，按一下 [系統]。 然後在 [類別] 區段中，按一下 [憑證]。  

4. 找出並按兩下 Mac 用戶端憑證的根 CA 憑證。  

5. 在根 CA 憑證的對話方塊中，展開 [信任]  區段，然後進行下列變更：  

    1. **使用此憑證時**：將 [永遠信任] 設定變更為 [使用系統預設值]。  

    2. **安全通訊端層 (SSL)** ：將 [未指定值] 變更為 [永遠信任]。  

6. 關閉對話方塊。 收到提示時輸入系統管理員的密碼，然後按一下 [更新設定]。  

在您完成此程序之後，根憑證只有在驗證 SSL 通訊協定時才受信任。 其他目前不受此根憑證信任的通訊協定包括安全郵件 (S/MIME)、可延伸的驗證 (EAP) 或程式碼簽署。  

> [!NOTE]  
> 如果您安裝獨立於 Configuration Manager 之外的用戶端憑證，也請使用此程序。


## <a name="security-issues-for-configuration-manager-clients"></a><a name="BKMK_SecurityIssues_Clients"></a> Configuration Manager 用戶端的安全性問題  

以下安全性問題並未降低：  

### <a name="status-messages-arent-authenticated"></a>狀態訊息未經驗證

未針對狀態訊息執行驗證。 當管理點接受 HTTP 用戶端連線時，任何裝置皆可傳送狀態訊息至管理點。 如果管理點只接受 HTTPS 用戶端連線，則裝置必須具有有效的用戶端驗證憑證，但也可能傳送任何狀態訊息。 管理點會捨棄從用戶端收到的任何無效狀態訊息。  

有數種方式可能針對此漏洞進行攻擊：

- 攻擊者可能會傳送假的狀態訊息，以取得以狀態訊息查詢為基礎之集合中的成員資格。
- 任何用戶端都可能對管理點湧入大量狀態訊息，以啟動阻斷服務。
- 如果狀態訊息觸發狀態訊息篩選規則中的動作，則攻擊者便可能觸發狀態訊息篩選規則。
- 攻擊者可能會傳送導致報告資訊轉譯錯誤的狀態訊息。  

### <a name="policies-can-be-retargeted-to-non-targeted-clients"></a>原則可能會被重定至非目標的用戶端  

攻擊者可以利用數種方式，將以一個用戶端為目標的原則套用至完全不同的用戶端。 例如，攻擊者可能會在信任的用戶端傳送錯誤的清查或探索資訊，將電腦加入到不應加入的集合。 然後，該用戶端會接收該集合的所有部署。

有控制項可預防攻擊者直接修改原則。 不過，攻擊者可將現有的原則重新格式化，並將 OS 重新部署，再傳送至不同的電腦。 此重新導向的原則可能會導致拒絕服務。 這些類型的攻擊需要具備準確的時間控制，以及多方的 Configuration Manager 基礎結構知識。  

### <a name="client-logs-allow-user-access"></a>用戶端記錄檔可供使用者存取  

所有用戶端記錄檔皆允許 **Users** 群組進行「讀取」存取，並且允許特殊的**互動**使用者進行「寫入」存取。 如果您啟用詳細資訊記錄，攻擊者可能會讀取記錄檔，尋找有關相容性或系統漏洞的資訊。 用戶端安裝在使用者內容中的處理序 (例如軟體) 必須使用低權限使用者帳戶來寫入記錄。 此行為表示攻擊者也可以利用低權限帳戶寫入記錄。  

最重大的風險是，攻擊者可能會將記錄檔中的資訊移除。 系統管理員可能需要此資訊進行稽核及偵測入侵。  

### <a name="a-computer-could-be-used-to-obtain-a-certificate-thats-designed-for-mobile-device-enrollment"></a>電腦可用於取得專為行動裝置註冊而設計的憑證  

當 Configuration Manager 處理註冊要求時，無法確認要求是源自於行動裝置，而不是電腦。 如果要求是來自電腦，則可以安裝 PKI 憑證，允許電腦向 Configuration Manager 登錄。

在此案例中，若要預防權限提高攻擊，就只能讓信任的使用者註冊行動裝置。 請謹慎監視站台中的裝置註冊活動。  

### <a name="a-blocked-client-can-still-send-messages-to-the-management-point"></a>封鎖的用戶端仍然可以傳送訊息至管理點

當您封鎖不再信任的用戶端，但該用戶端已針對用戶端通知建立網路連線時，Configuration Manager 不會中斷與工作階段的連線。 封鎖的用戶端可以繼續傳送封包至其管理點，直到用戶端與網路中斷連線為止。 這些封包只是小型的保持運作封包。 此用戶端在被解除封鎖之前，都無法由 Configuration Manager 進行管理。  

### <a name="automatic-client-upgrade-doesnt-verify-the-management-point"></a>自動用戶端升級不會驗證管理點

當您使用自動用戶端升級時，用戶端可能會被導向至管理點以下載用戶端來源檔案。 在此案例中，用戶端不會將管理點驗證為信任的來源。  

### <a name="when-users-first-enroll-mac-computers-theyre-at-risk-from-dns-spoofing"></a>使用者第一次註冊 Mac 電腦時，可能有 DNS 詐騙的風險  

當 Mac 電腦在註冊期間連線至註冊 Proxy 點時，Mac 電腦通常不具有受信任的根 CA 憑證。 此時，Mac 電腦不信任伺服器，並且會提示使用者繼續。 如果 Rogue DNS 伺服器解析註冊 Proxy 點的完整網域名稱 (FQDN)，則可能會將 Mac 電腦導向至 Rogue 註冊 Proxy 點，以安裝來自不信任來源的憑證。 為降低此風險，請遵循最佳作法以免環境中出現 DNS 詐騙。  

### <a name="mac-enrollment-doesnt-limit-certificate-requests"></a>Mac 註冊不會限制憑證要求  

每次要求新用戶端憑證時，使用者都可以重新註冊 Mac 電腦。 Configuration Manager 不會檢查是否有多個要求，或限制來自單一電腦要求的憑證數目。 Rogue 使用者可以執行重複命令列註冊要求的指令碼。 此攻擊可能會在網路上或發行憑證授權單位 (CA) 時導致拒絕服務。 為降低此風險，請小心監視發行 CA 此類可疑的行為。 從 Configuration Manager 階層立即封鎖有此類行為的任何電腦。  

### <a name="a-wipe-acknowledgment-doesnt-verify-that-the-device-has-been-successfully-wiped"></a>抹除認可並不會確認裝置是否已成功抹除  

當您對行動裝置起始抹除動作，並且 Configuration Manager 認可抹除時，驗證方式為確認 Configuration Manager 是否成功「傳送」訊息。 它不會確認裝置是否對要求進行「動作」。

對於由 Exchange Server 連接器管理的行動裝置，抹除認可會確認命令是否由 Exchange 接收，而非裝置。  

### <a name="if-you-use-the-options-to-commit-changes-on-windows-embedded-devices-accounts-might-be-locked-out-sooner-than-expected"></a>如果您使用選項認可 Windows Embedded 裝置上的變更，則可能會以比預期更快將帳戶鎖定  

如果 Windows Embedded 裝置執行 Windows 7 之前的 OS 版本，而且使用者嘗試在 Configuration Manager 停用寫入篩選器時登入，則帳戶鎖定前 Windows 所允許的已設定錯誤嘗試次數只有一半。

例如，您可以將 [帳戶鎖定閾值] 的網域原則設定為六次嘗試。 使用者輸入錯誤密碼三次，便會鎖定帳戶。此行為實際上會導致拒絕服務。 在此案例中，如果使用者必須登入內嵌裝置，請警告使用者鎖定閥值可能會降低。  


## <a name="privacy-information-for-configuration-manager-clients"></a><a name="BKMK_Privacy_Clients"></a> Configuration Manager 用戶端的隱私權資訊  

當您部署 Configuration Manager 用戶端時，會啟用用戶端設定，以使用 Configuration Manager 功能。 您用來設定功能的設定可套用至 Configuration Manager 階層中的所有用戶端。 無論是直接連線至內部網路、透過遠端工作階段連線，或是連線至網路網路，此行為都相同。  

用戶端資訊會儲存在您 SQL Server 中的 Configuration Manager 資料庫，不會傳送給 Microsoft。 資訊會保留在資料庫中，直到每 90 天由站台維護工作 [刪除過時探索資料] 刪除為止。 您可以設定刪除間隔。 

系統會將一些摘要或彙總的診斷及使用方式資料傳送給 Microsoft。 如需詳細資訊，請參閱[診斷和使用方式資料](../../../plan-design/diagnostics/diagnostics-and-usage-data.md)。  

在設定 Configuration Manager 用戶端之前，請考慮您的隱私需求。  

您可於 [Microsoft 隱私權聲明](https://privacy.microsoft.com/privacystatement)中深入了解 Microsoft 的資料收集和使用。

### <a name="client-status"></a>用戶端狀態  

Configuration Manager 會監視用戶端活動。 它會定期評估 Configuration Manager 用戶端，並可補救用戶端及其相依性問題。 預設會啟用用戶端狀態。 它使用伺服器端的度量來測量用戶端活動檢查。 用戶端狀態使用用戶端動作進行自我檢查、補救，以及傳送用戶端狀態資訊到站台。 用戶端會根據您設定的排程以執行自我檢查。 用戶端會將檢查結果傳送至 Configuration Manager 站台。 這項資訊會在傳輸過程中加密。  

用戶端狀態資訊會儲存在您 SQL Server 中的 Configuration Manager 資料庫，不會傳送給 Microsoft。 此資訊不會以加密格式儲存在站台資料庫內。 此資訊會保留在資料庫中，直到根據針對 [保留以下指定天數內的用戶端狀態歷程]  用戶端狀態設定所設定的值進行刪除為止。 此設定的預設值為每 31 天。  

透過用戶端狀態檢查安裝 Configuration Manager 用戶端之前，請考量您的隱私權需求。  


## <a name="privacy-information-for-mobile-devices-that-are-managed-with-the-exchange-server-connector"></a><a name="BKMK_Privacy_ExchangeConnector"></a> 使用 Exchange Server 連接器所管理的行動裝置隱私權資訊  

Exchange Server 連接器會藉由 ActiveSync 通訊協定尋找並管理連線至內部部署或託管 Exchange Server 的裝置。 Exchange Server 連接器找到的記錄會儲存在您 SQL Server 中的 Configuration Manager 資料庫。 此資訊會從 Exchange Server 進行收集。 伺服器不包含來自行動裝置傳送至 Exchange Server 的任何額外資訊。  

行動裝置資訊不會傳送給 Microsoft。 行動裝置資訊儲存在您 SQL Server 中的 Configuration Manager 資料庫。 資訊會保留在資料庫中，直到每 90 天由站台維護工作 [刪除過時探索資料] 刪除為止。 您可以設定刪除間隔。  

安裝並設定 Exchange Server 連接器之前，請考量您的隱私權需求。  

您可於 [Microsoft 隱私權聲明](https://privacy.microsoft.com/privacystatement)中深入了解 Microsoft 的資料收集和使用。
