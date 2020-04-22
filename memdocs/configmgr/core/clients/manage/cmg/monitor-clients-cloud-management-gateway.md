---
title: 監視雲端管理閘道
titleSuffix: Configuration Manager
description: 透過雲端管理閘道 (CMG) 監視用戶端和網路流量。
ms.date: 06/17/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 15f72f80-9850-40ce-9c3a-443ba04b6a03
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: b3233dc2f6bd13e56f7555536c95d42a34e01d5e
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81695146"
---
# <a name="monitor-cloud-management-gateway"></a>監視雲端管理閘道

適用於：  Configuration Manager (最新分支)

在雲端管理閘道 (CMG) 執行且用戶端可透過它進行連線之後，您可以監視用戶端與網路流量，以掌握服務的執行狀況。


## <a name="monitor-clients"></a>監視用戶端

透過 CMG 進行連線的用戶端，在設定管理員主控台中顯示的方式與內部部署用戶端相同。 如需詳細資訊，請參閱[如何監視用戶端](../monitor-clients.md)。


## <a name="monitor-traffic-in-the-console"></a>在主控台中監視流量

使用設定管理員主控台監視 CMG 上的流量：

1. 移至 [系統管理]  工作區，展開 [雲端服務]  ，然後選取 [雲端管理閘道]  節點。  

2. 在清單窗格中選取 CMG。  

3. 針對 CMG 連接點，以及其連線的站台系統角色，檢視詳細資料窗格中的流量資訊。 這些統計資料顯示傳入至這些角色的用戶端要求。 要求包括原則、位置、註冊、內容、清查及用戶端通知。<!-- SCCMDocs#1208 -->

## <a name="set-up-outbound-traffic-alerts"></a>設定輸出流量警示

輸出流量警示可協助您了解網路流量何時趨近 14 天的閾值。 當您建立 CMG 時，可以設定流量警示。 如果您略過這個部分，仍可在服務執行之後設定警示。 隨時調整警示設定。

1. 移至 [系統管理]  工作區，展開 [雲端服務]  ，然後選取 [雲端管理閘道]  節點。  

2. 在清單窗格中選取 CMG，然後選取功能區中的 [內容]  。  

3. 移至 [警示]  索引標籤以啟用閾值和警示。 指定 14 天的資料閾值 (GB)。 並指定引發不同警示等級的閾值百分比。  

4. 完成後，請選取 [確定]  。  


## <a name="monitor-logs"></a>監視記錄檔

CMG 會在數個記錄檔中產生項目。 如需詳細資訊，請參閱 [Configuration Manager 記錄檔](../../../plan-design/hierarchy/log-files.md#cloud-management-gateway)。


## <a name="cloud-management-dashboard"></a>雲端管理儀表板

<!--1358461-->
從 1806 版開始，雲端管理儀表板提供 CMG 使用量的集中式檢視。 當站台連線到 [Azure 服務](../../../servers/deploy/configure/azure-services-wizard.md)進行雲端管理時，它也會顯示雲端使用者和裝置相關資料。  

下列螢幕擷取畫面顯示雲端管理儀表板的某個部分顯示兩個可用的圖格：  
![雲端管理儀表板圖格 CMG 流量和目前的線上用戶端](media/1358461-cmg-dashboard.png)

在 Configuration Manager 主控台中，按一下 [監視]  工作區。 選取 [雲端管理]  節點，並檢視儀表板圖格。  


## <a name="connection-analyzer"></a>連接分析器

從 1806 版開始，您可以使用 CMG 連接分析器進行即時驗證，以協助解決問題。 主控台內的公用程式會檢查目前狀態的服務，以及檢查 CMG 連接點與任何允許 CMG 流量的管理點，二者之間通訊頻道。

1. 在 Configuration Manager 主控台中，移至 [系統管理]  工作區。 展開 [雲端服務]  ，然後選取 [雲端管理閘道]  節點。  

2. 選取目標 CMG 執行個體，然後選取功能區中的 [連接分析器]  。  

3. 在 CMG 連接分析器視窗中，選取下列其中一個選項，向服務進行驗證：  

     1. **Azure AD 使用者**：使用此選項來模擬以雲端使用者身分登入已加入 Azure AD 的 Windows 10 裝置通訊。 按一下 [登入]  ，放心輸入這個 Azure AD 使用者帳戶的認證。  

     2. **用戶端憑證**：使用此選項來模擬利用[用戶端驗證憑證](certificates-for-cloud-management-gateway.md#bkmk_clientauth)的 Configuration Manager 用戶端通訊。  

4. 選取 [開始]  以開始分析。 分析器視窗會顯示結果。 選取一個項目，然後在 [描述] 欄位查看更多的詳細資訊。  


## <a name="stop-cmg-when-it-exceeds-threshold"></a><a name="bkmk_stop"></a> CMG 超過閾值時予以停止

<!--3735092-->
從 1902 版開始，Configuration Manager 現可在總資料傳輸超過限制時停止 CMG 服務。 使用[警示](#set-up-outbound-traffic-alerts)，在使用量達到警告或重大層級時觸發通知。 為了協助減少因使用量突然增加而導致的任何非預期 Azure 成本，這個選項會關閉雲端服務。

> [!Important]  
> 即使服務未執行，但仍然有與雲端服務建立關聯的成本。 停止服務並不會消除所有相關聯的 Azure 成本。 若要移除雲端服務的所有成本，請[移除 CMG](setup-cloud-management-gateway.md#modify-a-cmg)。  
>
> 當 CMG 服務停止時，以網際網路為基礎的用戶端無法與 Configuration Manager 進行通訊。  

總資料傳輸 (輸出) 會包含來自雲端服務和儲存體帳戶的資料。 此資料來自下列流程：

- CMG 至用戶端  
- CMG 至站台，包括 CMG 記錄檔  
- 儲存體帳戶至用戶端 (如果您針對內容啟用 CMG 的話)  

如需這些資料流程的詳細資訊，請參閱 [CMG 連接埠和資料流程](plan-cloud-management-gateway.md#ports-and-data-flow)。

儲存體警示閾值是獨立的。 該警示會監視 Azure 儲存體執行個體的容量。

當您在主控台的 [雲端管理閘道]  節點中選取 CMG 執行個體時，可以看到 [詳細資料] 窗格中的總資料傳輸。

Configuration Manager 會每隔六分鐘檢查閾值一次。 如果使用量突然增加，Configuration Manager 可能需要最多六分鐘的時間，才能偵測到它超過閾值，接著停止服務。

### <a name="process-to-stop-the-cloud-service-when-it-exceeds-threshold"></a>雲端服務超過閾值時予以停止的程序

1. [設定輸出流量警示](#set-up-outbound-traffic-alerts)。  

2. 在 CMG 屬性視窗的 [警示]  索引標籤上，啟用 [超出重大閾值時，停止此服務]  的選項。  

若要測試此功能，請暫時降低下列其中一個值：  

- **輸出資料傳輸的 14 天閾值 (GB)** 。 預設值為 `10000`。  

- **引發重大警示的閾值百分比**。 預設值為 `90`。  
