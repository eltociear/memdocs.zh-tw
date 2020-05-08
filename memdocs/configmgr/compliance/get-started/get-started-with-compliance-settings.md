---
title: 開始使用合規性設定
titleSuffix: Configuration Manager
description: 深入了解核心概念與合規性設定的運作方式
ms.date: 03/22/2018
ms.prod: configuration-manager
ms.technology: configmgr-compliance
ms.topic: conceptual
ms.assetid: a2742d52-851e-4abc-b623-d12d91684c0b
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 9143c224082f00b882d3cb557b47b737012393fa
ms.sourcegitcommit: 214fb11771b61008271c6f21e17ef4d45353788f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/07/2020
ms.locfileid: "82906330"
---
# <a name="get-started-with-compliance-settings-in-configuration-manager"></a>開始使用 Configuration Manager 中的相容性設定

適用於：  Configuration Manager (最新分支)

建立 Configuration Manager 合規性設定之前，請先了解核心概念並了解其運作方式。  



## <a name="how-compliance-settings-work"></a>合規性設定的運作方式  
合規性設定讓您管理貴組織中用戶端的設定與合規性。  

組態項目可分為兩種主要類別：  

- **使用 Configuration Manager 用戶端管理的裝置設定** - 通常是您已安裝 Configuration Manager 用戶端軟體的裝置，以便您管理裝置。  

- **不使用 Configuration Manager 用戶端管理的裝置設定** - 通常是使用 Microsoft Intune 或 Configuration Manager 內部部署裝置管理來管理的裝置。  



## <a name="what-devices-are-supported"></a>支援哪些裝置？  

| 裝置類型 | 更多資訊 |  
|------------|----------------------|  
| Windows 電腦 (含 Configuration Manager 用戶端) | 建立自訂設定項目以評估物件，例如登錄機碼、檔案和 Active Directory 屬性。<br /><br /> 當您使用 Windows 10 的設定項目類型時，請從預先定義的清單中選取設定。 |  
| Windows 電腦 (已向內部部署 MDM 註冊) | 從預先定義的清單中選取設定。 |  
| Windows Phone 裝置 (已向內部部署 MDM 註冊) | 從預先定義的清單中選取設定。 |  
| Mac 電腦 (含 Configuration Manager 用戶端) | 建立自訂設定項目以評估物件 (例如 macOS 喜好設定)，以及由指令碼傳回的結果。 |  



## <a name="what-is-a-configuration-item"></a>什麼是設定項目？  
設定項目是儲存特定資訊的容器。 您所設定的資訊取決於設定項目類型。 設定項目可以包含下列資訊：

- **偵測方法資訊**只適用於包含應用程式設定的 Windows 設定項目。 它會偵測是否已安裝某個應用程式。 此偵測使用應用程式的 Windows 安裝程式檔案，或使用自訂指令碼。  

- **設定**代表評估用戶端裝置上合規性的商務或技術條件。 請進行新的設定，或瀏覽至參照電腦上現有的設定。  

- **合規性規則**指定定義設定項目設定的合規性的條件。 在用戶端評估合規性的設定之前，至少必須有一項合規性規則。 某些設定可以補救不符合規範的值。 請建立新的規則，或瀏覽至任何設定項目中現有的設定並選取當中的規則。  

- **支援的平台**是您定義的裝置平台，用戶端會在這些平台上評估設定項目的合規性。 如果您將設定項目部署至不在支援平台清單中的裝置，就不會評估合規性。  



## <a name="what-is-a-configuration-baseline"></a>什麼是組態基準？  
定義設定基準，當中包含要評估的設定項目。 也包含描述所需合規性層級的設定和規則。 從 Configuration Manager 設定套件匯入此設定資料。 Microsoft 和其他廠商會定義這些設定套件。 或者建立新的設定項目和設定基準。  

定義設定基準之後，請將它部署至使用者和裝置集合。 用戶端就會依排程評估合規性的基準設定。 您可以將多個設定基準部署至裝置。 此資料粒度提供更好的合規性控制。 

用戶端裝置會針對每個已部署的組態基準評估其相容性，並立即使用狀況訊息和狀態訊息，將結果報告至站台。 如果裝置目前未與網路連線，但已下載設定基準，它仍然會評估設定項目的合規性。 當裝置重新連線時，就會傳送合規性資訊。  

### <a name="monitoring-configuration-baselines"></a>監視設定基準
- 在 Configuration Manager 主控台的 [監視]  工作區下的 [部署]  節點中，監視合規性評估的結果。 例如：
  - 不符合規範的常見原因
  - 錯誤
  - 受影響的使用者和裝置數目
- 執行有其他詳細資料的合規性設定報告。 例如：
  - 哪些裝置符合規範或不符合規範
  - 設定基準的哪個元素導致電腦不符合規範
- 從執行 Configuration Manager 用戶端的 Windows 電腦檢視合規性評估結果。 開啟 **Configuration Manager** 控制台，切換至 [設定]  索引標籤。  



## <a name="user-data-and-profiles-configuration-items"></a>使用者資料和設定檔組態項目  
使用者資料和設定檔的設定項目所包含的設定可控制執行 Windows 8 和更新版本的電腦上的使用者如何管理：  
- 資料夾重新導向
- 離線檔案
- 漫遊設定檔  

將這些設定項目部署到使用者集合。 從 Configuration Manager 主控台的 [監視]  節點監控其合規性。 不同於其他設定項目，在部署之前，請不要將這些項目加入設定基準。 按一下功能區中的 [部署]  直接部署項目。  

如需詳細資訊，請參閱[建立使用者資料和設定檔設定項目](../deploy-use/create-user-data-and-profiles-configuration-items.md)。  



## <a name="remote-connection-profiles"></a>遠端連線設定檔  
遠端連線設定檔提供一組工具和資源，可協助您建立、部署和監視您遠端連線設定。 藉由將這些設定部署至裝置，可將使用者將電腦連線到公司網路所需的時間縮到最短。  

如需詳細資訊，請參閱[建立遠端連線設定檔](../deploy-use/create-remote-connection-profiles.md)。  



## <a name="windows-edition-upgrade"></a>Windows 版本升級
版本升級原則會將執行特定 Windows 10 版本的裝置自動升級至較新版本。 此原則會提供裝置用來升級的新產品金鑰或授權檔案。

如需詳細資訊，請參閱[使用版本升級原則升級 Windows 裝置](../deploy-use/upgrade-windows-version.md)



## <a name="microsoft-edge-browser-profiles"></a>Microsoft Edge 瀏覽器設定檔
<!-- 1357310 -->
從 1802 版開始，針對在 Windows 10 用戶端上使用 [Microsoft Edge](https://www.microsoft.com/itpro/microsoft-edge) 網頁瀏覽器的客戶，會建立合規性設定原則來設定數個 Microsoft Edge 設定。 

如需詳細資訊，請參閱 [Microsoft Edge 瀏覽器設定檔](../deploy-use/browser-profiles.md)。

