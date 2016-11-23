---
title: "適用於 iOS 和 Android 的 Azure 資訊保護應用程式常見問題集 | Azure 資訊保護"
description: 
keywords: "某些常見問題可協助您使用適用於 iOS 和 Android 的 Azure 資訊保護應用程式"
author: cabailey
manager: mbaldwin
ms.date: 10/14/2016
ms.topic: article
ms.prod: azure
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 539b4ff8-5d3b-4c4d-9c84-c14da83ff76d
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: c03bcfc5590035ab0d51cb3b4f2b7196db458ea3
ms.openlocfilehash: 1829557b41d2c49ac661cbde96f69dda2ccc5b19


---

# 適用於 iOS 和 Android 的 Microsoft Azure 資訊保護應用程式常見問答集

*適用於︰Active Directory Rights Management Services、Azure 資訊保護*

本頁回答適用於 iOS 和 Android 的 Azure 資訊保護應用程式常見問題。

## Azure 資訊保護應用程式可以做什麼？

如果您的電子郵件應用程式原本不支援權限管理資料保護，此應用程式可讓您檢視受版權保護的電子郵件訊息 (.rpmsg 檔案)。 此應用程式也可讓您檢視受版權保護的 PDF 檔案、圖片和文字檔案。 目前，您無法使用此應用程式來新建受保護的電子郵件訊息，亦無法回覆，或建立或編輯受保護的檔案。

## 我可以在受 SharePoint 保護的文件庫及商務用 OneDrive 中開啟 PDF 檔案嗎？

可以，您可以開啟其他人透過 SharePoint 及商務用 OneDrive 與您共用的受保護 PDF 檔案。 點選連結，然後選擇此應用程式開啟檔案。 

## 如何開始使用檢視器應用程式？

您必須存取行動裝置中受應用程式支援的其中一個檔案，才會看到檢視器作用。 例如：

- **.rpmsg 檔案**︰這是當您的行動裝置上的電子郵件應用程式原本不支援權限管理資料保護時，顯示為電子郵件附件的受版權保護的電子郵件訊息。 
    
    使用其他裝置，將您可以從行動裝置存取的受版權保護的電子郵件訊息傳送給自己。 例如，使用 Windows 電腦的 Outlook。 如需原本支援版權管理的電子郵件用戶端清單，請參閱[支援 Azure Rights Management 資料保護的應用程式](../get-started/requirements-applications.md)頁面的 [電子郵件] 資料行。

- **受版權保護的 PDF 檔案**︰使用 Rights Management 共用應用程式，從原本支援權限管理的 Windows 電腦或 PDF 應用程式，以電子郵件附件的方式將受版權保護的 PDF 檔案傳送給自己。 或者，將 PDF 檔案上傳至受保護的 SharePoint 程式庫，然後使用您的電子郵件地址共用此檔案。

- **.ptxt 或 .pjpg 或 .ppng**︰使用 Windows 電腦的 Rights Management 共用應用程式和 [共用保護的檔案][](sharing-app-protect-by-email.md) 選項，將受保護的檔案當成電子郵件附件傳送給自己。 如需可供測試用的檔案類型完整清單，請參閱《Rights Management 共用應用程式系統管理員指南》中[支援的檔案類型與副檔名](sharing-app-admin-guide-technical.md#supported-file-types-and-file-name-extensions)一節的第一份資料表。 

若要在 Azure 資訊保護檢視器應用程式中檢視這些檔案，請點選電子郵件附件或連結。 當系統提示您選取開啟檔案的應用程式時，請選取 [AIP Viewer] (AIP 檢視器) 應用程式。 接著，系統會提示您以您的工作或學校帳戶登入。 驗證成功後，Azure 資訊保護應用程式會顯示電子郵件或檔案供您閱讀。

## 我應該使用什麼認證登入此應用程式？

貴組織如已有 AD RMS 內部部署 (有行動裝置延伸模組)，或使用 Azure Rights Management Service，您就可以使用您的認證登入。 如果沒有，您可以使用 [Azure Rights Management 頁面](https://portal.office.com/signup?sku=rms&ru=https%3A%2F%2Fportal.azurerms.com%2F%23%2Fdownload)註冊免費的新帳戶。

## 我可以用個人的免費帳戶電子郵件地址，例如 Hotmail 或 Gmail 帳戶註冊嗎？

尚未提供此服務。 目前只能註冊公司電子郵件地址 (工作或學校帳戶)。 我們正在為提供個人電子郵件地址支援而努力，一完成即會更新此項目。

## 此應用程式可以開啟哪些格式的檔案？

您可以開啟 .rpmsg、.pdf、.ppdf、.pjpg、.ptxt 及其他數種文字和影像檔案格式。

##  我要如何提出對此應用程式的意見反應？

在應用程式中移至 [設定] > [傳送意見反應]。


## 我的問題未獲得解答，我該怎麼辦？

請將問題張貼在 [Yammer 網站](http://www.yammer.com/AskIPTeam)，或[傳送電子郵件給資訊保護小組](mailto:askIPteam@microsoft.com?subject=Question%20about%20Azure%20Information%20Protection%20app)。



<!--HONumber=Oct16_HO2-->


