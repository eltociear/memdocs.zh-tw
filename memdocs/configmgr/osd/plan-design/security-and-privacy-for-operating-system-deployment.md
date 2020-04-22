---
title: OS 部署的安全性與隱私權
titleSuffix: Configuration Manager
description: 了解 Configuration Manager 中 OS 部署的安全性和隱私權最佳做法。
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 5ee5928f-3d72-4b00-8156-1e0d1030a96c
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 53256889b8bbd6a9608748a57de33b38be77cfd8
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81709326"
---
# <a name="security-and-privacy-for-os-deployment-in-configuration-manager"></a>Configuration Manager 中 OS 部署的安全性和隱私權

適用於：  Configuration Manager (最新分支)

本文包含 Configuration Manager 中 OS 部署功能的安全性和隱私權資訊。  



##  <a name="security-best-practices-for-os-deployment"></a><a name="bkmk_security"></a> OS 部署的安全性最佳做法  

當您以 Configuration Manager 來部署作業系統時，可使用下列安全性最佳做法：  


### <a name="implement-access-controls-to-protect-bootable-media"></a>實作存取控制以保護可開機媒體

建立可開機媒體時，永遠指派密碼以保護媒體。 即使使用密碼，只會將包含敏感性資訊的檔案加密，而且會覆寫所有檔案。  

控制對媒體的實體存取，以防止攻擊者利用密碼編譯攻擊來取得用戶端驗證憑證。  

為協助防止用戶端安裝已遭竄改的內容或用戶端原則，內容須進行雜湊，並與原始原則搭配使用。 如果內容雜湊失敗，或確認內容符合原則，用戶端就不會使用可開機媒體。 只有內容雜湊。 原則未雜湊，但指定密碼時，就會進行加密及保護。 此行為讓攻擊者更難成功修改原則。  


### <a name="use-a-secure-location-when-you-create-media-for-os-images"></a>建立用於 OS 映像的媒體時可使用安全的位置

如果未被授權的使用者具有該位置的存取權，他們就能竄改您建立的檔案。 他們也可以使用所有可用的磁碟空間，因而造成媒體建立失敗。  


### <a name="protect-certificate-files"></a>保護憑證檔案 

使用強式密碼保護憑證檔案 (.pfx)。 如果您在網路上儲存檔案，在將檔案匯入 Configuration Manager 時，請保護網路通道

使用密碼來匯入用於可開機媒體的用戶端驗證憑證時，這項設定有助於保護憑證，使其免受攻擊者的攻擊。  

在網路位置和站台伺服器之間使用 SMB 簽署或 IPsec，以防止攻擊者竄改憑證檔案。  


### <a name="block-or-revoke-any-compromised-certificates"></a>封鎖或撤銷任何遭入侵的憑證 

如果用戶端憑證遭入侵，此時可封鎖 Configuration Manager 的憑證。 如果是 PKI 憑證，則可將它撤銷。  

若要使用可開機媒體和 PXE 開機來部署 OS，您必須擁有含私密金鑰的用戶端驗證憑證。 如果該憑證遭到入侵，請在 [系統管理]  工作區的 [憑證]  節點、[安全性]  節點封鎖憑證。  


### <a name="secure-the-communication-channel-between-the-site-server-and-the-sms-provider"></a>保護站台伺服器與 SMS 提供者之間的通訊通道

當 SMS 提供者在站台伺服器的遠端時，請保護通訊通道以保護開機映像。

當您修改開機映像，且 SMS 提供者正在非站台伺服器的伺服器上執行時，開機映像很容易遭到攻擊。 使用 SMB 簽署或 IPsec，可保護這些電腦之間的網路通道。  


### <a name="enable-distribution-points-for-pxe-client-communication-only-on-secure-network-segments"></a>啟用只在安全網路區段之 PXE 用戶端通訊的發佈點

當用戶端傳送 PXE 開機要求時，您無法確保有效支援 PXE 的發佈點會回應該要求。 此案例具有以下安全性風險：  

- 回應 PXE 要求的 rogue 發佈點，可提供遭竄改的映像給用戶端。  

- 攻擊者可能針對 PXE 使用的 TFTP 通訊協定啟動攔截式攻擊。 此攻擊可能會隨 OS 檔案傳送惡意程式碼。 攻擊者也可能建立 Rogue 用戶端，直接對發佈點發出 TFTP 要求。  

