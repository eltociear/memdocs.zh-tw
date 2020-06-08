---
title: Intune 端點安全性防火牆設定 | Microsoft Docs
description: Microsoft Intune 中適用於 Windows 和 macOS 的端點安全性防火牆原則設定
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 05/15/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.reviewer: mattsha
ms.openlocfilehash: d90870a60ea292939926816bb74b5d285dc6a09f
ms.sourcegitcommit: 48005a260bcb2b97d7fe75809c4bf1552318f50a
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/15/2020
ms.locfileid: "83431601"
---
# <a name="firewall-policy-settings-for-endpoint-security-in-intune"></a>Intune 中的端點安全性防火牆原則設定

檢視在 Intune [端點安全性] 節點的[端點安全性原則](../protect/endpoint-security-policy.md)中，您可以在 [防火牆] 原則設定檔內進行的設定。

支援的平台和設定檔：

- **macOS**：
  - 設定檔：**macOS 防火牆**

- **Windows 10 及更新版本**：
  - 設定檔：**Microsoft Defender 防火牆**

## <a name="macos-firewall-profile"></a>macOS 防火牆設定檔

### <a name="firewall"></a>防火牆

下列設定會設為 [macOS 防火牆的端點安全性原則](../protect/endpoint-security-firewall-policy.md)

- [啟用防火牆]

  - [未設定] (預設)
  - [是] - 啟用防火牆。
  
  若設為 [是]，您可以進行下列設定。  

  - [封鎖所有連入連線]

    - [未設定] (預設)
    - [是] - 除了基本網際網路服務所需的連線 (例如 DHCP、Bonjour 及 IPSec) 之外，封鎖所有連入連線。 這會封鎖所有的共用服務。

  - [啟用隱形模式]

    - [未設定] (預設)
    - [是] - 防止電腦回應探查要求。 電腦仍然會回應已授權應用程式的連入要求。

  - [防火牆應用程式]：展開下拉式清單，選取 [新增]，然後為應用程式的連入連線指定應用程式和規則。
    - [允許連入連線]
      - 尚未設定
      - 封鎖
      - 允許

    - [套件組合識別碼] - 識別碼可用來識別應用程式。 例如：*com.apple.app*

## <a name="microsoft-defender-firewall-profile"></a>Microsoft Defender 防火牆設定檔

### <a name="microsoft-defender-firewall"></a>Microsoft Defender 防火牆

下列設定會設為 [Windows 10 防火牆的端點安全性原則](../protect/endpoint-security-firewall-policy.md)。

