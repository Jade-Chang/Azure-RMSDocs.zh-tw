---
# required metadata

title: 案例 - 與其他組織的使用者共用 Office 檔案 | Azure RMS
description:
keywords:
author: cabailey
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: c10a4d7b-f57a-4a43-b66e-477777be59cc

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: esaggese
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# 案例 - 與其他組織的使用者共用 Office 檔案
此案例和支援的使用者文件會使用 Azure Rights Management，讓使用者可以與組織外的人安全地以電子郵件傳送 Office 檔案。 例如，Office 檔案可能是 Word 文件、Excel 試算表或 PowerPoint 簡報，其中包含合作夥伴的價目表資訊、經銷商的產品清單，或具有潛在客戶的傳遞時間明細行清單。 當使用者遵循指示時，附加到電子郵件訊息的檔案將受到 Azure Rights Management 的保護。

此案例適用於下列這組情況：

-   員工必須將資訊透過電子郵件以 Office 文件附件的形式傳送到組織外部。

-   文件包含非公用，但不是內部專用的資訊。

-   收件者使用者不需要進一步與其他人共用這項資訊、列印或使用做為自己文件的一部分。 如果不是這樣，您可以將僅檢視權限選取為允許收件者變更附件的另一個選項，來變更使用者指示。

-   員工可能有興趣了解此文件何時由外部使用者開啟。

## 部署指示
![](../media/AzRMS_AdminBanner.png)

繼續使用者文件之前，請確定符合下列需求。

## 此案例的需求
如果要讓使用者指示對這個案例運作，必須滿足下列條件：

