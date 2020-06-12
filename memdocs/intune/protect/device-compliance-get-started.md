---
title: Microsoft Intune 中的裝置合規性原則 - Azure | Microsoft Docs
description: 開始使用合規性原則，包括 Microsoft Intune 的合規性原則設定和裝置合規性原則。
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 05/28/2020
ms.topic: overview
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.reviewer: samyada
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 227a44436f4490c9b3e2188609a9714a0e842149
ms.sourcegitcommit: eb51bb38d484e8ef2ca3ae3c867561249fa413f3
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/29/2020
ms.locfileid: "84206310"
---
# <a name="use-compliance-policies-to-set-rules-for-devices-you-manage-with-intune"></a>使用合規性原則為使用 Intune 管理的裝置設定規則

像 Intune 這樣的行動裝置管理 (MDM) 解決方案，會藉由要求使用者和裝置符合一些需求，以協助保護組織資料。 在 Intune 中，此功能稱為「合規性原則」。

Intune 中的合規性原則：

- 定義使用者和裝置必須符合的規則和設定。
- 包括適用於不合規裝置的動作。 對不合規情形採取的動作可向使用者警示不合規的情況，並保護不合規裝置上的資料。
- 可[與條件式存取結合](#integrate-with-conditional-access)，以封鎖不符合規則的使用者和裝置。

Intune 的合規性原則分為兩部分：

- **合規性原則設定** – 全租用戶設定，就像是每部裝置都會收到的內建合規性原則。 合規性原則設定會設定您 Intune 環境中，合規性原則運作方式的基準，包括尚未收到任何裝置合規性原則的裝置是否合規。

- **裝置合規性原則** – 您設定並部署到使用者或裝置群組的平台特定規則。  這些規則會定義對裝置的要求，例如最低作業系統或使用磁碟加密。 裝置必須符合這些規則才算合規。

像其他 Intune 原則一樣，裝置的合規性原則評估會隨裝置簽入 Intune 的時間，以及[原則和設定檔重新整理週期](../configuration/device-profile-troubleshoot.md#how-long-does-it-take-for-devices-to-get-a-policy-profile-or-app-after-they-are-assigned)而定。

## <a name="compliance-policy-settings"></a>相容性原則設定

「合規性原則設定」是全租用戶的設定，可決定 Intune 合規性服務與您裝置的互動方式。 這些設定與您在裝置合規性原則中所設定的內容不同。

若要管理合規性原則設定，請登入 [Microsoft 端點管理員系統管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)，移至 [端點安全性] > [裝置合規性] > [合規性原則設定]。

合規性原則設定包括下列設定：

- **將未指派合規性原則的裝置標記為**

  此設定會決定 Intune 如何處理尚未指派裝置合規性原則的裝置。 此設定有兩個值：
  - [合規] (「預設值」)：這項安全性功能已關閉。 未收到裝置合規性原則的裝置即視為「合規」。
  - [不合規]：這項安全性功能已開啟。 未收到裝置合規性原則的裝置即視為「不合規」。

  如果對裝置合規性原則使用條件式存取，建議您將此設定變更為 [不合規]，以確保只有確認為合規的裝置才能存取您的資源。

  如果使用者因未獲得指派原則而不符合規範，則[公司入口網站應用程式](../apps/company-portal-app.md)就會顯示「未指派任何合規性原則」。

- **加強的越獄偵測** (僅適用於 *iOS/iPadOS*)

  此設定只會影響您以裝置合規性原則鎖定目標的裝置，而此原則可封鎖越獄裝置。  (請參閱 iOS/iPadOS 的[裝置健全狀況](compliance-policy-create-ios.md#device-health)設定。)

  此設定有兩個值：

  - [停用] (「預設值」)：這項安全性功能已關閉。 此設定對收到合規性原則的裝置無效，此原則可封鎖越獄裝置。
  - **啟用**：這項安全性功能已開啟。 收到封鎖越獄裝置之裝置合規性原則的裝置，會使用增強的越獄偵測。

  在適用的 iOS/iPadOS 裝置上啟用時，裝置會：

  - 啟用 OS 層級的位置服務。
  - 一律允許公司入口網站使用位置服務。
  - 更頻繁地使用其位置服務，在背景中觸發越獄偵測。 Intune 不會儲存使用者位置資料。

  增強的越獄偵測會在發生下列情況時執行評估：

  - 公司入口網站應用程式開啟時
  - 裝置會實際移動一段相當距離，約 500 公尺或更多。 Intune 無法保證每次顯著的位置變更都會執行越獄偵測檢查，因為這取決於裝置當時的網路連線。

  在 iOS 13 和更新版上，只要裝置提示使用者繼續允許公司入口網站在背景中使用其位置，此功能就會要求使用者選取 [一律允許]。 如果使用者不一律允許位置存取，也不設定有此設定的原則，其裝置即會標示為不合規。

- **合規性狀態有效期限 (天)**

  指定裝置必須成功報告所有收到的合規性原則的期間。 如果裝置在有效期到期之前，無法報告其原則合規性狀態，該裝置即會視為不合規。

  根據預設，期間設為 30 天。 您可以設定 1 到 120 天的期間。

  您可以檢視有效期設定中的裝置合規性詳細資料。 登入 [Microsoft 端點管理員系統管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)，移至 [裝置] > [監視] > [設定合規性]。 此設定在 [設定] 資料行中的名稱為**作用中**。  如需此設定及相關合規性狀態檢視的詳細資訊，請參閱[監視裝置合規性](compliance-policy-monitor.md)。

## <a name="device-compliance-policies"></a>裝置合規性原則

Intune 裝置合規性原則：

- 定義使用者和受控裝置必須符合才視為合規的規則和設定。 規則範例包括要求裝置執行最低 OS 版本、不被越獄中斷或 root 破解，以及位於或低於已與 Intune 整合之威脅管理軟體所指定的「威脅等級」。
- 支援適用不符合合規性規則裝置的這些動作。 動作的範例包括遠端鎖定，或將有關裝置狀態的電子郵件傳送給裝置使用者，以便修正問題。
- 部署至使用者群組中的使用者，或裝置群組中的裝置。 將合規性原則部署到使用者後，即會檢查該使用者所有裝置是否合規。 在此案例中使用裝置群組可協助進行合規性報告。

如果使用條件式存取，您的條件式存取原則就可以使用您的裝置合規性結果，封鎖不合規裝置對資源的存取。

您可以在裝置合規性原則中指定的可用設定，取決於您在建立原則時所選取的平台類型。 不同的裝置平台支援不同的設定，而每種平台類型都需要各自的原則。  

下列主題會連結到裝置設定原則不同層面的專文。

- [**針對不合規的動作**](actions-for-noncompliance.md)：每項裝置合規性原則都包含一或多個不合規的動作。 這些動作是要套用到不符合原則所設定條件之裝置的規則。

  根據預設，每項裝置合規性原則都會包含當裝置不符合原則規則時，將裝置標示為不合規的動作。 接著，原則會根據您為這些動作設定的排程，將您針對不合規設定的其他動作，套用至裝置。

  對不合規情形採取的動作可在使用者裝置不合規時向他們發出警示，或保護可能在裝置上的資料。 動作範例包括：

  - **傳送電子郵件警示**給使用者和群組，提供不合規裝置的詳細資料。 您可以設定原則，在裝置標示為不合規時立即傳送電子郵件，並定期重複傳送電子郵件，直到裝置符合規範為止。
  - **從遠端鎖定**已經不符合規範一段時間的裝置。
  - **淘汰**已經不符合規範一段時間的裝置。 此動作會從 Intune 管理移除裝置，並移除裝置中的所有公司資料。

- [**設定網路位置**](use-network-locations.md)：Android 裝置支援此功能，您可以設定「網路位置」，然後使用這些位置作為裝置合規性規則。 當裝置不在或離開指定的網路時，這種類型的規則會將裝置標示為不符合規範。 您必須先設定網路位置，才可以指定位置規則。

- [**建立原則**](create-compliance-policy.md)：您可以利用本文的資訊，檢閱必要條件、逐一完成設定規則的選項、針對不合規指定動作，以及將原則指派給群組。 本文也包含原則更新次數的相關資訊。

  請檢視不同裝置平台的裝置合規性設定：

  - [Android](compliance-policy-create-android.md)
  - [Android Enterprise](compliance-policy-create-android-for-work.md)
  - [iOS](compliance-policy-create-ios.md)
  - [macOS](compliance-policy-create-mac-os.md)
  - [Windows Holographic for Business](compliance-policy-create-windows.md#windows-holographic-for-business)
  - [Windows Phone 8.1](compliance-policy-create-windows-8-1.md)
  - [Windows 8.1 及更新版本](compliance-policy-create-windows-8-1.md)
  - [Windows 10 及以上版本](compliance-policy-create-windows.md)

## <a name="monitor-compliance-status"></a>監視合規性狀態

您可使用 Intune 的裝置合規性儀表板，監視裝置的合規性狀態，以及深入了解原則和裝置的詳細資訊。 若要深入了解此儀表板，請參閱[監視裝置合規性](compliance-policy-monitor.md)。

## <a name="integrate-with-conditional-access"></a>與條件式存取整合

當您使用條件式存取時，您可以設定條件式存取原則使用裝置合規性原則的結果，判斷哪些裝置可以存取您的組織資源。 此存取控制也獨立於您裝置合規性原則所包含的針對不合規動作之外。

當裝置在 Intune 中註冊時，會使用 Azure AD 註冊。 裝置的合規性狀態會回報給 Azure AD。 如果您的條件式存取原則已將存取控制設定為「需要將裝置標示為合規」，則條件式存取會使用該合規性狀態，決定要授與或封鎖對電子郵件和其他組織資源的存取。

如果要使用裝置合規性狀態搭配條件式存取原則，請檢查租用戶設定「將未指派合規性原則的裝置標記為」的方式，這可以在[合規性原則設定](#compliance-policy-settings)下管理。

如需使用條件式存取搭配裝置合規性原則的詳細資訊，請參閱 [裝置型條件式存取](conditional-access-intune-common-ways-use.md#device-based-conditional-access)

深入了解 Azure AD 文件中的條件式存取：

- [何謂條件式存取](https://docs.microsoft.com/azure/active-directory/conditional-access/overview)
- [何謂裝置身分識別](https://docs.microsoft.com/azure/active-directory/device-management-introduction)

### <a name="reference-for-non-compliance-and-conditional-access-on-the-different-platforms"></a>有關不同平台的不合規及條件式存取參考

下表描述搭配條件式存取原則使用合規性政策與時，系統如何管理不符合規範的設定。

- **已補救**：裝置作業系統強制符合規範。 例如，強制使用者設定 PIN。

- **已隔離**：裝置作業系統不強制符合規範。 例如，Android 和 Android Enterprise 裝置不強制使用者為裝置加密。 裝置不符合規範時，會採取下列動作：
  - 如果條件式存取原則適用於使用者，就會封鎖裝置。
  - 公司入口網站應用程式會通知使用者任何合規性問題的相關事項。

---------------------------

|**原則設定**| **平台** |
| --- | ----|
| **PIN 或密碼設定** | - **Android 4.0 及更新版本**：已隔離<br>- **Samsung Knox Standard 4.0 及更新版本**：已隔離<br>- **Android Enterprise**：已隔離  <br>  <br>- **iOS 8.0 及更新版本**：已修復<br>- **macOS 10.11 及更新版本**：已修復  <br>  <br>- **Windows 8.1 及更新版本**：已修復<br>- **Windows Phone 8.1 及更新版本**：已修復|
| **裝置加密** | - **Android 4.0 及更新版本**：已隔離<br>- **Samsung Knox Standard 4.0 及更新版本**：已隔離<br>- **Android Enterprise**：已隔離<br><br>- **iOS 8.0 及更新版本**：已修復 (藉由設定 PIN 碼)<br>- **macOS 10.11 及更新版本**：已修復 (藉由設定 PIN 碼)<br><br>- **Windows 8.1 及更新版本**：不適用<br>- **Windows Phone 8.1 及更新版本**：已修復 |
| **已越獄或 Root 的裝置** | - **Android 4.0 及更新版本**：隔離 (非設定)<br>- **Samsung Knox Standard 4.0 及更新版本**：隔離 (非設定)<br>- **Android Enterprise**：隔離 (非設定)<br><br>- **iOS 8.0 及更新版本**：隔離 (非設定)<br>- **macOS 10.11 及更新版本**：不適用<br><br>- **Windows 8.1 及更新版本**：不適用<br>- **Windows Phone 8.1 及更新版本**：不適用 |
| **電子郵件設定檔** | - **Android 4.0 及更新版本**：不適用<br>- **Samsung Knox Standard 4.0 及更新版本**：不適用<br>- **Android Enterprise**：不適用<br><br>- **iOS 8.0 及更新版本**：已隔離<br>- **macOS 10.11 及更新版本**：已隔離<br><br>- **Windows 8.1 及更新版本**：不適用<br>- **Windows Phone 8.1 及更新版本**：不適用 |
| **最低 OS 版本** | - **Android 4.0 及更新版本**：已隔離<br>- **Samsung Knox Standard 4.0 及更新版本**：已隔離<br>- **Android Enterprise**：已隔離<br><br>- **iOS 8.0 及更新版本**：已隔離<br>- **macOS 10.11 及更新版本**：已隔離<br><br>- **Windows 8.1 及更新版本**：已隔離<br>- **Windows Phone 8.1 及更新版本**：已隔離 |
| **最高 OS 版本** | - **Android 4.0 及更新版本**：已隔離<br>- **Samsung Knox Standard 4.0 及更新版本**：已隔離<br>- **Android Enterprise**：已隔離<br><br>- **iOS 8.0 及更新版本**：已隔離<br>- **macOS 10.11 及更新版本**：已隔離<br><br>- **Windows 8.1 及更新版本**：已隔離<br>- **Windows Phone 8.1 及更新版本**：已隔離 |
| **Windows 健康情況證明** | - **Android 4.0 及更新版本**：不適用<br>- **Samsung Knox Standard 4.0 及更新版本**：不適用<br>- **Android Enterprise**：不適用<br><br>- **iOS 8.0 及更新版本**：不適用<br>- **macOS 10.11 及更新版本**：不適用<br><br>- **Windows 10 和 Windows 10 Mobile**：已隔離<br>- **Windows 8.1 及更新版本**：已隔離<br>- **Windows Phone 8.1 及更新版本**：不適用 |

---------------------------

## <a name="next-steps"></a>後續步驟

- [設定位置](../protect/use-network-locations.md)以搭配 Android 裝置使用
- [建立並部署原則](../protect/create-compliance-policy.md)以及審核必要條件
- [監視裝置合規性](../protect/compliance-policy-monitor.md)
- [Microsoft Intune 裝置原則和設定檔的常見疑問、問題和解決方式](../configuration/device-profile-troubleshoot.md)
- 如需有關 Intune 資料倉儲原則實體的相關資訊，請參閱[原則實體的參考](../developer/reports-ref-policy.md)
