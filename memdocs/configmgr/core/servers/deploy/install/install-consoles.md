---
title: 安裝主控台
titleSuffix: Configuration Manager
description: 安裝 Configuration Manager 主控台以連線至管理中心網站或主要站台。
ms.date: 04/04/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: d39c201f-d364-4e7b-bde4-faa76d747f33
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: f5fda03090f7ec69eb78b20385dfc009bac88f40
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81700796"
---
# <a name="install-the-configuration-manager-console"></a>安裝 Configuration Manager 主控台

適用於：  Configuration Manager (最新分支)

系統管理員會使用 Configuration Manager 主控台來管理 Configuration Manager 環境。 每個 Configuration Manager 主控台都可以連線至管理中心網站 (CAS) 或主要站台。 不過，您無法將 Configuration Manager 主控台連線至次要站台。

Configuration Manager 主控台一律安裝在 CAS 的站台伺服器或主要站台上。 若要個別安裝主控台和站台伺服器，請執行獨立安裝程式。  



## <a name="prerequisites"></a>先決條件

- 您具有主控台之目標電腦上的本機**系統管理員**權限。  

- 您具有 Configuration Manager 主控台安裝檔位置的**讀取**權限。  



## <a name="source-paths"></a>來源路徑

決定要使用的來源路徑：  

- 站台伺服器上的 [ConsoleSetup] 資料夾：`<Configuration Manager site server installation path>\Tools\ConsoleSetup`  

    當您安裝站台伺服器時，它會將主控台安裝檔案與站台的支援語言套件複製到 **Tools\ConsoleSetup** 子資料夾。 您也可以選擇將 **ConsoleSetup** 資料夾複製到替代位置，以啟動安裝。 更新站台時，它一律會將其本機版本維持在最新狀態。  

- Configuration Manager 安裝媒體：`<Configuration Manager installation media>\SMSSETUP\BIN\I386`  

    從安裝媒體安裝 Configuration Manager 主控台，一律都會安裝英文版。 即使站台伺服器支援不同的語言，或目標電腦的作業系統設定為不同的語言，還是會發生此行為。  

如果可能，從 [ConsoleSetup]  資料夾而不是從來源媒體啟動主控台安裝程式。

> [!Important]  
> 不要使用 **CD.Latest** 原始程式檔安裝主控台。 這是一個不支援的案例，可能會導致主控台安裝出現問題。 如需詳細資訊，請參閱 [CD.Latest 資料夾](../../manage/the-cd.latest-folder.md#unsupported-scenarios)。<!-- SCCMDocs issue 1359 -->  

如果您建立用於在其他電腦上安裝主控台的套件，請確定該套件包含下列檔案：<!--3612513-->

- ConsoleSetup.exe
- AdminConsole.msi
- ConfigMgr.AC_Extension.i386.cab (從版本 1902 開始)
- ConfigMgr.AC_Extension.amd64.cab (從版本 1902 開始)



## <a name="use-the-setup-wizard"></a>使用安裝精靈  

1. 瀏覽至來源路徑，然後開啟 **ConsoleSetup.exe**。  

    > [!IMPORTANT]  
    > 一律使用 **ConsoleSetup.exe** 來安裝主控台。 雖然您可以執行 AdminConsole.msi 來安裝 Configuration Manager 主控台，但此方法不會執行先決條件或相依性檢查。 安裝可能無法正確安裝。  

2. 在精靈中，選取 [下一步]  。  

3. 在 [站台伺服器]  頁面上，輸入 Configuration Manager 主控台要連線之站台伺服器的完整網域名稱 (FQDN)。  

4. 在 [安裝資料夾]  頁面上，輸入 Configuration Manager 主控台的安裝資料夾。 資料夾路徑結尾不能包含空格，路徑中不可有 Unicode 字元。  

5. 在 [客戶經驗改進計畫]  頁面上，選取是否要加入客戶經驗改進計畫 (CEIP)。  

    > [!Note]  
    > 從 Configuration Manager 1802 版開始，已從產品中移除 CEIP 功能。

6. 在 [安裝準備就緒]  頁面上，按一下 [安裝]  。  



## <a name="install-from-a-command-prompt"></a>從命令提示字元安裝  

> [!TIP]  
> 從命令提示字元安裝 Configuration Manager 主控台，一律都會安裝英文版。 即使目標電腦的作業系統設定為不同的語言，還是會發生此行為。 若要使用英文以外的語言安裝 Configuration Manager 主控台，請[使用安裝精靈](#use-the-setup-wizard)。  


### <a name="consolesetupexe-command-line-options"></a>ConsoleSetup.exe 命令列選項

#### <a name="q"></a>/q

自動安裝 Configuration Manager。 只有在使用此選項時，才需要 **EnableSQM**、 **TargetDir**和 **DefaultSiteServerName** 選項。

#### <a name="uninstall"></a>/uninstall

解除安裝 Configuration Manager 主控台。 搭配 **/q** 選項使用時，請先指定此選項。

#### <a name="langpackdir"></a>LangPackDir

指定包含語言檔案的資料夾路徑。 您可以使用 **安裝程式下載程式** 來下載語言檔案。 如果未使用此選項，則安裝程式會在目前資料夾中尋找語言資料夾。 如果沒有找到語言資料夾，則安裝程式只會繼續安裝英文版。 如需詳細資訊，請參閱[安裝程式下載程式](setup-downloader.md)。

#### <a name="targetdir"></a>TargetDir

指定安裝資料夾以安裝 Configuration Manager 主控台。 只有在使用 **/q** 選項時，才需要此選項。

#### <a name="enablesqm"></a>EnableSQM

指定是否加入客戶經驗改進計畫 (CEIP)。 使用 **1** 的值加入 CEIP，**0** 的值則不加入計畫。 只有在使用 **/q** 選項時，才需要此選項。

> [!Important]  
> 從 Configuration Manager 1802 版開始，已從產品中移除 CEIP 功能。 使用此參數將導致安裝失敗。

#### <a name="defaultsiteservername"></a>DefaultSiteServerName

指定主控台開啟時所連線的網站伺服器 FQDN。 只有在使用 **/q** 選項時，才需要此選項。


### <a name="examples"></a>範例

> [!Important]  
> 針對 1802 版與更新版本，請勿包含 **EnableSQM** 參數

#### <a name="silent-install"></a>無訊息安裝

`ConsoleSetup.exe /q TargetDir="%ProgramFiles%\ConfigMgr Console" DefaultSiteServerName=MyServer.Contoso.com`

#### <a name="silent-install-with-language-packs"></a>含語言套件的無訊息安裝

`ConsoleSetup.exe /q TargetDir="C:\Program Files\ConfigMgr Console" DefaultSiteServerName=MyServer.Contoso.com LangPackDir=C:\Downloads\ConfigMgr`  

#### <a name="silent-uninstall"></a>無訊息解除安裝

`ConsoleSetup.exe /uninstall /q`  



## <a name="see-also"></a>請參閱

系統管理員在主控台中看到的物件，根據指派給其使用者帳戶的權限而定。 如需詳細資訊，請參閱[以角色為基礎的系統管理基本概念](../../../understand/fundamentals-of-role-based-administration.md)。

如需瀏覽 Configuration Manager 主控台之基本概念的詳細資訊，請參閱[使用主控台](../../manage/admin-console.md)。
