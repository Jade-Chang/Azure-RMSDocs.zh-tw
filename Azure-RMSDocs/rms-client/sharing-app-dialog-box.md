---
title: "Rights Management 共用應用程式的對話方塊選項 | Azure RMS"
description: "協助您在 RMS 共用應用程式的 [新增保護] 對話方塊或 [共用保護] 對話方塊中指定選項的資訊。 當您保護要共用的檔案或就地保護檔案並選擇自訂權限時，您會看到這個對話方塊。"
author: cabailey
manager: mbaldwin
ms.date: 08/25/2016
ms.topic: article
ms.prod: 
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 7b91ab30-6363-4929-bcbd-4dfbd05f644a
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 035c9eb6cb630cafd5bd7fc7e2371340043ddc5e
ms.openlocfilehash: 5f652b0e75350656f446c05d2464319ba46e06ad


---

# Rights Management 共用應用程式的對話方塊選項

>*適用於︰Active Directory Rights Management Services、Azure Rights Management、Windows 10、Windows 7 SP1、Windows 8、Windows 8.1*

使用此資訊來幫助您在 RMS 共用應用程式的 [新增保護]  對話方塊或 [共用保護]  對話方塊中指定選項。 當您[保護要共用的檔案](sharing-app-protect-by-email.md)或[就地保護檔案](sharing-app-protect-in-place.md)並選擇自訂權限時，您會看到這個對話方塊方塊。

