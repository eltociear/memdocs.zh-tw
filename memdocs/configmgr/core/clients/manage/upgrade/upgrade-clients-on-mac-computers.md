---
title: 升級 macOS 用戶端
titleSuffix: Configuration Manager
description: 升級 Mac 電腦上的 Configuration Manager 用戶端。
ms.date: 09/10/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 74c60941-5eae-4905-9e58-252bdb39df96
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: f34d0c9233b4f7384dfc2280dc92334450a785ed
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81696256"
---
# <a name="how-to-upgrade-clients-on-mac-computers-in-configuration-manager"></a>如何在 Configuration Manager 中升級 Mac 電腦上的用戶端

適用於：  Configuration Manager (最新分支)

請遵循本文中的高階步驟，使用 Configuration Manager 應用程式升級 Mac 電腦的用戶端。 您也可以下載 Mac 用戶端安裝檔案，將其複製到共用的網路位置或 Mac 電腦上本機資料夾，然後指示使用者手動執行安裝。  

> [!NOTE]  
> 請先確定您的 Mac 電腦符合必要條件，再執行這些步驟。 請參閱 [Mac 電腦的支援作業系統](../../../plan-design/configs/supported-operating-systems-for-clients-and-devices.md#mac-computers)。  

## <a name="download-the-latest-mac-client"></a>下載最新的 Mac 用戶端

Configuration Manager 安裝媒體不提供適用於 Configuration Manager 的 Mac 用戶端。 從 Microsoft 下載中心下載：[Microsoft Endpoint Configuration Manager - macOS 用戶端 (64 位元)](https://www.microsoft.com/download/details.aspx?id=100850) \(英文\)。 Mac 用戶端安裝檔案包含在名為 **ConfigmgrMacClient.msi** 的 Windows Installer 檔案中。  

## <a name="create-the-mac-client-installation-file"></a>建立 Mac 用戶端安裝檔案

在執行 Windows 的電腦上，執行 **ConfigmgrMacClient.msi**。 此安裝程式會解壓縮名為 **Macclient.dmg** 的 Mac 用戶端安裝檔案。 根據預設，您可在下列資料夾中找到此檔案：**C:\Program Files\Microsoft\System Center Configuration Manager for Mac client**。  

## <a name="extract-the-client-installation-files"></a>解壓縮用戶端安裝檔案

將 **Macclient.dmg** 複製到 Mac 電腦。 在 macOS 中裝載 Macclient.dmg 檔案，然後將內容複製到 Mac 電腦的資料夾。  

## <a name="create-a-cmmac-file"></a>建立 .cmmac 檔案

1. 開啟 Mac 用戶端安裝檔案的 **Tools** 資料夾。 使用 **CMAppUtil** 工具從用戶端安裝套件建立 .cmmac 檔案。 您會使用此檔案建立 Configuration Manager 應用程式。  

2. 將新 **CMClient.pkg.cmmac** 檔案複製到執行 Configuration Manager 主控台電腦可使用的網路位置。  

    如需詳細資訊，請參閱[建立和部署 Mac 電腦的應用程式補充程序](../../../../apps/get-started/creating-mac-computer-applications.md#supplemental-procedures-to-create-and-deploy-applications-for-mac-computers)。  

## <a name="create-and-deploy-the-app"></a>建立並部署應用程式

1. 在 Configuration Manager 主控台中，從 **CMClient.pkg.cmmac** 檔案[建立應用程式](../../../../apps/get-started/creating-mac-computer-applications.md)。  

2. [將此應用程式部署](../../../../apps/deploy-use/deploy-applications.md)至階層中的 Mac 電腦。  

## <a name="install-the-updated-client"></a>安裝更新的用戶端

Mac 電腦的現有 Configuration Manager 用戶端會提示使用者已有可用更新供安裝。 在安裝用戶端之後，使用者必須重新啟動 Mac 電腦。  

電腦重新啟動後，[電腦註冊精靈]  會自動執行以要求新的使用者憑證。

如果您不使用 Configuration Manager 註冊，而要在不透過 Configuration Manager 的情況下獨立安裝用戶端憑證，請參閱[設定用戶端使用現有的憑證](#BKMK_UpgradingClient_MachineEnrollment)。  

## <a name="configure-clients-to-use-an-existing-certificate"></a><a name="BKMK_UpgradingClient_MachineEnrollment"></a> 設定用戶端使用現有的憑證

使用此程序以防止 [電腦註冊精靈] 執行，且將升級的用戶端設定為使用現有的用戶端憑證。  

1. 在 Configuration Manager 主控台中，[建立 **Mac OS X** 類型的設定項目](../../../../compliance/deploy-use/create-configuration-items-for-mac-os-x-devices-managed-with-the-client.md)。  

1. 在此設定項目中新增 [指令碼]  類型的設定。  

1. 將下列指令碼新增至設定：  

  ``` Shell
  #!/bin/sh  
  echo "Starting script\n"  
  echo "Changing directory to MAC Client\n"  
  cd /Users/Administrator/Desktop/'MAC Client'/  
  echo "Import root cert\n"  
  /usr/bin/sudo /usr/bin/security import /Users/Administrator/Desktop/'MAC Client'/Root.pfx -A -k /Library/Keychains/System.Keychain -P ROOT  
  echo "Using openssl to convert pfx to a crt\n"  
  /usr/bin/sudo openssl pkcs12 -in /Users/Administrator/Desktop/'MAC Client'/Root.pfx -out Root1.crt -nokeys -clcerts -passin pass:ROOT  
  echo "Adding trust to root cert\n"  
  /usr/bin/sudo /usr/bin/security add-trusted-cert -d -r trustRoot -k /Library/Keychains/System.Keychain Root1.crt  
  echo "Import client cert\n"  
  /usr/bin/sudo /usr/bin/security import /Users/Administrator/Desktop/'MAC Client'/MacClient.pfx -A -k /Library/Keychains/System.Keychain -P MAC  
  echo "Executing ccmclient with MP\n"  
  sudo ./ccmsetup -MP https://SCCM34387.SCCM34387DOM.NET/omadm/cimhandler.ashx  
  echo "Editing Plist file\n"  
  sudo /usr/libexec/Plistbuddy -c 'Add:SubjectName string CMMAC003L' /Library/'Application Support'/Microsoft/CCM/ccmclient.plist  
  echo "Changing directory to CCM\n"  
  cd /Library/'Application Support'/Microsoft/CCM/  
  echo "Making connection to the server\n"  
  sudo open ./CCMClient  
  echo "Ending Script\n"  
  exit  
  ```  

1. 將設定項目新增至[設定基準](../../../../compliance/deploy-use/create-configuration-baselines.md)。 然後[將設定基準部署至](../../../../compliance/deploy-use/deploy-configuration-baselines.md)所有不透過 Configuration Manager 獨立安裝憑證的 Mac 電腦。  
