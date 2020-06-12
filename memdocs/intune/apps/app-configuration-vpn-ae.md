---
title: 設定適用於 Android 企業裝置的 VPN
titleSuffix: Microsoft Intune
description: 使用應用程式保護原則設定適用於 Android 企業裝置的 VPN。
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 06/01/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: tycast
ms.suite: ems
search.appverid: MET150
ms.custom: ''
ms.collection: M365-identity-device-management
ms.openlocfilehash: bcb7bd506d92befa3c73faf7270de28765f5b192
ms.sourcegitcommit: d498e5eceed299f009337228523d0d4be76a14c2
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/04/2020
ms.locfileid: "84347414"
---
# <a name="configure-a-vpn-for-android-enterprise-devices"></a>設定適用於 Android 企業裝置的 VPN

本主題說明如何建立應用程式設定原則，可與 Android 企業裝置上的 VPN 用戶端一起部署。 此設定可讓所選應用程式的網路流量存取公司資源。

> [!NOTE]
> Android 平台目前不支援在其中一個選擇的應用程式開啟時，自動觸發 VPN 用戶端連線。 您必須先手動起始 VPN 連線，或者可以使用 [Always-On VPN](../configuration/vpn-settings-android-enterprise.md)。

建立設定原則以獲得成功 VPN 存取的必要條件，包括所選 VPN 用戶端支援受控應用程式組態設定檔的功能。 目前，支援 Intune 應用程式設定原則的 VPN 用戶端包括：
- Cisco AnyConnect
- Citrix SSO
- F5 Access
- Palo Alto Global Connect
- Pulse Secure
- SonicWall Mobile Connect

如果 VPN 端點的驗證存取方法需要使用用戶端憑證，您應事先建立憑證設定檔，以利填入應用程式設定原則的必要值。

> [!NOTE]
> 雖然 Android 企業工作設定檔案例同時支援 SCEP 和 PKCS 憑證，但 Android 企業裝置擁有者案例目前僅支援 SCEP 憑證。 

建立和測試個別應用程式 VPN 設定檔的基本流程如下列步驟：
1.  為您的基礎結構選擇適當的 VPN 用戶端應用程式。
2.  識別您想要搭配 VPN 連線使用之生產力應用程式的應用程式套件識別碼。
3.  部署符合 VPN 連線驗證需求的任何憑證設定檔。 請務必驗證部署是否成功。
4.  部署 VPN 用戶端應用程式。
5.  使用在前述步驟中收集的資訊，準備應用程式設定型的 VPN 設定檔。
6.  部署新建立的 VPN 設定檔。
7.  確認 VPN 用戶端應用程式能夠成功連線到您的 VPN 伺服器基礎結構。
8.  驗證來自所選生產力應用程式的流量，能在使用中成功地傳輸 VPN。

## <a name="get-the-app-package-id"></a>取得應用程式套件識別碼

為您想要授與 VPN 存取權的每個應用程式，找出其套件識別碼。 針對可公開取得的應用程式，考慮在 Google Play 存放區中取得每個應用程式的套件識別碼。 每個應用程式所顯示的 URL 都包含套件識別碼。 例如，Android 版 Microsoft Edge 瀏覽器的套件識別碼是 `com.microsoft.emmx`。 套件識別碼會包含在 URL 中。

![尋找應用程式套件識別碼的範例。](./media/app-configuration-vpn-ae/app-configuration-vpn-ae-01.png)

如需商務營運 (LOB) 應用程式，請要求您的廠商或應用程式開發小組提供相關的套件識別碼。

## <a name="certificates"></a>憑證

在本主題中，我們假設您的 VPN 連線會使用憑證型驗證，而且您已成功在鏈結中部署讓用戶端驗證成功所需的所有憑證。 一般而言，這可能是用戶端憑證、任何中繼憑證以及根憑證。
如需 Android 企業憑證部署的其他資訊，請先複習此主題：[在 Microsoft Intune 中使用憑證進行驗證](../protect/certificates-configure.md)。

當用戶端驗證憑證設定檔部署完成後，您需要該設定檔的一些詳細資料，以建置 VPN 應用程式設定原則。
如果不熟悉建立應用程式組態設定檔的方式，請參閱此主題：[為受控的 Android 企業裝置新增應用程式設定原則](../apps/app-configuration-policies-use-android.md)。
 

## <a name="build-the-vpn-profile"></a>建置 VPN 設定檔

有兩種方式建置 VPN 應用程式的應用程式設定原則。 您可以使用**設定設計工具**或 **JSON 資料**選項。 當**設定設計工具**方法中未提供所有必要的 VPN 設定時，即需要使用 **JSON 資料**選項。 如果決定需要 JSON 選項支援，請洽詢 VPN 廠商。 在本主題中，我們會示範這兩種方法的範例。 在 **JSON 資料** 和**設定設計工具**這兩種方法中，您可以成功併入憑證型驗證。 使用 **JSON 資料**方法時，您可以從使用**設定設計工具**開始，以擷取必要的設定檔值。

