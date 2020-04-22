---
title: 保護電腦免受惡意程式碼的威脅
titleSuffix: Configuration Manager
description: 了解如何在 Configuration Manager 中實作 Endpoint Protection，以保護電腦免受惡意程式碼的攻擊。
ms.date: 05/30/2019
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: 539c7a89-3c03-4571-9cb4-02d455064eeb
author: mestew
ms.author: mstewart
manager: doubeby
ms.openlocfilehash: 6e0e350fe490de50a053e93f2922feba5e0ea8c5
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81706416"
---
# <a name="example-scenario-use-endpoint-protection-to-protect-computers-from-malware"></a>範例案例：使用 Endpoint Protection 保護電腦免受惡意程式碼的威脅

適用於：  Configuration Manager (最新分支)

本文提供一個範例案例，示範如何在 Configuration Manager 中實作 Endpoint Protection 以保護貴組織的電腦免受惡意程式碼的攻擊。  



## <a name="scenario-overview"></a>案例概觀

 Configuration Manager 已在 Woodgrove Bank 安裝並使用。 該銀行目前使用 System Center Endpoint Protection 保護電腦，以防範惡意程式碼的攻擊。 此外，該銀行也使用 Windows 群組原則以確保公司內的所有電腦上皆已啟用 Windows 防火牆，且當 Windows 防火牆阻擋新程式時通知使用者。  

因此，銀行要求 Configuration Manager 系統管理員將 Woodgrove Bank 的反惡意程式碼軟體升級為 System Center Endpoint Protection，以便能夠受益於最新的反惡意程式碼功能，同時透過 Configuration Manager 主控台來集中管理反惡意程式碼解決方案。 


## <a name="business-requirements"></a>商務需求

進行這項作業有下列需求：  

- 使用 Configuration Manager 來管理目前由群組原則所管理的 Windows 防火牆設定。  

- 使用 Configuration Manager 軟體，將惡意程式碼定義下載至電腦。 如果無法使用軟體更新，例如，如果電腦未連線到公司網路時，電腦就必須從 Microsoft Update 下載定義更新。  

- 使用者的電腦必須每天執行惡意程式碼的快速掃描。 但伺服器則必須於工作時間以外的星期六上午 1 點，執行完整的掃描。  

- 每次發生下列任一事件時，即傳送電子郵件警示：  

  -   在任何電腦上偵測到惡意程式碼  

  -   超過 5% 以上的電腦上偵測到相同的惡意程式碼威脅  

  -   在任何 24 小時的期間內偵測到 5 次以上相同的惡意程式碼威脅  

  -   在任何 24 小時的期間內偵測到 3 種以上不同類型的惡意程式碼  

  系統管理員接著執行下列步驟來實作 Endpoint Protection：  



##  <a name="steps-to-implement-endpoint-protection"></a>若要實作 Endpoint Protection 的步驟  

