---
title: 使用內部部署 MDM 管理裝置
titleSuffix: Configuration Manager
description: 使用 Configuration Manager 內部部署行動裝置管理（MDM），透過完整抹除、選擇性抹除、遠端鎖定或密碼重設來保護裝置資料。
ms.date: 08/14/2018
ms.prod: configuration-manager
ms.technology: configmgr-mdm
ms.topic: conceptual
ms.assetid: 770da7bd-02dd-474a-9604-93ff1ea0c1e4
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: e9849f3bef5aa67dcc45b00f64487242230edc2e
ms.sourcegitcommit: 578ad1e8088f7065b565e8a4f4619f5a26b94001
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81724722"
---
# <a name="manage-devices-and-protect-data-with-on-premises-mdm-in-configuration-manager"></a>在 Configuration Manager 中使用內部部署 MDM 管理裝置及保護資料

適用於：  Configuration Manager (最新分支)

行動裝置可以儲存敏感性資料，並讓您輕鬆存取許多組織資源。 若要協助保護裝置和資料，請使用 Configuration Manager 進行下列裝置管理動作：

- **完整**抹除：將裝置還原為其原廠設定

- **選擇性**抹除：僅移除組織資料

- **密碼重設**：當使用者忘記密碼時，移除或重設密碼

- **遠端鎖定**：協助保護可能遺失的裝置

## <a name="full-wipe"></a>完整抹除  

當您需要保護遺失的裝置，或當您淘汰裝置以供使用中時，您可以開始對其進行完整抹除。 此動作會將裝置還原為其原廠預設值。 它會移除所有組織和使用者的資料和設定。

1. 在 Configuration Manager 主控台中，移至 [**資產與相容性**] 工作區，然後選擇 [**裝置**] 節點。 您也可以選擇 [**裝置集合**]，然後選取裝置所屬的集合。

1. 選取您要抹除的裝置。

