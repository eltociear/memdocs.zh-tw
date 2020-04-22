---
title: 錯誤訊息
titleSuffix: Configuration Manager
description: 了解來自套件轉換管理員的錯誤訊息。
ms.date: 08/24/2018
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 0d3cf6e1-b295-4b05-821d-e9f57c74ca14
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 4d4a2fa66dc1c4a8af3b3f7f16c67d58edebb5fa
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81688966"
---
# <a name="technical-reference-for-package-conversion-manager-error-messages"></a>套件轉換管理員錯誤訊息的技術參考

適用於：  Configuration Manager (最新分支)

<!--1357861-->

本文說明套件轉換管理員所顯示的錯誤訊息。 它也會包含可能導致錯誤的原因及更正錯誤的方法。 套件轉換管理員會將錯誤訊息記錄於 **PCMTrace.log**。 如需詳細資訊 (包括如何控制詳細資訊層級)，請參閱[記錄檔](troubleshoot-pcm.md#log-files)。


#### <a name="application-creation-failed-with-the-following-exception"></a>應用程式建立失敗，發生下列例外狀況

指定的例外狀況會在將應用程式物件提交至 Configuration Manager 伺服器期間發生。

檢查您在 Configuration Manager 的權限、驗證您的連線能力，然後再試一次。 如果那些動作未能解決此問題，請檢查 **PCMtrace.log** 檔案 (詳細資訊層級 4) 和 **SMSProv.log**。


#### <a name="conversion-error--applies-to-a-package-transform-status"></a>轉換錯誤 – 適用於套件轉換狀態

套件轉換期間發生一般例外狀況。 請查看 **PCMtrace.log** 檔案 (詳細資訊層級 4)。

檢查網路共用 (套件資料來源) 的使用者權限、驗證您的連線能力，然後再試一次。 如果那些動作未能解決此問題，請檢查 **PCMtrace.log** 檔案 (詳細資訊層級 4)。


#### <a name="did-not-find-a-converted-package-and-its-resultant-application-in-the-workflow-outputs"></a>在工作流程輸出中找不到已轉換的套件及其產生的應用程式
已刪除應用程式 (轉換的套件/程式)。

請修改相依套件/程式，以確保相依套件/程式存在。


#### <a name="objects-were-not-created-successfully"></a>未成功建立物件
有數個可能的原因。

檢查您在 Configuration Manager 的權限、驗證您的連線能力，然後再試一次。 如果那些動作未能解決此問題，請檢查 **PCMtrace.log** 檔案 (詳細資訊層級 4) 和 **SMSProv.log** 檔案。


#### <a name="please-close-the-wizard-and-resolve-any-issues-with-the-selected-package-see-pcmtracelog-for-more-details"></a>請關閉此精靈，並解決任何所選取封裝的問題。 如需更多詳細資訊，請參閱 PCMTrace.Log
有數個可能的原因。

檢查您在 Configuration Manager 的權限、驗證您的連線能力，然後再試一次。 如果那些動作未能解決此問題，請檢查 **PCMtrace.log** 檔案 (詳細資訊層級 4) 和 **SMSProv.log** 檔案。


#### <a name="some-deployment-types-are-missing-detection-methods-all-deployment-types-must-have-detection-methods"></a>某些部署類型遺漏偵測方法。 所有部署類型都必須有偵測方法
從程式遺漏了偵測方法。

在**修正並轉換**程序中新增一或多個偵測方法。


#### <a name="there-was-an-error-preparing-the-package-for-conversion"></a>準備進行轉換的套件時發生錯誤
有數個可能的原因。

檢查您在 Configuration Manager 的權限、驗證您的連線能力，然後再試一次。 如果那些動作未能解決此問題，請檢查 **PCMtrace.log** 檔案 (詳細資訊層級 4) 和 **SMSProv.log** 檔案。