- 攻擊者可能利用惡意用戶端來啟動一項針對發佈點的服務攻擊回絕行動。  

使用深度防禦來保護網路區段，讓用戶端可從中存取支援 PXE 的發佈點。  

> [!WARNING]  
>  基於這些安全性風險，若 PXE 通訊的發佈點是不受任信的網路 (例如周邊網路) 時，請勿啟用該發佈點。  


### <a name="configure-pxe-enabled-distribution-points-to-respond-to-pxe-requests-only-on-specified-network-interfaces"></a>設定支援 PXE 的發佈點只在指定的網路介面回應 PXE 要求  

如果您允許發佈點在所有網路介面上回應 PXE 要求，此設定可能會對不受信任網域公開 PXE 服務  


### <a name="require-a-password-to-pxe-boot"></a>要求輸入密碼以將 PXE 開機

如果您要求輸入密碼以將 PXE 開機，此設定可為 PXE 開機程序增加一道額外的安全性等級。 這項設定有助於防止Rogue 用戶端加入 Configuration Manager 階層。  


### <a name="restrict-content-in-os-images-used-for-pxe-boot-or-multicast"></a>限制用於 PXE 開機或多點傳送的 OS 映像內容

請勿將包含敏感性資料的企業營運應用程式或軟體納入用於 PXE 開機或多點傳送的映像中。  

由於固有的安全性風險與 PXE 開機及多點傳送息息相關，如果 Rogue 電腦下載了 OS 映像，即需降低風險。  


### <a name="restrict-content-installed-by-task-sequence-variables"></a>限制工作順序變數所安裝的內容

請勿將包含敏感性資料的企業營運應用程式或軟體納入使用工作順序變數安裝的應用程式套件中。  

當您使用工作順序變數部署軟體時，它可能會安裝在電腦上，並安裝到未被授權接收該軟體的使用者。  


### <a name="secure-the-network-channel-when-migrating-user-state"></a>移轉使用者狀態時保護網路通道

當您移轉使用者狀態時，請使用 SMB 簽署或 IPsec 保護用戶端和狀態移轉點之間的網路通道。  

透過 HTTP 初始連線後，會使用 SMB 傳送使用者狀態移轉資料。 如果您未保護網路通道，攻擊者就可以讀取及修改此資料。  


### <a name="use-the-latest-version-of-usmt"></a>使用最新版的 USMT

使用 Configuration Manager 所支援的最新版使用者狀態移轉工具 (USMT)。  

最新版的 USMT 提供安全性增強功能，並且對於移轉使用者狀態資料時會有更好的控制。  


### <a name="manually-delete-folders-on-state-migration-points-when-you-decommission-them"></a>當您解除委任狀態移轉點上的資料夾時，請手動刪除資料夾  

當您在 Configuration Manager 主控台的狀態移轉點內容中移除狀態移轉點資料夾時，站台不會刪除實體資料夾。 若要防止使用者狀態移轉資料發生資訊洩漏，請手動移除網路共用，並刪除資料夾。  


### <a name="dont-configure-the-deletion-policy-to-immediately-delete-user-state"></a>請勿將刪除原則設定為立即刪除使用者狀態  

如果您將狀態移轉點上的刪除原則設定為立即移除標記刪除的資料，而且攻擊者比有效的電腦先擷取到使用者狀態資料，站台會立即刪除使用者狀態資料。 設定足夠的 [保留時間]  間隔，以確認成功還原使用者狀態資料。  


### <a name="manually-delete-computer-associations"></a>手動刪除電腦關聯 

當完成並確認使用者狀態移轉資料還原時，手動刪除電腦關聯。

Configuration Manager 不會自動移除電腦關聯。 手動刪除不再需要的電腦關聯，有助於保護使用者狀態資料的身分識別。  


### <a name="manually-back-up-the-user-state-migration-data-on-the-state-migration-point"></a>手動備份狀態移轉點上的使用者狀態移轉資料  

Configuration Manager 備份不會在站台備份中包含使用者狀態移轉資料。  


### <a name="implement-access-controls-to-protect-the-prestaged-media"></a>實作存取控制以保護預先設置的媒體  

控制對媒體的實體存取，防止攻擊者利用密碼編譯攻擊來取得用戶端驗證憑證和機密資料。  


