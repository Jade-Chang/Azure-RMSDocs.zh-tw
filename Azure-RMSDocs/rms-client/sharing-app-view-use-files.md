---
title: "檢視並使用 Rights Management 保護的檔案 | Azure RMS"
description: 
keywords: 
author: cabailey
manager: mbaldwin
ms.date: 05/09/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: e5fa4666-6906-405a-9e0c-2c52d4cd27c8
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: c611fa8a846612fed238e59e5077be67f6f9531a
ms.openlocfilehash: c243ad02bdbd5bd46ba1b2a4818839df8a7deb7b


---

# 檢視並使用 Rights Management 保護的檔案

*適用於︰Active Directory Rights Management Services、Azure Rights Management、Windows 10、Windows 7 SP1、Windows 8、Windows 8.1*

當[您的電腦上安裝 Rights Management (RMS) 共用應用程式](install-sharing-app.md)之後，您只要按兩下受保護的檔案即可檢視它。 檔案可能是電子郵件郵件的附件，您也可能在使用 [檔案總管] 時看見它。

> [!NOTE]
> RMS 必須先確認您有權檢視受保護的檔案 (檢查您的使用者名稱和密碼)，您才可以檢視檔案。 在某些情況下，這可能已快取，所以不會提示您提供認證。 在其他情況下會提示您提供認證。
>
> 如果您的組織不使用 Azure Rights Management (Azure RMS) 或 AD RMS，您可以申請免費帳戶，在接受您的認證後，您就可以開啟使用 RMS 保護的檔案：
>
> -   若要申請此帳戶，請按一下連結來申請 [個人版 RMS](http://go.microsoft.com/fwlink/?LinkId=309469)。
>
>     當您註冊時，使用您的公司電子郵件地址而不是個人的電子郵件地址。 如果您是因為在電子郵件中收到受保護的附加檔案而註冊，請使用電子郵件訊息寄給您時所使用的相同電子郵件地址。
> -   如需詳細資訊，請參閱[個人版 RMS 和 Azure Rights Management](../understand-explore/rms-for-individuals.md)。

## 檢視受保護的檔案
使用檔案總管或含有附件的電子郵件訊息，按兩下受保護的檔案，然後輸入您的認證 (如果提示您這樣做)。

如果您看到檔案有兩個版本，但副檔名不同，只有當無法開啟其中一個檔案時，才開啟副檔名為 .ppdf 的另一個檔案。 如果您也無法開啟 .ppdf 版本，請先安裝 [RMS 共用應用程式](install-sharing-app.md)，它知道如何開啟 .ppdf 副檔名的檔案。

> [!NOTE]
> 如需詳細資訊，請參閱[自動建立的 .ppdf 檔案是什麼？](sharing-app-dialog-box.md#what-s-the-ppdf-file-that-s-automatically-created-)

如何開啟檔案取決於它受保護的方式，從副檔名就可以判斷。 在各種情況下，開啟檔案時可能經過稽核，而且只要檔案受到保護，就會持續稽核。 此外，如果檔案是以電子郵件附件的形式傳送，則您每次開啟檔案時，寄件者就可能收到電子郵件通知。

- **此檔案副檔名為 *.pfile*。

    檔案受到一般保護。

    當您開啟檔案時，您會看到共用應用程式的 [受保護的檔案] 對話方塊，告知您檔案是由誰保護檔案，並提醒您遵守共同擁有者權限。 按一下 [開啟]  讀取檔案。

    ![使用 RMS 共用應用程式時，透過電子郵件共用的 pfile 對話方塊](../media/ADRMS_MSRMSApp_PfilePermission.png)

- **檔案的副檔名為 *.ppdf*，也可能是受保護的文字或影像檔 (例如 *.ptxt* 或 * .pjpg*)**

    檔案已受到原生保護成為唯讀複本。

    檔案是使用隨著 RMS 共用應用程式一起安裝的檢視器來開啟。 這個檔案是唯讀，即使儲存到別處或重新命名也一樣。

- **其他副檔名**

    檔案已受到原生保護。

    檔案是使用原始副檔名相關聯的應用程式來開啟，而且檔案頂端會顯示限制橫幅。 此橫幅可能顯示套用至檔案的權限，也可能提供連結來顯示權限。 例如，您可能會看到下列訊息，您必須按一下 **目前權限限制** ，查看套用到該檔案的實際權限，以及可存取它的人員：

    ![檔案受保護時的限制存取橫幅](../media/ADRMS_MSRMSApp_RestrictedAccess.png)



如需Rights Management 支援的副檔名清單，請參閱《[Rights Management 共用應用程式系統管理員指南](sharing-app-admin-guide.md)》的[支援的檔案類型和副檔名](sharing-app-admin-guide-technical.md#supported-file-types-and-file-name-extensions)一節。 如果未列出您的副檔名，請使用 Web 搜索以查看它是否為其他應用程式支援的副檔名。

> [!NOTE]
> 如果在確認檔案受 Rights Management 保護且未開啟之後，請下載並使用 [RMS Analyzer 工具](https://www.microsoft.com/en-us/download/details.aspx?id=46437)。 按照工具中的指示，檢查電腦上可能會使受保護的檔案無法開啟的問題。

## 使用已受保護的檔案 (例如編輯和列印檔案)
如果在開啟受保護的檔案之後，您不只想要讀取該檔案而已 (例如，編輯、複製和列印)，請依副檔名遵循相關指示：

- **此檔案副檔名為 *.pfile*。

    儲存已開啟的檔案，並提供新的副檔名 (與您想要使用的應用程式相關聯)。

    比方說，如果檔案是以檔案名稱 document.vsdx.pfile 而受保護，請檔案總管中檢視檔案，並將檔案儲存為 document.vsdx。

    新的檔案不再受到保護。 如果您想要保護檔案，則必須手動進行。 如需指示，請參閱[使用 Rights Management 共用應用程式保護裝置上的檔案 (就地保護)](sharing-app-protect-in-place.md)。

- **檔案的副檔名為 *.ppdf*，也可能是受保護的文字或影像檔 (例如 *.ptxt* 或 * .pjpg*)**

    您只能檢視檔案，如果您重新命名或移動它，檔案仍然是受到保護。

- **其他副檔名**

    您的裝置上必須有了解 Rights Management 的應用程式，才能使用這些檔案。 這些應用程式稱為啟用 RMS 的應用程式。 舉例來說，Office 2016、Office 2013 和 Office 2010 提供的應用程式 (例如 Word、Excel、PowerPoint 及 Outlook) 就是啟用 Rights Management 的應用程式。 但不是來自 Microsoft 的應用程式，例如其他軟體公司和自己的企業營運應用程式，也可能已啟用 Rights Management。

    已啟用 Rights Management 的應用程式知道如何開啟已受其他 Rights Management 應用程式所保護的檔案。 它們也會保留已套用的保護，即使您編輯檔案或儲存為其他檔名或另存別處也一樣。 這些應用程式可讓您根據目前套用至檔案的權限來使用檔案，因此只要您有權限使用檔案，您就可以這樣做。 例如，您可能可以編輯檔案但不能列印。


## 範例和其他指示
如需 Rights Management 共用應用程式的使用範例及作法指示，請參閱 Rights Management 共用應用程式使用者指南中下列各節：

-   [使用 RMS 共用應用程式的範例](sharing-app-user-guide.md#examples-for-using-the-rms-sharing-application)

-   [您想要做什麼事？](sharing-app-user-guide.md#what-do-you-want-to-do-)

## 另請參閱
[Rights Management 共用應用程式使用者指南 (英文)](sharing-app-user-guide.md)



<!--HONumber=Jun16_HO4-->


