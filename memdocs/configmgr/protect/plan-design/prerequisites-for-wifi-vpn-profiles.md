---
title: Wi-Fi 和 VPN 設定檔必要條件
titleSuffix: Configuration Manager
description: 了解在 Configuration Manager 中管理 Wi-Fi 設定檔和 VPN 設定檔的先決條件
ms.date: 01/14/2020
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: d2dacb2d-ab3b-42a2-8dc8-94da31f993c2
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 9e7a557bab6b41be6e6335e3aa2744e8627d285b
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81706066"
---
# <a name="prerequisites-for-wi-fi-and-vpn-profiles-in-configuration-manager"></a>Configuration Manager 的 Wi-Fi 和 VPN 設定檔先決條件

適用於：  Configuration Manager (最新分支)

Configuration Manager 中的 Wi-Fi 和 VPN 設定檔僅具有產品內的相依性。

您需有下列安全性權限才能管理公司資源存取設定，例如憑證設定檔、Wi-Fi 設定檔和 VPN 設定檔：  

- 若要檢視和管理 Wi-Fi 及設定檔的警示和報告：[警示]  物件的**建立**、**刪除**、**修改**、**修改報告**、**讀取**及**執行報告**。  

- 若要建立和管理憑證設定檔：[憑證設定檔]  物件的**撰寫原則**、**修改報告**、**讀取**及**執行報告**。  

- 若要管理 Wi-Fi、憑證和 VPN 設定檔部署：[集合]  物件的**部署設定原則**、**修改用戶端狀態警示**、**讀取**及**讀取資源**。  

- 若要管理所有設定原則：[設定原則]  物件的**建立**、**刪除**、**修改**、**讀取**及**設定安全性範圍**。  

- 若要執行與 Wi-Fi 及 VPN 設定檔相關的查詢：[查詢]  物件的**讀取**權限。  

- 若要檢視 Configuration Manager 主控台中的 Wi-Fi 和 VPN 設定檔資訊：[網站]  物件的 [讀取]  權限。  

- 若要檢視 Wi-Fi 及VPN 設定檔的狀態訊息：[狀態訊息]  物件的**讀取**權限。  

- 若要建立和修改信任的 CA 憑證設定檔：[受信任 CA 憑證設定檔]  物件的**撰寫原則**、**修改報告**、**讀取**及**執行報告**。  

- 若要建立和管理 VPN 設定檔：[VPN 設定檔]  物件的**撰寫原則**、**修改報告**、**讀取**及**執行報告**。  

- 若要建立和管理 Wi-Fi 設定檔：[Wi-Fi 設定檔]  物件的**撰寫原則**、**修改報告**、**讀取**及**執行報告**。  

**公司資源存取管理員**內建安全性角色包含在 Configuration Manager 中管理 Wi-Fi 設定檔所需的上列權限。 如需詳細資訊，請參閱[設定安全性](../../core/plan-design/security/configure-security.md)。
