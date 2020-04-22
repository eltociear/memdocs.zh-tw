---
title: 擷取和還原使用者狀態
titleSuffix: Configuration Manager
description: 您可以使用 Configuration Manager 工作順序來擷取和還原 OS 部署案例中的使用者狀態資料。
ms.date: 08/17/2018
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: d566d85c-bf7a-40e7-8239-57640a1db5f4
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 93a39ba21b9e7d6cacfe59f763756aeef3736d52
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81707346"
---
# <a name="create-a-task-sequence-to-capture-and-restore-user-state-in-configuration-manager"></a>在 Configuration Manager 中建立工作順序以擷取和還原使用者狀態

 適用於：  Configuration Manager (最新分支)

 您可以使用 Configuration Manager 工作順序來擷取和還原 OS 部署案例中的使用者狀態資料。 在這些案例中，您想要保留目前 OS 的使用者狀態。 視您建立的工作順序類型而定，擷取和還原步驟可能會自動新增為工作順序的一部分。 在其他情況下，您可能需要手動新增擷取和還原步驟至工作順序中。 本文提供必須新增到現有工作順序以擷取和還原使用者狀態資料的步驟。  



## <a name="task-sequence-steps"></a>工作順序步驟  

若要擷取和還原使用者狀態，請將下列步驟新增到工作順序中：  

