---
title: 來自 WSUS 的 Endpoint Protection 惡意程式碼定義
titleSuffix: Configuration Manager
ms.date: 04/23/2020
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: a34d9401-83e4-471d-8e23-b8042fc11c90
author: mestew
ms.author: mstewart
description: 了解如何設定 Windows Server Updates Services 以自動核准定義更新。
manager: dougeby
ms.openlocfilehash: 235caff52b877177b92792bf8d9fb3a2007127a5
ms.sourcegitcommit: 2871a17e43b2625a5850a41a9aff447c8ca44820
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/24/2020
ms.locfileid: "82126031"
---
# <a name="enable-endpoint-protection-malware-definitions-to-download-from-wsus-for-configuration-manager"></a>啟用 Endpoint Protection 惡意程式碼定義來從適用於 Configuration Manager 的 WSUS 下載

適用於：  Configuration Manager (最新分支)

如果您使用 WSUS 將反惡意程式碼定義維持在最新狀態，則您可以將其設定為自動核准定義更新。 雖然建議使用 Configuration Manager 軟體更新來將定義維持在最新狀態，但也可設定 WSUS，以將其作為允許使用者手動更新定義的方法。 使用下列程序將 WSUS 設定為定義更新來源。

## <a name="synchronize-definition-updates-for-configuration-manager"></a>同步 Configuration Manager 的定義更新

1. 在 Configuration Manager 主控台中，前往 [管理]  工作區，展開 [站台設定]  ，然後選取 [站台]  。

1. 選取包含軟體更新點的網站。 在功能區的 [設定]  群組中，選取 [設定站台元件]  ，然後選取 [軟體更新點]  。

1. 在 [軟體更新點元件內容]  視窗中，切換至 [分類]  索引標籤。選取 [定義更新]  。

1. 若要指定使用 WSUS 更新的 [產品]  ，請切換至 [產品]  索引標籤。

    - 針對 Windows 10 及更新版本：在 [Microsoft] > [Windows] 下方，選取 [Windows Defender]  。

    - 針對 Windows 8.1 及更早版本：在 [Microsoft] > [Forefront] 下方，選取 [System Center Endpoint Protection]  。

1. 選取 [確定]  以關閉 [軟體更新點元件內容]  視窗。

## <a name="synchronize-definition-updates-for-standalone-wsus"></a>同步獨立 WSUS 的定義更新

使用下列程序以在 WSUS 伺服器未與 Configuration Manager 環境整合時設定 Endpoint Protection 更新。

1. 在 WSUS 管理主控台中，展開 [電腦]  ，選取 [選項]  ，然後選取 [產品和分類]  。

1. 若要指定使用 WSUS 更新的 [產品]  ，請切換至 [產品]  索引標籤。

    - 針對 Windows 10 及更新版本：在 [Microsoft] > [Windows] 下方，選取 [Windows Defender]  。

    - 針對 Windows 8.1 及更早版本：在 [Microsoft] > [Forefront] 下方，選取 [System Center Endpoint Protection]  。

1. 切換至 [分類]  索引標籤。選取 [定義更新]  和 [更新]  。

## <a name="approve-definition-updates"></a>核准定義更新

Endpoint Protection 定義更新必須經過核准並下載至 WSUS 伺服器，才能將其提供給要求可用更新清單的用戶端。 用戶端連線至 WSUS 伺服器，以檢查適用的更新，然後要求最新已核准的定義更新。

### <a name="approve-definitions-and-updates-in-wsus"></a>在 WSUS 中核准定義和更新

1. 在 WSUS 管理主控台中，選取 [更新]  。 然後選取 [所有更新]  或所要核准的更新分類。

1. 在更新清單中，以滑鼠右鍵按一下想要為安裝核准的更新，然後選取 [核准]  。

1. 在 [核准更新]  視窗中，選取所要核准更新的電腦群組，然後按一下 [已核准安裝]  。

### <a name="configure-an-automatic-approval-rule"></a>設定自動核准規則

您也可設定定義更新及 Endpoint Protection 更新的自動核准規則。 此動作會將 WSUS 設為自動核准由 WSUS 下載的 Endpoint Protection 定義更新。

1. 在 WSUS 管理主控台中，按一下 [選項]  ，然後按一下 [自動核准]  。

1. 在 [更新規則]  索引標籤上，選取 [新增規則]  。

1. 在 [新增規則]  視窗中，於 [步驟 1:  選取屬性] 下方，選取選項：[當更新位於特定分類中時]  。

    1. 在 [步驟 2:  編輯屬性] 下方，選取 [任何分類]  。

    1. 清除 [定義更新]  之外的所有選項，然後選取 [確定]  。

1. 在 [新增規則]  視窗中，於 [步驟 1:  選取屬性] 下方，選取選項：[當更新位於特定產品中時]  。

    1. 在 [步驟 2:  編輯屬性] 下方，選取 [任何產品]  。

    1. 清除 [System Center Endpoint Protection]  (適用於 Windows 8.1 及更早版本) 和 [Windows Defender]  (適用於 Windows 10 及更新版本) 之外的所有選項。 然後選取 [確定]  。

1. 在 [步驟 3:  指定名稱] 下方，輸入規則的名稱，然後選取 [確定]  。

1. 在 [自動核准]  對話方塊中，選取新建立的規則，然後選取 [執行規則]  。

> [!NOTE]
> 若要在 WSUS 伺服器和用戶端電腦上達到最佳效能，請拒絕舊的定義更新。 若要完成這項工作，您可以設定修訂自動核准及自動拒絕已過期的更新。 如需詳細資訊，請參閱 [Microsoft 支援服務文章 938947](https://support.microsoft.com/kb/938947)。

> [!div class="nextstepaction"]
> [建立及部署反惡意程式碼原則](endpoint-antimalware-policies.md)
