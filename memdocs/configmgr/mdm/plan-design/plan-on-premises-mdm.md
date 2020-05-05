---
title: 規劃內部部署 MDM
titleSuffix: Configuration Manager
description: 規劃內部部署行動裝置管理，以在 Configuration Manager 中管理行動裝置
ms.date: 01/09/2020
ms.prod: configuration-manager
ms.technology: configmgr-mdm
ms.topic: conceptual
ms.assetid: 02979fb8-ea7e-4ec6-b7e0-ecbfda73e52d
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 5690e4fe003939d00dee1185e6f6551813c346e5
ms.sourcegitcommit: 578ad1e8088f7065b565e8a4f4619f5a26b94001
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81724692"
---
# <a name="plan-for-on-premises-mdm-in-configuration-manager"></a>Configuration Manager 中的內部部署 MDM 規劃

適用於：  Configuration Manager (最新分支)

當您打算在 Configuration Manager 中執行內部部署行動裝置管理（MDM）時，有幾個重要的區域需要審查：

- 支援的裝置和作業系統版本
- 必要的站台系統角色
- 安全通訊
- 裝置註冊

> [!IMPORTANT]
> 當網站或任何行動裝置未連線到 Microsoft Intune 時，您的組織仍需要 Intune 授權才能使用這項功能。 如需詳細資訊，請參閱[Microsoft Intune 授權](https://docs.microsoft.com/intune/fundamentals/licenses)。

準備 Configuration Manager 基礎結構來處理內部部署 MDM 之前，請先考慮下列需求。

## <a name="supported-devices"></a><a name="bkmk_devices"></a> 支援的裝置  

Configuration Manager 的最新分支支援對執行 Windows 10 之裝置的內部部署行動裝置管理註冊。 這些裝置類型主要包含膝上型電腦、IoT 和 Surface Hub。 如需詳細資訊和特定版本清單，請參閱[支援的用戶端和裝置作業系統版本](../../core/plan-design/configs/supported-operating-systems-for-clients-and-devices.md#bkmk_OnpremOS)。

## <a name="site-system-roles"></a><a name="bkmk_roles"></a> 站台系統角色

內部部署 MDM 至少需要下列其中一個網站系統角色：

- **註冊 Proxy 點** ，以支援註冊要求。

- **註冊點** ，以支援裝置註冊。

- **裝置管理點** ，用於傳遞原則。 此角色是管理點的變化，但允許行動裝置管理。

- **發佈點** ，用於傳遞內容。

視組織的需求而定，您可以在單一伺服器上，或在不同的伺服器上分別安裝這些角色。

> [!NOTE]
> 您必須將用於內部部署 MDM 的每個角色設定為 HTTPS 端點，以便與受信任的裝置通訊。 如需詳細資訊，請參閱 [必要的信任通訊](#bkmk_trustedComs)。

如需更多一般資訊，請參閱[規劃網站系統伺服器和角色](../../core/plan-design/hierarchy/plan-for-site-system-servers-and-site-system-roles.md)。

## <a name="trusted-communications"></a><a name="bkmk_trustedComs"></a>信任的通訊

內部部署 MDM 會要求您啟用網站系統角色以進行 HTTPS 通訊。 視您的需求而定，您可以使用組織的憑證授權單位單位（CA）來建立伺服器與裝置之間的信任連接。 您也可以使用公開提供的 CA 作為受信任的授權單位。 不論是哪一種方式，您都必須設定下列憑證：

- 在裝載必要網站系統角色的伺服器上，IIS 中的**web 伺服器憑證**。 如果一部伺服器裝載多個網站系統角色，則該伺服器只需要一個憑證。 如果每個角色都在不同的伺服器上，則每一部伺服器都需要個別的憑證。

- 發行 web 伺服器憑證之 CA 的**受信任根憑證**。 在所有需要連線到網站系統角色的裝置上安裝此根憑證。

如需詳細資訊，請參閱[在內部部署 MDM 中設定受信任通訊的憑證](../get-started/set-up-certificates-on-premises-mdm.md)。

## <a name="device-enrollment"></a><a name="bkmk_enrollment"></a>裝置註冊

若要啟用內部部署 MDM 的裝置註冊：

- 授與使用者透過用戶端設定註冊的許可權

- 設定裝置以與裝載所需角色的網站系統伺服器進行受信任的通訊

除了使用者起始的註冊以外，您還可以設定大量註冊套件。 此套件可讓裝置註冊，而不需要使用者介入。 在裝置布建供使用之前或經過其 OOBE 程式之後，將套件傳遞至裝置。

如需詳細資訊，請參閱[設定內部部署 MDM 的裝置註冊](../get-started/set-up-device-enrollment-on-premises-mdm.md)。

## <a name="next-step"></a>後續步驟

> [!div class="nextstepaction"]
> [安裝站台系統角色](../get-started/install-site-system-roles-for-on-premises-mdm.md)