- [要求狀態存放區](../understand/task-sequence-steps.md#BKMK_RequestStateStore)：如果您將使用者狀態儲存在狀態移轉點上，便需要此步驟。  

- [擷取使用者狀態](../understand/task-sequence-steps.md#BKMK_CaptureUserState)：此步驟會擷取使用者狀態資料。 然後它會將資料儲存在狀態移轉點，或使用永久連結的本機磁碟上。  

- [還原使用者狀態](../understand/task-sequence-steps.md#BKMK_RestoreUserState)：此步驟會在目的地電腦上還原使用者狀態資料。 它可以從狀態移轉點或從已在本機磁碟上建立的永久連結擷取資料。  

- [釋放狀態存放區](../understand/task-sequence-steps.md#BKMK_ReleaseStateStore)：如果您將使用者狀態儲存在狀態移轉點上，便需要此步驟。 此步驟會從狀態移轉點移除此資料。  


 請使用下列程序，以新增擷取和還原使用者狀態所需的工作順序步驟。 如需有關建立工作順序的詳細資訊，請參閱[管理工作順序以將工作自動化](manage-task-sequences-to-automate-tasks.md)。  



## <a name="capture-the-user-state"></a>擷取使用者狀態  

 若要新增工作順序步驟以擷取使用者狀態，請使用下列步驟：

1.  在 [工作順序]  清單中，選取工作順序，然後按一下 [編輯]  。  

2.  如果您使用狀態移轉點來儲存使用者狀態，請將 [要求狀態存放區]  步驟新增新增到工作順序中。 在 [工作順序編輯器]  中，按一下 [新增]  。 指向 [使用者狀態]  ，然後按一下 [要求狀態存放區]  。 為此步驟設定內容和選項，然後按一下 [套用]  。 如需有關可用設定的詳細資訊，請參閱[要求狀態存放區](../understand/task-sequence-steps.md#BKMK_RequestStateStore)。  

3.  新增 [擷取使用者狀態]  步驟至工作順序。 在 [工作順序編輯器]  中，按一下 [新增]  。 指向 [使用者狀態]  ，然後按一下 [擷取使用者狀態]  。 為此步驟設定內容和選項，然後按一下 [套用]  。 如需有關可用設定的詳細資訊，請參閱[擷取使用者狀態](../understand/task-sequence-steps.md#BKMK_CaptureUserState)。  

    > [!IMPORTANT]  
    >  當您將此步驟新增新增到工作順序中時，請一併設定 **OSDStateStorePath** 工作順序變數，以指定使用者狀態資料的儲存位置。 如果您將使用者狀態儲存在本機，則請勿指定根資料夾，因為這可能導致工作順序發生失效。 當您將使用者資料儲存在本機時，請一律使用資料夾或子資料夾。 如需有關此變數的詳細資訊，請參閱[工作順序變數](../understand/task-sequence-variables.md#OSDStateStorePath)。  

4.  如果您使用狀態移轉點，請將 [釋放狀態存放區]  步驟新增到工作順序中。 在 [工作順序編輯器]  中，按一下 [新增]  。 指向 [使用者狀態]  ，然後按一下 [釋放狀態存放區]  。 為此步驟設定內容和選項，然後按一下 [套用]  。 如需有關可用設定的詳細資訊，請參閱[釋放狀態存放區](../understand/task-sequence-steps.md#BKMK_ReleaseStateStore)。  

    > [!IMPORTANT]  
    >  在 [釋放狀態存放區]  步驟之前執行的工作順序動作必須先執行成功，[釋放狀態存放區]  步驟才能開始執行。  


 部署此工作順序以擷取目的地電腦上的使用者狀態。 如需如何部署工作順序的相關資訊，請參閱[部署工作順序](deploy-a-task-sequence.md)。  



## <a name="restore-the-user-state"></a>還原使用者狀態  

 若要新增工作順序步驟以還原使用者狀態，請使用下列步驟：

1. 在 [工作順序]  清單中，選取工作順序，然後按一下 [編輯]  。  

2. 將**還原使用者狀態**步驟新增至工作順序。 在 [工作順序編輯器]  中，按一下 [新增]  。 指向 [使用者狀態]  ，然後按一下 [還原使用者狀態]  。 此步驟會視需要建立與狀態移轉點的連線。 為此步驟設定內容和選項，然後按一下 [套用]  。 如需有關可用設定的詳細資訊，請參閱[還原使用者狀態](../understand/task-sequence-steps.md#BKMK_RestoreUserState)。  

   > [!Important]  
   >  當您使用[擷取使用者狀態](../understand/task-sequence-steps.md#BKMK_CaptureUserState)步驟搭配 [使用標準選項擷取所有使用者設定檔]  選項時，必須在 [還原使用者狀態]  步驟中選取 [還原本機使用者設定檔]  設定。 否則工作順序將會失敗。  

   > [!Note]  
   > 如果您使用本機永久連結來還原使用者狀態，而還原發生失敗，則您可以手動刪除所建立來儲存資料的永久連結。 工作順序可以執行 USMTUtils 工具，藉由[執行命令列](../understand/task-sequence-steps.md#BKMK_RunCommandLine)步驟來將此動作自動化。 如果您使用 USMTUtils 來刪除永久連結，請在執行 USMTUtils 後新增[重新啟動電腦](../understand/task-sequence-steps.md#BKMK_RestartComputer)步驟。  

3. 如果您使用狀態移轉點來儲存使用者狀態，請將 [釋放狀態存放區]  步驟新增到工作順序中。 在 [工作順序編輯器]  中，按一下 [新增]  。 指向 [使用者狀態]  ，然後按一下 [釋放狀態存放區]  。 為此步驟設定內容和選項，然後按一下 [套用]  。 如需有關可用設定的詳細資訊，請參閱[釋放狀態存放區](../understand/task-sequence-steps.md#BKMK_ReleaseStateStore)。  

   > [!IMPORTANT]  
   >  在 [釋放狀態存放區]  步驟之前執行的工作順序動作必須先執行成功，[釋放狀態存放區]  步驟才能開始執行。  


 部署這項工作順序以還原目的地電腦上的使用者狀態。 如需部署工作順序的相關資訊，請參閱[部署工作順序](deploy-a-task-sequence.md)。  



## <a name="next-steps"></a>後續步驟

[監視工作順序部署](monitor-operating-system-deployments.md#BKMK_TSDeployStatus)