### <a name="implement-access-controls-to-protect-the-reference-computer-imaging-process"></a>實作存取控制以保護參照電腦影像處理  

確定用來擷取 OS 映像的參照電腦位於安全的環境中。 使用適當的存取控制，如此一來，未預期的或惡意軟體就不會被安裝及不經意地包含在擷取的映像中。 當您擷取映像時，請確定目的地網路位置是安全的。 此程序有助於確保映像在擷取後不會遭到竄改。  


### <a name="always-install-the-most-recent-security-updates-on-the-reference-computer"></a>在參照電腦上一律安裝最新的安全性更新程式  

當參照電腦有最新的安全性更新程式時，就能減少新電腦第一次啟動時的漏洞。  


### <a name="implement-access-controls-when-deploying-an-os-to-an-unknown-computer"></a>將 OS 部署到未知電腦時可實作存取控制

如果您必須將 OS 部署到未知電腦，請實作存取控制以防止未經授權的電腦與網路連線。  

佈建未知電腦能提供便利方法，以依需求部署新電腦。 但它也讓攻擊者有效變成您網路上的受信任用戶端。 限制實體存取網路，以及監視用戶端以偵測未經授權的電腦。 

電腦若回應 PXE 起始的 OS 部署，可能會讓所有資料在程序期間損毀。 此行為可能會造成不經意重新格式化的系統無法使用。  


### <a name="enable-encryption-for-multicast-packages"></a>啟用多點傳送套件加密  

針對每個 OS 部署套件，您都可以在 Configuration Manager 利用多點傳送功能傳送套件時啟用加密。 這項設定有助於防止 Rogue 電腦加入多點傳送工作階段。 它也有助於防止攻擊者竄改傳輸。  


### <a name="monitor-for-unauthorized-multicast-enabled-distribution-points"></a>監視未經授權之啟用多點傳送發佈點  

如果攻擊者能夠取得您的網路存取權，就可以設定 Rogue 多點傳送伺服器來詐騙 OS 部署。  


### <a name="when-you-export-task-sequences-to-a-network-location-secure-the-location-and-secure-the-network-channel"></a>將工作順序匯出到網路位置時，保護位置和網路通道的安全

限制誰可以存取網路資料夾。  

在網路位置和站台伺服器之間使用 SMB 簽署或 IPsec，以防止攻擊者竄改匯出的工作順序。  


### <a name="if-you-use-the-task-sequence-run-as-account-take-additional-security-precautions"></a>如果您使用工作順序執行身分帳戶，請採取額外的安全預防措施

