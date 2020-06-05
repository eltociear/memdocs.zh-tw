---
title: 註冊 iOS/iPadOS 裝置 - 使用者註冊
titleSuffix: Microsoft Intune
description: 了解如何設定 iOS/iPadOS 與 iPadOS 使用者註冊。
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 10/2/2019
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: tisilver
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure;seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: 5d98f3f8205490848d9f5137e97e7796eee67a67
ms.sourcegitcommit: 7a5196d4d9736c5cd52a23155c479523e52a097d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/05/2020
ms.locfileid: "84436766"
---
# <a name="set-up-iosipados-and-ipados-user-enrollment-preview"></a>設定 iOS/iPadOS 與 iPadOS 使用者註冊 (預覽)

您可以設定 Intune 使用 Apple 的使用者註冊程序來註冊 iOS/iPadOS 與 iPadOS 裝置。 相較於其他註冊方法，使用者註冊會提供一組簡單好用的管理選項子集給管理員。

如需有關使用者註冊中提供哪些選項的詳細資訊，請參閱[使用者註冊支援的動作、密碼和其他選項](ios-user-enrollment-supported-actions.md)。

> [!NOTE]
> Intune 中對 Apple 使用者註冊的支援目前為預覽狀態。

## <a name="prerequisites"></a>先決條件
- [行動裝置管理 (MDM) 授權單位](../fundamentals/mdm-authority-set.md)
- [Apple MDM Push Certificate](apple-mdm-push-certificate-get.md)

## <a name="create-a-user-enrollment-profile-in-intune"></a>在 Intune 中建立使用者註冊設定檔

註冊設定檔會定義要在註冊期間套用至裝置群組的設定。 

1. 在 [Microsoft 端點管理員系統管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)內，選擇 [裝置] > [iOS] > [iOS 註冊] > [註冊類型 (預覽)] > [建立設定檔] > [iOS/iPadOS]。 您可以使用此設定檔指出 iOS/iPadOS 與 iPadOS 終端使用者將會在非透過公司 Apple 方法註冊的裝置上擁有什麼註冊體驗。 如果您想要變更，可以在建立設定檔之後加以編輯。

    ![建立 Apple 註冊設定檔](./media/ios-user-enrollment/create-profile.png)

2. 在 [基本] 頁面上，為設定檔輸入系統管理用的**名稱**與**描述**。 使用者看不到這些詳細資料。 您可以使用此 [名稱] 欄位，在 Azure Active Directory 中建立動態群組。 設定檔名稱可用來定義 enrollmentProfileName 參數，以註冊具備此註冊設定檔的裝置。 深入了解 [Azure Active Directory 動態群組](https://docs.microsoft.com/azure/active-directory/active-directory-groups-dynamic-membership-azure-portal#rules-for-devices)。

    ![基本頁面](./media/ios-user-enrollment/basics-page.png)

3. 選取 [下一步]。

4. 在 [設定] 頁面上，選取下列其中一個 [註冊類型] 選項：

    ![設定頁面](./media/ios-user-enrollment/settings-page.png)

    - **裝置註冊**：此設定檔中的所有使用者都將使用 [裝置註冊]。
    - **使用者註冊**：此設定檔中的所有使用者都將使用 [使用者註冊]。
    - **根據使用者的選擇來決定**：此群組中的所有使用者都可以選擇要使用的註冊類型。 當使用者註冊其裝置時，他們會看到可選擇 [我擁有此裝置] 或 [(公司) 擁有此裝置] 的選項。 如果選擇後者，就會使用裝置註冊來註冊裝置。 如果使用者選擇 [我擁有此裝置]，系統將會提供另一個選項，讓他們選擇要保護整部裝置，或只保護工作相關的應用程式與資料。 終端使用者選擇是否擁有裝置的動作會決定要在其裝置上實作的註冊類型。 Intune 中的「裝置擁有權」屬性也會反映這個使用者選擇項目。 若要深入了解使用者體驗，請參閱[設定 iOS/iPadOS 裝置對公司資源的存取](https://docs.microsoft.com/mem/intune/user-help/enroll-your-device-in-intune-macos-cp) \(英文\)。
    
5. 選取 [下一步]。

6. 在 [指派] 頁面上，選擇包含您要將此設定檔指派給他的使用者在內的使用者群組。 您可以選擇指派設定檔給所有使用者或特定群組。 所選群組中的所有使用者都將會使用上述選擇的註冊類型。 使用者註冊案例不支援裝置群組，因為該功能是以使者身分識別為基礎，而非裝置。 您可以選擇指派設定檔給所有使用者或特定群組。

    ![指派頁面](./media/ios-user-enrollment/assignments-page.png)

7. 選取 [下一步]。

8. 在 [檢閱及建立] 頁面上，檢閱您的選擇，然後選取 [建立] 以將設定檔指派給使用者。

    ![指派頁面](./media/ios-user-enrollment/assignments-page.png)


## <a name="profile-priority"></a>設定檔優先順序

當您建立了多個註冊類型設定檔之後，可以變更它們在套用時的優先順序。

1. 在 [Microsoft 端點管理員系統管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)內，選擇 [裝置] > [iOS] > [iOS 註冊] > [註冊類型 (預覽)]。
2. 以您想要套用的順序，用拖放方式調整設定檔在清單中的位置。

如果任一使用者的設定檔之間產生衝突，系統會為他們套用優先順序較高的設定檔。


