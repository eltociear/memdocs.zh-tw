---
title: 電腦分析的新功能
titleSuffix: Configuration Manager
description: 電腦分析雲端服務最新每月版本中的新功能摘要。
ms.date: 03/12/2020
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: conceptual
ms.assetid: fa300181-86cb-4afe-8fbf-895a7572378d
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: ce882f6bfc7a0d724688d5df59051dae17d54498
ms.sourcegitcommit: a4ec80c5dd51e40f3b468e96a71bbe29222ebafd
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/01/2020
ms.locfileid: "82693148"
---
# <a name="whats-new-in-desktop-analytics"></a>電腦分析的新功能

了解電腦分析中每個月的新功能。

> [!TIP]
> 每一次的每月更新都可能需要最多三天才會推出。 某些功能可能會在數週內推出，且不會在第一週就提供給所有客戶。

若要在此頁面更新時收到通知，請複製下列 URL 並貼到您的 RSS 摘要讀取程式：`https://docs.microsoft.com/api/search/rss?search=%22what%27s+new+in+desktop+analytics+-+Configuration+Manager%22&locale=en-us`
<!-- a locale is required for the RSS search string -->

## <a name="march-2020"></a>2020 年 3 月

### <a name="support-for-multiple-hierarchies"></a>支援多個階層

<!-- 4814075, 6079184 -->

您現在可以將多個 Configuration Manager 階層連線至具有電腦分析之單一商業識別碼的單一 Azure Active Directory 租用戶。 入口網站會將來自不同階層的裝置分類，並改善通用試驗與部署計劃的體驗。

- 當您設定通用試驗時，如果您所包含的集合中包含超過已註冊裝置總數的 20%，入口網站會顯示警告。
- 當您建立部署計劃時，如果您選取來自多個階層的集合，入口網站會顯示警告。

> [!NOTE]
> 對多個階層的支援需要 Configuration Manager 1910 版或更新版本。

如需詳細資訊，請參閱下列文章：

- [通用試驗](deploy-pilot.md#bkmk_GlobalPilot)
- [如何建立部署計劃](create-deployment-plans.md)

### <a name="identify-compatibility-safeguards"></a>識別相容性保護

<!-- 5746559 -->

Windows 相容性資料會使用「保護」  來分類某些應用程式與驅動程式，這可能會導致更新至 Windows 10 失敗或復原。 電腦分析現在可以協助您事先識別這些保護，讓您可以在部署更新之前先對資產進行補救。 如需詳細資訊，請參閱[相容性評定 - 保護](compat-assessment.md#safeguards)。

## <a name="january-2020"></a>2020 年 1 月

### <a name="additional-app-usage-detail"></a>其他應用程式使用方式詳細資料

<!-- 5533890 -->

當您選取某項應用程式來查看詳細資訊時，[詳細資料] 窗格現已包含其他使用方式資訊。 您可以使用這項資料以協助了解應用程式的安裝範圍，以及使用者經常使用此應用程式的裝置。 如需詳細資訊，請參閱[關於資產 - 應用程式使用方式](about-assets.md#usage)。

### <a name="provide-feedback-on-desktop-analytics"></a>提供有關電腦分析的意見反應

<!-- 5451636 -->

若要分享您對電腦分析的意見反應，請選取右側入口網站上方的**傳送笑臉**圖示。 如需詳細資訊，請參閱[分享產品意見反應](get-support.md#bkmk_feedback)。

## <a name="october-2019"></a>2019 年 10 月

### <a name="improvements-to-compatibility-recommendations"></a>相容性建議的改善

<!-- 3594545 -->

電腦分析現在會在偵測到 Windows 升級將會完全或部分移除應用程式或驅動程式時，提供額外的詳細資料。 如需詳細資訊，請參閱[相容性評定](compat-assessment.md#asset-is-removed-during-upgrade)。

### <a name="migrate-from-windows-analytics-to-existing-tenant"></a>從 Windows Analytics 遷移至現有租用戶

<!-- 5202803 -->

您現在可以在上線後，將輸入從現有的 Windows Analytics 工作區遷移至電腦分析。

## <a name="september-2019"></a>2019 年 9 月

### <a name="migrate-inputs-from-windows-analytics"></a>從 Windows Analytics 遷移輸入

<!-- 4252663 -->

在上線期間，您現在可以從現有的 Windows Analytics 工作區遷移輸入。

### <a name="offboard-from-desktop-analytics"></a>從電腦分析離線

<!-- 4972396 -->

若您在您的環境中設定電腦分析，但想要停止使用服務，您現在可以關閉您的帳戶。 若您在 90 天內改變心意，您可以重新啟用帳戶。 如需詳細資訊，請參閱[如何關閉您的帳戶](account-close.md)。

## <a name="august-2019"></a>2019 年 8 月

### <a name="reset-your-account"></a>重設您的帳戶

<!-- 3733897 -->

如果您在環境中設定電腦分析，但想要從頭開始上線和註冊，您現在可以進行重設。 如需流程的詳細資訊，請參閱[重設您的帳戶](account-reset.md)。

### <a name="automatic-upgrade-decision-of-system-and-store-apps"></a>系統和 Microsoft Store 應用程式的自動升級決策

<!-- 3587232 -->

為了減少您在標註值得注意應用程式時所耗費的精力，某些類型的應用程式會自動標記為 [不重要]  。 這些應用程式的部署計劃升級決策也會標記為 [就緒]  。 下列應用程式皆相容，而且在您升級 Windows 之後應可繼續運作：

- Microsoft 發佈的系統應用程式和元件

- 在 Microsoft Store 中管理和更新的應用程式

如需詳細資訊，請參閱[系統及 Microsoft Store 應用程式的自動升級決策](about-assets.md#bkmk_plan-autoapp)。

## <a name="whats-new-in-configuration-manager"></a>Configuration Manager 的新功能

電腦分析文件一律會參考 Configuration Manager 目前分支最新版本中的功能。 如需 Configuration Manager 中最新變更的詳細資訊，請參閱下列文章：

<!-- - [What's new in version 1910](../core/plan-design/changes/whats-new-in-version-1910.md#bkmk_da) -->

- [1906 版的新功能](../core/plan-design/changes/whats-new-in-version-1906.md#bkmk_da)

## <a name="deprecated-features"></a>已淘汰的功能

當 Microsoft 計畫移除 [電腦分析] 服務的重大功能時，該變更將預先宣佈為 Configuration Manager 已被取代的功能。 如需詳細資訊，請參閱[已淘汰的功能](../core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures.md#deprecated-features)。
