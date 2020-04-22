---
title: 狀況訊息
titleSuffix: Configuration Manager
description: 支援的 Configuration Manager 版本中的狀況訊息描述。
ms.date: 03/21/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: f04c0a71-57bc-4443-a47c-592373050d04
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: fe173e37d888dfe594ad8953ff5d7167d43a2981
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81704586"
---
# <a name="state-messages-in-configuration-manager"></a>Configuration Manager 中的狀況訊息 

適用於：  Configuration Manager (最新分支)

狀況訊息包含 Configuration Manager 用戶端上狀況的精確資訊。 Configuration Manager 的特定元件 (如軟體更新和組態設定) 會使用狀況訊息系統。

Configuration Manager 用戶端會傳送狀況訊息至後援狀態點或管理點站台系統，以報告作業的目前狀態。 您可以建立報表來檢視 Configuration Manager 用戶端所傳送的狀況訊息。

每個使用狀況訊息的 Configuration Manager 功能，都可藉由狀況訊息的主題類型來識別。 此文章中所列的狀況訊息主題類型可用來定義與狀況訊息相關的 Configuration Manager 功能。

> [!NOTE]  
> 狀況訊息識別碼為零 (0) 通常表示主題類型處於未知狀態。

## <a name="300-state_topictype_sum_assignment_compliance"></a>300 STATE_TOPICTYPE_SUM_ASSIGNMENT_COMPLIANCE

|      狀況訊息識別碼     |  狀況訊息描述 |
|:-------------|:------|
| 0 | 合規性狀態未知|
| 1 | 符合標準 | 
| 2 | 不相容 | 

## <a name="301-state_topictype_sum_assignment_enforcement"></a>301 STATE_TOPICTYPE_SUM_ASSIGNMENT_ENFORCEMENT

|       狀況訊息識別碼     |  狀況訊息描述 |
|:-------------|:------|
| 0  | 強制狀態未知 |
| 1  | 正在安裝更新        | 
| 2  | 正在等候重新啟動          | 
| 3  | 正在等候其他安裝完成         | 
| 4  | 已順利安裝更新          | 
| 5  | 系統重新啟動擱置中         | 
| 6  | 無法安裝更新         | 
| 7  | 正在下載更新   | 
| 8  | 已下載更新    | 
| 9  | 無法下載更新     | 
| 10 | 正在等候安裝前的維護期間         | 
| 11 | 正在等候協調         | 

## <a name="302-state_topictype_sum_assignment_evaluation"></a>302 STATE_TOPICTYPE_SUM_ASSIGNMENT_EVALUATION

|     狀況訊息識別碼     |  狀況訊息描述 |
|:-------------|:------|      
| 0 | 評估狀態未知|                 
| 1 |評估已啟用      |
| 2 |評估成功      |
| 3 |評估失敗      |


## <a name="400-state_topictype_sum_ci_detection"></a>400 STATE_TOPICTYPE_SUM_CI_DETECTION

|     狀況訊息識別碼     |  狀況訊息描述 |
|:-------------|:------|
| 0 | 偵測狀態未知|
| 1 | 不需要   |
| 2 | 未偵測到    |
| 3 | 偵測到   |

## <a name="401-state_topictype_sum_ci_compliance"></a>401 STATE_TOPICTYPE_SUM_CI_COMPLIANCE

|     狀況訊息識別碼     |  狀況訊息描述 |
|:-------------|:------|
| 0 | 合規性狀態未知|
| 1 |符合標準     |
| 2 |不相容     |
| 3 |偵測到衝突    |
| 4 |錯誤      |
| 5 |Unknown     |
| 6 |部分合規性   |
| 7 |未設定合規性    |

## <a name="402-state_topictype_sum_ci_enforcement"></a>402 STATE_TOPICTYPE_SUM_CI_ENFORCEMENT

|     狀況訊息識別碼     |  狀況訊息描述 |
|:-------------|:------|
| 0  | 強制狀態未知|
| 1  |強制已啟動          |
| 2  |強制正在等候內容         |
| 3  | 正在等候其他安裝完成        |
| 4  |正在等候安裝前的維護期間         |
| 5  |安裝前需要重新啟動         |
| 6  |一般性故障        |
| 7  |擱置安裝         |
| 8  |正在安裝更新          |
| 9  |系統重新啟動擱置中        |
| 10 |已順利安裝更新         |
| 11 |無法安裝更新        |
| 12 |正在下載更新        |
| 13 | 已下載更新        |
| 14 |無法下載更新        |

