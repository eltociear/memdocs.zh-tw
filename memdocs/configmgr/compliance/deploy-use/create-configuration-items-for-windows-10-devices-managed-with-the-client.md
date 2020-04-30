---
title: 建立 Windows 10 的設定項目
titleSuffix: Configuration Manager
description: 使用 Windows 10 設定項目來管理由 Configuration Manager 用戶端管理的 Windows 10 電腦設定。
ms.date: 01/06/2020
ms.prod: configuration-manager
ms.technology: configmgr-compliance
ms.topic: conceptual
ms.assetid: 14226fbe-dd07-4432-910b-130790624a4e
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: 9a1bda440ab3ccd02432f0b023a134b9f54cdafb
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81692536"
---
# <a name="create-configuration-items-for-windows-10-devices"></a>建立 Windows 10 的設定項目

使用 Configuration Manager **Windows 10** 設定項目來管理由 Configuration Manager 用戶端管理的 Windows 10 電腦設定。  
  
> [!IMPORTANT]  
>  在此版本中，如果您建立 [密碼]  設定作為 **Windows 10** 類型設定項目的一部分 (針對 Configuration Manager 用戶端管理的裝置)，請留意下列問題。 如果該設定尚不存在，或尚未在 Windows 10 裝置上設定，則會錯誤地評估為相容。  
>   
>  因應措施是當您建立這些裝置的設定時，請務必在 [建立設定項目精靈] 的 [設定] 頁面上，選取 [補救不相容的設定]  。 此外，若您部署的設定基準包括含密碼設定的 Windows 10 設定項目，請選取 [支援時補救不符合規範的規則]  。 您可以在 [部署設定基準] 對話方塊中進行此選取。 使用這個因應措施時，如果找到不符合規範的設定，就會加以監視並進行補救。 補救之後，即會將該設定正確回報為 [符合規範]  ，但若發生問題，則會回報 [錯誤]  。  
  
### <a name="to-create-a-windows-10-configuration-item"></a>建立 Windows 10 組態項目  
  
1. 在 Configuration Manager 主控台中，選擇 [資產與合規性]  。  
  
2. 在 [資產與合規性]  工作區中，展開 [合規性設定]  ，然後選取 [設定項目]  。  
  
3. 在 [首頁]  索引標籤的 [建立]  群組中，選取 [建立設定項目]  。  
  
4. 在 [建立設定項目精靈]  的 [一般]  頁面上，指定設定項目的名稱與選擇性描述。  
  
5. 在 [指定您要建立的組態項目類型]  下，選取 [Windows 10]  。  
  
6. 若您建立並指派類別以協助您在 Configuration Manager 主控台中搜尋及篩選設定項目，請選取 [類別]  。  
  
7. 在精靈的 [支援的平台]  頁面上，選取將評估組態項目的特定 Windows 10 平台。  
  
