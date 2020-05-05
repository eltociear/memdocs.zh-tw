---
title: 使用 Exchange 管理裝置
titleSuffix: Configuration Manager
description: 在 Configuration Manager 中使用 Exchange Server 連接器管理行動裝置。
ms.date: 12/31/2019
ms.prod: configuration-manager
ms.technology: configmgr-mdm
ms.topic: conceptual
ms.assetid: aba688d9-fd5b-4c42-8cb4-f7e1b161ef50
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 08d92d5c09331d675dc679a374e1bbf81633748e
ms.sourcegitcommit: 578ad1e8088f7065b565e8a4f4619f5a26b94001
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81724802"
---
# <a name="device-management-with-exchange-and-configuration-manager"></a>使用 Exchange 和 Configuration Manager 的裝置管理

適用於：  Configuration Manager (最新分支)

如果您有透過 ActiveSync 通訊協定連接到 Exchange Server 的行動裝置，您可以使用 Configuration Manager 中的 Exchange Server 連接器來管理這些裝置。 連接器適用于內部部署 Exchange Server 或 Exchange Online。 使用 Configuration Manager 主控台來設定 Exchange 行動裝置管理功能。 例如，遠端裝置抹除和設定可控制多部 Exchange 伺服器。

![具有 Configuration Manager 的 Exchange Server 連接器邏輯圖](media/configmgr-with-exchange.png)  

當您使用此連接器管理行動裝置時，不會安裝 Configuration Manager 用戶端或透過 MDM 註冊裝置。 相較于其他選項，Exchange Server 的管理功能會受到限制。 例如，您無法安裝軟體或使用設定專案來設定這些裝置。 如需詳細資訊，請參閱[選擇適用于 Configuration Manager 的裝置管理解決方案](../../core/plan-design/choose-a-device-management-solution.md)。  

## <a name="policies"></a>原則

當您使用連接器時，Configuration Manager 會在行動裝置上進行設定。 裝置不會使用預設的 Exchange ActiveSync 信箱原則。 定義您想要在下列群組中使用的設定：

- **一般**
- **密碼**
- **電子郵件管理**
- **安全性**
- **應用程式**

例如，在 [**密碼**] 群組中，您可以設定下列設定：

- 行動裝置是否需要密碼
- 最小密碼長度
- 密碼複雜度
- 是否允許密碼復原

只要在群組中至少設定一個設定值，Configuration Manager 就會在行動裝置上管理該群組的所有設定。 如果您未在群組中設定任何設定，Exchange 會繼續管理行動裝置的這些設定。 您在 Exchange 伺服器上設定並指派給使用者的任何 Exchange ActiveSync 信箱原則仍然會套用。

## <a name="access-rules-and-remote-actions"></a>存取規則和遠端動作

您也可以設定 Exchange Server 連接器來管理 Exchange 存取規則。 這些存取規則包括 [允許]、[封鎖] 或 [隔離行動裝置]。 您可以使用 Configuration Manager 主控台從遠端抹除行動裝置，而使用者可以使用應用程式類別目錄，從遠端抹除行動裝置。

當您管理使用者的行動裝置，且 Exchange Server 為內部部署時，該裝置就會自動出現在應用程式類別目錄中。 當您使用 Exchange Online 時，若要讓行動裝置出現在應用程式類別目錄中，請手動設定使用者裝置親和性。 如需詳細資訊，請參閱[連結使用者和裝置與使用者裝置親和性](../../apps/deploy-use/link-users-and-devices-with-user-device-affinity.md)。

> [!TIP]  
> 將行動裝置轉移給另一位使用者時，在新的擁有者于裝置上設定其 Exchange 帳戶之前，請先從 Configuration Manager 主控台刪除行動裝置。

## <a name="prerequisites"></a>先決條件

> [!IMPORTANT]  
> 安裝此連接器之前，請確認 Configuration Manager 支援您的 Exchange 版本。 如需詳細資訊，請參閱[支援的設定-Exchange Server 連接器](../../core/plan-design/configs/supported-operating-systems-for-clients-and-devices.md#bkmk_ExSrvConOS)。  

### <a name="permissions-to-configure-the-connector"></a>設定連接器的許可權

您需要下列安全性許可權，才能在 Configuration Manager 中設定 Exchange Server 連接器：

- 加入、修改及刪除 Exchange Server 連接器：[站台] **** 物件的 [修改] **** 權限。  

- 設定行動裝置設定：[站台] **** 物件的 [修改連接器原則] **** 權限。  

例如，**完整系統管理員**內建角色包含這些必要的許可權。  

### <a name="permissions-to-manage-mobile-devices"></a>管理行動裝置的許可權

您必須具備下列安全性許可權，才能管理行動裝置：  

- 抹除行動裝置：[集合] **** 物件的 [刪除資源] **** 。  

- 取消抹除命令：[集合] **** 物件的 [修改資源] **** 。  

- 允許及封鎖行動裝置：[集合] **** 物件的 [修改資源] **** 。  

例如， **Operations 系統管理員**內建角色包含這些必要的許可權。

如需詳細資訊，請參閱[設定以角色為基礎的系統管理](../../core/servers/deploy/configure/configure-role-based-administration.md)。

## <a name="next-steps"></a>後續步驟

> [!div class="nextstepaction"]
> [安裝和設定 Exchange connector](install-configure-exchange-connector.md)