## <a name="500-state_topictype_sum_update_detection"></a>500 STATE_TOPICTYPE_SUM_UPDATE_DETECTION

|     狀況訊息識別碼     |  狀況訊息描述 |
|:-------------|:------|
|0 |偵測狀態未知|
| 1 | 不需要更新  |
| 2 | 需要更新   |
| 3 | 已安裝更新  |

## <a name="501-state_topictype_sum_update_source_scan"></a>501 STATE_TOPICTYPE_SUM_UPDATE_SOURCE_SCAN

|     狀況訊息識別碼     |  狀況訊息描述 |
|:-------------|:------|
| 0 |掃描狀態未知|
| 1 | 掃描正在等待內容   |
| 2 | 掃描正在執行    |
| 3 | 掃描完成    |
| 4 | 掃描重試擱置中   |
| 5 | 掃描失敗   |
| 6 | 掃描完成但有錯誤 |

## <a name="700-state_topictype_resync_state_msg"></a>700 STATE_TOPICTYPE_RESYNC_STATE_MSG

無狀態識別碼。

## <a name="701-state_topictype_system_heartbeat"></a>701 STATE_TOPICTYPE_SYSTEM_HEARTBEAT

無狀態識別碼。

## <a name="702-state_topictype_ckd_update"></a>702 STATE_TOPICTYPE_CKD_UPDATE
 
無狀態識別碼。

## <a name="800-state_topictype_client_deployment"></a>800 STATE_TOPICTYPE_CLIENT_DEPLOYMENT

|     狀況訊息識別碼     |  狀況訊息描述 |
|:-------------|:------|
| 100 |已啟動用戶端部署      |       
| 101 |正在等待下載       |       
| 102 |部署已排程       |       
| 103 | 正在等候部署前的期間 |
| 104 |已跳過部署       |       
| 301 |未知的用戶端部署失敗 |       
| 302 |無法建立 ccmsetup 服務  |       
| 303 |無法刪除 ccmsetup 服務 |       
| 304 |無法在系統磁碟機上啟用檔案型寫入篩選器 (FBWF) 的嵌入式作業系統上安裝 |       
| 305 |原生安全性模式在 Windows 2000 上無效  |       
| 306 |無法啟動 ccmsetup 下載程序  |       
| 307 |無效的 ccmsetup 命令列 |       
| 308 |無法透過 WINHTTP 下載位於以下位址的檔案 |       
| 309 |無法透過 BITS 下載位於以下位址的檔案 |       
| 310 |無法安裝 BITS 版本 |       
| 311 |無法驗證先決條件檔案是否為 MS 簽署  |       
| 312 |因磁碟已滿而無法複製檔案 |       
| 313 |Client.msi 安裝失敗，出現 MSI 錯誤 |       
| 314 |無法載入 ccmsetup.xml 資訊清單檔案 |       
| 315 |無法取得用戶端憑證  |       
| 316 |先決條件檔案並非由 MS 簽署 |       
| 317 |需要重新開機才能繼續安裝  |       
| 318 |無法在 MP 上安裝用戶端，因為 MP 和用戶端版本不符 |       
| 319 |不支援作業系統或 Service Pack  |       
| 320 |不支援的部署       |       
| 321 |位元遺失        |       
| 322 |來源資料夾無法使用       |       
| 323 |不支援 Appv              |       
| 324 |不正確的站台版本              |       
| 325 |先決條件的雜湊不符       |       
| 326 |MDM 取消註冊失敗      |       
| 327 |偵測到 MDM 登錄      |       
| 328 |偵測到 Intune       |       
| 329 |不允許計量付費的網路      |       
| 400 |成功完成用戶端部署 |  
| 401 |部署成功，必須重新開機     |       
| 402 |部署成功，重新開機成功     |
| 500 |已啟動用戶端指派|
| 601 |未知的用戶端指派失敗|
| 602 |下列站台碼無效|
| 603 |無法指派至 MP|
| 604 |無法探索預設管理點|
| 605 |無法下載站台簽署憑證|
| 606 |無法自動探索站台碼|
| 607 |站台指派失敗。用戶端版本高於站台版本|
| 608 |無法從 Active Directory Domain Services 和 SLP 取得站台版本|
| 609 |無法取得用戶端版本|
| 700 |成功完成用戶端指派|