|需求|如果需要更多資訊|
|---------------|--------------------------------|
|您已針對 Office 365 或 Azure Active Directory 準備帳戶和群組|[準備 Azure Rights Management](https://technet.microsoft.com/library/jj585029.aspx)|
|Azure Rights Management 已啟動|[啟用 Azure Rights Management](https://technet.microsoft.com/library/jj658941.aspx)|
|Rights Management 共用應用程式已部署至執行 Windows 的使用者電腦|[自動部署 Microsoft Rights Management 共用應用程式](https://technet.microsoft.com/library/dn339003%28v=ws.10%29.aspx)|
|使用者具有 Office 2013 的 Outlook|如果使用者有 Office 2010，請參閱對等版本的螢幕擷取畫面，讓圖片符合使用者看到的項目。|
|您的 Azure RMS 訂用帳戶包含文件追蹤|如果您的 Azure RMS 的訂用帳戶不包括文件追蹤和撤銷，使用者將無法完成使用者指示中的所有步驟。 在此情況下，購買確實支援這些功能的訂用帳戶，或修改使用者指示以移除使用這些功能的步驟。<br /><br />若要檢查您的訂用帳戶支援的項目： [Rights Management Services (RMS) 產品項目的比較](https://technet.microsoft.com/dn858608)|

## 使用者文件指示
使用下列範本，將使用者指示複製並貼到使用者通訊上，然後進行這些修改以反映您的環境 ︰

1.  將 &lt;Office 文件類型的名稱&gt; 取代為您的使用者傳送的文件類型。 使用特定且在他們的工作流程中熟悉的字詞，例如「價目表」、「傳遞時間」和「投標提案」，而不是「Word 文件」和「Excel 試算表」。 這些更明確的文字有助於增加他們使用這些文件時遵循指示的可能性。

2.  將 &lt;連絡人詳細資料&gt; 取代為您的使用者可以與技術支援人員連絡的指示，例如網站連結、電子郵件地址或電話號碼。

3.  **您可能想要進行的其他修改：**

    -   在步驟 2 中，我們建議檢視者 - 僅檢視權限，使收件者對附加的文件 (而非原始檔案) 有唯讀權限。 如果這項限制不適用於您的商務需求，將這個選項變更為另外一組權限，例如檢閱者 - 檢視和編輯。

    -   在步驟 3 中，我們建議 [ 允許我立即撤銷這些文件的存取權 ]，如果您的使用者稍後撤銷文件，就沒有延遲，但是設定這個選項需要收件者一定有網際網路連線來開啟附件。 這個步驟也必須要有支援文件追蹤和撤銷的訂用帳戶。 如果不適用於您的使用者，請刪除此步驟。

    -   在步驟 4 中，我們建議 [ 當有人嘗試開啟這些文件時以電子郵件通知我] 選項。 如果使用者使用文件追蹤入口網站來追蹤其文件，您可能會決定不需要電子郵件通知，並且刪除此步驟。

    -   這些步驟不包含設定到期日。 如果資訊在特定日期後便失去效用，則再加另一個步驟設定適當的到期時間，例如傳送電子郵件訊息之後的 90 天。

    > [!NOTE]
    > 如需使用者可以選取之每個選項的詳細資訊，請參閱＜ [適用於 Rights Management 共用應用程式的對話方塊選項](https://technet.microsoft.com/library/dn574738.aspx)＞

4.  對此指示集進行任何想要的修改，然後將它傳送給這些使用者。

範例文件會顯示這些指示在您的自訂之後，就使用者看來的可能外觀如何。

![](../media/AzRMS_UsersBanner.png)

### 如何共用 &lt;Office 文件類型名稱&gt;

1.  指定電子郵件地址來建立您的電子郵件，輸入您的訊息，並將 &lt;Office 文件類型名稱&gt; 附加至電子郵件訊息。 然後，在 [ 訊息 ] 索引標籤的 [ RMS ] 群組中按一下 [ 共用保護 ]，然後再按一下 [ 共用保護 ]：

    ![](../media/AzRMSUserInstructions_ShareProtectedRibbon2013.png)

2.  在 [ 共用保護 ] 對話方塊中，選取 [ 檢視者 - 僅檢視]：

    ![](../media/AzRMS_SharedProtected_ViewerOnly.PNG)

3.  選取 [ 允許我立即撤銷這些文件的存取權]：

    ![](../media/AzRMS_SharedProtected_InstantRevoke.PNG)

4.  選取 [ 當有人嘗試開啟這些文件時以電子郵件通知我]：

    ![](../media/AzRMS_SharedProtected_EmailMe.PNG)

5.  按一下 [立即傳送]。

當 [ 收件者]、[ 副本] 或 [ 密件副本 ] 行上的人員收到這封電子郵件時，他們會看到訊息，指示他們如何讀取附加的 &lt;Office 文件類型名稱&gt;。 他們可以在許多裝置上讀取文件，包括 iPad、iPhone、Android 平板電腦和電話、Mac 電腦，以及 Windows 電腦。

使用 [文件追蹤入口網站](https://track.azurerms.com/) 來追蹤是否以及何時開啟附加的 &lt;Office 文件類型名稱&gt;。 請考慮在您看到他們開啟 &lt;Office 文件類型名稱&gt; 之後，立即以後續追蹤電話聯絡他們。

**需要協助嗎？**

-   如需其他資訊：

    -   [保護您以電子郵件共用的檔案](https://technet.microsoft.com/library/dn574735%28v=ws.10%29.aspx)

    -   [追蹤及撤銷您的文件](https://technet.microsoft.com/library/dn986611.aspx)

-   連絡技術支援人員：

    -   *&lt;連絡人詳細資料&gt;*

### 自訂使用者文件的範例
![](../media/AzRMS_ExampleBanner.png)

#### 如何與您的客戶共用價目表

1.  指定客戶的電子郵件地址來建立您的電子郵件，輸入您的訊息，並將最新的價目表附加至電子郵件訊息。 然後，在 [ 訊息 ] 索引標籤的 [ RMS ] 群組中按一下 [ 共用保護 ]，然後再按一下 [ 共用保護 ]：

    ![](../media/AzRMSUserInstructions_ShareProtectedRibbon2013.png)

2.  在 [ 共用保護 ] 對話方塊中，選取 [ 檢視者 - 僅檢視]：

    ![](../media/AzRMS_SharedProtected_ViewerOnly.PNG)

3.  選取 [ 允許我立即撤銷這些文件的存取權]：

    ![](../media/AzRMS_SharedProtected_InstantRevoke.PNG)

4.  選取 [ 當有人嘗試開啟這些文件時以電子郵件通知我]：

    ![](../media/AzRMS_SharedProtected_EmailMe.PNG)

5.  按一下 [立即傳送]。

當 [ 收件者]、[ 副本] 或 [ 密件副本 ] 行上的人員收到這封電子郵件時，他們會看到訊息，指示他們如何讀取附加的價目表。 他們可以在許多裝置上讀取文件，包括 iPad、iPhone、Android 平板電腦和電話、Mac 電腦，以及 Windows 電腦。

使用 [文件追蹤入口網站](https://track.azurerms.com/) 來追蹤是否以及何時開啟附加的價目表。 請考慮在您看到他們開啟價目表之後，立即以後續追蹤電話聯絡他們。

**需要協助嗎？**

-   如需其他資訊：

    -   [保護您以電子郵件共用的檔案](https://technet.microsoft.com/library/dn574735%28v=ws.10%29.aspx)

    -   [追蹤及撤銷您的文件](https://technet.microsoft.com/library/dn986611.aspx)

-   連絡技術支援人員：

    -   電子郵件：helpdesk@vanarsdelltd.com



<!--HONumber=Apr16_HO4-->


