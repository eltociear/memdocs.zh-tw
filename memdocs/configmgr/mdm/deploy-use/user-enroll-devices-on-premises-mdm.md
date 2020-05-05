---
title: 使用者如何註冊裝置
titleSuffix: Configuration Manager
description: 瞭解使用者如何在 Configuration Manager 中使用內部部署行動裝置管理（MDM）註冊裝置。
ms.date: 01/13/2020
ms.prod: configuration-manager
ms.technology: configmgr-mdm
ms.topic: conceptual
ms.assetid: 59004b34-b64f-4d77-898c-07bf3dc75430
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: f80b77d6a25d7af701ded249118e95201bcb9cc1
ms.sourcegitcommit: 578ad1e8088f7065b565e8a4f4619f5a26b94001
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81724882"
---
# <a name="how-users-enroll-devices-with-on-premises-mdm-in-configuration-manager"></a>使用者如何在 Configuration Manager 中使用內部部署 MDM 註冊裝置

適用於：  Configuration Manager (最新分支)

透過 Configuration Manager 的內部部署行動裝置管理（MDM），使用者可以註冊其裝置。 但具有以下兩個必要條件：

- 您可以使用用戶端設定，將註冊的許可權授與使用者。

- 您會在裝置上安裝所需的受信任根憑證。

如需如何設定註冊的詳細資訊，請參閱[設定內部部署 MDM 的裝置註冊](../get-started/set-up-device-enrollment-on-premises-mdm.md)。

## <a name="enroll-windows-10"></a><a name="bkmk_enrollDesk"></a>註冊 Windows 10

1. 在 Windows 10 電腦上，移至 [設定] ****。

1. 選取 [**帳戶**]，然後選取 [**存取公司或學校**]。

1. 選取 **[連線]**，輸入您的使用者主要名稱（UPN），然後選取 [**繼續**]。 UPN 可能與您的電子郵件地址相同，例如jdoe@contoso.com。

1. 輸入註冊 proxy 點的完整功能變數名稱（FQDN），然後選取 [**繼續**]。

1. 輸入您的密碼，然後選取 [登**入**]。

1. Windows 不需要記住此動作的登入資訊，因此請選取 [**略過**]。

經過一小段時間之後，裝置會向 Configuration Manager 註冊。

## <a name="enroll-windows-10-mobile"></a><a name="bkmk_enrollMob"></a>註冊 Windows 10 行動裝置版

1. 在 Windows 10 行動裝置上，請移至 [設定] ****。

1. 選取 [**帳戶**]，然後選取 [**公司存取**]。

1. 選取 [連接]  。

1. 輸入您的 UPN 和註冊 proxy 點的 FQDN。 然後選取 [連線]****。

1. 在下一個畫面上，輸入您的 UPN 和密碼，然後選取 [登**入**]。

經過一小段時間之後，裝置會向 Configuration Manager 註冊。 選取 [完成]  。

## <a name="verify-enrollment"></a><a name="bkmk_verify"></a>確認註冊

使用 Configuration Manager 主控台確認已成功註冊裝置。 在 Configuration Manager 主控台中，移至 [資產與合規性]**** 工作區，然後選取 [裝置]****。 流覽或搜尋裝置清單中已註冊的裝置。
