---
title: 原則實體的參考
titleSuffix: Microsoft Intune
description: Intune 資料倉儲 API 中 [原則] 類別實體集合的參考主題。
keywords: Intune 資料倉儲
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 05/26/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: developer
ms.localizationpriority: medium
ms.technology: ''
ms.reviewer: aanavath
ms.suite: ems
search.appverid: MET150
ms.custom: seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: 55ecb8a5a9071ce24a35943f0b0bae2b4f206212
ms.sourcegitcommit: 118587ddb31ce26b27801839db9b3b59f1177f0f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/29/2020
ms.locfileid: "84165884"
---
# <a name="reference-for-policy-entities"></a>原則實體的參考

[原則]  類別包含的行動裝置實體，可追蹤下列資訊：

- 裝置組態設定檔、應用程式組態設定檔和合規性原則的清查  
- 每日處於成功、擱置、失敗或錯誤狀態的裝置數目  
- 每日處於成功、擱置、失敗或錯誤狀態的使用者數目  
- 處於成功、擱置、失敗或錯誤狀態的累積裝置數目  

## <a name="policies"></a>原則

**policy** 實體列出裝置組態設定檔、應用程式組態設定檔和合規性原則。 您可以將具有行動裝置管理 (MDM) 的原則指派給企業中的群組。

| 屬性  | Description | 範例 |
|---------|------------|--------|
| policyKey |代表資料倉儲中原則的唯一索引鍵。 |123 |
| policyId |資料倉儲中原則的唯一識別碼。 |b66bc706-ffff-7437-0340-032819502773 |
| policyName |原則的名稱。 |"Windows 10 Baseline" |
| policyVersion |原則的版本。 編輯或變更原則時，會建立較新版本。 |1, 2, 3 |
| isDeleted |指出是否已更新 [原則] 記錄。  <br>True - 原則具有含已更新欄位的新記錄。 <br>False - 原則的最新記錄。 |True/False |
| startDateInclusiveUTC |在資料倉儲中建立原則的 UTC 日期和時間。 |11/23/2016 12:00:00 AM |
| deletedDateUTC |IsDeleted 變更為 True 的 UTC 日期和時間。 |11/23/2016 12:00:00 AM |
| rowLastModifiedDateTimeUTC |前次在資料倉儲中修改原則的 UTC 日期和時間。 |11/23/2016 12:00:00 AM |

## <a name="policytypes"></a>policyTypes

**policyType** 實體列出裝置組態設定檔、應用程式組態設定檔和合規性原則的類型。 您可以將具有行動裝置管理 (MDM) 的原則指派給企業中的群組。

| 屬性  | Description | 範例 |
|---------|------------|--------|
| policyTypeId |來源系統中原則的唯一識別碼。 |123 |
| policyTypeKey |資料倉儲中原則的唯一識別碼。 |1 |
| policyTypeName |原則類型的名稱。 |Windows 10 合規性原則。 |

## <a name="device-configuration"></a>裝置設定

**deviceConfigurationProfileDeviceActivity** 實體列出每日處於成功、擱置、失敗或錯誤狀態的**裝置**數目。 此數目會反映指派給實體的裝置組態設定檔。 例如，如果**裝置**的所有其指派原則都處於成功狀態，則會將該天的成功計數器往上加一。 如果裝置獲指派兩個設定檔，一個處於成功狀態，另一個則處於錯誤狀態，該實體會遞增成功計數器，並讓裝置處於錯誤狀態。 實體會列出過去 30 天的特定一天有多少裝置處於哪種狀態。

| 屬性  | Description | 範例 |
|---------|------------|--------|
| dateKey |將裝置組態設定檔簽入記錄在資料倉儲中的日期索引鍵。 |20160703 |
| 擱置 |處於擱置狀態的唯一裝置數目。 |123 |
| 成功 |處於成功狀態的唯一裝置數目。 |12 |
| 錯誤 |處於錯誤狀態的唯一裝置數目。 |10 |
| 操作 |處於失敗狀態的唯一裝置數目。 |2 |

**deviceConfigurationProfileUserActivity** 實體列出每日處於成功、暫止、失敗或錯誤狀態的**使用者**數目。 此數目會反映指派給實體的裝置組態設定檔。 例如，如果**使用者**的所有指派原則都處於成功狀態，則會將該天的成功計數器向上加一。 如果使用者獲指派兩個設定檔，一個處於成功狀態，另一個則處於錯誤狀態，會計算處於錯誤狀態的使用者。  **deviceConfigurationProfileUserActivity** 實體列出過去 30 天內的某一天，有多少使用者處於哪種狀態。

| 屬性  | Description | 範例 |
|---------|------------|--------|
| dateKey |將裝置組態設定檔簽入記錄在資料倉儲中的日期索引鍵。 |20160703 |
| 擱置 |處於擱置狀態的唯一使用者數目。 |123 |
| 成功 |處於成功狀態的唯一使用者數目。 |12 |
| 錯誤 |處於錯誤狀態的唯一使用者數目。 |10 |
| 操作 |處於失敗狀態的唯一使用者數目。 |2 |

## <a name="policytypeactivities"></a>policyTypeActivities

**policyTypeActivity** 實體列出處於成功、擱置、失敗或錯誤狀態的累積裝置數目。 它會列出與每日裝置組態設定檔、應用程式組態設定檔或相容性原則有關的這些狀態。

