---
# required metadata

title: 保護使用 Rights Management 共用應用程式，透過電子郵件共用的檔案 | Azure RMS
description:
keywords:
author: cabailey
manager: mbaldwin
ms.date: 05/09/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 4c1cd1d3-78dd-4f90-8b37-dcc9205a6736

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: esaggese
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# 藉由使用 Rights Management 共用應用程式，保護您透過電子郵件共用的檔案

*適用於︰Active Directory Rights Management Services、Azure Rights Management、Windows 10、Windows 7 SP1、Windows 8、Windows 8.1*

當您保護您透過電子郵件共用的檔案時，它會建立新版本的原始檔。 原始檔仍未受保護，且新版本受保護且會自動附加到您稍後要傳送的電子郵件。

在某些情況下 (如 Microsoft Word、Excel 和 PowerPoint 所建立的檔案)，RMS 共用應用程式會將它附加到電子郵件訊息的檔案建立兩個版本。 檔案的第二個版本具有 **.ppdf** 副檔名，而且是檔案的 PDF 陰影複製。 即使收件者安裝的應用程式與您用來建立檔案的應用程式不同，這個版本的檔案仍可確保收件者永遠可以讀取檔案。 此案例通常適用於人員在行動裝置上讀取他們的電子郵件，並想要檢視其電子郵件附件時。 若要開啟檔案，他們只需要 RMS 共用應用程式。 然後，他們就可以讀取附加的檔案，但是在他們使用支援 RMS 的應用程式開啟其他版本的檔案之前，他們無法將其變更。

如果您的組織使用 Azure RMS，您就可以追蹤您透過共用保護的檔案：

-   選取一個選項，以在有人嘗試開啟這些受保護的附件時收到電子郵件。 每次有人存取檔案時，您都會收到通知，了解誰在嘗試開啟檔案、何時嘗試以及是否成功 (他們是否成功通過驗證)。

-   使用文件追蹤網站。 您甚至可以藉由在文件追蹤網站中撤銷檔案的存取權以停止共用檔案。 如需詳細資訊，請參閱 [當您使用 RMS 共用應用程式時，追蹤及撤銷文件](sharing-app-track-revoke.md)。.

## 使用 Outlook：保護您以電子郵件共用的檔案

1.  建立電子郵件訊息並附加檔案。 然後，在 **[訊息]** 索引標籤的 **[RMS]** 群組中，按一下 **[共用保護]** ，接著再按一下 **[共用保護]** ：

    ![適用於 RMS 共用應用程式的 Outlook 增益集](../media/ADRMS_MSRMSApp_SP_OutlookToolbar.png)

    如果看不到這個按鈕，很可能您的電腦上未安裝 RMS 共用應用程式、沒有安裝最新版本，或您的電腦必須重新啟動以完成安裝。 如需如何安裝共用應用程式的詳細資訊，請參閱 [下載及安裝 Rights Management 共用應用程式](install-sharing-app.md)。.

2.  在 [[共用保護的檔案]](sharing-app-dialog-box.md) 對話方塊中，為此檔案指定您想要的選項，然後按一下 **[立即傳送]**。.

### 保護您透過電子郵件共用之檔案的其他方式
除了使用 Outlook 共用受保護的檔案，您也可以使用這些替代方案：

-   從 [檔案總管]：這個方法適用於所有檔案。

-   從 Office 應用程式：這個方法適用於 RMS 共用應用程式使用 Office 增益集支援的應用程式，如此您就會在功能區上看到 **RMS** 群組。

#### 使用 [檔案總管] 或 Office 應用程式：保護您以電子郵件共用的檔案

1.  使用下列其中一個選項：

    -   對於 [檔案總管]：以滑鼠右鍵按一下檔案，選取 [利用 RMS 保護]，然後選取 [共用保護]：

        ![[共用受保護的檔案] 功能表選項](../media/ADRMS_MSRMSApp_ShareProtectedMenu.png)

    -   若為 Office 應用程式、Word、Excel 和 PowerPoint：確定您已先行儲存檔案。 然後，在 [ **首頁** ] 索引標籤的 [ **RMS** ] 群組中按一下 [ **共用保護** ]，然後再次按一下 [ **共用保護** ]：

        ![Office 工具列增益集](../media/ADRMS_MSRMSApp_SP_OfficeToolbar.png)

    如果看不到保護的這些選項，很可能您的電腦上未安裝 RMS 共用應用程式、沒有安裝最新版本，或您的電腦必須重新啟動以完成安裝。 如需如何安裝共用應用程式的詳細資訊，請參閱 [下載及安裝 Rights Management 共用應用程式](install-sharing-app.md)。.

2.  在 [[共用受保護的檔案]](sharing-app-dialog-box.md) 對話方塊中，為此檔案指定您想要的選項，然後按一下 **[傳送]**。.

3.  您可能會快速看到一個對話方塊，告訴您檔案已受保護，然後您會看到為您建立的電子郵件訊息，告知您受到 Microsoft RMS 保護之附件的收件者，以及他們必須登入。 當使用者按一下連結以登入時，他們會看到指示與連結，以確保他們可以開啟您的受保護附件。

    範例：

    ![Azure RMS 的電子郵件訊息](../media/ADRMS_MSRMSApp_EmailMessage.PNG)

    您想知道：[自動建立的 .ppdf 檔案是什麼？](sharing-app-dialog-box.md#what-s-the-ppdf-file-that-s-automatically-created-)

4.  選用：您可以任意變更此電子郵件訊息中的任何項目。 例如，您可以加入或變更訊息中的主旨或文字。

    > [!WARNING]
    > 雖然您可以從此電子郵件訊息新增或移除人員，但這不會變更您在 [ **共用保護** ] 對話方塊中指定的附件權限。 如果您想要變更那些權限，例如，授與新的人員開啟檔案的權限，關閉電子郵件訊息但不儲存或傳送，以及返回步驟 1。

5.  傳送電子郵件訊息。

## 範例和其他指示
如需 Rights Management 共用應用程式的使用範例及作法指示，請參閱 Rights Management 共用應用程式使用者指南中下列各節：

-   [使用 RMS 共用應用程式的範例](sharing-app-user-guide.md#examples-for-using-the-rms-sharing-application)

-   [您想要做什麼事？](sharing-app-user-guide.md#what-do-you-want-to-do-)

## 另請參閱
[Rights Management 共用應用程式使用者指南 (英文)](sharing-app-user-guide.md)


<!--HONumber=May16_HO2-->


