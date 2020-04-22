---
title: 支援中心快速入門
titleSuffix: Configuration Manager
description: 快速擷取 Configuration Manager 用戶端的狀態以供進行疑難排解。
ms.date: 11/27/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 5cb41e2b-4c79-4da9-a432-ff869c0870f8
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: c8c43fe1dbca9155bf9b554a2554c652b1482583
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81707456"
---
# <a name="support-center-quickstart-guide"></a>支援中心快速入門指南

適用於：  Configuration Manager (最新分支)

支援中心具有包括疑難排解和即時記錄檔檢視在內的強大功能。 它只要幾分鐘即可擷取 Configuration Manager 用戶端電腦的狀態。 此功能包括存取遠端用戶端。

建立可擷取用戶端狀態的完整「疑難排解配套」  檔案 (.zip)。 配套檔案不只包含記錄檔。 還包含其他類型的資料，例如登錄設定和用戶端設定。 向使用支援中心檢視器的支援技術人員提供配套。



## <a name="prerequisites"></a>先決條件

- Configuration Manager 用戶端的本機系統管理權限  

- 支援中心安裝程式。 此檔案位在 `cd.latest\SMSSETUP\Tools\SupportCenter\SupportCenterInstaller.msi` 的站台伺服器。 如需詳細資訊，請參閱[支援中心 - 安裝](support-center.md#install)。  



## <a name="step-1-create-a-data-bundle-on-a-local-client"></a>步驟 1：在本機用戶端上建立資料組合

1.  在 Configuration Manager 用戶端安裝支援中心。  

2.  移至 [開始]  功能表，在 **Microsoft System Center** 群組中，選取 [支援中心]  。  

3.  在功能區的 [常用] 索引標籤上選取 [Collect Selected Data] \(收集選取的資料\)  。 根據預設，支援中心只收集最小的資料集：記錄檔、用戶端設定和作業系統。  

4.  將疑難排解配套檔案 (.zip) 儲存在電腦的資料夾中。 根據預設，檔案名稱類似下列範例：`Support_c885cdfed3c7482bba4f9e662978ec07.zip`。  



## <a name="step-2-view-the-data-bundle-using-support-center-viewer"></a>步驟 2：使用支援中心檢視器檢視資料配套檔案

1.  啟動 [支援中心檢視器]  。 此動作會發生在安裝支援中心的任何電腦上。  

2.  選取 [Open bundle] \(開啟配套檔案\)  ，瀏覽至配套檔案，然後選取 [開啟]  。  

3.  在支援中心檢視器處理檔案後，切換到每個可用的索引標籤。檢視預設支援中心預設收集的資料類型：  

    - **設定**  

        - Configuration Manager 用戶端設定  

        - 作業系統  

        - 電腦  

        - 服務  

        - 網路介面卡  

    - **記錄檔**：在清單中選擇一或多個項目，然後選取 [開啟]  。 這個動作會在記錄檔檢視器中開啟選取的記錄檔。 使用此功能查閱錯誤碼，並使用進階篩選以利更快速地分析記錄檔。  



## <a name="collect-more-data"></a>收集更多資料

除了這些基本功能之外，支援中心還可以收集其他各種用戶端狀態資訊。 開啟 [支援中心]  ，然後選取[Collect All Data] \(收集所有資料\)  。 此程序一般會持續幾分鐘，即使在較新的電腦上也一樣。 支援中心會收集下列其他資料：

- **原則**：Configuration Manager 原則設定，包括要求的原則設定和實際原則設定  

- **憑證**：用戶端憑證的公開金鑰資訊。 支援中心不會收集憑證私密金鑰。  

- **用戶端登錄**：從登錄收集用戶端設定資訊。 支援中心只會收集 Configuration Manager 登錄資訊。  

- **用戶端 WMI**：來自 WMI 的用戶端設定資訊。 支援中心不會收集用戶端原則。  

- **疑難排解**：即時針對資料進行疑難排解，協助診斷 Active Directory、管理點、網路功能、原則指派和註冊的常見用戶端問題。  

- **偵錯傾印**：執行用戶端和相關處理序的偵錯傾印。 偵錯傾印可能很大。 只在針對用戶端效能問題進行疑難排解時，才啟用此選項。  

