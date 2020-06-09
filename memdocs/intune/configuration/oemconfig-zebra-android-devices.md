---
title: 使用 Microsoft Intune 將多個 OEMConfig 設定檔部署至 Zebra 裝置 - Azure |Microsoft Docs
description: 使用 Microsoft Intune 在執行 Android 企業版的 Zebra 裝置上，建立及部署多個 OEMConfig 裝置組態設定檔。 使用 Zebra 動作與步驟來排序您的設定檔。
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 06/02/2020
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
ms.openlocfilehash: 2a38c445018200d9fe80db19142f123aba783b60
ms.sourcegitcommit: 8a023e941d90c107c9769a1f7519875a31ef9393
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/03/2020
ms.locfileid: "84311150"
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

在 Zebra 裝置上，您可以在每個裝置上同時擁有多個設定檔。 您可利用此功能，將 Zebra OEMConfig 設定分割成較小的設定檔。 例如，建立會影響所有裝置的基準設定檔。 接著，建立更多可設定裝置特定設定的設定檔。

Zebra 的 OEMConfig 結構描述也會使用**動作**。 動作是在裝置上執行的作業。 其不會設定任何設定。 使用這些動作可觸發檔案下載、清除剪貼簿等等。 如需完整的支援動作清單，請參閱 [Zebra 文件](https://techdocs.zebra.com/oemconfig/10-0/about/) (英文) (開啟 Zebra 的網站)。

例如，您建立了一個會將某些設定套用到裝置的 Zebra OEMConfig 設定檔。 還有另一個 Zebra OEMConfig 設定檔，包含會清除剪貼簿的動作。 您將第一個設定檔指派給 Zebra 裝置群組。 然後，您需要清除這些裝置上的剪貼簿。 您不需要變更第一個設定檔，就可以將第二個設定檔指派給相同的裝置群組。 清除裝置的剪貼簿時，不會重新傳送或影響在第一個設定檔中所建立的組態設定。

在另一個範例中，您指派設定了一個 OEMConfig 設定檔，已設有某些 Zebra 裝置設定。 而最近，使用者回報有關特定應用程式的問題，您想要清除該應用程式的快取。 請建立一個新 OEMConfig 設定檔，只包含「清除快取」動作。 然後將該設定檔指派給需要的裝置。

## <a name="ordering"></a>排序

當每部裝置上有多個設定檔時，無法保證部署的設定檔順序。 此行為是 Google Play 的限制。 若要依序執行作業，您可以使用 [Zebra 的交易步驟功能](https://techdocs.zebra.com/oemconfig/10-0/mc/) \(英文\) (會開啟 Zebra 的網站)。 

總而言之，若順序很重要，您可以使用 [Zebra 的交易步驟功能](https://techdocs.zebra.com/oemconfig/10-0/mc/) \(英文\) (會開啟 Zebra 的網站)。 若順序不重要，您可以使用多個 Intune 設定檔。 

讓我們來看看一些範例：

- 您想要先為所有剛註冊的 Zebra 裝置開啟藍牙，再設定這些裝置上的任何其他設定。 若要依序執行作業，請使用 Zebra 結構描述中的**步驟**功能。

  建立一個包含兩個「交易步驟」的 Intune 設定檔。 第一個步驟包含藍牙設定，而第二個步驟則進行其他的設定。 當 Zebra 的 OEMCong 應用程式接收到該設定檔時，其會依序執行步驟。

  如需詳細資訊，請參閱 [Zebra 交易步驟](https://techdocs.zebra.com/oemconfig/10-0/mc/) (英文) (開啟 Zebra 的網站)。

- 您想要讓所有 Zebra 裝置以 24 小時制顯示時間。 針對這些裝置中的某些裝置，您想要關閉相機。 時間與相機設定彼此不相依。

  建立兩個 Intune 設定檔：

  - **設定檔 1**：以 24 小時制顯示時間。 在星期一，此設定檔指派給了**所有 Zebra AE 裝置**群組。
  - **設定檔 2**：關閉相機。 在星期二，此設定檔指派給了 **Zebra AE 工廠裝置**群組。

  星期三，您對 Intune 註冊 10 個新的 Zebra 裝置。 已指派設定檔 1 與設定檔 2。 在新裝置與 Intune 同步之後，所有裝置就會收到設定檔。 裝置可能會在取得設定檔 1 之前，先取得了設定檔 2。

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
