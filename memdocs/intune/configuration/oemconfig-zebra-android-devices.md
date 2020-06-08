---
title: 使用 Microsoft Intune 將多個 OEMConfig 設定檔部署至 Zebra 裝置 - Azure |Microsoft Docs
description: 使用 Microsoft Intune 在執行 Android 企業版的 Zebra 裝置上，建立及部署多個 OEMConfig 裝置組態設定檔。 使用 Zebra 動作與步驟來排序您的設定檔。
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 05/12/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: ''
ms.technology: ''
ms.assetid: ''
ms.reviewer: jieyan
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 2227face347e6d82cf7807bea241eda4856c1d67
ms.sourcegitcommit: 302556d3b03f1a4eb9a5a9ce6138b8119d901575
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/27/2020
ms.locfileid: "83988684"
---
# <a name="deploy-multiple-oemconfig-profiles-to-zebra-devices-in-microsoft-intune"></a>在 Microsoft Intune 中對 Zebra 裝置部署多個 OEMConfig 設定檔

在 Microsoft Intune 中，使用 OEMConfig 來自訂適用於 Android 企業版裝置的 OEM 專屬設定。 這些設定是裝置製造商獨有的設定，同時使用 Intune 中的組態設定檔進行部署。

您可以在 Zebra 裝置上，對相同的裝置部署及指派多個設定檔。 現有的 OEMConfig 設定檔可在裝置下一次與 Intune 同步時，使用此功能。

本功能適用於：

- 執行 Android 企業版的 Zebra 裝置

若要深入了解 OEMConfig，包含其功能及使用方式，請參閱 [OEMConfig 組態設定檔](android-oem-configuration-overview.md)。

本文說明如何對 Zebra 裝置部署多個 OEMConfig 設定檔，以及說明如何排序與使用 Microsoft Intune 中的報告功能。

## <a name="prerequisites"></a>先決條件

建立 [OEMConfig 組態設定檔](android-oem-configuration-overview.md)。

## <a name="use-multiple-profiles"></a>使用多個設定檔

在 Zebra 裝置上，您可以在每個裝置上同時擁有多個設定檔。 您可利用此功能，將 Zebra OEMConfig 設定分割成較小的設定檔。 Zebra 的 OEMConfig 結構描述也會使用**動作**。 動作是在裝置上執行的作業。 其不會設定任何設定。 使用這些動作可觸發檔案下載、清除剪貼簿等等。 如需完整的支援動作清單，請參閱 [Zebra 文件](https://techdocs.zebra.com/oemconfig/10-0/about/) (英文) (開啟 Zebra 的網站)。

例如，您建立了一個會將某些設定套用到裝置的 Zebra OEMConfig 設定檔。 還有另一個 Zebra OEMConfig 設定檔，包含會清除剪貼簿的動作。 您將第一個設定檔指派給 Zebra 裝置群組。 然後，您需要清除這些裝置上的剪貼簿。 您不需要變更第一個設定檔，就可以將第二個設定檔指派給相同的裝置群組。 清除裝置的剪貼簿時，不會重新傳送或影響在第一個設定檔中所建立的組態設定。

在另一個範例中，您指派設定了一個 OEMConfig 設定檔，已設有某些 Zebra 裝置設定。 而最近，使用者回報有關特定應用程式的問題，您想要清除該應用程式的快取。 請建立一個新 OEMConfig 設定檔，只包含「清除快取」動作。 然後將該設定檔指派給需要的裝置。

## <a name="ordering"></a>排序

當每部裝置上有多個設定檔時，無法保證部署的設定檔順序。 此行為是 Google Play 的限制。 若要依序執行作業，可以使用 [Zebra 的交易功能](https://techdocs.zebra.com/oemconfig/9-1/mc/) (英文) (開啟 Zebra 的網站)。 讓我們來看看範例。

有兩個設定檔：

- **設定檔 1**：開啟藍牙。 此設定檔在星期一指派給了**所有裝置**群組。
- **設定檔 2**：設定所有其他設定。 此設定檔在星期二指派給了**所有裝置**群組。

在設定其他設定之前，必須先開啟藍牙。

星期三，您對 Intune 註冊 10 個新的 Zebra 裝置。 設定檔 1 與設定檔 2 指派給**所有裝置**群組。 在新裝置與 Intune 同步之後，所有裝置就會收到設定檔。 而這些裝置可能會收到設定檔 1 之前，先取得了設定檔 2。

請使用 Zebra 結構描述中的**步驟**功能，確認作業會依序執行。 在此情況下，可以建立一個包含兩個「交易步驟」的設定檔。 第一個步驟包含藍牙設定，而第二個步驟則進行其他的設定。 當 Zebra 的 OEMCong 應用程式接收到該設定檔時，Zebra 保證會依序執行步驟。

如需詳細資訊，請參閱 [Zebra 交易步驟](https://techdocs.zebra.com/oemconfig/9-1/mc/) (英文) (開啟 Zebra 的網站)。

## <a name="enhanced-reporting"></a>增強型回報

部署設定檔後，其會由裝置上的 Zebra OEMConfig 應用程式執行。 Zebra OEMConfig 應用程式會對 Intune 回報該設定檔的狀態。 在端點管理員系統管理中心內，可看到已部署之 OEMConfig 設定檔的狀態，以及所有錯誤或警告。

1. 開啟 [Microsoft 端點管理員系統管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)。
2. 選取您的 Zebra OEMConfig 設定檔 > [監視器]  >  [裝置狀態]。 此選項會顯示已指派有 OEMConfig 設定檔的裝置。
3. 選取裝置 > [裝置設定] > 選取您的 Zebra OEMConfig 設定檔。 此選項會顯示成功或失敗的設定檔設定。

    選取失敗的資料列。 隨即會顯示詳細資料，包含失敗原因的詳細資訊。

## <a name="next-steps"></a>後續步驟

- 深入了解 [OEMConfig 組態設定檔](android-oem-configuration-overview.md)。
- 在 Android 裝置系統管理員中，設定[行動延伸模組 (MX)](android-zebra-mx-overview.md)。
- [監視設定檔狀態](device-profile-monitor.md)。
