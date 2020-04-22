---
title: 支援的站台系統伺服器
titleSuffix: Configuration Manager
description: 了解您可用來裝載 Configuration Manager 站台或站台系統角色的 Windows 版本。
ms.date: 02/19/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 17905b4c-3895-4ad4-a69c-5e0d0fc5a8c3
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: cc58ae7f7b5629319d239f9c48b5c6572fb28116
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81691376"
---
# <a name="supported-operating-systems-for-configuration-manager-site-system-servers"></a>Configuration Manager 站台系統伺服器支援的作業系統

適用於：  Configuration Manager (最新分支)

本文詳述您可用來裝載 Configuration Manager 站台或站台系統角色的 Windows 版本。

使用本文的資訊時，請一併參閱下列文章的資訊︰

- [Configuration Manager 的建議硬體](recommended-hardware.md)
- [Configuration Manager 的站台和站台系統必要條件](site-and-site-system-prerequisites.md)
- [Configuration Manager 的大小和縮放比例](size-and-scale-numbers.md)

## <a name="windows-server-2019"></a><a name="bkmk_2019"></a> Windows Server 2019

*適用於 Windows Server 2019：Standard and Datacenter* 

從 1810 版開始，為下列角色支援此作業系統版本：

#### <a name="site-servers"></a>站台伺服器

- 管理中心網站  
- 主要網站  
- 次要網站  

#### <a name="site-system-servers"></a>站台系統伺服器

