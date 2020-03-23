---
title: Exchange Connector 疑難排解
titleSuffix: Microsoft Intune
description: 針對與 Intune On-Premises Exchange Connector 相關的問題進行疑難排解。
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 10/02/2019
ms.topic: troubleshooting
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: medium
ms.technology: ''
ms.assetid: a7e3c742-295b-40bb-9afa-17f243062500
ms.reviewer: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: af44b09f5e539306a24ae0e0294b3ad674f7cb74
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/13/2020
ms.locfileid: "79338548"
---
# <a name="troubleshoot-the-intune-exchange-connector"></a>為 Intune Exchange Connector 進行疑難排解

本文描述如何針對與 Intune Exchange Connector 相關的問題進行疑難排解。

## <a name="before-you-start"></a>在您開始使用 Intune 之前

在您開始針對 Intune 中的 Exchange Connector 問題進行疑難排解之前，請先收集一些基本資訊，以便在穩固的基礎上運作。 此方法可協助您進一步了解問題的本質，並更快速地解決問題。

- 確認程序符合安裝需求。 請參閱[安裝內部部署 Intune Exchange 連接器](exchange-connector-install.md)。
- 確認帳戶具有 Exchange 和 Intune 系統管理員權限。
- 記下完整且確實的錯誤訊息文字、詳細資料，以及訊息的顯示位置。
- 判斷問題何時開始： 
  - 第一次設定連接器嗎？ 
  - 連接器是否原本運作正常，後來才失敗？
  - 如果原本運作正常，那麼 Intune 環境、Exchange 環境或執行連接器軟體的電腦上發生了哪些變更？
- 什麼是 MDM 授權單位？
- 使用哪一版的 Exchange？

### <a name="use-powershell-to-get-more-data-on-exchange-connector-issues"></a>使用 PowerShell 取得 Exchange Connector 問題的更多資料

- 若要取得信箱的所有行動裝置清單，請使用 `Get-ActiveSyncDeviceStatistics -mailbox mbx`
- 若要取得信箱的 SMTP 位址清單，請使用 `Get-Mailbox -Identity user | select emailaddresses | fl`
- 若要取得有關裝置存取狀態的詳細資訊，請使用 `Get-CASMailbox <upn> | fl`

## <a name="review-the-connector-configuration"></a>檢閱連接器設定

檢閱[內部部署 Exchange Connector 需求](exchange-connector-install.md#intune-exchange-connector-requirements)，確定已正確設定環境和連接器。 

### <a name="general-considerations-for-the-connector"></a>連接器的一般考量

- 確定防火牆和 Proxy 伺服器允許在裝載 Intune Exchange Connector 和 Intune 服務的伺服器之間進行通訊。

- 裝載 Intune Exchange Connector 和 Exchange Client Access Server (CAS) 的電腦應該已加入網域且位於相同 LAN 上。 確定已針對 Intune Exchange Connector 所使用的帳戶新增必要權限。

- 使用通知帳戶來擷取 [自動探索]  設定。 如需 Exchange 中自動探索的詳細資訊，請參閱 [Exchange Server 中的自動探索服務](https://docs.microsoft.com/exchange/architecture/client-access/autodiscover?view=exchserver-2016) (機器翻譯)。

- Intune Exchange Connector 藉由使用通知帳戶認證來傳送內含 [開始使用]  連結 (以在 Intune 中註冊) 的通知電子郵件訊息，以將要求傳送到 EWS URL。 Android 的非 Knox 裝置要求必須使用 [開始使用]  連結來進行註冊。 否則，條件式存取將會封鎖這些裝置。

### <a name="common-issues-for-connector-configurations"></a>連接器設定的常見問題

- **帳戶權限**：在 [Microsoft Intune Exchange Connector] 對話方塊中，確定已指定具有適當權限的使用者帳戶執行[必要的 Windows PowerShell Exchange Cmdlet](exchange-connector-install.md#exchange-cmdlet-requirements)。
- **通知電子郵件訊息**：啟用通知並指定通知帳戶。
- **Client Access Server 同步處理**：設定 Exchange Connector 時，指定 CAS 與裝載 Exchange Connector 的伺服器之間要盡可能有最低網路延遲。 CAS 與 Exchange Connector 之間的通訊延遲，可能會延遲裝置探索，尤其是在使用 Exchange Online Dedicated 時。
- **同步處理排程**：新註冊裝置的使用者在取得存取權時，可能會因 Exchange Connector 與 Exchange CAS 同步而延遲。 完整同步會一天執行一次，而差異 (快速) 同步則會一天執行多次。 您可以[手動強制執行快速同步或完整同步](exchange-connector-install.md#manually-force-a-quick-sync-or-full-sync)將延遲降到最低。

## <a name="next-steps"></a>後續步驟
下列文章可協助解決常見問題和特定錯誤：

- [解決 Intune Exchange Connector 的常見問題](troubleshoot-exchange-connector-common-problems.md)。
- [解決 Intune Exchange Connector 的常見錯誤](troubleshoot-exchange-connector-common-errors.md)。

向支援人員或 Intune 社群尋求協助：

- 請參閱[取得支援](../fundamentals/get-support.md)以使用 Intune 主控台協助針對問題進行疑難排解，或向 Microsoft 開啟支援案例。 
- 在 [Microsoft Intune 論壇](https://social.technet.microsoft.com/Forums/en-US/home?forum=microsoftintuneprod)中張貼問題。  
