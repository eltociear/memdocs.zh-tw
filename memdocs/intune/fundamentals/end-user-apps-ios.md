---
title: iOS/iPadOS 使用者如何取得其應用程式
description: 讓終端使用者可以使用 iOS/iPadOS 應用程式的方法
keywords: ''
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 03/11/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 7e3135c1-df26-48c9-aa4c-cdab6168897a
ms.reviewer: aanavath
ms.suite: ems
search.appverid: MET150
ms.custom: intune-classic
ms.collection: M365-identity-device-management
ms.openlocfilehash: 957c63c760dcc576ab30bb85440d52833307818d
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/13/2020
ms.locfileid: "79344086"
---
# <a name="how-your-iosipados-users-get-their-apps"></a>iOS/iPadOS 使用者如何取得其應用程式

使用這項資訊，了解您的使用者取得您透過 Microsoft Intune 散發之應用程式的方式和位置。

**必要的應用程式** - 依據不同的平台，系統管理員所需且安裝在最少使用者介入之裝置上的應用程式。

**可用的應用程式** - 公司入口網站應用程式清單中所提供且使用者可選擇性地選擇要安裝的應用程式。

**受管理的應用程式** - 可透過原則進行管理的應用程式，以及已由 Intune「包裝」或已透過 Intune 應用程式軟體開發套件 (SDK) 建置的應用程式。 這些應用程式可由 Intune 管理，並套用應用程式保護原則。

**非受控的應用程式** - 使用者可從 iOS/iPadOS App Store (未與 Intune 應用程式 SDK 整合) 下載的應用程式 。 Intune 無法控制這些應用程式的散發、管理或選擇性抹除。  

已註冊的使用者可在公司入口網站應用程式的 [應用程式] 畫面上點選下列磚，以取得他們的應用程式：

- [所有應用程式]  會指向[公司入口網站](https://portal.manage.microsoft.com) [所有] 索引標籤中所有應用程式的清單。

- [精選應用程式]  則將使用者帶往公司入口網站的 [精選] 索引標籤。

- [類別]  會指向公司入口網站的 [類別] 索引標籤。

![iOS 公司入口網站應用程式畫面](./media/end-user-apps-ios/ios-cp-app-main-apps-screen.png)

如需如何新增應用程式的資訊，請參閱[如何將應用程式新增至 Microsoft Intune](../apps/apps-add.md)。

## <a name="app-management-takeover"></a>應用程式管理接管
如果應用程式已安裝在終端使用者的裝置上，則 iOS/iPadOS 裝置會顯示警示以允許組織管理應用程式。 終端使用者必須允許組織接管應用程式，才能將應用程式設定套用至受控裝置。 如果使用者取消警示，只要裝置受控且已指派應用程式，警示就會定期出現。  


![[應用程式管理變更] 警示的影像，其中顯示 [取消] 和 [管理] 選項。](./media/end-user-apps-ios/intune-app-management-confirmation-2002.png)

## <a name="see-also"></a>請參閱  

[Android 使用者如何取得其應用程式](end-user-apps-android.md)

[Windows 使用者如何取得其應用程式](end-user-apps-windows.md)
