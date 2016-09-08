---
title: "案例 - 保留 SharePoint 中儲存之文件的控制 | Azure RMS"
description: "此案例和支援的使用者文件使用 Azure Rights Management 來確保您能夠控制儲存在 SharePoint 中的 Office 文件。 例如，文件會自動施以保護，以避免使用者蓄意或意外洩漏，同時還能在文件下載或同步處理之後，封鎖對內容的存取。 需要保護的檔案可能會是需要內部共同作業的設計文件或計畫，也可能屬於其他交付項目。 當您設定 SharePoint 的受保護文件庫時，其中所儲存的 Office 檔案會由 Azure Rights Management 提供保護。"
author: cabailey
manager: mbaldwin
ms.date: 08/24/2016
ms.topic: get-started-article
ms.prod: 
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 1b6244c7-5ab9-4881-bc8f-6fa960390d89
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 024a29d7c7db2e4c0578a95c93e22f8e7a5b173e
ms.openlocfilehash: f0dfe895820d33eab1d3a69c92e881287072f554


---

# 案例 - 保留 SharePoint 中儲存之文件的控制

>*適用於︰Azure Rights Management、Office 365*

此案例和支援的使用者文件使用 Azure Rights Management 來確保您能夠控制儲存在 SharePoint 中的 Office 文件。 例如，文件會自動施以保護，以避免使用者蓄意或意外洩漏，同時還能在文件下載或同步處理之後，封鎖對內容的存取。 需要保護的檔案可能會是需要內部共同作業的設計文件或計畫，也可能屬於其他交付項目。 當您設定 SharePoint 的受保護文件庫時，其中所儲存的 Office 檔案會由 Azure Rights Management 提供保護。

指示適用於下列一組情況：

-   員工共用及合作處理 SharePoint 文件庫中的 Office 文件。

-   對於系統管理員在文件庫層級所設定的權限，員工無須設定或變更。

-   員工不需要與組織外的人共用這些文件。

## 部署指示
![Azure RMS 快速部署的系統管理員指示](../media/AzRMS_AdminBanner.png)

繼續使用者文件之前，請確定符合下列需求和支援程序。

## 此案例的需求
此案例要能運作，必須滿足下列條件：

