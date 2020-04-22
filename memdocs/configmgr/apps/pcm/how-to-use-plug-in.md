---
title: 如何使用轉換外掛程式
titleSuffix: Configuration Manager
description: 使用套件轉換管理員外掛程式來自訂分析和轉換程序。
ms.date: 08/24/2018
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 83cf156c-36de-483f-a9e6-2e06158f3b20
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: 4ca16ade5f8581cb124df39294c3cfc27627a346
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81688956"
---
# <a name="how-to-use-the-package-conversion-manager-plug-in"></a>如何使用套件轉換管理員外掛程式

適用於：  Configuration Manager (最新分支)

<!--1357861-->

套件轉換管理員外掛程式可協助您自訂分析和轉換程序。 若要使用套件轉換管理員外掛程式，請撰寫可執行檔或指令碼檔案來執行自訂作業。 接著，編輯設定檔 Microsoft.ConfigurationManagement.exe.config 來呼叫可執行檔或指令碼。 用來撰寫指令碼的最常見語言為 VBScript 或 PowerShell。

套件轉換管理員外掛程式會針對每個套件執行一次。 如果您一次分析或轉換多個套件，套件轉換管理員外掛程式每次都會執行。

> [!NOTE]  
> 如需 Configuration Manager 設定檔中套件轉換管理員元素的詳細資訊，請參閱[套件轉換管理員外掛程式設定 XML 的技術參考](plugin-config-xml.md)。



## <a name="default-process"></a>預設程序

根據預設，套件轉換管理員會執行下列動作：

1.  讀取 Configuration Manager 套件。  

2.  從套件中建立應用程式並新增預設屬性。  

3.  分析應用程式並判斷套件整備狀態。  

4.  依據套件轉換管理員作業，採取下列其中一個動作：  

    - **分析**：在 Configuration Manager 主控台中顯示套件整備狀態。  

    - **轉換**：將應用程式寫入 Configuration Manager 資料庫。  


## <a name="plug-in-based-process"></a>以外掛程式為基礎的程序 

當您使用外掛程式時，套件轉換管理員會執行下列動作：

1.  讀取 Configuration Manager 套件。  

2.  從套件中建立應用程式並新增預設屬性。  

3.  將應用程式轉換為 XML。 然後將檔案儲存到磁碟。  

4.  執行外掛程式指令碼來修改應用程式 XML。 如需詳細資訊，請參閱[套件轉換管理員外掛程式設定 XML 的技術參考](plugin-config-xml.md)。  

5.  將應用程式 XML 轉換為 Configuration Manager 應用程式。  

6.  分析應用程式並判斷套件整備狀態。  

7.  依據套件轉換管理員作業，採取下列其中一個動作：  

    - **分析**：在 Configuration Manager 主控台中顯示套件整備狀態。  

    - **轉換**：將應用程式寫入 Configuration Manager 資料庫。  



## <a name="see-also"></a>請參閱

[套件轉換管理員外掛程式設定 XML 的技術參考](plugin-config-xml.md)
