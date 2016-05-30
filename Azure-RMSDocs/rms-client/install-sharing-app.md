---
# required metadata

title: 下載並安裝 Rights Management 共用應用程式 | Azure RMS
description:
keywords:
author: cabailey
manager: mbaldwin
ms.date: 05/09/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 2bf09690-9dba-43b7-9e0a-0110915d4081

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: esaggese
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# 下載及安裝 Rights Management 共用應用程式

*適用於︰Active Directory Rights Management Services、Azure Rights Management、Windows 10、Windows 7 SP1、Windows 8、Windows 8.1*

您不需要是本機系統管理員也能安裝 RMS 共用應用程式。 然而，如果你不是本機系統系統管理員，且使用 Office 2010，則會有一些限制。 如需詳細資訊，請參閱本頁面上的[如果您不是本機系統管理員並使用 Office 2010](#if-you-are-not-a-local-administrator-and-use-office-2010) 一節。

## 下載及安裝 Rights Management 共用應用程式

1.  移至 Microsoft 網站上的 [Microsoft Rights Management](http://go.microsoft.com/fwlink/?LinkId=303970) 頁面。

2.  在 [電腦]  區段中，按一下 [適用於 Windows 的 RMS 應用程式]  的圖示並儲存 **Setup.exe** 檔案，以安裝 Microsoft Rights Management 共用應用程式。

3.  按兩下下載的 Setup.exe 檔案。 如果系統提示您繼續進行，請按一下 **[是]**.

4.  在 [安裝 Microsoft RMS]  頁面上按 [下一步] ，並等候安裝完成。

    > [!NOTE]
    > RMS 共用應用程式需要至少 Microsoft.NET Framework 4.0 版。 安裝程式會檢查是否已安裝，如果尚未安裝，您會看到訊息，具有安裝的連結。

5.  當安裝完成時，按一下 [重新啟動]  以重新啟動您的電腦並完成安裝。 或者按一下 [關閉]  ，稍後重新啟動電腦以完成安裝。

您現在已就緒可以開始保護您的檔案，或者讀取其他人已保護的檔案。

## 如果你不是本機系統管理員並使用 Office 2010
如果您登入您的電腦，且不具有本機系統管理權限，當安裝程式偵測到你已經安裝 Office 2010，你會看到一則警告訊息，指出某些案例將不適用於此設定。 案例包括：

-   如果您的組織使用 Azure RMS，而不是內部部署版本的 RMS：

    -   將無法使用 Office 的資訊版權管理 (IRM) 功能。 例如，電子郵件的**不要轉發**選項、可以從 Word 和 Excel 的 [檔案] 功能表設定的**限制存取**許可權。 您可以使用功能區上的 [保護的共用] 選項，以及 [檔案總管] 中的按右鍵選項。

-   如果您的組織使用內部部署的 RMS，而不是 Azure RMS：

    -   若使用 Azure RMS 的其他組織中的人傳送受保護的文件給您，你將無法讀取文件。

如果您不是本機系統管理員，並使用 Office 365 或辦公室 2013，你不會看到這則訊息和支援的那些案例。

您可以繼續安裝並接受這些已知的限制。 或者，你可以停止安裝，然後重新執行安裝並在執行步驟 3 的 Setup.exe 時使用 [以系統管理員身份執行] 選項，或是請系統管理員為您安裝。 系統管理員可以為您[用指令碼進行此安裝](sharing-app-admin-guide.md#automatic-deployment-for-the-microsoft-rights-management-sharing-application)，讓它自動安裝。

## 範例和其他指示
如需 Rights Management 共用應用程式的使用範例及作法指示，請參閱 Rights Management 共用應用程式使用者指南中下列各節：

-   [使用 RMS 共用應用程式的範例](sharing-app-user-guide.md#examples-for-using-the-rms-sharing-application)

-   [您想要做什麼事？](sharing-app-user-guide.md#what-do-you-want-to-do-)

## 另請參閱
[Rights Management 共用應用程式使用者指南 (英文)](sharing-app-user-guide.md)



<!--HONumber=May16_HO2-->


