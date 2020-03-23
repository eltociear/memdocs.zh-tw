---
title: 您的裝置遺失憑證 | Microsoft Docs
description: ''
keywords: ''
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 07/29/2019
ms.topic: article
ms.prod: ''
ms.service: microsoft-intune
ms.subservice: end-user
ms.technology: ''
ms.assetid: f0ba4cbb-ef0a-4335-86bf-f1d006867fa2
searchScope:
- User help
ROBOTS: ''
ms.reviewer: arnab
ms.suite: ems
ms.custom: intune-enduser
ms.collection: ''
ms.openlocfilehash: b4a16204afc99169183e02eb269ab24d7f63cc49
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/13/2020
ms.locfileid: "79346049"
---
# <a name="install-missing-certificate-required-by-your-organization"></a>安裝組織要求的遺漏憑證  

如果裝置未在 Intune 註冊，且遺漏必要的憑證，即無法登入公司入口網站應用程式。 當您嘗試登入時，您會看到下列訊息：

![screenshot-error-message-about-missing-certificate](./media/andr-cert_install-1-cert_missing.png)

您可以嘗試兩個選項來下載必要的憑證並註冊裝置。 

- 在公司入口網站應用程式中啟用瀏覽器存取。
- 識別公司或學校電腦上遺漏的憑證。 然後搜尋網際網路來下載遺漏的憑證。 

請先完成啟用瀏覽器存取的步驟。 之後，若仍然無法註冊裝置，請遵循步驟來在網際網路上尋找憑證。 

## <a name="enable-browser-access"></a>啟用瀏覽器存取
請完成這些步驟來啟用瀏覽器存取。 在啟用存取後，公司入口網站將會安裝適當的憑證並繼續註冊。    

1. 在公司入口網站應用程式中，前往右側的角落並選取功能表。  
2. 選取 [設定]  。  
3. 選取位於 [啟用瀏覽器存取]  旁邊的 [啟用]  。  
4. 在裝置管理員畫面上，選取 [啟用]  。 

## <a name="identify-and-download-the-missing-certificate-through-web-search"></a>透過 Web 搜尋識別及下載遺漏的憑證
完成這些步驟來手動識別及在裝置上安裝憑證。  

1. 在電腦上開啟 Internet Explorer。 如果您沒有可用於此用途的電腦，請連絡公司支援人員。 如需公司支援人員的連絡資訊，請查看[公司入口網站](https://go.microsoft.com/fwlink/?linkid=2010980)。

2. 請移至[公司入口網站](https://go.microsoft.com/fwlink/?linkid=2010980)，並使用您的公司或學校認證登入。

3. 在瀏覽器的網址列最右側，選擇看似掛鎖的符號，如下方螢幕擷取畫面所示。

    ![screenshot-internet-explorer-address-bar-padlock-symbol](./media/andr-missing-cert-ie-padlock-symbol.png)

    如果未顯示掛鎖符號，請停止作業，並連絡您公司的支援人員。 鎖頭符號表示您已經安全地登入，因此除非您看到該符號，否則不應該繼續。

4. 按一下 [檢視憑證]  。

    ![screenshot-internet-explorer-view-certificates-button-on-website-identification-dialog](./media/andr-missg-cert-ie-view-cert-button.png)

5. 選擇 [憑證路徑]  索引標籤，然後找出您需要從網際網路取得的憑證。 您可在上述範例螢幕擷取畫面中反白顯示之憑證的相同位置，找到所需憑證的名稱。

6. 使用搜尋引擎 (例如 Bing 或 Google) 搜尋您在上一節中識別的遺失憑證名稱。 憑證可能會以不同的副檔名結束，例如 ".crt" 或 ".pem" 等。

7. 從網站下載根憑證。

8. 下載憑證之後，從您的裝置頂端下拉以開啟通知，然後點選通知清單中的憑證名稱。

4. 在下方螢幕擷取畫面顯示的 [命名憑證]  對話方塊中，接受預設憑證名稱。

5. 請確認 [認證使用]  設為 [用於 VPN 和應用程式]  ，然後點選 [確定]  。

    ![screenshot-certificate-name-dialog-showing-certificate-name](./media/andr-missing-cert-cert-name.png)

6. 關閉公司入口網站應用程式。

7. 重新開啟公司入口網站應用程式。 您現在應該能夠登入公司入口網站應用程式。 如果您需要協助，請連絡您公司的支援人員。

如果您已經遵循相關步驟，卻仍顯示上述相同的「遺失憑證」訊息，可能表示您需要公司支援人員協助安裝其他憑證。 請使用可在[公司入口網站](https://go.microsoft.com/fwlink/?linkid=2010980)取得的連絡資訊來連絡您公司的支援人員以取得協助。

## <a name="next-steps"></a>後續步驟  

是否仍需要協助？ 請連絡您公司的支援人員。 如需連絡資訊，請查看[公司入口網站](https://go.microsoft.com/fwlink/?linkid=2010980)。  