## <a name="801-state_topictype_device_client_deployment"></a>801 STATE_TOPICTYPE_DEVICE_CLIENT_DEPLOYMENT

無狀態識別碼。

## <a name="810-state_topictype_client_comanagement"></a>810 STATE_TOPICTYPE_CLIENT_COMANAGEMENT

|     狀況訊息識別碼     |  狀況訊息描述 |
|:-------------|:------|
| 100 | 註冊狀態   |
| 101 | 已排程註冊   |
| 102 | 已取消註冊   |
| 105 | 已開始註冊   |
| 106 | 註冊成功但未佈建
| 107 | 註冊成功且已佈建
| 108 | 註冊沒有作用中使用者   |
| 110 | 註冊失敗   |


## <a name="820--state_topictype_client_wufb"></a>820 STATE_TOPICTYPE_CLIENT_WUFB

|     狀況訊息識別碼     |  狀況訊息描述 |
|:-------------|:------|
| 1 | 商務用 Windows Update 用戶端狀態| 

## <a name="900-state_topictype_branch_dp"></a>900 STATE_TOPICTYPE_BRANCH_DP

|     狀況訊息識別碼     |  狀況訊息描述 |
|:-------------|:------|
| 1 | 磁碟空間   | 

## <a name="901-state_topictype_remote_dp_monitoring"></a>901 STATE_TOPICTYPE_REMOTE_DP_MONITORING

無狀態識別碼。

## <a name="902-state_topictype_pull_dp_monitoring"></a>902 STATE_TOPICTYPE_PULL_DP_MONITORING

無狀態識別碼。

## <a name="903-state_topictype_dp_usage"></a>903 STATE_TOPICTYPE_DP_USAGE

無狀態識別碼。

## <a name="1000--state_topictype_client_framework_comm"></a>1000 STATE_TOPICTYPE_CLIENT_FRAMEWORK_COMM

|     狀況訊息識別碼     |  狀況訊息描述 |
|:-------------|:------|
| 1 | 用戶端順利與管理點通訊 |
| 2 | 用戶端無法與管理點通訊 |

## <a name="1001-state_topictype_client_framework_local"></a>1001 STATE_TOPICTYPE_CLIENT_FRAMEWORK_LOCAL

|     狀況訊息識別碼     |  狀況訊息描述 |
|:-------------|:------|
| 1 |用戶端從本機憑證存放區成功擷取憑證    |
| 2 |用戶端無法從本機憑證存放區擷取憑證 |

## <a name="1002-state_topictype_device_client_framework_comm"></a>1002 STATE_TOPICTYPE_DEVICE_CLIENT_FRAMEWORK_COMM

無狀態識別碼。

## <a name="1003-state_topictype_device_client_framework_local"></a>1003 STATE_TOPICTYPE_DEVICE_CLIENT_FRAMEWORK_LOCAL

無狀態識別碼。

## <a name="1004-state_topictype_device_client_framework_certificate"></a>1004 STATE_TOPICTYPE_DEVICE_CLIENT_FRAMEWORK_CERTIFICATE

無狀態識別碼。

## <a name="1005-state_topictype_device_client_wipe"></a>1005 STATE_TOPICTYPE_DEVICE_CLIENT_WIPE

無狀態識別碼。

## <a name="1006-state_topictype_device_client_retire"></a>1006 STATE_TOPICTYPE_DEVICE_CLIENT_RETIRE

無狀態識別碼。

## <a name="1007-state_topictype_device_client_wipe_intune"></a>1007 STATE_TOPICTYPE_DEVICE_CLIENT_WIPE_INTUNE

無狀態識別碼。

## <a name="1008-state_topictype_device_client_retire_intune"></a>1008 STATE_TOPICTYPE_DEVICE_CLIENT_RETIRE_INTUNE

無狀態識別碼。

## <a name="1009-state_topictype_device_client_devicelock"></a>1009 STATE_TOPICTYPE_DEVICE_CLIENT_DEVICELOCK

無狀態識別碼。

## <a name="1010-state_topictype_device_client_devicelock_intune"></a>1010 STATE_TOPICTYPE_DEVICE_CLIENT_DEVICELOCK_INTUNE

無狀態識別碼。

## <a name="1011-state_topictype_device_client_devicepinreset"></a>1011 STATE_TOPICTYPE_DEVICE_CLIENT_DEVICEPINRESET

無狀態識別碼。

