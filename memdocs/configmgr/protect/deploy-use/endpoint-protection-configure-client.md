---
title: Endpoint Protection 用戶端狀設定
titleSuffix: Configuration Manager
description: 了解如何設定 Endpoint Protection 的自訂用戶端設定。
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: e63f2394-6eb1-4a33-bec5-8377fc62a34e
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 25a1803d7a2feebe7947478c0671e0112830b0d3
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81709176"
---
# <a name="configure-custom-client-settings-for-endpoint-protection"></a>設定 Endpoint Protection 的自訂用戶端設定

適用於：  Configuration Manager (最新分支)

此程序會設定 Endpoint Protection 的自訂用戶端設定，您可以將這些設定部署至階層中的裝置集合。

> [!IMPORTANT]  
>  如果您確定要將設定套用到階層中的所有電腦，請僅設定預設的 Endpoint Protection 用戶端設定。 



## <a name="to-enable-endpoint-protection-and-configure-custom-client-settings"></a>啟用 Endpoint Protection 及設定自訂用戶端設定

1. 在 Configuration Manager 主控台中，按一下 [系統管理]  。  

2. 在 [系統管理]  工作區中，按一下 [用戶端設定]  。  

3. 在 [首頁]  索引標籤的 [建立]  群組中，按一下 [建立自訂用戶端裝置設定]  。  

4. 在 [建立自訂用戶端裝置設定]  對話方塊中，提供設定群組的名稱和說明，然後選取 [Endpoint Protection]  。  

