---
title: Microsoft Store 應用程式
titleSuffix: Configuration Manager
description: 使用 Configuration Manager 管理並部署從商務與教育用 Microsoft Store 取得的應用程式。
ms.date: 12/03/2019
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 8cdb22a6-72d7-41f5-9bed-c098b1bcf675
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: b8ba727aff682e3efbba6a91941a5499f9f00e8b
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81689316"
---
# <a name="manage-apps-from-the-microsoft-store-for-business-and-education-with-configuration-manager"></a>使用 Configuration Manager 管理從商務與教育用 Microsoft Store 取得的應用程式

您可利用[商務與教育用 Microsoft Store](https://docs.microsoft.com/microsoft-store/) 為組織尋找並取得 Windows 應用程式。 當您將市集連接到 Configuration Manager 時，接著會同步處理您已取得的應用程式清單。 請在 Configuration Manager 主控台中檢視這些應用程式，並如同部署任何其他應用程式般加以部署。

## <a name="online-and-offline-apps"></a><a name="bkmk_apps"></a> 線上和離線應用程式

商務用與教育用 Microsoft Store 支援兩種應用程式類型：

- **連線**：此授權類型需要使用者和裝置連線到市集，以取得應用程式及其授權。 Windows 10 裝置必須已加入 Azure Active Directory (Azure AD) 或已加入混合式 Azure AD。  

- **離線**：此類型可讓您快取應用程式和授權，以直接部署於內部部署網路內。 裝置不需要連線至市集，或已連線至網際網路。

如需詳細資訊，請參閱[商務與教育用 Microsoft Store 概觀](https://docs.microsoft.com/microsoft-store/microsoft-store-for-business-overview)。

### <a name="summary-of-capabilities"></a>功能摘要

Configuration Manager 同時支援在具有 Configuration Manager 用戶端的 Windows 10 裝置上及在向 Microsoft Intune 註冊的 Windows 10 裝置上，管理商務與教育用 Microsoft Store 應用程式。 Configuration Manager 提供線上和離線應用程式的下列功能：

|功能|離線應用程式|線上應用程式|
|------------|------------|------------|
|將應用程式資料同步處理至 Configuration Manager<br>(每隔 24 小時同步處理一次)|是|是|
|從市集應用程式建立 Configuration Manager 應用程式|是|是|
|支援市集中的免費應用程式|是|是|
|支援市集中的付費應用程式|否|是<sup>[附註 1](#bkmk_note1)</sup>|
|支援使用者或裝置集合的必要部署|是|是|
|支援使用者或裝置集合的可用部署|是|是|
|支援市集中的企業營運應用程式|是|是|
|為裝置<sup>[備註 2](#bkmk_note2)</sup> 上的所有使用者佈建市集應用程式<!--1358310-->|是|是|

#### <a name="note-1-online-licensed-apps-version-requirement"></a><a name="bkmk_note1"></a> 附註 1：線上授權應用程式版本需求

若要使用 Configuration Manager 用戶端將線上授權的應用程式部署到 Windows 10 裝置，必須執行 Windows 10 1703 版或更新版本。  

#### <a name="note-2-configuration-manager-minimum-version"></a><a name="bkmk_note2"></a> 附註 2：Configuration Manager 最低版本

從 1806 版開始。 如需詳細資訊，請參閱[建立 Windows 應用程式](../get-started/creating-windows-applications.md#bkmk_provision)。  

### <a name="deploying-online-apps-using-the-microsoft-store-for-business-and-education-to-devices-that-run-the-configuration-manager-client"></a>使用商務與教育用 Microsoft Store 將線上應用程式部署到執行 Configuration Manager 用戶端的裝置

將商務與教育用 Microsoft Store 應用程式部署到執行完整 Configuration Manager 用戶端的裝置之前，請先考量下列各點：

- 如需完整功能，裝置必須執行 Windows 10 1703 版或更新版本。  

- 將裝置註冊或加入至與您註冊商務用和教育用 Microsoft Store 相同的 Azure AD 租用戶，作為管理工具。  

- 當本機系統管理員帳戶登入裝置時，其並無法存取商務與教育用 Microsoft Store 應用程式。  

- 裝置必須透過即時的網際網路連線到商務與教育用 Microsoft Store。 如需包括 Proxy 設定的詳細資訊，請參閱[必要條件](https://docs.microsoft.com/microsoft-store/prerequisites-microsoft-store-for-business)。  

### <a name="notes-for-devices-running-earlier-versions-of-windows-10"></a>執行舊版 Windows 10 裝置的注意事項

在具有 Configuration Manager 用戶端且執行 Windows 10 1607 版或更早版本的裝置上，適用下列功能：  

當您透過下列其中一種方法，在裝置上強制安裝應用程式時：  

- 使用者安裝應用程式  

- 部署達到其安裝期限

- 所需部署的後續安裝重新評估  

即會發生下列行為：  

- Configuration Manager 用戶端會啟動 Microsoft Store 應用程式來「強制執行」該應用程式  

- 使用者必須從市集完成安裝  

- 在 Configuration Manager 主控台中，應用程式部署狀態回報失敗，錯誤如下：「Microsoft Store 應用程式已在用戶端電腦上開啟，正在等候使用者完成安裝」。  

在下一個應用程式評估週期︰  

- 如果使用者已從市集安裝應用程式，應用程式會報告狀態**成功**  

- 如果使用者未嘗試從市集安裝應用程式：  

  - 對於必要的部署，Configuration Manager 用戶端會嘗試重新啟動市集應用程式  

  - Configuration Manager 不會重新強制執行可用的部署

#### <a name="devices-running-earlier-versions-of-windows-10"></a>執行舊版 Windows 10 的裝置

- 您無法從商務與教育用 Microsoft Store 部署企業營運應用程式

- 當您從市集部署付費應用程式時，使用者必須登入市集並自行取得應用程式  

- 如果您部署可停用存取 Microsoft Store 取用者版本的群組原則，則無法從商務與教育用 Microsoft Store 進行部署。 即使已啟用商務用與教育用 Microsoft Store，仍然會發生這種行為。  

## <a name="set-up-synchronization"></a><a name="bkmk_setup"></a>設定同步處理

當您同步處理貴組織所取得的商務用與教育用 Microsoft Store 清單時，即可在 Configuration Manager 主控台中查看這些應用程式。

將 Configuration Manager 站台連線到 Azure AD 以及商務與教育用 Microsoft Store。 如需此程序的詳細資訊和詳細資料，請參閱[設定 Azure 服務](../../core/servers/deploy/configure/azure-services-wizard.md)。 建立**商務用 Microsoft Store** 服務的連線。

請確定服務連接點和目標裝置可以存取雲端服務。 如需詳細資訊，請參閱[商務用與教育用 Microsoft Store 的必要條件 - Proxy 設定](https://docs.microsoft.com/microsoft-store/prerequisites-microsoft-store-for-business#proxy-configuration) (部分機器翻譯)。

### <a name="supplemental-information-and-configuration"></a><a name="bkmk_config"></a> 補充資訊和設定

在 [Azure 服務精靈] 的 [應用程式]  頁面上，先設定 [Azure 環境]  和 [Web 應用程式]  。 然後，閱讀頁面底部的 [更多資訊]  區段。 這項資訊包含商務與教育用 Microsoft Store 入口網站的下列其他動作：  

- 將 Configuration Manager 設定為市集管理工具。 如需詳細資訊，請參閱[設定管理提供者](https://docs.microsoft.com/microsoft-store/configure-mdm-provider-microsoft-store-for-business)。  

- 啟用離線授權應用程式的支援。 如需詳細資訊，請參閱[發佈離線應用程式](https://docs.microsoft.com/microsoft-store/distribute-offline-apps)。  

- 取得至少一個應用程式。 如需詳細資訊，請參閱[尋找並取得應用程式](https://docs.microsoft.com/microsoft-store/find-and-acquire-apps-overview)。  

在 [Azure 服務精靈] 的 [設定]  頁面上，指定下列資訊：  

- **商務用 Microsoft Store 應用程式內容儲存體的路徑**：指定共用的網路路徑，包括資料夾。 例如 `\\server\share\folder`。 當站台伺服器與市集同步處理時，它會在此位置中快取內容。 當您在 Configuration Manager 中建立應用程式時，站台伺服器會將應用程式內容從這個本機快取複製到站台的內容庫中。  

- **選取的語言**：選取要從市集同步處理，並在軟體中心內向使用者顯示的語言。 比方說，如果使用者設定德文版 Windows，則軟體中心就會為市集應用程式顯示德文字串。 此行為需要同步處理該語言，且特定應用程式有該語言存在。

- **預設語言**：如果未提供使用者的語言，請選取要使用的預設語言。  

## <a name="create-and-deploy-the-app"></a><a name="bkmk_deploy"></a> 建立並部署應用程式

在同步處理之後，建立及部署商務用與教育用 Microsoft Store 應用程式類似於其他任何 Configuration Manager 應用程式。

1. 在 Configuration Manager 主控台的 [軟體程式庫]  工作區中，展開 [應用程式管理]  ，然後選取 [市集應用程式的授權資訊]  節點。  

2. 選擇要部署的應用程式，然後在功能區中選取 [建立應用程式]  。  

站台會隨即建立包含商務與教育用 Microsoft Store 應用程式的 Configuration Manager 應用程式。

然後如同處理任何其他 Configuration Manager 應用程式一樣，部署和監視此應用程式。 如需詳細資訊，請參閱下列文章：  

- [部署應用程式](deploy-applications.md)
- [從主控台監視應用程式](monitor-applications-from-the-console.md)

## <a name="next-steps"></a>後續步驟

在 [軟體程式庫]  工作區中，展開 [應用程式管理]  ，然後選取 [市集應用程式的授權資訊]  節點。

針對您管理的每個市集應用程式，檢視有關應用程式的下列資訊：

- 應用程式名稱
- 應用程式平台
- 您所擁有之應用程式的授權數目
- 可用授權數目

部署線上應用程式之後，該應用程式的任何更新都是直接來自 Microsoft Store。 此外，Configuration Manager 不會檢查線上應用程式的版本相容性，只會檢查 Windows 將應用程式回報為已安裝。  

將離線應用程式部署至具有 Configuration Manager 用戶端的 Windows 10 裝置時，不允許使用者更新 Configuration Manager 部署外部的應用程式。 在多使用者環境 (例如教室) 中，離線應用程式更新的控制特別重要。 停用 Microsoft Store 的其中一個選項是使用[群組原則](https://docs.microsoft.com/windows/configuration/stop-employees-from-using-microsoft-store#block-microsoft-store-using-group-policy)。

商務與教育用 Microsoft Store 系統管理員取得離線應用程式之後，請不要透過市集將應用程式發佈給使用者。 此設定可確保使用者無法線上安裝或更新。 使用者透過 Configuration Manager 只會收到離線應用程式更新。

## <a name="see-also"></a>請參閱

[針對商務用與教育用 Microsoft Store 與 Configuration Manager 的整合進行疑難排解](troubleshoot-microsoft-store-for-business-integration.md)
