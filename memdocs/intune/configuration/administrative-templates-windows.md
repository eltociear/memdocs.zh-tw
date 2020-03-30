---
title: 在 Microsoft Intune 中使用 Windows 10 裝置的範本 - Azure | Microsoft Docs
description: 在 Microsoft Intune 和端點管理員中使用系統管理範本，為 Windows 10 裝置建立設定群組。 使用裝置組態設定檔中的這些設定來控制 Office 程式和 Microsoft Edge、保護 Internet Explorer 中的功能、控制對 OneDrive 的存取、使用遠端桌面功能、啟用 [自動播放]、設定電源管理設定、使用 HTTP 列印、使用不同的使用者登入選項，以及控制事件記錄檔大小。
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 03/23/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: high
ms.technology: ''
ms.reviewer: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 75ef2a03c9f42f0bda78af009f0fb563fbcedb75
ms.sourcegitcommit: 795e8a6aca41e1a0690b3d0d55ba3862f8a683e7
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/24/2020
ms.locfileid: "80220000"
---
# <a name="use-windows-10-templates-to-configure-group-policy-settings-in-microsoft-intune"></a>在 Microsoft Intune 中使用 Windows 10 範本設定群組原則設定

當您管理組織中的裝置時，您想要建立一組設定來套用至不同的裝置群組。 例如，您有數個裝置群組。 針對群組 A，您想要指派一組特定設定。 針對群組 B，您想要指派另一組設定。 您也需要可進行之設定的簡單檢視。

您可以在 Microsoft Intune 中使用 [系統管理範本]  來完成這項工作。 系統管理範本包含數百個設定，可控制 Microsoft Edge 77 版和更新版本、Internet Explorer、Microsoft Office 程式、遠端桌面、OneDrive、密碼和 PIN 中的功能。 這些設定可讓群組管理員使用雲端來管理群組原則。

本功能適用於：

- Windows 10 和更新版本

