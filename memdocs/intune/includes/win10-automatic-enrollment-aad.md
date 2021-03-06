## <a name="enable-windows-10-automatic-enrollment"></a>啟用 Windows 10 自動註冊

使用者可利用自動註冊，在 Intune 中註冊其 Windows 10 裝置。 若要註冊，使用者必須將其公司帳戶新增至個人擁有的裝置，或將公司擁有的裝置加入 Azure Active Directory。 裝置會於背景註冊及加入 Azure Active Directory。 註冊之後，會使用 Intune 來管理裝置。

**先決條件**

- Azure Active Directory Premium 訂閱 ([試用訂閱](https://go.microsoft.com/fwlink/?LinkID=816845))
- Microsoft Intune 訂閱

### <a name="configure-automatic-mdm-enrollment"></a>設定自動執行 MDM 註冊

1. 登入 [Azure 入口網站](https://portal.azure.com)，然後選取 [Azure Active Directory]  。

   ![Azure 入口網站的螢幕擷取畫面](../enrollment/media/windows-enroll/auto-enroll-azure-main.png)

2. 選取 [行動性 (MDM 與 MAM)]  。

   ![Azure 入口網站的螢幕擷取畫面](../enrollment/media/windows-enroll/auto-enroll-mdm.png)

3. 選取 [Microsoft Intune]  。

   ![Azure 入口網站的螢幕擷取畫面](../enrollment/media/windows-enroll/auto-enroll-intune.png)

4. 設定 [MDM 使用者範圍]  。 指定哪些使用者的裝置應該由 Microsoft Intune 管理。 這些 Windows 10 裝置將會自動註冊，而由 Microsoft Intune 管理。

   - **無**：停用 MDM 自動註冊
   - **部分**：選取可以自動註冊其 Windows 10 裝置的「群組」 
   - **全部**：所有使用者都可以自動註冊其 Windows 10 裝置

      > [!IMPORTANT]
      > 針對 Windows BYOD 裝置，若為所有使用者 (或相同的使用者群組) 同時啟用了 MAM 使用者範圍和 MDM 使用者範圍 (自動 MDM 註冊)，則 MAM 使用者範圍優先順序會較高。 若有進行設定，裝置便不會註冊 MDM，且會套用 Windows 資訊保護 (WIP) 原則。
      >
      > 若您的目的是為 Windows BYOD 裝置啟用 MDM 自動註冊：請將 MDM 使用者範圍設為 [全部]  (或 [部分]  ，然後指定群組)，並將 MAM 使用者範圍設為 [無]  (或 [部分]  ，然後指定群組。請確認使用者並非同時是 MDM 和 MAM 使用者範圍所瞄準群組的成員)。
      >
      >針對[企業裝置](../enrollment/enrollment-restrictions-set.md#blocking-personal-windows-devices)，若同時啟用了 MDM 和 MAM 使用者範圍，則 MDM 使用者範圍的優先順序會較高。 裝置將會自動在設定的 MDM 中註冊。

   > [!NOTE]
   > MDM 使用者範圍必須設定為包含使用者物件的 Azure AD 群組。

   ![Azure 入口網站的螢幕擷取畫面](../enrollment/media/windows-enroll/auto-enroll-scope.png)

5. 使用下列 URL 的預設值：
    - **MDM 使用條款 URL**
    - **MDM 探索 URL**
    - **MDM 合規性 URL**

6. 選取 [儲存]  。

根據預設，並未對服務啟用雙因素驗證。 不過，於註冊裝置時，會建議使用雙因素驗證。 若要啟用雙重要素驗證，請在 Azure AD 中設定雙重要素驗證提供者，並將您的使用者帳戶設定為進行雙重要素驗證。 請參閱[開始使用 Azure Multi-Factor Authentication Server](https://docs.microsoft.com/azure/multi-factor-authentication/multi-factor-authentication-get-started-cloud)。
