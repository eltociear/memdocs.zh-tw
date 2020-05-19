---
title: 監視共同管理
titleSuffix: Configuration Manager
description: 使用共同管理儀表板來檢閱共同管理裝置的相關資訊。
ms.date: 05/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-comanage
ms.topic: conceptual
ms.assetid: e83a7b0d-b381-4b4a-8eca-850385abbebb
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: e4516ca9baa7398322c204908c25248921a69d25
ms.sourcegitcommit: fddbb6c20cf7e19944944d4f81788adf249c963f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/12/2020
ms.locfileid: "83268057"
---
# <a name="how-to-monitor-co-management-in-configuration-manager"></a>如何在 Configuration Manager 中監視共同管理

適用於：Configuration Manager (最新分支)

啟用共同管理之後，您可以使用下列方法監視共同管理裝置：

- [共同管理儀表板](#co-management-dashboard)  

- [部署原則](#deployment-policies)

- [WMI 裝置資料](#wmi-device-data)

## <a name="co-management-dashboard"></a>共同管理儀表板

從 1802 版開始，檢視具有共同管理相關資訊的儀表板。 該儀表板可協助您檢閱在環境中共同受管理的機器。 圖形有助於識別可能需要注意的裝置。<!--1356648-->

在 Configuration Manager 主控台中，前往 [監視] 工作區，然後選取 [共同管理] 節點。

從 1810 版開始，共同管理儀表板已使用更多詳細資訊予以增強。 <!--1358980-->

![共同管理儀表板的螢幕擷取畫面](media/co-management-dashboard.png)

### <a name="co-managed-devices"></a>共同管理的裝置

*適用於 1802 版和 1806 版*

顯示共同管理裝置在整個環境中的百分比。

![共同管理的裝置圖格](media/co-management-dashboard/Percent-Co-managed-graph.PNG)

### <a name="client-os-distribution"></a>用戶端 OS 發佈

*適用於所有版本* 

顯示依版本的每個 OS 用戶端裝置數目。 會使用下列群組：  

- Windows 7 和 8.x
- 低於 1709 的 Windows 10  
- Windows 10 1709 和更高版本  

    > [!Tip]  
    > Windows 10 1709 版和更新版本是共同管理的必要條件。  

將滑鼠游標移到圖表區段上方可顯示裝置在該 OS 群組中的百分比。

![用戶端 OS 發佈圖格](media/co-management-dashboard/Co-management-OS-distribution-graph.PNG)

### <a name="co-management-status-donut"></a>共同管理狀態 (環圈圖)

*適用於 1802 版和 1806 版*

顯示裝置成功或失敗的細項，其類別如下：

- 成功，已加入混合式 Azure AD
- 成功，已加入 Azure AD  
- 失敗：自動註冊失敗  

將滑鼠游標移到圖表區段上方可顯示裝置在該類別中的百分比。

![共同管理狀態 (環圈圖) 圖格](media/co-management-dashboard/Co-management-status-graph.PNG)

選取圖形區段以檢視該類別的裝置清單。

![註冊失敗的裝置清單](media/co-management-dashboard/Enrollment-Failure_Device-List.PNG)

### <a name="co-management-status-funnel"></a>共同管理狀態 (漏斗圖)

*適用於 1810 版和更新版本*

顯示在註冊程序中具有下列狀態之裝置數目的漏斗圖：
  
- 合格裝置
- 已排程  
- 已起始註冊  
- 已註冊  

![共同管理狀態 (漏斗圖) 磚](media/co-management-dashboard/1358980-status-funnel.png)

### <a name="co-management-enrollment-status"></a>共同管理註冊狀態

*適用於 1810 版和更新版本*

顯示裝置狀態的細項，其類別如下：

- 成功，混合式 Azure AD 聯結  
- 成功，Azure AD 聯結  
- 正在註冊，混合式 Azure AD 聯結  
- 失敗，混合式 Azure AD 聯結  
- 失敗，Azure AD 聯結  
- 暫止的使用者登入  

    > [!Note]  
    > 從 1906 版開始，若要降低處於此擱置狀態的裝置數目，新的共同管理裝置現在會根據其 Azure AD「裝置」權杖自動註冊到 Microsoft Intune 服務。 不需要等待使用者登入裝置以啟動自動註冊。 若要支援此行為，裝置需要執行 Windows 10 1803 版或更新版本。
    >
    > 如果裝置權杖失敗，則會透過使用者權杖回復為先前的行為。 請查看 **ComanagementHandler.log** 以取得下列項目的資訊：`Enrolling device with RegisterDeviceWithManagementUsingAADDeviceCredentials`

在磚中選取狀態，以鑽研至處於該狀態的裝置清單。  

![共同管理註冊狀態磚](media/co-management-dashboard/1358980-enrollment-status.png)


### <a name="workload-transition"></a>工作負載轉換

*適用於所有版本*

顯示的橫條圖，是您針對可用工作負載轉換到 Microsoft Intune 的裝置數目。

工作負載清單會依 Configuration Manager 版本而異。 如需詳細資訊，請參閱[可轉換至 Intune 的工作負載](workloads.md)。

將滑鼠游標移到圖表區段上方，顯示針對該工作負載轉換的裝置數目。 

![工作負載轉換橫條圖](media/co-management-dashboard/Workload-Transition.PNG)


### <a name="enrollment-errors"></a>註冊錯誤

*適用於 1810 版和更新版本*

此表格是來自裝置的註冊錯誤清單。 這些錯誤可能來自 Windows、核心 Windows OS 或 Configuration Manager 用戶端中的 MDM 元件。

有數百個可能的錯誤。 下表列出最常見的錯誤。
<!-- SCCMDocs issue 1064, BUG 3158555 -->

| 錯誤 | 說明 |
|---------|---------|
| 2147549183 (0x8000FFFF) | MDM 註冊尚未在 Azure AD 中設定，或者註冊 URL 不是預期的 URL。<br><br>[啟用 Windows 10 自動註冊](https://docs.microsoft.com/intune/windows-enroll#enable-windows-10-automatic-enrollment) |
| 2149056536 (0x80180018)<br>MENROLL_E_USERLICENSE | 使用者的授權處於封鎖註冊的錯誤狀態<br><br>[將授權指派給使用者](https://docs.microsoft.com/intune/licenses-assign) |
| 2149056555 (0x8018002B)<br>MENROLL_E_MDM_NOT_CONFIGURED | 嘗試向 Intune 自動註冊，但不會完整套用 Azure AD 設定時。 此問題應該是暫時性的，因為裝置會在短時間後重試。 |
| 2149056554 (0x‭8018002A‬)<br>&nbsp; | 使用者已取消作業<br><br>如果 MDM 註冊需要多重要素驗證，而且使用者尚未使用支援的第二個要素登入，Windows 就會向使用者顯示快顯通知以進行註冊。 如果使用者未回應快顯通知，就會發生此錯誤。 此問題應該是暫時性的，因為 Configuration Manager 將重試並提示使用者。 使用者應該在登入 Windows 時使用多重要素驗證。 此外，也會教育他們要預期此行為，並在出現提示時採取動作。 | 
| 2149056533 (0x80180015)<br>MENROLL_E_NOTSUPPORTED | 通常不支援行動裝置管理 | 
| 2149056514 (0x80180002)<br>MENROLL_E_DEVICE_AUTHENTICATION_ERROR | 伺服器無法驗證使用者<br><br> 沒有任何適用於使用者的 Azure AD 權杖。 確定使用者可向 Azure AD 進行驗證。 |
| 2147942450 (0x‭80070032‬)<br>&nbsp; | 僅 Windows RS3 和更新版本支援 MDM 自動註冊。<br><br>確定該裝置符合共同管理的[最低需求](overview.md#windows-10)。 |
| 3400073293 | ADAL 使用者領域帳戶回應未知<br><br>檢查您的 Azure AD 設定，並確定使用者可以成功驗證。 | 
| 3399548929 | 需要使用者登入<br><br>此問題應該是暫時性的。 當使用者在註冊工作發生前快速登出時，就會發生此問題。 | 
| 3400073236 | ADAL 安全性權杖要求失敗。<br><br>檢查您的 Azure AD 設定，並確定使用者可以成功驗證。 |
| 2149122477 | 一般 HTTP 問題 |
| 3400073247 | 僅同盟流程支援 ADAL 整合式 Windows 驗證<br><br>[規劃混合式 Azure Active Directory 加入實作](https://docs.microsoft.com/azure/active-directory/devices/hybrid-azuread-join-plan) \(機器翻譯\) | 
| 3399942148 | 找不到伺服器或 Proxy。<br><br>當用戶端無法與雲端通訊時，此問題應該是暫時性的。 如果持續發生，請確定用戶端與 Azure 具有一致的連線。 | 
| 2149056532 | 不支援特定平台或版本<br><br>確定該裝置符合共同管理的[最低需求](overview.md#windows-10)。 |
| 2147943568 | 找不到元素<br><br>此問題應該是暫時性的。 如果持續發生，請連絡 Microsoft 支援服務。 |
| 2192179208 | 沒有足夠的記憶體資源可用來處理此命令。<br><br>此問題應該是暫時性的，它應該會在用戶端重試時自行解決。 |
| 3399614467 | 此判斷提示的 ADAL 授權授與失敗<br><br>檢查您的 Azure AD 設定，並確定使用者可以成功驗證。 |
| 2149056517 | 來自管理伺服器的一般失敗，例如 DB 存取錯誤<br><br>此問題應該是暫時性的。 如果持續發生，請連絡 Microsoft 支援服務。 |
| 2149134055 | Winhttp 名稱無法解析<br><br>用戶端無法解析服務的名稱。 請檢查 DNS 設定。 | 
| 2149134050 | 網際網路逾時<br><br>當用戶端無法與雲端通訊時，此問題應該是暫時性的。 如果持續發生，請確定用戶端與 Azure 具有一致的連線。 |

如需詳細資訊，請參閱 [MDM 註冊錯誤值](https://docs.microsoft.com/windows/desktop/mdmreg/mdm-registration-constants) \(英文\)。

## <a name="deployment-policies"></a>部署原則

[監視] 工作區的 [部署] 節點中會建立兩個原則。 一個用於試驗群組，另一個用於生產。 這些原則只會報告 Configuration Manager 已套用原則的裝置數目。 它們不會考慮在 Intune 中註冊了多少部裝置，這是共同受控裝置的需求。  

生產原則 (CoMgmtSettingsProd) 會以 [所有系統] 集合為目標。 它具有能檢查 OS 類型和版本的適用性條件。 如果用戶端是伺服器 OS 或非 Windows 10，系統將不會套用該原則，且不會採取任何動作。

## <a name="wmi-device-data"></a>WMI 裝置資料

在站台伺服器上的 **ROOT\SMS\site_&lt;SITECODE>** 命名空間中，查詢 **SMS_Client_ComanagementState** WMI 類別。 您可以在 Configuration Manager 中建立自訂集合，以協助判斷共同管理部署的狀態。 如需建立自訂集合的詳細資訊，請參閱[如何建立集合](../core/clients/manage/collections/create-collections.md)。

WMI 類別中的可用欄位如下：  

- **MachineId**：Configuration Manager 用戶端的唯一裝置識別碼  

- **MDMEnrolled**：指定裝置是否為 MDM 註冊  

- **Authority**：註冊裝置的授權單位  

- **ComgmtPolicyPresent**：指定用戶端上是否有 Configuration Manager 共同管理原則。 如果 **MDMEnrolled** 值是 **0**，則裝置不受共同管理，無論用戶端上是否有共同管理原則。  

當 [MDMEnrolled] 欄位和 [ComgmtPolicyPresent] 欄位的值都是 **1** 時，裝置受共用管理。  