## <a name="1012-state_topictype_device_client_devicepinreset_intune"></a>1012 STATE_TOPICTYPE_DEVICE_CLIENT_DEVICEPINRESET_INTUNE

無狀態識別碼。

## <a name="1013-state_topictype_device_client_devicepinreset_onprem"></a>1013 STATE_TOPICTYPE_DEVICE_CLIENT_DEVICEPINRESET_ONPREM

無狀態識別碼。

## <a name="1014-state_topictype_device_client_devicealbypass"></a>1014 STATE_TOPICTYPE_DEVICE_CLIENT_DEVICEALBYPASS

無狀態識別碼。

## <a name="1015-state_topictype_device_client_devicealbypass_intune"></a>1015 STATE_TOPICTYPE_DEVICE_CLIENT_DEVICEALBYPASS_INTUNE

無狀態識別碼。

## <a name="1100-state_topictype_client_framework_modereadiness"></a>1100 STATE_TOPICTYPE_CLIENT_FRAMEWORK_MODEREADINESS

|     狀況訊息識別碼     |  狀況訊息描述 |
|:-------------|:------|
| 1 |用戶端未準備好使用原生模式  |
| 2 |用戶端已準備好使用原生模式     |


## <a name="1300-state_topictype_client_health"></a>1300 STATE_TOPICTYPE_CLIENT_HEALTH

|     狀況訊息識別碼     |  狀況訊息描述 |
|:-------------|:------|
| 1 | 成功|
| 2 | 失敗 |

## <a name="1401-state_topictype_state_report"></a>1401 STATE_TOPICTYPE_STATE_REPORT

無狀態識別碼。

## <a name="1500-state_topictype_cal_track_ut"></a>1500 STATE_TOPICTYPE_CAL_TRACK_UT

無狀態識別碼。

## <a name="1502-state_topictype_cal_track_mt"></a>1502 STATE_TOPICTYPE_CAL_TRACK_MT

無狀態識別碼。

## <a name="1503-state_topictype_cal_track_ml"></a>1503 STATE_TOPICTYPE_CAL_TRACK_ML

無狀態識別碼。 

## <a name="1600-state_topictype_user_affinity"></a>1600 STATE_TOPICTYPE_USER_AFFINITY

|     狀況訊息識別碼     |  狀況訊息描述 |
|:-------------|:------|
| 1 |已設定使用者親和性       |
| 2 |已移除使用者親和性       |

## <a name="1700-state_topictype_app_ci_scan"></a>1700 STATE_TOPICTYPE_APP_CI_SCAN

無狀態識別碼。

## <a name="1701-state_topictype_app_ci_compliance"></a>1701 STATE_TOPICTYPE_APP_CI_COMPLIANCE

無狀態識別碼。

## <a name="1702-state_topictype_app_ci_enforcement"></a>1702 STATE_TOPICTYPE_APP_CI_ENFORCEMENT

|     狀況訊息識別碼     |  狀況訊息描述 |
|:-------------|:------|
| 1000  |設定項目成功           |
| 1001 |設定項目成功，已安裝         |
| 1002 |設定項目成功，正式發行前小眾測試          |
| 1003 |設定項目快速狀態成功          |
| 2000 |進行中的設定項目           |
| 2001 |進行中的設定項目，正在等待內容         |
| 2002 |進行中的設定項目，正在安裝          |
| 2003 |進行中的設定項目，正在等待重新開機         |
| 2004 |進行中的設定項目，正在等待維護期間        |
| 2005 |進行中的設定項目，正在等待排程         |
| 2006 |進行中的設定項目，正在下載相依內容     |
| 2007 |進行中的設定項目，正在安裝相依內容        |
| 2008 |進行中的設定項目，重新開機擱置中         |
| 2009 |進行中的設定項目，已下載內容         |
| 2010 |進行中的設定項目，更新擱置中         |
| 2011 |進行中的設定項目，正在等待使用者重新連線        |
| 2012 |進行中的設定項目，正在等待使用者登出         |
| 2013 |進行中的設定項目，正在等待使用者登入         |
| 2014 |進行中的設定項目，正在等待安裝         |
| 2015 |進行中的設定項目，正在等待重試         |
| 2016 |進行中的設定項目，正在等待 presmode         |
| 2017 |進行中的設定項目，正在等候協調        |
| 2018 |進行中的設定項目，正在等待網路         |
| 2019 |進行中的設定項目，更新 VE 擱置中         |
| 2020 |進行中的設定項目，正在更新 VE         |
| 3000 |設定項目不符合需求           |
| 3001 |設定項目不符合需求，主機不適用        |
| 4000 |未知的設定項目           |
| 5000 |設定項目錯誤            |
| 5001 |設定項目錯誤，正在評估          |
| 5002 |設定項目錯誤，正在安裝          |
| 5003 |設定項目錯誤，正在擷取內容         |
| 5004 |設定項目錯誤，正在安裝相依性         |
| 5005 |設定項目錯誤，正在擷取內容相依性        |
| 5006 |設定項目錯誤，規則衝突          |
| 5007 |設定項目錯誤，正在等待重試          |
| 5008 |設定項目錯誤，正在解除安裝取代        |
| 5009 |設定項目錯誤，正在下載取代         |
| 5010 |設定項目錯誤，正在更新 VE          |
| 5011 |設定項目錯誤，正在安裝授權         |
| 5012 |設定項目錯誤，正在擷取，允許所有受信任的應用程式       |
| 5013 |設定項目錯誤，沒有可用的授權         |
| 5014 |設定項目錯誤，不支援的 OS          |
| 6000 |設定項目啟動成功            |
| 6010 |設定項目啟動錯誤            |
| 6020 |設定項目啟動未知|

