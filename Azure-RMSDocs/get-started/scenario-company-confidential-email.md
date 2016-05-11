---
# required metadata

title: 案例 - 傳送公司機密電子郵件 | Azure RMS
description:
keywords:
author: cabailey
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 950799e9-2289-48c7-b95a-f54a8ead520a

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: esaggese
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# 案例 - 傳送公司機密電子郵件
此案例和支援使用者文件會使用 Azure Rights Management，如此組織中的任何使用者都可以安全地傳送電子郵件通訊，讓組織外部的人員無法讀取。 例如，如果有人轉送電子郵件訊息給另一個組織的某個人，或個人的電子郵件帳戶。 這些電子郵件及所有附件均由 Azure Rights Management 提供保護，且使用者從電子郵件用戶端選取的範本。

若要啟用這種情況，最簡單的方法是使用其中一個內建的預設範本來自動限制存取組織中的所有使用者。 但如果需要，您可以更嚴格限制，例如，藉由建立自訂範本、限制使用者子集的存取權，或設定其他限制，例如唯讀或到期日，或停用電子郵件用戶端中的 [轉寄] 按鈕。

> [!IMPORTANT]
> 在此案例中，雖然您可以從設定的自訂範本直接移除 [轉寄]，且這會停用電子郵件用戶端中的 [轉寄] 按鈕，但此設定不會防止使用者與其他授權的使用者共用電子郵件。 收件者可儲存電子郵件 (和任何附件)，然後使用其他共用的機制以共用資訊。
> 
> 比方說，Bob 使用套用了 [儲存檔案] 和 [編輯內容] 自訂權限 (針對行銷群組) 的自訂範本，將電子郵件寄給 Alice，並且不含 [轉寄] 權限。 即使 Alice 無法將電子郵件轉寄給其他人，她可以將電子郵件訊息和任何附件儲存至 USB 磁碟機或檔案伺服器共用，其中行銷群組的任何成員接著可以讀取並編輯 (如果他們可存取這些檔案)。 非行銷群組中的使用者無法開啟內容。

指示適用於下列一組情況：

-   組織內的任何使用者若要與組織內的其他人共用資訊，但不應在組織外部共用資訊。

-   要共用的資訊可以在電子郵件訊息或附件中。

-   使用者必須從他們的電子郵件用戶端中手動選取範本。

## 部署指示
![](../media/AzRMS_AdminBanner.png)

繼續使用者文件之前，請確定符合下列需求。

## 此案例的需求
此案例的指示要能運作，必須滿足下列條件：

