---
title: UNIX/Linux 用戶端元件服務和命令
titleSuffix: Configuration Manager
description: 了解 Configuration Manager 中 Linux 和 UNIX 用戶端上的元件服務和命令。
ms.date: 03/27/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: e5a8c79f-5791-49c5-8055-086d742e5559
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: de564595ce51a336b5f11d4050928fa812269601
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81693886"
---
# <a name="linux-and-unix-clients-component-services-and-commands-for-configuration-manager"></a>Configuration Manager 的 Linux 和 UNIX 用戶端元件服務和命令

適用於：  Configuration Manager (最新分支)

> [!Important]  
> 從 1902 版開始，Configuration Manager 不支援 Linux 或 UNIX 用戶端。 
> 
> 請考慮以 Microsoft Azure 管理來管理 Linux 伺服器。 Azure 解決方案具有廣泛的 Linux 支援，在大部分情況下都超越 Configuration Manager 的功能性，包括 Linux 的完整修補程式管理。


 下表列出針對 Linux 和 UNIX 之 Configuration Manager 用戶端的用戶端元件服務。  

|檔案名稱|更多資訊|  
|---------------|----------------------|  
|ccmexec.bin|此服務類似 Windows 型用戶端上的 ccmexc 服務。 它負責所有與 Configuration Manager 站台系統角色的通訊，也與 omiserver.bin 服務通訊以從本機電腦收集硬體清查。<br /><br /> 如需支援之命令列引數的清單，請執行 `ccmexec -h`|  
|omiserver.bin|這項服務為 CIM 伺服器。 CIM 伺服器提供稱為提供者之隨插即用軟體模組的架構。 提供者與 Linux 及 UNIX 電腦資源互動，並收集硬體清查資料。 例如， **處理序提供者** Linux 的電腦會收集與 Linux 作業系統處理程序相關聯的資料。|  

 下列的資料表清單命令可讓您啟動、 停止或重新啟動的用戶端服務 (ccmexec.bin 和 omiserver.bin) 上的 Linux 或 UNIX 每個版本。 當您啟動或停止 ccmexec 服務時，omiserver 服務也會啟動或停止。  

|作業系統|命令|  
|----------------------|--------------|  
|通用代理程式<br /><br /> RHEL 4 及 SLES 9|啟動：`/etc/init d/ccmexecd start`<br /><br /> 停止：`/etc/init d/ccmexecd stop`<br /><br /> 重新啟動：`/etc/init d/ccmexecd restart`|  
|Solaris 9|啟動：`/etc/init d/ccmexecd start`<br /><br /> 停止：`/etc/init d/ccmexecd stop`<br /><br /> 重新啟動：`/etc/init d/ccmexecd restart`|  
|Solaris 10|啟動：<br /><br /> `svcadm enable -s svc:/application/management/omiserver`<br /><br /> `svcadm enable -s svc:/application/management/ccmexecd`<br /><br /> 停止：<br /><br /> `svcadm disable -s svc:/application/management/ccmexecd`<br /><br /> `svcadm disable -s svc:/application/management/omiserver`|  
|Solaris 11|啟動：<br /><br /> `svcadm enable -s svc:/application/management/omiserver`<br /><br /> `svcadm enable -s svc:/application/management/ccmexecd`<br /><br /> 停止：<br /><br /> `svcadm disable -s svc:/application/management/ccmexecd`<br /><br /> `svcadm disable -s svc:/application/management/omiserver`|  
|AIX|啟動：<br /><br /> `startsrc -s omiserver`<br /><br /> `startsrc -s ccmexec`<br /><br /> 停止：<br /><br /> `stopsrc -s ccmexec`<br /><br /> `stopsrc -s omiserver`|  
|HP-UX|啟動：`/sbin/init.d/ccmexecd start`<br /><br /> 停止：`/sbin/init.d/ccmexecd stop`<br /><br /> 重新啟動：`/sbin/init.d/ccmexecd restart`|  