## <a name="1703-state_topictype_app_ci_assignment_evaluatio"></a>1703 STATE_TOPICTYPE_APP_CI_ASSIGNMENT_EVALUATIO

無狀態識別碼。

## <a name="1704-state_topictype_app_ci_launch"></a>1704 STATE_TOPICTYPE_APP_CI_LAUNCH

無狀態識別碼。

## <a name="1800-state_topictype_event_intrinsic"></a>1800 STATE_TOPICTYPE_EVENT_INTRINSIC

無狀態識別碼。

## <a name="1801-state_topictype_event_extrinsic"></a>1801 STATE_TOPICTYPE_EVENT_EXTRINSIC

無狀態識別碼。

## <a name="1900-state_topictype_ep_am_infection"></a>1900 STATE_TOPICTYPE_EP_AM_INFECTION

無狀態識別碼。

## <a name="1901-state_topictype_ep_am_health"></a>1901 State_Topictype_Ep_Am_Health

無狀態識別碼。

## <a name="1902-state_topictype_ep_malware"></a>1902 STATE_TOPICTYPE_EP_MALWARE

無狀態識別碼。

## <a name="1950-state_topictype_atp_health_status"></a>1950 STATE_TOPICTYPE_ATP_HEALTH_STATUS

無狀態識別碼。

## <a name="2001-state_topictype_ep_client_deployment"></a>2001 STATE_TOPICTYPE_EP_CLIENT_DEPLOYMENT

|     狀況訊息識別碼     |  狀況訊息描述 |
|:-------------|:------|
| 1 |Endpoint Protection 非受控   |
| 2 |Endpoint Protection 正在等待安裝  |
| 3 |Endpoint Protection 受控   |
| 4 |Endpoint Protection 安裝失敗  |
| 5 |Endpoint Protection 重新開機擱置中  |
| 6 |不支援的 Endpoint Protection   |
| 7 |Endpoint Protection 共同受控   |

## <a name="2002-state_topictype_ep_client_policyapplication"></a>2002 STATE_TOPICTYPE_EP_CLIENT_POLICYAPPLICATION

|     狀況訊息識別碼     |  狀況訊息描述 |
|:-------------|:------|
| 0 |Endpoint Protection 原則應用程式狀態未知    |
| 1 |Endpoint Protection 原則應用程式成功    |
| 2 |Endpoint Protection 原則應用程式失敗    |

## <a name="2003-state_topictype_client_action"></a>2003 STATE_TOPICTYPE_CLIENT_ACTION

|     狀況訊息識別碼     |  狀況訊息描述 |
|:-------------|:------|
| 0 |  Unknown    |
| 1 |  作用中    |
| 2 |  非使用中    |

## <a name="2100-state_topictype_wp_client_deployment"></a>2100 STATE_TOPICTYPE_WP_CLIENT_DEPLOYMENT

