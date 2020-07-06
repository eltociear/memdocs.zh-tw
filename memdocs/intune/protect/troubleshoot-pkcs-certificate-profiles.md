---
title: 針對使用 Microsoft Intune 以 PKCS 憑證設定檔佈建憑證進行疑難排解 | Microsoft Docs
description: 針對裝置用來要求憑證以搭配 Intune 使用的私密和公用金鑰組 (PKCS) 設定檔進行疑難排解。
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 05/29/2020
ms.topic: troubleshooting
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: high
ms.technology: ''
ms.reviewer: lacranda
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 7667cf1d62040c4435f41ffbe377452d3666a3ec
ms.sourcegitcommit: 411e9d93cbafc7585f5a0f9a05097fe589de804f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/24/2020
ms.locfileid: "85343070"
---
# <a name="troubleshoot-pkcs-certificate-deployment-in-microsoft-intune"></a>針對 Microsoft Intune 中的 PKCS 憑證部署進行疑難排解

此文章中的資訊可協助您解決在 Microsoft Intune 中部署私密和公開金鑰組 (PKCS) 憑證時的幾個常見問題。 進行疑難排解之前，請確定您已完成在[透過 Intune 設定並使用 PKCS 憑證](../protect/certficates-pfx-configure.md#export-the-root-certificate-from-the-enterprise-ca)中找到的下列工作：

- 請檢閱[使用 PKCS 憑證設定檔的需求](../protect/certficates-pfx-configure.md#requirements)
- 從企業憑證授權單位 (CA) 匯出根憑證
- 設定憑證授權單位上的憑證範本
- 安裝及設定 Intune 憑證連接器
- 建立並部署信任的憑證設定檔，以部署根憑證
- 建立並部署 PKCS 憑證設定檔

PKCS 憑證設定檔的最常見問題來源是使用 PKCS 憑證設定檔的設定。 檢閱設定檔設定，並尋找伺服器名稱或完整網域名稱 (FQDN) 中的拼字錯誤，並確認 [憑證授權單位] 與 [憑證授權單位名稱] 是正確的。

- **憑證授權單位**：憑證授權單位電腦的內部 FQDN。 例如，server1.domain.local。
- **憑證授權單位名稱**：[憑證授權單位] MMC 中所顯示的憑證授權單位名稱。 在 [憑證授權單位 (本機)] 下尋找

您可以在 CA 上使用 [certutil 命令列程式](https://docs.microsoft.com/windows-server/administration/windows-commands/certutil) \(部分機器翻譯\) 來確認 [憑證授權單位] 與 [憑證授權單位名稱] 的正確名稱。

## <a name="pkcs-communication-overview"></a>PKCS 通訊概觀

下圖提供 Intune 中 PKCS 憑證部署程序的基本概觀。

> [!div class="mx-imgBorder"]
> ![PKCS 憑證設定檔流程](./media/troubleshoot-pkcs-certificate-profiles/pkcs-overview-graphic.png)

1. 管理員在 Intune 中建立 PKCS 憑證設定檔。
2. Intune 服務要求內部部署 Intune 憑證連接器為使用者建立新的憑證。
3. Intune 憑證連接器將 PFX Blob 與要求傳送給您的 Microsoft 憑證授權單位。
4. 憑證授權單位發出 PFX 使用者憑證，並將其傳送回 Intune 憑證連接器。
5. Intune 憑證連接器將加密的 PFX 使用者憑證上傳至 Intune。
6. Intune 將 PFX 使用者憑證解密，並使用裝置管理憑證重新加密裝置。  Intune 接著將 PFX 使用者憑證傳送至裝置。
7. 裝置向 Intune 回報憑證狀態。

## <a name="data-and-log-files"></a>資料與記錄檔

若要識別通訊與憑證佈建工作流程的問題，請檢閱來自伺服器基礎結構與裝置的記錄檔。 針對 PKCS 憑證設定檔進行疑難排解的後續各節會提及此節所參考的記錄檔。

- [基礎結構與伺服器記錄檔](#logs-for-on-premises-infrastructure)

裝置記錄檔相依於裝置平台：

- [iOS 與 iPadOS](#logs-for-ios-and-ipados-devices)
- [Android](#logs-for-android-devices)
- [Windows](#logs-for-windows-devices)

### <a name="logs-for-on-premises-infrastructure"></a>內部部署基礎結構的記錄
  
支援使用 PKCS 憑證設定檔進行憑證部署的內部部署基礎結構包括 Microsoft Intune 憑證連接器、在 Windows Server 上執行的 NDES，以及憑證授權單位。

這些角色的記錄檔包括 Windows 事件檢視器、憑證主控台，以及各種特定於 Intune 憑證連接器、NDES 或其他角色與作業 (屬於內部部署基礎結構) 的各種記錄檔。

- **NDESConnector_date_time.svclog**：

  此記錄顯示從 Microsoft Intune 憑證連接器到 Intune 雲端服務的通訊。 您可以使用[服務追蹤檢視器工具](https://docs.microsoft.com/dotnet/framework/wcf/service-trace-viewer-tool-svctraceviewer-exe) \(部分機器翻譯\) 來檢視此記錄檔。

  相關的登錄機碼：*HKLM\SW\Microsoft\MicrosoftIntune\NDESConnector\ConnectionStatus*

  位置：在裝載 NDES 之伺服器的 *%program_files%\Microsoft intune\ndesconnectorsvc\logs\logs*

- **CertificateRegistrationPoint_date_time.svclog**：

  此記錄顯示接收及驗證憑證要求的 NDES 原則模組。 您可以使用[服務追蹤檢視器工具](https://docs.microsoft.com/dotnet/framework/wcf/service-trace-viewer-tool-svctraceviewer-exe) \(部分機器翻譯\) 來檢視此記錄檔。

  位置：在裝載 NDES 之伺服器的 *%program_files%\Microsoft intune\ndesconnectorsvc\logs\logs*

- **NDESPlugin.log**：

  此記錄檔顯示憑證要求傳遞至憑證登錄點，以及針對那些要求產生的驗證結果。

  位置：在裝載 NDES 之伺服器上的 *%program_files%\Microsoft Intune\NDESPolicyModule\logs*

- **Windows 應用程式記錄檔**：

  位置：在裝載 NDES 的伺服器上：執行 **eventvwr.msc** 以開啟 Windows 事件檢視器

### <a name="logs-for-android-devices"></a>Android 裝置的記錄

針對執行 Android 的裝置，請使用 **Android 公司入口網站**應用程式記錄檔 (**OMADM.log**)。 在您收集及檢閱記錄之前，請先確認[詳細資訊記錄](../user-help/use-verbose-logging-to-help-your-it-administrator-fix-device-issues-android.md)已啟用，然後重現問題。

若要從裝置收集 OMADM.logs，請參閱[使用 USB 纜線上傳記錄並以電子郵件傳送](../user-help/send-logs-to-your-it-admin-using-cable-android.md)。

您也可以[上傳記錄並以電子郵件傳送](../user-help/send-logs-to-your-it-admin-by-email-android.md#upload-and-email-logs-from-microsoft-intune-app)給技術支援。

### <a name="logs-for-ios-and-ipados-devices"></a>iOS 與 iPadOS 裝置的記錄

針對執行 iOS/iPadOS 的裝置，您可以使用偵錯記錄與在 Mac 電腦上執行的 **Xcode**：

1. 將 iOS/iPadOS 裝置連線到 Mac，然後前往 [應用程式] > [工具程式] 以開啟 [終端機] 應用程式。

2. 在 [動作] 下，選取 [包含資訊訊息] 和 [包含偵錯訊息]。

   ![選取記錄選項](../protect/media/troubleshoot-pkcs-certificate-profiles/message-options.png)

3. 重現問題，並將記錄儲存至文字檔：
   1. 選取 [編輯] > [全選] 以選取目前畫面上的所有訊息，然後選取 [編輯] > [複製] 以將訊息複製到剪貼簿。
   2. 開啟 [文字編輯] 應用程式，將複製的記錄貼入新文字檔中，然後儲存檔案。

適用於 iOS 與 iPadOS 裝置的公司入口網站記錄不包含 PKCS 憑證設定檔的相關資訊。

### <a name="logs-for-windows-devices"></a>Windows 裝置的記錄

針對執行 Windows 的裝置，請使用 Windows 事件記錄檔來診斷裝置 (使用 Intune 管理) 的註冊或裝置管理問題。

在裝置上，開啟 [事件檢視器] > [應用程式及服務記錄檔] > [Microsoft] > [Windows] > [DeviceManagement-Enterprise-Diagnostic-Provider]

![Windows 事件記錄檔](../protect/media/troubleshoot-pkcs-certificate-profiles/windows-event-log.png)

## <a name="common-errors"></a>常見錯誤

下一節會解決下列常見的錯誤：

- [RPC 伺服器無法使用 0x800706ba](#the-rpc-server-is-unavailable-0x800706ba)
- [找不到註冊原則伺服器 0x80094015](#an-enrollment-policy-server-cannot-be-located-0x80094015)
- [提交擱置中](#the-submission-is-pending)
- [參數不正確 0x80070057](#the-parameter-is-incorrect-0x80070057)
- [被原則模組拒絕](#denied-by-policy-module)
- [憑證設定檔停滯為擱置](#certificate-profile-stuck-as-pending)
- [錯誤 -2146875374 CERTSRV_E_SUBJECT_EMAIL_REQUIRED](#error--2146875374-certsrv_e_subject_email_required)

### <a name="the-rpc-server-is-unavailable-0x800706ba"></a>RPC 伺服器無法使用 0x800706ba

在 PFX 部署期間，受信任的根憑證會出現在裝置上，但 PFX 憑證不會出現在裝置上。 NDESConnector 記錄檔包含字串「RPC 伺服器無法使用。0x800706ba」，如下列範例的第一行所示：

```
IssuePfx - COMException: System.Runtime.InteropServices.COMException (0x800706BA): CCertRequest::Submit: The RPC server is unavailable. 0x800706ba (WIN32: 1722 RPC_S_SERVER_UNAVAILABLE)
IssuePfx -Generic Exception: System.ArgumentException: CCertRequest::Submit: The parameter is incorrect. 0x80070057 (WIN32: 87 ERROR_INVALID_PARAMETER)
IssuePfx - COMException: System.Runtime.InteropServices.COMException (0x80094800): The requested certificate template is not supported by this CA. (Exception from HRESULT: 0x80094800)
```

#### <a name="cause-1---incorrect-configuration-of-the-ca-in-intune"></a>原因 1 - Intune 中的 CA 設定不正確

當 PKCS 憑證設定檔指定錯誤的伺服器，或 CA 的名稱或 FQDN 包含拼字錯誤時，就會發生此問題。 CA 是在設定檔的下列屬性中指定：

- 憑證授權單位
- 憑證授權單位名稱

**解決方案**：

請檢閱下列設定，並加以修正 (若其不正確)：

- [憑證授權單位] 屬性會顯示您 CA 伺服器的內部 FQDN。
- [憑證授權單位名稱] 屬性會顯示您的 CA 名稱。

#### <a name="cause-2---ca-doesnt-support-certificate-renewal-for-requests-signed-by-previous-ca-certificates"></a>原因 2 - CA 不支援先前 CA 憑證所簽署之要求的憑證更新

如果 PKCS 憑證設定檔中的 CA FQDN 與名稱正確，請檢閱憑證授權單位伺服器上的 Windows 應用程式記錄檔。 尋找**事件識別碼 128**，其類似於下列範例：

```
Log Name: Application:
Source: Microsoft-Windows-CertificationAuthority
Event ID: 128
Level: Warning
Details:
An Authority Key Identifier was passed as part of the certificate request 2268. This feature has not been enabled. To enable specifying a CA key for certificate signing, run: "certutil -setreg ca\UseDefinedCACertInRequest 1" and then restart the service.
```

當 CA 憑證更新時，其必須簽署線上憑證狀態通訊協定 (OCSP) 回應簽署憑證。 簽署可讓 OCSP 回應簽署憑證透過檢查其撤銷狀態來驗證其他憑證。 預設不會啟用此簽署。

**解決方案**：

手動強制簽署憑證：

1. 在 CA 伺服器上，開啟提升權限的命令提示字元，然後執行下列命令：**certutil -setreg ca\UseDefinedCACertInRequest 1**
2. 重新啟動「憑證服務」服務。

「憑證服務」服務重新啟動之後，裝置就可以接收憑證。

### <a name="an-enrollment-policy-server-cannot-be-located-0x80094015"></a>找不到註冊原則伺服器 0x80094015

**找不到註冊原則伺服器**與 **0x80094015**，如下列範例所示：

```
IssuePfx - COMException: System.Runtime.InteropServices.COMException (0x80094015): An enrollment policy server cannot be located. (Exception from HRESULT: 0x80094015)
```

#### <a name="cause---certificate-enrollment-policy-server-name"></a>原因 - 憑證註冊原則伺服器名稱

如果裝載 Intune NDES 連接器的電腦找不到憑證註冊原則伺服器，就會發生此問題。

**解決方案**：

在裝載 NDES 連接器的電腦上，手動設定憑證註冊原則伺服器的名稱。 若要設定名稱，請使用 [Add-CertificateEnrollmentPolicyServer](https://docs.microsoft.com/powershell/module/pkiclient/add-certificateenrollmentpolicyserver?view=win10-ps) PowerShell Cmdlet。

### <a name="the-submission-is-pending"></a>提交擱置中

將 PKCS 憑證設定檔部署到行動裝置之後，就不會取得憑證，而且 NDESConnector 記錄檔會包含「提交擱置中」的字串，如下列範例所示：

```
IssuePfx - The submission is pending: Taken Under Submission
IssuePfx -Generic Exception: System.InvalidOperationException: IssuePfx - The submission is pending
```

此外，在憑證授權單位伺服器上，您可以在 [待決的要求] 資料夾中看到 PFX 要求：

> [!div class="mx-imgBorder"]
> ![憑證授權單位 [待決的要求] 資料夾的螢幕擷取畫面](./media/troubleshoot-pkcs-certificate-profiles/pending-requests.png)

#### <a name="cause---incorrect-configuration-for-request-handling"></a>原因 - 要求處理的設定不正確

如果選項 [將憑證要求狀態設為擱置。系統管理員必須明確發行憑證] 已在憑證授權單位 [屬性] > [原則模組] > [內容] 對話方塊中選取，就會發生此問題。

> [!div class="mx-imgBorder"]
> ![[原則模組] 屬性的螢幕擷取畫面](./media/troubleshoot-pkcs-certificate-profiles/policy-module-properties.png)

**解決方案**：

編輯要設定的 [原則模組] 屬性：**遵循憑證範本中的設定 (如果適用的話)。否則將自動發行憑證。**

### <a name="the-parameter-is-incorrect-0x80070057"></a>參數不正確 0x80070057

成功安裝並設定 Intune 憑證連接器之後，裝置就不會收到 PKCS 憑證，而且 NDESConnector 記錄檔會包含字串「參數不正確。0x80070057」，如下列範例所示：

```
CCertRequest::Submit: The parameter is incorrect. 0x80070057 (WIN32: 87 ERROR_INVALID_PARAMETER)
```

#### <a name="cause---configuration-of-the-pkcs-profile"></a>原因 - PKCS 設定檔的設定

如果 Intune 中的 PKCS 設定檔設定錯誤，就會發生此問題。 以下是常見的設定錯誤：

- 設定檔包含不正確的 CA 名稱。
- 主體別名 (SAN) 已針對電子郵件地址進行設定，但目標使用者尚未具備有效的電子郵件地址。 這種組合會導致 SAN 有無效的 Null 值。

**解決方案**：

確認 PKCS 設定檔的下列設定，然後等候裝置上的原則重新整理：

- 以 CA 的名稱設定
- 已指派給正確的使用者群組
- 群組中的使用者具有有效的電子郵件地址

如需詳細資訊，請參閱[透過 Intune 設定並使用 PKCS 憑證](../protect/certficates-pfx-configure.md)。

### <a name="denied-by-policy-module"></a>被原則模組拒絕

當裝置收到受信任的根憑證，但未收到 PFX 憑證，且 NDESConnector 記錄包含字串「提交失敗:被原則模組拒絕」，如下列範例所示：

```
IssuePfx - The submission failed: Denied by Policy Module
IssuePfx -Generic Exception: System.InvalidOperationException: IssuePfx - The submission failed
   at Microsoft.Management.Services.NdesConnector.MicrosoftCA.GetCertificate(PfxRequestDataStorage pfxRequestData, String containerName, String& certificate, String& password)
Issuing Pfx certificate for Device ID <Device ID> failed  
```

#### <a name="cause--computer-account-permissions-to-the-certificate-template"></a>原因 – 憑證範本的電腦帳戶權限

當裝載 Intune 憑證連接器之伺服器的電腦帳戶沒有憑證範本的權限時，就會發生此問題。

**解決方案**：

1. 使用具有系統管理權限的帳戶登入您的企業 CA。
2. 開啟 [憑證授權單位] 主控台、以滑鼠右鍵按一下 [憑證範本]，然後選取 [管理]。
3. 找到憑證範本，然後開啟範本的 [屬性] 對話方塊。
4. 選取 [安全性] 索引標籤，並新增您安裝 Microsoft Intune 憑證連接器之伺服器的電腦帳戶。 授與該帳戶 [讀取] 與 [註冊] 權限。
5. 選取 [套用] > [確定] 以儲存憑證範本，然後關閉 [憑證範本] 主控台。
6. 在 [憑證授權單位] 主控台中，以滑鼠右鍵按一下 [憑證範本] > [新增] > [要發出的憑證範本]。
7. 選取您修改的範本，然後按一下 [確定]。

如需詳細資訊，請參閱[設定 CA 上的憑證範本](../protect/certficates-pfx-configure.md#configure-certificate-templates-on-the-ca)。

### <a name="certificate-profile-stuck-as-pending"></a>憑證設定檔停滯為擱置

在 Microsoft Endpoint Manager 系統管理中心中，PKCS 憑證設定檔無法部署，狀態為 [擱置]。 NDESConnector 記錄檔中沒有明顯的錯誤。
由於未在記錄檔中清楚地識別此問題的原因，因此請解決以下原因。

#### <a name="cause-1---unprocessed-request-files"></a>原因 1 - 未處理的要求檔案

請檢閱要求檔案中指出無法處理的錯誤。

1. 在裝載 NDES 連接器的電腦上，使用 [檔案總管] 瀏覽至 **%programfiles%\Microsoft Intune\PfxRequest**。
2. 使用您慣用的文字編輯器，檢閱 [失敗] 與 [處理中] 資料夾中的檔案。

   > [!div class="mx-imgBorder"]
   > ![檢閱 PfxRequest 資料夾](./media/troubleshoot-pkcs-certificate-profiles/pfxrequest-folder.png)

3. 在這些檔案中，尋找指出錯誤或建議問題的項目。 使用網頁型搜尋，查閱錯誤訊息以取得有關要求無法處理的原因，以及那些問題的解決方案。

#### <a name="cause-2---misconfiguration-for-the-pkcs-certificate-profile"></a>原因 2 - PKCS 憑證設定檔設定錯誤

當您在 [失敗]、[處理中] 或 [成功] 資料夾中找不到要求檔案時，原因可能是與 PKCS 憑證設定檔相關聯的錯誤憑證。 例如，次級 CA 與設定檔相關聯，或使用錯誤的根憑證。

**解決方案**：

1. 請檢閱受信任的憑證設定檔，以確定您已將來自企業 CA 的根憑證部署到裝置。
2. 請檢閱您的 PKCS 憑證設定檔，以確保其會參考正確的 CA、憑證類型，以及將根憑證部署到裝置的受信任憑證設定檔。

如需詳細資訊，請參閱 Microsoft Intune 中的[使用憑證進行驗證](../protect/certificates-configure.md)。

### <a name="error--2146875374-certsrv_e_subject_email_required"></a>錯誤 -2146875374 CERTSRV_E_SUBJECT_EMAIL_REQUIRED

PKCS 憑證無法部署，而且發行 CA 上的憑證主控台會顯示一則訊息，其中包含字串 **-2146875374 CERTSRV_E_SUBJECT_EMAIL_REQUIRED**，如下列範例所示：

```
Active Directory Certificate Services denied request abc123 because The Email name is unavailable and cannot be added to the Subject or Subject Alternate name. 0x80094812 (-2146875374 CERTSRV_E_SUBJECT_EMAIL_REQUIRED). The request was for CN=” Common Name”.  Additional information: Denied by Policy Module”.
```

#### <a name="cause---supply-in-the-request-is-miscongifured"></a>原因 - [在要求中提供] 設定錯誤

如果未在憑證範本 [屬性] 對話方塊的 [主體名稱] 索引標籤上啟用 [在要求中提供] 選項，就會發生此問題。

> [!div class="mx-imgBorder"]
> ![設定 NDES 屬性](./media/troubleshoot-pkcs-certificate-profiles/supply-in-the-request.png)

**解決方案**：

編輯範本以解決設定問題：

1. 使用具有系統管理權限的帳戶登入您的企業 CA。
2. 開啟 [憑證授權單位] 主控台、以滑鼠右鍵按一下 [憑證範本]，然後選取 [管理]。
3. 開啟憑證範本的 [屬性] 對話方塊。
4. 在 [主體名稱]  索引標籤上，選取 [在要求中提供] 。
5. 選取 [確定] 以儲存憑證範本，然後關閉 [憑證範本] 主控台。
6. 在 [憑證授權單位] 主控台中，以滑鼠右鍵按一下 [範本] > [新增] > [要發出的憑證範本]。
7. 選取您修改的範本，然後選取 [確定]。

## <a name="next-steps"></a>後續步驟

如果您仍需要解決方案或正在尋找有關 Intune 的詳細資訊，請在我們的 [Microsoft Intune 論壇](https://social.technet.microsoft.com/Forums/home?category=microsoftintune&filter=alltypes&sort=lastpostdesc) \(英文\) 中張貼問題。 許多支援工程師、MVP 與我們的開發小組成員經常參加這些論壇，因此有很多人都可以幫忙。

若要向 Microsoft Intune 產品支援小組提出支援要求，請參閱[如何取得 Microsoft Intune 支援](../fundamentals/get-support.md)。
如需 PKCS 憑證部署的詳細資訊，請參閱下列文章：

- [透過 Intune 設定並使用 PKCS 憑證](../protect/certficates-pfx-configure.md)
- [在 Microsoft Intune 中設定您裝置的憑證設定檔](../protect/certificates-configure.md)
- [在 Microsoft Intune 中移除 SCEP 與 PKCS 憑證](../protect/remove-certificates.md)
