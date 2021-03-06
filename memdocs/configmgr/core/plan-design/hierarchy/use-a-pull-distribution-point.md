---
title: 提取發佈點
titleSuffix: Configuration Manager
description: 了解透過 Configuration Manager 使用提取發佈點的設定和限制。」
ms.date: 04/24/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 7d8f530b-1a39-4a9d-a2f0-675b516da7e4
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: c243897a4c52eff04263325b998c4b23d6b3dde4
ms.sourcegitcommit: ad4b3e4874a797b755e774ff84429b5623f17c5c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "82166582"
---
# <a name="use-a-pull-distribution-point-with-configuration-manager"></a>透過 Configuration Manager 使用提取發佈點

適用於：  Configuration Manager (最新分支)

當您在 Configuration Manager 主控台中將內容發佈至標準發佈點時，站台伺服器會將內容推送至發佈點。 提取發佈點會如同用戶端從來源位置下載以取得內容。  

當您將內容發佈至多個發佈點時，提取發佈點有助於降低站台伺服器的處理負載。 它們也可以加快將內容傳輸至每部伺服器的速度。 一般而言，站台伺服器上的發佈管理員元件會將內容傳輸至每個發佈點。 相反地，站台會卸載將內容傳輸至提取發佈點的程序。  

您可設定個別發佈點來作為提取發佈點。 針對每個提取發佈點，指定可從中取得內容的一或多個來源發佈點。 提取發佈點只能從您指定為來源發佈點的發佈點下載內容。

當您在主控台中將內容發佈至提取發佈點時，站台伺服器會傳送通知給它。 提取發佈點接著會從來源發佈點下載內容。 提取發佈點會從已具有內容複本的發佈點下載，以便管理內容傳輸作業。  

提取發佈點支援的設定和功能，與一般發佈點相同。 例如，提取發佈點支援：

- 多點傳送和 PXE 設定
- 內容驗證
- 依需求發佈內容
- 來自用戶端的 HTTP 或 HTTPS 通訊
- 與其他發佈點相同的憑證選項
- 個別管理，或以發佈點群組的成員進行管理  

