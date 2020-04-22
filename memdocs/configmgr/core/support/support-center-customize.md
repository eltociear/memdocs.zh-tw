---
title: 自訂支援中心
titleSuffix: Configuration Manager
description: 自訂支援中心設定檔案。
ms.date: 11/27/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: a6f7f6b7-9ef3-4ffa-a3cf-d877ac55983b
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 1436f40dc989202725d7b83d551d318b970f9b5d
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81707436"
---
# <a name="customize-support-center"></a>自訂支援中心

適用於：  Configuration Manager (最新分支)

[支援中心](support-center.md)工具包含您可以自訂的設定檔。 根據預設，當您安裝支援中心時，這個檔案位於下列路徑：`C:\Program Files (x86)\Configuration Manager Support Center\ConfigMgrSupportCenter.exe.config`。 設定檔會變更程式的行為：

- [自訂資料收集](#bkmk_datacoll)：編輯資料收集期間所包含的登錄機碼和 WMI 命名空間集合  

- [自訂記錄檔群組](#bkmk_loggroups)：使用規則運算式定義新的記錄檔群組。 也將其他記錄檔新增至記錄檔群組。  

- [使用萬用字元收集其他記錄檔](#bkmk_wildcards)：使用萬用字元搜尋以收集其他記錄檔  

若要進行這些變更，您需要已安裝支援中心之用戶端的本機系統管理員權限。 使用文字編輯器或 XML 編輯器，例如 [記事本] 或 Visual Studio 來自訂這些項目。

> [!Important]  
> 支援中心設定檔是 XML 格式的檔案。 對支援中心的作業至為重要。 建議只有熟悉 XML 和規則運算式的使用者才能修改這個檔案。  

請先儲存原始備份，再自訂支援中心設定檔。 如果您在編輯檔案時發生錯誤，此備份可讓您復原原始的支援中心功能。 如果您未建立備份，而支援中心在您修改設定檔後無法正確運作，請重新安裝支援中心。 您也可以複製另一個支援中心安裝的設定檔。



## <a name="customize-data-collection"></a><a name="bkmk_datacoll"></a> 自訂資料收集

您可以使用 `<dataCollectorSettings>` 項目所包含的 XML 元素來修改支援中心設定檔，以在用戶端上自訂資料收集作業。


### <a name="wmi-data-collection"></a>WMI 資料收集

`<CcmWmiDataCollector>` 項目包含 `<collectionScopes>` 項目。 使用此項目來變更支援中心資料收集來源的 WMI 命名空間。 它也包含 `<ignoreScopes>` 項目。 從定義於 `<collectionScopes>` 項目中的命名空間部分，使用此項目篩選出資料集合。  
    
#### <a name="example"></a>範例
預設設定檔會從 `root\ccm` 命名空間收集資料。 它會將此路徑包含在 `<collectionScopes>` 的 `<add/>` 項目中。 

它也會忽略此命名空間 `\cimodels`、`\invagt`、 `\events` 和 `\policy` 路徑下的所有內容。 它會將這些路徑包含在 `<ignoreScopes>` 的 `<add/>` 項目中。

```XML
<CcmWmiDataCollector>
  <collectionScopes>
    <!-- Collect these namespaces (ignoring the sub-scopes in the ignoreScopes block) -->
    <add key="root\ccm"/>
    <add key="root\cimv2\sms"/>
  </collectionScopes>
  <ignoreScopes>
    <!-- Collecting these namespaces is known to be problematic/unnecessary -->
    <add key="root\ccm\cimodels"/>
    <add key="root\ccm\invagt"/>
    <add key="root\ccm\events"/>
    <!-- Do not collect policy, there's already a separate policy collector.-->
    <add key="root\ccm\policy"/>
  </ignoreScopes>
</CcmWmiDataCollector>
```


### <a name="registry-data-collection"></a>登錄資料收集

`<RegistryDataCollector>` 元素包含一個 `<registryKeys>` 元素。 使用此項目變更支援中心在 `HKEY_LOCAL_MACHINE` 路徑下收集的登錄機碼和子機碼。 支援中心不支援從其他根登錄路徑收集登錄資料。

#### <a name="example"></a>範例
若要收集安裝在裝置上的傳統程式登錄機碼，請新增下列 `<registryKeys>` 項目中的 `<add/>` 項目：`<add key="software\\microsoft\\windows\\currentversion\\uninstall"/>`

```XML
<RegistryDataCollector>
  <registryKeys>
    <!-- Registry keys (and all subkeys) to collect -->
    <add key="software\\microsoft\\ccm"/>
    <add key="software\\microsoft\\sms"/>
    <add key="software\\microsoft\\ccmsetup"/>
    <add key="software\\microsoft\\windows\\currentversion\\uninstall"/>
  </registryKeys>
</RegistryDataCollector>
```



## <a name="customize-log-file-groups"></a><a name="bkmk_loggroups"></a> 自訂記錄檔群組

若要自訂支援中心收集的記錄檔，以及如何在**記錄檔群組**清單中呈現它們，請使用 `<logGroups>` 項目中的項目。 當您啟動支援中心時，它會掃描設定檔的這個區段。 然後為在 `<logGroups>` 項目包含之 `<add/>` 項目中找到的每個唯一索引鍵屬性值，在**記錄檔群組**清單上建立群組。

- **元件記錄檔群組**：`<componentLogGroup>` 項目使用索引鍵屬性定義清單中出現的記錄檔群組名稱。 它也會使用包含規則運算式 (regex) 的值屬性。 它會使用這個 regex 收集一組相關的記錄檔。  

- **靜態記錄檔群組：** `<staticLogGroup>` 項目使用索引鍵屬性定義清單中出現的記錄檔群組名稱。 它也會使用定義記錄檔名稱的值屬性。  

如果 `<componentLogGroup>` 項目和 `<staticLogGroup>` 項目內的 `<add/>` 項目使用相同的索引鍵屬性值，則支援中心會建立單一群組。 此群組包含使用相同索引鍵之兩個項目所定義的記錄檔。

#### <a name="example"></a>範例
```XML
<logGroups>
  <componentLogGroup>
    <add key="Application Management" value="^(app.*|ci.*|contentaccess|contenttransfermanager|datatransferservice|dcm.*|execmgr.*|UserAffinity.*|.*Handler$|.*Provider$)"/>
    <add key="Client Registration" value="^(clientregistration|locationservices|ccmmessaging|ccmexec)"/>
    <add key="Inventory" value="^(ccmmessaging|inventoryagent|mtrmgr|swmtrreportgen|virtualapp|mtr.*|filesystemfile)"/>
    <add key="Policy" value="^(ccmmessaging|policyagent_.*|policyevaluator_.*)"/>
    <add key="Software Updates" value="^(ci.*|contentaccess|contenttransfermanager|datatransferservice|dcm.*|update.*|wuahandler|xmlstore|scanagent)"/>
    <add key="Software Distribution" value="^(datatransferservice|execmgr.*|contenttransfermanager|locationservices|contentaccess|filebits)"/>
    <add key="Desired Configuration Management" value="^(ci.*|dcm.*)"/>
    <add key="Operating System Deployment" value="^(ts.*)"/>
  </componentLogGroup>
  <staticLogGroup>
    <add key="Application Management" value="ccmsdkprovider.log"/>
    <add key="Desired Configuration Management" value="ccmsdkprovider.log"/>
    <add key="Software Updates" value="ccmsdkprovider.log"/>
  </staticLogGroup>
</logGroups>
```



## <a name="collecting-additional-log-files-using-wildcards"></a><a name="bkmk_wildcards"></a> 使用萬用字元收集其他記錄檔

若要收集其他記錄檔，請在檔案路徑或檔名中使用萬用字元。 這些萬用字元包含全系統環境變數，例如 `%WINDIR%`，但排除使用者限定範圍的環境變數，例如 `%USERPROFILE%`。 若要使用非遞迴記錄檔搜尋收集其他記錄檔，請在 `<additionalLogFiles>` 元素內使用 `<add/>` 元素。 

這些範例會示範支援中心如何在預設設定檔中使用這項功能。

#### <a name="example-1-collect-all-windows-update-log-files-in-the-windows-directory"></a>範例 1：收集 Windows 目錄中的所有 Windows Update 記錄檔
下列項目會收集在 Windows 目錄中找到之所有名為 `WindowsUpdate.log` 的檔案： 

`<add key="%WINDIR%\WindowsUpdate.log" />`

#### <a name="example-2-collect-all-log-files-in-the-windows-logs-directory"></a>範例 2：收集 Windows Logs 目錄中的所有記錄檔
下列項目會收集在 Windows Logs 目錄中找到之所有結尾為 `.log` 的檔案： 

`<add key="%WINDIR%\logs\*.log" />`

#### <a name="full-example-xml"></a>完整範例 XML
```XML
<CcmLogDataCollector>
  <additionalLogFiles>
    <!-- Collect these additional log files. Can pass in a wildcard for the filename. System variables are also supported. -->
    <!--
    <add key="%WINDIR%\WindowsUpdate.log" />
    <add key="%WINDIR%\logs\*.log" />
    -->
  </additionalLogFiles>
</CcmLogDataCollector>
```
