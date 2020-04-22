---
title: 遠端控制安全性隱私權
titleSuffix: Configuration Manager
description: 取得 Configuration Manager 中遠端控制的安全性和隱私權資訊。
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 272ee86b-d3d9-4fd9-b5c4-73e490e1a1e4
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 83631b331030f9648c3e88a2e101a013cfa0e98f
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81696396"
---
# <a name="security-and-privacy-for-remote-control-in-configuration-manager"></a>Configuration Manager 中的遠端控制安全性與隱私權

適用於：  Configuration Manager (最新分支)

本主題包含 Configuration Manager 中遠端控制的安全性和隱私權資訊。  

##  <a name="security-best-practices-for-remote-control"></a><a name="BKMK_Security_HardwareInventory"></a> 遠端控制的安全性最佳做法  
 當您使用遠端控制管理用戶端電腦使用下列安全性最佳作法。  

|安全性最佳做法|更多資訊|  
|----------------------------|----------------------|  
|當您連線到遠端電腦時，如果使用了 NTLM 而非 Kerberos 驗證，請勿繼續。|當 Configuration Manager 偵測到使用 NTLM 而非 Kerberos 驗證遠端控制工作階段，會出現提示警告您：無法驗證遠端電腦的身分識別。 請勿繼續進行遠端控制工作階段。 NTLM 驗證是比 Kerberos 弱的驗證通訊協定，更容易被重新執行和模擬。|  
|請不要在遠端控制檢視器中共用剪貼簿。|剪貼簿支援可執行檔和文字等物件，而且主機電腦的使用者可以在遠端控制工作階段使用剪貼簿在原始電腦上執行程式。|  
|從遠端管理電腦時，請勿輸入特殊權限帳戶的密碼。|監視鍵盤輸入的軟體可以擷取到密碼。 或者，如果用戶端電腦目前執行的程式不是遠端控制使用者所以為的程式，該程式可能在擷取密碼。 需要帳戶和密碼時，使用者應該輸入它們。|  
|遠端控制工作階段期間請鎖定鍵盤和滑鼠。|如果 Configuration Manager 偵測到遠端控制連線已終止，Configuration Manager 會自動鎖定鍵盤和滑鼠，讓使用者無法接管已開啟的遠端控制工作階段。 但這項偵測可能不會立即進行，而如果遠端控制服務已終止，偵測也不會發生。<br /><br /> 請在 [ConfigMgr 遠端控制]  視窗中選取 [鎖定遠端鍵盤和滑鼠]  動作。|  
|不要讓使用者在軟體中心內設定遠端控制設定。|不要啟用 [使用者可以在軟體中心變更原則或通知設定]  用戶端設定，以防使用者被監視。 若使用者將其變更，即可遠端地檢視相同電腦上的其他使用者。 <br /><br />**這項設定適用於電腦，不適用於登入的使用者**。|  
|啟用 **網域** Windows 防火牆設定檔。|啟用 [啟用用戶端防火牆例外設定檔的遠端控制]  用戶端設定，然後為內部網路電腦選取 **網域** Windows 防火牆。|  
|如果在遠端控制工作階段期間登出，又以其他使用者身分登入，請確定您登出再中斷遠端控制工作階段。|這種情況下如未登出，工作階段會保持開啟狀態。|  
|請勿提供使用者本機系統管理員權限。|當您提供使用者本機系統管理員權限時，他們可能會接管您的遠端控制工作階段或危害您的認證。|  
|請使用群組原則或 Configuration Manager 來設定遠端協助設定，但不要同時使用。|您可以使用 Configuration Manager 和群組原則來變更遠端協助設定的設定。 用戶端的群組原則重新整理時，預設只變更伺服器已變更的原則，以提升效率。 Configuration Manager 會變更本機安全性原則中的設定，除非強制更新群組原則，否則可能不會覆寫設定。<br /><br /> 這兩個位置的設定原則可能會造成結果不一致。 請選擇這些方法的其中之一來設定遠端協助設定。|  
|啟用 [提示使用者提供遠端控制權限]  用戶端設定。|雖然這項用戶端設定有很多方法可以提示使用者確認遠端控制工作階段，但啟用這項設定可以降低使用者在處理機密工作時被監視的機會。<br /><br /> 此外，請教育使用者確認在遠端控制工作階段期間所顯示的帳戶名稱，如果懷疑帳戶未獲得授權，請中斷工作階段連線。|  
|限制 [允許的檢視者] 清單。|使用者不需要本機系統管理員權限，也能夠能夠使用遠端控制。|  

### <a name="security-issues-for-remote-control"></a>遠端控制的安全性問題  
 使用遠端控制管理用戶端電腦具有下列安全性問題：  

-   請不要認為遠端控制稽核訊息是可靠的。  

     如果您開始遠端控制工作階段，並使用替代認證登入，原始帳戶就會傳送稽核訊息，不是使用替代認證的帳戶。  

     如果您複製遠端控制的二進位檔案，而不是安裝 Configuration Manager 主控台，就不會傳送稽核訊息，接著會在命令提示字元中執行遠端控制。  

##  <a name="privacy-information-for-remote-control"></a><a name="BKMK_Privacy_HardwareInventory"></a> 遠端控制的隱私權資訊  
 遠端控制可讓您在 Configuration Manager 用戶端電腦上檢視作用中的工作階段，而且可能可以檢視儲存在這些電腦上的任何資訊。 預設不啟用遠端控制。  

 雖然您可以設定遠端控制提供顯著的通知，並在遠端控制工作階段開始之前取得使用者同意，但仍然可以在不經使用者同意或覺察下監視使用者。 您可以設定 [只檢視] 或 [完全控制] 存取層級，使遠端控制不能變更任何內容。 遠端控制工作階段中會顯示連線系統管理員的帳戶，幫助使用者識別誰正在連線到他們的電腦。  

 Configuration Manager 預設會將遠端控制權限授與本機系統管理員群組。  

 設定遠端控制之前，請考慮您的隱私權需求。  
