---
title: 安裝內部部署 MDM 的角色
titleSuffix: Configuration Manager
description: 在 Configuration Manager 中安裝內部部署行動裝置管理（MDM）所需的網站系統角色。
ms.date: 01/09/2020
ms.prod: configuration-manager
ms.technology: configmgr-mdm
ms.topic: conceptual
ms.assetid: c3cf9f64-c2b9-4ace-9527-2aba6d4eef04
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: f47d78eeafb745732d4917dd7abd80f752f4dd20
ms.sourcegitcommit: 578ad1e8088f7065b565e8a4f4619f5a26b94001
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81724702"
---
# <a name="install-site-system-roles-for-on-premises-mdm-in-configuration-manager"></a>在 Configuration Manager 中安裝內部部署 MDM 的網站系統角色

適用於：  Configuration Manager (最新分支)

Configuration Manager 內部部署行動裝置管理（MDM）需要您 Configuration Manager 網站中的下列網站系統角色：

- 註冊點

- 註冊 Proxy 點

- 發佈點

- 裝置管理點，這是您允許行動裝置使用的管理點

## <a name="requirements-and-limitations"></a>需求與限制

- 內部部署 MDM 會要求您啟用網站系統角色以進行 HTTPS 通訊。 如需詳細資訊，請參閱[在內部部署 MDM 中設定受信任通訊的憑證](set-up-certificates-on-premises-mdm.md)。

- Configuration Manager 的最新分支只支援從裝置到發佈點的*內部*網路連線，以及適用于內部部署 MDM 的裝置管理點。 不過，如果您也管理 macOS 電腦，這些用戶端需要對那些相同角色的*網際網路連線*。 當您設定發佈點和裝置管理點時，請使用 [**允許內部網路和網際網路連線**] 選項。

- 您為內部網路連線設定的發佈點需要為其設定網站界限。 Configuration Manager 僅支援內部部署 MDM 的 IPv4 範圍界限。 如需詳細資訊，請參閱[定義站台界限與界限群組](../../core/servers/deploy/configure/define-site-boundaries-and-boundary-groups.md)。

- 如果您將[資料庫複本](../../core/servers/deploy/configure/database-replicas-for-management-points.md)與裝置管理點搭配使用，新註冊的裝置一開始將無法連接。 發生此連接失敗，因為資料庫複本沒有成功連線所需的新註冊裝置的相關資訊。 複本每五分鐘同步處理一次。 裝置在註冊後的前五分鐘將無法連線，這通常是兩次連線嘗試。 然後，裝置將會成功連線。

## <a name="add-roles"></a>新增角色

如果您要將內部部署 MDM 新增至具有 Configuration Manager 用戶端管理之大部分裝置的網站，您可能已經在網站上安裝其中一些角色。 例如，發佈點是通用角色，而裝置管理點則是管理 macOS 裝置的必要條件。

如需如何將角色新增至網站的詳細資訊，請參閱[新增網站系統角色](../../core/servers/deploy/configure/install-site-system-roles.md)。

## <a name="configure-roles"></a>設定角色

設定新的或現有的角色來管理行動裝置。 請遵循下列步驟，將發佈點和裝置管理點設定為可針對內部部署 MDM 正常運作：

1. 在 Configuration Manager 主控台中，移至 [系統管理]  工作區，並展開 [站台設定]  ，然後選取 [伺服器和站台系統角色]  節點。

1. 選取您想要設定的發佈點或裝置管理點的網站系統伺服器。 在清單中選取伺服器，然後在 [網站系統角色] 詳細資料窗格中選取**網站系統**角色。 在功能區的 [**網站角色**] 索引標籤上，選取 [**屬性**]。

    > [!TIP]
    > 在大型網站中，您可以將此視圖的範圍設為僅顯示具有特定角色的伺服器。 當您選取 [**伺服器和網站系統角色**] 節點時，請在功能區的 [首頁] 標籤上，選取 [**具有角色的伺服器**]。 然後從網站目前可用的角色清單中選取您想要的角色。

    在**網站系統**內容的 [**一般**] 索引標籤上，確認**名稱**是完整功能變數名稱（FQDN）。 關閉 [屬性]。

1. 在 [主控台] 清單中，選取具有內部部署發佈點角色的伺服器。 在 [網站系統角色] 詳細資料窗格中，選取**發佈點**角色。 在功能區的 [**網站角色**] 索引標籤上，選取 [**屬性**]。 在**發佈點**內容的 [**通訊**] 索引標籤上：

    1. 選取 [ **HTTPS**]，然後選取 [**僅允許內部**網路連線]。

        > [!IMPORTANT]
        > 如果您也要使用 Configuration Manager 用戶端來管理 macOS 電腦，請改用 [**允許內部網路和網際網路連線**]。

    1. 啟用 [允許行動**裝置連線到此發佈點]** 選項，然後關閉 [內容]。

1. 開啟**管理點**網站系統角色的 [屬性]。

    1. 在 [**一般**] 索引標籤上，選取 [ **HTTPS**]，然後選取 [**僅允許內部**網路連線]。

        > [!IMPORTANT]
        > 如果您也要使用 Configuration Manager 用戶端來管理 macOS 電腦，請改用 [**允許內部網路和網際網路連線**]。

    1. 啟用 [允許行動**裝置和 Mac 電腦使用此管理點**] 選項，然後關閉內容。

        > [!NOTE]
        > 此選項會有效地將管理點轉換為*裝置*管理點。  

## <a name="next-step"></a>後續步驟

在您新增和設定管理行動裝置的角色之後，請將伺服器設定為受信任的端點。 此信任可讓角色與受管理的裝置進行通訊及註冊。

> [!div class="nextstepaction"]
> [Set up certificates for trusted communications](set-up-certificates-on-premises-mdm.md)
