---
title: 從 Intune 公司入口網站取得 macOS 裝置的修復金鑰
description: 檢視已註冊的受控 macOS 裝置其修復金鑰。
keywords: ''
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 12/04/2019
ms.topic: end-user-help
ms.prod: ''
ms.service: microsoft-intune
ms.subservice: end-user
ms.technology: ''
ms.assetid: ''
searchScope:
- User help
ROBOTS: ''
ms.reviewer: ''
ms.suite: ems
ms.custom: intune-enduser
ms.collection: ''
ms.openlocfilehash: e206725f4c68a370f473a2c378d02148b9f73259
ms.sourcegitcommit: a77ba49424803fddcaf23326f1befbc004e48ac9
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/27/2020
ms.locfileid: "83881271"
---
# <a name="get-a-recovery-key-for-a-macos-device"></a>取得 macOS 裝置的修復金鑰

使用公司入口網站取得已鎖定 macOS 裝置的修復金鑰。 如果您忘記裝置密碼，則可從另一部裝置登入公司入口網站來擷取金鑰。  

## <a name="get-recovery-key-from-company-portal-website"></a>從公司入口網站取得修復金鑰

此選項適用於組織使用 FileVault 來加密的裝置。 不適用於個人所加密的裝置。

1. 在任何裝置上，登入[公司入口網站](https://portal.manage.microsoft.com)，然後選取 [功能表]  按鈕 > [裝置]  。  
2. 選取加密的 macOS 裝置。  
3. 選取 [取得修復金鑰]  。  

    ![公司入口網站的螢幕擷取畫面，其中醒目提示 [取得修復金鑰] 區段。](./media/1907-recovery2-cpweb-intune.PNG)  

4. 修復金鑰隨即出現。

    ![公司入口網站的螢幕擷取畫面，其中顯示修復金鑰。](./media/1907-recovery-cpweb-intune.PNG)  

    基於安全考量，此金鑰會在五分鐘後消失。 若要再次查看金鑰，請選取 [取得修復金鑰]  。

如果找不到金鑰，但裝置已正確加密，請連絡組織的支援人員。 如需連絡資訊，請查看[公司入口網站](https://go.microsoft.com/fwlink/?linkid=2010980)。  

## <a name="get-recovery-key-from-company-portal-app-for-ios"></a>從 iOS 版公司入口網站應用程式取得修復金鑰

您可以使用 iOS 版公司入口網站應用程式來擷取個人修復金鑰 (FileVault 金鑰)。 具有個人修復金鑰的裝置必須向 Intune 註冊，並透過 Intune 以 FileVault 加密。 此選項不適用於個人加密的裝置。 

使用公司入口網站應用程式，即可開啟 Safari Web 檢視，並擷取個人修復金鑰。 

1. 開啟 [公司入口網站]。
2. 按一下 [取得修復金鑰]  。

    ![iOS 版公司入口網站應用程式的螢幕擷取畫面，其中顯示修復金鑰](./media/get-recovery-key-cpweb-02.png)  

公司入口網站會在 Safari Web 檢視中開啟並顯示金鑰。 

## <a name="it-pro-support"></a>IT 專業人員支援

如果您是 IT 支援人員，並想要設定和管理 macOS 裝置的 FileVault 加密，請參閱[搭配 Intune 使用裝置加密](/intune/protect/encrypt-devices)。

## <a name="next-steps"></a>後續步驟

了解可從公司入口網站執行的其他動作。 如需動作清單，請參閱[使用 Intune 公司入口網站](using-the-intune-company-portal-website.md)。  

是否仍需要協助？ 請連絡 IT 支援人員。 如需連絡資訊，請查看[公司入口網站](https://go.microsoft.com/fwlink/?linkid=2010980)。  
