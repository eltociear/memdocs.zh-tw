---
title: 在 Microsoft Intune 中依網路位置繫結 Android 裝置 - Azure | Microsoft Docs
description: 在 Microsoft Intune 中為 Android 裝置建立或設定網路位置。 您可以依據裝置的網路位置將裝置標示為不符合規範。 如果裝置離開網路位置，您可以封鎖對公司資源的存取。
keywords: ''
author: Brenduns
ms.author: brenduns
manager: dougeby
ms.date: 11/13/2019
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: ayesham
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 9974177b27d94b7ad058fe9f0fa188a62c3d2be6
ms.sourcegitcommit: 302556d3b03f1a4eb9a5a9ce6138b8119d901575
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/27/2020
ms.locfileid: "83990969"
---
# <a name="use-locations-network-fence-in-intune"></a>使用 Intune 中的位置 (網路範圍)

如果裝置離開某個位置，您可能想要封鎖對公司網路的存取。 Intune 中的**位置**功能提供這項功能。 

您可以建立依據網路位置的合規性原則，也稱為網路隔離。 此原則可確保裝置必須連線至公司網路，以符合規範。 此原則可以與條件式存取原則搭配使用，如此一來，裝置就「只有」  在連線至公司網路時才能存取工作資源。 裝置未連線至公司網路時，裝置會變成不符合規範，並失去對工作資源的存取權。

考慮下列案例：

在您的製造設備中，一些員工使用 Android 裝置。 某位員工將 Android 裝置帶到設備或工廠之外。 若要協助防止未經授權的存取，您可以：

1. 建立一個包含 IPv4 範圍且稱為 **Manufacturing floor** 的位置。
2. 建立需要將這些裝置連線至公司網路的合規性原則，並指派此原則。
3. 如果裝置離開製造工廠，裝置即視為不符合規範，因此沒有公司資源的存取權。

此外，您可以新增[不符合規範時所採取的動作](#configure-the-actions-for-noncompliance)。 當裝置回到內部部署且位於網路位置時，它會重新取得公司資源的存取權。

## <a name="prerequisites"></a>必要條件

若要建立依據位置的合規性原則，請：

- 針對裝置連線的閘道伺服器、DHCP 伺服器及/或 DNS 伺服器，建立網路位置作為 IPV4 網路範圍
- 建立合規性原則，以使用這些位置，並定義裝置不再連線至網路位置時所採取的動作
- 公司入口網站應用程式已更新的 Android 裝置 6.0 和更新版本

## <a name="create-a-location"></a>建立位置

1. 在 [Microsoft 端點管理員系統管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)內，選取 [裝置]   > [合規性政策]   > [位置]   > [建立]  。

2. 輸入下列內容：  

   - 必要。 輸入位置的 [名稱]  ，例如 **Manufacturer floor** 或 **Building 44-secure**。
   - 選擇性。 以 CIDR (無類別網域間路由選擇) 標記法輸入 [IPv4 範圍]  ，例如 `aaa.bbb.ccc.ddd/n`。
   - 選擇性。 輸入 [IPv4 閘道]  位址，例如 `aaa.bbb.ccc.ddd`。
   - 選擇性。 輸入 [IPv4 閘道]  位址，例如 `aaa.bbb.ccc.ddd`。
   - 選擇性。 輸入 [IPv4 DNS 伺服器]  位址的清單。 這項設定使用**子集比對**。 如果裝置上的 IPv4 DNS 伺服器是所定義值的子集，則裝置會被視為在範圍內。 請務必每行輸入一個位址，例如：  
     `aaa.bbb.ccc.ddd`  
     `aaa.bbb.ccc.ddd`
   - 選擇性。 輸入 [DNS 尾碼]  的清單。 這項設定使用**子集比對**。 如果裝置上的 DNS 尾碼是所定義值的子集，則裝置會被視為在範圍內。 請務必在每一行中輸入一個網域名稱，例如：  
     `contoso.com`  
     `contoso.org`

3. [儲存]  變更。

## <a name="create-the-location-compliance-policy"></a>建立位置合規性原則

當您[建立合規性政策](create-compliance-policy.md)時，選取 [Android]  作為 [平台]  。 在 [位置]  中，您可以選擇一或多個新增的網路位置。 這些位置是您要為裝置建立之網路範圍的一部分。

## <a name="configure-the-actions-for-noncompliance"></a>指定不符合規範時所採取的動作

建立合規性原則之後，不符合規範的預設動作會套用至裝置。 您可以新增更多動作。 例如，新增一項動作，在裝置不再符合位置時，傳送電子郵件給使用者。

[新增不符合規範時所採取的動作](actions-for-noncompliance.md)提供一些指引。

## <a name="company-portal-app"></a>公司入口網站應用程式

當裝置連線至您的位置時，裝置在公司入口網站應用程式中會顯示為符合規範。 當裝置未連線至您的其中一個位置時，裝置會顯示為不符合規範。

## <a name="next-steps"></a>後續步驟

[監視裝置合規性原則](compliance-policy-monitor.md)  
[開始使用合規性原則](device-compliance-get-started.md)
