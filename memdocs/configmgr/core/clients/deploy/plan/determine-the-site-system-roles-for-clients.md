---
title: 用戶端的站台系統角色
titleSuffix: Configuration Manager
description: 在 Configuration Manager 中判斷用戶端的站台系統角色。
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 984e8d92-7327-4b08-9228-0c955e6ac778
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 32895df466c41ca828d1107857212b8d5a777026
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81693746"
---
# <a name="determine-the-site-system-roles-for-configuration-manager-clients"></a>為 Configuration Manager 用戶端判斷站台系統角色

適用於：  Configuration Manager (最新分支)

本文可協助您判斷部署 Configuration Manager 用戶端所需的站台系統角色。

如需在階層的何處安裝這些角色的詳細資訊，請參閱[設計站台階層](../../../plan-design/hierarchy/design-a-hierarchy-of-sites.md)。  

如需如何安裝及設定這些角色的詳細資訊，請參閱[安裝站台系統角色](../../../servers/deploy/configure/install-site-system-roles.md)。  

## <a name="management-point"></a>管理點

根據預設，所有 Windows 用戶端電腦都會使用發佈點來安裝 Configuration Manager 用戶端。 當發佈點無法使用時，它們可切換回管理點。 不過，當您使用 CCMSetup 命令列屬性 `/source:<Path>` 時，可從替代來源在電腦上安裝 Windows 用戶端。 例如，如果您在網際網路上安裝用戶端，可能就會執行此動作。 另一種案例是當您想要在用戶端安裝期間，避免在電腦與管理點之間傳送網路封包。 此案例是因為防火牆會封鎖所需的連接埠，或是因為您具有低頻寬的連線。 不過，所有的用戶端都必須和要指派到站台的管理點通訊，並由 Configuration Manager 進行管理。  

如需用戶端命令列屬性的詳細資訊，請參閱[關於用戶端安裝屬性](../about-client-installation-properties.md)。  

當您在階層中安裝一個以上的管理點時，用戶端會根據其樹系成員資格及網路位置，自動連線到其中一個點。 您無法在次要站台中安裝一個以上的管理點。  

Mac 電腦用戶端以及您向 Configuration Manager 註冊的行動裝置用戶端，一律需要管理點以進行用戶端安裝。 此管理點必須位於主要站台、必須設定為支援行動裝置，並且必須接受來自網際網路的用戶端連線。 這些用戶端無法在次要站台中使用管理點，或連線到其他主要站台的管理點。  

## <a name="distribution-point"></a>發佈點

您不需要發佈點就能在 Windows 電腦上安裝 Configuration Manager。 根據預設，Configuration Manager會使用發佈點，在 Windows 電腦上安裝用戶端來源檔案。 它可以切換回從管理點下載這些檔案。 發佈點不會用來安裝由 Configuration Manager 註冊的行動裝置用戶端，但如果您安裝了行動裝置舊版用戶端，就會使用發佈點。 如果您將 Configuration Manager 用戶端當成 OS 部署的一部分來安裝，便會儲存並從發佈點擷取 OS 映像。

雖然您可能不需要發佈點就能安裝大多數的 Configuration Manager 用戶端，但您還是需要使用它們，在用戶端上安裝應用程式和軟體更新之類的軟體。  

## <a name="fallback-status-point"></a>後援狀態點

您可以使用後援狀態點來監視 Windows 電腦的用戶端部署。 您也可以識別因無法與管理點通訊而非受控的 Windows 電腦用戶端。

下列用戶端類型不會使用後援狀態點：

- Mac 電腦
- 由 Configuration Manager 註冊的行動裝置
- 使用 Exchange Server 連接器所管理的行動裝置

不需要後援狀態點，就能監視用戶端活動及用戶端健康情況。  

後援狀態點永遠都是透過 HTTP 來和用戶端通訊，其使用未經授權的連線，並以純文字傳送資料。 此行為會使後援狀態點容易遭受攻擊，尤其是在搭配使用網際網路型用戶端管理時。 為了協助減少受攻擊面，一律將伺服器專用於執行後援狀態點。 請勿在實際執行環境中的相同伺服器上安裝其他網站系統角色。  

如果下列所有條件都適用，則安裝後援狀態點：  

- 您希望將 Windows 電腦的用戶端通訊錯誤傳送到站台，即使這些用戶端電腦無法與管理點通訊也一樣。  

- 您想要使用 Configuration Manager 用戶端部署報告，這些報告會顯示由後援狀態點所傳送的資料。  

- 您擁有此站台系統角色專用的伺服器，並且用其他安全性量值進行保護，防止伺服器遭受攻擊。  

- 使用後援狀態點的好處，勝過與未授權連線以及透過 HTTP 流量傳送純文字相關聯的安全性風險。  

如果使用未經授權的連線來執行網站以及純文字傳送的安全性風險，勝過識別出用戶端通訊問題的好處，請勿安裝後援狀態點。  

## <a name="reporting-services-point"></a>Reporting Services 點

Configuration Manager 提供許多報告，協助您在 Configuration Manager 主控台監視安裝、指派及管理用戶端。 有些用戶端部署報告要求將用戶端指派到後援狀態點。  

不需要報告，就能部署用戶端。 您可以在 Configuration Manager 主控台中查看一些部署資訊，或使用用戶端記錄檔來取得詳細資訊。 不過，用戶端報告會提供有用的資訊，協助您監視和疑難排解用戶端部署。  

## <a name="enrollment-point-and-enrollment-proxy-point"></a>註冊點和註冊 Proxy 點

Configuration Manager 需要使用註冊點和註冊 Proxy 點註冊行動裝置，並註冊 Mac 電腦的憑證。 在下列情況中，您不需要這些站台系統角色：

- 您打算使用 Exchange Server 連接器來管理行動裝置
- 例如，您要針對 Windows CE 安裝行動裝置舊版用戶端
- 您會在 Mac 電腦上，單獨從 Configuration Manager 要求並安裝用戶端憑證

## <a name="application-catalog"></a>應用程式類別目錄

> [!Important]  
> 從 1806 最新分支版本開始即不支援應用程式類別目錄的 Silverlight 使用者體驗。 從 1906 版開始，已更新的用戶端會自動使用適用於使用者可用應用程式部署的管理點。 此外，您也無法安裝新的應用程式目錄角色。 1910 版會終止對應用程式類別目錄角色的支援。  
>
> 如需詳細資訊，請參閱下列文章：
>
> - [設定軟體中心](../../../../apps/plan-design/plan-for-software-center.md#bkmk_userex)
> - [已移除和已淘汰的功能](../../../plan-design/changes/deprecated/removed-and-deprecated-cmfeatures.md)  

## <a name="cloud-management-gateway-connector-point"></a>雲端管理閘道連接器端點

如果您正在設定[雲端管理閘道](../../manage/cmg/plan-cloud-management-gateway.md)以[管理網際網路上的用戶端](../../manage/manage-clients-internet.md)，則需要雲端管理閘道連接器點。
