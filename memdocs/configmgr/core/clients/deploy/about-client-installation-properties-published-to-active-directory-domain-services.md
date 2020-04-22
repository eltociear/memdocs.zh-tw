---
title: Active Directory 中的用戶端安裝內容
titleSuffix: Configuration Manager
description: 將 Configuration Manager 的用戶端安裝內容發佈至 Active Directory Domain Services。
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 101d7d4d-92db-419d-b2ae-3c1c1dea68e9
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 49b2edf7234e53c3fc03542f803933463190e8c1
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81692066"
---
# <a name="about-client-installation-properties-published-to-active-directory-domain-services"></a>關於發佈至 Active Directory 網域服務的用戶端安裝內容

適用於：  Configuration Manager (最新分支)

當您擴充 Configuration Manager 的 Active Directory 架構並將站台發佈至 Active Directory Domain Services 時，許多用戶端安裝內容也會發佈至 Active Directory Domain Services。 如果電腦可以找到這些用戶端安裝內容，就可在 Configuration Manager 用戶端部署期間使用。  

 使用 Active Directory 網域服務發佈用戶端安裝內容的優點如下：  

-   以軟體更新點為基礎的安裝和群組原則用戶端安裝不需要在每台電腦上設定安裝參數。  

-   由於這是自動產生的資訊，因此可以排除手動輸入安裝內容所可能出現的人為錯誤風險。  

> [!NOTE]  
>  如需如何延伸 Configuration Manager 的 Active Directory 架構，以及如何發佈站台的詳細資訊，請參閱 [Configuration Manager 的架構延伸](../../plan-design/network/schema-extensions.md)。  

## <a name="client-installation-properties-published-to-active-directory-domain-services"></a>發佈至 Active Directory 網域服務的用戶端安裝內容  
以下是用戶端安裝內容的清單。 如需以下列出各個項目的詳細資訊，請參閱[關於用戶端安裝內容](../../../core/clients/deploy/about-client-installation-properties.md)。  

- Configuration Manager 站台碼。  

- 站台伺服器簽署憑證。  

- 受信任根金鑰。  

- 用戶端的 HTTP 和 HTTPS 連接埠。  

- 後援狀態點。 如果站台有多個後援狀態點，只有第一個安裝的後援狀態點會發佈至 Active Directory 網域服務。  

- 表示用戶端只能使用 HTTPS 進行通訊的設定。  

- 與 PKI 憑證相關的設定：  

  -   是否要使用用戶端 PKI 憑證。  

  -   憑證選擇的選擇準則。 這可能為必要項目，因為用戶端有多個可用於 Configuration Manager 的有效 PKI 憑證。  

  -   完成憑證選擇程序之後，如果用戶端有多個有效憑證，該設定可決定要使用哪一個憑證。  

  -   包含受信任根 CA 憑證清單的憑證發行者清單。  

- 在 用戶端推入安裝內容  對話方塊的 用戶端  索引標籤中指定的 Client.mis 安裝內容。

唯有在未使用下列任何方法指定其他內容的情況下，用戶端安裝 (CCMSetup) 才會使用發佈至 Active Directory 網域服務的內容：  

-   手動安裝方法 (本文稍後說明)

-   群組原則安裝方法 (本文稍後說明)

> [!NOTE]  
>  用於安裝用戶端的用戶端安裝內容。 用戶端安裝完畢且成功指派至 Configuration Manager 站台後，這些內容就可能所指派站台的新設定覆寫。  

 請運用下列各節的資訊判斷哪些 Configuration Manager 用戶端安裝方法會使用 Active Directory 網域服務取得用戶端安裝內容。  

## <a name="client-push-installation"></a>用戶端推入安裝  
 用戶端推入安裝不會使用 Active Directory 網域服務取得安裝內容。  

 反之，您可以在 [用戶端推入安裝內容]  對話方塊的 [安裝內容]  索引標籤中，指定用戶端安裝內容。 這些選項和與用戶端相關的站台設定全數儲存在一個檔案中，安裝用戶端時，用戶端會讀取該檔案。  

> [!NOTE]  
>  您不需要在 [安裝內容]  索引標籤中，指定用戶端推送安裝的 CCMSetup 內容、後援狀態點或受信任的根金鑰。使用用戶端推入安裝安裝用戶端時，會自動提供這些設定給用戶端。
除了 Client.msi 內容之外，CCMSetup 還支援下列參數：/forcereboot、/skipprereq、/logon、/BITSPriority、/downloadtimeout、/forceinstall

 如果站台發佈至 Active Directory Domain Services，系統會將您在 [安裝內容]  索引標籤中指定的任何內容發佈至 Active Directory Domain Services。 在不使用安裝內容執行 CCMSetup 的情況下，用戶端安裝會讀取這些設定。  

## <a name="software-update-point-based-installation"></a>以軟體更新點為基礎的安裝  
 以軟體更新為基礎的安裝方法不支援將在 CCMSetup 命令列中加入安裝內容。  

 如果未在用戶端電腦上使用群組原則佈建任何命令列內容，CCMSetup 會在 Active Directory 網域服務中搜尋安裝內容。  

## <a name="group-policy-installation"></a>群組原則安裝  
 群組原則安裝方法不支援將在 CCMSetup 命令列中加入安裝內容。  

 如果未在用戶端電腦上佈建任何命令列內容，CCMSetup 會在 Active Directory 網域服務中搜尋安裝內容。  

## <a name="manual-installation"></a>手動安裝  
 下列情況下，CCMSetup 會在 Active Directory 網域服務中搜尋安裝內容：  

-   CCMSetup.exe 命令之後未指定任何命令列內容。  

-   未使用群組原則在電腦上佈建安裝內容。  

## <a name="logon-script-installation"></a>登入指令碼安裝  
 下列情況下，CCMSetup 會在 Active Directory 網域服務中搜尋安裝內容：  

-   CCMSetup.exe 命令之後未指定任何命令列內容。  

-   未使用群組原則在電腦上佈建安裝內容。  

## <a name="software-distribution-installation"></a>軟體發佈安裝  
 下列情況下，CCMSetup 會在 Active Directory 網域服務中搜尋安裝內容：  

-   CCMSetup.exe 命令之後未指定任何命令列內容。  

-   未使用群組原則在電腦上佈建安裝內容。  

## <a name="installations-for-clients-that-cannot-access-active-directory-domain-services"></a>無法存取 Active Directory 網域服務的用戶端安裝  
這些用戶端電腦無法從 Active Directory 網域服務讀取或存取已發佈的安裝內容。

 這些用戶端包括︰  

-   工作群組電腦。  

-   指派至未發佈到 Active Directory 網域服務之 Configuration Manager 站台的用戶端。  

-   在用戶端連上網際網路時安裝的用戶端。  