> [!IMPORTANT]
> 如果您看到的選項與此處所列的不同，您可能未安裝最新版本的共用應用程式。 您可以從 [Microsoft Rights Management](http://go.microsoft.com/fwlink/?LinkId=303970) 頁面下載最新版本。
> 
> 如何知道是否您有最新版本？ 尋找列在 [程式和功能] 中的 [Microsoft Rights Management 共用應用程式]  ，並檢查對應的版本號碼。 若要查看及使用資料表中的選項，版本應該至少是 **1.0.1770.0**。 您可以從下載頁面檢查最新版本號碼。

除了您可以選擇的選項，您可能也想知道：

-   [自動建立的 .ppdf 檔案是什麼？](#what-s-the-ppdf-file-that-s-automatically-created)

-   [一般保護和內建 (原生) 保護有何差異？](#what-s-the-difference-between-generic-protection-and-built-in-native-protection)

|選項|描述|
|----------|---------------|
|**使用者**|如果您尚未從 Outlook 指定電子郵件地址，請輸入您允許開啟檔案的人員的電子郵件地址。<br /><br />請注意，RMS 共用應用程式不支援所有的電子郵件地址。<br /><br />如果您的組織使用 Rights Management (AD RMS) 內部部署版本，您可以指定電子郵件地址僅限於組織內的人員。 在此情況下，如果您嘗試指定外部電子郵件地址，您會看到訊息指出，您的公司設定僅允許在公司內共用受保護的內容。 <br /><br /> 如果您的組織使用 Azure RMS，您指定的電子郵件地址可以是您組織內的人或另一個組織的人。<br /><br />例如：**janetm@contoso.com; p.dover@fabrikam.com**<br /><br />RMS 共用應用程式目前不支個人電子郵件地址。|
|**一般保護**|如果選取這個選項，就表示您選取的檔案無法受到原生保護。 如需詳細資訊，請參閱 本頁面的[一般保護和內建 (原生) 保護有何差異？](#what-s-the-difference-between-generic-protection-and-built-in-native-protection)|
|**檢閱者 - 僅檢視**<br /><br />**檢閱者 - 檢視及編輯**<br /><br />**共同作者 - 檢視、編輯、複製及列印**<br /><br />**共同擁有者 - 所有權限**<br /><br />注意：這些選項的名稱前面全都有一個代表地球儀的圓形圖示。 使用這個圖示是因為，當您傳送附件給另一個組織中的某人時，通常會選取其中一個選項。|如果您想要定義受保護文件的權限，請選取其中一個選項。 按一下每個選項可檢視描述。<br /><br />當您選擇其中一個選項時，只有您在 [使用者]  中指定的人員，才有您指定的權限可開啟和使用文件。 例如，如果他們轉寄給別人，則別人無法開啟文件。|
|您的系統管理員所設定的原則範本。<br /><br />例如，如果您的公司名稱是 Contoso, Ltd，您可能會看到 **Contoso, Ltd - 僅限機密檢視**<br /><br />注意：這些選項的名稱前面全都有一個代表辦公大樓的方形圖示。 使用這個圖示是因為，當您傳送附件給您組織中的某人時，通常會選取其中一個選項。|當與您組織中的人員共用文件時，您會看到系統管理員所設定的可用原則範本。 不應該在組織外共用文件時，請選擇其中一個原則範本。<br /><br />當您選擇其中一個選項時，您的系統管理員會定義文件的權限和哪些人可以開啟文件。|
|**這些文件的到期日**|僅針對時間緊迫的檔案選取這個選項，您選取的使用者在您指定日期之後就無法開啟這些檔案。 您仍然可以開啟原始檔案，但在您指定的那天午夜過後 (您目前的時區)，其他人將無法開啟檔案。<br /><br />如果您選取系統管理員所設定的原則範本，則無法使用這個選項。|
|**當有人嘗試開啟這些文件時傳送電子郵件給我**|注意：這個選項目前為預覽狀態。<br /><br />每當有人嘗試開啟您所保護的文件時，如果您想要收到電子郵件通知，請選取這個選項。 電子郵件訊息將告訴您是誰嘗試開啟、何時嘗試及是否成功。<br /><br />只有當您的組織使用 Azure RMS 時，才有這個選項可用。 如果您的組織使用 Rights Management (AD RMS) 內部部署版本，您不會看到這個選項。|
|**允許我立即撤銷這些文件的存取權**|如果您稍後可能需要使用文件追蹤網站撤銷文件的存取權，且撤銷必須立即生效，請選擇這個選項。 不過，設定這個選項表示在未撤銷文件之前，使用者每次存取文件時，永遠需要網際網路連線才能讀取文件。 在某些情況下，使用者可能無法將他們的裝置連線到網際網路，使用者也就無法如您預期般地讀取文件。<br /><br />如果您沒有選擇這個選項，您稍後還是可以使用文件追蹤網站來撤銷文件。 不過，因為使用者不一定需要網際網路連線才能讀取文件，所以不會立即得知文件已被撤銷，因而能夠繼續讀取文件，直到下次再向 Azure RMS 驗證為止。 根據預設，某人最多有 30 天可以持續讀取您已撤銷的受保護文件，但是系統管理員可以將此值變更為少於或多於 30 天。<br /><br />只有當您的組織使用 Azure RMS 時，才有這個選項可用。 如果您的組織使用 Rights Management (AD RMS) 內部部署版本，您不會看到這個選項。|

## 一般保護和內建 (原生) 保護有何差異？

-   當您 **對檔案施以一般保護**時，未經授權的人員無法開啟檔案。 但在獲得授權的人員開啟檔案之後，他們可以將檔案以未受保護的方式轉寄給其他人，或儲存在其他人可以存取的位置。 不過，他們會看到訊息，指出他們對檔案擁有的權限，並要求他們遵守，但無法強制執行這項保護。 此外，當您對檔案施以一般保護時，您無法超越授權來限制權限。 比方說，您不能將內容限制為僅檢視或不可列印。

    > [!NOTE]
    > 受一般保護的檔案一律具有副檔名 **.pfile**。

-   相較之下，當您使用 Rights Management 的**內建 (原生) 保護**來保護支援此選項的應用程式時 (例如 Office 檔案)，檔案保護即生效，即使檔案後來傳送給別人或另存他處也一樣。 當您保護這些檔案時，您可以使用嚴格的權限，例如唯讀，或可編輯但不可列印或複製的權限。 例如，您可以選取 [檢閱者 - 僅檢視] ，以禁止編輯、列印或複製內容。

如需其他技術資訊，請參閱《[Rights Management 共用應用程式系統管理員指南](sharing-app-admin-guide.md)》中的[保護層級 – 原生和一般](sharing-app-admin-guide-technical.md#levels-of-protection-native-and-generic)一節。

## 什麼是自動建立的 .ppdf 檔案？

-   當您透過電子郵件共用受保護的檔案時 (共用保護)，RMS 共用應用程式會自動為 Word、 Excel、 PowerPoint 或 PDF 建立檔案的 **.ppdf** 版本。 這是檔案的唯讀受保護版本，只有獲得授權的人員才可以開啟，也可確保收件者一定可以讀取附件，即使他們使用的行動裝置沒有原本就支援 Rights Management 的應用程式也沒問題。 如果這些人有安裝 RMS 共用應用程式，他們將能夠讀取附件。

    在此情況下，不同於受一般保護的檔案，將會強制執行使用限制。 收件者將無法儲存這個版本的檔案，如果他們將附件轉寄給別人，文件仍然保有原始限制。 只有已獲授權開啟受保護文件的人才可以開啟文件。

    > [!NOTE]
    > 共用保護時 (透過電子郵件共用) 會自動建立 .ppdf 檔案，但就地保護時不會建立。

## 範例和其他指示
如需 Rights Management 共用應用程式的使用範例及作法指示，請參閱 Rights Management 共用應用程式使用者指南中下列各節：

-   [使用 RMS 共用應用程式的範例](sharing-app-user-guide.md#examples-for-using-the-rms-sharing-application)

-   [您想要做什麼事？](sharing-app-user-guide.md#what-do-you-want-to-do)

## 另請參閱
[Rights Management 共用應用程式使用者指南 (英文)](sharing-app-user-guide.md)




<!--HONumber=Aug16_HO4-->


