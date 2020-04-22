---
title: 升級 Linux 和 UNIX 用戶端
titleSuffix: Configuration Manager
description: 在 Configuration Manager 中升級 Linux 或 UNIX 伺服器的用戶端。
ms.date: 03/27/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 7d2bb377-1005-4a55-bd1f-b80a6d0b22e1
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: f71a36dff92f888d595538ff2fd483d7c212358f
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81696816"
---
# <a name="how-to-upgrade-clients-for-linux-and-unix-servers-in-configuration-manager"></a>如何在 Configuration Manager 中升級 Linux 和 UNIX 伺服器的用戶端

適用於：  Configuration Manager (最新分支)

> [!Important]  
> 從 1902 版開始，Configuration Manager 不支援 Linux 或 UNIX 用戶端。 
> 
> 請考慮以 Microsoft Azure 管理來管理 Linux 伺服器。 Azure 解決方案具有廣泛的 Linux 支援，在大部分情況下都超越 Configuration Manager 的功能性，包括 Linux 的完整修補程式管理。

您可以將電腦上 Linux 和 UNIX 用戶端的版本升級為至較新的用戶端版本，而不需要先解除安裝目前的用戶端。 若要這樣做，請在電腦上安裝新的用戶端安裝套件，同時使用 **-keepdb** 命令列屬性。 安裝 Linux 和 UNIX 用戶端時，會將現有用戶端資料覆寫為新的用戶端檔案。 不過， **-keepdb** 命令列屬性會指示安裝程序保留用戶端唯一識別碼 (GUID)、本機資訊資料庫，以及憑證存放區。 新的用戶端安裝之後會使用這項資訊。  

 例如，您有從 Linux 和 UNIX 之 Configuration Manager 用戶端的原始版本執行用戶端的 RHEL5 x64 電腦。 若要將這個用戶端升級至累計更新 1 中的用戶端版本，請手動執行 **install** 指令碼再加上 **-keepdb** 命令列參數，以安裝累計更新 1 中適用的用戶端套件。 請參閱下列範例命令列：  

`./install -mp <hostname\> -sitecode <code\> -keepdb ccm-Universal-x64.<build\>.tar`  



## <a name="how-to-use-a-software-deployment-to-upgrade-the-client-on-linux-and-unix-servers"></a>如何在 Linux 和 UNIX 伺服器上使用軟體部署來升級用戶端  
 您可以使用軟體部署，將 Linux 和 UNIX 的用戶端升級為新的用戶端版本。 不過，Configuration Manager 用戶端無法直接執行安裝指令碼來安裝新的用戶端，因為安裝新用戶端時，必須先將目前的用戶端解除安裝。 此動作會先結束執行安裝指令碼的 Configuration Manager 用戶端程序，再開始安裝新的用戶端。 若要順利使用軟體部署來安裝新的用戶端，您必須排程在未來的時間開始安裝，並透過作業系統的內建排程功能來執行安裝。  

 請使用軟體部署先將新用戶端安裝套件的檔案複製到用戶端電腦。 接著，再部署和執行指令碼來排定用戶端安裝程序。 指令碼會使用作業系統的內建 **at** 命令來延遲其開始時間。 當指令碼執行時，負責管理其作業的是用戶端作業系統，而非電腦上的 Configuration Manager 用戶端。 此行為可讓指令碼所呼叫的命令列先將 Configuration Manager 用戶端解除安裝，然後再安裝新的用戶端。 這些動作會完成 Linux 或 UNIX 電腦上的用戶端升級程序。 完成升級之後，升級的用戶端仍由 Configuration Manager 所管理。  

 使用下列程序可協助您設定軟體部署來升級 Linux 和 UNIX 的用戶端。 下列步驟和範例將執行用戶端初始版本的 RHEL5 x64 電腦升級為累計更新 1 用戶端版本。  

#### <a name="to-use-a-software-deployment-to-upgrade-the-client-on-linux-and-unix-servers"></a>在 Linux 和 UNIX 伺服器上使用軟體部署來升級用戶端  

1. 將新用戶端安裝套件複製到執行要升級的 Configuration Manager 用戶端電腦。  

    例如，將累計更新 1 的用戶端安裝套件和安裝指令碼放在用戶端電腦上的下列位置： **/tmp/PATCH**  

2. 建立指令碼來管理 Configuration Manager 用戶端的升級。 接著，將一份指令碼放在用戶端電腦上與步驟 1 用戶端安裝檔案相同的資料夾中。  

    此指令碼不需要特定的名稱。 它所包含的命令列必須足以使用用戶端電腦上本機資料夾中的用戶端安裝檔案，以及使用 **-keepdb** 命令列屬性來安裝用戶端安裝套件。 請使用 **-keepdb** 命令列屬性來維護目前用戶端的唯一識別碼，以供將安裝的新用戶端使用。  

    例如，請建立名為 **upgrade.sh** 且包含下列各行的指令碼：  

   ```  
   #!/bin/sh  
   #  
   /tmp/PATCH/install -sitecode <code> -mp <hostname> -keepdb /tmp/PATCH/ccm-Universal-x64.<build>.tar  

   ```  

    接著，將其複製到用戶端電腦上的 **/tmp/PATCH**資料夾。

3. 使用軟體部署，讓每個用戶端先使用電腦內建 **at** 命令來執行具有短暫延遲的 **upgrade.sh** 指令碼，再執行指令碼。  

    例如，使用下列命令列來執行指令碼：**at -f /tmp/upgrade.sh -m now + 5 minutes**  

   用戶端成功排程 **upgrade.sh** 指令碼執行之後，用戶端會提交狀態訊息，指出已順利完成軟體部署。 不過，在延遲之後，實際用戶端安裝之後是由電腦所管理。 完成用戶端升級之後，請檢閱用戶端電腦上的 **/var/opt/microsoft/scxcm.log** 檔案來驗證安裝。 請在 Configuration Manager 主控台 [資產與合規性]  工作區的 [裝置]  節點中檢視用戶端的詳細資料，以確認已安裝用戶端且正在與站台通訊。  