> [!NOTE]
> 雖然許多 VPN 用戶端設定參數都很類似，但每個應用程式都有自己的唯一索引鍵和選項。 如有問題，請洽詢您的 VPN 廠商。 

## <a name="use-the-configuration-designer-flow"></a>使用設定設計工具的流程

1.  首先，為**受控裝置**新增應用程式設定原則。
2.  輸入適當的名稱。
3.  選取 [Android 企業] 作為平台。
4.  如果需要憑證型驗證，請選取 [僅限工作設定檔] 或 [僅限裝置擁有者] 作為設定檔類型。 [Work Owner and Device Owner Profile] \(工作擁有者和裝置擁有者設定檔\) 與憑證型驗證不相容。
5.  請為目標應用程式，選取您已部署的 VPN 用戶端；在本範例中，我們使用之前已部署的 Cisco AnyConnect VPN 用戶端

  ![建立應用程式設定原則的範例 - 基本概念。](./media/app-configuration-vpn-ae/app-configuration-vpn-ae-02.png)

6. 在下一個頁面中，使用 [組態設定] 下拉式選單選取 [Use Configuration designer] \(使用設定設計工具\) 選項。

  ![使用設定設計工具流程的範例 - 設定。](./media/app-configuration-vpn-ae/app-configuration-vpn-ae-03.png)

7. 按一下 [新增]，以顯示設定金鑰的清單。
8.  選取所選設定需要的所有設定金鑰。 在此範例中，我們會使用最少的清單來設定 AnyConnect VPN，包括憑證型驗證和個別應用程式 VPN。
  
  <img alt="Example of using the Configuration Designer Flow - Configuration keys." src="./media/app-configuration-vpn-ae/app-configuration-vpn-ae-04.png" width="350">

9. 輸入 [連線名稱]、[主機] 和 [通訊協定] 金鑰的適當值。

  ![使用設定設計工具流程的範例 - 選取設定金鑰。](./media/app-configuration-vpn-ae/app-configuration-vpn-ae-05.png)  

  > [!NOTE]
  > 這些金鑰的名稱會隨您建立原則的 VPN 用戶端應用程式而有所不同。

10. 輸入您稍早在 [Per App VPN Allowed Apps] \(個別應用程式 VPN 允許的應用程式\) 金鑰中收集到的應用程式套件識別碼。

  ![使用設定設計工具流程的範例 - 應用程式套件識別碼。](./media/app-configuration-vpn-ae/app-configuration-vpn-ae-06.png)  

11. 在 [KeyChain Certificate Alias] \(KeyChain 憑證別名\) (選擇性) 金鑰中，將 [值類型] 從 [字串] 切換至 [憑證]，這可讓您挑選正確的用戶端憑證設定檔，搭配 VPN 驗證使用。

  ![使用設定設計工具流程的範例 - 更新 KeyChain 憑證別名。](./media/app-configuration-vpn-ae/app-configuration-vpn-ae-07.png)  

12. 在下一個頁面中，選擇任何適當的範圍標籤。
13. 在下一個頁面中，輸入要部署應用程式設定原則的適當群組。
14. 選取 [建立] 以完成原則的建立和部署。

  ![使用設定設計工具流程的範例 - 檢閱。](./media/app-configuration-vpn-ae/app-configuration-vpn-ae-08.png)  

## <a name="use-the-json-flow"></a>使用 JSON 流程

建立暫存設定檔：
1.  首先，為**受控裝置**新增應用程式設定原則。
2.  輸入適當的名稱 (暫時使用此設定檔，因為「不」儲存)。
3.  選取 [Android 企業] 作為平台。
4.  為目標應用程式選取您已部署的 VPN 用戶端。
5.  如果需要憑證型驗證，請選取 [僅限工作設定檔] 或 [僅限裝置擁有者] 作為設定檔類型。 [Work Owner and Device Owner Profile] \(工作擁有者和裝置擁有者設定檔\) 與憑證型驗證不相容。

  ![使用 JSON 流程的範例 - 基本概念。](./media/app-configuration-vpn-ae/app-configuration-vpn-ae-09.png)  

6.  在下一個頁面中，使用 [組態設定] 下拉式選單選取 [Use Configuration designer] \(使用設定設計工具\) 選項。

  ![使用 JSON 流程的範例 - 組態設定格式。](./media/app-configuration-vpn-ae/app-configuration-vpn-ae-10.png)  