您可以在安裝發佈點時設定提取發佈點。 建立發佈點之後，您可以透過編輯角色內容來將它設定為提取發佈點。 如需如何啟用發佈點作為提取發佈點的詳細資訊，請參閱[提取發佈點](../../servers/deploy/configure/install-and-configure-distribution-points.md#bkmk_config-pull)。  

編輯發佈點內容以移除設為提取發佈點的設定。 當您移除設為提取發佈點的設定時，它會恢復正常運作。 站台伺服器會管理發佈點的未來內容傳輸作業。  

## <a name="distribution-process"></a>發佈程序

當您將內容發佈至提取發佈點時，會發生下列一連串事件：

- 當您在主控台中將內容發佈至提取發佈點之後，站台伺服器上的套件傳輸管理員元件會檢查站台資料庫，以確認內容是否可在來源發佈點上使用。 如果它無法確認內容是否位於提取發佈點的來源發佈點上，則會每隔 20 分鐘重複檢查一次，直到確認內容可用為止。  

- 當套件傳輸管理員確認內容可用時，它會通知提取發佈點下載內容。 如果通知失敗，它會根據提取發佈點的軟體發佈元件 [重試設定]  來重試。 當提取發佈點收到此通知時，它會嘗試從其來源發佈點下載內容。  

- 當提取發佈點下載內容時，套件傳輸管理員會根據提取發佈點的軟體發佈元件 [狀態輪詢設定]  來輪詢狀態。  在提取發佈點完成內容的下載之後，它會將此狀態提交至管理點。  

## <a name="configure-site-component-settings"></a>設定站台元件設定

當您使用提取發佈點時，檢閱並設定下列站台元件設定：  

1. 在 Configuration Manager 主控台中，移至 [系統管理]  工作區，展開 [站台設定]  ，然後選取 [站台]  節點。  

2. 選取站台。 在功能區中，選取 [設定站台元件]  ，然後選取 [軟體發佈]  。  

3. 切換至 [提取發佈點]  索引標籤。  

4. 在 [重試設定]  群組中，檢閱下列值：  

    - **重試次數**：套件傳輸管理員會嘗試通知提取發佈點下載內容的次數。 嘗試次數達到此值之後，套件傳輸管理員會取消傳輸。 根據預設，此值為 30。  

    - **重試前延遲 (分鐘)** ：套件傳輸管理員在每次嘗試之間等待的分鐘數。 根據預設，此值為 20。  

5. 在 [狀態輪詢設定]  群組中，檢閱下列值：  

    - **輪詢次數**：套件傳輸管理員連絡提取發佈點以擷取作業狀態的次數。 如果在作業完成之前嘗試次數達到此值，套件傳輸管理員會取消傳輸。 根據預設，此值為 72。

    - **重試前延遲 (分鐘)** ：套件傳輸管理員在每次嘗試之間等待的分鐘數。 根據預設，此值為 60。

    > [!NOTE]  
    >  當套件傳輸管理員因超過輪詢重試次數而取消作業時，提取發佈點會繼續下載內容。 完成時，提取發佈點會傳送適當的狀態訊息，且主控台會反映新的狀態。  

## <a name="limitations"></a>限制

- 您無法將雲端發佈點設定為提取發佈點。  

- 您無法將站台伺服器上的發佈點角色設定為提取發佈點。  

- 預先設置的內容設定會覆寫提取發佈點設定。 如果您在提取發佈點上開啟 [啟用此發佈點供預先設置的內容使用]  選項，它會等待內容。 它不會從來源發佈點提取內容。 如同為預先設置的內容啟用的標準發佈點，它不會從站台伺服器接收內容。 如需詳細資訊，請參閱[預先設置的內容](manage-network-bandwidth.md#BKMK_PrestagingContent)。  

- 提取發佈點不會使用排程或速率限制設定。 當您將先前安裝的發佈點設定為提取發佈點時，會儲存但不使用排程與速率限制的設定。 如果稍後您移除提取發佈點設定，則會依先前的設定實作排程與速率限制設定。  

    > [!NOTE]  
    >  發佈點的內容中不會顯示 [排程]  和 [速率限制]  索引標籤。  

- 提取發佈點不會使用每個站台的 [軟體發佈元件內容]  的 [一般]  索引標籤上的設定。 這些設定包括 [同時發佈]  和 [多點傳送重試]  。  

- 若要從遠端樹系中的來源發佈點傳輸內容，請在提取發佈點上安裝 Configuration Manager 用戶端。 此外，請設定可存取來源發佈點的網路存取帳戶。 如果啟用 [為 HTTP 站台系統使用 Configuration Manager 產生的憑證]  站台選項，則不需要網路存取帳戶。<!--1358228-->  

- 如果提取發佈點同時為 Configuration Manager 用戶端，用戶端版本必須與安裝提取發佈點的 Configuration Manager 站台相同。 提取發佈點使用提取發佈點與 Configuration Manager 用戶端共通的 CCMFramework。  

## <a name="about-source-distribution-points"></a>關於來源發佈點  

設定提取發佈點時，指定一或多個來源發佈點：  

- 精靈只會顯示符合來源發佈點資格的發佈點。  

- 提取發佈點可以指定為其他提取發佈點的來源發佈點。  

- 當您使用 Configuration Manager 主控台時，只能將支援 HTTP 的發佈點指定為來源發佈點。  

- 使用 Configuration Manager SDK 指定為 HTTP 設定的來源發佈點。 若要使用為 HTTPS 設定的來源發佈點，請在提取發佈點上安裝 Configuration Manager 用戶端。  

- 如果遠端辦公室有較佳網際網路連線，或要降低 WAN 連結上的負載，請使用 Microsoft Azure 中的[雲端發佈點](use-a-cloud-based-distribution-point.md)作為來源。 提取發佈點必須能夠存取網際網路，才能與 Microsoft Azure 通訊。 內容必須發佈至來源雲端發佈點。<!--1321554-->  

    > [!Note]  
    > 此功能會導致您的 Azure 訂用帳戶需要支付資料儲存和網路輸出的費用。 如需詳細資訊，請參閱[使用雲端發佈點的成本](use-a-cloud-based-distribution-point.md#bkmk_cost)。  

> [!Tip]  
> 當提取發佈點從來源發佈點下載內容時，該提取發佈點會在 [發佈點使用摘要]  報告的 [存取的用戶端 (唯一)]  欄內計為用戶端。  

### <a name="source-priorities"></a>來源優先順序

- 將個別優先順序指派給每個來源發佈點，或為多個來源發佈點指派相同的優先順序。  

- 優先順序會決定提取發佈點從其來源發佈點要求內容的順序。  

- 提取發佈點一開始會與優先順序值最低的來源發佈點連絡。 如果有多個來源發佈點具有相同的優先順序，則提取發佈點會隨機選取具有該優先順序的其中一個來源。  

- 如果選取的來源無法使用內容，提取發佈點會接著嘗試從具有該相同優先順序的其他發佈點下載內容。  

- 如果具有指定優先順序的發佈點都沒有內容，則提取發佈點會嘗試從具有次高優先順序層級的來源發佈點下載內容。 它會繼續此搜尋，直到找到內容為止。

- 如果已指派的來源發佈點都沒有內容，則提取發佈點會等待 30 分鐘，然後重新開始此程序。  

## <a name="inside-the-pull-distribution-point"></a>提取發佈點內部

- 為管理內容的傳輸作業，提取發佈點使用 **CCMFramework** 元件。 Configuration Manager 用戶端包含此元件。  

- 當您啟用提取發佈點時，站台會安裝 **pulldp.msi**。 此安裝程式也會新增 CCMFramework 元件。 該架構不需要 Configuration Manager 用戶端。  

- 安裝提取發佈點之後，它主要使用 **CCMExec** 服務來運作。  

- 提取發佈點傳輸內容時，會使用內建於 Windows 的**背景智慧型傳送服務** (BITS)。 提取發佈點不需要您安裝 IIS 伺服器的 BITS 延伸模組。<!--sms.503672 -Clarified BITS use-->

- 如需操作詳細資料，請參閱有關提取發佈點的下列記錄檔：  

  - **DataTransferService.log**
  - **PullDP.log**

> [!TIP]
> 在新增提取發佈點之後，如果在記錄檔中看到 HTTP 403 錯誤，請進行下列變更：
>
> 1. 在來源發佈點上設定下列登錄值：`HKLM\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL, ClientAuthTrustMode = 2 (REG_DWORD)`
> 1. 將來源發佈點伺服器重新開機。
>
> 接下來，提取發佈點應該會開始從來源下載內容。 如需此登錄機碼的詳細資訊，請參閱 [TLS-SSL (安全通道 SSP) 概觀](https://docs.microsoft.com/windows-server/security/tls/what-s-new-in-tls-ssl-schannel-ssp-overview) (機器翻譯)。<!-- SCCMDocs#1973 -->

## <a name="see-also"></a>請參閱  

[內容管理的基本概念](fundamental-concepts-for-content-management.md)
