---
title: 使用 Microsoft Intune 的端點安全性原則管理防毒設定 | Microsoft Docs
description: 針對您在 Microsoft 端點管理員中使用端點安全性防毒原則管理的裝置，設定及部署原則並使用相關報告。
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
ms.openlocfilehash: bfefdee7e949faf9e484ea20e7fc203ee72a9784
ms.sourcegitcommit: 97f150f8ba8be8746aa32ebc9b909bb47e22121c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/17/2020
ms.locfileid: "84879649"
---
# <a name="antivirus-policy-for-endpoint-security-in-intune"></a>Intune 端點安全性的防毒原則

Intune 端點安全性防毒原則可協助安全性系統管理員專注於管理受控裝置的個別幾組防毒設定。 若要使用防毒原則，請將 Intune 與 Microsoft Defender 進階威脅防護 (Microsoft Defender ATP) 整合為行動威脅防禦解決方案。

防毒原則包含數個設定檔。 每個設定檔只包含適用於 macOS、Windows 10 或 Windows 10 裝置上 Windows 安全性應用程式使用者體驗的 Microsoft Defender ATP 防毒相關設定。

您可以在 [Microsoft 端點管理員系統管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)，端點安全性節點的 [管理] 下方找到防毒原則。

防毒原則包括[裝置設定](../configuration/device-profile-create.md)原則中「端點保護」或「裝置限制」設定檔中的相同設定，並類似於[裝置合規性](../protect/device-compliance-get-started.md)原則的設定。 不過，這些原則類型包含與防毒無關的其他設定類別。 額外設定可能會將防毒設定工作變得更複雜。 此外，您無法透過其他原則類型來使用 macOS 防毒原則中的設定。 macOS 防毒設定檔可讓您不需使用 `.plist` 檔案進行設定。

## <a name="prerequisites-for-antivirus-policy"></a>防毒原則的必要條件

- **macOS**
  - 所有受支援的 macOS 版本
  - 您必須在裝置上安裝 Microsoft Defender ATP，才能使用 Intune 管理該裝置的防毒設定。 請參閱： [適用於 macOS 的 Microsoft Defender ATP](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/microsoft-defender-atp-mac) (位於 Microsoft Defender ATP 文件中)

- **Windows 10 及以上版本**
  - 您必須在裝置上安裝 Microsoft Defender ATP，才能使用 Intune 管理該裝置的防毒設定。 請參閱 Intune 文件中[適用於 Windows 的 Microsoft Defender ATP](../protect/advanced-threat-protection.md)。
  - Windows 安全性應用程式會安裝在執行 Window 10 的所有裝置上，而且不需要任何其他必要條件。

## <a name="antivirus-profiles"></a>防毒設定檔

**macOS 設定檔**：

- **防毒**：管理 macOS 的[防毒原則設定](../protect/antivirus-microsoft-defender-settings-macos.md)。

  使用[適用於 Mac 的 Microsoft Defender ATP](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/microsoft-defender-atp-mac) 時，您可以透過 Intune 設定及部署受控 macOS 裝置的防毒設定，而不需使用 `.plist` 檔案加以設定。

**Windows 10 設定檔**：

- **Microsoft Defender 防毒軟體**：管理 Windows 10 的[防毒原則設定](../protect/antivirus-microsoft-defender-settings-windows.md)。

  Defender 防毒軟體是 Microsoft Defender 進階威脅防護 (Microsoft Defender ATP) 的新一代保護元件。 新世代保護整合了機器學習、巨量資料分析、縱深威脅抵禦研究及雲端基礎結構來保護企業組織中的裝置。

  「Microsoft Defender 防毒軟體」設定檔是一項獨立的防毒設定執行個體，位於「裝置設定」原則的「裝置限制」設定檔中。
  
  這些設定可用於共同管理的裝置，因此和「裝置限制」設定檔中的防毒設定不同。 若要使用這些設定，您必須將 Endpoint Protection 的[共同管理工作負載滑桿](https://docs.microsoft.com/configmgr/comanage/how-to-switch-workloads)設為 Intune。

- **Windows 安全性體驗**：管理終端使用者能在 Microsoft Defender 安全性中心檢視的 [Windows 安全性設定](../protect/antivirus-security-experience-windows-settings.md)及其所收到的通知。 許多 Windows 安全性功能都會使用 Windows 安全性應用程式來提供電腦健全狀況與安全性相關的通知。 安全性應用程式通知包括防火牆、防毒產品、Windows Defender SmartScreen 等通知。

## <a name="antivirus-policy-reports"></a>防毒原則報告

防毒原則報告會顯示端點安全性防毒原則和裝置狀態的狀態詳細資料。 您可以在 Microsoft 端點管理員系統管理中心的端點安全性節點中找到這些報告。

若要檢視報告，請前往 [Microsoft 端點管理員系統管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)的 [端點安全性]，然後選取 [防毒]。 選取 [防毒] 後，開啟 [摘要] 頁面。 其他頁面會顯示其他報告和狀態檢視。

### <a name="summary"></a>[摘要]

在 [摘要] 頁面上，您可以[建立新原則](../protect/endpoint-security-policy.md#create-an-endpoint-security-policy)，並檢視先前建立的原則清單。 此清單包括原則所含設定檔的整體詳細資料 (原則類型)，以及該原則是否已指派。

![防毒原則的概觀頁面](./media/endpoint-security-antivirus-policy/antivirus-summary.png)

當您從清單中選取原則時，該原則執行個體的 [概觀] 頁面隨即開啟，並顯示詳細資訊。 當您從這個檢視選取磚時，Intune 會顯示該設定檔的其他詳細資料 (如果有的話)。

![防毒原則的概觀頁面](./media/endpoint-security-antivirus-policy/policy-overview.png)

### <a name="windows-10-unhealthy-endpoints"></a>Windows 10 狀況不良的端點

在 [Windows 10 狀況不良的端點] 頁面中，您可以檢視 MDM 受控 Windows 10 裝置的防毒狀態相關資訊。 裝置上執行的 Windows Defender 防毒軟體會將這些資訊以「威脅代理程式狀態」傳回。

只有偵測到問題的裝置才會出現在這個檢視中。 此檢視不會顯示確認沒有問題的裝置詳細資料。

![防毒原則的概觀頁面](./media/endpoint-security-antivirus-policy/antivirus-unhealthy-endpoints.png)

## <a name="next-steps"></a>後續步驟

[設定端點安全性原則](../protect/endpoint-security-policy.md#create-an-endpoint-security-policy)
