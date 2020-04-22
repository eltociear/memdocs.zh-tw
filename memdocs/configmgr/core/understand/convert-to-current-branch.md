---
title: 將 LTSB 升級至最新分支
titleSuffix: Configuration Manager
description: 了解如何將長期維護分支 (LTSB) 站台轉換成最新分支站台。
ms.date: 02/8/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: ec5b54cf-62b7-4ed1-9bb3-e8c63b9641c8
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: b9f79eae1eee29fee33a9a841a303aae55686c55
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81707226"
---
# <a name="upgrade-the-long-term-servicing-branch-to-the-current-branch"></a>將長期維護分支升級至最新分支

適用於：  System Center Configuration Manager (長期維護分支)

使用本主題了解如何將執行 Configuration Manager 長期維護分支 (LTSB) 的站台和階層升級 (轉換) 為最新分支。

當目前的軟體保證合約 (或類似的授權權限) 授與您使用最新分支的權限，您就可以將 LTSB 安裝轉換成最新分支。  這是單向轉換，因為不支援將最新分支站台轉換成 LTSB。

如有多個站台，您只需要轉換階層的頂層站台。 轉換頂層站台之後︰
- 子主要站台會自動轉換。
- 您必須從 Configuration Manager 主控台內手動更新次要站台。

## <a name="run-setup-to-convert-the-long-term-servicing-branch"></a>執行安裝程式，將長期服務分支轉換為維護分支
在階層的頂層站台，您可以從合格的基準媒體執行 Configuration Manager 安裝程式，並選取 [站台維護]  。  然後，當您看到授權頁面時，請選取最新分支的選項來完成精靈。

當站台轉換到最新分支時，原先無法使用的功能即可使用。

> [!NOTE]  
> 合格的基準媒體是和您的 LTSB 安裝版本一樣或更新的媒體。

例如，因為 LTSB 是以 1606 版為基礎，所以您無法使用 1511 版基準媒體轉換成最新分支。 而是要從用於安裝 LTSB 站台所用的相同 1606 版基準媒體來執行安裝程式，並選擇最新分支的授權選項。  或者，如果已發行最新分支的新版基準，也可以從該基準媒體執行安裝程式。

如需基準版本清單，請參閱 [Updates for Configuration Manager](../servers/manage/updates.md) (System Center Configuration Manager 的更新) 中的 **Baseline and update versions** (基準和更新版本)。

## <a name="use-the-configuration-manager-console-to-convert-the-long-term-servicing-branch"></a>使用 Configuration Manager 主控台轉換長期維護分支
如果您的站台執行 LTSB，您可以使用 Configuration Manager 主控台中的下列選項轉換成最新分支︰

 1. 在主控台中，前往 [管理]   >  **[站台設定]**  > [站台]  ，然後開啟 [階層設定]  。  

 2. 在 [階層設定]  中，切換至 [授權]  索引標籤。選取 [轉換為最新分支]  選項，然後選擇 [套用]  。  

當站台轉換到最新分支時，原先無法使用的功能即可使用。
