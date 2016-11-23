---
title: "使用 Rights Management 共用應用程式保護裝置上的檔案 (就地保護) | Azure Information Protection"
description: "如何安全地在您的電腦、伺服器或另一個存放裝置上儲存檔案的指示。"
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 09/25/2016
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 33920329-5247-4f6c-8651-6227afb4a1fa
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 9d8354f2d68f211d349226970fd2f83dd0ce810b
ms.openlocfilehash: 1b95c1bf1c747808c7baed97daa449f5c8bb234d


---

# <a name="protect-a-file-on-a-device-protect-inplace-by-using-the-rights-management-sharing-application"></a>使用 Rights Management 共用應用程式保護裝置上的檔案 (就地保護)

>*適用對象︰Active Directory Rights Management Services、Azure Information Protection、Windows 10、Windows 7 SP1、Windows 8、Windows 8.1*

當您就地保護檔案時，它會取代原始、未受保護的檔案。 然後您就可以讓檔案留在原處，將它複製到另一個資料夾或裝置，或共用其所在的資料夾，而檔案仍然會受到保護。 雖然共用受電子郵件保護之檔案的建議方式是直接從 [檔案總管] 或 Office 應用程式 (請參閱[保護使用 Rights Management 共用應用程式，透過電子郵件共用的檔案](sharing-app-protect-by-email.md))，您也可以將受保護檔案附加到電子郵件訊息。

> [!TIP]
> 如果您在嘗試保護檔案時看到任何錯誤，請參考 [Windows 的 Microsoft Rights Management 共用應用程式常見問題集](http://go.microsoft.com/fwlink/?LinkId=303971)。

## <a name="to-protect-a-file-on-a-device-protect-inplace"></a>保護裝置上的檔案 (就地保護)

1.  在 [檔案總管] 中，選取要保護的檔案。 以滑鼠右鍵按一下，選取 [利用 RMS 保護]，然後選取 [就地保護]。 例如：

    ![[就地保護] 功能表選項](../media/ADRMS_MSRMSApp_SP_CompanyDefined.png)

    > [!NOTE]
    > 如果您看不到 [利用 RMS 保護]  選項，可能是您的電腦上未安裝 RMS 共用應用程式，或您的電腦必須重新啟動以完成安裝。 如需如何安裝 RMS 共用應用程式的詳細資訊，請參閱[下載及安裝 Rights Management 共用應用程式](install-sharing-app.md)。

2.  請執行下列其中一項動作：

    -   選取原則範本：這些是通常會在組織中對人員限制存取和使用方式的預先定義權限。 例如，如果您的組織名稱是 Contoso, Ltd，您可能會看到 **Contoso, Ltd - 僅限機密檢視**。 如果這是您第一次在這部電腦上保護檔案，您必須先選取 [公司定義的保護] 以下載範本。

        下一次按 [就地保護] 選項時，您將看到多達 10 個範本可供選擇。 如果有 10 個以上可用的範本但未顯示您想要的範本，請按一下 [公司定義的保護] 以下載並查看所有的範本。

        當您選取原則範本時，您也可以保護多個檔案和資料夾。 當您選取資料夾時，該資料夾中的所有檔案會自動選取為受保護，但您在該資料夾中建立的新檔案將不會自動受到保護。

    -   選取 [自訂權限] ：如果範本沒有提供您需要的保護層級，或者您想要明確地自行設定保護選項，請選擇此選項。 在[新增保護對話方塊](sharing-app-dialog-box.md)中，指定您想用於這個檔案的選項，然後按一下 [套用]。

3.  您可能會快速查看會告訴您檔案正受到保護的對話方塊，然後焦點會返回 [檔案總管]。 選取的檔案目前受到保護。 在某些情況下 (新增的保護變更副檔名時)，[檔案總管] 中的原始檔案會取代為具有 Rights Management 保護鎖定圖示的新檔案。 例如：

    ![RMS 共用應用程式之具有鎖定圖示的受保護檔案](../media/ADRMS_MSRMSApp_Pfile.png)

如果您改變對權限的心意，或之後需要加以修改，只要再次保護檔案。

如果您需要移除檔的保護，請參閱[透過使用 Rights Management 共用應用程式從檔案移除保護](sharing-app-remove-protection.md)。

## <a name="examples-and-other-instructions"></a>範例和其他指示
如需 Rights Management 共用應用程式的使用範例及作法指示，請參閱 Rights Management 共用應用程式使用者指南中下列各節：

-   [使用 RMS 共用應用程式的範例](sharing-app-user-guide.md#examples-for-using-the-rms-sharing-application)

-   [您想要做什麼？](sharing-app-user-guide.md#what-do-you-want-to-do)

## <a name="see-also"></a>另請參閱
[Rights Management 共用應用程式使用者指南 (英文)](sharing-app-user-guide.md)



<!--HONumber=Nov16_HO2-->


