---
title: 範例 PKI 憑證部署
titleSuffix: Configuration Manager
description: 遵循逐步範例以了解如何建立與部署 Configuration Manager 使用的 PKI 憑證。
ms.date: 02/14/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 3417ff88-7177-4a0d-8967-ab21fe7eba17
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 45ef103645630b8e203710ec0ff36a71b3cef4cf
ms.sourcegitcommit: 214fb11771b61008271c6f21e17ef4d45353788f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/07/2020
ms.locfileid: "82904239"
---
# <a name="step-by-step-example-deployment-of-the-pki-certificates-for-configuration-manager-windows-server-2008-certification-authority"></a>為 Configuration Manager 部署 PKI 憑證的逐步範例：Windows Server 2008 憑證授權單位

適用於：  Configuration Manager (最新分支)

此部署逐步範例使用 Windows Server 2008 憑證授權單位 (CA)，其中包含的程序會示範如何建立及部署 Configuration Manager 使用的公開金鑰基礎結構 (PKI) 憑證。 這些程序使用企業憑證授權單位 (CA) 和憑證範本。 這些步驟僅適用於測試網路以做為概念證明。  

由於目前沒有任何單一方法可部署必要的憑證，因此請參閱您的特殊 PKI 部署文件，以取得部署生產環境必要憑證所需的程序和最佳做法。 如需憑證需求的詳細資訊，請參閱 [Configuration Manager 的 PKI 憑證需求](pki-certificate-requirements.md)。  

> [!TIP]
> 對於＜測試網路需求＞一節中未記載的作業系統，您可以調整本主題中的相關指示。 不過，如果您正在 Windows Server 2012 上執行發行 CA，系統不會要求您提供憑證範本版本。 反而會在範本內容的 [相容性]  索引標籤處指定：  
>
> - **憑證授權單位**：**Windows Server 2003**  
>   - **憑證收件者**：**Windows XP / Server 2003**  

## <a name="test-network-requirements"></a><a name="BKMK_testnetworkenvironment"></a> 測試網路需求

逐步指示具有下列需求：  

- 測試網路正在使用 Windows Server 2008 來執行 Active Directory 網域服務，並安裝為單一網域、單一樹系。  

- 您有一個執行 Windows Server 2008 Enterprise Edition 的成員伺服器已安裝 Active Directory 憑證服務角色，並已設定為企業根憑證授權單位 (CA)。  

- 您有一部已安裝 Windows Server 2008 (Standard Edition 或 Enterprise Edition、R2 或更新版本) 的電腦，該電腦已指定為成員伺服器，且已安裝 Internet Information Services (IIS)。 此電腦將會是您將設定內部網路完整網域名稱 (FQDN) 以支援內部網路上的用戶端連線，以及設定網際網路 FQDN (如果您必須支援由 System Center Configuration Manager 和用戶端在網際網路上註冊的行動裝置) 的 Configuration Manager 站台系統伺服器。  

- 您有一個已安裝最新版 Service Pack 的 Windows Vista 用戶端，並且以包含 ASCII 字元的電腦名稱設定此電腦，且已加入網域中。 此電腦將會是 Configuration Manager 用戶端電腦。  

- 您可以使用根網域系統管理員帳戶或企業網域系統管理員帳戶登入，並使用此帳戶進行此範例部署中的所有程序。  

## <a name="overview-of-the-certificates"></a><a name="BKMK_overview2008"></a> 憑證的概觀

下表列出 Configuration Manager 可能需要的 PKI 憑證類型並描述其使用方式。  

