---
# required metadata

title: Rights Management 共用應用程式使用者指南 | Azure RMS
description:
keywords:
author: cabailey
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: eaf6d02c-aa36-4915-856e-49bb71ab1484

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: esaggese
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Rights Management 共用應用程式使用者指南 (英文)
Windows 的 Microsoft Rights Management (RMS) 共用應用程式可協助您保護重要的文件與圖片不被不應該看到的人看到，即使您以電子郵件傳送或將它們儲存到另一個裝置。 您也可以使用此應用程式開啟及使用其他人使用相同的 Rights Management 技術保護的檔案。

你只需要至少執行 Windows 7 Service Pack 1 的電腦。 然後從 Microsoft [下載並安裝](http://go.microsoft.com/fwlink/?LinkId=303970) 這個免費的應用程式。

如果您有任何本指南未回答的問題，請參閱 [Windows 的 Microsoft Rights Management 共用應用程式常見問題集](http://go.microsoft.com/fwlink/?LinkId=303971)。 如果您遇到問題，這個網頁也有一些疑難排解的資訊。

## 使用 RMS 共用應用程式的範例
以下是您如何使用 RMS 共用應用程式以協助保護您的檔案的一些範例。

|我想要...|如何執行此動作|
|----------------|------------------|
|**… 與我信任的、在其他組織工作的人安全地分享財務資訊**<br /><br />您與夥伴公司合作並且想要以電子郵件傳送包含預計銷售圖表的 Excel 試算表給他們。 您想要讓他們檢視圖表但不進行變更。|您使用 Excel 中功能區上的 [共用保護]  按鈕，輸入夥伴公司中合作的兩個人員的電子郵件地址，選取 [檢閱者 - 僅檢視] ，然後按一下 [傳送] 。<br /><br />當電子郵件送達夥伴公司時，只有電子郵件中的收件者可以檢視試算表，且他們無法儲存、編輯、列印或轉寄。<br /><br />步驟：[保護使用 Rights Management 共用應用程式，透過電子郵件共用的檔案](sharing-app-protect-by-email.md)。|
|**… 安全地透過電子郵件將文件傳送給使用 iOS 裝置的人**<br /><br />您想要以電子郵件將高度機密的 Word 文件傳送給您知道他們會定期在其 iOS 裝置上檢查電子郵件的同事。|您使用檔案總管以滑鼠右鍵按一下檔案，並選取 [受共用保護]  將檔案當作附件傳送給您的同事。<br /><br />收件者會在其 iOS 裝置上收到電子郵件。 因為收件者沒有用於 iPad 和 iPhone 的 Office，她會按一下電子郵件中的連結會告訴她如何下載共用應用程式，安裝 iOS 裝置版本，然後檢視文件¹。<br /><br />步驟：[保護使用 Rights Management 共用應用程式，透過電子郵件共用的檔案](sharing-app-protect-by-email.md)。|
|**… 檢查誰在何時已開啟我的受保護的文件，並且視需要撤銷存取權**<br /><br />您已安全地與潛在的供應商共用機密設計文件，現在您想要查看誰在何時從哪裡存取它。 然後，當與其中一個供應商進行業務配合時，您想要撤銷原始文件的存取權，讓原先共用的人員無法再讀取文件。|以電子郵件共用文件之後，您移至 [文件追蹤網站](http://go.microsoft.com/fwlink/?LinkId=529562) 以檢查誰已經在何時存取文件。 當您需要停止共用文件時，您選取選項以撤銷存取權。<br /><br />步驟：[當您使用 RMS 共用應用程式時，追蹤及撤銷文件](sharing-app-track-revoke.md)。|
|**… 讀取電子郵件中收到的附件，該電子郵件有安全的共用檔案附件，但是我無法讀取，因為我的公司未使用 Rights Management**<br /><br />電子郵件寄件者是您信任的人員，因為您們過去有業務上的往來，而且您懷疑他們可能會傳送給您潛在新商機的相關資訊。|您依照電子郵件中的指示並按一下連結以註冊 Microsoft Rights Management。 Microsoft 會確認您的組織沒有包含 Azure Rights Management 的訂用帳戶，傳送電子郵件給您以完成免費的註冊程序，然後您使用您的新帳戶登入。 您按一下電子郵件中的第二個連結以安裝 Rights Management 共用應用程式，然後就可以開啟電子郵件附件來了解新商機。<br /><br />步驟：[檢視並使用 Rights Management 保護的檔案](sharing-app-view-use-files.md)。|
|**… 保護我的膝上型電腦上的公司機密檔案，讓我的公司以外的人員無法存取**<br /><br />您經常出差並且使用您的膝上型電腦存取和更新資料夾中的檔案，該資料夾必須受到保護免於未經授權的存取。|您在您的膝上型電腦上已安裝 RMS 共用應用程式。 您可以使用 [檔案總管] 藉由使用範本來保護檔案，範本可以快速保護檔案。 如果您的膝上型電腦遭竊，您不用擔心您的公司以外的人可以存取這些文件。<br /><br />步驟：[使用 Rights Management 共用應用程式保護裝置上的檔案 (就地保護)](sharing-app-protect-in-place.md)。|
¹ PDF 轉譯由 Foxit 提供。 Copyright © 2003–2014 by Foxit Corporation.

## 您想要做什麼事？
> [!NOTE]
> 如需更多技術資訊，例如支援的檔案類型以及如何在企業網路上安裝此應用程式，請參閱《[Rights Management 共用應用程式系統管理員指南](sharing-app-admin-guide.md)》。

-   [下載及安裝共用應用程式](install-sharing-app.md)

-   [保護裝置上的檔案 (就地保護)](sharing-app-protect-in-place.md)

-   [保護您透過電子郵件共用的檔案](sharing-app-protect-by-email.md)

-   [追蹤及撤銷您的文件](sharing-app-track-revoke.md)

-   [檢視及使用受保護的檔案](sharing-app-view-use-files.md)

-   [移除檔案的保護](sharing-app-remove-protection.md)

-   [使用鍵盤快速鍵](sharing-app-keyboard-shortcuts.md)

-   [在對話方塊中指定設定](sharing-app-dialog-box.md)





<!--HONumber=Apr16_HO4-->


