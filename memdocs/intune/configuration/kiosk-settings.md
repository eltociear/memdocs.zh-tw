---
title: Microsoft Intune 中適用於 Windows 和全像攝影版裝置的 Kiosk 設定 - Azure | Microsoft Docs
description: 在 Microsoft Intune 中，將您的 Windows 10 (和更新版本) 與 Windows Holographic for Business 裝置設定為單一應用程式和多應用程式 Kiosk、自訂 [開始] 功能表、新增應用程式、顯示工作列，以及設定網頁瀏覽器。
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 05/13/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: high
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure; seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: a9be644a47a361cf29e7b7132b2c87a4921553ea
ms.sourcegitcommit: 302556d3b03f1a4eb9a5a9ce6138b8119d901575
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/27/2020
ms.locfileid: "83989439"
---
# <a name="windows-10-and-windows-holographic-for-business-device-settings-to-run-as-a-dedicated-kiosk-using-intune"></a>使用 Intune 以專用 Kiosk 執行的 Windows 10 和 Windows Holographic for Business 裝置設定

在 Windows 10 裝置上，使用 Intune 執行裝置作為 kiosk，有時也稱為專用裝置。 Kiosk 模式中的裝置可以執行一或多個應用程式。 您可以顯示和自訂 [開始] 功能表、新增不同的應用程式 (包括 Win32 應用程式)、將特定首頁新增至網頁瀏覽器，以及執行更多作業。 

本功能適用於：

- Windows 10 及更新版本
- Windows Holographic for Business

若要建立其他平台的 kiosk 設定檔，請參閱 [Android 裝置系統管理員](device-restrictions-android.md#kiosk)、[Android Enterprise](device-restrictions-android-for-work.md#dedicated-devices) 和 [iOS/iPadOS](device-restrictions-ios.md#kiosk)。

Intune 針對每部裝置支援一個 kiosk 設定檔。 如果您需要在單一裝置上有多個 kiosk 設定檔，則可以使用[自訂 OMA-URI](custom-settings-windows-10.md)。

Intune 會使用「組態設定檔」，依據貴組織的需求來建立和自訂這些設定。 當您於設定檔中新增這些功能之後，請將這些設定部署至貴組織中的群組。

本文示範如何建立裝置組態設定檔。 如需所有設定的清單及其用途，請參閱 [Windows 10 Kiosk 設定](kiosk-settings-windows.md)和 [Windows Holographic for Business Kiosk 設定](kiosk-settings-holographic.md)。

## <a name="create-the-profile"></a>建立設定檔

1. 登入 [Microsoft Endpoint Manager 系統管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)。
2. 選取 [裝置] > [組態設定檔] > [建立設定檔]。
3. 輸入下列內容：

   - **平台**：選取 [Windows 10 及更新版本]。
   - **設定檔**：選取 [Kiosk]。

4. 選取 [建立]。
5. 在 [基本資訊] 中，輸入下列內容：

   - **名稱**：為新的設定檔輸入描述性名稱。
   - **描述**：輸入設定檔的描述。 這是選擇性設定，但建議執行。

6. 選取 [下一步]。
7. 在 [組態設定] 中 >  **[選取kiosk 模式]** ，選擇原則支援的 kiosk 模式類型。 這些選項包括：

    - **未設定** (預設)：Intune 不會變更或更新此設定。 不啟用 kiosk 模式的原則。
    - **單一應用程式、全螢幕 kiosk**：裝置以單一使用者帳戶執行，並將其鎖定到單一市集應用程式。 因此當使用者登入時，會啟動特定的應用程式。 此模式也會限制使用者開啟新的應用程式或變更執行中的應用程式。
    - **多應用程式 kiosk**：裝置藉由使用應用程式使用者模型識別碼 (AUMID) 來執行多個市集應用程式、Win32 應用程式或現成的 Windows 應用程式。 只有您新增的應用程式才可在裝置上使用。

        多應用程式 Kiosk (或固定用途裝置) 的優點是讓使用者只存取所需的應用程式，來為他們提供一個簡單明瞭的體驗。 此外，還可從其檢視中移除不需要的應用程式。

    如需所有設定的清單及其用途，請參閱：

      - [Windows 10 Kiosk 設定](kiosk-settings-windows.md)
      - [Windows Holographic for Business Kiosk 設定](kiosk-settings-holographic.md)

8. 選取 [下一步]。

9. 在 [範圍標籤] (選擇性) 中，指派標籤來針對特定 IT 群組篩選設定檔，例如 `US-NC IT Team` 或 `JohnGlenn_ITDepartment`。 如需範圍標籤的詳細資訊，請參閱[針對分散式 IT 使用 RBAC 和範圍標籤](../fundamentals/scope-tags.md)。

    選取 [下一步]。

10. 在 [指派] 中，選取將會收到您設定檔的使用者或使用者群組。 如需指派設定檔的詳細資訊，請參閱[指派使用者和裝置設定檔](device-profile-assign.md)。

    選取 [下一步]。

11. 在 [檢閱 + 建立] 中，檢閱您的設定。 當您選取 [建立] 時，系統會儲存您的變更，然後指派設定檔。 原則也會顯示在設定檔清單中。

當每個裝置下次簽入時，就會套用原則。

## <a name="next-steps"></a>後續步驟

[指派設定檔](device-profile-assign.md)後，[監視其狀態](device-profile-monitor.md)。

您可以針對執行下列平台的裝置建立 kiosk 設定檔：

- [Android 裝置系統管理員](device-restrictions-android.md#kiosk)
- [Android Enterprise](device-restrictions-android-for-work.md#dedicated-devices)
- [Windows 10 及以上版本](kiosk-settings-windows.md)
- [Windows Holographic for Business](kiosk-settings-holographic.md)