- 應用程式類別目錄 Web 服務點  
- 應用程式類別目錄網站點  
- Asset Intelligence 同步處理點  
- 憑證登錄點  
- 雲端管理閘道連接點  
- 資料倉儲服務點  
- 發佈點 <sup>[Note 1](#bkmk_note1)</sup>  
- Endpoint Protection 點  
- 註冊點  
- 註冊 Proxy 點  
- 後援狀態點  
- 管理點
- Reporting Services 點  
- 服務連接點  
- 站台資料庫伺服器名稱 <sup>[節點 2](#bkmk_note2)</sup>  
- SMS_Provider  
- 軟體更新點  
- 狀態移轉點

## <a name="windows-server-2016"></a><a name="bkmk_2016"></a> Windows Server 2016

*適用於 Windows Server 2016：Standard and Datacenter*

為下列角色支援此作業系統：

#### <a name="site-servers"></a>站台伺服器

- 管理中心網站  
- 主要網站  
- 次要網站  

#### <a name="site-system-servers"></a>站台系統伺服器

- 應用程式類別目錄 Web 服務點  
- 應用程式類別目錄網站點  
- Asset Intelligence 同步處理點  
- 憑證登錄點  
- 雲端管理閘道連接點  
- 資料倉儲服務點  
- 發佈點 <sup>[Note 1](#bkmk_note1)</sup>  
- Endpoint Protection 點  
- 註冊點  
- 註冊 Proxy 點  
- 後援狀態點  
- 管理點
- Reporting Services 點  
- 服務連接點  
- 站台資料庫伺服器名稱 <sup>[節點 2](#bkmk_note2)</sup>  
- SMS_Provider  
- 軟體更新點  
- 狀態移轉點

## <a name="windows-storage-server-2016"></a><a name="bkmk_stor2016"></a> Windows Storage Server 2016

#### <a name="site-system-server"></a>網站系統伺服器

- 發佈點 <sup>[Note 1](#bkmk_note1)</sup>  

## <a name="windows-server-2012-r2"></a><a name="bkmk_2012r2"></a> Windows Server 2012 R2

*適用於 Windows Server 2012 R2：Standard and Datacenter*

#### <a name="site-servers"></a>站台伺服器

- 管理中心網站  
- 主要網站  
- 次要網站  

#### <a name="site-system-servers"></a>站台系統伺服器

- 應用程式類別目錄 Web 服務點  
- 應用程式類別目錄網站點  
- Asset Intelligence 同步處理點  
- 憑證登錄點  
- 雲端管理閘道連接點  
- 資料倉儲服務點  
- 發佈點 <sup>[Note 1](#bkmk_note1)</sup>  
- Endpoint Protection 點  
- 註冊點  
- 註冊 Proxy 點  
- 後援狀態點  
- 管理點
- Reporting Services 點  
- 服務連接點  
- 站台資料庫伺服器名稱 <sup>[節點 2](#bkmk_note2)</sup>  
- SMS_Provider  
- 軟體更新點  
- 狀態移轉點  

## <a name="windows-server-2012"></a><a name="bkmk_2012"></a> Windows Server 2012  

*適用於 Windows Server 2012：Standard and Datacenter*

#### <a name="site-servers"></a>站台伺服器

- 管理中心網站  
- 主要網站  
- 次要網站  

#### <a name="site-system-servers"></a>站台系統伺服器

- 應用程式類別目錄 Web 服務點  
- 應用程式類別目錄網站點  
- Asset Intelligence 同步處理點  
- 憑證登錄點  
- 雲端管理閘道連接點  
- 資料倉儲服務點  
- 發佈點 <sup>[Note 1](#bkmk_note1)</sup>  
- Endpoint Protection 點  
- 註冊點  
- 註冊 Proxy 點  
- 後援狀態點  
- 管理點
- Reporting Services 點  
- 服務連接點  
- 站台資料庫伺服器名稱 <sup>[節點 2](#bkmk_note2)</sup>  
- SMS_Provider  
- 軟體更新點  
- 狀態移轉點  

## <a name="client-os-versions"></a><a name="bkmk_client"></a> 用戶端作業系統版本

支援將下列用戶端作業系統版本，用作為**發佈點** <sup>[附註 1](#bkmk_note1)</sup>：  

- Windows 10 (x86, x64)：Pro 和 Enterprise

    如需所支援組建版本的詳細資訊，請參閱[對於 Windows 10 的支援](support-for-windows-10.md)。

- Windows 8.1 (x86, x64)：Professional 和 Enterprise

這項支援有如下限制：  

- 此 OS 上的發佈點不支援具有預設 Windows 部署服務的 PXE 或多點傳送。 從 1806 版開始，您可以透過 [啟用沒有 Windows 部署服務的 PXE 回應程式]  選項，讓此 OS 上的發佈點具備 PXE 功能。 如需詳細資訊，請參閱[安裝及設定發佈點](../../servers/deploy/configure/install-and-configure-distribution-points.md#bkmk_config-pxe)。  

## <a name="server-core-installations"></a><a name="bkmk_core"></a> 伺服器核心安裝

支援下列伺服器作業系統版本的伺服器核心安裝，用作為**發佈點**：

- Windows Server 2019 (自 Configuration Manager 1810 版開始)  
- Windows Server 1809 版 (自 Configuration Manager 1810 版開始)  
- Windows Server 1803 版 (自 Configuration Manager 1802 版開始)  
- Windows Server 1709 版 (自 Configuration Manager 1710 版開始)  
- Windows Server 2016  
- Windows Server 2012 R2  
- Windows Server 2012  

這項支援有如下限制：  

- 此 OS 上的發佈點不支援具有預設 Windows 部署服務的 PXE 或多點傳送。 從 1806 版開始，您可以透過 [啟用沒有 Windows 部署服務的 PXE 回應程式]  選項，讓此 OS 上的發佈點具備 PXE 功能。 如需詳細資訊，請參閱[安裝及設定發佈點](../../servers/deploy/configure/install-and-configure-distribution-points.md#bkmk_config-pxe)。  

## <a name="general-notes"></a>一般注意事項

### <a name="note-1-distribution-points"></a><a name="bkmk_note1"></a> 附註 1：發佈點

發佈點支援數個不同的設定，各有不同需求。 在某些情況下，這些設定不僅支援安裝在伺服器上，也支援安裝在用戶端作業系統上。 如需詳細資訊，請參閱[管理內容與內容基礎結構](../../servers/deploy/configure/manage-content-and-content-infrastructure.md)。  

### <a name="note-2-site-database-servers"></a><a name="bkmk_note2"></a> 附註 2：站台資料庫伺服器

唯讀網域控制站 (RODC) 上不支援站台資料庫伺服器。 如需詳細資訊，請參閱 Microsoft 支援服務文章：[您在網域控制站安裝 SQL Server 時，可能會遇到問題](https://support.microsoft.com/help/2032911)。 

此外，任何網域控制站都不支援次要站台伺服器。  