|需求|如果需要更多資訊|
|---------------|--------------------------------|
|您已針對 Office 365 或 Azure Active Directory 準備帳戶和群組|[準備 Azure Rights Management](https://technet.microsoft.com/library/jj585029.aspx)|
|Azure Rights Management 已啟動|[啟用 Azure Rights Management](https://technet.microsoft.com/library/jj658941.aspx)|
|若要使用 SharePoint Server：部署 RMS 連接器，並針對 SharePoint 加以設定|[部署 Azure Rights Management 連接器](https://technet.microsoft.com/library/dn375964.aspx)|
|設定 SharePoint 網站要保護的權限|[管理清單、文件庫、資料夾、文件或清單項目的權限](https://support.office.com/en-ca/article/Manage-permissions-for-a-list-library-folder-document-or-list-item-9d13e7df-a770-4646-91ab-e3c117fcef45)<br /><br />[將資訊版權管理套用至清單或文件庫](http://office.microsoft.com/sharepoint-help/apply-information-rights-management-to-a-list-or-library-HA102891460.aspx)|
|設定 SharePoint 的 IRM 及受保護文件庫|[在 SharePoint 系統管理中心設定資訊版權管理 (IRM)](https://support.office.com/en-us/article/Set-up-Information-Rights-Management-IRM-in-SharePoint-admin-center-239ce6eb-4e81-42db-bf86-a01362fed65c)<br /><br />[將資訊版權管理套用至清單或文件庫](http://office.microsoft.com/sharepoint-help/apply-information-rights-management-to-a-list-or-library-HA102891460.aspx)|

### 設定 IRM 設定中的 SharePoint 文件庫

1.  設定 SharePoint 使用 IRM 服務之後，瀏覽至您的 SharePoint 文件庫以 Azure RMS 保護。 在網站的 **[設定]** &gt; **[資訊版權管理 (IRM)]** 頁面中，需選取 **[限制此文件庫的下載權限]**，並指定系統管理員的原則標題和使用者的原則描述，然後按一下 **[顯示選項]**。

2.  選取下列選項：

    -   **不允許使用者上傳不支援 IRM 的文件**

    -   選擇性：**允許群組保護。預設群組**，然後指定額外群組的名稱，此群組可能需要對此文件庫中儲存之文件共同作業，但是在 SharePoint 之外。 例如，「銷售」群組具有網站的編輯權限，群組中的某人下載了文件、將它儲存至磁碟，然後以電子郵件傳送給不屬於「銷售」群組的同事。 如果該名同事屬於您在此處指定的群組，她會自動繼承為此網站設定的相同權限，而且能夠編輯文件。

        若不選取此選項，有權存取 SharePoint 文件庫的使用者將能夠在這些文件共同作業，且只能直接從 SharePoint 下載文件。 在許多情況下，這項限制是適當的。

## 使用者文件指示
此案例因為不需要使用者執行任何特殊的動作，所以沒有給使用者的程序指示。 文件會依據 SharePoint 系統管理員為網站設定的權限而在下載時自動受到保護。 但是，請告知使用者這項改變讓他們知道會遇到的情況，並且讓技術支援人員知道哪些文件庫受到保護，以及他們在使用這類文件時的限制。 例如目前的限制可能會讓文件只能在行動裝置上檢視而無法編輯。 如果您設定群組保護，請讓使用者知道哪些群組可存取及編輯 SharePoint 外部的文件。

使用下列範本，將公告複製並貼到使用者通訊上，然後進行這些修改以反映您的環境︰

1.  以您為 Azure Rights Management 設定的 SharePoint 文件庫名稱和連結取代 *&lt;SharePoint 文件庫名稱&gt;* 的每個執行個體。 如果此通訊是針對多個受保護的文件庫，請據此變更的指示。

2.  如果您設定了 **[允許群組保護預設群組]** 選項，請以您設定的群組名稱取代 *&lt;群組名稱&gt;*，並提供 &lt;為何此群組具有存取權限可在此檔案共同作業，但不是使用 SharePoint 文件庫&gt; 的原因。 如果您未設定此選項，請刪除這一句。

3.  將*&lt;連絡人詳細資料&gt;* 取代為您的使用者可以與技術支援人員連絡的指示，例如網站連結、電子郵件地址或電話號碼。

4.  對公告進行您想要的任何其他修改，然後將其傳送給這些使用者。

範例文件會顯示這項公告在您的自訂之後，就使用者看來的可能外觀如何。

![Azure RMS 快速部署的範本使用者文件](../media/AzRMS_UsersBanner.png)

### IT 公告︰變更為 &lt;SharePoint 文件庫的名稱&gt; 網站
SharePoint 網站 **&lt;SharePoint 文件庫的名稱&gt;** 現在已設有保護，可安全地共同作業。 現在，只有 &lt;群組名稱&gt; 的成員可以從這個網站打開這些文件，即使您保存在本機或以電子郵件傳送給其他人。 例外情況是，在您下載文件後您可以與 &lt;群組名稱&gt; 的成員共用它們，符合 &lt;為何此群組具有存取權限可在此檔案共同作業，但不是使用 SharePoint 文件庫&gt; 所述。 當你編輯檔案時，在文件最上方會看黃色的資訊橫幅，告知您它受到這項保護以及誰可以存取文件。

這項變更有助於保護我們公司的機密資料安全，不被不該看到的人看到。 如果您使用行動裝置存取這些受保護的文件，你可以檢視它們，但您必須使用桌面設備才能編輯它們。

如果 &lt;SharePoint 網站的名稱&gt; 網站不支援安全的共同作業，您將無法將文件上傳到此網站。

**需要協助嗎？**

-   請連絡技術支援人員：&lt;連絡人詳細資料&gt;

### 範例使用者文件
![Azure RMS 快速部署的範例使用者文件](../media/AzRMS_ExampleBanner.png)

#### IT 公告：變更銷售預測與報表網站
SharePoint **銷售預測與報表**網站現在已設有保護，可安全地共同作業。 現在，只有｢銷售和行銷團隊｣的成員可以從這個網站打開這些文件，即使你保存在本機或以電子郵件傳送給其他人。 例外情況是，你可以在下載文件後與｢財務團隊｣的成員共用文件，以便他們可以擷取每月的預測數字。 當你編輯檔案時，在文件最上方會看黃色的資訊橫幅，告知您它受到這項保護以及誰可以存取文件。

這項變更有助於保護我們公司的機密資料安全，不被不該看到的人看到。 如果您使用行動裝置存取這些受保護的文件，你可以檢視它們，但您必須使用桌面設備才能編輯它們。

如果｢銷售預測和報告｣網站不支援安全的共同作業，你將無法將文件上傳到｢銷售預測和報告｣網站。

**需要協助嗎？**

-   請連絡技術支援人員：helpdesk@vanarsdelltd.com




<!--HONumber=Aug16_HO4-->