|程序|參考|  
|-------------|---------------|  
|系統管理員檢閱 Configuration Manager 中 Endpoint Protection 基本概念的相關可用資訊。|如需 Endpoint Protection 的概觀資訊，請參閱 [Endpoint Protection](endpoint-protection.md)。|  
|系統管理員檢閱使用 Endpoint Protection 的必要先決條件並進行實作。|如需 Endpoint Protection 先決條件的詳細資訊，請參閱 [Endpoint Protection 規劃](../plan-design/planning-for-endpoint-protection.md)。|  
|系統管理員只在 Woodgrove Bank 階層頂端的一個站台系統伺服器上，安裝 Endpoint Protection 站台系統角色。|如需如何安裝 Endpoint Protection 站台系統角色的詳細資訊，請參閱[設定 Endpoint Protection](endpoint-protection-configure.md) 中的＜先決條件＞。|  
|系統管理員將 Configuration Manager 設定為使用 SMTP 伺服器傳送電子郵件警示。<br /><br /> **注意︰** 若您想要於產生 Endpoint Protection 警示時收到電子郵件通知，才必須設定 SMTP 伺服器。|如需詳細資訊，請參閱[設定 Endpoint Protection 警示](endpoint-configure-alerts.md)。|  
|系統管理員建立一個裝置集合，其中包含所有電腦與伺服器，用以安裝 Endpoint Protection 用戶端。 他們將此集合命名為 **Endpoint Protection 保護的所有電腦**。<br /><br /> **提示：** 您無法設定使用者集合的警示。|如需如何建立集合的詳細資訊，請參閱[如何建立集合](../../core/clients/manage/collections/create-collections.md)|  
|系統管理員會設定下列集合警示： <br /><br />1) **已偵測到惡意程式碼**：系統管理員會設定 [嚴重]  的警示嚴重性。 <br /><br />2) **在多部電腦上偵測到相同類型的惡意程式碼**：系統管理員會設定 [嚴重]  的警示嚴重性，並指定當有超過 5% 的電腦偵測到惡意程式碼時就會產生警示。 <br /><br />3) **於指定的時間間隔內，在電腦上重複偵測到相同類型的惡意程式碼**：系統管理員會設定 [嚴重] 的警示嚴重性，並指定當 24 小時內偵測到惡意程式碼 5 次以上時就會產生警示。 <br /><br />4) **在指定的間隔於同一部電腦上偵測到多種類型的惡意程式碼**：系統管理員會設定 [嚴重] 的警示嚴重性，並指定當 24 小時內產生 3 種以上的惡意程式碼類型時就會產生警示。<br /><br /> **警示嚴重性**的值表示將在 Configuration Manager 主控台中顯示的警示等級，以及系統管理員在電子郵件訊息中收到的警示等級。<br /><br /> 他們另外還會選取 [在 Endpoint Protection 儀表板中檢視此集合]  選項，以便在 Configuration Manager 主控台中監視警示。|請參閱[設定 Endpoint Protection](endpoint-configure-alerts.md) 中的＜設定 Endpoint Protection 的警示＞。|  
|系統管理員使用自動部署規則，將 Configuration Manager 軟體更新設定為每天下載及部署 3 次定義更新。|如需詳細資訊，請參閱[設定 System Center Configuration Manager 中的 Endpoint Protection](endpoint-definitions-configmgr.md) 之＜使用 Configuration Manager 軟體更新來傳遞定義更新＞一節。|  
|系統管理員檢查預設反惡意程式碼原則中的設定，其中包含來自 Microsoft 所建議的安全性設定。 對於每天皆會執行快速掃描的電腦，其會變更下列設定：<br /><br /> 1) **在用戶端電腦上執行每日快速掃描**：**是**。<br /><br /> 2) **每日快速掃描排程時間**：**上午 9:00**。<br /><br /> 系統管理員注意到預設已選取 [從 Microsoft Update 發佈的更新]  作為定義更新的來源。 如此一來，當電腦無法收到 Configuration Manager 軟體更新時，即可從 Microsoft Update 下載定義以滿足業務需求。|請參閱[如何建立和部署 Endpoint Protection 的反惡意程式碼原則](endpoint-antimalware-policies.md)。|  
|系統管理員建立一個集合，其中只包含名稱為 **Woodgrove Bank 伺服器**的 Woodgrove Bank 伺服器。|請參閱[如何建立集合](../../core/clients/manage/collections/create-collections.md)|  
|系統管理員建立名稱為 **Woodgrove Bank 伺服器原則**的自訂反惡意程式碼原則。 他們只會新增 [排程掃描]  設定，並進行下列變更：<br /><br /> **掃描類型**：**完整**<br /><br /> **掃描日**：**星期六**<br /><br /> **掃描時間**：**上午 1:00**<br /><br /> **在用戶端電腦上執行每日快速掃描**：**否**。|請參閱[如何建立和部署 Endpoint Protection 的反惡意程式碼原則](endpoint-antimalware-policies.md)。|  
|系統管理員將 **Woodgrove Bank 伺服器原則**這個自訂反惡意程式碼原則，部署至 **Woodgrove Bank 伺服器**集合。|請參閱[如何建立和部署 Endpoint Protection 的反惡意程式碼原則](endpoint-antimalware-policies.md)一文中的＜將反惡意程式碼原則部署到用戶端電腦＞。|  
|系統管理員為 Endpoint Protection 建立一組新的自訂用戶端裝置設定，並將其命名為 **Woodgrove Bank Endpoint Protection 設定**。<br /><br /> **注意︰** 如果不想在階層中的所有用戶端上安裝及啟用 Endpoint Protection，請確定預設用戶端設定中的 [在用戶端電腦上管理 Endpoint Protection 用戶端]  與 [在用戶端電腦上安裝 Endpoint Protection 用戶端]  選項皆已設定為 [否]  。|如需詳細資訊，請參閱[設定 Endpoint Protection 的自訂用戶端設定](endpoint-protection-configure-client.md)。|  
|系統管理員會為 Endpoint Protection 設定下列設定：<br /><br /> **在用戶端電腦上管理 Endpoint Protection 用戶端**：**是**<br /><br /> 此設定與值可確保任何已安裝的現有 Endpoint Protection 用戶端，都會變成由 Configuration Manager 所管理。<br /><br /> **在用戶端電腦上安裝 Endpoint Protection 用戶端**：**是**。</br></br>**注意：** 從 Configuration Manager 1802 開始，Windows 10 裝置不需要安裝 Endpoint Protection 代理程式。 如果 Windows 10 裝置上已安裝該代理程式，Configuration Manager 不會將其移除。 系統管理員可移除至少執行 1802 用戶端版本之 Windows 10 裝置的 Endpoint Protection 代理程式。|如需詳細資訊，請參閱[設定 Endpoint Protection 的自訂用戶端設定](endpoint-protection-configure-client.md)。|  
|系統管理員將 [Woodgrove Bank Endpoint Protection 設定]  的用戶端設定，部署至 **Endpoint Protection 保護的所有電腦**集合。|請參閱 [Configuring Endpoint Protection in Configuration Manager](endpoint-antimalware-policies.md) (在 Configuration Manager 中設定 Endpoint Protection) 之＜設定 Endpoint Protection 的自訂用戶端設定＞。|  
|系統管理員使用 [建立 Windows 防火牆原則精靈] 來建立原則，方法是為該網域設定檔設定下列設定：<br /><br /> 1) **啟用 Windows 防火牆**：**是**<br /><br /> 2)<br />                    **當 Windows 防火牆封鎖新的程式時，通知使用者**：**是**|請參閱[如何建立及部署 Endpoint Protection 的 Windows 防火牆原則](../../protect/deploy-use/create-windows-firewall-policies.md)|  
|系統管理員將新防火牆原則部署到他們之前所建立 **Endpoint Protection 保護的所有電腦** 集合中。|請參閱[如何建立及部署 Endpoint Protection 的 Windows 防火牆原則](create-windows-firewall-policies.md)中的＜部署 Windows 防火牆原則＞一節|  
|系統管理員使用適用於 Endpoint Protection 的管理工作來管理反惡意程式碼與 Windows 防火牆原則、必要時對電腦執行隨選掃描、強制電腦下載最新的定義，以及指定在偵測到惡意程式碼時要採取的任何進一步動作。|請參閱[如何管理 Endpoint Protection 的反惡意程式碼原則及防火牆設定](endpoint-antimalware-firewall.md)|  
|系統管理員使用下列方法來監視 Endpoint Protection 的狀態，以及 Endpoint Protection 所採取的動作：<br /><br /> 1) 使用 [監視]  工作區中 [安全性]  下的 [Endpoint Protection 狀態]  節點。<br /><br /> 2) 使用 [資產與相容性]  工作區中的 [Endpoint Protection]  節點。<br /><br /> 3) 使用 Configuration Manager 的內建報告。|請參閱[如何監視 Endpoint Protection](monitor-endpoint-protection.md)|  

 根據公司給系統管理員的業務需求，他們向其主管回報已成功實作 Endpoint Protection，並確認 Woodgrove Bank 的電腦現已受反惡意程式碼保護。 

## <a name="next-steps"></a>後續步驟

如需詳細資訊，請參閱[如何設定 Endpoint Protection](endpoint-protection-configure.md)