1. 在功能區的 [裝置] 群組中，選取 [**遠端裝置動作**]，然後選擇 [**淘汰/** 抹除]。

1. 在 [**從 Configuration Manager 淘汰**] 視窗中，選取 [抹除行動**裝置並從 Configuration Manager 淘汰**] 選項。

## <a name="selective-wipe"></a>選擇性抹除

若只要從裝置移除組織資料，請啟動選擇性抹除。

### <a name="behaviors-by-os-version"></a>依作業系統版本的行為

下表描述要移除哪些資料，以及在選擇性抹除之後對保留在裝置上的資料有何影響。

#### <a name="windows-10-windows-81-windows-rt-81-and-windows-rt"></a>Windows 10、Windows 8.1、Windows RT 8.1 和 Windows RT

|內容|選擇性抹除行為|  
|-------|--------|
|Configuration Manager 安裝的應用程式和相關聯的資料|它會卸載應用程式，並移除任何側載金鑰。 它會撤銷使用 Windows 選擇性抹除之應用程式的加密金鑰，而且無法再存取該資料。|
|VPN 和 Wi-Fi 設定檔|移除設定檔|
|憑證|移除及撤銷憑證|
|設定|移除需求|
|電子郵件設定檔|移除已啟用 EFS 的電子郵件，其中包含 Windows 電子郵件和附件的郵件應用程式。|

#### <a name="windows-10-mobile-windows-phone-80-and-windows-phone-81"></a>Windows 10 行動裝置版、Windows Phone 8.0 和 Windows Phone 8。1

|內容|選擇性抹除行為|  
|-------|--------|
|Configuration Manager 安裝公司應用程式和相關聯的資料|它會卸載應用程式，並移除組織的應用程式資料。|
|VPN 和 Wi-Fi 設定檔|移除 Windows 10 行動裝置版和 Windows Phone 8.1 的設定檔|
|憑證|移除 Windows Phone 8.1 的憑證|
|電子郵件設定檔|移除設定檔（Windows Phone 8.0 除外）|

Windows 10 行動裝置版和 Windows Phone 8.1 裝置也移除了下列設定︰  

- **需要密碼才可解除鎖定行動裝置**  
- **允許簡單密碼**  
- **密碼長度下限**  
- **必要的密碼類型**
- **密碼到期 (天數)**  
- **記住密碼歷程記錄**  
- **重複登入失敗多少次之後抹除該裝置**  
- **在非使用狀態幾分鐘後需要輸入密碼**  
- **需要的密碼類型 – 最小字元集數**  
- **允許相機**
- **行動裝置需要加密**  
- **允許卸除式存放裝置**  
- **允許網頁瀏覽器**  
- **允許應用程式市集**  
- **允許螢幕擷取**  
- **允許使用地理位置**  
- **允許 Microsoft 帳戶**  
- **允許複製並貼上**  
- **允許 Wi-Fi 網際網路共用功能**  
- **允許自動連線到免費的 Wi-Fi 熱點**  
- **允許 Wi-Fi 熱點回報**  
- **允許原廠重設**
- **允許藍芽**  
- **允許 NFC**
- **允許 Wi-Fi**

### <a name="start-a-selective-wipe"></a>開始選擇性抹除

1. 在 Configuration Manager 主控台中，移至 [**資產與相容性**] 工作區，然後選擇 [**裝置**] 節點。 您也可以選擇 [**裝置集合**]，然後選取裝置所屬的集合。

1. 選取您要抹除的裝置。

1. 在功能區的 [裝置] 群組中，選取 [**遠端裝置動作**]，然後選擇 [**淘汰/** 抹除]。

1. 在 [**從 Configuration Manager 淘汰**] 視窗中，選取下列選項： [抹除**公司內容] 和 [從 Configuration Manager 淘汰行動裝置**]。

### <a name="recommendations-for-selective-wipe"></a>選擇性抹除的建議

- 若要成功抹除電子郵件，請將電子郵件設定檔設定為 Windows Phone 8.1 裝置。

- 若要成功抹除應用程式，請確定該應用程式為透過行動裝置應用程式管理發佈。

## <a name="passcode-reset"></a>密碼重設

如果使用者忘記其密碼，請使用此動作，在裝置上強制執行新的暫時密碼。 您也可以完全移除密碼。 下表列出密碼重設在不同行動平台上的運作方式。

| OS 版本 | 密碼重設 |
|------------|----------------|
| Windows 10 | 不支援 |
| Windows 10 Mobile | 支援，不包括已加入 Azure Active Directory 的裝置 |
| Windows Phone 8 和 Windows Phone 8.1 | 支援 |
| Windows RT 8.1 | 不支援 |
| Windows 8.1 | 不支援 |

> [!Note]
> 從頂層網站啟動 [密碼重設] 動作。 例如，如果您使用管理中心網站，您只能在該網站上執行動作。 如果您使用的是獨立的主要網站，您只能從該網站進行動作。

### <a name="remotely-reset-the-passcode-on-a-mobile-device"></a>從遠端重設行動裝置上的密碼

1. 在 Configuration Manager 主控台中，移至 [**資產與相容性**] 工作區，然後選擇 [**裝置**] 節點。 您也可以選擇 [**裝置集合**]，然後選取裝置所屬的集合。

1. 選取要重設密碼的一或多部裝置。

1. 在功能區的 [裝置] 群組中，選取 [**遠端裝置動作**]，然後選擇 [**密碼重設**]。  

### <a name="show-the-state-of-the-passcode-reset"></a>顯示密碼重設的狀態  

1. 在 Configuration Manager 主控台中，移至 [**資產與相容性**] 工作區，然後選擇 [**裝置**] 節點。 您也可以選擇 [**裝置集合**]，然後選取裝置所屬的集合。

1. 選取要顯示密碼重設狀態的一或多部裝置。

1. 在功能區的 [裝置] 群組中，選取 [**遠端裝置動作**]，然後選擇 [**顯示密碼狀態**]。  

## <a name="remote-lock"></a>遠端鎖定

如果使用者遺失裝置，您可以從遠端鎖定裝置。 下表列出遠端鎖定在不同行動平台上的運作方式。  

|OS 版本|遠端鎖定|
|----------|-----------|
|Windows 10|不支援|
|Windows Phone 8 和 Windows Phone 8.1|支援|
|Windows RT 8.1|支援，如果裝置的目前使用者是註冊裝置的相同使用者。|
|Windows 8.1|支援，如果裝置的目前使用者是註冊裝置的相同使用者。|

> [!Note]
> 從頂層網站啟動遠端鎖定動作。 例如，如果您使用管理中心網站，您只能在該網站上執行動作。 如果您使用的是獨立的主要網站，請從該網站進行動作。

### <a name="remotely-lock-a-mobile-device"></a>遠端鎖定行動裝置

1. 在 Configuration Manager 主控台中，移至 [**資產與相容性**] 工作區，然後選擇 [**裝置**] 節點。 您也可以選擇 [**裝置集合**]，然後選取裝置所屬的集合。

1. 選取要鎖定的一或多部裝置。

1. 在功能區的 [裝置] 群組中，選取 [**遠端裝置動作**]，然後選擇 [**遠端鎖定**]。 確認動作。

### <a name="show-the-state-of-the-remote-lock"></a>顯示遠端鎖定的狀態

1. 在 Configuration Manager 主控台中，移至 [**資產與相容性**] 工作區，然後選擇 [**裝置**] 節點。 您也可以選擇 [**裝置集合**]，然後選取裝置所屬的集合。

1. 選取要顯示遠端鎖定狀態的裝置。

1. 在功能區的 [裝置] 群組中，選取 [**遠端裝置動作**]，然後選擇 [**顯示遠端鎖定狀態**]。
