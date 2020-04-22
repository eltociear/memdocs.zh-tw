---
title: 使用 Microsoft Intune 重設 Windows 10 裝置 - Azure | Microsoft Docs
description: 使用 [全新開始] 在 Windows 10 電腦上使用 Microsoft Intune 移除或解除安裝應用程式。
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 02/27/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: remote-actions
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 5aa5cfa3-c483-4099-b40f-578ff8dca425
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: f6d409f3ba1dc91815ce3dc67a2d65e5703c7268
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "80322556"
---
# <a name="use-fresh-start-to-reset-windows-10-devices-with-intune"></a>透過 Intune 使用「重新開始」重設 Windows 10 裝置


[!INCLUDE [azure_portal](../includes/azure_portal.md)]

[全新開始]  裝置動作會移除安裝在執行 Windows 10 1703 版或更新版本之電腦上的任何應用程式。 [全新開始] 有利於移除一般新電腦會有的預先安裝 (OEM) 應用程式。 

1. 登入 [Microsoft 端點管理員系統管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)，然後選取 [裝置]   > [所有裝置]  。
2. 從您管理的裝置清單中，選擇 Windows 10 電腦裝置。
3. 按一下 [全新開始]  。 
4. 選取 [保留此裝置上的使用者資料]  到：
   * 維持裝置 Azure AD 加入網域的狀態
   * 當啟用 Azure Active Directory 的使用者登入裝置時，裝置會再次向行動裝置管理註冊。
   * 保留裝置使用者的主資料夾內容，並移除應用程式與設定。

  > [!IMPORTANT]
 > 如果您未保留使用者資料，則系統會將裝置還原為預設的 OOBE (全新體驗) 完成狀態，並保留內建的系統管理員帳戶。
 > BYOD 裝置將會從 Azure AD 與行動裝置管理取消註冊。
 > 當啟用 Azure Active Directory 的使用者登入裝置時，Azure AD 聯結裝置會再次向行動裝置管理註冊。
 
5. 按一下 [確定]  。   
6. 若要查看此動作的狀態，請返回 [裝置]  並按一下 [裝置動作]  。  
7. 裝置將會還原為初始登入畫面。
