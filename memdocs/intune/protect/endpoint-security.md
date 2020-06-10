---
title: 在 Microsoft Intune 中管理端點安全性 | Microsoft Docs
description: 了解安全性系統管理員如何在 Microsoft 端點管理員中使用端點安全性節點，來管理裝置安全性及補救裝置問題。
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 05/15/2020
ms.topic: overview
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.reviewer: mattsha
ms.openlocfilehash: 99ac1e069386c69011543ac40878dd62a0d50527
ms.sourcegitcommit: 302556d3b03f1a4eb9a5a9ce6138b8119d901575
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/27/2020
ms.locfileid: "83990819"
---
# <a name="manage-endpoint-security-in-microsoft-intune"></a>在 Microsoft Intune 中管理端點安全性

身為安全性系統管理員，請使用 Intune 中的「端點安全性」節點來設定裝置安全性，並在這些裝置有風險時管理裝置的安全性工作。 端點安全性原則設計為可協助您專注於裝置的安全性，並降低風險。 可用的工作能協助您識別具風險裝置，以補救這些裝置並將其還原至相容或更安全的狀態。

端點安全性節點會將可透過 Intune 取得的工具進行分組，以讓您用來將裝置保持安全：

- **檢閱您所有受控裝置的狀態**。 使用[所有裝置](#manage-devices)檢視時，您可以在其中概要檢視裝置合規性，然後鑽研至特定裝置以了解哪些合規性原則未滿足，以便您解決問題。

- **部署可建立裝置最佳做法安全性設定的安全性基準**。 Intune 包含 Windows 裝置的[安全性基準](#manage-security-baselines)，以及不斷增加的應用程式清單，例如 Microsoft Defender 進階威脅防護 (Defender ATP) 和 Microsoft Edge。 安全性基準是預先設定的 Windows 設定群組，可協助您套用已知的設定群組，與相關安全性小組所建議的預設值。

- **透過緊密聚焦的原則來管理裝置安全性設定**。  每個[端點安全性原則](#use-policies-to-manage-device-security)都注重於裝置安全性的各個層面，例如防毒軟體、磁碟加密、防火牆及透過與 Defender ATP 整合所提供的數個區域。

- **透過合規性政策來建立裝置和使用者需求**。 使用[合規性政策](../protect/device-compliance-get-started.md)時，您可以設定裝置和使用者必須符合才能視為符合規範的規則。 規則可能包含 OS 版本、密碼需求、裝置威脅層級等等。

  當您整合 Azure Active Directory (Azure AD) [條件式存取原則](#configure-conditional-access)以施行合規性政策時，您可以控制受控裝置及未受控裝置對公司資源的存取權。

- **將 Intune 與您的 Microsoft Defender ATP 小組整合**。 [與 Defender ATP 整合](#set-up-integration-with-defender-atp)可讓您存取[安全性工作](#review-security-tasks-from-defender-atp)。 安全性工作會將 Defender ATP 和 Intune 緊密結合，以協助您的安全性小組找出具風險裝置，並將詳細的補救步驟傳遞給 Intune 系統管理員以便採取行動。

本文下列章節將討論您可從系統管理中心端點安全性節點執行的不同工作，以及所需的角色型存取控制 (RBAC) 權限。

## <a name="manage-devices"></a>管理裝置

端點安全性節點包含「所有裝置」檢視，您可以在其中從 Azure AD 檢視 Microsoft 端點管理員提供的所有裝置清單。

在此檢視中，您可以選取要鑽研的裝置以取得詳細資訊，例如裝置不符合哪些原則。 您也可以使用此檢視的存取權來補救裝置問題，包括重新啟動裝置、啟動惡意程式碼掃描或在 Windows 10 裝置上輪替 BitLocker 金鑰。

如需詳細資訊，請參閱[使用 Microsoft Intune 的端點安全性管理裝置](../protect/endpoint-security-manage-devices.md)。

## <a name="manage-security-baselines"></a>管理安全性基準

Intune 安全性基準是預先設定的設定群組，這些設定是產品相關 Microsoft 安全性小組的最佳做法建議。 Intune 支援 Windows 10 裝置設定、Microsoft Edge、Microsoft Defender 進階威脅防護等的安全性基準。

您可以使用安全性基準，快速部署裝置和應用程式設定的「最佳做法」設定，以保護您的使用者和裝置。 執行 Windows 10 1809 版及更新版本的裝置支援安全性基準。

如需詳細資訊，請參閱[在 Intune 中使用安全性基準來設定 Windows 10 裝置](../protect/security-baselines.md)。

安全性基準是 Intune 中數種方法的其中一種，用於設定裝置上的設定。 管理設定時，請務必了解您的環境使用哪些其他方法來設定裝置，以避免造成衝突。 請參閱本文後面的[避免原則衝突](#avoid-policy-conflicts)。

## <a name="review-security-tasks-from-defender-atp"></a>檢閱 Defender ATP 的安全性工作

當您整合 Intune 與 Microsoft Defender Advanced 威脅防護 (Defender ATP) 時，您可以在 Intune 中檢閱可識別具風險裝置並提供步驟來降低風險的「安全性工作」。 然後您可以使用這些工作，在成功降低這些風險時回報給 Defender ATP。

- 您的 Defender ATP 小組會判斷有哪些裝置具風險，並將該資訊傳遞給您的 Intune 小組作為安全性工作。 只需要按幾下，他們就能建立 Intune 的安全性工作，可識別具風險裝置、弱點並提供如何降低風險的指引。

- Intune 系統管理員會檢閱安全性工作，然後在 Intune 內採取行動來補救這些工作。 降低風險後，他們會將工作設定為完成，即會將該狀態傳回 Defender ATP 小組。

透過安全性工作，這兩個小組會對於哪些裝置具風險、這些風險的補救方式和時機方面保持同步。

若要深入了解如何使用安全性工作，請參閱[使用 Intune 來補救 Microsoft Defender ATP 識別出的弱點](../protect/atp-manage-vulnerabilities.md)。

## <a name="use-policies-to-manage-device-security"></a>使用原則來管理裝置安全性

身為安全性系統管理員，請使用端點安全性節點中「管理」下方的安全性原則。 使用這些原則後，您就可以設定裝置安全性，而不需承擔從裝置組態設定檔和安全性基準瀏覽較大主體與設定範圍的額外負荷。

![管理原則](./media/endpoint-security/endpoint-security-policies.png)

若要深入了解如何使用這些安全性原則，請參閱[使用端點安全性原則來管理裝置安全性](../protect/endpoint-security-policy.md)。

端點安全性原則是 Intune 中數種方法的其中一種，用於設定裝置上的設定。 管理設定時，請務必了解您的環境使用哪些其他方法來設定裝置，以避免造成衝突。 請參閱本文後面的[避免原則衝突](#avoid-policy-conflicts)。

也請參閱「管理」下方的「裝置合規性」及「條件式存取」原則。 這些原則類型並不是用於設定端點的重點安全性原則，而是管理裝置及存取公司資源的重要工具。

## <a name="use-device-compliance-policy"></a>使用裝置合規性政策

使用裝置合規性政策來建立條件，讓裝置和使用者存取您的網路和公司資源。

[可用的合規性設定](../protect/device-compliance-get-started.md#next-steps)取決於您使用的平台，但常見的原則規則包括：

- 需要裝置執行最低或特定的 OS 版本
- 設定密碼需求
- 指定允許的裝置威脅層級上限，由 Defender ATP 或其他行動威脅防禦合作夥伴來決定

除了原則規則外，合規性政策也支援：

- 您在 Intune 中定義的[位置](../protect/use-network-locations.md)。 當您以合規性政策使用位置時，政策可以確保裝置連線到工作網路以符合規範。
- [處理不符合規範狀況的動作](../protect/actions-for-noncompliance.md)。 這些動作是依時間排序的一系列動作，適用於不符合規範的裝置。 這些動作包括傳送電子郵件或通知以警示裝置使用者有關不符合規範的資訊、遠端鎖定裝置，甚至淘汰不符合規範的裝置，並移除任何可能存在的公司資料。

當您整合 Intune 與 Azure AD [條件式存取原則](#configure-conditional-access)以施行合規性政策時，條件式存取可以使用合規性資料來控制受控裝置及未受控裝置對公司資源存取的存取權。

若要深入了解，請參閱[在裝置上設定規則以允許在您的組織中使用 Intune 存取資源](../protect/device-compliance-get-started.md)。

裝置合規性政策是 Intune 中數種方法的其中一種，用於設定裝置上的設定。 管理設定時，請務必了解您的環境使用哪些其他方法來設定裝置，以避免造成衝突。 請參閱本文後面的[避免原則衝突](#avoid-policy-conflicts)。

## <a name="configure-conditional-access"></a>設定條件式存取

若要保護您的裝置和公司資源，您可以搭配 Intune 使用 Azure Active Directory (Azure AD) 條件式存取原則。

Intune 會將裝置合規性政策的結果傳遞至 Azure AD，然後使用條件式存取原則來施行哪些裝置和應用程式可存取您的公司資源。 條件式存取原則可以協助您控制不受 Intune 管理之裝置的存取權。 您甚至可以使用與 Intune 整合之[行動威脅防禦合作夥伴](../protect/mobile-threat-defense.md)的合規性詳細資料。

下列為搭配 Intune 使用條件式存取的兩種常見方法：

- **裝置型條件式存取**，可確保只有受控及合規的裝置可以存取網路資源。
- **應用程式型條件式存取**，其使用應用程式防護原則來管理使用者在您未使用 Intune 進行管理的裝置上，對網路資源的存取權。

若要深入了解如何搭配 Intune 使用條件式存取，請參閱[了解條件式存取和 Intune](../protect/conditional-access.md)。

## <a name="set-up-integration-with-defender-atp"></a>設定與 Defender ATP 的整合

當您將 Microsoft Defender 進階威脅防護 (Defender ATP) 與 Intune 整合時，您可以改善識別及回應風險的能力。

雖然 Intune 可以與數個[行動威脅防禦合作夥伴](../protect/mobile-threat-defense.md)整合，但是當您使用 Defender ATP 時，Defender ATP 將能與 Intune 的緊密整合，並可存取深層的裝置保護選項，包括：

- 安全性工作 - 在 ATP 與 Intune 管理員之間，能對具風險裝置、如何補救這些裝置及確認已降低這些風險時進行順暢通訊。
- 在用戶端上簡化 Defender ATP 的上線。
- 在 Intune 合規性政策中使用 ATP 裝置風險訊號。
- 使用「篡改防護」功能。

 若要深入了解如何搭配 Intune 使用 Defender ATP，請參閱[在 Intune 中使用條件式存取強制執行 Microsoft Defender ATP 的合規性](../protect/advanced-threat-protection.md)。

## <a name="role-based-access-control-requirements"></a>角色型存取控制需求

若要管理 Microsoft 端點管理員系統管理中心端點安全性節點的工作，帳戶必須：

- 受指派 Intune 的授權。
- 讓角色型存取控制 (RBAC) 權限等同於**端點安全性管理員**內建 Intune 角色所提供的權限。 「端點安全性管理員」角色會授與存取 Microsoft 端點管理員系統管理中心的權限。 此角色可供負責管理安全性與合規性功能的人員使用，包括安全性基準、裝置合規性、條件式存取與 Microsoft Defender ATP。

如需詳細資訊，請參閱[使用 Microsoft Intune 的角色型存取控制 (RBAC)](../fundamentals/role-based-access-control.md)

### <a name="permissions-granted-by-the-endpoint-security-manager-role"></a>「端點安全性管理員」角色授與的權限

您可以在 Microsoft 端點管理員系統管理中心內前往 [租用戶管理] > [角色] > [所有角色]，選取 [端點安全性管理員] > [屬性]，以檢視下列權限的清單。

**權限：**

- **Android for work**
  - 讀取
- **稽核資料**
  - 讀取
- **公司裝置識別碼**
  - 讀取
- **裝置相容性原則**
  - 指派
  - 建立
  - 刪除
  - 讀取
  - 更新
  - 檢視報表
- **服務設定**
  - 讀取
- **裝置註冊管理員**
  - 讀取
- **Endpoint Protection 報告**
  - 讀取
- **註冊計劃**
  - 讀取裝置
  - 讀取設定檔
  - 讀取權杖
- **Intune 資料倉儲**
  - 讀取
- **受管理的應用程式**
  - 讀取
- **受管理的裝置**
  - 刪除
  - 讀取
  - 設定主要使用者
  - 更新
- **行動應用程式**
  - 讀取
- **組織**
  - 讀取
- **PolicySets**
  - 讀取
- **遠端協助**
  - 讀取
- **遠端工作**
  - 取得 FileVault 金鑰。
- **角色**
  - 讀取
- **安全性基準**
  - 指派
  - 建立
  - 刪除
  - 讀取
  - 更新
- **安全性工作**
  - 讀取
  - 更新
- **電信費用**
  - 讀取
- **條款及條件**
  - 讀取

## <a name="avoid-policy-conflicts"></a>避免原則衝突

您能夠為裝置設定的許多設定，都可以透過 Intune 中的不同功能來管理。 這些功能包括 (但不限於)：

- 端點安全性原則
- 安全性基準
- 裝置設定原則
- Windows 10 註冊原則

例如，端點安全性原則中的設定，是可在 *Endpoint Protection* 中找到的設定子集，以及裝置設定原則中的「裝置限制」設定檔，並且這些也可透過各種安全性基準來管理。

避免衝突的其中一種方法，是不使用不同基準、不使用相同基準的執行個體，或不使用不同原則類型和執行個體來管理裝置上的相同設定。 這需要規劃要用於將設定部署至不同裝置的方法。 當您使用多種方法或相同方法的執行個體來設定相同設定時，請確認您的不同方法不會衝突，或不部署到相同的裝置。

如果發生衝突，您可以使用 Intune 內建工具來識別及解決這些衝突的來源。 如需詳細資訊，請參閱：

- [針對 Intune 中的原則和設定檔進行疑難排解](../configuration/troubleshoot-policies-in-microsoft-intune.md)
- [監視您的安全性基準](../protect/security-baselines-monitor.md#troubleshoot-using-per-setting-status)

## <a name="next-steps"></a>後續步驟

設定：

- [安全性基準](../protect/security-baselines.md)
- [合規性原則](../protect/device-compliance-get-started.md)
- [條件式存取原則](#configure-conditional-access)
- [與 Defender ATP 整合](../protect/advanced-threat-protection.md)
