---
title: 內部部署 MDM
titleSuffix: Configuration Manager
description: 瞭解 Configuration Manager 中的內部部署行動裝置管理（MDM）
ms.date: 01/09/2020
ms.prod: configuration-manager
ms.technology: configmgr-mdm
ms.topic: conceptual
ms.assetid: 497c05c7-fe9f-4b88-983b-1c5b3d59308e
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 38d68447093d098f1a8157a2e18e19a6c4f88364
ms.sourcegitcommit: 578ad1e8088f7065b565e8a4f4619f5a26b94001
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81724672"
---
# <a name="on-premises-mdm-in-configuration-manager"></a>Configuration Manager 中的內部部署 MDM

適用於：  Configuration Manager (最新分支)

Configuration Manager 內部部署行動裝置管理（MDM）是一種裝置管理解決方案，其依賴 Windows 的內建管理功能。 這項功能是以開放行動聯盟（OMA）裝置管理（DM）標準為基礎。 它會使用您組織的 Configuration Manager 基礎結構來管理和維護裝置。 您的組織需要 Microsoft Intune 授權才能使用這項功能，但不需要任何雲端連線。 Configuration Manager 會將您裝置的所有資料儲存在您的內部部署網站資料庫中。

內部部署 MDM 與 Microsoft Intune 不同，後者也依賴內建的 OMA-URI DM 功能。 Intune 中的所有管理功能都是透過雲端服務來傳遞。 內部部署 MDM 也不同于傳統上由 Configuration Manager 所提供的用戶端管理解決方案。 它依賴類似的基礎結構，但不會在其所管理的裝置上使用個別安裝的用戶端軟體。  

## <a name="comparison"></a>比較

下列各節列出內部部署 MDM 與傳統用戶端管理的優缺點：  

### <a name="advantages"></a>優點

- **簡化的基礎結構**：需要較少的網站系統角色。

- **更容易維護**：由於管理功能內建于裝置作業系統，因此在網站引進新的管理功能時，不需要新版本的 Configuration Manager 用戶端。

- 內部**部署**：-所有管理和資料都會保留在內部部署環境中。

### <a name="disadvantages"></a>缺點

**較少的用戶端管理功能**：無協調流程、軟體計量、協力廠商整合、工作順序或軟體中心支援。

- **有限裝置支援**：內部部署 MDM 不支援與 Configuration Manager 用戶端數目相同的作業系統版本。 如需詳細資訊，請參閱[針對用戶端和裝置支援的 OS 版本](../../core/plan-design/configs/supported-operating-systems-for-clients-and-devices.md#bkmk_OnpremOS)。

## <a name="next-step"></a>後續步驟

瞭解在內部部署 MDM 中設定 Configuration Manager 基礎結構和規劃裝置註冊時要考慮的事項。

> [!div class="nextstepaction"]
> [規劃內部部署 MDM](../plan-design/plan-on-premises-mdm.md)  
