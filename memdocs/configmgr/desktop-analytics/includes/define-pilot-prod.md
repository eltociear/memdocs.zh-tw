---
author: aczechowski
ms.author: aaroncz
ms.reviewer: acabello
ms.prod: configuration-manager
ms.topic: include
ms.date: 12/30/2018
ms.openlocfilehash: 431c88b07889f7c80d2723425aaef2245c7f06bc
ms.sourcegitcommit: fddbb6c20cf7e19944944d4f81788adf249c963f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/12/2020
ms.locfileid: "83268773"
---
使用下列定義來區別試驗和生產：  

- **試驗**：您想要在部署至較大集合之前驗證的裝置子集。 使用電腦分析，將裝置標示為試驗集的唯一。 當沒有任何資產被封鎖時，試驗中的裝置就可以準備進行升級。 封鎖資產會標示為「重大」  且「無法」  升級。  

- **Production**：所有其他已註冊至電腦分析且不在試驗中的裝置。 當所有資產都已核准時，生產裝置就可以準備進行升級。 電腦分析會自動核准所有非重大資產。  
