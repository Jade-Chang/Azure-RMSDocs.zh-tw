---
title: "針對使用 Rights Management 保護的檔案變更權限 | Azure RMS"
description: "當檔案已受 Rights Management 保護時，您可以藉由重新保護它，然後指定應該能存取它們的所有使用者以及要授與他們的權限，來變更權限。"
keywords: 
author: cabailey
manager: mbaldwin
ms.date: 08/03/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 5ac121b3-d7a0-40e4-8fe7-90bf4cf796f1
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: ba029e48b540fda8474eba83322c531ff3daa7b3
ms.openlocfilehash: a123338e34a8c4585a01782a473a400ecb58f166


---

# 針對使用 Rights Management 保護的檔案變更權限

*適用於︰Active Directory Rights Management Services、Azure Rights Management、Windows 10、Windows 7 SP1、Windows 8、Windows 8.1*

當檔案已受 Rights Management 保護時，您可以藉由重新保護它，然後指定應該能存取它們的所有使用者以及要授與他們的權限，來變更權限。

> [!IMPORTANT]
> 這不是增量變更，而是完全取代。 您實際上是以您要的完整權限集重新保護檔案。
> 
>  例如，如果檔案受到保護，使得只有行銷部門的人員可以開啟它，而您想要讓銷售部門的人員也可以開啟它，則您必須重新保護檔案，讓銷售部門和行銷部門都能開啟它。
>
> 同樣地，如果您想要新增或移除權限，無法只指定要新增或移除該權限，而是必須指定您希望讓指定的人員具有的所有權限。

如果您是檔案擁有者，想要重新保護 (例如，您原本使用共用應用程式保護它)，則您會自動具有重新保護檔案的權限。 如果不是擁有者，您不一定具有重新保護檔案的權限，這視受保護檔案目前的權限而定。 您需要[完整的控制使用權](../deploy-use/configure-usage-rights.md#usage-rights-and-descriptions)以重新保護檔案。

例如，如果有其他人使用 Rights Management 共用應用程式來保護檔案，並且指定您所屬的群組和 [共同擁有者] 作為自訂權限，則您將能夠重新保護檔案。 不過，如果他們未指定您的名稱或您所屬的群組，或是他們選取了 [檢閱者 - 檢視及編輯]，或是不讓您移除權限的範本，那麼您將無法重新保護檔案。 要找出的最簡單方法，就是嘗試重新保護檔案。

如果您想要完全移除所有權限，讓該檔案不再受到保護，請參閱[移除檔案的保護](sharing-app-remove-protection.md)。

## 就地重新保護檔案

1.  在 [檔案總管] 中，選取要保護的檔案。 以滑鼠右鍵按一下，選取 [利用 RMS 保護]，然後選取 [就地保護]。 例如：

    ![[就地保護] 功能表選項](../media/ADRMS_MSRMSApp_SP_CompanyDefined.png)

    > [!NOTE]
    > 如果您看不到 [利用 RMS 保護]  選項，可能是您的電腦上未安裝 RMS 共用應用程式，或您的電腦必須重新啟動以完成安裝。 如需如何安裝 RMS 共用應用程式的詳細資訊，請參閱[下載及安裝 Rights Management 共用應用程式](install-sharing-app.md)。

2.  請執行下列其中一項動作：

    -   選取原則範本：這些是通常會在組織中對人員限制存取和使用方式的預先定義權限。 例如，如果您的組織名稱是 Contoso, Ltd，您可能會看到 **Contoso, Ltd - 僅限機密檢視**。 如果這是您第一次在這部電腦上保護檔案，您必須先選取 [公司定義的保護] 以下載範本。

        下一次按 [就地保護] 選項時，您將看到多達 10 個範本可供選擇。 如果有 10 個以上可用的範本但未顯示您想要的範本，請按一下 [公司定義的保護] 以下載並查看所有的範本。

        當您選取原則範本時，您也可以保護多個檔案和資料夾。 當您選取資料夾時，該資料夾中的所有檔案會自動選取為受保護，但您在該資料夾中建立的新檔案將不會自動受到保護。

    -   選取 [自訂權限] ：如果範本沒有提供您需要的保護層級，或者您想要明確地自行設定保護選項，請選擇此選項。 在[新增保護對話方塊](sharing-app-dialog-box.md)中，指定您想用於這個檔案的選項，然後按一下 [套用]。

3. 如果您無權重新保護檔案，您會看到 [無法保護內容] 的訊息，以及連絡人 (文件擁有者) 的電子郵件地址，以便他們能夠為您變更權限。

    如果您有權限可以重新保護檔案，您可能會很快看到對話方塊，告訴您檔案正受到保護，然後焦點會返回檔案總管。 選取的檔案目前受到您的變更保護。 

> [!NOTE]
> RMS 必須先確認您有權對這個檔案進行重新保護的動作，您才可以重新保護檔案。 在某些情況下，這可能已快取，所以不會提示您提供認證。 在其他情況下會提示您提供認證。
>
> 如果您的組織不使用 Azure Rights Management (Azure RMS) 或 AD RMS，您可以申請免費帳戶，在接受您的認證後，您就可以使用 RMS 所保護的檔案：
>
> -   若要申請此帳戶，請按一下連結來申請 [個人版 RMS](http://go.microsoft.com/fwlink/?LinkId=309469)。
>
>     當您註冊時，使用您的公司電子郵件地址而不是個人的電子郵件地址。 如果您是因為在電子郵件中收到受保護的附加檔案而註冊，請使用電子郵件訊息寄給您時所使用的相同電子郵件地址。
> -   如需詳細資訊，請參閱[個人版 RMS 和 Azure Rights Management](../understand-explore/rms-for-individuals.md)。

## 重新保護您以電子郵件傳送的檔案

如果您想要變更您以電子郵件傳送之檔案的權限︰

- **讓其他人讀取檔案**︰將檔案以電子郵件傳送給他們，並遵循[保護您以電子郵件共用的檔案](sharing-app-protect-by-email.md)中的指示。

- **變更檔案的權限**︰再次以電子郵件傳送檔案，並遵循[保護您以電子郵件共用的檔案](sharing-app-protect-by-email.md)中的指示，然後選擇您想要的新權限。 

    因為您無法移除原先以電子郵件傳送之檔案上的權限，只能將它們取代為新的版本，所以請考慮撤銷先前以電子郵件傳送的檔案，讓收件者無法再開啟該版本的文件。 如果您需要使權限更嚴格 (例如，移除不應該能存取檔案的人員，或是他們應該無法再對其進行編輯)，撤銷便很適合。

    若要撤銷以電子郵件傳送的檔案，請參閱[追蹤及撤銷您的文件](sharing-app-track-revoke.md)。


## 範例和其他指示
如需 Rights Management 共用應用程式的使用範例及作法指示，請參閱 Rights Management 共用應用程式使用者指南中下列各節：

-   [使用 RMS 共用應用程式的範例](sharing-app-user-guide.md#examples-for-using-the-rms-sharing-application)

-   [您想要做什麼事？](sharing-app-user-guide.md#what-do-you-want-to-do)

## 另請參閱
[Rights Management 共用應用程式使用者指南 (英文)](sharing-app-user-guide.md)



<!--HONumber=Aug16_HO1-->