| 屬性  | Description | 範例 |
|---------|------------|--------|
| dateKey |資料倉儲中記錄裝置組態設定檔簽入的日期索引鍵。 |20160703 |
| policyKey |policyKey，可以與 policy 聯結以取得 policyName。 |Windows 10 基準 |
| policyTypeKey |原則索引鍵類型，可以與 [原則類型] 聯結以取得原則類型名稱。 |Windows 10 合規性原則 |
| 擱置 |處於擱置狀態的唯一裝置數目。 |123 |
| 成功 |處於成功狀態的唯一裝置數目。 |12 |
| 錯誤 |處於錯誤狀態的唯一裝置數目。 |10 |
| 操作 |處於失敗狀態的唯一裝置數目。 |2 |

## <a name="compliance-policy"></a>相容性原則

合規性政策 API 參考包含實體，其提供指派給裝置的合規性政策相關狀態資訊。

### <a name="compliancepolicystatusdeviceactivities"></a>compliancePolicyStatusDeviceActivities

下表摘要了裝置的合規性政策指派狀態。 其列出各合規性狀態下發現的裝置計數。


|屬性     |Description  |範例  |
|---------|---------|---------|
|dateKey  |日期索引鍵，時間點為建立合規性政策的摘要時。|20161204 |
|不明  |離線或因為其他原因而無法與 Intune 或 Azure AD 通訊的裝置數目。 |5|
|notApplicable      |管理員設為目標的裝置合規性政策並不適用的裝置數目。|201 |
|compliant      |一或多項管理員設為目標的裝置合規性政策已成功套用的裝置數目。 |4083 |
|inGracePeriod      |不合規但仍在管理員定義之寬限期內的裝置數目。 |57|
|nonCompliant      |管理員設為目標的裝置合規性政策無法套用，或使用者未予以遵循的裝置數目。|43 |
|錯誤      |無法與 Intune 或 Azure AD 通訊且傳回錯誤訊息的裝置數目。 |3|

### <a name="compliancepolicystatusdeviceperpolicyactivities"></a>compliancePolicyStatusDevicePerPolicyActivities 

下表摘要了裝置的合規性政策指派狀態，以各原則及各原則類型為基礎。 其列出指派的各項合規性政策各個合規性狀態下發現的裝置計數。



|屬性  |Description  |範例  |
|---------|---------|---------|
|dateKey  |日期索引鍵，時間點為建立合規性政策的摘要時。|20161219|
|policyKey     |已建立摘要之合規性政策的索引鍵。 |10178 |
|policyPlatformKey      |已建立摘要之合規性政策平台類型的索引鍵。|5|
|不明     |離線或因為其他原因而無法與 Intune 或 Azure AD 通訊的裝置數目。|13|
|notApplicable     |管理員設為目標的裝置合規性政策並不適用的裝置數目。|3|
|compliant      |一或多項管理員設為目標的裝置合規性政策已成功套用的裝置數目。 |45|
|inGracePeriod      |不合規但仍在管理員定義之寬限期內的裝置數目。 |3|
|nonCompliant      |管理員設為目標的裝置合規性政策無法套用，或使用者未予以遵循的裝置數目。|7|
|錯誤      |無法與 Intune 或 Azure AD 通訊且傳回錯誤訊息的裝置數目。 |3|

### <a name="policyplatformtypes"></a>policyPlatformTypes

下表包含所有受指派原則的平台類型。 從未指派給任何裝置的原則平台類型不會出現在此表格中。


|屬性  |Description  |範例  |
|---------|---------|---------|
|policyPlatformTypeKey      |原則平台類型的唯一索引鍵。 |20170519 |
|policyPlatformTypeId      |原則平台類型的唯一識別碼。|1|
|policyPlatformTypeName      |原則平台類型的名稱。|AndroidForWork |

### <a name="policydeviceactivities"></a>policyDeviceActivities

下表列出每日處於成功、擱置、失敗或錯誤狀態的裝置數目。 該數目反映每個原則類型設定檔的資料。 例如，如果裝置的所有其指派原則都處於成功狀態，則會將該天的成功計數器往上加一。 如果裝置獲指派兩個設定檔，一個處於成功狀態，另一個則處於錯誤狀態，該實體會遞增成功計數器，並讓裝置處於錯誤狀態。 policyDeviceActivity 實體會列出過去 30 天的任何一天內有多少裝置處於哪種狀態。

|屬性  |Description  |範例  |
|---------|---------|---------|
|dateKey|將裝置組態設定檔簽入記錄在資料倉儲中的日期索引鍵。|20160703|
|擱置|處於擱置狀態的唯一裝置數目。|123|
|已成功|處於成功狀態的唯一裝置數目。|12|
|policyKey|policyKey，可以與 policy 聯結以取得 policyName。|Windows 10 基準|
|錯誤|處於錯誤狀態的唯一裝置數目。|10|
|操作|處於失敗狀態的唯一裝置數目。|2|

### <a name="policyuseractivities"></a>policyUserActivities

下表列出每日處於成功、擱置、失敗或錯誤狀態的使用者數目。 該數目反映每個原則類型設定檔的資料。 例如，如果使用者的所有其指派原則都處於成功狀態，則會將該天的成功計數器向上加一。 如果使用者獲指派兩個設定檔，一個處於成功狀態，另一個則處於錯誤狀態，會計算處於錯誤狀態的使用者。 PolicyUserActivity 實體會列出過去 30 天的某一天，有多少使用者處於哪種狀態。


| 屬性  |                                         Description                                         |       範例       |
|-----------|---------------------------------------------------------------------------------------------|---------------------|
|  dateKey  | 將裝置組態設定檔簽入記錄在資料倉儲中的日期索引鍵。 |      20160703       |
|  擱置  |                         處於擱置狀態的唯一裝置數目。                          |         123         |
| 成功 |                         處於成功狀態的唯一裝置數目。                          |         12          |
| policyKey |                 policyKey，可以與 policy 聯結以取得 policyName。                 | Windows 10 基準 |
|   錯誤   |                          處於錯誤狀態的唯一裝置數目。                           |         10          |

