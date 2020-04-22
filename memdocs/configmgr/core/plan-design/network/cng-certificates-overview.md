---
title: CNG 憑證概觀
titleSuffix: Configuration Manager
description: 了解 Configuration Manager 用戶端和伺服器對新一代密碼編譯 (CNG) 憑證的支援。
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: dba904ae-7c44-46db-ae63-999b9821cb46
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 4574b7ae97e8200da248a0b798677eacadb6229f
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81703076"
---
# <a name="cng-certificates-overview"></a>CNG 憑證概觀
<!-- 1356191 --> 

Configuration Manager 對密碼編譯新一代 (CNG) 憑證的支援有限。 設定管理員用戶端可以搭配 CNG 金鑰儲存提供者 (KSP) 中的私密金鑰來使用 PKI 用戶端驗證憑證。 有 KSP 的支援，Configuration Manager 用戶端可以支援硬體式私用金鑰，例如 PKI 用戶端驗證憑證的 TPM KSP。

## <a name="supported-scenarios"></a>支援的案例
下列案例可以使用[密碼編譯 API 新一代 (CNG)](https://msdn.microsoft.com/library/windows/desktop/bb204775.aspx) 憑證範本：

- 搭配 HTTPS 管理點進行用戶端登錄及通訊   
- 搭配 HTTPS 發佈點進行軟體發佈及應用程式部署   
- 作業系統部署  
- 用戶端傳訊 SDK (含最新更新) 及 ISV Proxy   
- 雲端管理閘道設定  

從 1802 版開始，請針對以下支援 HTTPS 的伺服器角色使用 CNG 憑證： <!-- 1357314 -->   
- 管理點
- 發佈點
- 軟體更新點
- 狀態移轉點     

從 1806 版開始，請針對以下支援 HTTPS 的伺服器角色使用 CNG 憑證：

- 憑證登錄點，包括自帶 Configuration Manager 原則模組的 NDES 伺服器 <!--1357314-->

> [!NOTE]
> CNG 與密碼編譯 API (CAPI) 相容。 即使用戶端已啟用 CNG 支援，仍繼續支援 CAPI 憑證。

## <a name="unsupported-scenarios"></a>不支援的案例

目前不支援下列案例：

- 在 HTTPS 模式中使用已繫結至 Internet Information Services (IIS) 中之網站的 CNG 憑證進行安裝時，下列伺服器角色不會運作： 
    - 應用程式類別目錄 Web 服務
    - 應用程式類別目錄網站
    - 註冊點  
    - 註冊 Proxy 點  

- 已部署到使用者或使用者群組集合的應用程式和套件，軟體中心未顯示為可用。

- 使用 CNG 憑證建立雲端發佈點。

- 如果 NDES 原則模組使用 CNG 憑證進行用戶端驗證，與憑證登錄點的通訊就會失敗。 
    - 自 Configuration Manager 1806 版開始支援此功能。

- 如果您在建立工作順序媒體時指定 CNG 憑證，精靈就無法建立可開機媒體。
    - 自 Configuration Manager 1806 版開始支援此功能。

## <a name="to-use-cng-certificates"></a>使用 CNG 憑證

若要使用 CNG 憑證，您的憑證授權單位 (CA) 必須為目標電腦提供 CNG 憑證範本。 範本詳細資料會因案例而有所不同，不過下列屬性皆為必要項目：

- [相容性]  索引標籤

    - [憑證授權單位]  必須為 Windows Server 2008 或更新版本。 (建議使用 Windows Server 2012)。

    - [憑證接收者]  必須為 Windows Vista/Server 2008 或更新版本。 (建議使用 Windows 8/Windows Server 2012)。

- [密碼編譯]  索引標籤

    - [提供者類別]  必須為 [金鑰儲存提供者]  。 (必要)
    - **要求必須使用下列其中一個提供者：** 必須是 **Microsoft 軟體金鑰儲存體提供者**。 

> [!NOTE]
> 環境或組織的需求可能不同。 請連絡您的 PKI 專家。 考量的重點是憑證範本必須使用金鑰儲存提供者，以善加利用 CNG。

若要獲得最佳結果，建議根據 Active Directory 資訊建置 [主體名稱]。 使用 [DNS 名稱] 作為 [主體名稱格式]  ，並將 DNS 名稱包含在次要主體名稱中。 否則，您必須在裝置註冊至憑證設定檔時提供此資訊。
