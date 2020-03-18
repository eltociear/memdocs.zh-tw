---
title: 將角色指派給 Intune 使用者
description: 了解如何將內建或自訂角色指派給 Microsoft Intune 中的使用者。
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 03/26/2019
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: pjain
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure; get-started
ms.collection: M365-identity-device-management
ms.openlocfilehash: e4ea84b0b378030a02c73da20b4a59d0b65ca288
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/13/2020
ms.locfileid: "79363144"
---
# <a name="assign-a-role-to-an-intune-user"></a>將角色指派給 Intune 使用者

您可以將[內建](role-based-access-control.md#built-in-roles)或[自訂](create-custom-role.md)角色指派給 Intune 使用者。

若要建立、編輯或指派角色，您的帳戶必須具備下列其中一項 Azure AD 權限︰
- **全域管理員**
- **Intune 服務管理員**

1. 在 [Microsoft 端點管理員系統管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)中，選擇 [租用戶系統管理]   > [角色]   > [所有角色]  。

2. 在 [Intune 角色 - 所有角色]  刀鋒視窗中，選擇您要指派的內建角色 > [指派]   > [指派]  。

5. 在 [基本]  頁面上，輸入 [指派名稱]  及選擇性的 [指派描述]  ，然後選擇 [下一步]  。

6. 在 [系統管理群組]  頁面上，選取包含您欲授與權限使用者的群組。 選擇 [下一步] 

7. 在 [範圍 (群組)]  頁面上，選擇以上成員允許進行管理，包含使用者/裝置的群組。 選擇 [下一步]  。

8. 在 [範圍 (標籤)]  頁面上，選擇將套用此角色指派的標籤。 選擇 [下一步]  。

9. 在 [檢閱 + 建立]  頁面上，當您完成操作時，請選擇 [建立]  。 新指派會隨即顯示在指派清單中。

## <a name="next-steps"></a>後續步驟
- [深入了解 Intune 中的角色型存取控制](role-based-access-control.md)
- [建立自訂角色](create-custom-role.md)


