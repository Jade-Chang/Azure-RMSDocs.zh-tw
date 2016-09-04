---
title: "系統管理員和使用者看到的內容？ | Azure RMS"
description: "本文顯示系統管理員和使用者所見內容，以及使用 Azure Rights Management (Azure RMS) 保護敏感或機密資訊的一些常見例子。"
author: cabailey
manager: mbaldwin
ms.date: 06/28/2016
ms.topic: article
ms.prod: 
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 013e0eb4-49a7-4e81-9e4d-f56c0ceb017f
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 26b043f1f9e7a1e0cd00c2f31c28f7d6685f0232
ms.openlocfilehash: 4a2f473c657b7fe27e2a6d42000fd540c49e8895


---


# Azure RMS 運作方式：系統管理員和使用者看到的內容

>*適用於︰Azure Rights Management、Office 365*

本文顯示系統管理員和使用者所見內容，以及使用 Azure Rights Management (Azure RMS) 保護敏感或機密資訊的一些常見例子。

> [!NOTE]
> 在 Azure RMS 保護資料的所有這些例子中，內容擁有者持續擁有資料 (檔案或電子郵件) 的完整存取權，即使套用的保護授與權限給擁有者未隸屬的群組，或套用的保護包含到期日也一樣。
>
> 同樣地，利用 Rights Management 的進階使用者功能，將委派存取權授與您指定的獲授權使用者或服務，IT 即可毫無限制地存取受保護的資料。 此外，IT 可以追蹤和監視受保護資料的使用情況 - 例如，誰在存取資料和何時存取。

