---
title: 外掛程式設定 XML
titleSuffix: Configuration Manager
description: 套件轉換管理員外掛程式 XML 元素的技術參考。
ms.date: 08/24/2018
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 940cc075-4066-44d5-972a-927c0b0a1143
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: ced1cc1347167451d4efb789b40746ff849710ee
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81689076"
---
# <a name="technical-reference-for-the-package-conversion-manager-plug-in-configuration-xml"></a>套件轉換管理員外掛程式設定 XML 的技術參考

適用於：  Configuration Manager (最新分支)

<!--1357861-->

本文說明 Configuration Manager 設定檔 (Microsoft.ConfigurationManagement.exe.config) 中，用於控制套件轉換管理員外掛程式操作的 XML 元素。 如需如何使用此外掛程式的詳細資訊，請參閱[如何使用套件轉換管理員外掛程式](how-to-use-plug-in.md)。



## <a name="xml-configuration-elements"></a>XML 設定元素

下表說明 Configuration Manager 設定檔中，與套件轉換管理員外掛程式相關的 XML 元素。

|元素  |類型  |說明  |
|---------|---------|---------|
|**PcmPlugIn**|字串|用來作為套件轉換管理員外掛程式之指令碼或可執行檔的名稱。|
|**PcmPlugInTimeoutMilliseconds**|整數|等候套件轉換管理員外掛程式指令碼或可執行檔完成套件處理的最長時間，以毫秒為單位。|
|**PcmPluginExitCode**|整數|預期來自外掛程式處理序的結束代碼。 這個值表示成功。 所有其他代碼則視為錯誤。|
|**ForceRequirementsExtraction**|布林值|允許自動轉換以使用與套件相關聯的集合需求。 只有在使用設計目的為決定使用哪些需求的套件轉換管理員外掛程式時，才應將此項設定為 True。|



## <a name="sample-configuration-xml"></a>範例設定 XML

本節提供 Configuration Manager 設定檔 **Microsoft.ConfigurationManagement.exe.config** 中套件轉換管理員設定 XML 元素的範例。根據預設，這個檔案位於下列路徑：  
`C:\Program Files (x86)\Microsoft Configuration Manager\AdminConsole\bin\Microsoft.ConfigurationManagement.exe.config`

在此範例中，與套件轉換管理員相關的元素位於下列元素內：`Microsoft.ConfigurationManagement.UserCentric.Workflow.Properties.Settings`

``` XML
<?xml version="1.0" encoding="utf-8" ?>
<configuration>
...
    </Microsoft.ConfigurationManagement.AdminConsole.Properties.Settings>
    <Microsoft.ConfigurationManagement.UserCentric.Workflow.Properties.Settings>
      <setting name="DecisionVerbosity" serializeAs="String">
        <value>2</value>
      </setting>
      <setting name="PcmPlugIn" serializeAs="String">
        <value>pcmplugin.vbs</value>
      </setting>
      <setting name="PcmPlugInTimeoutMilliseconds" serializeAs="String">
        <value>10000</value>
      </setting>
      <setting name="PcmPluginExitCode" serializeAs="String">
        <value>0</value>
      </setting>
      <setting name="ForceRequirementsExtraction" serializeAs="String">
        <value>True</value >
      </setting>
    </Microsoft.ConfigurationManagement.UserCentric.Workflow.Properties.Settings>
  </applicationSettings>
...
```