|憑證需求|憑證描述|  
|-----------------------------|-----------------------------|  
|執行 IIS 的站台系統 Web 伺服器憑證|此憑證是用來加密資料以及對用戶端驗證伺服器。 它必須從 Configuration Manager 外部安裝在執行 Internet Information Services (IIS) 且在 Connfiguration Manager 中設定以使用 HTTPS 的站台系統伺服器上。<br /><br /> 如需設定和安裝此憑證的步驟，請參閱本主題中的[為執行 IIS 的站台系統部署 Web 伺服器憑證](#BKMK_webserver2008_cm2012)。|  
|供用戶端連線到雲端架構發佈點的服務憑證|如需設定和安裝此憑證的步驟，請參閱本主題中的[為雲端架構的發佈點部署服務憑證](#BKMK_clouddp2008_cm2012)。<br /><br /> **重要：** 此憑證會搭配 Windows Azure 管理憑證使用。 如需管理憑證的詳細資訊，請參閱[如何建立管理憑證](https://docs.microsoft.com/azure/cloud-services/cloud-services-certs-create#create-a-new-self-signed-certificate) \(部分機器翻譯\)，以及[如何將管理憑證新增至 Windows Azure 訂用帳戶](https://docs.microsoft.com/azure/cloud-services/cloud-services-configure-ssl-certificate-portal#step-3-upload-a-certificate) \(部分機器翻譯\)。|  
|Windows 電腦的用戶端憑證|此憑證是用來對已設定為使用 HTTPS 的站台系統驗證 Configuration Manager 用戶端電腦。 它也可用於管理點和狀態移轉點，以監視其在設定為使用 HTTPS 時的操作狀態。 它必須從 Configuration Manager 外部安裝在電腦上。<br /><br /> 如需設定和安裝此憑證的步驟，請參閱本主題中的[部署 Windows 電腦的用戶端憑證](#BKMK_client2008_cm2012)。|  
|發佈點的用戶端憑證|此憑證有兩種用途：<br /><br /> 憑證是用來在發佈點傳送狀態訊息之前，對具備 HTTPS 功能的管理點驗證發佈點。<br /><br /> 當選取 [為用戶端啟用 PXE 支援]  散佈點選項時，憑證會傳送至 PXE 開機的電腦，使其在部署作業系統期間可連線到具備 HTTPS 功能的管理點。<br /><br /> 如需設定和安裝此憑證的步驟，請參閱本主題中的[部署發佈點的用戶端憑證](#BKMK_clientdistributionpoint2008_cm2012)。|  
|適用於行動裝置的註冊憑證|此憑證是用來對已設定為使用 HTTPS 的站台系統驗證 Configuration Manager 行動裝置用戶端。 它必須在 Configuration Manager 上安裝為行動裝置註冊的一部分，而您要選擇已設定的憑證範本作為行動裝置用戶端設定。<br /><br /> 如需設定此憑證的步驟，請參閱本主題中的[為行動裝置部署註冊憑證](#BKMK_mobiledevices2008_cm2012)。|  
|Mac 電腦的用戶端憑證|您可以在使用 Configuration Manager 註冊時從 Mac 電腦要求並安裝此憑證，並選擇已設定的憑證範本作為行動裝置用戶端設定。<br /><br /> 如需設定此憑證的步驟，請參閱本主題中的[部署 Mac 電腦的用戶端憑證](#BKMK_MacClient_SP1)。|  

## <a name="deploy-the-web-server-certificate-for-site-systems-that-run-iis"></a><a name="BKMK_webserver2008_cm2012"></a> 為執行 IIS 的站台系統部署 Web 伺服器憑證

此憑證部署的程序如下：  

- 在憑證授權單位建立及發行 Web 伺服器憑證範本  

- 要求 Web 伺服器憑證  

- 設定 IIS 以使用 Web 伺服器憑證  

### <a name="create-and-issue-the-web-server-certificate-template-on-the-certification-authority"></a><a name="BKMK_webserver22008"></a> 在憑證授權單位建立及發行 Web 伺服器憑證範本

此程序會建立 Configuration Manager 站台系統的憑證範本，並將它新增至憑證授權單位。  

##### <a name="to-create-and-issue-the-web-server-certificate-template-on-the-certification-authority"></a>在憑證授權單位上建立及發行 Web 伺服器憑證範本

1.  建立一個包含成員伺服器並命名為 **ConfigMgr IIS Servers** 的安全性群組，以安裝將執行 IIS 的 Configuration Manager 站台系統。  

2.  在已安裝憑證服務的成員伺服器上，以滑鼠右鍵按一下 [憑證授權單位] 主控台的 [憑證範本]  ，然後選擇 [管理]  以載入 [憑證範本]  主控台。  

3.  在結果窗格中，以滑鼠右鍵按一下 [範本顯示名稱]  欄中有 [Web 伺服器]  的項目，然後選擇 [複製範本]  。  

4.  在 [複製範本]  對話方塊中，確認已選取 [Windows 2003 Server, Enterprise Edition]  ，然後選擇 [確定]  。  

    > [!IMPORTANT]  
    >  請勿選取 [Windows 2008 Server, Enterprise Edition]  。  

5.  在 [新範本的內容]  對話方塊的 [一般]  索引標籤上，輸入範本名稱 (例如 **ConfigMgr Web 伺服器憑證**) 來產生 Configuration Manager 站台系統會用到的 Web 憑證。  

6.  選擇 [主體名稱]  索引標籤，並確認已選取 [在要求中提供]  。  

7.  選擇 [安全性]  索引標籤，並從 [Domain Admins]  和 [Enterprise Admins]  安全性群組中移除 [註冊]  權限。  

8.  選擇 [新增]  ，在文字方塊中輸入 **ConfigMgr IIS Servers**，然後選擇 [確定]  。  

9. 選擇此群組的 [註冊]  權限，但請勿清除 [讀取]  權限。  

10. 選擇 [確定]  ，然後關閉 [憑證範本]  主控台。  

11. 在 [憑證授權單位] 主控台中，以滑鼠右鍵按一下 [憑證範本]  ，選擇 [新增]  ，然後選擇 [要發行的憑證範本]  。  

12. 在 [啟用憑證範本]  對話方塊中，選擇您剛才建立的新範本 [ConfigMgr Web 伺服器憑證]  ，然後選擇 [確定]  。  

13. 如果您不需要建立及發行其他憑證，請關閉 [憑證授權單位]  。  

###  <a name="request-the-web-server-certificate"></a><a name="BKMK_webserver32008"></a> 要求 Web 伺服器憑證  
 此程序可讓您指定將在站台系統伺服器內容中設定的內部網路和網際網路 FQDN 值，然後在執行 IIS 的成員伺服器上安裝 Web 伺服器憑證。  

##### <a name="to-request-the-web-server-certificate"></a>要求 Web 伺服器憑證  

1.  重新啟動執行 IIS 的成員伺服器，使用您設定的 [讀取]  和 [註冊]  權限，確認電腦可存取您建立的憑證範本。  

2.  依序選擇 [開始]  和 [執行]  ，然後輸入 **mmc.exe**。 在空白主控台中，選擇 [檔案]  ，然後選擇 [新增/移除嵌入式管理單元]  。  

3.  在 [新增或移除嵌入式管理單元]  對話方塊中，從 [可用的嵌入式管理單元]  清單中選擇 [憑證]  ，然後選擇 [新增]  。  

4.  在 [憑證嵌入式管理單元]  對話方塊中，選擇 [電腦帳戶]  ，然後選擇 [下一步]  。  

5.  在 [選取電腦]  對話方塊中，確定選取 [本機電腦: (執行這個主控台的電腦)]  ，然後選擇 [完成]  。  

6.  在 [新增或移除嵌入式管理單元]  對話方塊中，選擇 [確定]  。  

7.  在主控台中，展開 [憑證 (本機電腦)]  ，然後選擇 [個人]  。  

8.  以滑鼠右鍵按一下 [憑證]  ，選擇 [所有工作]  ，然後選擇 [要求新憑證]  。  

9. 在 [開始之前]  頁面上，選擇 [下一步]  。  

10. 如果看到 [選取憑證註冊原則]  頁面，請選擇 [下一步]  。  

11. 在 [要求憑證]  頁面上，從可用的憑證清單中識別 [ConfigMgr Web 伺服器憑證]  ，然後選擇 **[需要更多資訊才能註冊此憑證。請按一下此處以設定設定值。]** 。  

12. 在 [憑證內容]  對話方塊的 [主體]  索引標籤中，不要對 [主體名稱]  進行任何變更。 這表示 [主體名稱]  區段的 [值]  方塊會保留空白。 改為在 [別名]  區段中選擇 [類型]  下拉式清單，然後選擇 [DNS]  。  

13. 在 [值]  方塊中，指定您將在 Configuration Manager 站台系統內容中指定的 FQDN 值，然後選擇 [確定]  以關閉 [憑證內容]  對話方塊。  

     範例：  

    - 如果站台系統只接受來自內部網路的用戶端連線，而且站台系統伺服器的內部網路 FQDN 是 **server1.internal.contoso.com**，請輸入 **server1.internal.contoso.com**，然後選擇 [新增]  。  

    - 如果站台將接受來自內部網路和網際網路的用戶端連線，則站台系統伺服器的內部網路 FQDN 會是 **server1.internal.contoso.com** ，且站台系統伺服器的網際網路 FQDN 會是 **server.contoso.com**：  

        1.  輸入 **server1.internal.contoso.com**，然後選擇 [新增]  。  

        2.  輸入 **server.contoso.com**，然後選擇 [新增]  。  

        > [!NOTE]  
        >  您可以依照任何順序為 Configuration Manager 指定 FQDN。 不過，您應檢查將使用憑證的所有裝置 (例如行動裝置和 Proxy Web 伺服器) 是否可使用憑證主體別名 (SAN) 和 SAN 中的多個值。 如果裝置對於憑證中的 SAN 值的支援受到限制，您可能必須變更 FQDN 的順序或改用主體值。  

14. 在 [要求憑證]  頁面上，從可用的憑證清單中選擇 [ConfigMgr Web 伺服器憑證]  ，然後選擇 [註冊]  。  

15. 在 [憑證安裝結果]  頁面上，等待憑證安裝完成，然後選擇 [完成]  。  

16. 關閉 [憑證 (本機電腦)]  。  

###  <a name="configure-iis-to-use-the-web-server-certificate"></a><a name="BKMK_webserver42008"></a> 設定 IIS 以使用 Web 伺服器憑證  
 此程序會將已安裝的憑證繫結到 IIS [預設的網站]  。  

##### <a name="to-set-up-iis-to-use-the-web-server-certificate"></a>設定 IIS 以使用 Web 伺服器憑證  

1. 在已安裝 IIS 的成員伺服器上，依序選擇 [開始]  、[程式集]  和 [系統管理工具]  ，然後選擇 [Internet Information Services (IIS) 管理員]  。  

2. 展開 [站台]  ，以滑鼠右鍵按一下 [預設的網站]  ，然後選擇 [編輯繫結]  。  

3. 選擇 [https]  項目，然後選擇 [編輯]  。  

4. 在 [編輯站台繫結]  對話方塊中，使用 ConfigMgr Web 伺服器憑證範本來選取您所要求的憑證，然後選擇 [確定]  。  

   > [!NOTE]  
   >  如果您不確定哪一個是正確的憑證，請選擇其中一個，然後選擇 [檢視]  。 這可讓您比較所選憑證的詳細資料與 [憑證] 嵌入式管理單元中的憑證。 例如，[憑證] 嵌入式管理單元會顯示過去用於要求憑證的憑證範本。 然後您可以比對使用 ConfigMgr Web 伺服器憑證範本要求的憑證的憑證指紋，以及目前在 [編輯站台繫結]  對話方塊中所選取憑證的憑證指紋。  

5. 在 [編輯站台繫結]  對話方塊中選擇 [確定]  ，然後選擇 [關閉]  。  

6. 關閉 [Internet Information Services (IIS) 管理員]  。  

   成員伺服器現在已搭配 Configuration Manager Web 伺服器憑證進行設定。  

> [!IMPORTANT]  
>  當您在這部電腦上安裝 Configuration Manager 站台系統伺服器時，請確定您在站台系統內容中指定的 FQDN 與要求憑證時所指定的 FQDN 相同。  

##  <a name="deploy-the-service-certificate-for-cloud-based-distribution-points"></a><a name="BKMK_clouddp2008_cm2012"></a> 為雲端架構的發佈點部署服務憑證  

此憑證部署的程序如下：  

- [在憑證授權單位建立及發行自訂 Web 伺服器憑證範本](#BKMK_clouddpcreating2008)  

- [要求自訂 Web 伺服器憑證](#BKMK_clouddprequesting2008)  

- [匯出雲端架構發佈點的自訂 Web 伺服器憑證](#BKMK_clouddpexporting2008)  

###  <a name="create-and-issue-a-custom-web-server-certificate-template-on-the-certification-authority"></a><a name="BKMK_clouddpcreating2008"></a> 在憑證授權單位建立及發行自訂 Web 伺服器憑證範本  
 此程序會建立以 Web 伺服器憑證範本為基礎的自訂憑證範本。 此憑證適用於 Configuration Manager 雲端架構發佈點，且私密金鑰必須可以匯出。 憑證範本建立後，就會新增至憑證授權單位。  

> [!NOTE]
>  此程序使用的憑證範本與您為執行 IIS 的站台系統所建立的 Web 伺服器憑證範本不同。 雖然這兩種憑證都需要伺服器驗證功能，但雲端架構發佈點的憑證還需要您在 [主體名稱] 中輸入自訂的定義值，且必須匯出私密金鑰。 基於安全性最佳做法的考量，請勿將憑證範本設定為可匯出私密金鑰，除非這是必要的設定。 雲端架構的發佈點會需要此設定，因為您必須匯入檔案形式的憑證，而不是在憑證存放區中選擇。  
> 
>  當您為此憑證建立新的憑證範本時，您可以限制哪些可要求憑證的電腦可以匯出私密金鑰。 在生產網路中，您可能還需要考慮為此憑證新增下列變更：  
> 
> - 安裝憑證需要核准，以增強安全性。  
>   - 延長憑證有效期間。 由於每次在憑證到期之前您都必須匯出及匯入憑證，因此延長有效期間可降低必須重複此程序的頻率。 不過，延長有效期間也會降低憑證的安全性，因為這會讓攻擊者有更多的時間將私密金鑰解密和竊取憑證。  
>   - 使用憑證主體別名 (SAN) 中的自訂值可協助您在搭配 IIS 使用的標準 Web 伺服器憑證中識別此憑證。  

##### <a name="to-create-and-issue-the-custom-web-server-certificate-template-on-the-certification-authority"></a>在憑證授權單位建立及發行自訂 Web 伺服器憑證範本  

1.  建立一個包含成員伺服器並命名為 **ConfigMgr Site Servers** 的安全性群組，以安裝將管理雲端架構發佈點的 Configuration Manager 主要站台伺服器。  

2.  在執行 [憑證授權單位] 主控台的成員伺服器上，以滑鼠右鍵按一下 [憑證範本]  ，然後選擇 [管理]  以載入憑證範本管理主控台。  

3.  在結果窗格中，以滑鼠右鍵按一下 [範本顯示名稱]  欄中有 [Web 伺服器]  的項目，然後選擇 [複製範本]  。  

4.  在 [複製範本]  對話方塊中，確認已選取 [Windows 2003 Server, Enterprise Edition]  ，然後選擇 [確定]  。  

    > [!IMPORTANT]  
    >  請勿選取 [Windows 2008 Server, Enterprise Edition]  。  

5.  在 [新範本的內容]  對話方塊的 [一般]  索引標籤上，輸入範本名稱 (例如 **ConfigMgr 雲端架構發佈點憑證**) 來產生雲端架構發佈點的 Web 伺服器憑證。  

6.  選擇 [要求處理]  索引標籤，然後選擇 [允許匯出私密金鑰]  。  

7.  選擇 [安全性]  索引標籤，然後從 [Enterprise Admins]  安全性群組移除 [註冊]  權限。  

8.  選擇 [新增]  ，在文字方塊中輸入 **ConfigMgr Site Servers**，然後選擇 [確定]  。  

9. 選取此群組的 [註冊]  權限，但請勿清除 [讀取]  權限。  

10. 選擇 [加密]  索引標籤，並確定 [最小金鑰大小]  已設定為 **2048**。

11. 選擇 [確定]  ，然後關閉 [憑證範本]  主控台。  

12. 在 [憑證授權單位] 主控台中，以滑鼠右鍵按一下 [憑證範本]  ，選擇 [新增]  ，然後選擇 [要發行的憑證範本]  。  

13. 在 [啟用憑證範本]  對話方塊中，選擇您剛才建立的新範本 [ConfigMgr 雲端架構發佈點憑證]  ，然後選擇 [確定]  。  

14. 如果您不需要建立及發行其他憑證，請關閉 [憑證授權單位]  。  

###  <a name="request-the-custom-web-server-certificate"></a><a name="BKMK_clouddprequesting2008"></a> 要求自訂 Web 伺服器憑證  
 此程序會在將執行站台伺服器的成員伺服器上，要求並安裝自訂 Web 伺服器憑證。  

##### <a name="to-request-the-custom-web-server-certificate"></a>要求自訂 Web 伺服器憑證  

1.  在建立及設定 **ConfigMgr Site Servers** 安全性群組後重新啟動成員伺服器，以確保電腦可使用您設定的 [讀取]  和 [註冊]  權限來存取您建立的憑證範本。  

2.  依序選擇 [開始]  和 [執行]  ，然後輸入 **mmc.exe**。 在空白主控台中，選擇 [檔案]  ，然後選擇 [新增/移除嵌入式管理單元]  。  

3.  在 [新增或移除嵌入式管理單元]  對話方塊中，從 [可用的嵌入式管理單元]  清單中選擇 [憑證]  ，然後選擇 [新增]  。  

4.  在 [憑證嵌入式管理單元]  對話方塊中，選擇 [電腦帳戶]  ，然後選擇 [下一步]  。  

5.  在 [選取電腦]  對話方塊中，確定選取 [本機電腦: (執行這個主控台的電腦)]  ，然後選擇 [完成]  。  

6.  在 [新增或移除嵌入式管理單元]  對話方塊中，選擇 [確定]  。  

7.  在主控台中，展開 [憑證 (本機電腦)]  ，然後選擇 [個人]  。  

8.  以滑鼠右鍵按一下 [憑證]  ，選擇 [所有工作]  ，然後選擇 [要求新憑證]  。  

9. 在 [開始之前]  頁面上，選擇 [下一步]  。  

10. 如果看到 [選取憑證註冊原則]  頁面，請選擇 [下一步]  。  

11. 在 [要求憑證]  頁面上，從可用的憑證清單中識別 [ConfigMgr 雲端架構發佈點憑證]  ，然後選擇 [需要更多資訊才能註冊此憑證。請選擇此處以設定設定值]  。  

12. 在 [憑證內容]  對話方塊的 [主體]  索引標籤中，找到 [主體名稱]  並選擇 [一般名稱]  作為 [類型]  。  

13. 在 [值]  方塊中，使用 FQDN 格式指定您選擇的服務名稱以及網域名稱。 例如： **clouddp1.contoso.com**。  

    > [!NOTE]  
    >  確定此服務名稱在您的命名空間中是唯一的。 您將使用 DNS 來建立別名(CNAME 記錄)，以將此服務名稱對應至從 Windows Azure 自動產生的識別碼 (GUID) 和 IP 位址。  

14. 選擇 [新增]  ，然後選擇 [確定]  以關閉 [憑證內容]  對話方塊。  

15. 在 [要求憑證]  頁面上，從可用的憑證清單中選擇 [ConfigMgr 雲端架構發佈點憑證]  ，然後選擇 [註冊]  。  

16. 在 [憑證安裝結果]  頁面上，等待憑證安裝完成，然後選擇 [完成]  。  

17. 關閉 [憑證 (本機電腦)]  。  

###  <a name="export-the-custom-web-server-certificate-for-cloud-based-distribution-points"></a><a name="BKMK_clouddpexporting2008"></a> 匯出雲端架構發佈點的自訂 Web 伺服器憑證  
 此程序會將自訂 Web 伺服器憑證匯出為檔案，使您可在建立雲端架構的發佈點時將其匯入。  

##### <a name="to-export-the-custom-web-server-certificate-for-cloud-based-distribution-points"></a>匯出雲端架構發佈點的自訂 Web 伺服器憑證  

1. 在 [憑證 (本機電腦)]  主控台中，以滑鼠右鍵按一下剛才安裝的憑證，選擇 [所有工作]  ，然後選擇 [匯出]  。  

2. 在 [憑證匯出精靈] 中，選擇 [下一步]  。  

3. 在 [匯出私密金鑰]  頁面上，選擇 [是，匯出私密金鑰]  ，然後選擇 [下一步]  。  

   > [!NOTE]  
   >  如果此選項無法使用，表示該憑證在建立時未使用匯出私密金鑰選項。 在此案例中，您無法以所需的格式匯出憑證。 您必須將憑證範本設定為可匯出私密金鑰，然後再次要求憑證。  

4. 在 [匯出檔案格式]  頁面上，確定已選取 [個人資訊交換 - PKCS #12 (.PFX)]  選項。  

5. 在 [密碼]  頁面上，指定強式密碼以保護匯出的憑證及其私密金鑰，然後選擇 [下一步]  。  

6. 在 [要匯出的檔案]  頁面上，指定您要匯出的檔案名稱，然後選擇 [下一步]  。  

7. 若要關閉精靈，請在 [憑證匯出精靈]  頁面中選擇 [完成]  ，然後在確認對話方塊中選擇 [確定]  。  

8. 關閉 [憑證 (本機電腦)]  。  

9. 安全儲存檔案並確保您可以從 Configuration Manager 主控台存取它。  

   當您建立雲端架構的發佈點時，就可以將憑證匯入。  

##  <a name="deploy-the-client-certificate-for-windows-computers"></a><a name="BKMK_client2008_cm2012"></a> 部署 Windows 電腦的用戶端憑證  
 此憑證部署的程序如下：  

- 在憑證授權單位建立及發行工作站驗證憑證範本  

- 使用群組原則設定工作站驗證範本的自動註冊  

- 自動註冊工作站驗證憑證並在電腦上驗證其安裝  

###  <a name="create-and-issue-the-workstation-authentication-certificate-template-on-the-certification-authority"></a><a name="BKMK_client02008"></a> 在憑證授權單位建立及發行工作站驗證憑證範本  
 此程序會建立 Configuration Manager 用戶端電腦的憑證範本，並將其新增至憑證授權單位。  

##### <a name="to-create-and-issue-the-workstation-authentication-certificate-template-on-the-certification-authority"></a>在憑證授權單位上建立及發行工作站驗證憑證範本  

1.  在執行 [憑證授權單位] 主控台的成員伺服器上，以滑鼠右鍵按一下 [憑證範本]  ，然後選擇 [管理]  以載入憑證範本管理主控台。  

2.  在結果窗格中，以滑鼠右鍵按一下 [範本顯示名稱]  欄中有 [工作站驗證]  的項目，然後選擇 [複製範本]  。  

3.  在 [複製範本]  對話方塊中，確認已選取 [Windows 2003 Server, Enterprise Edition]  ，然後選擇 [確定]  。  

    > [!IMPORTANT]  
    >  請勿選取 [Windows 2008 Server, Enterprise Edition]  。  

4.  在 [新範本的內容]  對話方塊的 [一般]  索引標籤上，輸入範本名稱 (例如 **ConfigMgr 用戶端伺服器憑證**) 來產生 Configuration Manager 用戶端電腦會用到的用戶端憑證。  

5.  選擇 [安全性]  索引標籤， 選取 [網域電腦]  群組，然後選取 [讀取]  和 [自動註冊]  的額外權限。 請勿清除 [註冊]  。  

6.  選擇 [確定]  ，然後關閉 [憑證範本]  主控台。  

7.  在 [憑證授權單位] 主控台中，以滑鼠右鍵按一下 [憑證範本]  ，選擇 [新增]  ，然後選擇 [要發行的憑證範本]  。  

8.  在 [啟用憑證範本]  對話方塊中，選擇您剛才建立的新範本 [ConfigMgr 用戶端憑證]  ，然後選擇 [確定]  。  

9. 如果您不需要建立及發行其他憑證，請關閉 [憑證授權單位]  。  

###  <a name="configure-autoenrollment-of-the-workstation-authentication-template-by-using-group-policy"></a><a name="BKMK_client12008"></a> 使用群組原則設定工作站驗證範本的自動註冊  
 此程序會設定群組原則在電腦上自動註冊用戶端憑證。  

##### <a name="to-set-up-autoenrollment-of-the-workstation-authentication-template-by-using-group-policy"></a>使用群組原則設定工作站驗證範本的自動註冊  

1.  在網域控制站上，依序選擇 [開始]  和 [系統管理工具]  ，然後選擇 [群組原則管理]  。  

2.  移至您的網域，以滑鼠右鍵按一下網域，然後選擇 [在這個網域中建立 GPO 並連結到]  。  

    > [!NOTE]  
    >  此步驟會使用最佳作法來建立自訂設定的新群組原則，而不會編輯透過 Active Directory 網域服務所安裝的預設網域原則。 當您在網域層級指派此群組原則時，您就可以將其套用到網域中的所有電腦。 在生產環境中，您可以限制自動註冊，使其只能在選取的電腦上註冊。 您可以在組織單位層級指派群組原則，也可以透過安全性群組篩選網域群組原則，使其只會套用到群組中的電腦。 如果您限制自動註冊，請記得納入已設定為管理點的伺服器。  

3.  在 [新增 GPO]  對話方塊中，輸入新的群組原則名稱 (例如**自動註冊憑證**)，然後選擇 [確定]  。  

4.  在結果窗格的 [已連結的群組原則物件]  索引標籤上，以滑鼠右鍵按一下新的群組原則，然後選擇 [編輯]  。  

5.  在 [群組原則管理編輯器]  中，展開 [電腦設定]  下方的 [原則]  ，然後移至 [Windows 設定]   / [安全性設定]   / [公開金鑰原則]  。  

6.  以滑鼠右鍵按一下名為 [憑證服務用戶端 - 自動註冊]  的物件類型，然後選擇 [內容]  。  

7.  從 [設定模型]  下拉式清單中，依序選擇 [已啟用]  、[更新過期的憑證，更新擱置中的憑證並移除撤銷的憑證]  和 [更新使用憑證範本的憑證]  ，然後選擇 [確定]  。  

8.  關閉 [群組原則管理]  。  

###  <a name="automatically-enroll-the-workstation-authentication-certificate-and-verify-its-installation-on-computers"></a><a name="BKMK_client22008"></a> 自動註冊工作站驗證憑證並在電腦上驗證其安裝  
 此程序會在電腦上安裝用戶端憑證，並驗證其安裝。  

##### <a name="to-automatically-enroll-the-workstation-authentication-certificate-and-verify-its-installation-on-the-client-computer"></a>自動註冊工作站驗證憑證並在用戶端電腦上驗證其安裝  

1. 重新啟動工作站電腦，等待幾分鐘再登入。  

   > [!NOTE]  
   >  重新啟動電腦是確定憑證自動註冊是否成功的最可靠方法。  

2. 使用具有系統管理權限的帳戶登入。  

3. 在搜尋方塊中輸入 **mmc.exe**，然後按 **Enter**。  

4. 在空白的管理主控台中，選擇 [檔案]  ，然後選擇 [新增/移除嵌入式管理單元]  。  

5. 在 [新增或移除嵌入式管理單元]  對話方塊中，從 [可用的嵌入式管理單元]  清單中選擇 [憑證]  ，然後選擇 [新增]  。  

6. 在 [憑證嵌入式管理單元]  對話方塊中，選擇 [電腦帳戶]  ，然後選擇 [下一步]  。  

7. 在 [選取電腦]  對話方塊中，確定選取 [本機電腦: (執行這個主控台的電腦)]  ，然後選擇 [完成]  。  

8. 在 [新增或移除嵌入式管理單元]  對話方塊中，選擇 [確定]  。  

9. 在主控台中，依序展開 [憑證 (本機電腦)]  和 [個人]  ，然後選擇 [憑證]  。  

10. 在結果窗格中，確認憑證在 [使用目的]  欄中有 [用戶端驗證]  ，在 [憑證範本]  欄中有 [ConfigMgr 用戶端憑證]  。  

11. 關閉 [憑證 (本機電腦)]  。  

12. 針對成員伺服器重複執行步驟 1 到 11，以確認將設定為管理點的伺服器也有用戶端憑證。  

    電腦現在已搭配 Configuration Manager 用戶端憑證進行設定。  

##  <a name="deploy-the-client-certificate-for-distribution-points"></a><a name="BKMK_clientdistributionpoint2008_cm2012"></a> 部署發佈點的用戶端憑證  

> [!NOTE]  
>  此憑證也可以用於不使用 PXE 開機的媒體映像，因為憑證需求是相同的。  

 此憑證部署的程序如下：  

- 在憑證授權單位建立及發行自訂工作站驗證憑證範本  

- 要求自訂工作站驗證憑證  

- 匯出發佈點的用戶端憑證  

###  <a name="create-and-issue-a-custom-workstation-authentication-certificate-template-on-the-certification-authority"></a><a name="BKMK_clientdistributionpoint02008"></a> 在憑證授權單位建立及發行自訂工作站驗證憑證範本  
 此程序會為 Configuration Manager 發佈點建立可匯出私密金鑰的自訂憑證範本，並將憑證範本新增至憑證授權單位。  

> [!NOTE]
>  此程序使用的憑證範本與您為用戶端電腦所建立的憑證範本不同。 雖然這兩種憑證都需要用戶端驗證功能，但發佈點的憑證還需要匯出私密金鑰。 基於安全性最佳做法的考量，請勿將憑證範本設定為可匯出私密金鑰，除非這是必要的設定。 發佈點會需要此設定，因為您必須匯入檔案形式的憑證，而不是在憑證存放區中選擇。  
> 
>  當您為此憑證建立新的憑證範本時，您可以限制哪些可要求憑證的電腦可以匯出私密金鑰。 在我們的範例部署中，這些電腦將是您先前為執行 IIS 的 Configuration Manager 站台系統伺服器所建立的安全性群組。 在發佈 IIS 站台系統角色的實際執行網路上，考慮為執行發佈點的伺服器建立新的安全性群組，如此就能限制只有這些站台系統伺服器可以使用憑證。 您也可以考慮針對此憑證新增下列修改：  
> 
> - 安裝憑證需要核准，以增強安全性。  
>   - 延長憑證有效期間。 由於每次在憑證到期之前您都必須匯出及匯入憑證，因此延長有效期間可降低必須重複此程序的頻率。 不過，延長有效期間也會降低憑證的安全性，因為這會讓攻擊者有更多的時間將私密金鑰解密和竊取憑證。  
>   - 在憑證 [主體] 欄位或 [主體別名]\(SAN) 中使用自訂值，以協助識別此憑證是否為標準的用戶端憑證。 這對於將在多個發佈點上使用相同憑證的情況特別有用。  

##### <a name="to-create-and-issue-the-custom-workstation-authentication-certificate-template-on-the-certification-authority"></a>在憑證授權單位建立及發行自訂工作站驗證憑證範本  

1.  在執行 [憑證授權單位] 主控台的成員伺服器上，以滑鼠右鍵按一下 [憑證範本]  ，然後選擇 [管理]  以載入憑證範本管理主控台。  

2.  在結果窗格中，以滑鼠右鍵按一下 [範本顯示名稱]  欄中有 [工作站驗證]  的項目，然後選擇 [複製範本]  。  

3.  在 [複製範本]  對話方塊中，確認已選取 [Windows 2003 Server, Enterprise Edition]  ，然後選擇 [確定]  。  

    > [!IMPORTANT]  
    >  請勿選取 [Windows 2008 Server, Enterprise Edition]  。  

4.  在 [新範本的內容]  對話方塊的 [一般]  索引標籤上，輸入範本名稱 (例如 **ConfigMgr 用戶端發佈點憑證**) 來產生發佈點的用戶端驗證憑證。  

5.  選擇 [要求處理]  索引標籤，然後選擇 [允許匯出私密金鑰]  。  

6.  選擇 [安全性]  索引標籤，然後從 [Enterprise Admins]  安全性群組移除 [註冊]  權限。  

7.  選擇 [新增]  ，在文字方塊中輸入 **ConfigMgr IIS Servers**，然後選擇 [確定]  。  

8.  選取此群組的 [註冊]  權限，但請勿清除 [讀取]  權限。  

9. 選擇 [確定]  ，然後關閉 [憑證範本]  主控台。  

10. 在 [憑證授權單位] 主控台中，以滑鼠右鍵按一下 [憑證範本]  ，選擇 [新增]  ，然後選擇 [要發行的憑證範本]  。  

11. 在 [啟用憑證範本]  對話方塊中，選擇您剛才建立的新範本 [ConfigMgr 用戶端發佈點憑證]  ，然後選擇 [確定]  。  

12. 如果您不需要建立及發行其他憑證，請關閉 [憑證授權單位]  。  

###  <a name="request-the-custom-workstation-authentication-certificate"></a><a name="BKMK_clientdistributionpoint12008"></a> 要求自訂工作站驗證憑證  
 此程序會在執行 IIS 且將設定為發佈點的成員伺服器上，要求並安裝自訂用戶端憑證。  

##### <a name="to-request-the-custom-workstation-authentication-certificate"></a>要求自訂工作站驗證憑證  

1.  依序選擇 [開始]  和 [執行]  ，然後輸入 **mmc.exe**。 在空白主控台中，選擇 [檔案]  ，然後選擇 [新增/移除嵌入式管理單元]  。  

2.  在 [新增或移除嵌入式管理單元]  對話方塊中，從 [可用的嵌入式管理單元]  清單中選擇 [憑證]  ，然後選擇 [新增]  。  

3.  在 [憑證嵌入式管理單元]  對話方塊中，選擇 [電腦帳戶]  ，然後選擇 [下一步]  。  

4.  在 [選取電腦]  對話方塊中，確定選取 [本機電腦: (執行這個主控台的電腦)]  ，然後選擇 [完成]  。  

5.  在 [新增或移除嵌入式管理單元]  對話方塊中，選擇 [確定]  。  

6.  在主控台中，展開 [憑證 (本機電腦)]  ，然後選擇 [個人]  。  

7.  以滑鼠右鍵按一下 [憑證]  ，選擇 [所有工作]  ，然後選擇 [要求新憑證]  。  

8.  在 [開始之前]  頁面上，選擇 [下一步]  。  

9. 如果看到 [選取憑證註冊原則]  頁面，請選擇 [下一步]  。  

10. 在 [要求憑證]  頁面上，從可用的憑證清單中選擇 [ConfigMgr 用戶端發佈點憑證]  ，然後選擇 [註冊]  。  

11. 在 [憑證安裝結果]  頁面上，等待憑證安裝完成，然後選擇 [完成]  。  

12. 在結果窗格中，確認憑證在 [使用目的]  欄中有 [用戶端驗證]  ，在 [憑證範本]  欄中有 [ConfigMgr 用戶端發佈點憑證]  。  

13. 請勿關閉 [憑證 (本機電腦)]  。  

###  <a name="export-the-client-certificate-for-distribution-points"></a><a name="BKMK_exportclientdistributionpoint22008"></a> 匯出發佈點的用戶端憑證  
 此程序會將自訂工作站驗證憑證匯出為檔案，使其可以在發佈點內容中匯入。  

##### <a name="to-export-the-client-certificate-for-distribution-points"></a>匯出發佈點的用戶端憑證  

1. 在 [憑證 (本機電腦)]  主控台中，以滑鼠右鍵按一下剛才安裝的憑證，選擇 [所有工作]  ，然後選擇 [匯出]  。  

2. 在 [憑證匯出精靈] 中，選擇 [下一步]  。  

3. 在 [匯出私密金鑰]  頁面上，選擇 [是，匯出私密金鑰]  ，然後選擇 [下一步]  。  

   > [!NOTE]  
   >  如果此選項無法使用，表示該憑證在建立時未使用匯出私密金鑰選項。 在此案例中，您無法以所需的格式匯出憑證。 您必須將憑證範本設定為可匯出私密金鑰，然後再次要求憑證。  

4. 在 [匯出檔案格式]  頁面上，確定已選取 [個人資訊交換 - PKCS #12 (.PFX)]  選項。  

5. 在 [密碼]  頁面上，指定強式密碼以保護匯出的憑證及其私密金鑰，然後選擇 [下一步]  。  

6. 在 [要匯出的檔案]  頁面上，指定您要匯出的檔案名稱，然後選擇 [下一步]  。  

7. 若要關閉精靈，請在 [憑證匯出精靈]  頁面中選擇 [完成]  ，然後在確認對話方塊中選擇 [確定]  。  

8. 關閉 [憑證 (本機電腦)]  。  

9. 安全儲存檔案並確保您可以從 Configuration Manager 主控台存取它。  

   當您設定發佈點時，就可以將憑證匯入。  

> [!TIP]  
>  當您為未使用 PXE 開機的作業系統部署設定媒體映像，以及安裝必須與要求 HTTPS 用戶端連線的管理點連線之映像的工作順序時，便可以使用相同的憑證檔案。  

##  <a name="deploy-the-enrollment-certificate-for-mobile-devices"></a><a name="BKMK_mobiledevices2008_cm2012"></a> 為行動裝置部署註冊憑證  
 此憑證部署需要在憑證授權單位執行單一程序，以建立及發行註冊憑證範本。  

### <a name="create-and-issue-the-enrollment-certificate-template-on-the-certification-authority"></a>在憑證授權單位建立及發行註冊憑證範本  
 此程序會建立 Configuration Manager 行動裝置的註冊憑證範本，並將其新增至憑證授權單位。  

##### <a name="to-create-and-issue-the-enrollment-certificate-template-on-the-certification-authority"></a>在憑證授權單位建立及發行註冊憑證範本  

1. 建立一個安全性群組，其包含將在 Configuration Manager 中註冊行動裝置的使用者。  

2. 在已安裝憑證服務的成員伺服器上，以滑鼠右鍵按一下 [憑證授權單位] 主控台的 [憑證範本]  ，然後選擇 [管理]  以載入 [憑證範本] 管理主控台。  

3. 在結果窗格中，以滑鼠右鍵按一下 [範本顯示名稱]  欄中有 [已驗證的工作階段]  的項目，然後選擇 [複製範本]  。  

4. 在 [複製範本]  對話方塊中，確認已選取 [Windows 2003 Server, Enterprise Edition]  ，然後選擇 [確定]  。  

   > [!IMPORTANT]  
   >  請勿選取 [Windows 2008 Server, Enterprise Edition]  。  

5. 在 [新範本的內容]  對話方塊的 [一般]  索引標籤上，輸入範本名稱 (例如 **ConfigMgr 行動裝置註冊憑證**) 來產生受 Configuration Manager 管理之行動裝置的註冊憑證。  

6. 選擇 [主體名稱]  索引標籤，確定已選取 [用這項 Active Directory 資訊來建立]  ，針對 [主體名稱格式:]  選取 [一般名稱]  ，然後從 [在次要主體名稱中包含這些資訊]  清除 [使用者主體名稱 (UPN)]  。  

7. 依序選擇 [安全性]  索引標籤和包含要註冊行動裝置之使用者的安全性群組，然後選擇 [註冊]  的額外權限。 請勿清除 [讀取]  。  

8. 選擇 [確定]  ，然後關閉 [憑證範本]  主控台。  

9. 在 [憑證授權單位] 主控台中，以滑鼠右鍵按一下 [憑證範本]  ，選擇 [新增]  ，然後選擇 [要發行的憑證範本]  。  

10. 在 [啟用憑證範本]  對話方塊中，選擇您剛才建立的新範本 [ConfigMgr 行動裝置註冊憑證]  ，然後選擇 [確定]  。  

11. 如果您不需要建立及發行其他憑證，請關閉 [憑證授權單位] 主控台。  

    您現在可以在用戶端設定中設定行動裝置註冊設定檔時，選取行動裝置註冊憑證範本。  

##  <a name="deploy-the-client-certificate-for-mac-computers"></a><a name="BKMK_MacClient_SP1"></a> 部署 Mac 電腦的用戶端憑證  

此憑證部署需要在憑證授權單位執行單一程序，以建立及發行註冊憑證範本。  

###  <a name="create-and-issue-a-mac-client-certificate-template-on-the-certification-authority"></a><a name="BKMK_MacClient_CreatingIssuing"></a> 在憑證授權單位建立及發行 Mac 用戶端憑證範本  
 此程序會為 Configuration Manager Mac 電腦建立自訂憑證範本，並將憑證範本新增至憑證授權單位。  

> [!NOTE]  
>  此程序會使用不同於您為 Windows 用戶端電腦或發佈點所建立的憑證範本。  
>   
>  當您為此憑證建立新的憑證範本時，您可以將憑證要求限制為只有授權的使用者可以使用。  

##### <a name="to-create-and-issue-the-mac-client-certificate-template-on-the-certification-authority"></a>在憑證授權單位建立及發行 Mac 用戶端憑證範本  

1. 建立一個安全性群組，其包含系統管理使用者的使用者帳戶，而這些使用者將會使用 Configuration Manager 在 Mac 電腦上註冊憑證。  

2. 在執行 [憑證授權單位] 主控台的成員伺服器上，以滑鼠右鍵按一下 [憑證範本]  ，然後選擇 [管理]  以載入憑證範本管理主控台。  

3. 在結果窗格中，以滑鼠右鍵按一下 [範本顯示名稱]  欄中顯示 [已驗證的工作階段]  的項目，然後選擇 [複製範本]  。  

4. 在 [複製範本]  對話方塊中，確認已選取 [Windows 2003 Server, Enterprise Edition]  ，然後選擇 [確定]  。  

   > [!IMPORTANT]  
   >  請勿選取 [Windows 2008 Server, Enterprise Edition]  。  

5. 在 [新範本的內容]  對話方塊的 [一般]  索引標籤上，輸入範本名稱 (例如 **ConfigMgr Mac 用戶端憑證**) 來產生 Mac 用戶端憑證。  

6. 選擇 [主體名稱]  索引標籤，確定已選取 [用這項 Active Directory 資訊來建立]  ，針對 [主體名稱格式:]  選擇 [一般名稱]  ，然後從 [在次要主體名稱中包含這些資訊]  清除 [使用者主體名稱 (UPN)]  。  

7. 選擇 [安全性]  索引標籤，並從 [Domain Admins]  和 [Enterprise Admins]  安全性群組中移除 [註冊]  權限。  

8. 選擇 [新增]  ，指定您在步驟一建立的安全性群組，然後選擇 [確定]  。  

9. 選擇此群組的 [註冊]  權限，但請勿清除 [讀取]  權限。  

10. 選擇 [確定]  ，然後關閉 [憑證範本]  主控台。  

11. 在 [憑證授權單位] 主控台中，以滑鼠右鍵按一下 [憑證範本]  ，選擇 [新增]  ，然後選擇 [要發行的憑證範本]  。  

12. 在 [啟用憑證範本]  對話方塊中，選擇您剛才建立的新範本 [ConfigMgr Mac 用戶端憑證]  ，然後選擇 [確定]  。  

13. 如果您不需要建立及發行其他憑證，請關閉 [憑證授權單位]  。  

    您現在可以在設定註冊的用戶端設定時，選取 Mac 用戶端憑證範本。
