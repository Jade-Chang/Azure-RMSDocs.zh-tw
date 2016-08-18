---
title: "Office 應用程式和服務 | Azure RMS"
description: 
keywords: 
author: cabailey
manager: mbaldwin
ms.date: 06/30/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 388e67cd-c16f-4fa0-a7bb-ffe0def2be81
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 99eb67f6296ad1782c787aabb73a28458c02f367
ms.openlocfilehash: affb37cc3b991609f5de51370485b10fed932421


---


# Office 應用程式和服務

*適用於︰Azure Rights Management、Office 365*

使用者 Office 應用程式 (例如 Word、Excel、PowerPoint 及 Outlook) 和 Office 服務 (例如 Exchange 和 SharePoint) 可使用 Microsoft Azure Rights Management 來協助保護貴組織的資料。

## Office 應用程式：Word、Excel、PowerPoint 及 Outlook
這些應用程式原本就使用資訊版權管理 (IRM) 支援 Rights Management，並可讓使用者套用保護至儲存的文件或要傳送的電子郵件訊息。 使用者可以套用範本，或針對 Word、Excel 及 PowerPoint 選擇可充分自訂的存取、權限與使用限制設定。 

例如，使用者可以設定讓 Word 文件僅供貴組織中的人員存取，或是控制 Excel 試算表是否可供編輯、限制成唯讀或防止列印。 對於時間有限的檔案，可以設定一個讓檔案不能再被存取的到期時間 (由使用者直接設定或透過套用範本設定)。 除了選擇範本，Outlook 的使用者還可選擇 [不可轉寄] 選項來協助防止資料外洩。

## Exchange Online 和 Exchange Server
使用 Exchange Online 或 Exchange Server 時，您可以使用資訊版權管理 (IRM) 整合來提供其他資訊保護方案：

-   **Exchange ActiveSync IRM** ：可讓行動裝置保護和使用受保護的電子郵件訊息。

-   適用於 **Outlook Web App**的 RMS 支援：實作方式與 Outlook 用戶端類似，可讓使用者透過範本或指定個別選項來保護電子郵件訊息，而且使用者可以讀取和使用傳送給他們的受保護電子郵件訊息。

