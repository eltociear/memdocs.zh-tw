---
title: 如何重設帳戶
titleSuffix: Configuration Manager
description: 了解如何重設電腦分析帳戶。
ms.date: 08/16/2019
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: conceptual
ms.assetid: 884d4864-950b-4139-b778-d5368e1f6ef2
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.reviewer: acabello
ms.openlocfilehash: 29f108254e3201925917a0546dd96d36a19763b6
ms.sourcegitcommit: fddbb6c20cf7e19944944d4f81788adf249c963f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/12/2020
ms.locfileid: "83268873"
---
# <a name="how-to-reset-your-account"></a>如何重設帳戶

<!-- 3733897 -->

如果您在環境中設定電腦分析，但想要從頭開始上線和註冊，請使用此程序來重設帳戶。

## <a name="prerequisites"></a>必要條件

只有**全域管理員**可在 Azure 入口網站中重設帳戶。

## <a name="behaviors"></a>行為

- 此程序不會變更任何現有的 Azure AD 使用者、應用程式或權限

- 如果您選擇新增新的工作區，則不保留下列所有使用者對資產的輸入內容：
    - 重要性
    - Owner
    - 升級決策
    - 補救附註

## <a name="process"></a>程序

1. 以具有[全域管理員](https://aka.ms/desktopanalytics)角色的使用者身分，在 Microsoft 365 裝置管理中開啟**電腦分析入口網站**。

1. 在 [全域設定]  功能表中，選取 [已連線的服務]  。 在 [註冊裝置] 區段中，選取 [重設]  選項。

1. 如果決定繼續，即會重設帳戶。 您必須再次設定電腦分析。

## <a name="next-steps"></a>後續步驟

重設之後，請重新整理頁面並重新執行上線程序。 如需詳細資訊，請參閱[如何設定電腦分析](set-up.md)。

如在執行程序期間遇到任何問題，請連絡 Microsoft 支援服務尋求進一步協助。
