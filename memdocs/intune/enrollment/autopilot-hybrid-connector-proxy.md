---
title: 設定用於 Intune Connector for Active Directory 的 Proxy 設定
description: 說明如何設定 Intune Connector for Active Directory，來使用現有的內部部署 Proxy 伺服器。
keywords: ''
author: master11218
ms.author: erikje
manager: dougeby
ms.date: 4/16/2019
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: tanvira
ms.suite: ems
search.appverid: ''
ms.custom: ''
ms.collection: M365-identity-device-management
ms.openlocfilehash: 227ed78b593ce10d47b9a1cdcc14dfbd58acdd93
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "79339510"
---
# <a name="work-with-existing-on-premises-proxy-servers"></a>使用現有的內部部署 Proxy 伺服器

本文說明如何設定 Intune Connector for Active Directory，來使用輸出 Proxy 伺服器。 它適用於網路環境具有現有 Proxy 的客戶。

根據預設，Intune Connector for Active Directory 會嘗試使用 Web Proxy 自動探索 (WPAD)，自動在網路上尋找 Proxy 伺服器。 如果已在網路上設定，則可能不需要額外的設定。  如果需要變更，下列各節將描述如何利用 [設定 Proxy 設定的標準 .NET Framework 功能](https://docs.microsoft.com/dotnet/framework/configure-apps/file-schema/network/defaultproxy-element-network-settings)來覆寫預設設定。  該文件中有其他選項的描述。

如需連接器運作方式的詳細資訊，請參閱[了解 Azure AD 應用程式 Proxy 連接器](https://docs.microsoft.com/azure/active-directory/manage-apps/application-proxy-connectors)。

## <a name="completely-bypass-outbound-proxies"></a>完全略過輸出 Proxy

您可以設定連接器以略過內部部署 Proxy，確保它對 Azure 服務使用直接連線。 只要您的網路原則允許，我們會建議使用這種方法，因為這表示您要維護的設定會少一項。

若要停用連接器的輸出 Proxy 使用，請編輯 C:\Program Files\Microsoft Intune\ODJConnector\ODJConnectorUI\ODJConnectorUI.exe.config 檔案，並在此程式碼範例所示的區段中新增 Proxy 位址和 Proxy 連接埠：

```xml
<?xml version="1.0" encoding="utf-8" ?>
<configuration>
    <system.net>  
        <defaultProxy>   
            <defaultProxy enabled="False" /> 
        </defaultProxy>  
    </system.net>
    <runtime>
        <assemblyBinding xmlns="urn:schemas-microsoft-com:asm.v1">
            <dependentAssembly>
                <assemblyIdentity name="mscorlib" publicKeyToken="b77a5c561934e089" culture="neutral"/>
                <bindingRedirect oldVersion="0.0.0.0-2.0.0.0" newVersion="4.6.0.0" />
            </dependentAssembly>
        </assemblyBinding>
    </runtime>
    <startup> 
        <supportedRuntime version="v4.0" sku=".NETFramework,Version=v4.6" />
    </startup>
    <appSettings>
        <add key="SignInURL" value="https://portal.manage.microsoft.com/Home/ClientLogon"/>
        <add key="LocationServiceEndpoint" value="RestUserAuthLocationService/RestUserAuthLocationService/ServiceAddresses"/>
    </appSettings>
</configuration>
```

若要確保連接器更新程式服務也會略過 Proxy，請對 C:\Program Files\Microsoft Intune\ODJConnector\ODJConnectorSvc\ODJConnectorSvc.exe.config 進行類似的變更。

```xml
<?xml version="1.0" encoding="utf-8" ?>
<configuration>
    <system.net>  
        <defaultProxy>
            <defaultProxy enabled="False" /> 
        </defaultProxy>  
    </system.net>
    <startup>
        <supportedRuntime version="v4.0" sku=".NETFramework,Version=v4.6" />
    </startup>
    <appSettings>
        <add key="BaseServiceAddress" value="https://manage.microsoft.com/" />
    </appSettings>
</configuration>
```

請務必複製原始檔案，以防您需要還原為預設的 .config 檔案。

一旦修改設定檔，您必須重新啟動 Intune Connector 服務。 

1. 開啟 **services.msc**。
2. 尋找並選取 [Intune ODJConnector Service]  。
3. 選取 [重新啟動]  。

![重新啟動服務的螢幕擷取畫面](./media/autopilot-hybrid-connector-proxy/service-restart.png)


## <a name="specifying-an-alternative-proxy-server"></a>指定替代 Proxy 伺服器

如果必須搭配 Intune Connector for Active Directory 使用不同的 Proxy 伺服器 (例如略過驗證的伺服器)，則可以使用類似的方式來指定此伺服器。 若要執行這項操作，請編輯 :\Program Files\Microsoft Intune\ODJConnector\ODJConnectorUI\ODJConnectorUI.exe.config 檔案，並在此程式碼範例所示的區段中新增 Proxy 位址和 Proxy 連接埠：

```xml
<?xml version="1.0" encoding="utf-8" ?>
<configuration>
    <system.net>  
        <defaultProxy>   
            <proxy proxyaddress="<PROXY ADDRESS HERE>:<PORT HERE>" bypassonlocal="True" usesystemdefault="True"/>   
        </defaultProxy>  
    </system.net>
    <runtime>
        <assemblyBinding xmlns="urn:schemas-microsoft-com:asm.v1">
            <dependentAssembly>
                <assemblyIdentity name="mscorlib" publicKeyToken="b77a5c561934e089" culture="neutral"/>
                <bindingRedirect oldVersion="0.0.0.0-2.0.0.0" newVersion="4.6.0.0" />
            </dependentAssembly>
        </assemblyBinding>
    </runtime>
    <startup> 
        <supportedRuntime version="v4.0" sku=".NETFramework,Version=v4.6" />
    </startup>
    <appSettings>
        <add key="SignInURL" value="https://portal.manage.microsoft.com/Home/ClientLogon"/>
        <add key="LocationServiceEndpoint" value="RestUserAuthLocationService/RestUserAuthLocationService/ServiceAddresses"/>
    </appSettings>
</configuration>
```

若要確保連接器更新程式服務也會略過 Proxy，請對 C:\Program Files\Microsoft Intune\ODJConnector\ODJConnectorSvc\ODJConnectorSvc.exe.config 進行類似的變更。

```xml
<?xml version="1.0" encoding="utf-8" ?>
<configuration>
    <system.net>  
        <defaultProxy>   
            <proxy proxyaddress="<PROXY ADDRESS HERE>:<PORT HERE>" bypassonlocal="True" usesystemdefault="True"/>   
        </defaultProxy>  
    </system.net>
    <startup>
        <supportedRuntime version="v4.0" sku=".NETFramework,Version=v4.6" />
    </startup>
    <appSettings>
        <add key="BaseServiceAddress" value="https://manage.microsoft.com/" />
    </appSettings>
</configuration>
```

請務必複製原始檔案，以防您需要還原為預設的 .config 檔案。

一旦修改設定檔，您必須重新啟動 Intune Connector 服務。 

1. 開啟 **services.msc**。
2. 尋找並選取 [Intune ODJConnector Service]  。
3. 選取 [重新啟動]  。

![重新啟動服務的螢幕擷取畫面](./media/autopilot-hybrid-connector-proxy/service-restart.png)


## <a name="next-steps"></a>後續步驟

[管理您的裝置](../remote-actions/device-management.md)
