---
title: 建立使用者與電腦的關聯
titleSuffix: Configuration Manager
description: 設定讓 Configuration Manager 在部署作業系統時，將使用者與目的地電腦建立關聯。
ms.date: 08/17/2018
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 07c3c6d9-f056-4c4d-bc70-ede5ca933807
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: f3a77e06dd2502b9007244ff9a3c9c9922fea592
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81709006"
---
# <a name="associate-users-with-a-destination-computer-in-configuration-manager"></a>在 Configuration Manager 中將使用者與目的地電腦建立關聯

適用於：  Configuration Manager (最新分支)

當您使用 Configuration Manager 來部署作業系統時，可以將使用者與目的地電腦建立關聯。 不論目的地電腦的主要使用者是單一使用者還是多個使用者，此選項都可運作。  

使用者裝置親和性支援部署應用程式時使用者為中心的管理。 當您將使用者與要安裝 OS 的目的地電腦建立關聯時，您可以稍後將應用程式部署至該使用者，應用程式將會自動安裝在目的地電腦上。 隨然您可以在進行 OS 部署時，設定對使用者裝置親和性的支援，但無法利用使用者裝置親和性來部署 OS。  

如需使用者裝置親和性的詳細資訊，請參閱[使用使用者裝置親和性連結使用者和裝置](../../apps/deploy-use/link-users-and-devices-with-user-device-affinity.md)。  

您可以藉由數種方法，將使用者裝置親和性整合到您的 OS 部署中。 您可以將使用者裝置親和性整合至 PXE 部署、可開機媒體部署和預先設置的媒體部署。  


### <a name="create-a-task-sequence-that-includes-the-smstsassignusersmode-variable"></a>建立包含 **SMSTSAssignUsersMode** 變數的工作順序

請使用[設定工作順序變數](../understand/task-sequence-steps.md#BKMK_SetTaskSequenceVariable)步驟，將 **SMSTSAssignUsersMode** 變數新增到工作順序的開頭。 此變數會指定工作順序處理使用者資訊的方式。

如需詳細資訊，請參閱[工作順序變數](../understand/task-sequence-variables.md#SMSTSAssignUsersMode)。


### <a name="create-a-prestart-command-that-gathers-the-user-information"></a>建立收集使用者資訊的啟動前置命令

啟動前置命令可能是一個含有輸入方塊的 VBScript。 它也可能是一個驗證他們所輸入使用者資料的 HTML 應用程式 (HTA)。 

此啟動前置命令必須設定在工作順序執行時所使用的 **SMSTSUDAUsers** 變數。 此變數可以在電腦、集合或工作順序變數上設定。

如需詳細資訊，請參閱[工作順序變數](../understand/task-sequence-variables.md#SMSTSUDAUsers)。


### <a name="configure-how-distribution-points-and-media-associate-the-user-with-the-destination-computer"></a>設定發佈點和媒體將使用者與目的地電腦產生關聯的方式

發佈點或媒體支援將使用者與部署 OS 的目的地電腦建立關聯。 使用下列其中一種方法： 

- [將發佈點設定成接受 PXE 開機要求](prepare-site-system-roles-for-operating-system-deployments.md#BKMK_PXEDistributionPoint)  
- [建立可開機媒體](../deploy-use/create-bootable-media.md)  
- [建立預先設置媒體](../deploy-use/create-prestaged-media.md)  


設定使用者裝置親和性支援並沒有內建方法可驗證使用者身分識別。 當技術人員要佈建電腦並代表使用者輸入資訊時，此行為相當重要。 除了設定工作順序如何處理使用者資訊之外，在發佈點和媒體上設定這些選項將能夠讓您限制從 PXE 開機或從特定類型媒體啟動的部署。