7.  按一下 [新增]，以顯示設定金鑰的清單。
8.  選取 [值類型] 為 [字串] 的任一金鑰，然後按一下 [確定]。

  <img alt="Example of using the JSON Flow - Select a key." src="./media/app-configuration-vpn-ae/app-configuration-vpn-ae-11.png" width="350">

9.  現在將 [值類型] 從 [字串] 變更為 [憑證]。 這可讓您挑選正確的用戶端憑證設定檔，搭配 VPN 驗證使用。

  ![使用 JSON 流程的範例 - 連線名稱。](./media/app-configuration-vpn-ae/app-configuration-vpn-ae-12.png)  

10. 立即將 [值類型] 變更回 [字串]。 請注意，[設定值] 會變更為 `{{cert:GUID}}` 格式的權杖。
11. 選取以權杖表示的憑證，並將其複製到替代位置，例如文字編輯器。

  ![使用 JSON 流程的範例 - 設定值。](./media/app-configuration-vpn-ae/app-configuration-vpn-ae-13.png)  

12. 捨棄正在建立的設定檔 – 前幾個步驟的唯一目的是判斷憑證權杖。

### <a name="create-the-vpn-profile"></a>建立 VPN 設定檔

1.  首先，為**受控裝置**新增應用程式組態設定檔。
2.  輸入適當的名稱。
3.  選取 [Android 企業] 作為平台。
4.  為目標應用程式選取您已部署的 VPN 用戶端。
5.  如果需要憑證型驗證，請選取 [僅限工作設定檔] 或 [僅限裝置擁有者] 作為設定檔類型。 [Work Owner and Device Owner Profile] \(工作擁有者和裝置擁有者設定檔\) 與憑證型驗證不相容。
6.  使用 [組態設定] 下拉式選單選取 [輸入 JSON 資料] 選項。
7.  您可以直接編輯 JSON，或如果您想的話，也可以使用 [下載 JSON 範本] 按鈕下載，然後在自選的外部編輯器中修改範本。 請謹慎使用具有**智慧引號**的文字編輯器，因為包含智慧引號會使得 JSON 無效。

  ![使用 JSON 流程的範例 - 編輯 JSON。](./media/app-configuration-vpn-ae/app-configuration-vpn-ae-14.png)  

8.  無論您使用哪一種方法，一旦填入所需設定值之後，就必須移除整個 JSON 中所有包含 "STRING_VALUE" 或 STRING_VALUE 值的剩餘設定。

#### <a name="example-json-for-f5-access-vpn"></a>使用 F5 存取 VPN 的 JSON 範例

以下是使用 F5 存取 VPN 的 JSON 資料範例。

``` JSON
{
    "kind": "androidenterprise#managedConfiguration",
    "productId": "app:com.f5.edge.client_ics",
    "managedProperty": [
        {
            "key": "disallowUserConfig",
            "valueBool": false
        },
        {
            "key": "vpnConfigurations",
            "valueBundleArray": [
                {
                    "managedProperty": [
                        {
                            "key": "name",
                            "valueString": "MyCorpVPN"
                        },
                        {
                            "key": "server",
                            "valueString": "vpn.contoso.com"
                        },
                        {
                            "key": "weblogonMode",
                            "valueBool": false
                        },
                        {
                            "key": "fipsMode",
                            "valueBool": false
                        },
                        {
                            "key": "clientCertKeychainAlias",
                            "valueString": "{{cert:77333880-14e9-0aa0-9b2c-a1bc6b913829}}"
                        },
                        {
                            "key": "allowedApps",
                            "valueString": "com.microsoft.emmx"
                        },
                        {
                            "key": "mdmAssignedId",
                            "valueString": ""
                        },
                        {
                            "key": "mdmInstanceId",
                            "valueString": ""
                        },
                        {
                            "key": "mdmDeviceUniqueId",
                            "valueString": ""
                        },
                        {
                            "key": "mdmDeviceWifiMacAddress",
                            "valueString": ""
                        },
                        {
                            "key": "mdmDeviceSerialNumber",
                            "valueString": ""
                        },
                        {
                            "key": "allowBypass",
                            "valueBool": false
                        }
                    ]
                }
            ]
        }
    ]
}
```

## <a name="summary"></a>[摘要]

若對已註冊 Android Enterprise 的裝置使用應用程式設定原則，則不論平台是否直接支援個別應用程式的 VPN 行為，您都能加以利用。 

## <a name="additional-information"></a>其他資訊

如需相關資訊，請參閱下列主題：
- [為受控的 Android Enterprise 裝置新增應用程式設定原則](../apps/app-configuration-policies-use-android.md)
- [在 Intune 中設定 VPN 的 Android 企業裝置設定](../configuration/vpn-settings-android-enterprise.md)

## <a name="next-steps"></a>後續步驟

- [在 Intune 中建立 VPN 設定檔以連線到 VPN 伺服器](../configuration/vpn-settings-configure.md)
