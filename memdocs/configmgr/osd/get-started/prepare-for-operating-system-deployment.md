---
title: 準備 OS 部署
titleSuffix: Configuration Manager
description: 了解如何在 Configuration Manager 中準備作業系統部署
ms.date: 02/22/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 8d27e5ac-4f19-4b3d-85c7-fa34eb5d5e7e
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: bdd8cd61aedb06fe35a4ba268806f64cc18bf85d
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81708836"
---
# <a name="prepare-for-os-deployment-in-configuration-manager"></a>在 Configuration Manager 中準備 OS 部署

適用於：  Configuration Manager (最新分支)

有幾件事，必須先在 Configuration Manager 完成，才能部署作業系統。 使用下列文章來準備進行 OS 部署：  

-   [管理開機映像](manage-boot-images.md)  

-   [管理 OS 映像](manage-operating-system-images.md)  

-   [管理 OS 升級套件](manage-operating-system-upgrade-packages.md)  

-   [管理驅動程式](manage-drivers.md)  

-   [管理使用者狀態](manage-user-state.md)  

-   [準備未知電腦部署](prepare-for-unknown-computer-deployments.md)  

-   [為使用者與目的地電腦建立關聯](associate-users-with-a-destination-computer.md)  



### <a name="os-image-size"></a>OS 映像大小  

OS 映像的大小太大。 例如，Windows 7 的映像大小為 3 GB 以上。 同時要將 OS 部署到其中的映像大小和電腦數目，會影響網路效能和可用頻寬。 請確定會測試網路效能。 測試影響可更好地衡量映像部署可能造成的影響及其用來完成部署的時間。 Configuration Manager 活動包括將映像發佈到發佈點、將映像從某個站台發佈到另一個站台，以及將映像下載到用戶端。  

同時，確定您已在裝載 OS 映像的發佈點上，規劃了足夠的磁碟儲存空間。  

如需詳細資訊，請參閱[發佈點的額外規劃考量](prepare-site-system-roles-for-operating-system-deployments.md#BKMK_AdditionalPlanning)。


### <a name="client-cache-size"></a>用戶端快取大小  

當 Configuration Manager 用戶端下載內容時，它們會自動使用背景智慧型傳送服務 (BITS) (如果可用)。 當您部署安裝 OS 的工作順序時，可以在部署上設定一個選項，使 Configuration Manager 用戶端先將完整映像下載至本機快取，再執行工作順序。  

當 Configuration Manager 用戶端必須下載 OS 映像，但快取中沒有足夠的空間時，用戶端可清除其快取中的空間。 它會檢查快取中的其他套件，以判斷刪除任何舊套件是否將釋放足夠的磁碟空間來容納映像。 如果刪除套件無法釋放足夠的空間，則用戶端不會下載映像，而部署也會失敗。 如果快取具有已設定為必須在快取中保存的大型套件，則會發生此行為。 如果刪除封裝可以在快取中釋放足夠的可用磁碟空間，用戶端便會刪除這些封裝，然後下載映像至快取。  

Configuration Manager 用戶端上的預設快取大小，可能不足以容納大部分的 OS 映像部署。 如果您打算將完整映像下載至用戶端快取，請調整目的地電腦上的用戶端快取大小，以容納您要部署的映像大小。  

如需詳細資訊，請參閱[設定用戶端快取](../../core/clients/manage/manage-clients.md#BKMK_ClientCache)。  