|     狀況訊息識別碼     |  狀況訊息描述 |
|:-------------|:------|
| 1 | 未安裝喚醒 Proxy    |
| 2 | 正在等待安裝喚醒 Proxy   |
| 3 | 已安裝喚醒 Proxy    |
| 4 | 喚醒 Proxy 安裝失敗   |
| 5 | 喚醒 Proxy 正在等待重新開機   |
| 6 | 喚醒 Proxy 在此 OS 上不受支援  |
| 7 | 喚醒 Proxy 伺服器選擇退出   |
| 8 | 喚醒 Proxy 解除安裝失敗   |
| 9 | 不支援喚醒 Proxy 執行階段   |

## <a name="2200-state_topictype_fdm"></a>2200 STATE_TOPICTYPE_FDM

無狀態識別碼。

## <a name="2201-state_topictype_ccm_cert_binding"></a>2201 STATE_TOPICTYPE_CCM_CERT_BINDING

無狀態識別碼。

## <a name="2202-state_topictype_server_statistic"></a>2202 STATE_TOPICTYPE_SERVER_STATISTIC

無狀態識別碼。

## <a name="3000-state_topictype_dm_wns_channel"></a>3000 STATE_TOPICTYPE_DM_WNS_CHANNEL

|     狀況訊息識別碼     |  狀況訊息描述 |
|:-------------|:------|
|0 | Windows 推播通知服務通道已設定|

## <a name="4000-state_topictype_mdm_device_property"></a>4000 STATE_TOPICTYPE_MDM_DEVICE_PROPERTY

無狀態識別碼。

## <a name="4002-state_topictype_mdm_client_idenitity"></a>4002 STATE_TOPICTYPE_MDM_CLIENT_IDENITITY

無狀態識別碼。

## <a name="4003-state_topictype_mdm_application_request"></a>4003 STATE_TOPICTYPE_MDM_APPLICATION_REQUEST

無狀態識別碼。

## <a name="4004-state_topictype_mdm_application_state"></a>4004 STATE_TOPICTYPE_MDM_APPLICATION_STATE

無狀態識別碼。

## <a name="4005-state_topictype_mdm_license_device_relation"></a>4005 STATE_TOPICTYPE_MDM_LICENSE_DEVICE_RELATION

無狀態識別碼。

## <a name="4006-state_topictype_mdm_license_keys"></a>4006 STATE_TOPICTYPE_MDM_LICENSE_KEYS

無狀態識別碼。

## <a name="4007-state_topictype_mdm_policy_assignment"></a>4007 STATE_TOPICTYPE_MDM_POLICY_ASSIGNMENT

無狀態識別碼。

## <a name="4008-state_topictype_mdm_android_count"></a>4008 STATE_TOPICTYPE_MDM_ANDROID_COUNT

無狀態識別碼。

## <a name="4009-state_topictype_mdm_slk_status"></a>4009 STATE_TOPICTYPE_MDM_SLK_STATUS

無狀態識別碼。

## <a name="4010-state_topictype_mdm_user_company_term_acceptance"></a>4010 STATE_TOPICTYPE_MDM_USER_COMPANY_TERM_ACCEPTANCE

無狀態識別碼。

## <a name="4022-state_topictype_mdm_dep_syncnow_status"></a>4022 STATE_TOPICTYPE_MDM_DEP_SYNCNOW_STATUS

無狀態識別碼。

## <a name="4023-state_topictype_mdm_mam_store_app_sync"></a>4023 STATE_TOPICTYPE_MDM_MAM_STORE_APP_SYNC

無狀態識別碼。

## <a name="5000-state_topictype_certificate_enrollment"></a>5000 STATE_TOPICTYPE_CERTIFICATE_ENROLLMENT

|     狀況訊息識別碼     |  狀況訊息描述 |
|:-------------|:------|
| 1 |已發出挑戰         |
| 2 |發出挑戰失敗        |
| 3 |要求建立失敗        |
| 4 |要求提交失敗        |
| 5 |挑戰驗證成功       |
| 6 |挑戰驗證失敗       |
| 7 |問題失敗         |
| 8 |問題待決         |
| 9 |已發出          |
| 10 |回應處理失敗       |
| 11 |回應待決         |
| 12 |註冊成功         |
| 13 |不需要註冊         |
| 14 |已撤銷          |
| 15 |已從集合中移除        |
| 16 |更新已驗證         |
| 17 |安裝失敗        |
| 18 |已安裝         |
| 19 |刪除失敗         |
| 20 |已刪除         |
| 21 |已要求更新        |


## <a name="5001-state_topictype_certificate_crp"></a>5001 STATE_TOPICTYPE_CERTIFICATE_CRP

