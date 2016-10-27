---
title: "資料保護的應用程式支援 | Azure 資訊保護"
description: "找出使用 RMS API 以原生方式支援 Azure 資訊保護之 Azure Rights Management Service 的應用程式。"
author: cabailey
manager: mbaldwin
ms.date: 10/03/2016
ms.topic: get-started-article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 7b33bcb8-63da-46be-ad56-b06de97822fa
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 451952f7d0c293db2c9d4f5040ef0e14aa973866
ms.openlocfilehash: a9b0fcddf9b11a8ab2d105ca5fc778831913bb72


---


# 支援 Azure Rights Management 資料保護的應用程式

>*適用於︰Azure 資訊保護、Office 365*


請使用下表找出以原生方式支援提供 Azure 資訊保護資料保護之 Azure Rights Management Service (Azure RMS) 的應用程式。 

這些應用程式使用 Rights Management API 緊密整合 Rights Management 支援，來支援使用限制。 這些應用程式也稱為 RMS 創新。

除非另外註明，否則支援的功能適用於 Azure RMS 與 AD RMS 兩者。 此外，在 iOS、Android、OS X 和 Windows Phone 8.1 上的 AD RMS 支援需要 [Active Directory 權限管理服務行動裝置延伸模組](https://technet.microsoft.com/library/dn673574.aspx)。

表格欄位的相關資訊：

-   **受保護的 PDF**：這些檔案具有 .ppdf 副檔名，而且會在您使用 RMS 共用應用程式來透過電子郵件共用 Office 檔案和 PDF 檔案時自動建立。 RMS 共用應用程式和 iOS 與 Android 的 Azure 資訊保護應用程式包含受保護 PDF 檔案的讀取器。 如果您之前使用 Azure RMS 或 AD RMS 建立保護的 PDF 檔案，您可以繼續在 Windows、iOS 和 Android 裝置上，使用 Foxit Reader 和 Nitro Pro 讀取這些檔案。

-   **電子郵件：**列出的電子郵件用戶端可以保護電子郵件訊息本身，這樣會自動保護任何附加檔案。 在此情況下，用戶端的預覽功能可讓授權的收件者看見受保護的內容 (訊息和附件)。 不過，若電子郵件訊息本身未受保護，但附件受到保護，則用戶端預覽功能無法讓授權的收件者看見受保護的附件。

-   **其他檔案類型**：文字和影像檔包含副檔名為 .txt、.xml、.jpg 和 .jpeg 的檔案。 這些檔案在受到 Rights Management 原生保護後會變更其副檔名並成為唯讀狀態。 無法受到原生保護的檔案在 Rights Management 對其進行一般保護後，會有 .pfile 副檔名。 如需詳細資訊，請參閱[Rights Management 共用應用程式系統管理員指南](../rms-client/sharing-app-admin-guide.md)。


|**裝置作業系統**|Word、Excel、PowerPoint|受保護的 PDF|電子郵件|其他檔案類型|
|-------------------------------|---------------------------|-----------------|---------|--------------------|
|**Windows**|Office 2010<br /><br />Office 2013<br /><br />Office 2016 <br /><br />Office Mobile 應用程式 (僅適用於 Azure RMS) [[1]](#footnote-1)<br /><br />Office Online [[2]](#footnote-2)|Gaaiho Doc<br /><br />GigaTrust Desktop PDF Client for Adobe<br /><br />Foxit Reader<br /><br />Nitro PDF 閱讀程式<br /><br />RMS 共用應用程式|Outlook 2010<br /><br />Outlook 2013<br /><br />Office 2016 <br /><br />Outlook Web App (OWA) [[3]](#footnote-3)<br /><br />Windows Mail [[4]](#footnote-4)|適用於 Windows 的 RMS 共用應用程式：文字、影像、pfile<br /><br />Siemens JT2Go：JT 檔案 (僅限 Windows 10)|
|**iOS**|Office for iPad and iPhone [[5]](#footnote-5)<br /><br />Office Online [[2]](#footnote-2)<br /><br />TITUS 文件|Azure 資訊保護應用程式 [[1]](#footnote-1)<br /><br /> Foxit Reader<br /><br />TITUS 文件|Azure 資訊保護應用程式 [[1]](#footnote-1)<br /><br />Citrix WorxMail [[6]](#footnote-6)<br /><br />NitroDesk [[4]](#footnote-4)<br /><br />Outlook for iPad and iPhone [[4]](#footnote-4)<br /><br />OWA for iOS [[3]](#footnote-3)<br /><br />TITUS Mail|Azure 資訊保護應用程式 [[1]](#footnote-1)：文字、影像、pfile<br /><br />TITUS 文件︰Pfile|
|**Android**|GigaTrust App for Android<br /><br />Office Online [[2]](#footnote-2)<br /><br />Office Mobile (僅限 Azure RMS) [[1]](#footnote-1)|Azure 資訊保護應用程式 [[1]](#footnote-1)<br /><br />GigaTrust App for Android<br /><br />Foxit Reader<br /><br />RMS 共用應用程式 [[1]](#footnote-1)|9Folders [[4]](#footnote-4)<br /><br />Azure 資訊保護應用程式 [[1]](#footnote-1)<br /><br />GigaTrust App for Android [[4]](#footnote-4)<br /><br />Citrix WorxMail [[6]](#footnote-6)<br /><br />NitroDesk [[4]](#footnote-4)<br /><br />Outlook for Android [[4]](#footnote-4)<br /><br />OWA for Android [[3]](#footnote-3) 和 [[7]](#footnote-7)<br /><br />Samsung Email (S3 和更新版本) [[7]](#footnote-7)<br /><br />TITUS Classification for Mobile|Azure 資訊保護應用程式 [[1]](#footnote-1)：文字、影像、pfile|
|**OS X**|Office 2011 (僅適用於 AD RMS)<br /><br />Office 2016 for Mac<br /><br />Office Online [[2]](#footnote-2)|Foxit Reader<br /><br />RMS 共用應用程式 [[1]](#footnote-1)|Outlook 2011 (僅適用於 AD RMS)<br /><br />Outlook 2016 for Mac<br /><br />Outlook for Mac|RMS 共用應用程式 [[1]](#footnote-1)︰文字、影像、pfile|
|**Windows 10 Mobile**|Office Mobile 應用程式(僅適用於 Azure RMS) [[1]](#footnote-1)|不支援|Citrix WorxMail [[6]](#footnote-6)<br /><br />Outlook Mail|不支援|
|**Windows RT**|Office 2013 RT<br /><br />Office Online [[2]](#footnote-2)|不支援|Outlook 2013 RT<br /><br />Windows 郵件應用程式<br /><br />Windows Mail [[4]](#footnote-4)|Siemens JT2Go：JT 檔案|
|**Windows Phone 8.1**|Office Mobile (僅適用於 AD RMS)|RMS 共用應用程式 [[1]](#footnote-1)|Outlook Mobile [[4]](#footnote-4)|RMS 共用應用程式 [[1]](#footnote-1)︰文字、影像、pfile|
|**Blackberry 10**|不支援|不支援|Blackberry 電子郵件 [[4]](#footnote-4)|不支援|


##### 註腳 1
支援檢視受保護的內容。

##### 註腳 2 
支援檢視 SharePoint Online、商務用 OneDrive 和 Outlook Web Access 中受保護的內容。

##### 註腳 3
如果收件者收到受保護電子郵件，但並未使用 Exchange 作為郵件伺服器，或寄件者屬於其他組織，收件者就只能在豐富型電子郵件用戶端 (如 Outlook) 中開啟此內容。 不能從 Outlook Web Access 開啟此內容。

##### 註腳 4
使用 Exchange ActiveSync IRM，必須由 Exchange 系統管理員啟用。 使用者可以檢視、回覆和全部回覆受保護的電子郵件訊息，但使用者本身無法保護新的電子郵件訊息。

如果收件者收到受保護電子郵件，但並未使用 Exchange 作為郵件伺服器，或寄件者屬於其他組織，收件者就只能在豐富型電子郵件用戶端 (如 Outlook) 中開啟此內容。 收件者無法從 Outlook Web Access 或使用 Exchange Active Sync IRM 的行動郵件用戶端開啟此內容。

##### 註腳 5
支援檢視和編輯受保護的文件。 如需詳細資訊，請參閱下列 Office 部落格文章︰[Azure Rights Management 支援已適用 Office for iPad and iPhone](https://blogs.office.com/2015/07/22/azure-rights-management-support-comes-to-office-for-ipad-and-iphone-2/)

##### 註腳 6
如需詳細資訊，請參閱 [WorxMail 的 Citrix 產品文件集](http://docs.citrix.com/en-us/worx-mobile-apps/10/xmob-worx-mail.html)。

##### 註腳 7
如需詳細資訊，請參閱下列 Office 部落格文章︰[OWA for Android 目前可在選取的裝置上使用](http://blogs.office.com/2014/06/11/owa-for-android-now-available-on-select-devices/)

## Office 的 Azure RMS 支援的詳細資訊

Azure RMS 與 Word、Excel、PowerPoint 及 Outlook 應用程式緊密整合；這些應用程式通常稱此功能為資訊版權管理 (IRM)。 下列 Office 用戶端版本支援使用 Azure RMS 保護檔案和電子郵件︰

- Office Professional Plus 2016

- Office Professional Plus 2013

- Office Professional Plus 2010

所有版本的 Office (不包括 Office 2007) 都支援取用受保護的內容。

Azure RMS 與 Office Professional Plus 2010 或 Office Professional 2010：

- 需要適用於 Windows 的 Rights Management 共用應用程式

- 不支援 Windows 10

## iOS 與 Android 的 Azure 資訊保護應用程式詳細資訊

iOS 與 Android 的 Azure 資訊保護應用程式現在已取代這些裝置的 RMS 共用應用程式。 它除提供相同的功能，另支援受權限保護的電子郵件訊息以及 SharePoint Online 上受權限保護的 PDF 檔案。

如果您的 iOS 和 Android 裝置是由 Microsoft Intune 註冊，您可以使用原則管理的應用程式來部署及管理此應用程式。 如需詳細資訊，請參閱 Intune 文件的[在 Microsoft Intune 主控台中設定及部署行動應用程式管理原則](/intune/deploy-use/configure-and-deploy-mobile-application-management-policies-in-the-microsoft-intune-console)。 在此 Intune 文件的步驟 2 中，使用發行原則管理應用程式的指示。

如需詳細資訊，請參閱[適用於 iOS 和 Android 的 Microsoft Azure 資訊保護應用程式常見問答集](../rms-client/mobile-app-faq.md)。


## Rights Management 共用應用程式的詳細資訊

如需有關適用於 Windows 之 Rights Management 共用應用程式的詳細資訊，請參閱下列資源：

-   [Rights Management 共用應用程式系統管理員指南 (英文)](../rms-client/sharing-app-admin-guide.md)

-   [Rights Management 共用應用程式使用者指南 (英文)](../rms-client/sharing-app-user-guide.md)

如需有關行動平台之 Rights Management 共用應用程式的詳細資訊，請參閱下列資源：

-   使用 [Microsoft Rights Management 頁面](http://go.microsoft.com/fwlink/?LinkId=303970)上的連結，下載相關的應用程式

-   [行動平台的 Microsoft Rights Management 共用應用程式常見問題集](https://technet.microsoft.com/dn451248)

> [!NOTE]
> 適用於 iOS 和 Android 的 RMS 共用應用程式現在已由 Azure 資訊保護應用程式取代。

## 其他支援 Azure RMS 之應用程式的詳細資訊

除了資料表中的應用程式，任何支援 RMS API 的應用程式都可以和 Azure RMS 整合，包括︰

- 使用 RMS SDK 在內部撰寫的企業營運系統應用程式

- 使用 RMS SDK 撰寫之軟體廠商的應用程式。

如需有關 SDK 的詳細資訊，請參閱 [Microsoft Rights Management SDK](../develop/developers-guide.md)。

## Azure RMS 不支援的應用程式

Azure RMS 目前不支援下列應用程式，包括：

-   Microsoft Office for Mac 2011

-   Microsoft OneDrive for Business for SharePoint Server 2013

-   XPS 檢視器
 
此外，RMS 共用應用程式具有下列限制：

-   對於 Windows 電腦：需要 Windows 7 Service Pack 1 的最低版本



## 後續步驟
若要檢查其他需求，請參閱 [Azure 資訊保護的需求](requirements-azure-rms.md)。

如需最常使用的應用程式如何支援 Azure RMS 的詳細資訊，請參閱[應用程式如何支援 Azure Rights Management Service](../understand-explore/applications-support.md)。

如需如何設定 Azure RMS 最常使用應用程式的詳細資訊，請參閱[設定 Azure Rights Management 的應用程式](../deploy-use/configure-applications.md)。


<!--HONumber=Oct16_HO1-->


