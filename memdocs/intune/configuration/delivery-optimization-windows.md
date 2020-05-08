---
title: Microsoft Intune 中 Windows 10 的傳遞最佳化設定 - Azure | Microsoft Docs
description: 設定您利用 Intune 管理的 Windows 10 裝置如何使用傳遞最佳化。 在 Intune 中，建立裝置組態設定檔，以從網際網路安裝更新。 另請參閱如何使用傳遞最佳化設定檔來取代現有更新通道。
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 04/28/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: high
ms.technology: ''
ms.suite: ems
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.reviewer: kerimh
ms.openlocfilehash: c37563dee40d776d352dec4e0b8ef11b1dc8f67b
ms.sourcegitcommit: 7b3eed763b394075766ea080968889a8538bfe56
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/29/2020
ms.locfileid: "82506534"
---
# <a name="delivery-optimization-settings-in-microsoft-intune"></a>Microsoft Intune 中的傳遞最佳化設定

使用 Intune，您可以為 Windows 10 裝置使用傳遞最佳化設定，以減少那些裝置下載應用程式與更新時的頻寬耗用量。 設定傳遞最佳化作為裝置組態設定檔的一部分。  

本文描述如何設定傳遞最佳化設定，作為裝置組態設定檔的一部分。 在您建立設定檔之後，接著會將該設定檔指派或部署到您的 Windows 10 裝置。

若要檢視 Intune 支援的傳遞最佳化設定清單，請參閱 [Intune 的傳遞最佳化設定](delivery-optimization-settings.md)。  

若要了解 Windows 10 上的傳遞最佳化，請參閱 Windows 文件中的[傳遞最佳化更新](https://docs.microsoft.com/windows/deployment/update/waas-delivery-optimization)。  

## <a name="create-the-profile"></a>建立設定檔

1. 登入 [Microsoft Endpoint Manager 系統管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)。

2. 選取 [裝置]   > [組態設定檔]   > [建立設定檔]  。

3. 輸入下列內容：
   - **平台**：選取 [Windows 10 及更新版本]  。
   - **設定檔類型**：選取 [傳遞最佳化]  。

4. 選取 [建立]  。

5. 在 [基本]  頁面上，輸入新設定檔的名稱與描述，然後選擇 [下一步]  。

6. 在 [組態設定]  頁面上，定義要下載更新及應用程式的方式。 如需可用設定的資訊，請參閱 [Intune 的傳遞最佳化設定](delivery-optimization-settings.md)。

   當完成設定時，請選取 [下一步]  。

7. 在 [範圍 (標籤)]  頁面上，選取 [選取範圍標籤]  以開啟 [選取標籤]  窗格並指派範圍標籤到設定檔。
  
   選取 [下一步]  以繼續進行操作。

8. 在 [指派]  頁面上，選取將接收此設定檔的群組。 如需指派設定檔的詳細資訊，請參閱[指派使用者和裝置設定檔](../configuration/device-profile-assign.md)。

   選取 [下一步]  。

9. 在 [適用性規則]  頁面上，使用 [規則]  、[屬性]  和 [值]  選項來定義此設定檔在指派群組中套用的方式。

10. 在 [檢閱 + 建立]  頁面上，當您完成操作時，請選擇 [建立]  。 設定檔隨即建立並顯示在清單中。 接下來，[指派設定檔](device-profile-assign.md)，然後[監視其狀態](device-profile-monitor.md)。

## <a name="remove-delivery-optimization-from-windows-10-update-rings"></a>從 Windows 10 更新通道移除傳遞最佳化

傳遞最佳化先前設定為軟體更新通道的一部分。 從 2019 年 2 月開始，傳遞最佳化設定已設定為傳遞最佳化裝置組態設定檔的一部分，其中包括的其他設定會影響裝置的軟體更新傳遞。 如果還沒有這麼做，請透過將傳遞最佳化設定設定為 [未設定]  以將其從更新通道移除，然後使用傳遞最佳化設定檔來管理較大範圍的可用選項。

1. 建立傳遞最佳化裝置組態設定檔：

    1. 在 Microsoft Endpoint Manager 系統管理中心內，選取 [裝置]   > [組態設定檔]   > [建立設定檔]  。
    2. 輸入下列內容：

        - **名稱**：為新的設定檔輸入描述性名稱。
        - **描述**：輸入設定檔的描述。 這是選擇性設定，但建議執行。
        - **平台**：選取 [Windows 10 及更新版本]  。
        - **設定檔類型**：選取 [傳遞最佳化]  。
        - **設定**：針對 [傳遞最佳化下載模式]  ，除非您想要變更套用到裝置的設定，否則請選擇現有軟體更新通道所使用的相同模式。 選項包括：
            - **未設定**
            - **只有 HTTP，沒有任何對等**
            - **HTTP 混合 (具有相同 NAT 後方之對等互連)**
            - **HTTP 混合 (具有跨私人群組的對等互連)**
            - **混合網際網路對等的 HTTP**
            - **無對等的簡式下載模式**
            - **略過模式**
    3. 設定您可能要管理的任何其他設定。

2. 將此新的設定檔指派至與現有軟體更新通道相同的裝置和使用者。 [指派設定檔](device-profile-assign.md)列出步驟。

3. 將現有軟體通道取消設定：
    1. 在 Microsoft Endpoint Manager 系統管理中心內，移至 [軟體更新]  > [Windows 10 更新通道]。
    2. 在清單中，選取您的更新通道。
    3. 在設定中，將 [傳遞最佳化下載模式]  設定成 [未設定]  。
    4. 按一下 [確定]   > [儲存]  來儲存您的變更。

## <a name="next-steps"></a>後續步驟

[指派設定檔](device-profile-assign.md)並[監視其狀態](device-profile-monitor.md)。  
檢視 Intune 的[傳遞最佳化設定](delivery-optimization-settings.md)。
