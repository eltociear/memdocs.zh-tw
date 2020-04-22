---
title: 在軟體中心中共用應用程式
titleSuffix: Configuration Manager
description: 在 Configuration Manager 的軟體中心中共用應用程式的連結。
ms.date: 07/31/2017
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 2629c376-ec43-4f0e-a78b-4223cc9302bf
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: be2e930e3f59bc5a4d7db9e27ce2f875814fd358
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81689236"
---
# <a name="share-an-application-from-software-center"></a>從軟體中心共用應用程式

適用於：  Configuration Manager (最新分支) <!-- 1706 -->

您可以使用 [應用程式詳細資料] 檢視中的 ![共用](media/share15.png) [共用]  按鈕來複製軟體中心中應用程式的超連結。 您只能共用應用程式的超連結。 如果應用程式變得無法使用，超連結會開啟含有應用程式無法使用之訊息的視窗。

1. 選擇 [應用程式]  ，然後選擇應用程式。
2. 按一下 ![共用](media/share15.png) [共用]  按鈕。
3. 在視窗中按一下 [複製]  。
4. 將 URL 貼入到電子郵件以共用應用程式。  

> [!TIP]  
>  若要在 Outlook 電子郵件中建立連結，請按 **CTRL** + **K**，然後貼上 URL。  
>  
> 根據預設，Outlook 會在收件者按一下連結時，顯示軟體中心通訊協定的安全性警訊。 將受信任的通訊協定金鑰新增至登錄，即可防止在您的環境中發生這種狀況。 例如， `HKCU\Software\Policies\Microsoft\Office\16.0\Common\Security\Trusted Protocols\All Applications\softwarecenter:`  