|需求|如果需要更多資訊|
|---------------|--------------------------------|
|您已針對 Office 365 或 Azure Active Directory 準備帳戶和群組|[準備 Azure Rights Management](https://technet.microsoft.com/library/jj585029.aspx)|
|您的 Azure Rights Management 租用戶金鑰由 Microsoft 管理；您不會使用 BYOK|[規劃及實作 Azure Rights Management 租用戶金鑰](https://technet.microsoft.com/library/dn440580.aspx)|
|Azure Rights Management 已啟動|[啟用 Azure Rights Management](https://technet.microsoft.com/library/jj658941.aspx)|
|發生下列情形之一：<br /><br />Azure Rights Management 會啟用 Exchange Online<br /><br />RMS 連接器已針對 Exchange 內部部署安裝和設定|針對 Exchange Online：請參閱 Exchange Online：IRM 組態一節 (位於[針對 Azure Rights Management 設定應用程式](https://technet.microsoft.com/library/jj585031.aspx))。<br /><br />針對 Exchange 內部部署：[部署 Azure Rights Management 連接器](https://technet.microsoft.com/library/dn375964.aspx)|
|您尚未封存預設的 Azure Rights Management 範本 &lt;組織&gt; - 機密。 或者，您已經針對此目的設定自訂範本 (因為您需要更嚴格的設定)，或只有組織中的部分使用者能夠讀取受保護的電子郵件。|[設定 Azure Rights Management 的自訂範本](https://technet.microsoft.com/library/dn642472.aspx)<br /><br />提示︰如果需要更嚴格的使用原則設定，但對於組織中的所有使用者，複製然後編輯其中一個預設範本，而不從頭開始建立範本。<br /><br />不會針對此案例中的電子郵件用戶端立即重新整理更新的範本。 如需詳細資訊，請參閱設定範本文章的[重新整理使用者的範本](https://technet.microsoft.com/library/dn642472.aspx)一節。|
|傳送受保護電子郵件的使用者擁有 Outlook 2013 或 Outlook 2016 或 Outlook Web Access。<br /><br />收到電子郵件的使用者具有可支援 Azure Rights Management 的電子郵件用戶端。|您可以使用 Outlook 2010，但是您必須[安裝適用於 Windows 的 Rights Management 共用應用程式](https://technet.microsoft.com/library/dn339003.aspx)，並據此調整使用者指示。<br /><br />如需支援 Azure Rights Management 的電子郵件用戶端清單，請參閱 [Azure Rights Management 的需求](https://technet.microsoft.com/library/dn655136.aspx)的[用戶端裝置功能](https://technet.microsoft.com/library/dn655136.aspx)資料表中的電子郵件資料行。|

## 使用者文件指示
使用下列範本，將使用者指示複製並貼到使用者通訊上，然後進行這些修改以反映您的環境 ︰

1.  以您的組織名稱取代 &lt;組織名稱&gt; 的所有執行個體。

2.  以您的預設或自訂範本名稱取代 &lt;組織名稱 - 機密&gt; 的所有執行個體。

3.  取代螢幕擷取畫面，使它們顯示您的組織範本名稱。

4.  將 &lt;連絡人詳細資料&gt; 取代為您的使用者可以與技術支援人員連絡的指示，例如網站連結、電子郵件地址或電話號碼。

5.  **您可能想要進行的其他修改：**

    -   如果能將指示限制成僅供一個電子郵件用戶端，則為了簡單起見，請考慮這麼做並刪除其他指示集。

    -   如果您使用自訂範本而非建議的預設範本，請據此修改文字︰

        -   製作更具體的標題。

        -   在步驟 1 中指定要選取的使用者或群組。

        -   在步驟 2 中指定自訂範本的名稱。

        -   修改最後一個段落以解釋收件者將會有的限制。

6.  對此指示集進行任何想要的修改，然後將它傳送給這些使用者。

7.  由於某些用戶端不支援 Rights Management，您可能需要對這些受保護的電子郵件訊息的收件者提供指引和建議。 此資訊會根據您的組織正在使用的裝置和電子郵件應用程式，和您擁有的任何喜好設定。 例如，建議 iOS 使用者使用 Outlook for iPad and iPhone 讀取受保護的電子郵件，而非原生的 iOS 郵件用戶端。

    如需電子郵件用戶端的田資訊，請參閱 [Azure Rights Management 的需求](https://technet.microsoft.com/library/dn655136.aspx)的[用戶端裝置功能](https://technet.microsoft.com/library/dn655136.aspx)資料表中的電子郵件資料行。

範例文件會顯示這些指示在您的自訂之後，就使用者看來的可能外觀如何。

![](../media/AzRMS_UsersBanner.png)

### 如何使用 Outlook 傳送包含公司機密資訊的電子郵件

1.  在 Outlook 中，建立新的電子郵件訊息，新增您想要包括的任何附件，然後從 [&lt;組織名稱&gt;] 選取使用者或群組。

2.  從 [選項] 索引標籤，按一下 [權限]，然後選取 [&lt;組織名稱 - 機密&gt;]：

    ![](../media/AzRMS_OutlookTemplate.PNG)

3.  傳送訊息。

### 如何使用 Outlook Web App 傳送包含公司機密資訊的電子郵件

1.  在 Outlook Web App 中，建立新的電子郵件訊息，新增您想要包括的任何附件，然後從通訊錄中選取 [&lt;組織名稱&gt;] 使用者或群組。

2.  按一下 ...，按一下 [設定權限]，然後選取 [&lt;組織名稱 - 機密&gt;]：

    ![](../media/AzRMS_OWATemplate.png)

3.  傳送訊息。

當 [收件者]、[副本] 或 [密件副本] 行的某人收到這封電子郵件時，他們可能會被要求先經過驗證才能讀取訊息，確認他們是來自 &lt;組織名稱&gt; 的使用者。 若使用者已經過驗證，則不會提示其驗證。

接收您傳送的電子郵件的人員都能夠將其轉寄給其他人，但只有來自 &lt;組織名稱&gt; 的使用者可以讀取它。 如果附加 Office 文件，會有相同的保護，即使該附件已使用不同的名稱儲存至另一個位置。 不過，成功驗證的使用者可以從電子郵件或附件複製和貼上，或從中進行列印。 如果您需要更嚴格的保護來防止此類動作，請連絡技術支援人員。

**需要協助嗎？**

-   連絡技術支援人員：

    -   *&lt;連絡人詳細資料&gt;*

### 自訂使用者文件的範例
![](../media/AzRMS_ExampleBanner.png)

#### 如何使用 Outlook 傳送包含公司機密資訊的電子郵件

1.  在 Outlook 中，建立新的電子郵件訊息，新增您想要包括的任何附件，然後從通訊錄選取 VanArsdel 使用者或群組。

2.  從 [選項] 索引標籤上按一下 [權限]，然後選取 [VanArsdel, Ltd - 機密]：

    ![](../media/AzRMS_OutlookTemplate.PNG)

3.  傳送訊息。

#### 如何使用 Outlook Web App 傳送包含公司機密資訊的電子郵件

1.  在 Outlook Web App 中，建立新的電子郵件訊息，新增您想要包括的任何附件，然後從通訊錄選取 VanArsdel 使用者或群組。

2.  按一下 ...，按一下 [設定權限]，然後選取 [VanArsdel, Ltd - 機密]：

    ![](../media/AzRMS_OWATemplate.png)

3.  傳送訊息。

當 [收件者]、[副本] 或 [密件副本] 行的某人收到這封電子郵件時，他們可能會被要求先經過驗證才能讀取訊息，確認他們是來自 VanArsdel, Ltd. 的使用者。 若使用者已經過驗證，則不會提示其驗證。

接收您傳送的電子郵件的人員都能夠將其轉寄給其他人，但只有來自 VanArsdel 的使用者可以讀取它。 如果附加 Office 文件，會有相同的保護，即使該附件已使用不同的名稱儲存至另一個位置。 不過，成功驗證的使用者可以從電子郵件或附件複製和貼上，或從中進行列印。 如果您需要更嚴格的保護來防止此類動作，請連絡技術支援人員。

**需要協助嗎？**

-   連絡技術支援人員：

    -   電子郵件：helpdesk@vanarsdelltd.com



<!--HONumber=Apr16_HO4-->