|     狀況訊息識別碼     |  狀況訊息描述 |
|:-------------|:------|
| 1 |已發出挑戰         |
| 2 |發出挑戰失敗        |
| 3 |要求建立失敗        |
| 4 |要求提交失敗        |
| 5 |挑戰驗證成功       |
| 6 |挑戰驗證失敗       |
| 7 |問題失敗         |
| 8 |問題待決         |
| 9 |已發出          |
| 10 |回應處理失敗       |
| 11 |回應待決         |
| 12 |註冊成功         |
| 13 |不需要註冊         |
| 14 |已撤銷          |
| 15 |已從集合中移除        |
| 16 |更新已驗證         |
| 17 |安裝失敗        |
| 18 |已安裝         |
| 19 |刪除失敗         |
| 20 |已刪除         |
| 21 |已要求更新        |

## <a name="5200-state_topictype_resource_access_status"></a>5200 STATE_TOPICTYPE_RESOURCE_ACCESS_STATUS

|     狀況訊息識別碼     |  狀況訊息描述 |
|:-------------|:------|
| 1 | 狀態釘選設定成功       |
| 2 | 狀態釘選設定失敗       |
| 3 | 不支援狀態釘選設定      |
| 4 | 正在進行狀態釘選設定      |

## <a name="6000-state_topictype_remoteapp_subscription_status"></a>6000 STATE_TOPICTYPE_REMOTEAPP_SUBSCRIPTION_STATUS

無狀態識別碼。

## <a name="6001-state_topictype_remoteapp_subscription_sync_status"></a>6001 STATE_TOPICTYPE_REMOTEAPP_SUBSCRIPTION_SYNC_STATUS

無狀態識別碼。

## <a name="6002-state_topictype_remoteapp_authcookies_sync_status"></a>6002 STATE_TOPICTYPE_REMOTEAPP_AUTHCOOKIES_SYNC_STATUS

無狀態識別碼。

## <a name="6003-state_topictype_remoteapplications_sync_status"></a>6003 STATE_TOPICTYPE_REMOTEAPPLICATIONS_SYNC_STATUS

無狀態識別碼。

## <a name="6004-state_topictype_remoteapp_lock_result"></a>6004 STATE_TOPICTYPE_REMOTEAPP_LOCK_RESULT

無狀態識別碼。

## <a name="7000-state_topictype_user_company_term_acceptance"></a>7000 STATE_TOPICTYPE_USER_COMPANY_TERM_ACCEPTANCE

無狀態識別碼。

## <a name="7001-state_topictype_pfx_certificate"></a>7001 STATE_TOPICTYPE_PFX_CERTIFICATE

|     狀況訊息識別碼     |  狀況訊息描述 |
|:-------------|:------|
| 1 |已發出挑戰    |
| 2 |發出挑戰失敗   |
| 3 |要求建立失敗   |
| 4 |要求提交失敗   |
| 5 |挑戰驗證成功  |
| 6 |挑戰驗證失敗  |
| 7 |問題失敗    |
| 8 |問題待決    |
| 9 |已發出     |
| 10 |回應處理失敗  |
| 11 |回應待決    |
| 12 |註冊成功    |
| 13 |不需要註冊    |
| 14 |已撤銷     |
| 15 |已從集合中移除   |
| 16 |更新已驗證    |
| 17 |安裝失敗   |
| 18 |已安裝    |
| 19 |刪除失敗    |
| 20 |已刪除    |
| 21 |已要求更新   |

## <a name="7010-state_topictype_conditional_access_compliance"></a>7010 STATE_TOPICTYPE_CONDITIONAL_ACCESS_COMPLIANCE

|     狀況訊息識別碼     |  狀況訊息描述 |
|:-------------|:------|
|| 1 | 合規性成功    |
| 2 | 在 MP 的合規性失敗   |
| 3 | 在用戶端的合規性失敗   |
| 4 | 在 Intune 的合規性失敗   |
| 5 | 在 AAD 的合規性失敗   |
| 6 | 合規性 Comgmt Intune   |

## <a name="7200-state_topictype_super_peer_update_cache_map"></a>7200 STATE_TOPICTYPE_SUPER_PEER_UPDATE_CACHE_MAP

|     狀況訊息識別碼     |  狀況訊息描述 |
|:-------------|:------|
| 1 |已新增對等快取來源       |
| 2 |已移除對等快取來源      |

