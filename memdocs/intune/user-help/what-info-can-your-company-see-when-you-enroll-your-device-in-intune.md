---
title: 當您註冊您的裝置時，貴公司會看到什麼內容？
description: 說明 IT 在您受控裝置上可以看到及不能看到的內容。
keywords: ''
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 06/11/2020
ms.topic: end-user-help
ms.prod: ''
ms.service: microsoft-intune
ms.subservice: end-user
ms.technology: ''
ms.assetid: 12655728-a1af-4d89-97bc-925fe36c0dc4
searchScope:
- User help
ROBOTS: ''
ms.reviewer: esmich
ms.suite: ems
ms.collection: ''
ms.openlocfilehash: 740d9b68a0101e04e6bf690d09ecce7eaff4509e
ms.sourcegitcommit: 3217778ebe7fd0318810696e8931e427a85da897
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2020
ms.locfileid: "85107324"
---
# <a name="what-information-can-my-organization-see-when-i-enroll-my-device"></a>當我註冊裝置時，我的組織可以看到哪些資訊？

當您向 Microsoft Intune 註冊裝置時，組織不會看到您的個人資訊。 當您註冊裝置時，會授與組織檢視裝置上特定資訊的權限，例如裝置型號和序號。 組織會使用這項資訊來協助保護裝置上的公司資料。

**組織絕對不會看到的資訊：**

- 電話和 Web 瀏覽歷程記錄
- 電子郵件和簡訊
- 連絡人
- 行事曆
- 密碼
- 圖片，包括相片應用程式或手機相簿的內容
- 檔案

**組織一律會看到的資訊：**

- 裝置型號，例如 Google Pixel
- 裝置製造商，例如 Microsoft
- 作業系統和版本，例如 iOS 12.0.1
- 應用程式清查和應用程式名稱，例如 Microsoft Word。 在個人裝置上，組織只能看到您的受控應用程式清查。 在公司擁有的裝置上，組織可以看到所有的應用程式清查。
- 裝置擁有者
- 裝置名稱
- 裝置序號
- IMEI

 > [!NOTE]
 > 針對 Android Enterprise 完全受控和專用裝置，您將無法看到所有應用程式清查。
 
 > [!NOTE]
 > 以下列其中一種方式安裝的應用程式會被視為**受控應用程式**：
 > 1. 在 Intune 系統管理員發佈為**可用**之後，使用者可從公司入口網站應用程式安裝的應用程式。
 > 2. Intune 系統管理員將此應用程式發佈為**必要**，且安裝在裝置上。 
 >
 > 若您是組織中的 IT 系統管理員或支援人員，而且想要了解在 Intune 中管理應用程式的詳細資訊，請參閱[了解非受控應用程式、受控應用程式和 MAM 應用程式的功能](https://techcommunity.microsoft.com/t5/enterprise-mobility-security/understanding-the-capabilities-of-unmanaged-apps-managed-apps/ba-p/249164) (英文)。
    
**組織可能會看到的資訊：**

- 電話號碼：針對公司所擁有的裝置，組織可以看到您完整的電話號碼。 如果是個人所擁有的裝置，組織便只能看到電話號碼的最後四個數字。 您可在個別裝置的 [裝置詳細資料] 頁面上看到每個個別裝置的所有權類型。
- 裝置儲存空間：如果您無法安裝必要的應用程式，組織可以查看裝置儲存空間，以了解是否是空間不足。  
- 位置：在公司擁有的裝置上，組織可以看到遺失的裝置位置。 至於個人擁有的裝置，除非嘗試尋找遺失的受監督 iOS 裝置，否則您的組織看不到裝置位置。 請瀏覽 [Apple iOS 文件](https://go.microsoft.com/fwlink/?linkid=853816)，以深入了解受監督的裝置。  
- 應用程式清查詳細資料：如果您的組織使用 Mobile Threat Defense，他們將能夠檢視您 iOS 裝置上應用程式的相關詳細資料。 深入了解 [Mobile Threat Defense](set-up-mobile-threat-defense.md)。 否則，在個人擁有的裝置上，組織只能看到您的受控應用程式清查。 對於公司擁有的裝置，組織可以看到所有的應用程式清查。
- 網路資訊：有些與 Android 裝置網路連線相關的資訊，可能會提供給您組織的支援人員。 例如，如果您的組織要求裝置保留在某個建築物內，則您的裝置會識別網路連線位置。 
