---
title: Intune 端點安全性端點偵測和回應設定 | Microsoft Docs
description: Microsoft Intune 中的端點安全性端點偵測和回應原則設定
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 05/22/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.reviewer: mattsha
ms.openlocfilehash: dd53ec47435ba9dc416d2b152719b393d1647f90
ms.sourcegitcommit: 2f9999994203194a8c47d8daa6406c987a002e02
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/24/2020
ms.locfileid: "83823991"
---
# <a name="endpoint-detection-and-response-policy-settings-for-endpoint-security-in-intune"></a>Intune 中端點安全性的端點偵測和回應原則設定

在 Intune 端點安全性節點中，檢視可在設定檔設定[端點偵測和回應原則](../protect/endpoint-security-edr-policy.md)的設定。

支援的平台和設定檔：

- **Windows 10 及以上版本**：原則若是部署至使用 Intune 管理的裝置，請使用此平台。
  - 設定檔：**端點偵測及回應 (MDM)**

- **Windows 10 與 Windows Server**：原則若是部署至由 Configuration Manager 管理的裝置，請使用此平台。
  - 設定檔：**端點偵測及回應 (ConfigMgr) (預覽)**
  
  *此平台和設定檔現為公開預覽*。

## <a name="endpoint-detection-and-response-mdm"></a>端點偵測及回應 (MDM)

**端點偵測與回應**：

- **Microsoft Defender ATP 用戶端設定套件類型**

  上傳用來將 Microsoft Defender ATP 用戶端上線的已簽署設定套件。

  - [未設定] (預設)
  - **上線 Blob**  
  - **下線 Blob**  

  設定為「上線 Blob」時，您可以設定下列設定：

  - **進階威脅防護上線 Blob**  
    按一下 **[選取上線檔案]** 即可開啟選取上線檔案窗格，並可在這裡指定 `.onboarding` 檔案。

  設定為「離線 Blob」時，您可以進行下列設定：
  
  - **進階威脅防護離線 Blob**  
     按一下 **[選取離線檔案]** 即可開啟選取離線檔案窗格，您可在這裡指定 `.offboarding` 檔案。

- **所有檔案的範例共用**  

  傳回或設定 Microsoft Defender 進階威脅防護範例共用設定參數。  
  - [未設定]   (預設)
  - **是**

- **加快遙測回報頻率**

  - [未設定]   (預設)
  - [是] - 增加 Microsoft Defender 進階威脅防護遙測回報頻率。

## <a name="endpoint-detection-and-response-configmgr-preview"></a>端點偵測和回應 (ConfigMgr) (預覽)

**端點偵測和回應**：

- **所有檔案的範例共用**  

  傳回或設定 Microsoft Defender 進階威脅防護範例共用設定參數。  
  - [未設定]   (預設)
  - **是**

- **加快遙測回報頻率**

  - [未設定]   (預設)
  - [是] - 增加 Microsoft Defender 進階威脅防護遙測回報頻率。

## <a name="next-steps"></a>後續步驟

[EDR 的端點安全性原則](../protect/endpoint-security-edr-policy.md)