## <a name="7201-state_topictype_super_peer_update_config"></a>7201 STATE_TOPICTYPE_SUPER_PEER_UPDATE_CONFIG

|     狀況訊息識別碼     |  狀況訊息描述 |
|:-------------|:------|
| 1 |已停用對等快取來源       |
| 2 |對等快取來源使用中       |

## <a name="7202-state_topictype_download_aggregate_data"></a>7202 STATE_TOPICTYPE_DOWNLOAD_AGGREGATE_DATA
|     狀況訊息識別碼     |  狀況訊息描述 |
|:-------------|:------|
| 1 |下載彙總資料上傳       |

## <a name="7203-state_topictype_peersource_req_rejection_stats"></a>7203 STATE_TOPICTYPE_PEERSOURCE_REQ_REJECTION_STATS

|     狀況訊息識別碼     |  狀況訊息描述 |
|:-------------|:------|
| 1 |對等來源拒絕資料上傳     |

## <a name="7300-state_topictype_proxy_traffic"></a>7300 STATE_TOPICTYPE_PROXY_TRAFFIC

無狀態識別碼。

## <a name="7301-state_topictype_proxy_connection"></a>7301 STATE_TOPICTYPE_PROXY_CONNECTION

無狀態識別碼。

## <a name="7302-state_topictype_srs_usage_data"></a>7302 STATE_TOPICTYPE_SRS_USAGE_DATA

無狀態識別碼。

## <a name="7303-state_topictype_proxy_traffic_identity"></a>7303 STATE_TOPICTYPE_PROXY_TRAFFIC_IDENTITY

無狀態識別碼。

## <a name="8001-state_topictype_has_report"></a>8001 STATE_TOPICTYPE_HAS_REPORT

|     狀況訊息識別碼     |  狀況訊息描述 |
|:-------------|:------|
| 1 |支援健康情況證明      |
| 2 |不支援健康情況證明      |

## <a name="state_topictype_device_client_edplog"></a>STATE_TOPICTYPE_DEVICE_CLIENT_EDPLOG

無狀態識別碼。

## <a name="8003-state_topictype_enable_lostmode"></a>8003 STATE_TOPICTYPE_ENABLE_LOSTMODE

無狀態識別碼。

## <a name="8004-state_topictype_disable_lostmode"></a>8004 STATE_TOPICTYPE_DISABLE_LOSTMODE

無狀態識別碼。

## <a name="8005-state_topictype_locate_device"></a>8005 STATE_TOPICTYPE_LOCATE_DEVICE

無狀態識別碼。

## <a name="8006-state_topictype_reboot_device"></a>8006 STATE_TOPICTYPE_REBOOT_DEVICE

無狀態識別碼。

## <a name="8007-state_topictype_logoutuser"></a>8007 STATE_TOPICTYPE_LOGOUTUSER

無狀態識別碼。

## <a name="8008-state_topictype_userslist"></a>8008 STATE_TOPICTYPE_USERSLIST

無狀態識別碼。

## <a name="8009-state_topictype_deleteuser"></a>8009 STATE_TOPICTYPE_DELETEUSER

無狀態識別碼。

## <a name="8010-state_topictype_cleanpcretaininguserdata"></a>8010 STATE_TOPICTYPE_CLEANPCRETAININGUSERDATA

無狀態識別碼。

## <a name="8011-state_topictype_cleanpcwithoutretaininguserdata"></a>8011 STATE_TOPICTYPE_CLEANPCWITHOUTRETAININGUSERDATA

無狀態識別碼。

## <a name="8012-state_topictype_setdevicename"></a>8012 STATE_TOPICTYPE_SETDEVICENAME

無狀態識別碼。

## <a name="9000-state_topictype_book_ci_compliance"></a>9000 STATE_TOPICTYPE_BOOK_CI_COMPLIANCE

無狀態識別碼。

## <a name="9001-state_topictype_book_ci_enforcement"></a>9001 STATE_TOPICTYPE_BOOK_CI_ENFORCEMENT

無狀態識別碼。

## <a name="next-steps"></a>後續步驟

- [Configuration Manager 中狀態訊息的描述](https://support.microsoft.com/help/4459394/description-of-state-messaging-in-system-center-configuration-manager) \(機器翻譯\)
- [適用於 Configuration Manager 的軟體更新管理白皮書](https://www.microsoft.com/download/details.aspx?id=44578) \(英文\)
