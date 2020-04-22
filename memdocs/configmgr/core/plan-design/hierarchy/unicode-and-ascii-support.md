---
title: Unicode 與 ASCII 支援
titleSuffix: Configuration Manager
description: 了解 Configuration Manager 物件中的 Unicode 和 ASCII 字元支援。
ms.date: 08/21/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 2bdec799-905f-48bc-aed5-2d92134739e8
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 7bd3dad5f0ef24074ac8c8e6d2edf01d5641b541
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81699896"
---
# <a name="unicode-and-ascii-support-in-configuration-manager"></a>Configuration Manager 的 Unicode 和 ASCII 支援

適用於：  Configuration Manager (最新分支)

Configuration Manager 會使用 Unicode 字元來建立大部分的物件。 不過，有幾個物件僅支援 ASCII 字元，或者有其他限制。  

## <a name="objects-that-use-ascii-characters"></a><a name="BKMK_ASCIIchar"></a> 使用 ASCII 字元的物件

在建立下列物件時，Configuration Manager 只支援 ASCII 字元集：  

- 站台碼  

- 所有站台系統伺服器電腦的名稱  

- 下列 Configuration Manager 帳戶：  

    > [!NOTE]  
    > 這些帳戶支援 ASCII 字元，並在以俄文執行的站台上支援 RUS 字元。  

    - 用戶端推入安裝帳戶  

    - 管理點資料庫連線帳戶  

    - 網路存取帳戶  

    - 套件存取帳戶  

    - 標準傳送者帳戶  

    - 站台系統安裝帳戶  

    - 軟體更新點連線帳戶  

    - 軟體更新點 Proxy 伺服器帳戶  

    > [!NOTE]  
    > 您所指定之以角色為基礎的系統管理帳戶支援 Unicode。  
    >
    > Reporting Services 點帳戶支援 Unicode，但不支援 RUS 字元。  

- 站台伺服器及站台系統的完整網域名稱 (FQDN)  

- Configuration Manager 的安裝路徑  

- SQL Server 執行個體名稱  

- 下列站台系統角色的路徑：  

    - 註冊點  

    - 註冊 Proxy 點  

    - Reporting Services 點  

    - 狀態移轉點  

- 下列資料夾的路徑：  

    - 用於儲存用戶端狀態移轉資料的資料夾  

    - 包含 Configuration Manager 報告的資料夾  

    - 用於儲存 Configuration Manager 備份的資料夾  

    - 用於儲存站台安裝程式安裝來源檔案的資料夾  

    - 用於儲存安裝程式必須使用之下載內容的資料夾  

- 下列物件的路徑：  

    - IIS 網站  

    - 虛擬應用程式的安裝路徑  

    - 虛擬應用程式名稱  

- 開機媒體 ISO 檔案名稱  


## <a name="additional-limitations"></a><a name="BKMK_OtherCharLimitations"></a> 其他限制

以下是可支援字元集和語言版本的其他限制：  

- Configuration Manager 不支援變更站台伺服器電腦的地區設定。  

- 企業憑證授權單位 (CA) 不支援使用雙位元組字元集 (DBCS) 的用戶端電腦名稱。 可使用的用戶端電腦名稱受限於 IA5 字元集的 PKI 限制。 Configuration Manager 不支援使用 DBCS 的 CA 名稱或主體名稱值。  


## <a name="objects-that-arent-localized"></a><a name="BKMK_LangNonLocalize"></a> 未當地語系化的物件

Configuration Manager 資料庫針對它所儲存的大部分物件皆支援 Unicode。 可能的話，它會以符合電腦地區設定的 OS 語言顯示此資訊。 電腦的地區設定必須與安裝在站台之用戶端或伺服器語言一致，用戶端介面或 Configuration Manager 主控台才能以該電腦的 OS 語言顯示資訊。  

有數個 Configuration Manager 物件不支援 Unicode。 它們是使用 ASCII 來儲存在資料庫中，或是具有其他語言限制。 這個資訊一律會使用 ASCII 字元集，或是以建立該物件時所使用的語言來顯示。  
