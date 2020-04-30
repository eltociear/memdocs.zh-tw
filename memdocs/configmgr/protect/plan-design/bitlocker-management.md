---
title: BitLocker 管理規劃
titleSuffix: Configuration Manager
description: 規劃使用 Configuration Manager 來管理 BitLocker 磁碟機加密
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: a4d8cda2-bc9b-4fb4-aa0d-23c31b4fc60b
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 926d1483739b85f787ebc9e2a992ea7ed39633c2
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81706186"
---
# <a name="plan-for-bitlocker-management"></a>BitLocker 管理規劃

適用於：  Configuration Manager (最新分支)

<!-- 3601034 -->

從 1910 版開始，請使用 Configuration Manager 來管理內部部署 Windows 用戶端的 BitLocker 磁碟機加密 (BDE)。 Configuration Manager 提供完整的 BitLocker 生命週期管理，其可取代使用 Microsoft BitLocker Administration and Monitoring (MBAM)。

> [!Note]  
> 根據預設，Configuration Manager 不會啟用此選擇性功能。 您必須先先啟用這項功能才能使用它。 如需詳細資訊，請參閱[從更新啟用選擇性功能](../../core/servers/manage/install-in-console-updates.md#bkmk_options)。  

如需詳細資訊，請參閱 [BitLocker 概觀](https://docs.microsoft.com/windows/security/information-protection/bitlocker/bitlocker-overview)。

> [!TIP]
> 若要使用 Microsoft 端點管理員雲端服務來管理共同受控 Windows 10 裝置上的加密，請將 [**Endpoint Protection** 工作負載](../../comanage/workloads.md#endpoint-protection)切換至 Intune。 如需使用 Intune 的詳細資訊，請參閱 [Windows 加密](/intune/protect/endpoint-protection-windows-10#windows-encryption)。

## <a name="features"></a>功能

Configuration Manager 提供下列適用於 BitLocker 磁碟機加密的管理功能：

### <a name="client-deployment"></a>用戶端部署

將 BitLocker 用戶端部署到在 Windows 10 或 Windows 8.1 上執行的受控 Windows 裝置

### <a name="manage-encryption-policies"></a>管理加密原則

- 例如：選擇磁碟機加密和加密強度、設定使用者豁免原則、固定的資料磁碟機加密設定。

- 決定用來加密裝置的演算法，以及所要加密的磁碟。

- 強制使用者在使用裝置之前先取得新安全性原則的相容性。

- 依據每部裝置來自訂組織的安全性設定檔。

- 當使用者解除鎖定 OS 磁碟機時，請指定是否只解除鎖定 OS 磁碟機，或解除所有連結的磁碟機。

### <a name="compliance-reports"></a>合規性報告

下列項目的內建報告：

- 每個磁碟區或每部裝置的加密狀態
- 裝置的主要使用者
- 合規性狀態
- 不符合規範的原因

### <a name="administration-and-monitoring-website"></a>管理和監視網站

允許組織其他角色在 Configuration Manager 主控台外部協助進行金鑰復原，包括金鑰輪替和其他 BitLocker 相關支援。 例如，技術支援中心系統管理員可以協助使用者進行金鑰復原。

### <a name="user-self-service-portal"></a>使用者自助入口網站

讓使用者利用單一金鑰來協助自己解除鎖定 BitLocker 加密的裝置。 使用此金鑰之後，即會為裝置產生新的金鑰。

## <a name="prerequisites"></a>先決條件

- 若要建立 BitLocker 管理原則，則需要在 Configuration Manager 中具備**系統高權限管理員**角色。

- BitLocker金鑰服務需要 HTTPS，才能從 Configuration Manager 用戶端將網路上的修復金鑰加密至管理點。 有兩個選項：

  - 針對在管理點上裝載復原服務的 IIS 網站啟用 HTTPS。 此選項僅適用於 Configuration Manager 2002 版。<!-- 5925660 -->

  - 設定 HTTPS 的管理點。 此選項適用於 Configuration Manager 1910 或 2002 版。

  如需詳細資訊，請參閱[加密復原資料](../deploy-use/bitlocker/encrypt-recovery-data.md)。

- 若要使用 BitLocker 管理報告，請安裝 Reporting Services 點站台系統角色。 如需詳細資訊，請參閱[設定報告](../../core/servers/manage/configuring-reporting.md)。

    > [!NOTE]
    > 若要讓**復原稽核報告**能在管理與監視網站上運作，請僅在主要站台使用 Reporting Services 點。

- 若要使用自助入口網站或管理與監視網站，您需要執行 IIS 的 Windows Server。 您可重複使用 Configuration Manager 站台系統，或使用可連線至站台資料庫伺服器的獨立網頁伺服器。 使用[站台系統伺服器支援的 OS 版本](../../core/plan-design/configs/supported-operating-systems-for-site-system-servers.md)。

    > [!NOTE]
    > 只安裝具有主要站台資料庫的自助入口網站，以及管理與監視網站。 在階層中，為每個主要站台安裝這些網站。

- 在即將裝載自助入口網站的網頁伺服器上，安裝 [Microsoft ASP.NET MVC 4.0](https://docs.microsoft.com/aspnet/mvc/mvc4)。

- 執行入口網站安裝程式指令碼的使用者帳戶需要站台資料庫伺服器上的 SQL **系統管理員**權限。 在安裝流程中，該指令碼會設定網頁伺服器電腦帳戶的登入、使用者與 SQL 角色權限。 當完成安裝自助入口網站和管理與監視網站後，即可以從系統管理員角色移除此使用者帳戶。

- 虛擬機器 (VM) 不支援 BitLocker 管理。 因此，某些功能在虛擬機器上可能無法如預期般運作。 例如，BitLocker 管理不會在虛擬機器的固定磁碟機上啟動加密。 虛擬機器中的其他固定磁碟機可能會顯示為符合規範，即使其並未加密也一樣。

> [!TIP]
> 根據預設，**啟用 BitLocker** 工作順序步驟只會加密磁碟機上「已使用的空間」  。 BitLocker 管理使用「完整磁碟」  加密。 設定此工作順序步驟以啟用**使用完整磁碟加密**的選項。 如需詳細資訊，請參閱[工作順序步驟 - 啟用 BitLocker](../../osd/understand/task-sequence-steps.md#BKMK_EnableBitLocker)。

## <a name="next-steps"></a>後續步驟

[加密復原資料](../deploy-use/bitlocker/encrypt-recovery-data.md) (第一次部署原則之前的選擇性必要條件)

[部署 BitLocker 管理用戶端](../deploy-use/bitlocker/deploy-management-agent.md)
