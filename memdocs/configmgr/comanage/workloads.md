---
title: 共同管理工作負載
titleSuffix: Configuration Manager
description: 了解您可以如何將工作負載從 Configuration Manager 切換至 Microsoft Intune。
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 04/15/2020
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-comanage
ms.assetid: 4c90befe-9c4e-4c27-a947-625887e15052
ms.openlocfilehash: 8c91ba1c2b4b5ef7072c030eddd9b97dd69933e5
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2020
ms.locfileid: "82075705"
---
# <a name="co-management-workloads"></a>共同管理工作負載

您不需要切換工作負載，您也可以在準備好時個別切換它們。 Configuration Manager 會繼續管理所有其他工作負載 (包括那些沒有切換到 Intune 的工作負載)，以及共同管理不支援的所有其他 Configuration Manager 功能。

如果您將工作負載切換到 Intune，但之後又改變主意，您可以將它切換回 Configuration Manager。

共同管理支援下列工作負載：

- [合規性原則](#compliance-policies)  

- [Windows Update 原則](#windows-update-policies)  

- [什麼是 Microsoft Intune 裝置設定檔？](#resource-access-policies)  

- [Endpoint Protection](#endpoint-protection)  

- [裝置設定](#device-configuration)  

- [Office 隨選即用應用程式](#office-click-to-run-apps)  

- [用戶端應用程式](#client-apps)  

## <a name="compliance-policies"></a>相容性原則

合規性政策會定義裝置必須符合，才能被條件式存取原則視為符合規範的規則與設定。 也請使用合規性政策，來監視和修復與條件式存取無關的裝置合規性問題。 從 Configuration Manager 1910 版開始，您可以將自訂設定基準的評估新增為合規性政策評定規則。 如需詳細資訊，請參閱[在合規性政策評定中納入自訂設定基準](../compliance/deploy-use/create-configuration-baselines.md#bkmk_CAbaselines)。

如需 Intune 功能的詳細資訊，請參閱[裝置合規性原則](https://docs.microsoft.com/intune/device-compliance-get-started)。  

## <a name="windows-update-policies"></a>Windows Update 原則

商務用 Windows Update 原則可讓您設定 Windows 10 功能更新或品質更新的延遲原則，讓商務用 Windows Update 直接管理 Windows 10 裝置。

如需 Intune 功能的詳細資訊，請參閱[設定商務用 Windows Update 延遲原則](https://docs.microsoft.com/intune/windows-update-for-business-configure)。  

## <a name="resource-access-policies"></a>資源存取原則

資源存取原則會在裝置上設定 VPN、Wi-Fi、電子郵件和憑證設定。

如需 Intune 功能的詳細資訊，請參閱[部署資源存取設定檔](https://docs.microsoft.com/intune/device-profiles)。

> [!Note]  
> 資源存取工作負載也是裝置設定的一部分。 當您切換[裝置設定](#device-configuration)工作負載時，這些原則會由 Intune 管理。

## <a name="endpoint-protection"></a>Endpoint Protection

<!--1357365-->

Endpoint Protection 工作負載包含 Windows Defender 的反惡意程式碼保護功能套件：

- Windows Defender 反惡意程式碼軟體
- Windows Defender 應用程式防護  
- Windows Defender 防火牆  
- Windows Defender SmartScreen  
- Windows 加密
- Windows Defender 惡意探索防護  
- Windows Defender 應用程式控制  
- Windows Defender 資訊安全中心  
- Windows Defender 進階威脅防護 (現在稱為 Microsoft Defender 威脅防護)
- Windows 資訊保護  

如需 Intune 功能的詳細資訊，請參閱 [Microsoft Intune 的 Endpoint Protection](https://docs.microsoft.com/intune/endpoint-protection-windows-10)。

> [!Note]  
> 當您切換此工作負載時，Configuration Manager 原則會保留在裝置上，直到 Intune 原則覆寫它們為止。 此行為可確保裝置在轉換期間仍然具有保護原則。
>
> Endpoint Protection 工作負載也是裝置設定的一部分。 當您切換[裝置設定](#device-configuration)工作負載時，會套用相同的行為。<!-- SCCMDocs.nl-nl issue #4 -->
>
> 屬於 Intune 裝置設定之裝置限制設定檔類型的「Microsoft Defender 防毒軟體」設定並不包含在 Endpoint Protection 滑桿的範圍內。 若要為已啟用 Endpoint Protection 滑桿的共同管理裝置管理「Microsoft Defender 防毒軟體」，請使用 [Microsoft 端點管理員系統管理中心]   > [端點安全性]   > [防毒]  中的新防毒原則。 新原則類型提供新的且已改良的選項，並支援裝置限制設定檔中提供的所有相同設定。 <!--6609171-->
>
> Windows 加密功能包括 BitLocker 管理。 如需有關此功能搭配共同管理之行為的詳細資訊，請參閱[部署 BitLocker 管理](../protect/deploy-use/bitlocker/deploy-management-agent.md#co-management-and-intune)。<!-- SCCMDocs#2321 -->

## <a name="device-configuration"></a>裝置設定

<!--1357903-->

裝置設定工作負載包含可管理組織中裝置的設定。 切換此工作負載也會移動**資源存取**與 **Endpoint Protection** 工作負載。

即使 Intune 是裝置設定授權單位，您仍可以將設定從 Configuration Manager 部署至共同管理的裝置。 這個例外可用來配置您組織所需要但 Intune 目前還沒有的設定。 在 [Configuration Manager 設定基準](../compliance/deploy-use/create-configuration-baselines.md)上，指定這個例外狀況。 啟用該選項以在建立基準時，**即使用是共同管理的用戶端也一律套用此基準**。 您可以稍後在現有基準之屬性的 [一般]  索引標籤上變更它。  

如需 Intune 功能的詳細資訊，請參閱[在 Microsoft Intune 中建立裝置設定檔](https://docs.microsoft.com/intune/device-profile-create)。  

## <a name="office-click-to-run-apps"></a>Office 隨選即用應用程式

<!--1357841-->

此工作負載可管理共同受控裝置上的 Office 365 應用程式。

- 移動工作負載之後，該應用程式會顯示在裝置的**公司入口網站**中  

- 除非重新啟動裝置，否則 Office 更新可能需要約 24 小時的時間才會顯示在用戶端  

- 有一個新的全域條件：**在裝置上是否由 Intune 管理 Office 365 應用程式**。 預設會新增這項條件，作為新的 Office 365 應用程式的需求。 當您轉換此工作負載時，受共同管理的用戶端不符合應用程式的需求。 然後他們不會安裝透過 Configuration Manager 部署的 Office 365。  

如需 Intune 功能的詳細資訊，請參閱[使用 Microsoft Intune 將 Office 365 應用程式指派給 Windows 10 裝置](https://docs.microsoft.com/intune/apps-add-office365)。

## <a name="client-apps"></a>用戶端應用程式

<!--1357892-->

請使用 Intune 來管理 Windows 10 共同受控裝置上的用戶端應用程式和 PowerShell 指令碼。 轉換此工作負載之後，從 Intune 部署的所有可用應用程式均可在公司入口網站中使用。 您從 Configuration Manager 部署的應用程式可在軟體中心使用。

如需 Intune 功能的詳細資訊，請參閱[什麼是 Microsoft Intune 應用程式管理？](https://docs.microsoft.com/intune/app-management)。

> [!Tip]  
> 這項功能最初是以[發行前版本功能](../core/servers/manage/pre-release-features.md)的形式引進 1806 版。 從 2002 版開始，即不再是發行前版本功能。  
>
> 這項功能可能會以**適用於共同受控裝置的行動應用程式**的形式出現在功能清單中。<!-- 5849669 -->

從 1910 版開始，當您在 Configuration Manager 發佈點上啟用 Microsoft 已連線快取時，這些發佈點現在可以將 Microsoft Intune Win32 應用程式提供給共同受控用戶端。 如需詳細資訊，請參閱 [Configuration Manager 中的 Microsoft 連線快取](../core/plan-design/hierarchy/microsoft-connected-cache.md#bkmk_intune)。

## <a name="diagram-for-app-workloads"></a>應用程式工作負載的圖表

![共同管理應用程式工作負載的圖表](media/co-management-apps.svg)

[檢視完整大小的圖表](media/co-management-apps.svg)

## <a name="known-issues"></a>已知問題

當 Endpoint Protection 工作負載移到 Intune 時，用戶端仍可能遵循 Configuration Manager 和 Microsoft Defender 所設定的原則。 <!--5024559-->

若要解決此問題，請使用下方的步驟，在用戶端收到 Intune 原則之後，使用 ConfigSecurityPolicy.exe 來套用 CleanUpPolicy.xml：

1. 將下方文字複製並儲存為 `CleanUpPolicy.xml`。

   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
   <SecurityPolicy xmlns="http://forefront.microsoft.com/FEP/2010/01/PolicyData" Name="FEP clean-up policy"><PolicySection Name="FEP.AmPolicy"><LocalGroupPolicySettings><IgnoreKey Name="SOFTWARE\Policies\Microsoft\Microsoft Antimalware"/><IgnoreKey Name="SOFTWARE\Policies\Microsoft\Windows Defender"/></LocalGroupPolicySettings></PolicySection></SecurityPolicy>
   ```
1. 將已提升權限的命令提示字元開啟至 `ConfigSecurityPolicy.exe`。 此可執行檔通常位於下列其中一個目錄：
   - C:\Program Files\Windows Defender
   - C:\Program Files\Microsoft 安全性用戶端
1. 從命令提示字元，傳入 xml 檔案以清除原則。 例如 `ConfigSecurityPolicy.exe C:\temp\CleanUpPolicy.xml`。  

## <a name="next-steps"></a>後續步驟

[如何切換工作負載](how-to-switch-workloads.md)  