-   適用於 Outlook 用戶端的**保護規則** ：這是系統管理員所設定，可將 RMS 範本自動套用至指定之收件者的電子郵件訊息。 例如，當內部電子郵件被傳送至您的法務部門時，只有法務部門的成員可以讀取該郵件且無法轉寄。 使用者會在傳送電子郵件訊息之前看到訊息已套用保護，並且根據預設，如果使用者覺得沒有必要套用保護，便可將保護移除。 電子郵件會先經過加密再傳送。 如需詳細資訊，請參閱 Exchange 文件庫中的 [Outlook 保護規則](https://technet.microsoft.com/library/dd638178%28v=exchg.150%29.aspx)和[建立 Outlook 保護規則](https://technet.microsoft.com/library/dd638196%28v=exchg.150%29.aspx)。

-   **傳輸規則** ：這是系統管理員所設定，可根據寄件者、收件者、郵件主旨及內容之類的屬性，將 RMS 範本自動套用至電子郵件訊息。 這些規則在概念上與保護規則類似，但是無法讓使用者移除保護、可以套用至 Outlook Web Access 和行動裝置所傳送的電子郵件，並且從用戶端傳送電子郵件訊息之前不會予以加密。 如需詳細資訊，請參閱 Exchange 文件庫中的[建立傳輸保護規則](https://technet.microsoft.com/library/dd302432.aspx)。

-   **資料外洩防護 (DLP) 原則** ：包含幾組條件，可篩選電子郵件訊息並採取動作來協助防止機密或敏感性內容 (例如個人資訊或信用卡資訊) 的資料外洩。 偵測到敏感性資料時可以使用原則提示，以根據電子郵件訊息中的資訊來警示使用者可能需要套用資訊保護。 如需詳細資訊，請參閱 Exchange 文件庫中的[資料外洩防護](https://technet.microsoft.com/library/jj150527%28v=exchg.150%29.aspx)。

-   **Office 365 郵件加密** ：這會使用傳輸規則將加密的電子郵件傳送給貴公司外的人員，並且是在介面類似於 Outlook Web App 的瀏覽器中讀取電子郵件。 您可以在貴公司的加密電子郵件中自訂免責聲明文字和標頭文字，甚至是加入貴公司的標誌。 如需詳細資訊，請參閱 Office 網站上的 [Office 365 郵件加密](https://office.microsoft.com/o365-message-encryption-FX104179182.aspx)。

如果您使用的是 Exchange Server，則可透過部署 RMS 連接器將資訊保護功能與 [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)] 搭配使用，RMS 連接器會負責您內部部署伺服器與 RMS 雲端服務之間的轉送。 如需詳細資訊，請參閱[部署 Azure Rights Management 連接器](../deploy-use/deploy-rms-connector.md)。

## SharePoint Online 和 SharePoint Server
使用 SharePoint Online 或 SharePoint Server 時，您可以使用資訊版權管理 (IRM) 整合，讓系統管理員能夠保護清單或文件庫，以便在使用者簽出文件時保護檔案，而只有獲授權的人員可以根據您指定的資訊保護原則來檢視和使用該檔案。 例如，檔案可能為唯讀、停用文字複製功能、不允許儲存本機複本以及不允許列印檔案。

清單和文件庫的資訊保護一律是由系統管理員套用，絕對不會由使用者套用。 而且，它是套用在該容器中所有文件的清單或文件庫層級，而不是套用在個別檔案。  如果您使用 SharePoint Online，使用者也可以套用 IRM 至其 OneDrive for Business 文件庫。

您必須先為 SharePoint 啟用 IRM 服務。 然後，您可以指定程式庫的資訊版權管理。 在 SharePoint Online 和 OneDrive for Business，使用者也可以為其 OneDrive for Business 文件庫指定資訊版權管理。 雖然您可以選取最符合可在範本中所指定設定的 SharePoint 組態設定，但是 SharePoint 不會使用權限原則範本。

如果您使用的是 SharePoint Server，則可透過部署 RMS 連接器將資訊保護功能與 [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)] 搭配使用，RMS 連接器會負責您內部部署伺服器與 RMS 雲端服務之間的轉送。 如需詳細資訊，請參閱[部署 Azure Rights Management 連接器](../deploy-use/deploy-rms-connector.md)。

> [!NOTE]
> 目前，搭配使用 IRM 和 SharePoint 有一些限制：
> 
> -   您無法使用您在 Azure 傳統入口網站中管理的預設或自訂範本。
> -   受保護的 PDF 檔案不支援副檔名為 .PPDF 的檔案。 使用原生支援 RMS 的 PDF 閱讀程式時，支援副檔名為 .PDF 原本就受 RMS 保護的檔案。
> -   因為行動裝置上的 Office 尚未支援 RMS，這些裝置必須使用瀏覽器來檢視受 RMS 保護的檔案和唯讀檔案。

從 SharePoint 下載文件時，Azure RMS 就會對文件套用使用限制和資料加密，而不是在第一次於 SharePoint 建立文件或上載到文件庫時套用。 有關如何在下載前保護文件的資訊，請參閱 SharePoint 文件中的 [商務用 OneDrive 和 SharePoint Online 中的資料加密](https://technet.microsoft.com/library/dn905447.aspx) 。

如需搭配使用 Azure RMS 和 SharePoint的詳細資訊，請參閱下列 Office 部落格文章： [SharePoint 和 SharePoint Online 的資訊版權管理新功能](http://blogs.office.com/2012/11/09/whats-new-with-information-rights-management-in-sharepoint-and-sharepoint-online/)

## 後續步驟

若要查看其他應用程式和服務如何支援 Azure Rights Management，請參閱[應用程式如何支援 Azure Rights Management](applications-support.md)。


<!--HONumber=Jul16_HO1-->


