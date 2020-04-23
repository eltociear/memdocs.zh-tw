---
title: 針對 Intune Exchange Connector 的常見問題進行疑難排解
titleSuffix: Microsoft Intune
description: 針對內部部署 Microsoft Intune Exchange Connector 的常見問題進行疑難排解並加以解決。
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 11/26/2019
ms.topic: troubleshooting
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: medium
ms.technology: ''
ms.assetid: ''
ms.reviewer: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 55f51f94cf26aa2486ef390d5fbb668eaf013e10
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "79350625"
---
# <a name="resolve-common-problems-with-the-intune-exchange-connector"></a>解決 Intune Exchange Connector 的常見問題
 
本文可協助 Intune 系統管理員解決 Intune Exchange Connector 操作的常見問題。

開始進行疑難排解之前，請先檢閱 [針對 Intune On-Premises Exchange Connector 進行疑難排解](troubleshoot-exchange-connector.md)，以取得連接器的基本資訊。 另請檢閱連接器設定的常見問題。

## <a name="an-exchange-activesync-device-isnt-discovered-from-exchange"></a>無法從 Exchange 探索 Exchange ActiveSync 裝置

未從 Exchange 探索到 Exchange ActiveSync 裝置時，請[監視 Exchange Connector 活動](exchange-connector-install.md#on-premises-intune-exchange-connector-high-availability-support)，以查看 Exchange Connector 是否正在與 Exchange Server 同步。 如果自裝置加入後未進行任何同步，請收集同步記錄，並附加到支援要求。 如果自裝置加入後已成功完成完整同步或快速同步，請檢查是否有下列問題：

- 確定使用者具有 Intune 授權。 如果沒有，Exchange Connector 就無法探索其裝置。

- 如果使用者的主要 SMTP 位址和其在 Azure Active Directory (Azure AD) 中的使用者主體名稱 (UPN) 不同，Exchange Connector 將無法探索該使用者的任何裝置。 修正主要 SMTP 位址以解決問題。

- 如果您的環境中同時有 Exchange 2010 和 Exchange 2013 信箱伺服器，建議將 Exchange Connector 指向 Exchange 2013 CAS (Client Access Server)。 如果 Exchange Connector 設定為與 Exchange 2010 CAS 通訊，Exchange Connector 將不會探索任何 Exchange 2013 使用者裝置。

- 在 Exchange Online Dedicated 環境中，您必須在初始設定期間將 Exchange Connector 指向專用環境中的 Exchange 2013 CAS (而非 Exchange 2010 CAS)。 只有在執行 PowerShell Cmdlet 時，連接器才會與 Exchange 2013 CAS 通訊。

## <a name="problems-with-the-notification-email-message"></a>通知電子郵件訊息的問題

若要在未執行 Android Knox 的裝置上支援內部部署信箱的條件式存取，請確定 Intune 註冊是從 Intune Exchange Connector 所傳送的「立即開始使用」電子郵件訊息開始進行。 從訊息開始註冊可確保裝置會在所有平台 (Exchange、Azure AD、Intune) 間收到唯一的 ActiveSyncID。

使用者可能不會收到通知電子郵件訊息，因為：

- 通知帳戶設定錯誤。
- 通知帳戶的自動探索失敗。
- 用來傳送電子郵件訊息的 Exchange Web 服務 (EWS) 要求失敗。

請檢閱下列各節，以針對電子郵件通知問題進行疑難排解。

### <a name="check-the-notification-account-that-retrieves-autodiscover-settings"></a>檢查可擷取自動探索設定的通知帳戶

1. 請確定已在 Exchange 用戶端存取服務上設定自動探索服務和 EWS。 如需詳細資訊，請參閱[用戶端存取服務](https://docs.microsoft.com/Exchange/architecture/client-access/client-access) (機器翻譯) 和 [Exchange Server 中的自動探索服務](https://docs.microsoft.com/Exchange/architecture/client-access/autodiscover?view=exchserver-2019) (機器翻譯)。

2. 確認通知帳戶符合下列需求：

   - 此帳戶具有由 Exchange 內部部署伺服器裝載的使用中信箱。

   - 帳戶 UPN 符合 SMTP 位址。

3. 自動探索需要 DNS 伺服器，其中具有指向 Exchange Client Access Server 的 **Autodiscover.SMTPdomain.com** (例如 Autodiscover.contoso.com) DNS 記錄。 若要檢查是否有記錄，請指定 FQDN 來取代 *Autodiscover.SMTPdomain.com*，並遵循下列步驟執行：

   1. 在命令提示字元中輸入 *NSLOOKUP*。

   2. 輸入 *Autodiscover.SMTPdomain.com*。 輸出應如下圖所示：![Nslookup 結果 ](./media/troubleshoot-exchange-connector-common-problems/nslookup-results.png
      )

   您也可以在 https://testconnectivity.microsoft.com 上從網際網路測試自動探索服務。 或者，使用 Microsoft 連線分析程式工具，從本機網域進行測試。 如需詳細資訊，請參閱 [Microsoft 連線分析程式工具](https://docs.microsoft.com/previous-versions/office/exchange-remote-connectivity/jj851141(v=exchg.80))。


### <a name="check-autodiscovery"></a>檢查自動探索

如果自動探索失敗，請嘗試下列步驟：

1. [設定有效的自動探索 DNS 記錄](https://docs.microsoft.com/previous-versions/exchange-server/exchange-150/mt473798(v=exchg.150))。

2. 在 Intune Exchange Connector 設定檔中將，以硬式編碼的方式寫入 EWS URL：

   1. 判斷 EWS URL。 Exchange 的預設 EWS URL 是 `https://<mailServerFQDN>/ews/exchange.asmx`，但 URL 可能不同。 請連絡 Exchange 系統管理員，為環境驗證正確的 URL。

   2. 編輯 *OnPremisesExchangeConnectorServiceConfiguration.xml* 檔案。 根據預設，此檔案位於 Exchange Connector 執行所在電腦上的 *%ProgramData%\Microsoft\Windows Intune Exchange Connector* 中。 請在文字編輯器中開啟檔案，然後變更下列這一行，以反映環境的 EWS URL：`<ExchangeWebServiceURL>https://<YourExchangeHOST>/EWS/Exchange.asmx</ExchangeWebServiceURL>`

3. 儲存檔案，然後重新啟動電腦或 Microsoft Intune Exchange Connector 服務。

>[!NOTE]
> 在此設定中，Intune Exchange Connector 會停止使用自動探索，而改為直接連線到 EWS URL。

## <a name="next-steps"></a>後續步驟

如需特定錯誤的說明，請嘗試[解決 Intune Exchange Connector 的常見錯誤](troubleshoot-exchange-connector-common-errors.md)。

若要取得支援，或從 Intune 社群取得協助，請：

- 參閱[取得支援](../fundamentals/get-support.md)以使用 Intune 主控台針對問題進行疑難排解，或向 Microsoft 開啟支援案例。
- 在 [Microsoft Intune 論壇](https://social.technet.microsoft.com/Forums/home?forum=microsoftintuneprod)中張貼問題。