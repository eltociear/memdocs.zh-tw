---
title: 部署資源存取設定檔
titleSuffix: Configuration Manager
description: 了解如何在 Configuration Manager 中部署 Wi-Fi、VPN 和憑證設定檔。
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: 3753608d-b539-44dc-8e3f-b631319e7687
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 0272c50429973cc3e15c295303b91593075ebe01
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81709456"
---
# <a name="deploy-resource-access-profiles-in-configuration-manager"></a>在 Configuration Manager 中部署資源存取設定檔

適用於：  Configuration Manager (最新分支)

建立下列其中一個資源存取設定檔之後，請將該檔案部署到一或多個集合：

- [Wi-Fi](create-wifi-profiles.md)
- [VPN](create-vpn-profiles.md)
- [憑證](create-certificate-profiles.md)

當您部署這些設定檔時，您可以指定目標集合，並指定用戶端評估設定檔相容性的頻率。  

## <a name="deploy-a-profile"></a>部署設定檔

1. 在 Configuration Manager 主控台中，移至 [資產與合規性]  工作區。 依序展開 [相容性設定]  和 [公司資源存取]  ，然後選擇適當的設定檔節點。 例如，[Wi-Fi 設定檔]  。

1. 在設定檔清單中，選取您想要部署的設定檔。 然後，在功能區 [常用]  索引標籤上的 [部署]  群組中，選取 [部署]  。  

1. 在 [部署設定檔] 視窗中，指定下列資訊：  

    - **集合**：選取您要部署設定檔的集合。

    - **產生警示**：啟用此選項可設定警示。 如果設定檔相容性低於指定日期和時間所指定的百分比，站台就會產生此警示。 您也可以選取是否要將警示傳送至 System Center Operations Manager。

    - **隨機延遲 (小時)** ：針對包含簡單憑證註冊通訊協定 (SCEP) 設定的設定檔，指定延遲時間範圍以避免網路裝置註冊服務 (NDES) 處理過度。 預設值為 `64` 小時。  

    - **指定此設定檔的合規性評估排程**：指定用戶端評估此設定檔合規性的頻率。 選取 [簡易排程]  或設定 [自訂排程]  。 根據預設，簡易排程會每隔 `12` 小時執行一次。

1. 選取 [確定]  以關閉視窗並建立部署。

## <a name="delete-a-deployment"></a>刪除部署

如果您想要刪除部署，請從清單中選取該部署。 在詳細資料窗格中，切換至 [部署]  索引標籤。選取部署，然後在功能區的 [部署]  索引標籤中，選取 [刪除]  。

> [!IMPORTANT]
> 當您移除 VPN 設定檔部署時，Configuration Manager 不會從 Windows 移除 VPN 設定檔。 如果要從裝置移除設定檔，請手動將其移除。

## <a name="next-steps"></a>後續步驟

[監視 Wi-Fi 和 VPN 設定檔](monitor-wifi-email-vpn-profiles.md)

[監視憑證設定檔](monitor-certificate-profiles.md)