如需其他螢幕擷取畫面和實作示範 RMS 的影片，請參閱 [Enterprise Mobility and Security Blog](https://blogs.technet.microsoft.com/enterprisemobility/?product=azure-rights-management-services) (Enterprise Mobility and Security 部落格)。

## 啟用及設定 Rights Management
雖然您可以使用 Windows PowerShell 來啟用及設定 Azure RMS，但從管理入口網站來做最簡單。 啟用此服務之後，隨即就有兩個預設範本供系統管理員和使用者選擇，可快速又輕鬆地將資訊保護套用至檔案。 但是，您也可以建立自己的自訂範本以進行其他選項和設定。

![系統管理員在步驟 1 中看到的內容](../media/AzRMS_StoryboardActivate_small1.png)


**系統管理員在步驟 1 看到的內容：**您可以使用 Office 365 系統管理中心 (第一張圖片) 或 Azure 傳統入口網站 (第二張圖片) 來啟用 RMS。<br /><br />只要按一下來啟用，再按一下來確認，組織中的系統管理員和使用者即可受到資訊保護。

---

![系統管理員在步驟 2 中看到的內容](../media/AzRMS_TemplatesPortal_small.png)

**系統管理員在步驟 2 看到的內容：**啟用之後，自動就有兩個權限原則範本可供組織使用。 其中一個範本用於唯讀存取權 (名稱中包含 [僅限機密檢視])，另一個用於讀取和修改存取權 ([機密])。

將這些範本套用至檔案或電子郵件，就可限制只有組織中的使用者才能存取。 這是防止公司資料洩漏給組織外部人士最快速又輕鬆的方法。

> [!TIP]
> 這些預設範本的開頭都會自動加上您的組織名稱，很容易識別。 在我們的範例中是 **VanArsdel, Ltd**。

如果不想讓使用者看到這些範本，或者您想要建立您自己的範本，您可以從 Azure 傳統入口網站執行這項作業。 依下圖所示，精靈會引導您完成自訂範本建立程序。

---

![系統管理員在步驟 3 中看到的內容](../media/AzRMS_TemplatesSettings3.png)

**系統管理員在步驟 3 看到的內容：**如果您決定要建立自己的範本，可用的一些組態設定包括離線存取、到期日設定，以及是否要立即發佈範本 (讓它顯示在支援 Rights Management 的應用程式中)。

---

![系統管理員在步驟 4 中看到的內容](../media/AzRMS_TemplatesPortal_ExplorerWord3.png)

**使用者在步驟 4 看到的內容：**由於發佈這些範本，使用者現在可以在檔案總管和 Microsoft Word 等應用程式中選取它們：

- 使用者可以選擇預設範本 **VanArsdel, Ltd – 機密**。 然後，只有 VanArsdel 組織的員工才能開啟和使用這份文件，即使後來以電子郵件傳送給組織外部的人或儲存到公用位置也一樣。

- 使用者可以選擇系統管理員建立的自訂範本 [銷售和行銷 - 僅限讀取和列印]。 然後，不只是組織外部的人無法存取檔案，更限制只有銷售和行銷部門的員工才能存取此檔案。 此外，這些員工沒有此文件的完整權限，只能讀取和列印。 例如，他們不能修改或複製此文件。

---

**如需此案例的詳細資訊：**

- 如需逐步指示，請參閱[啟用 Azure Rights Management](../deploy-use/activate-service.md) 和[設定 Azure Rights Management 的自訂範本](../deploy-use/configure-custom-templates.md)。

- 若要協助使用者保護重要的公司檔案，請參閱[協助使用者使用 Azure Rights Management 來保護檔案](../deploy-use/help-users.md)。

接下來，請參閱系統管理員如何套用範本來自動為檔案和電子郵件設定資訊保護的一些範例。

## 在執行 Windows Server 和檔案分類基礎結構的檔案伺服器上自動保護檔案

此範例示範如何使用 Azure RMS，在至少執行 Windows Server 2012 且設定為使用檔案分類基礎結構的檔案伺服器上，自動保護檔案。

有許多方法可將分類值套用至檔案。 例如，您可以檢查檔案的內容，再據以套用內建的分類，例如「機密性」和「個人識別資訊」。 不過，在此範例中，系統管理員建立 [行銷]  這個自訂分類，將自動套用到 [促銷]  資料夾中儲存的所有使用者文件。 雖然此資料夾受到 NTFS 權限的保護，限制只有 [行銷] 群組的成員才能存取，但系統管理員知道，如果該群組中的某人移動或以電子郵件傳送檔案，可能會丟失這些權限。 然後，未經授權的使用者就可能存取檔案中的資訊。

![系統管理員在步驟 1 中看到的內容](../media/AzRMS_FCI_ConnectorSmall.png)

**系統管理員在步驟 1 看到的內容：**系統管理員安裝並設定 Rights Management (RMS) 連接器，做為內部部署伺服器與 Azure RMS 之間的轉送站。

---

![系統管理員在步驟 2 中看到的內容](../media/AzRMS_ExampleFCI_ConfigurationSmall.png)

**系統管理員在步驟 2 看到的內容：**在檔案伺服器上，系統管理員設定分類規則和工作，以自動將 [促銷] 資料夾中的所有使用者檔案分類為 [行銷]，並以 RMS 加密來保護。

她選取我們在第一個範例中建立的自訂 RMS 範本，限制只有銷售和行銷部門的成員才能存取： **銷售和行銷 - 僅限讀取和列印**。

因此，該資料夾中的所有文件都自動設定為 [行銷] 分類，並以 [銷售和行銷] RMS 範本來保護。

---

![系統管理員在步驟 3 中看到的內容](../media/AzRMS_FCI_EmailSmall.png)

**使用者在步驟 3 看到的內容：**RMS 如何協助防止資料洩漏給不應該存取敏感或機密資訊的人：

- [行銷] 群組中的 Janet 從 [促銷] 資料夾中以電子郵件傳送一份機密報表。 此報表包含新的產品功能和廣告計劃，正在出差的同事要求取得一份。 不過，Janet 誤將此報表寄給別人，她沒發現到已經不小心選取另一家公司中名稱類似的收件者。<br><br>
該收件者無法讀取此機密報表，因為他不是 [銷售和行銷] 群組的成員。

---

**如需此案例的詳細資訊：**

- 如需逐步指示，請參閱[部署 Azure Rights Management 連接器](../deploy-use/deploy-rms-connector.md)。

## 使用 Exchange Online 和資料外洩防護原則來自動保護電子郵件

前一個範例示範如何自動保護包含敏感或機密資訊的檔案，但如果資訊不是在檔案中，而是在電子郵件訊息中，該怎麼辦？ Exchange Online 資料外洩防護 (DLP) 原則在此派上用場，可提示使用者套用資訊保護 (利用原則提示) 或自動套用 (利用傳輸規則)。

在此範例中，系統管理員設定原則來協助組織遵守美國的個人識別資訊資料保護規定，但也可以針對其他法規來設定規則，或根據您定義的自訂規則。

![系統管理員在步驟 1 中看到的內容](../media/AzRMS_DLPExample1.png)

**系統管理員在步驟 1 看到的內容：**在 Exchange 系統管理中心，系統管理員用名為**美國個人識別資訊 (PII) 資料**的 Exchange 範本來建立及設定新的 DLP 原則。 此範本會在電子郵件訊息中尋找社會安全號碼和駕駛執照號碼等資訊。

對於包含這項資訊和傳送到組織外部的電子郵件訊息，設定的規則會利用 RMS 範本來自動套用權限保護，以限制只有公司員工才能存取。

在這裡，規則設定為使用我們第一個範例的其中一個預設範本：[VanArsdel, Ltd – 機密] 。 此外，您也可以看到可供選擇的範本中包含您已建立的任何自訂範本，以及 Exchange 專用的 [禁止轉寄]  選項。

> [!NOTE]
> 如果您看到的設定選項與圖片有些許差異，在您設定規則時，可能需要先選取 **[其他選項]**。 然後您可以依序選取 **[修改郵件安全性]** > 、**[套用權限保護]**，然後選取 RMS 範本。

---

![系統管理員在步驟 2 中看到的內容](../media/AzRMS_DLPUnprotectedEmail_small.png)

**使用者在步驟 2 看到的內容：**人事經理撰寫一封電子郵件，內容中含有一位新進員工的社會安全號碼號碼。 他將此電子郵件訊息傳送給人力資源部門的 Sherrie。

---

![系統管理員在步驟 3 中看到的內容](../media/AzRMS_DLPProtectedEmail_small.png)

**使用者在步驟 3 看到的內容：**如果此電子郵件訊息傳送或轉寄到組織外部的某人，DLP 規則會自動套用權限保護。

電子郵件在離開組織基礎結構時會經過加密，因此，不論是在傳輸中或收件者的收件匣中，都無法讀取電子郵件訊息中的社會安全號碼號碼。 除非收件者是 VanArsdel 員工，否則無法讀取訊息。

---

**如需此案例的詳細資訊：**

-   如需 Azure RMS 與 Exchange Online 如何搭配運作的詳細資訊，請參閱[應用程式如何支援 Azure Rights Management](applications-support.md) 中的 [Exchange Online 和 Exchange Server](office-apps-services-support.md#exchange-online-and-exchange-server) 一節。

-   如需 Exchange Online for Azure RMS 的設定逐步指示，請參閱[設定 Azure Rights Management 的應用程式](../deploy-use/configure-applications.md)中的 [Exchange Online：IRM 設定](../deploy-use/configure-office365.md#exchange-online-irm-configuration)。

## 使用 SharePoint Online 和受保護的文件庫自動保護檔案

本節示範如何使用 SharePoint Online 和受保護的文件庫來輕鬆保護文件。

在此範例中，Contoso 的 SharePoint 系統管理員已經為每個部門建立文件庫，用以集中儲存和取出文件來編輯和進行版本控制。 例如，銷售、行銷、人力資源等部門各有一個文件庫。 當新文件上傳或建立於其中一個受保護的文件庫時，該文件會獲得文件庫的保護 (不需要選取權限原則範本)，而且該文件會自動且持續受到保護，即使移到 SharePoint 文件庫之外也一樣。

![系統管理員在步驟 1 中看到的內容](../media/AzRMS_StoryboardSPO_small1.png)

**系統管理員在步驟 1 看到的內容：**系統管理員對 SharePoint 網站啟用資訊版權管理。

---

![系統管理員在步驟 2 中看到的內容](../media/AzRMS_StoryboardSPO_small2.png)

**系統管理員在步驟 2 看到的內容：**然後，她對一個文件庫啟用 Rights Management。 雖然還有其他選項，但這個簡單的設定通常就足夠。

從此文件庫下載文件後，文件便自動受到 Rights Management 的保護，並繼承針對文件庫所設定的保護。

---

![系統管理員在步驟 3 中看到的內容](../media/AzRMS_StoryboardSPO_small3.png)

**使用者在步驟 3 看到的內容：**當銷售部門的人從文件庫取出此銷售報表時，他們會在頂端的資訊橫幅清楚看到這是受保護的文件且限制存取。

就算使用者將文件重新命名、儲存到其他位置或透過電子郵件分享，文件仍受到保護。 不論檔案如何命名、儲存在何處，或是否透過電子郵件分享，只有銷售部門的成員才能讀取。

---

**如需此案例的詳細資訊：**

-   如需 Azure RMS 與 SharePoint 如何搭配運作的詳細資訊，請參閱[應用程式如何支援 Azure Rights Management](applications-support.md) 中的 [SharePoint Online 和 SharePoint Server](office-apps-services-support.md#sharepoint-online-and-sharepoint-server) 一節。

-   如需 SharePoint for Azure RMS 的設定逐步指示，請參閱[設定 Azure Rights Management 的應用程式](../deploy-use/configure-applications.md)中的 [SharePoint Online 和 OneDrive for Business：IRM 設定](../deploy-use/configure-office365.md#sharepoint-online-and-onedrive-for-business-irm-configuration)。

## 使用者安全地與行動使用者共用附件

前述範例示範系統管理員如何將資訊保護自動套用至敏感和機密資料。 但在某些情況下，使用者可能需要自行套用此保護。 例如，他們與其他組織中的夥伴共同作業、需要範本中未定義的自訂權限或設定，或面對先前範例未涵蓋的特殊情況。 在這些情況下，使用者可以自行套用 RMS 範本或設定自訂權限。

此範例示範使用者如何輕鬆地與其他公司中共同合作的人共用文件，但是仍然能夠保護文件，並深信收件者能夠讀取文件，即使是從熱門的行動裝置也一樣。 此案例使用 Rights Management 共用應用程式，而該應用程式可自動部署至組織中的 Windows 電腦。 或者，也可以由使用者自行安裝。

在此範例中，Contoso 的 Alice 以電子郵件將機密的 Word 文件傳送給 Fabrikam 的 Bob。 他在 iPad 上閱讀此文件，但他可以在 iPhone、Android 平板電腦或手機、Mac 電腦或 Windows 手機或電腦上輕鬆地閱讀此文件。

![使用者在步驟 1 中看到的內容](../media/AzRMS_StoryboardEmail_small1.png)

**使用者在步驟 1 看到的內容：**Alice 在她的 Windows PC 上建立標準的電子郵件訊息，並附加文件。

她按一下功能區的 [共用保護]  ，這樣會從 RMS 共用應用程式載入 [共用保護]  對話方塊。

Alice 想要限制 Bob 只能檢視和編輯此文件，而不希望他複製或列印此文件，因此她選取 [檢閱者 - 檢視及編輯] 。 她也想要在當有人嘗試開啟文件時收到電子郵件，並且能夠視需要稍後撤銷文件，以及知道撤銷會立即生效。

---

![使用者在步驟 2 中看到的內容](../media/AzRMS_StoryboardEmail_small2.png)

**使用者在步驟 2 看到的內容：**Bob 在他的 iPad 上看到電子郵件。

除了 Alice 的訊息和附件，還有可讓他在 iPad 上註冊和安裝 RMS 共用應用程式的指示。

---

![使用者在步驟 3 中看到的內容](../media/AzRMS_StoryboardEmail_small3.png)

**使用者在步驟 3 看到的內容：**Bob 現在可以開啟附件。 首先會要求他登入，以確認他是預定的收件者。

當 Bob 檢視文件時，他也看到限制存取的資訊，告訴他可以檢視和編輯文件，但不能複製或列印。

---

![使用者在步驟 4 中看到的內容](../media/AzRMS_StoryboardEmail_small4.png)

**使用者在步驟 4 看到的內容：**Alice 收到電子郵件訊息，得知 Bob 已成功開啟她所傳送的文件及他何時存取文件。

如果 Bob 將他的電子郵件連同附件轉寄出去，或儲存到其他人可存取的位置，或在網路上遭到攔截，則其他人也無法讀取文件。

---

**如需此案例的詳細資訊：**

- 如需逐步指示，請參閱《[Rights Management 共用應用程式使用者指南](../rms-client/sharing-app-user-guide.md)》中的[保護您以電子郵件共用的檔案](../rms-client/sharing-app-protect-by-email.md)和[檢視及使用已保護的檔案](../rms-client/sharing-app-view-use-files.md)。

- [Azure Rights Management 快速入門教學課程](../get-started/quick-start-tutorial.md)包含此案例的逐步指示。

## 後續步驟

現在您已看過 Azure RMS 用途的一些範例，您可能想要了解其運作方式。 如需 Azure RMS 運作方式的技術資訊，請參閱 [Azure RMS 如何運作？](how-does-it-work.md)



<!--HONumber=Aug16_HO4-->