如果您使用[工作順序執行身分帳戶](../../core/plan-design/hierarchy/accounts.md#task-sequence-run-as-account)，請採取下列預防性步驟：  

- 使用具最小權限的帳戶。  

- 請勿對此帳戶使用網路存取帳戶。  

- 永不使帳戶成為網域系統管理員。  

- 永不設定此帳戶的漫遊設定檔。 工作順序在執行時會下載帳戶的漫遊設定檔，導致很容易在本機電腦上存取該設定檔。  

- 限制帳戶的範圍。 例如，為每一個工作順序建立不同的工作順序執行身分帳戶。 如果一個帳戶遭到洩露，則只有該帳戶可存取的用戶端電腦會遭到洩露。 如果命令列需要電腦的系統管理存取權，請考慮為工作順序執行身分帳戶單獨建立一個本機系統管理員帳戶。 在執行工作順序的所有電腦上建立此本機帳戶；如果不再需要，請立即刪除帳戶。  


### <a name="restrict-and-monitor-the-administrative-users-who-are-granted-the-os-deployment-manager-security-role"></a>限制並監視被授與 OS 部署管理員安全性角色的系統管理使用者

被授與 **OS 部署管理員**安全性角色的系統管理使用者可以建立自我簽署憑證。 之後這些憑證可用來模擬用戶端，並從 Configuration Manager 取得用戶端原則。  


### <a name="use-enhanced-http-to-reduce-the-need-for-a-network-access-account"></a>使用增強 HTTP 降低網路存取帳戶的需求

從 1806 版開始，當您啟用 [增強 HTTP](../../core/plan-design/hierarchy/enhanced-http.md) 時，數個 OS 部署案例不需要網路存取帳戶即可從發佈點下載內容。 如需詳細資訊，請參閱[工作順序和網路存取帳戶](planning-considerations-for-automating-tasks.md#BKMK_TSNetworkAccessAccount)。<!--1358278--> 



## <a name="security-issues-for-os-deployment"></a>OS 部署的安全性問題  

雖然 OS 部署是為您網路上的電腦部署最安全作業系統和設定的簡便方法，卻有下列安全性風險：  


### <a name="information-disclosure-and-denial-of-service"></a>洩漏資訊與阻斷服務  

如果攻擊者可取得您的 Configuration Manager 基礎結構控制權，就可以執行任何的工作順序。 此程序可能包括將所有用戶端電腦的硬碟格式化。 工作順序可以設定為包含機密資料，例如具備加入網域權限和磁碟區授權識別碼的帳戶。  


### <a name="impersonation-and-elevation-of-privileges"></a>模擬和提高權限  

工作順序可將電腦加入網域，其可提供 rogue 電腦已驗證的網路存取權。 

保護用於可開機工作順序媒體及 PXE 開機部署的用戶端驗證憑證。 當您擷取用戶端驗證憑證時，此程序給予攻擊者取得憑證私密金鑰的機會。 此憑證可讓他們模擬網路上的有效用戶端。 在此案例中，rogue 電腦可下載包含機密資料的原則。  

如果用戶端使用網路存取帳戶來存取儲存在狀態移轉點上的資料，這些用戶端便可有效地共用相同的身分識別。 它們可存取來自另一個使用網路存取帳戶之用戶端的狀態移轉資料。 資料會經過加密，因此只有原始用戶端可以讀取該資料，但資料有可能遭到竄改或刪除。  


### <a name="client-authentication-to-the-state-migration-point-is-achieved-by-using-a-configuration-manager-token-that-is-issued-by-the-management-point"></a>針對狀態移轉點的用戶端驗證是使用由管理點核發的 Configuration Manager 權杖所完成。  

Configuration Manager 不會限制或管理儲存在狀態移轉點上的資料量。 攻擊者可能會填滿可用的磁碟空間並造成拒絕服務。  


### <a name="if-you-use-collection-variables-local-administrators-can-read-potentially-sensitive-information"></a>如果您使用集合變數，本機系統管理員可以讀取潛在的敏感資訊。  

雖然集合變數有彈性方法以部署作業系統，但這項功能可能會造成資訊洩漏。  



##  <a name="privacy-information-for-os-deployment"></a><a name="bkmk_privacy"></a> OS 部署的隱私權資訊  

除了將 OS 部署至沒有 OS 的電腦之外，還可以使用 Configuration Manager 將使用者檔案與設定從一部電腦移轉至另一部電腦。 系統管理員會設定要傳輸的資訊，包括個人資料檔案、組態設定以及瀏覽器 Cookie。  

Configuration Manager 會將資訊儲存在狀態移轉點上，並在傳輸與儲存期間加密資訊。 只有與狀態資訊相關的新電腦才能擷取儲存的資訊。 如果新電腦遺失用來擷取資訊的金鑰，在電腦關聯執行個體物件上具有 [檢視復原資訊]  權限的 Configuration Manager 系統管理員可存取該資訊，並建立其與新電腦的關聯。 新電腦還原狀態資訊之後，預設會在一天後刪除資料。 您可以設定狀態移轉點何時移除標示為可刪除的資料。 Configuration Manager 不會將狀態移轉資訊儲存在站台資料庫中，而且不會將它傳送給 Microsoft。  

如果您使用開機映像部署 OS 映像，請一律使用預設選項以透過密碼來保護開機媒體。 密碼會加密儲存在工作順序內的任何變數，但未儲存在變數內的所有資訊則會有外洩的風險。  

OS 部署可以使用工作順序在部署程序期間執行許多不同的工作，包括安裝應用程式與軟體更新。 設定工作順序時，您還必須注意安裝軟體所產生的隱私權問題。  

根據預設，Configuration Manager 不會實作 OS 部署。 在收集使用者狀態資訊，或是建立工作順序或開機映像之前，需要數個設定步驟。  

設定 OS 部署之前，請考慮您的隱私需求。  



## <a name="see-also"></a>請參閱

[診斷和使用情況資料](../../core/plan-design/diagnostics/diagnostics-and-usage-data.md)

[Configuration Manager 的安全性和隱私權](../../core/plan-design/security/security-and-privacy.md)