- **停用具狀態檔案傳輸通訊協定 (FTP)**  
  CSP：[MdmStore/Global/DisableStatefulFtp](https://go.microsoft.com/fwlink/?linkid=872536)

  - [未設定] (預設) - 防火牆會使用 FTP 來檢查及篩選次要網路連線，但可能會因此而略過防火牆規則。
  - **是**
  
- **刪除安全性關聯前的閒置秒數**  
  CSP：[MdmStore/Global/SaIdleTime](https://go.microsoft.com/fwlink/?linkid=872539)

  指定保留安全性關聯的時間長度 (300 到 3600 秒之間)，之後將不會再看到網路流量。
  
  如果您未指定任何值，則系統會在閒置 300 秒後刪除安全性關聯。
  
- **預先共用金鑰編碼**  
  CSP：[MdmStore/Global/PresharedKeyEncoding](https://go.microsoft.com/fwlink/?linkid=872541)

  若不需要 *UTF-8*，則預先共用金鑰一開始會使用 UTF-8 編碼。 在此之後，裝置使用者可以選擇其他編碼方法。

  - [未設定] (預設)
  - **無**
  - [UTF8]

- [防火牆 IP sec 豁免允許芳鄰探索]  
  CSP：[MdmStore/Global/IPsecExempt](https://go.microsoft.com/fwlink/?linkid=872547)

  - [未設定] (預設)
  - [是] - 防火牆 IPsec 豁免允許芳鄰探索。

- [防火牆 IP sec 豁免允許 ICMP]  
  CSP：[MdmStore/Global/IPsecExempt](https://go.microsoft.com/fwlink/?linkid=872547)

  - [未設定] (預設)
  - [是] - 防火牆 IPsec 豁免允許 ICMP。

- [防火牆 IP sec 豁免允許路由器探索]  
  CSP：[MdmStore/Global/IPsecExempt](https://go.microsoft.com/fwlink/?linkid=872547)

  - [未設定] (預設)
  - [是] - 防火牆 IPsec 豁免允許路由器探索。

- [防火牆 IP sec 豁免允許 DHCP]  
  CSP：[MdmStore/Global/IPsecExempt](https://go.microsoft.com/fwlink/?linkid=872547)

  - [未設定] (預設)
  - [是] - 防火牆 IP sec 豁免允許 DHCP

- **憑證撤銷清單 (CRL) 驗證**  
  CSP：[MdmStore/Global/CRLcheck](https://go.microsoft.com/fwlink/?linkid=872548)

   指定憑證撤銷清單 (CRL) 驗證的強制執行方式。
  - [未設定] (預設) - 用戶端預設為停用 CRL 驗證。
  - **無**
  - **嘗試**
  - **需要**

- [要求金鑰處理模組只忽略其不支援的驗證套件]  
  CSP：[MdmStore/Global/OpportunisticallyMatchAuthSetPerKM](https://go.microsoft.com/fwlink/?linkid=872550)

  - [未設定] (預設)
  - [是] - 金鑰處理模組會忽略不支援的驗證套件。

- **封包佇列**  
  CSP：[MdmStore/Global/EnablePacketQueue](https://go.microsoft.com/fwlink/?linkid=872551)

  指定如何啟用接收端軟體的規模調整，處理 IPsec 通道閘道案例中加密的接收和純文字轉送。 這可確定保留封包順序。
  - [未設定] (預設) - 封包佇列會恢復用戶端預設，也就是停用。
  - **停用**
  - **輸入佇列**
  - **輸出佇列**
  - **將兩者放入佇列**

- [開啟網域網路的 Microsoft Defender 防火牆]  
  CSP：[EnableFirewall](https://go.microsoft.com/fwlink/?linkid=872558)

  - [未設定] (預設) - 用戶端會恢復預設，也就是啟用防火牆。
  - [是] - **網域**網路類型的 Microsoft Defender 防火牆已開啟並施行。
  - [否] - 停用防火牆。

- [開啟私人網路的 Microsoft Defender 防火牆]  
  CSP：[EnableFirewall](https://go.microsoft.com/fwlink/?linkid=872558)

  - [未設定] (預設) - 用戶端會恢復預設，也就是啟用防火牆。
  - [是] - **私人**網路類型的 Microsoft Defender 防火牆已開啟並施行。
  - [否] - 停用防火牆。

- [開啟公用網路的 Microsoft Defender 防火牆]  
  CSP：[EnableFirewall](https://go.microsoft.com/fwlink/?linkid=872558)

  - [未設定] (預設) - 用戶端會恢復預設，也就是啟用防火牆。
  - [是] - **公用**網路類型的 Microsoft Defender 防火牆已開啟並施行。
  - [否] - 停用防火牆。

<!-- Microsoft Defender Firewall rules added in 2005  -->

### <a name="microsoft-defender-firewall-rules"></a>Microsoft Defender 防火牆規則

此設定檔處於預覽階段。

下列設定會設為 [Windows 10 防火牆的端點安全性原則](../protect/endpoint-security-firewall-policy.md)。

#### <a name="windows-firewall-rule"></a>Windows 防火牆規則

- **Name**  
  為您的規則指定易記名稱。 這個名稱會出現在規則清單中，以協助您識別。

- **描述**  
  提供規則的描述。

- [方向]  
  - [未設定] (預設) - 此規則預設為輸出流量。
  - [輸出] - 此規則會套用至輸出流量。
  - [輸入] - 此規則會套用至輸入流量。

- **動作**  
  - [未設定] (預設) - 此規則預設為允許流量。
  - **封鎖** - 依照您設定的「方向」封鎖流量。
  - **允許** - 依照您設定的「方向」允許流量。

- **網路類型**  
  指定規則所屬的網路類型。 您可以選擇下列一或多個項目。 如果您未選取任何選項，規則會套用至所有網路類型。
  - **網域**
  - **私人**
  - **公用**
  - **未設定**

- **套件系列名稱**  
  [Get-AppxPackage](https://docs.microsoft.com/previous-versions//hh856044(v=technet.10))

  可以透過從 PowerShell 執行 Get-AppxPackage 命令，以擷取套件系列名稱。

- **檔案路徑**  
  CSP：[FirewallRules/FirewallRuleName/App/FilePath](https://docs.microsoft.com/windows/client-management/mdm/firewall-csp#filepath)

  若要指定應用程式的檔案路徑，請輸入用戶端裝置上的應用程式位置。 例如：`C:\Windows\System\Notepad.exe` 或 `%WINDIR%\Notepad.exe`

- **服務名稱**  
  [FirewallRules/FirewallRuleName/App/ServiceName](https://docs.microsoft.com/windows/client-management/mdm/firewall-csp#servicename)

  當服務 (而不是應用程式) 正在傳送或接收流量時，使用 Windows 服務的簡短名稱。 您可以從 PowerShell 執行 `Get-Service` 命令來擷取服務的簡短名稱。

- **通訊協定**  
  CSP：[FirewallRules/FirewallRuleName/Protocol](https://docs.microsoft.com/windows/client-management/mdm/firewall-csp#protocol)

  指定此連接埠規則的通訊協定。
  - 傳輸層通訊協定 (例如 *TCP (6)*  和 *UDP (17)* ) 可讓您指定連接埠或連接埠範圍。
  - 針對自訂通訊協定，輸入 *0* 和 *255* 之間的數字表示 IP 通訊協定。
  - 若未指定任何內容，規則會預設為「任何」。

- **介面類型**  
  指定規則所屬的介面類型。 您可以選擇下列一或多個項目。 如果您未選取任何選項，規則會套用至所有介面類型：
  - **遠端存取**
  - **無線**
  - **區域網路**
  - **未設定**

- **授權的使用者**  
  [FirewallRules/FirewallRuleName/LocalUserAuthorizationList](https://docs.microsoft.com/windows/client-management/mdm/firewall-csp#localuserauthorizedlist)

  為此規則指定已授權的本機使用者清單。 如果此原則中的「服務名稱」設為 Windows 服務，則無法指定已授權的使用者清單。 如果未指定授權的使用者，則預設值為「所有使用者」。

- **任何本機位址**  
  **未設定** (預設) - 使用下列設定，「本機位址範圍」* 來設定要支援的位址範圍。
  - **是** - 支援任何本機位址，並且不設定位址範圍。

- **本機位址範圍**  
  CSP：[FirewallRules/FirewallRuleName/LocalAddressRanges](https://docs.microsoft.com/windows/client-management/mdm/firewall-csp#localaddressranges)  

  將一或多個位址新增為規則涵蓋的本機位址清單 (以逗號分隔)。 有效項目 (權杖) 包含下列選項：
  - **星號** - 星號 (\*) 表示任何本機位址。 如果有的話，星號必須是唯一包含在內的權杖。
  - **子網路** - 使用子網路遮罩或網路首碼表示法來指定子網路。 如果未指定子網路遮罩或網路首碼，則子網路遮罩預設會是 255.255.255.255。
  - **有效的 IPv6 位址**
  - **IPv4 位址範圍** - IPv4 範圍的格式必須為「起始位址 - 結束位址」(不包含空格)，其中起始位址小於結束位址。
  - **IPv6 位址範圍** - IPv6 範圍的格式必須為「起始位址 - 結束位址」(不包含空格)，其中起始位址小於結束位址。

  若未指定任何值，則此設定預設會使用「任何位址」。

- **任何遠端位址**  
  **未設定** (預設) - 使用下列設定，「遠端位址範圍」* 來設定要支援的位址範圍。
  - **是** - 支援任何遠端位址，並且不設定位址範圍。

- **遠端位址範圍**  
  CSP：[FirewallRules/FirewallRuleName/RemoteAddressRanges](https://docs.microsoft.com/windows/client-management/mdm/firewall-csp#remoteaddressranges)  

  將一或多個位址新增為規則涵蓋的遠端位址清單 (以逗號分隔)。 有效項目 (權杖) 包含下列項目，不區分大小寫：
  - **星號** - 星號 (\*) 表示任何遠端位址。 如果有的話，星號必須是唯一包含在內的權杖。
  - **Defaultgateway**
  - **DHCP**
  - **DNS**
  - **WINS**
  - **Intranet** - 在執行 Windows 1809 或更新版本的裝置上支援。
  - **RmtIntranet** - 在執行 Windows 1809 或更新版本的裝置上支援。
  - **Ply2Renders** - 在執行 Windows 1809 或更新版本的裝置上支援。
  - **LocalSubnet** - 表示本機子網路上的任何本機位址。
  - **子網路** - 使用子網路遮罩或網路首碼表示法來指定子網路。 如果未指定子網路遮罩或網路首碼，則子網路遮罩預設會是 255.255.255.255。
  - **有效的 IPv6 位址**
  - **IPv4 位址範圍** - IPv4 範圍的格式必須為「起始位址 - 結束位址」(不包含空格)，其中起始位址小於結束位址。
  - **IPv6 位址範圍** - IPv6 範圍的格式必須為「起始位址 - 結束位址」(不包含空格)，其中起始位址小於結束位址。

  若未指定任何值，則此設定預設會使用「任何位址」。

<!-- End of 2005 additions  -->

## <a name="next-steps"></a>後續步驟

[防火牆端點安全性原則](../protect/endpoint-security-firewall-policy.md)
