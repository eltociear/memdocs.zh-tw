---
title: 從遠端協助 Intune 所管理的行動裝置
description: 您可以使用四種不同的選項，從遠端協助使用者使用其行動裝置。
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 03/20/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: remote-actions
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 34f88d4e7aefe9a32238bb6d14203de0defd65ef
ms.sourcegitcommit: 302556d3b03f1a4eb9a5a9ce6138b8119d901575
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/27/2020
ms.locfileid: "83988252"
---
# <a name="remotely-assist-mobile-devices-managed-by-microsoft-endpoint-manager"></a>從遠端協助 Microsoft Endpoint Manager 所管理的行動裝置

有四個選項可用於從遠端管理 Microsoft Endpoint Manager 所管理的裝置：

- [Microsoft Teams](https://products.office.com/microsoft-teams/) 是團隊合作的中樞，無論您在何處，都可以聊天、開會及共同作業。
- [快速助手](https://support.microsoft.com/help/4027243/windows-10-solve-pc-problems-with-quick-assist)是 Windows 10 應用程式，可讓兩人透過遠端連線共用裝置。
- [TeamViewer](https://www.teamviewer.com/) 是可另外購買的協力廠商程式。 該程式提供了一組完整的遠端存取及支援功能。 Intune 與 [TeamViewer 整合](teamviewer-support.md)可讓您使用 TeamViewer 進行遠端支援，而連接器則直接在 Intune 中管理。
- [遠端控制](https://docs.microsoft.com/configmgr/core/clients/manage/remote-control/introduction-to-remote-control)隨附在 Microsoft Endpoint Configuration Manager 中。 其用途為從遠端進行系統管理、提供協助，或檢視任何工作群組電腦與已加入網域的電腦。

| 功能、平台、授權 | **Teams** | 快速助手 | TeamViewer (Intune) | 遠端控制 (ConfigMgr) |
|:---:|:---:|:---:|:---:|:---:|
| 遠端檢視及控制 |![核取記號](../enrollment/media/enrollment-method-capab/checkmark.png)|![核取記號](../enrollment/media/enrollment-method-capab/checkmark.png)|![核取記號](../enrollment/media/enrollment-method-capab/checkmark.png)|![核取記號](../enrollment/media/enrollment-method-capab/checkmark.png)|
| 聊天 |![核取記號](../enrollment/media/enrollment-method-capab/checkmark.png)||![核取記號](../enrollment/media/enrollment-method-capab/checkmark.png)||
| 檔案傳輸 |![核取記號](../enrollment/media/enrollment-method-capab/checkmark.png)|![核取記號](../enrollment/media/enrollment-method-capab/checkmark.png)|![核取記號](../enrollment/media/enrollment-method-capab/checkmark.png)|![核取記號](../enrollment/media/enrollment-method-capab/checkmark.png)|
| 提高權限的系統管理員存取權 |||![核取記號](../enrollment/media/enrollment-method-capab/checkmark.png)|![核取記號](../enrollment/media/enrollment-method-capab/checkmark.png)|
| 自動存取 |||![核取記號](../enrollment/media/enrollment-method-capab/checkmark.png)|![核取記號](../enrollment/media/enrollment-method-capab/checkmark.png)|
| 同時遠端控制 |![核取記號](../enrollment/media/enrollment-method-capab/checkmark.png)|![核取記號](../enrollment/media/enrollment-method-capab/checkmark.png)|||
| 多重使用者的支援 |||![核取記號](../enrollment/media/enrollment-method-capab/checkmark.png)|![核取記號](../enrollment/media/enrollment-method-capab/checkmark.png)|
| 遠端動作 ||![核取記號](../enrollment/media/enrollment-method-capab/checkmark.png)|![核取記號](../enrollment/media/enrollment-method-capab/checkmark.png)|![核取記號](../enrollment/media/enrollment-method-capab/checkmark.png)|
| 網際網路支援 |![核取記號](../enrollment/media/enrollment-method-capab/checkmark.png)|![核取記號](../enrollment/media/enrollment-method-capab/checkmark.png)|![核取記號](../enrollment/media/enrollment-method-capab/checkmark.png)||
| 稽核報告 |![核取記號](../enrollment/media/enrollment-method-capab/checkmark.png)||![核取記號](../enrollment/media/enrollment-method-capab/checkmark.png)|![核取記號](../enrollment/media/enrollment-method-capab/checkmark.png)|
| 支援所有平台 (Windows、iOS、Android、macOS) |![核取記號](../enrollment/media/enrollment-method-capab/checkmark.png)||![核取記號](../enrollment/media/enrollment-method-capab/checkmark.png)||
| 與 Windows 10 整合 – 不需要額外的應用程式 ||![核取記號](../enrollment/media/enrollment-method-capab/checkmark.png)|||
| 要求裝置必須由 Configuration Manager 與 Intune 共同管理 ||||![核取記號](../enrollment/media/enrollment-method-capab/checkmark.png)|
| 需要額外的授權\* |![核取記號](../enrollment/media/enrollment-method-capab/checkmark.png)||![核取記號](../enrollment/media/enrollment-method-capab/checkmark.png)|![核取記號](../enrollment/media/enrollment-method-capab/checkmark.png)|

\* Teams 需要 O365 或 M365 授權。 使用 TeamViewer 與 Intune 需要來自 TeamViewer 與 Intune 的授權。 遠端控制是 Configuration Manager 的一個功能，而且需要 Configuration Manager 授權。
