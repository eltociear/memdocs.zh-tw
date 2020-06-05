---
title: 在 Intune 中使用 BitLocker 加密 Windows 10 裝置
titleSuffix: Microsoft Intune
description: 使用 BitLocker 內建加密方法來加密裝置，並在 Intune 入口網站管理這些已加密裝置的修復金鑰。
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 05/18/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: annovich
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.openlocfilehash: 16a2558a0f4b002528e749f4a66d3341e83c8576
ms.sourcegitcommit: 302556d3b03f1a4eb9a5a9ce6138b8119d901575
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/27/2020
ms.locfileid: "83989663"
---
# <a name="manage-bitlocker-policy-for-windows-10-in-intune"></a>在 Intune 中管理 Windows 10 的 BitLocker 原則

使用 Intune 在執行 Windows 10 的裝置上設定 BitLocker 磁碟機加密。

BitLocker 適用於執行 Windows 10 或更新版本的裝置。 裝置必須有支援的 TPM，才能設定某些 BitLocker 設定。

使用下列其中一項原則類型，在您管理的裝置設定 BitLocker

- **[Windows 10 BitLocker 的端點安全性磁碟加密原則](#create-an-endpoint-security-policy-for-bitlocker)** 。 「端點安全性」 中的 BitLocker 設定檔是專用於設定 BitLocker 的一組設定。

  檢視[磁碟加密原則中 BitLocker 設定檔](../protect/endpoint-security-disk-encryption-profile-settings.md#bitlocker)提供的 BitLocker 設定。

- **[適用於 Windows 10 BitLocker 的 Endpoint Protection 裝置設定檔](#create-an-endpoint-security-policy-for-bitlocker)** 。 BitLocker 設定是 Windows 10 Endpoint Protection 的可用設定類別之一。

  檢視可供 [Endpoint Protection 設定檔表單裝置設定原則中之 BitLocker](../protect/endpoint-protection-windows-10.md#windows-settings) 使用的 BitLocker 設定。

> [!TIP]
> Intune 所提供的內建[加密報告](encryption-monitor.md)會顯示涵蓋所有受控裝置的裝置加密狀態詳細資料。 您在 Intune 使用 BitLocker 加密 Windows 10 裝置後，即可於檢視加密報告時，檢視並擷取 BitLocker 修復金鑰。
>
> 您也可以從裝置存取 BitLocker 的重要資訊，如同在 Azure Active Directory (Azure AD) 中找到的。
顯示涵蓋所有受控裝置之裝置加密狀態詳細資料的[加密報告](encryption-monitor.md)。

## <a name="permissions-to-manage-bitlocker"></a>管理 BitLocker 所須的權限

若要在 Intune 中管理 BitLocker，您的帳戶必須有適用的 Intune [角色型存取控制](../fundamentals/role-based-access-control.md) (RBAC) 權限。

下列為屬於遠端工作類別的 BitLocker 權限，以及授與權限的內建 RBAC 角色：

- **輪替 BitLocker 金鑰**
  - 技術服務人員

## <a name="create-and-deploy-policy"></a>建立並部署原則

用下列其中一個程序來建立您偏好的原則類型。

### <a name="create-an-endpoint-security-policy-for-bitlocker"></a>建立 BitLocker 的端點安全性原則

1. 登入 [Microsoft Endpoint Manager 系統管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)。

2. 選取 [端點安全性] > [磁碟加密] > [建立原則]。

3. 設定下列選項：
   1. **平台**：Windows 10 或更新版本
   2. **設定檔**：BitLocker

   ![選取 BitLocker 設定檔](./media/encrypt-devices/select-windows-bitlocker-es.png)

4. 在**組態設定**頁面中，設定符合您商務需求的 BitLocker 設定。  

   若您想要以無訊息方式啟用 BitLocker，請參閱此文章中的[在裝置上以無訊息方式啟用 BitLocker](#silently-enable-bitlocker-on-devices)，以了解必須使用的其他必要條件及設定組態。

   選取 [下一步]。

5. 在**範圍 (標籤)** 頁面上，選擇 **[選取範圍標籤]** 以開啟 [選取標籤] 窗格，並將範圍標籤指派到設定檔。

   選取 [下一步] 以繼續進行操作。

6. 在 [指派] 頁面上，選取將接收此設定檔的群組。 如需指派設定檔的詳細資訊，請參閱＜指派使用者和裝置設定檔＞。

   選取 [下一步]。

7. 在 [檢閱 + 建立] 頁面上，當您完成操作時，請選擇 [建立]。 當您為自己建立的設定檔選取原則類型時，新的設定檔就會顯示在清單中。

### <a name="create-a-device-configuration-profile-for-bitlocker"></a>建立適用於 BitLocker 的裝置組態設定檔

1. 登入 [Microsoft Endpoint Manager 系統管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)。

2. 選取 [裝置] > [組態設定檔] > [建立設定檔]。

3. 設定下列選項：
   1. **平台**：Windows 10 及更新版本
   2. **設定檔類型**：Endpoint Protection

   ![選取 BitLocker 設定檔](./media/encrypt-devices/select-windows-bitlocker-dc.png)

4. 選取 [設定] > [Windows 加密]。

   ![Bitlocker 設定](./media/encrypt-devices/bitlocker-settings.png)

5. 設定符合您商務需求的 BitLocker 設定。

   若您想要以無訊息方式啟用 BitLocker，請參閱[在裝置上以無訊息方式啟用 BitLocker](#silently-enable-bitlocker-on-devices)，此文章內容包含必須使用的其他必要條件及設定組態。

6. 選取 [確定]。

7. 完成其他組態設定，然後儲存設定檔。

## <a name="manage-bitlocker"></a>管理 BitLocker

若要檢視接收 BitLocker 原則的裝置相關資訊，請參閱[監視器磁碟加密](../protect/encryption-monitor.md)。 您也可以在檢視加密報告時，檢視和擷取 BitLocker 修復金鑰。

### <a name="silently-enable-bitlocker-on-devices"></a>在裝置上以無訊息方式啟用 BitLocker

您可以設定 BitLocker 原則，並以自動且無訊息的方式在裝置上啟用 BitLocker。 這表示即使終端使用者不是裝置上的本機系統管理員，BitLocker 也能成功啟用，而不會向該使用者顯示任何 UI。

**裝置必要條件**：

裝置必須符合下列條件，才能以無訊息方式啟用 BitLocker：

- 該裝置必須執行 Windows 10 1809 版或更新版本
- 該裝置必須已加入 Azure AD  

**BitLocker 原則設定**：

下列兩項 *BitLocker 基本設定*必須在 BitLocker 原則中設定：

- [其他磁碟加密警告] = 封鎖。
- [允許標準使用者在 Azure AD Join 時啟用加密] = 允許

BitLocker 原則**不得要求**使用啟動 PIN 或啟動金鑰。 當 TPM 啟動 PIN 或啟動金鑰為「必要」時，無法以無訊息方式啟用 BitLocker，且 BitLocker 必須與終端使用者互動。  您必須透過相同原則中的下列三個 *BitLocker OS 磁碟機設定*以符合這項需求：

- **相容 TPM 啟動 PIN** 不得設定為「需要使用 TPM 的啟動 PIN」
- **相容 TPM 啟動金鑰**不得設定為「需要使用 TPM 的啟動金鑰」
- **相容 TPM 啟動金鑰與 PIN**不得設定為「需要使用 TPM 的啟動金鑰與 PIN」

### <a name="view-details-for-recovery-keys"></a>檢視修復金鑰詳細資料

Intune 可讓您從 Intune 入口網站內存取 Azure AD 刀鋒視窗中的 BitLocker，以便檢視您 Windows 10 裝置的 BitLocker 金鑰識別碼與修復金鑰。 為了能夠存取，裝置必須將其金鑰委付給 Azure AD。

1. 登入 [Microsoft Endpoint Manager 系統管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)。

2. 選取 [裝置] > [所有裝置]。

3. 從清單中選取裝置，然後在 [監視] 下方選取 [修復金鑰]。
  
   當 Azure AD 中有可用的金鑰時，會提供下列資訊：
   - BitLocker 金鑰識別碼
   - BitLocker 修復金鑰
   - 磁碟機類型

   當金鑰不在 Azure AD 時，Intune 會顯示 [找不到此裝置的 BitLocker 金鑰]。

您可以使用 [BitLocker 設定服務提供者](https://docs.microsoft.com/windows/client-management/mdm/bitlocker-csp) (CSP) 來取得 BitLocker 的資訊。 Windows 10 1703 版和更新版本，以及 Windows 10 專業版 1809 版和更新版本支援 BitLocker CSP。

### <a name="rotate-bitlocker-recovery-keys"></a>輪替 BitLocker 修復金鑰

您可以使用 Intune 裝置動作來遠端輪替執行 Windows 10 1909 版或更新版本之裝置的 BitLocker 修復金鑰。

#### <a name="prerequisites"></a>先決條件

裝置必須符合下列必要條件，以支援 BitLocker 修復金鑰的輪替：

- 裝置必須執行 Windows 10 1909 版或更新版本

- 已加入 Azure AD 的裝置和已加入混合式的裝置必須啟用金鑰輪替支援：

  - **用戶端驅動的復原密碼旋轉**

  此設定位於 [Windows 加密] 底下，且為 Windows 10 Endpoint Protection 裝置設定原則的一部分。

#### <a name="to-rotate-the-bitlocker-recovery-key"></a>輪替 BitLocker 修復金鑰

1. 登入 [Microsoft Endpoint Manager 系統管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)。

2. 選取 [裝置] > [所有裝置]。

3. 在您管理的裝置清單中，選取裝置，選取 [其他]，然後選取 [BitLocker 金鑰輪替] 裝置遠端動作。

4. 在裝置的**概觀**頁面上，選取 **[BitLocker 金鑰輪替]** 。 若沒看到此選項，請選取省略號 ( **…** ) 以顯示其他選項，然後選取 **[BitLocker 金鑰輪替]** 裝置遠端動作。

   ![選取省略號以檢視更多選項](./media/encrypt-devices/select-more.png)

## <a name="next-steps"></a>後續步驟

[管理 FileVault 原則](../protect/encrypt-devices-filevault.md)

[監視磁碟加密](../protect/encryption-monitor.md)
