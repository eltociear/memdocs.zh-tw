---
title: 站台元件
titleSuffix: Configuration Manager
description: 了解如何設定站台元件，以修改站台系統角色和站台狀態報告的行為。
ms.date: 10/26/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 5fccbbeb-0faa-4943-83c2-e67db62d392d
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: a3447e6ac71e9c5441a9e82034ee41eabda59374
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81700926"
---
# <a name="site-components-for-configuration-manager"></a>Configuration Manager 的站台元件

適用於：  Configuration Manager (最新分支)

針對每個 Configuration Manager 站台，您都可以設定站台元件，以修改站台系統角色和站台狀態報告的行為。 站台元件設定適用於站台，以及該站台上適用站台系統角色的每個執行個體。  

在 Configuration Manager 主控台中，移至 [系統管理]  工作區，展開 [站台設定]  ，然後選取 [站台]  節點。 選取站台。 在功能區的 [設定]  群組中，選擇 [設定站台元件]  。 選取下列其中一個選項：

- [軟體發佈](#software-distribution)  
- [軟體更新點](#software-update-point) 
- [作業系統部署](#operating-system-deployment)
- [管理點](#management-point)  
- [狀態報告](#status-reporting)  
- [電子郵件通知](#email-notification)
- [集合成員資格評估](#bkmk_colleval)


## <a name="about-site-components"></a>關於站台元件  

 在 Configuration Manager 主控台檢視不同站台元件的選項時，大部分選項的意義都可透過其名稱得知。 不過，下列詳細資料可協助解說某些較複雜的設定，或將您導向至其他內容。  

> [!Note]  
> 有些元件的可用選項會視您選取的是管理中心網站、主要站台或次要站台而有所不同。 有些元件則完全不適用於特定類型的站台。  



### <a name="software-distribution"></a>軟體發佈  

#### <a name="content-distribution-settings"></a>內容發佈設定
在 [一般]  索引標籤上，指定設定以修改站台伺服器將內容傳輸到其發佈點的方式。 如果您將用於並行發佈設定的值提高，內容發佈就可以使用更多的網路頻寬。  

#### <a name="pull-distribution-point"></a>提取發佈點
如需詳細資訊，請參閱[使用提取發佈點](../../../plan-design/hierarchy/use-a-pull-distribution-point.md)。

#### <a name="network-access-account"></a>網路存取帳戶
如需詳細資訊，請參閱[網路存取帳戶](../../../plan-design/hierarchy/accounts.md#network-access-account)。  


### <a name="software-update-point"></a>軟體更新點  

如需詳細資訊，請參閱[安裝軟體更新點](../../../../sum/get-started/install-a-software-update-point.md)。  


### <a name="operating-system-deployment"></a>作業系統部署

如需詳細資訊，請參閱[指定提供離線 OS 映像服務的磁碟機](../../../../osd/get-started/manage-operating-system-images.md#bkmk_servicing-drive)。


### <a name="management-point"></a>管理點  

在 [一般]  索引標籤上，將站台設定為將其管理點的相關資訊發佈至 Active Directory 網域服務。  

Configuration Manager 用戶端使用管理點來尋找服務，以及尋找界限群組成員資格和 PKI 憑證選擇選項這類站台資訊。 用戶端也會使用管理點，在下載軟體的站台和發佈點中尋找其他管理點。 管理點也可協助用戶端完成站台指派，以及下載用戶端原則與上傳用戶端資訊。  

用戶端用來尋找管理點的最安全方法，就是在 Active Directory 網域服務中發佈這些管理點。 此服務位置方法需要符合下列條件：

- 已延伸 Configuration Manager 的架構。
- 具有 [系統管理]  容器，包含可讓站台伺服器發佈至此容器的適當安全性權限。
- Configuration Manager 站台設定成發行到 Active Directory 網域服務。
- 用戶端屬於與站台伺服器樹系相同的 Active Directory 樹系。  

當內部網路上的用戶端無法使用 Active Directory 網域服務尋找管理點時，請使用 [DNS 發佈](../../../plan-design/hierarchy/understand-how-clients-find-site-resources-and-services.md#bkmk_dns)。  

如需服務位置的一般資訊，請參閱[了解用戶端如何找到站台資源和服務](../../../plan-design/hierarchy/understand-how-clients-find-site-resources-and-services.md)。  


#### <a name="publish-selected-intranet-management-points-in-dns"></a>在 DNS 中發佈選取的內部網路管理點
當內部網路上的用戶端無法從 Active Directory 網域服務找到管理點時，請指定此選項。 相反地，用戶端可以使用 DNS 服務位置資源記錄 (SRV RR) 在其指派的站台找到管理點。  

如果 Configuration Manager 要將內部網路管理點發行至 DNS，則必須符合下列所有條件：  

-   您的 DNS 服務包含 8.1.2 (含) 以上版本的 BIND。  

-   您的 DNS 伺服器已設定為自動更新，並支援服務位置資源記錄。  

-   Configuration Manager 中管理點的指定完整網域名稱 (FQDN) 在 DNS 中包含主機項目 (A 或 AAA 記錄)。  

> [!WARNING]  
>  對於要尋找 DNS 中所發行之管理點的用戶端，您必須將用戶端指派給特定站台，而不是使用自動站台指派。 設定這些用戶端，透過其管理點的網域尾碼來使用站台碼。 如需詳細資訊，請參閱[尋找管理點](../../../clients/deploy/assign-clients-to-a-site.md#locating-management-points)。  

如果 Configuration Manager 用戶端無法使用 Active Directory 網域服務或 DNS 在內部網路上尋找管理點，則會使用 [WINS](../../../plan-design/hierarchy/understand-how-clients-find-site-resources-and-services.md#bkmk_wins)。 為此站台安裝的第一個管理點設定為接受內部網路的 HTTP 用戶端連線時，即會自動發佈至 WINS。  


### <a name="status-reporting"></a>狀態報告  

這些設定會直接設定站台及用戶端狀態報表內含的詳細資料層級。  


### <a name="email-notification"></a>電子郵件通知  

指定帳戶和電子郵件伺服器詳細資料，讓 Configuration Manager 傳送警示的電子郵件通知。  

如需詳細資訊，請參閱[使用警示和狀態系統](../../manage/use-alerts-and-the-status-system.md)。


### <a name="collection-membership-evaluation"></a><a name="bkmk_colleval"></a> 集合成員資格評估  

使用此元件以設定累加式評估集合成員資格的頻率。 累加式評估只會更新已新增或變更資源的集合成員資格。  

如需詳細資訊，請參閱[集合的最佳做法](../../../clients/manage/collections/best-practices-for-collections.md)。



##  <a name="use-the-configuration-manager-service-manager-to-manage-site-components"></a><a name="BKMK_ServiceMgr"></a> 使用 Configuration Manager Service Manager 管理站台元件  

您可以使用 Configuration Manager Service Manager 來控制 Configuration Manager 服務，以及檢視任一 Configuration Manager 服務或工作執行緒的狀態。 這些服務和執行緒統稱為 Configuration Manager 元件。 了解 Configuration Manager 元件的下列陳述：  

-   元件可以在任何站台系統上執行。  

-   管理元件的方式與您管理 Windows 中的服務一樣。 您可以啟動、停止、暫停、繼續或查詢 Configuration Manager 元件。  

Configuration Manager 服務會在具有任務時執行。 此動作通常發生於將設定檔寫入元件的收件匣時。 


### <a name="use-the-configuration-manager-service-manager"></a>使用 Configuration Manager Service Manager  

1.  在 Configuration Manager 主控台中，移至 [監視]  工作區，展開 [系統狀態]  ，然後選取 [元件狀態]  節點。  

2.  在功能區的 [元件]  群組中，選取 [開始]  ，然後選擇 [Configuration Manager Service Manager]  。  

3.  Configuration Manager Service Manager 開啟時，連線至您要管理的網站。  

     如果您沒有看到要管理的站台，請移至 [站台]  功能表並選取 [連線]  。 然後輸入正確站台的站台伺服器名稱。  

4.  展開網站，並根據您要管理的元件所在位置瀏覽至 [元件]  或 [伺服器]  。  

5.  在右側窗格中，選取一個或多個元件。 然後，在 [元件]  功能表上，選取 [查詢]  以更新選取項目的狀態。  

6.  更新元件狀態後，使用 [元件]  功能表上四種以動作為基礎的選項之一，以修改元件作業。 要求動作後，您必須查詢元件，以顯示元件的新狀態。  

7.  完成修改元件操作狀態後，請關閉 Configuration Manager Service Manager。  