8. 在精靈的 [裝置設定]  頁面上，選取您想要設定的設定群組。 (如需詳細資訊，請參閱本文的 [Windows 10 設定項目的設定參考](#BKMK_Ref)。)然後選取 [下一步]  。  
  
   > [!TIP]  
   >  如果未列出您想要的設定，請選取 [設定不在預設設定群組中的其他設定]  核取方塊。  
  
9. 在每一個設定頁面上，進行您需要的設定，並指定這些設定與裝置不相容時是否要進行補救 (如果支援的話)。  
  
10. 針對每個設定群組，您也可以設定當發現設定項目不符合規範時要回報的嚴重性：  
  
    -   **無**：不符合此合規性規則的裝置不會針對 Configuration Manager 報告回報失敗嚴重性。  
  
    -   **資訊**：不符合這項相容性規則的裝置會回報 Configuration Manager 報告的 [資訊]  失敗嚴重性。  
  
    -   **警告**：不符合這項相容性規則的裝置會回報 Configuration Manager 報告的 [警告]  失敗嚴重性。  
  
    -   **重大**：不符合這項相容性規則的裝置會回報 Configuration Manager 報告的 [重大]  失敗嚴重性。  
  
    -   **重大事件**：不符合這項相容性規則的裝置會回報 Configuration Manager 報告的 [重大]  失敗嚴重性。 此嚴重性層級也會在應用程式事件記錄檔中記錄為 Windows 事件。  
  
11. 在精靈的 [平台適用性]  頁面上，檢閱是否有與您先前選取的支援平台不相容的任何設定。 您可以返回並移除這些設定，也可以繼續。  
  
    > [!TIP]  
    >  系統不會針對不支援的設定進行相容性評估。  
  
12. 完成精靈。  
  
    您可以在 [資產與合規性]  工作區的 [設定項目]  節點中檢視新的設定項目。  
  
## <a name="windows-10-configuration-item-settings-reference"></a><a name="BKMK_Ref"></a> Windows 10 configuration item settings reference  
  
### <a name="password"></a>密碼  
  
|設定|詳細資料|  
|-------------|-------------|  
|**需要裝置上的密碼設定**|需要支援裝置上的密碼。|  
|**最小密碼長度 (字元數)**|密碼字元長度下限。|  
|**密碼到期天數**|密碼必須變更之前的天數。|  
|**記住的密碼數目**|防止重複使用先前的密碼。|  
|**抹除裝置前允許的失敗登入次數**|如果登入失敗達到這個次數即會抹除裝置。|  
|**鎖定裝置前的閒置時間**|指定裝置閒置幾分鐘之後就會自動鎖定。|  
|**密碼複雜性**|選擇是否可以指定 PIN (如 '1234')，或是否必須提供強式密碼。|
|**密碼所需複雜字元集數**|如果您選取**強式**密碼，請使用此設定來設定複雜字元集所需的數目。 針對強式密碼，此設定至少應該設定為 **3**，表示需要字母與數字。 如果想要強制要求另需特殊字元 (例如 **%$** ) 的密碼，請選取 [4]  。<br>(僅限 Windows 10)  |
  
###  <a name="device"></a>裝置  
  
|設定名稱|詳細資料|  
|------------------|-------------|  
|**Bluetooth**|裝置上允許使用 Bluetooth 功能。|  
  
### <a name="cloud"></a>雲端  
  
|設定名稱|詳細資料|  
|------------------|-------------|  
|**設定同步處理**|允許裝置之間的設定同步處理。|  
|**認證同步處理**|允許裝置之間的認證同步處理。|  
|**透過計量付費連線的設定同步處理**|當使用計量付費網際網路連線時，允許同步處理設定。|  
  
### <a name="roaming"></a>漫遊  
  
|設定名稱|詳細資料|  
|------------------|-------------|  
|**數據漫遊**|存取資料時允許在網路之間漫遊。|  
  
### <a name="encryption"></a>加密  
  
|設定名稱|詳細資料|  
|------------------|-------------|  
|**裝置上的檔案加密**|裝置上的檔案需要加密。|  
  
### <a name="system-security"></a>系統安全性  
  
|設定名稱|詳細資料|  
|------------------|-------------|  
|**使用者帳戶控制**|設定裝置上 Windows 使用者帳戶控制的運作方式。<br />例如，您可以停用它或設定通知等級。|  
|**網路防火牆**|啟用或停用 Windows 防火牆。|  
|**SmartScreen**|啟用或停用 Windows SmartScreen。|  
|**防毒保護**|必須安裝和設定防毒軟體。|  
|**防毒特徵已是最新版本**|裝置上防毒軟體的簽章檔案必須是最新狀態。|  
  
### <a name="windows-information-protection"></a>Windows 資訊保護

企業中員工擁有的裝置日漸增加，資料不慎從應用程式與服務 (如電子郵件、社交媒體和公用雲端) 外洩的風險也更高。 這並不在組織的控制範圍內。 相關範例包括員工進行下列作業時：

- 從個人電子郵件帳戶傳送最新的工程圖片。
- 將產品資訊複製並貼到推文中。
- 將進行中的銷售報告儲存至其公用雲端儲存體。

Windows 資訊保護 (WIP，先前稱為企業資料保護) 有助於防止此類資料外洩的可能，同時不干擾員工的體驗。 WIP 也能協助保護企業應用程式與資料，防止企業擁有的裝置和員工自備工作用的個人裝置意外外洩資料。 WIP 不需要變更您的環境或其他應用程式。

Configuration Manager Windows 資訊保護設定項目可管理下列各項：

- 由 WIP 保護的應用程式清單
- 企業網路位置
- 保護等級
- 加密設定
  
如需如何使用 Configuration Manager 設定 WIP 的相關資訊，請參閱：

- [使用 Windows 資訊保護 (WIP) 保護您的企業資料](https://docs.microsoft.com/windows/security/information-protection/windows-information-protection/protect-enterprise-data-using-wip)
- [使用 Configuration Manager 建立和部署 Windows 資訊保護 (WIP) 原則](https://docs.microsoft.com/windows/security/information-protection/windows-information-protection/create-wip-policy-using-configmgr)
- [使用 Windows 資訊保護 (WIP) 時的限制](https://docs.microsoft.com/windows/security/information-protection/windows-information-protection/limitations-with-wip)

## <a name="see-also"></a>請參閱  
[由 Configuration Manager 用戶端管理之裝置的設定項目](../../compliance/deploy-use/create-configuration-items.md)
