---
title: 監視電子郵件、Wi-Fi 和 VPN 設定檔
titleSuffix: Configuration Manager
description: 了解如何在 Configuration Manager 中監視電子郵件、Wi-Fi 和 VPN 設定檔的合規性狀態。
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: e2315b8b-98bc-40e1-8ef9-bfb5e69ab109
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 59e372641c303e77f0d88e655bb917660c9e677c
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81709426"
---
# <a name="monitor-email-wi-fi-and-vpn-profiles-in-configuration-manager"></a>在 Configuration Manager 中監視電子郵件、Wi-Fi 和 VPN 設定檔

適用於：  Configuration Manager (最新分支)

將 Configuration Manager 電子郵件、Wi-Fi 或 VPN 設定檔部署至階層中的使用者之後，您就可以使用下列程序監視設定檔的合規性狀態：  

-   [如何在 Configuration Manager 主控台中檢視相容性結果](#BKMK_console)  

-   [如何使用報告檢視相容性結果](#BKMK_Reports)  

##  <a name="how-to-view-compliance-results-in-the-configuration-manager-console"></a><a name="BKMK_console"></a> 如何在 Configuration Manager 主控台中檢視相容性結果  
 使用這個程序，在 Configuration Manager 主控台中檢視已部署設定檔的合規性詳細資料。  

#### <a name="to-view-compliance-results-in-the-configuration-manager-console"></a>在 Configuration Manager 主控台中檢視合規性結果  

1.  在 Configuration Manager 主控台中，按一下 [監視]  。  

2.  在 [監視]  工作區中按一下 [部署]  。  

3.  在 [部署]  清單中，選取您要檢閱相容性資訊的設定檔部署。  

4.  您可以在主頁面檢閱有關設定檔部署相容性的摘要資訊。 若要檢視更詳細的資訊，請選取設定檔部署，然後在 [首頁]  索引標籤的 [部署]  群組中，按一下 [檢視狀態]  以開啟 [部署狀態]  頁面。  

     [部署狀態]  頁面包含下列索引標籤：  

    -   **符合規範：** 根據受影響的資產數目，顯示設定檔的合規性。 您可以按兩下規則，在 [資產與相容性]  工作區的 [使用者]  節點下方建立臨時節點，其中包含與此設定檔相容的所有使用者。 [資產詳細資料]  窗格會顯示與設定檔相容的使用者。 按兩下清單中的使用者以顯示其他資訊。  

        > [!IMPORTANT]  
        >  如果設定檔在用戶端裝置上不適用，就不會進行評估；不過，會傳回為相容。  

    -   **錯誤：** 根據受影響的資產數目，顯示所選設定檔部署的所有錯誤清單。 您可以按兩下規則，在 [資產與相容性]  工作區的 [使用者]  節點下方建立臨時節點，其中包含因此設定檔而產生錯誤的所有使用者。 當您選取使用者時，[資產詳細資料]  窗格會顯示受到所選問題影響的使用者。 按兩下清單中的使用者以顯示與此問題有關的其他資訊。  

    -   **不符合規範：** 根據受影響的資產數目，顯示一份設定檔中所有不相容規則的清單。 您可以按兩下規則，在 [資產與相容性]  工作區的 [使用者]  節點下方建立臨時節點，其中包含與此設定檔不相容的所有使用者。 當您選取使用者時，[資產詳細資料]  窗格會顯示受到所選問題影響的使用者。 按兩下清單中的使用者以顯示與此問題有關的進一步資訊。  

    -   **未知：** 顯示未回報所選設定檔部署合規性的所有使用者清單，以及裝置目前的用戶端狀態。  

5.  在 [部署狀態]  頁面中，您可以檢閱與部署之設定檔相容性有關的詳細資訊。 [部署]  節點下方會建立一個臨時節點以協助您更快再找到此資訊。  

##  <a name="how-to-view-compliance-results-by-using-reports"></a><a name="BKMK_Reports"></a> 如何使用報告檢視相容性結果  
 合規性設定包含 System Center Configuration Manager 中的設定檔，亦包含數個內建報告，可讓您監視關於設定檔的資訊。 這些報告具有 [相容性和設定管理]  的報告類別。  

> [!IMPORTANT]  
>  當您在相容性設定報告中使用 [裝置篩選器]  和 [使用者篩選器]  參數時，必須使用萬用字元 (%)。  

 如需如何在 Configuration Manager 中設定報告的詳細資訊，請參閱[報告簡介](../../core/servers/manage/introduction-to-reporting.md)。  
