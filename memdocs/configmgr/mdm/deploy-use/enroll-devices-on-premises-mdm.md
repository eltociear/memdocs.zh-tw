---
title: 註冊內部部署 MDM 的裝置
titleSuffix: Configuration Manager
description: 深入瞭解在 Configuration Manager 中為內部部署行動裝置管理（MDM）註冊裝置的方法。
ms.date: 01/13/2020
ms.prod: configuration-manager
ms.technology: configmgr-mdm
ms.topic: conceptual
ms.assetid: b58472e3-31a5-4305-8eb6-2522befebe02
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 1ca7f792bb6b419dd1d20d495bdb53bc7c2be506
ms.sourcegitcommit: 578ad1e8088f7065b565e8a4f4619f5a26b94001
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81724602"
---
# <a name="enroll-devices-for-on-premises-mdm-in-configuration-manager"></a>在 Configuration Manager 中註冊內部部署 MDM 的裝置

適用於：  Configuration Manager (最新分支)

若要使用 Configuration Manager 的內部部署行動裝置管理（MDM）來管理裝置，您必須先註冊它們。 然後 Configuration Manager 可以與裝置進行通訊，以進行管理工作。 Configuration Manager 提供兩種註冊裝置的方法：

- **使用者註冊**：使用者會在其裝置上啟動註冊程式。 使用者註冊若要成功，請在裝置上安裝受信任的根憑證，並在用戶端設定中布建使用者以進行註冊。 若要註冊裝置，使用者只需要輸入其認證。

    如需詳細資訊，請參閱[使用者註冊裝置的方式](user-enroll-devices-on-premises-mdm.md)。

- **大量註冊**：裝置的使用者不會開始註冊。 您會在 Configuration Manager 中建立大量註冊套件。 當您在裝置上開啟它時，套件會提供註冊裝置所需的資訊。

    如需詳細資訊，請參閱[如何大量註冊裝置](bulk-enroll-devices-on-premises-mdm.md)。

如需 Configuration Manager 支援在內部部署 MDM 中註冊裝置之作業系統版本的詳細資訊，請參閱[支援](../../core/plan-design/configs/supported-operating-systems-for-clients-and-devices.md#bkmk_OnpremOS)的設定。
