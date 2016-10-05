---
title: "協助使用者使用 Azure Rights Management Service 來保護檔案| Azure Information Protection"
description: "部署和設定 Azure Information Protection 的 Azure Rights Management Service 之後，協助您提供指引給使用者、系統管理員及技術支援中心的資訊。"
author: cabailey
manager: mbaldwin
ms.date: 09/25/2016
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 58f9a6ff-4121-4c8c-9865-1bb290604ad2
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 55fd22b60ad87dadce0ffb89bb658e949670f728
ms.openlocfilehash: 56bb2e90f9d1ecb7c925ab22cf1dba16246876f7


---

# 協助使用者使用 Azure Rights Management Service 來保護檔案

>*適用於︰Azure Information Protection、Office 365*

在為您的組織部署和設定 Azure Information Protection 之後，請提供說明和指引給使用者、系統管理員及技術支援中心：

-   **使用者資訊：**

    讓使用者知道如何和何時保護含有機密資訊的文件和電子郵件。 請盡可能將這項資訊提供給其現有的工作流程，讓他們可以將其他步驟納入已熟悉的程序中，而不是引進全新的程序。 務必讓他們了解您公司特有的優點 (和風險)，並提供指引來說明他們何時應該保護檔案和電子郵件。 如果您已設定[自訂範本](configure-custom-templates.md)，而範本名稱和描述不夠充分，無法讓他們做出正確的選擇，請提供指引來說明選取何者。

    > [!TIP]
    > 使用者的範例影片：
    >
    > -   [Azure RMS 使用者體驗](http://channel9.msdn.com/Series/Information-Protection/Azure-RMS-user-experience)
    > -   [Azure RMS 文件追蹤和撤銷](http://channel9.msdn.com/Series/Information-Protection/Azure-RMS-Document-Tracking-and-Revocation)

-   **系統管理員資訊：**

    部分應用程式會採用系統管理員所設定的原則和設定，而自動套用資訊保護。 對於這些應用程式，您可能需要提供指示給負責管理這些應用程式和服務的系統管理員。 如需詳細資訊，請參閱[應用程式如何支援 Azure Rights Management Service](../understand-explore/applications-support.md) 和[設定 Azure Rights Management Service 的應用程式](configure-applications.md)。

-   **服務台資訊：**

    服務台的其中一個最有用工具為 [RMS 分析器](https://www.microsoft.com/en-us/download/details.aspx?id=46437)。 服務台操作員可以搭配 Azure RMS 系統管理員選項執行它，而且他們可以要求使用者搭配 Azure RMS 使用者選項執行它。 這項工具不只可以協助識別問題，也可以修正其找到的問題，而且如果仍然無法修正，請記錄追蹤記錄。

    如果合法要求對受保護的文件具有完整存取權，例如法務部門或經理在員工離職之後所提出的要求，請確定技術支援中心具有使用 Azure Rights Management [進階使用者功能](configure-super-users.md)來要求此存取權的程序。

    此外，這些是使用者可能報告的一些典型問題：

    -   **登入說明：**

        當 Azure Rights Management Service 需要驗證使用者，但無法使用快取認證時，可能會提示使用者出示認證。 這是與您的 Office 365 租用戶或 Azure Active Directory 租用戶相關聯的使用者工作或學校帳戶和密碼。 這不是 Microsoft 帳戶 (先前稱為 Microsoft Live ID) 或其個人電子郵件帳戶，因為 Azure Rights Management Service 目前不支援這些帳戶。 提供指示給使用者和技術支援中心，說明當使用者以 Azure Rights Management Service 使用這些應用程式時，則提示使用者出示認證時應該使用什麼帳戶。

    -   **保護或取用內容的問題：**

        請確定使用者對其使用的應用程式具有適當的指示，而且正在使用 Azure Rights Management Service 支援的應用程式和裝置。 如需支援之應用程式和裝置的詳細資訊，請參閱 [Azure Rights Management 的需求](../get-started/requirements-azure-rms.md)。

        如果使用者在嘗試保護或取用內容時看到錯誤，請要求他們以 Azure RMS 使用者身分執行 [RMS 分析器](https://www.microsoft.com/en-us/download/details.aspx?id=46437) 。

        如果使用者報告他們可以開啟受保護的內容，但沒有他們需要的權限，請要求他們以 Azure RMS 使用者身分執行 [RMS 分析器](https://www.microsoft.com/en-us/download/details.aspx?id=46437) ，然後下載並檢視範本。 這將確認他們已成功下載範本，並具有範本提供的權限。 問題可能是使用者不是在針對範本設定的正確群組中，或需要重新設定適用於使用者的範本。

請使用下列各節來取得應用程式特定的資訊，以協助使用者保護機密文件和電子郵件。

## 透過 Rights Management 共用應用程式使用資訊保護
如果使用者使用 Office 2010，可能需要 Rights Management (RMS) 共用應用程式才能保護和取用受保護的內容，但也建議用於所有支援 Azure Rights Management Service 的電腦和行動裝置。

除了可讓使用者更輕鬆地保護重要的文件外，RMS 共用應用程式還可讓使用者追蹤他們所保護的文件，而且如有必要，可撤銷他們的存取權。

在 Windows 電腦上使用此應用程式的指示，請參閱 [Rights Management 共用應用程式使用者指南](../rms-client/sharing-app-user-guide.md)。

針對行動裝置，請參閱＜ [行動平台的 Microsoft Rights Management 共用應用程式常見問題集](http://technet.microsoft.com/dn451248)＞。

> [!TIP]
> 如需含有螢幕擷取畫面的概要範例案例，請參閱[使用者安全地與行動使用者共用附件](../understand-explore/what-admins-users-see.md#users-safely-share-attachments-with-mobile-users)。

## 對 Office 365、Office 2016 或 Office 2013 使用資訊保護
如果您使用 Azure Rights Management Service 且尚未安裝 Rights Management 共用應用程式，則使用者在功能區看不到 [共用保護] 按鈕，或在檔案總管中看不到 [就地保護]，這些都是可讓使用者輕鬆保護檔案的選項。 這些使用者必須依照如下的指示進行。

> [!TIP]
> 若要尋找對這些應用程式使用資訊保護的應用程式特定說明和指示，請搜尋 **IRM** 及應用程式名稱和版本。

#### 在 Word 2013 中保護文件

1.  在 Microsoft Word 內建立新文件。

2.  從 **[檔案]** 功能表按一下 **[資訊]**，按一下 **[保護文件]**，按一下 **[限制存取]**，然後選擇範本以快速套用適當的使用權限，或選取 **[限制存取]** ，然後自行選取使用權限。

    > [!NOTE]
    > 如果是第一次使用 Rights Management，您將會連絡[!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)]服務，且會提示您出示認證來設定 Office IRM 用戶端。

3.  儲存文件。

當其他人開啟此文件時，首先會驗證他們的身分。 如果他們未獲授權來開啟此文件，則文件不會開啟。 如果他們獲授權開啟此文件，則會以對該使用者指定的限制使用權限來開啟文件。 例如，「僅限檢視」使用權限不允許使用者編輯或儲存文件，即使先複製到其他位置也一樣。 文件頂端會以限制橫幅顯示使用權限。 此橫幅可能顯示套用至文件的權限，也可能提供連結來顯示權限。

#### 使用 Outlook 2013 和 Exchange Online 保護電子郵件訊息

1.  在 Outlook 內，建立新的電子郵件訊息，以寄給組織內的收件者。

2.  從 **[選項]** 索引標籤上按一下 **[權限]**，然後選取一個選項。 例如：**[不可轉寄]**、**[&lt;公司名稱&gt; - 機密]** 或 **[&lt;公司名稱&gt; - 僅限機密檢視]**。

3.  傳送訊息。

與檢視受保護的文件類似，當收件者收到電子郵件訊息，首先會驗證他們的身分。 如果他們獲授權開啟此電子郵件訊息，則會以對該使用者指定的限制使用權限來開啟訊息。 例如，若您選取 **[不可轉寄]**，則功能區的 [轉寄] 按鈕無法使用。

#### 使用 Outlook Web App 保護電子郵件訊息

1.  在 Outlook Web App 內，建立新的電子郵件訊息，以寄給組織內的收件者。

2.  按一下  **…**、按一下 **[設定權限]**，然後選取選項。 例如：**[不可轉寄]**、**[不可全部回覆]**、**[&lt;公司名稱&gt; - 機密]** 或 **[&lt;公司名稱&gt; - 僅限機密檢視]**。

3.  傳送訊息。

與檢視受保護的文件類似，當收件者收到電子郵件訊息，首先會驗證他們的身分。 如果他們獲授權開啟此電子郵件訊息，則會以對該使用者指定的限制使用權限來開啟訊息。 例如，若您選取 **[不可全部回覆]**，則訊息視窗中的 **[全部回覆]** 選項無法使用。





<!--HONumber=Sep16_HO4-->