5. 設定您需要的 Endpoint Protection 用戶端設定。 如需您可設定之 Endpoint Protection 用戶端設定的完整清單，請參閱[關於用戶端設定](../../core/clients/deploy/about-client-settings.md#endpoint-protection)中的＜Endpoint Protection＞一節。  

   > [!IMPORTANT]  
   >  請先安裝 Endpoint Protection 站台系統角色，再設定 Endpoint Protection 的用戶端設定。  

6. 按一下 [確定]  關閉 [建立自訂用戶端裝置設定]  對話方塊。 新的用戶端設定會顯示在 [系統管理]  工作區的 [用戶端設定]  節點中。  

7. 接下來，將自訂用戶端設定部署至集合。 選取您要部署的自訂用戶端設定。 在 [首頁]  索引標籤的 [用戶端設定]  群組中，按一下 [部署]  。  

8. 在 [選取集合]  對話方塊中，選取您想要在其中部署用戶端設定的集合，然後按一下 [確定]  。 新的部署會顯示在 [詳細資料] 窗格的 [部署]  索引標籤中。  

用戶端會在下一次下載用戶端原則時進行這些設定。 如需詳細資訊，請參閱[起始 Configuration Manager 用戶端的原則抓取](../../core/clients/manage/manage-clients.md#BKMK_PolicyRetrieval)。  



## <a name="how-to-provision-the-endpoint-protection-client-in-a-disk-image"></a>如何在磁碟映像中佈建 Endpoint Protection 用戶端

在將作為 Configuration Manager OS 部署磁碟映像來源的電腦上，安裝 Endpoint Protection 用戶端。 這個電腦通常稱為參照電腦。 在您建立 OS 映像之後，使用 Configuration Manager OS 部署來部署映像。

> [!Important]  
> Windows 10 和 Windows Server 2016 預設已安裝 Windows Defender。 這些 Windows 版本上不需要此程序。  

使用下列程序可協助您在參照電腦上安裝並設定 Endpoint Protection 用戶端。


### <a name="prerequisites"></a>先決條件

以下清單包含在參照電腦上安裝 Endpoint Protection 用戶端軟體所需的必要條件。

- 您必須能夠存取 Endpoint Protection 用戶端安裝套件 **scepinstall.exe**。 在站台伺服器上 Configuration Manager 安裝資料夾的 **Client** 資料夾中找到這個套件。  

- 若要部署 Endpoint Protection 用戶端與您組織所需的設定，請建立並匯出反惡意程式碼原則。 然後，當您手動安裝 Endpoint Protection 用戶端時，指定此原則。 如需詳細資訊，請參閱[如何建立和部署反惡意程式碼原則](endpoint-antimalware-policies.md)。  

  > [!NOTE]  
  >  您無法匯出 [預設用戶端反惡意程式碼原則]  。  

- 如果您想要安裝具有最新定義的 Endpoint Protection 用戶端，請從 [Windows Defender Security Intelligence](https://www.microsoft.com/wdsi) 下載。  

> [!NOTE]  
> 從 Configuration Manager 1802 開始，您不需要在 Windows 10 裝置上安裝 Endpoint Protection 代理程式 (SCEPInstall)。 如果 Windows 10 裝置上已安裝該代理程式，Configuration Manager 不會移除它。 系統管理員可移除至少執行 1802 用戶端版本之 Windows 10 裝置的 Endpoint Protection 代理程式。 SCEPInstall.exe 仍可能出現在某些電腦上的 C:\Windows\ccmsetup 中，但新的用戶端安裝應該不會下載它。 <!--503654-->


### <a name="how-to-install-the-endpoint-protection-client-on-the-reference-computer"></a>如何在參照電腦上安裝 Endpoint Protection 用戶端

請從命令提示字元在參照電腦上本機安裝 Endpoint Protection 用戶端。 先取得安裝檔案 **scepinstall.exe**。 如需詳細資訊，請參閱[從命令提示字元安裝 Endpoint Protection 用戶端](#bkmk_manual-install)。

如有必要，也可以包含預先設定的反惡意程式碼原則或先前匯出的反惡意程式碼原則。 



## <a name="to-install-the-endpoint-protection-client-from-a-command-prompt"></a><a name="bkmk_manual-install"></a> 從命令提示字元安裝 Endpoint Protection 用戶端

1. 從 Configuration Manager 安裝資料夾的 **Client** 資料夾，將 **scepinstall.exe** 複製到您要安裝 Endpoint Protection 用戶端軟體的電腦上。  

2. 以系統管理員身分開啟命令提示字元。 將目錄變更為安裝程式所在的資料夾。 然後執行 `scepinstall.exe`，並新增您所需的任何其他命令列屬性：


   |  屬性   |                                  說明                                   |
   |-------------|--------------------------------------------------------------------------------|
   |    `/s`     |                           以無訊息模式執行安裝程式                           |
   |    `/q`     |                        以無訊息模式解壓縮安裝程式檔案                        |
   |    `/i`     |                           正常執行安裝程式                           |
   |  `/policy`  | 指定要在安裝期間設定用戶端的反惡意程式碼原則檔案 |
   | `/sqmoptin` |     加入 Microsoft 客戶經驗改進計畫 (CEIP)     |


3. 遵循畫面上的指示完成用戶端安裝。  

4. 如果您已下載最新的更新定義套件，請複製套件至用戶端電腦，然後按兩下定義套件予以安裝。  

   > [!NOTE]  
   >  在 Endpoint Protection 用戶端安裝完成之後，用戶端會自動執行定義更新檢查。 如果此更新檢查成功，您就不需要手動安裝最新的定義更新套件。  

#### <a name="example-install-the-client-with-an-antimalware-policy"></a>範例：使用反惡意程式碼原則安裝用戶端

`scepinstall.exe /policy <full path>\<policy file>`



## <a name="verify-the-endpoint-protection-client-installation"></a>確認 Endpoint Protection 用戶端安裝

在參照電腦上安裝 Endpoint Protection 用戶端之後，請確認用戶端是否正常運作。

1.  在參照電腦上，從 Windows 通知區域開啟 **System Center Endpoint Protection**。  

2.  在 [System Center Endpoint Protection]  對話方塊的 [首頁]  索引標籤上，確認 [即時保護]  已設為 [開啟]  。  

3.  確認 [病毒和間諜軟體定義]  顯示為 [最新]  。  

4.  若要確認您的參照電腦已就緒可進行映像處理，請在 [掃描選項]  下選取 [完整]  ，然後按一下 [立即掃描]  。  



## <a name="prepare-the-endpoint-protection-client-for-imaging"></a>準備 Endpoint Protection 用戶端以進行映像處理

執行下列步驟以準備 Endpoint Protection 用戶端進行映像處理：

1. 在參照電腦上，以系統管理員身分登入。  

2. 從 [Windows SysInternals](https://docs.microsoft.com/sysinternals/downloads/psexec) 下載並安裝 **PsExec**。  

3. 以系統管理員身分執行命令提示字元，將目錄變更為您安裝 PsTools 的資料夾，然後鍵入下列命令：  

   `psexec.exe -s -i regedit.exe`  

   > [!IMPORTANT]  
   >  以此方式執行登錄編輯程式時請留意。 PsExec.exe 會在 LocalSystem 內容中執行它。  

4. 在登錄編輯程式中，刪除下列登錄機碼：  

   > [!IMPORTANT]  
   >  刪除這些登錄機碼是在製作參照電腦映像之前的最後步驟。 Endpoint Protection 用戶端會在啟動時重新建立這些機碼。 如果您重新啟動參照電腦，請再次刪除登錄機碼。  

   -   `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft Antimalware\InstallTime`  

   -   `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft Antimalware\Scan\LastScanRun`  

   -   `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft Antimalware\Scan\LastScanType`  

   -   `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft Antimalware\Scan\LastQuickScanID`   

   -   `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft Antimalware\Scan\LastFullScanID`  

   -   `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\RemovalTools\MRT\GUID`

您現在可以準備參照電腦進行映像處理。

當您部署含有 Endpoint Protection 用戶端的 OS 映像時，它會自動將資訊報告給裝置指派的 Configuration Manager 站台。 用戶端會下載並套用任何目標反惡意程式碼原則。  



## <a name="see-also"></a>請參閱

如需 Configuration Manager 中 OS 部署的詳細資訊，請參閱[管理 OS 映像](../../osd/get-started/manage-operating-system-images.md)。

