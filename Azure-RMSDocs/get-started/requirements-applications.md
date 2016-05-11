---
# required metadata

title: Azure RMS 需求：應用程式 | Azure RMS
description:
keywords:
author: cabailey
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 7b33bcb8-63da-46be-ad56-b06de97822fa

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: esaggese
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---


# Azure RMS 需求︰應用程式

請使用下列表格來識別原生支援 Azure RMS 的應用程式，這意味 RMS 使用 RMS API 來支援使用限制，藉此嚴密整合至這些應用程式中。 這些應用程式也稱為 RMS 創新。

除非另外註明，否則支援的功能適用於 Azure RMS 與 AD RMS 兩者。 此外，在 iOS、Android、OS X 和 Windows Phone 8.1 上的 AD RMS 支援需要 [Active Directory 權限管理服務行動裝置延伸模組](https://technet.microsoft.com/library/dn673574.aspx)。

表格欄位的相關資訊：

-   受保護的 PDF：這些檔案具有 .ppdf 副檔名，而且會在您使用 RMS 共用應用程式來透過電子郵件共用 Office 檔案和 PDF 檔案時自動建立。 RMS 共用應用程式含有用來讀取受保護的 PDF 檔案的閱讀程式。 如果您之前使用 Azure RMS 或 AD RMS 建立保護的 PDF 檔案，您可以繼續在 Windows、iOS 和 Android 裝置上，使用 Foxit Reader 和 Nitro Pro 讀取這些檔案。

-   電子郵件：列出的電子郵件用戶端可以保護電子郵件訊息本身，這樣會自動保護任何附加檔案。 在此情況下，用戶端的預覽功能可讓授權的收件者看見受保護的內容 (訊息和附件)。 不過，若電子郵件訊息本身未受保護，但附件受到保護，則用戶端預覽功能無法讓授權的收件者看見受保護的附件。

-   其他檔案類型：文字和影像檔包含副檔名為 .txt、.xml、.jpg 和 .jpeg 的檔案。 這些檔案在受到 RMS 原生保護後會變更其副檔名並成為唯讀狀態。 無法受到原生保護的檔案在 RMS 對其進行一般保護後，會有 .pfile 副檔名。 如需詳細資訊，請參閱[Rights Management 共用應用程式系統管理員指南](../rms-client/sharing-app-admin-guide.md)。


|**裝置作業系統**|Word、Excel、PowerPoint|受保護的 PDF|電子郵件|其他檔案類型|
|-------------------------------|---------------------------|-----------------|---------|--------------------|
|**Windows**|Office 2010<br /><br />Office 2013<br /><br />Office Mobile 應用程式 (僅適用於 Azure RMS) [[1]](#footnote-1)<br /><br />Office Online [[2]](#footnote-2)|Gaaiho Doc<br /><br />GigaTrust Desktop PDF Client for Adobe<br /><br />Foxit Reader<br /><br />Nitro PDF 閱讀程式<br /><br />RMS 共用應用程式|Outlook 2010<br /><br />Outlook 2013<br /><br />Outlook Web App (OWA) [[3]](#footnote-3)<br /><br />Windows Mail [[4]](#footnote-4)|適用於 Windows 的 RMS 共用應用程式：文字、影像、pfile<br /><br />Siemens JT2Go：JT 檔案 (僅限 Windows 10)|
|**iOS**|Office for iPad and iPhone [[5]](#footnote-5)<br /><br />Office Online [[2]](#footnote-2)<br /><br />TITUS 文件|Foxit Reader<br /><br />RMS 共用應用程式 [[1]](#footnote-1)<br /><br />TITUS 文件|Citrix WorxMail<br /><br />NitroDesk [[4]](#footnote-4)<br /><br />Outlook for iPad and iPhone [[4]](#footnote-4)<br /><br />OWA for iOS [[3]](#footnote-3)<br /><br />TITUS Mail|RMS 共用應用程式 [[1]](#footnote-1)︰文字、影像、pfile<br /><br />TITUS 文件︰Pfile|
|**Android**|GigaTrust App for Android<br /><br />Office Online [[2]](#footnote-2)|GigaTrust App for Android<br /><br />Foxit Reader<br /><br />RMS 共用應用程式 [[1]](#footnote-1)|9Folders [[4]](#footnote-4)<br /><br />GigaTrust App for Android [[4]](#footnote-4)<br /><br />Citrix WorxMail<br /><br />NitroDesk [[4]](#footnote-4)<br /><br />OWA for Android [[3]](#footnote-3) 和 [[6]](#footnote-6)<br /><br />Samsung Email (S3 和更新版本) [[6]](#footnote-6)<br /><br />TITUS Classification for Mobile|RMS 共用應用程式 [[1]](#footnote-1)︰文字、影像、pfile|
|**OS X**|Office 2011 (僅適用於 AD RMS)<br /><br />Office 2016 for Mac<br /><br />Office Online [[2]](#footnote-2)|Foxit Reader<br /><br />RMS 共用應用程式 [[1]](#footnote-1)|Outlook 2011 (僅適用於 AD RMS)<br /><br />Outlook 2016 for Mac<br /><br />Outlook for Mac|RMS 共用應用程式 [[1]](#footnote-1)︰文字、影像、pfile|
|**Windows 10 Mobile**|Office Mobile 應用程式(僅適用於 Azure RMS) [[1]](#footnote-1)|不支援|Citrix WorxMail<br /><br />Outlook Mail|不支援|
|**Windows RT**|Office 2013 RT<br /><br />Office Online [[2]](#footnote-2)|不支援|Outlook 2013 RT<br /><br />Windows 郵件應用程式<br /><br />Windows Mail [[4]](#footnote-4)|Siemens JT2Go：JT 檔案|
|**Windows Phone 8.1**|Office Mobile (僅適用於 AD RMS)|RMS 共用應用程式 [[1]](#footnote-1)|Outlook Mobile [[4]](#footnote-4)|RMS 共用應用程式 [[1]](#footnote-1)︰文字、影像、pfile|
|**Blackberry 10**|不支援|不支援|Blackberry 電子郵件 [[4]](#footnote-4)|不支援|


###### 註腳 1
支援檢視受保護的內容。

###### 註腳 2 
支援檢視 SharePoint Online、商務用 OneDrive 和 Outlook Web Access 中受保護的內容。

###### 註腳 3
如果收件者的信箱在內部部署的 Exchange 中，並收到受保護的電子郵件，則只可以在豐富的電子郵件用戶端 (如 Outlook) 中開啟此內容。  不能從 Outlook Web Access 開啟此內容。

###### 註腳 4
使用 Exchange ActiveSync IRM，必須由 Exchange 系統管理員啟用。 使用者可以檢視、回覆和全部回覆受保護的電子郵件訊息，但使用者本身無法保護新的電子郵件訊息。

如果收件者的信箱在內部部署的 Exchange 中，並收到來自其他使用 Exchange 的組織的受保護電子郵件，則只可以在豐富的電子郵件用戶端 (如 Outlook) 中開啟此內容。  不能從使用 Exchange Active Sync IRM 的裝置開啟此內容。

###### 註腳 5
支援檢視和編輯受保護的文件。 如需詳細資訊，請參閱下列 Office 部落格文章︰[Azure Rights Management 支援已適用 Office for iPad and iPhone](https://blogs.office.com/2015/07/22/azure-rights-management-support-comes-to-office-for-ipad-and-iphone-2/)

###### 註腳 6
如需詳細資訊，請參閱下列 Office 部落格文章︰[OWA for Android 目前可在選取的裝置上使用](http://blogs.office.com/2014/06/11/owa-for-android-now-available-on-select-devices/)

## Office 的 Azure RMS 支援的詳細資訊

所有版本的 Office (不包括 Office 2007) 都支援取用受保護的內容。

Azure RMS 與 Office Professional Plus 2010 或 Office Professional 2010：

- 需要適用於 Windows 的 Rights Management 共用應用程式

- 不支援 Windows 10


## Rights Management 共用應用程式的詳細資訊

如需有關適用於 Windows 之 Rights Management 共用應用程式的詳細資訊，請參閱下列資源：

-   [Rights Management 共用應用程式系統管理員指南 (英文)](../rms-client/sharing-app-admin-guide.md)

-   [Rights Management 共用應用程式使用者指南 (英文)](../rms-client/sharing-app-user-guide.md)

如需有關行動平台之 Rights Management 共用應用程式的詳細資訊，請參閱下列資源：

-   使用 [Microsoft Rights Management 頁面](http://go.microsoft.com/fwlink/?LinkId=303970)上的連結，下載相關的應用程式

-   如果您有 Microsoft Intune，您可以使用原則管理的應用程式部署和管理應用程式︰ 

    -   如需了解 Intune 所註冊的 iOS 和 Android 裝置，請參閱[在 Microsoft Intune 主控台中設定及部署行動應用程式管理原則](/intune/deploy-use/configure-and-deploy-mobile-application-management-policies-in-the-microsoft-intune-console)

    -   如需了解非 Intune 所註冊的 Android 裝置，請參閱[使用 Microsoft Intune 建立及部署行動應用程式管理原則](/intune/deploy-use/create-and-deploy-mobile-app-management-policies-with-microsoft-intune)

-   [行動平台的 Microsoft Rights Management 共用應用程式常見問題集](https://technet.microsoft.com/dn451248)



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
若要檢查其他需求，請參閱 [Azure Rights Management 的需求](requirements-azure-rms.md)。

如需最常使用的應用程式如何支援 Azure RMS 的詳細資訊，請參閱[應用程式如何支援 Azure Rights Management](../understand-explore/applications-support.md)。

如需如何設定 Azure RMS 最常使用應用程式的詳細資訊，請參閱[設定 Azure Rights Management 的應用程式](../deploy-use/configure-applications.md)。

<!--HONumber=Apr16_HO4-->


