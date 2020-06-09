---
title: 在 Microsoft Intune 中管理端點安全性原則 | Microsoft Docs
description: 了解安全性系統管理員如何在 Microsoft 端點管理員中使用端點安全性原則及設定檔聚焦於裝置安全性設定。
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 05/15/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.reviewer: mattsha
ms.openlocfilehash: 9c2e6f742610eb8f2f526c6fc7a5afabfbadcbbf
ms.sourcegitcommit: 302556d3b03f1a4eb9a5a9ce6138b8119d901575
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/27/2020
ms.locfileid: "83990861"
---
# <a name="manage-device-security-with-endpoint-security-policies-in-microsoft-intune"></a>在 Microsoft Intune 中使用端點安全性原則管理裝置安全性

安全性系統管理員可以使用 Intune「端點安全性」中的安全性原則來設定裝置安全性，而不必費神瀏覽裝置設定設定檔和安全性基準中較大量且較廣泛的設定。

每個原則類型各支援一或多個設定檔。 您會在設定檔中進行設定，以及針對不同平台，或針對較大原則區域中的不同聚焦區域將設定分組。

這些原則位於 [Microsoft 端點管理員系統管理中心](https://go.microsoft.com/fwlink/?linkid=2109431) [端點安全性] 節點中的 [管理] 下方。

![管理原則](./media/endpoint-security-policy/endpoint-security-policies.png)

以下是每個端點安全性原則類型的簡短描述。 若要深入了解這些類型，包含各類型可用的設定檔，請前往各原則類型的專屬內容連結：

- [防毒](../protect/endpoint-security-antivirus-policy.md) - 防毒原則可以協助安全性系統管理員專注於管理受控裝置的個別防毒設定群組。 若要使用防毒原則，請將 Microsoft Defender 進階威脅防護 (Defender ATP) 與 Intune 整合為行動威脅防禦解決方案。

- [磁碟加密](../protect/endpoint-security-disk-encryption-policy.md) - 端點安全性磁碟加密設定檔只會聚焦在與裝置內建加密方法相關的設定，例如 FileVault 或 BitLocker。 這樣聚焦可讓安全性系統管理員輕鬆管理磁碟加密設定，而無須瀏覽大量不相關的設定。

- [防火牆](../protect/endpoint-security-firewall-policy.md) - 使用 Intune 中的端點安全性防火牆原則來為執行 macOS 和 Windows 10 的裝置設定裝置內建防火牆。 內建防火牆包括適用於 Windows 裝置的 BitLocker 以及適用於 macOS 的 FileVault。

- [端點偵測及回應](../protect/endpoint-security-edr-policy.md) - 當您將 Defender ATP 與 Intune 整合時，請使用端點偵測及回應 (EDR) 的端點安全性原則來管理 EDR 設定，並讓裝置在 Defender ATP 上線。

- [受攻擊面縮小](../protect/endpoint-security-asr-policy.md) - 在您的 Windows 10 裝置上使用 Defender 防毒軟體時，請使用受攻擊面縮小的 Intune 端點安全性原則管理裝置的這些設定。

- [帳戶防護](../protect/endpoint-security-account-protection-policy.md) - 帳戶防護原則可以協助您保護使用者的身分識別和帳戶。 帳戶防護原則著重於 Windows Hello 和 Credential Guard 的設定，這是 Windows 身分識別與存取管理的一部分。

下列各節適用於所有端點安全性原則。

## <a name="create-an-endpoint-security-policy"></a>建立端點安全性原則

1. 登入 [Microsoft Endpoint Manager 系統管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)。

2. 依序選取 [端點安全性]、您要設定的原則類型及 [建立原則]。 從下列原則類型中選擇：
   - 防毒
   - 磁碟加密
   - 防火牆
   - 端點偵測與回應
   - 受攻擊面縮小
   - 帳戶防護

3. 輸入下列內容：
   - **平台**：選擇您要為其建立原則的平台。 可用選項取決於您選取的原則類型：
     - macOS
     - Windows 10 及更新版本
   - **設定檔**：針對您選取的平台，從可用的設定檔中選擇。 如需設定檔的資訊，請參閱本文中適用於您所選擇原則類型的專屬章節。

4. 選取 [建立]。

5. 在 [基本] 頁面上，輸入新設定檔的名稱與描述，然後選擇 [下一步]。

6. 在 [組態設定] 頁面上，展開每個設定群組，然後設定您要透過此設定檔管理的設定。

   當完成設定時，請選取 [下一步]。

7. 在 [範圍標籤] 頁面上，選擇 [選取範圍標籤] 來開啟 [選取標籤] 窗格，以將範圍標籤指派給設定檔。
  
   選取 [下一步] 以繼續進行操作。

8. 在 [指派] 頁面上，選取將接收此設定檔的群組。 如需指派設定檔的詳細資訊，請參閱[指派使用者和裝置設定檔](../configuration/device-profile-assign.md)。

   選取 [下一步]。

9. 在 [檢閱 + 建立] 頁面上，當您完成操作時，請選擇 [建立]。 新的設定檔會在您選取所建立設定檔的原則類型時顯示在清單中。

## <a name="duplicate-a-policy"></a>複製原則

端點安全性原則支援複製，以建立原始原則的複本。 當您需要將相似的原則指派給不同群組，但是不想要手動重新建立整個原則時，複製原則的功能就很實用。 與其手動重新建立，您可以複製原始原則，然後只進行新原則所需要的變更。 您可以只變更特定設定，以及該原則要指派的目標群組。

建立複本時，請為複本提供新名稱。 此複本會使用原始版本的相同設定和範圍標籤，但沒有任何指派。 您之後會需要編輯新的原則以建立指派。  

以下原則類型支援複製：

- 防毒
- 磁碟加密
- 防火牆
- 端點偵測與回應
- 受攻擊面縮小
- 帳戶防護

建立新原則後，請檢閱及編輯原則以變更其設定。

### <a name="to-duplicate-a-policy"></a>複製原則

1. 登入 [Microsoft Endpoint Manager 系統管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)。
2. 選取您要複製的原則。 接下來，選取 [複製]，或是選取位於原則右側的省略符號 ( **…** )，然後選取 [複製]。
3. 為原則提供**新名稱**，然後選取 [儲存]。

### <a name="to-edit-a-policy"></a>編輯原則

1. 選取新的原則，然後選取 [屬性]。
2. 選取 [設定] 以展開原則中的組態設定清單。 您無法透過這個檢視來修改設定，但可以檢閱設定方式。
3. 若要修改原則，請針對每個您希望進行變更的類別選取 [編輯]：
   - 基本
   - 作業
   - 範圍標籤
   - 組態設定
4. 進行變更後，選取 [儲存] 以儲存您的編輯。  您必須先儲存對其中一個類別進行的編輯，才能對其他類別進行編輯。

## <a name="manage-conflicts"></a>管理衝突

您可以透過端點安全性原則 (安全性原則) 管理的許多裝置設定，也都可以透過 Intune 中的其他原則類型來管理。 其他原則類型包括「裝置設定」原則和「安全性基準」。 因為您可以管理具備數種不同原則類型的一個設定，或是具備相同原則類型的多個設定，所以您可能會需要在裝置不符合預期設定時，辨別及解決原則衝突。

- 安全性基準可以為設定指定非預設的值，使其符合基準指出的建議設定。
- 根據預設，其他原則類型 (包括端點安全性原則) 會將值設為「未設定」。 其他原則類型會需要您在原則中明確進行設定。

無論原則方法為何，透過多種原則類型，或透過相同原則類型的多個原則來管理相同裝置上的相同設定，都可能會導致應避免的衝突。

下列連結中的資訊可協助您辨別及解決衝突：

- [針對 Intune 中的原則和設定檔進行疑難排解](../configuration/troubleshoot-policies-in-microsoft-intune.md)
- [監視您的安全性基準](../protect/security-baselines-monitor.md#troubleshoot-using-per-setting-status)

## <a name="next-steps"></a>後續步驟

[在 Intune 中管理端點安全性](../protect/endpoint-security.md)