Windows 設定類似於 Active Directory (AD) 中的群組原則 (GPO) 設定。 這些設定內建於 Windows 中，且是使用 XML 的 [ADMX 支援設定](https://docs.microsoft.com/windows/client-management/mdm/understanding-admx-backed-policies)。 Office 與 Microsoft Edge 設定為 ADMX 內嵌，且使用 [Office 系統管理範本檔案](https://www.microsoft.com/download/details.aspx?id=49030) 和 [Microsoft Edge 系統管理範本檔案](https://www.microsoftedgeinsider.com/enterprise)中的 ADMX 設定。 此外，Intune 範本是 100% 雲端式的。 它們提供一個簡單且直接的方法來進行設定，以及尋找您想要的設定。

**系統管理範本**內建於 Intune 中，並不需要任何自訂項目，包括使用 OMA-URI。 作為行動裝置管理 (MDM) 解決方案的一部分，請使用這些範本設定作為您一次管理 Windows 10 裝置的位置。

此文章列出建立 Windows 10 裝置範本的步驟，並示範如何篩選 Intune 中的所有可用設定。 當您建立範本時，它會建立裝置組態設定檔。 您可以接著將此設定檔指派或部署到您組織中的 Windows 10 裝置。

## <a name="before-you-begin"></a>開始之前

- 從 Windows 10 1703 版 (RS2/組建 15063) 開始，可以使用其中一些設定。 有些設定不會包含在所有的 Windows 版本中。 為了獲得最佳體驗，建議使用 Windows 10 企業版 1903 (19H1/組建 18362) 和更新版本。

- Windows 設定會使用 [Windows 原則 CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-configuration-service-provider#policies-supported-by-group-policy-and-admx-backed-policies)。 CSP 適用於不同版本的 Windows，例如 Home、Professional、Enterprise 等。 若要查看 CSP 是否適用於特定版本，請前往 [Windows 原則 CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-configuration-service-provider#policies-supported-by-group-policy-and-admx-backed-policies)。

## <a name="create-the-template"></a>建立範本

1. 登入 [Microsoft Endpoint Manager 系統管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)。
2. 選取 [裝置]   > [組態設定檔]   > [建立設定檔]  。
3. 輸入下列內容：

    - **平台**：選取 [Windows 10 及更新版本]  。
    - **設定檔**：選取 [系統管理範本]  。

4. 選取 [建立]  。
5. 在 [基本資訊]  中，輸入下列內容：

    - **名稱**：為設定檔輸入描述性名稱。 命名您的設定檔，以方便之後能輕鬆識別。 例如，一個良好的設定檔名稱是**系統管理範本：可在 Microsoft Edge 中進行 xyz 設定的 Windows 10 系統管理範本**。
    - **描述**：輸入設定檔的描述。 這是選擇性設定，但建議執行。

6. 選取 [下一步]  。

7. 在 [組態設定]  中，設定套用到裝置的設定 (**電腦設定**)，以及套用到使用者的設定 (**使用者設定**)：

    > [!div class="mx-imgBorder"]
    > ![將 ADMX 範本設定套用到 Microsoft Intune 端點管理員中的使用者和裝置](./media/administrative-templates-windows/administrative-templates-choose-computer-user-configuration.png)

8. 當您選取 [電腦設定]  時，就會顯示設定類別。 您可以選取任意類別來查看可用設定。

    例如，選取 [電腦設定]   > [Windows 元件]   > [Internet Explorer]  ，以查看套用到 Internet Explorer 的所有裝置設定：

    > [!div class="mx-imgBorder"]
    > ![在 Microsoft Intune 端點管理員中查看套用到 Internet Explorer 的所有裝置設定](./media/administrative-templates-windows/administrative-templates-all-internet-explorer-settings-device.png)

9. 您也可以選取 [所有設定]  ，以查看每個裝置設定。 向下捲動，以使用向前和向後箭號來查看更多設定：

    > [!div class="mx-imgBorder"]
    > ![查看設定清單範例並使用上一個和下一個按鈕](./media/administrative-templates-windows/administrative-templates-sample-settings-list.png)

10. 選取任何設定。 例如，篩選 **Office**，然後選取 [啟用限制瀏覽]  。 設定的詳細描述會隨即顯示。 選擇 [已啟用]  、[已停用]  ，或將設定保留為 [尚未設定]  \(預設\)。 此詳細描述也會說明當您選擇 [已啟用]  、[已停用]  或 [尚未設定]  時所發生的情況。

    > [!TIP]
    > Intune 中的 Windows 設定會與您在本機群組原則編輯器 (`gpedit`) 中看到的內部部署群組原則路徑相互關聯

11. 按一下 [確定]  以儲存您的變更。

    繼續檢閱設定清單，並設定您環境中所需的設定。 以下是一些範例：

    - 使用 [VBA 巨集通知設定]  設定來處理不同 Microsoft Office 程式 (包括 Word 和 Excel) 中的 VBA 巨集。
    - 使用 [允許檔案下載]  設定來允許或防止從 Internet Explorer 下載。
    - 使用 [喚醒電腦時必須使用密碼 (一般電源)]  ，以提示使用者從睡眠模式喚醒裝置時輸入密碼。
    - 使用 [下載未簽署的 ActiveX 控制項]  設定來防止使用者從 Internet Explorer 下載未簽署的 ActiveX 控制項。
    - 使用 [關閉系統還原]  設定來允許或防止使用在裝置上執行系統還原。
    - 使用 [Allow importing of favorites] \(允許匯入我的最愛\)  設定，允許或封鎖使用者將其他瀏覽器的最愛項目匯入 Microsoft Edge。
    - 還有更多項目...

12. 選取 [下一步]  。
13. 在 [範圍標籤]  (選擇性) 中，指派標籤來針對特定 IT 群組篩選設定檔，例如 `US-NC IT Team` 或 `JohnGlenn_ITDepartment`。 如需範圍標籤的詳細資訊，請參閱[針對分散式 IT 使用 RBAC 和範圍標籤](..//fundamentals/scope-tags.md)。

    選取 [下一步]  。

14. 在 [指派]  中，選取將接收您設定檔的使用者或群組。 如需指派設定檔的詳細資訊，請參閱[指派使用者和裝置設定檔](device-profile-assign.md)。

    選取 [下一步]  。

15. 在 [檢閱 + 建立]  中，檢閱您的設定。 當您選取 [建立]  時，系統會儲存您的變更，然後指派設定檔。 原則也會顯示在設定檔清單中。

當裝置下一次檢查設定更新時，會套用您所設定的設定。

## <a name="find-some-settings"></a>尋找一些設定

這些範本提供數百項設定。 若要更輕鬆地尋找特定設定，請使用內建功能：

- 在您的範本中，選取 [設定]  、[狀態]  、[設定類型]  或 [路徑]  欄來排序清單。 例如，選取 [路徑]  資料行，並使用 [下一步] 箭號來查看 `Microsoft Excel` 路徑中的設定：

- 在您的範本中，使用 [搜尋]  方塊來尋找特定設定。 您可以依設定 (或路徑) 搜尋。 例如，搜尋 `copy`。 這會顯示包含 `copy` 的所有設定：

  > [!div class="mx-imgBorder"]
  > ![搜尋複本，以顯示 Intune 中系統管理範本內的所有裝置設定](./media/administrative-templates-windows/search-copy-settings.png) 

  在另一個範例中，搜尋 `microsoft word`。 您會看到可為 Microsoft Word 程式設定的設定。 搜尋 `explorer`，以查看您可以新增至範本的 Internet Explorer 設定。

## <a name="next-steps"></a>後續步驟

範本已建立，但可能還不會執行任何動作。 接下來，[指派範本 (也稱為設定檔)](device-profile-assign.md) 並[監視其狀態](device-profile-monitor.md)。

[使用系統管理範本更新 Office 365](administrative-templates-update-office.md)。

[教學課程：使用雲端在具有 ADMX 範本和 Microsoft Intune 的 Windows 10 裝置上設定群組原則](tutorial-walkthrough-administrative-templates.md)
