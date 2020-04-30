---
title: BitLocker 自助入口網站
titleSuffix: Configuration Manager
description: 如何使用 Configuration Manager 中的使用者自助入口網站來進行 BitLocker 修復
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: 88e0ad46-7f0c-4f5c-9b48-54773c23768d
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: fda719aed4d70cd9783d158e17d546b698497997
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81699686"
---
# <a name="bitlocker-self-service-portal"></a>BitLocker 自助入口網站

適用於：  Configuration Manager (最新分支)

<!--3601034-->

在[安裝 BitLocker 自助入口網站](setup-websites.md)後，如果 BitLocker 鎖定使用者的裝置，使用者可以獨立存取其電腦。 自助入口網站不需要技術支援人員的協助。

[![預設 BitLocker 自助入口網站的螢幕擷取畫面](media/bitlocker-self-service-portal.png)](media/bitlocker-self-service-portal.png#lightbox)

> [!IMPORTANT]
> 若要從自助入口網站取得修復金鑰，使用者至少必須已成功登入電腦一次。 此登入必須是在裝置的本機，而不是在遠端工作階段中登入。 否則的話，使用者就必須連絡服務台來取得金鑰修復。 服務台系統管理員可以使用[管理和監視網站](helpdesk-portal.md)來要求修復金鑰。

在下列情況下，BitLocker 會鎖定裝置：

- 使用者忘記其 BitLocker 密碼或 PIN

- 裝置的 OS 檔案、BIOS 或信賴平台模組 (TPM) 有所變更

若要從自助入口網站要求 BitLocker 修復金鑰：

1. 當 BitLocker 鎖定裝置時，其會在啟動期間顯示 BitLocker 修復畫面。 請記下 32 位數的 BitLocker 修復金鑰識別碼。

1. 在另一部電腦上，於網頁瀏覽器中移至自助入口網站，例如 `https://webserver.contoso.com/SelfService`。

1. 閱讀並接受通知。

1. 在 [修復金鑰識別碼]  欄位中，輸入 BitLocker 修復金鑰識別碼的前八個數字。 如果其符合多個金鑰，則請將 32 個數字全都輸入。

1. 針對此要求的 [原因]  ，選擇下列其中一個選項：

    - BIOS/TPM 已變更
    - OS 檔案已修改
    - 遺失 PIN/複雜密碼

1. 選取 [取得金鑰]  。 自助入口網站會顯示 48 位數的 **BitLocker 修復金鑰**。

1. 請將此 48 位數代碼輸入您電腦上的 BitLocker 修復畫面。

> [!NOTE]
> BitLocker 自助入口網站可能會在一段時間沒有活動後逾時。 例如，在五分鐘後，您可能會看到倒數計時 60 秒的逾時警告。
>
> ![BitLocker 自助入口網站逾時警告](media/bitlocker-self-service-portal-timeout-warning.png)
>
> 如果您沒有回應倒數計時，工作階段將會過期。
>
> ![BitLocker 自助入口網站工作階段已過期頁面](media/bitlocker-self-service-portal-session-expired.png)
