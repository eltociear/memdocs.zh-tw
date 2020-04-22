---
title: 建立自訂工作順序
titleSuffix: Configuration Manager
description: 在 Configuration Manager 中編輯自訂工作順序，以在工作順序中新增步驟。
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: b9800a66-7541-47ca-8276-da8ef6cb6d1b
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 9107e9787cf7f12cab624101c37344ea20684112
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81704196"
---
# <a name="create-a-custom-task-sequence-with-configuration-manager"></a>使用 Configuration Manager 建立自訂工作順序

適用於：  Configuration Manager (最新分支)

當在 Configuration Manager 中建立自訂工作順序時，該工作順序不會包含任何工作順序步驟。 建立工作順序之後，您必須加以編輯，並新增您需要的工作順序步驟。  

## <a name="create-a-custom-task-sequence"></a><a name="BKMK_CustomTS"></a> 建立自訂工作順序

使用下列程序建立自訂工作順序：

1. 在 Configuration Manager 主控台中，移至 [軟體程式庫]  工作區，展開 [作業系統]  ，然後選取 [工作順序]  節點。  

1. 在功能區的 [首頁]  索引標籤上，選取 [建立]  群組中的 [建立工作順序]  。 這個動作會啟動 [建立工作順序精靈]。  

1. 在 [建立新的工作順序]  頁面上，選取 [建立新的自訂工作順序]  。  

1. 在 [工作順序資訊]  頁面上指定：

    - 工作的名稱
    - 工作順序的描述
    - 讓工作順序使用的選擇性開機映像

完成 [建立工作順序精靈] 後，Configuration Manager 會將自訂的工作順序新增至 [工作順序]  節點。 您現在可以編輯此工作順序，為其新增工作順序步驟。  

## <a name="see-also"></a>請參閱

如需可用工作順序步驟的清單，請參閱[工作順序步驟](../understand/task-sequence-steps.md)。  

如需如何編輯工作順序的詳細資訊，請參閱[使用工作順序編輯器](../understand/task-sequence-editor.md)。  

通常會使用工作順序將 OS 部署的工作自動化，但是您可建立自訂工作順序，以自動化各種不同的工作。 如需詳細資訊，請參閱[建立非 OS 部署的工作順序](create-a-task-sequence-for-non-operating-system-deployments.md)。

從 2002 版開始，可透過應用程式模型以使用工作順序來安裝複雜的應用程式。 將部署類型新增到本身為工作順序的應用程式 (安裝或解除安裝應用程式)。 如需詳細資訊，請參閱[建立 Windows 應用程式](../../apps/get-started/creating-windows-applications.md#bkmk_tsdt)。<!-- 3555953 -->

## <a name="next-steps"></a>後續步驟

[部署工作順序](deploy-a-task-sequence.md)
