---
title: "快速入門教學課程步驟 5 | Azure Information Protection"
description: "簡介教學課程的步驟 5，可讓貴組織快速試用 Microsoft Azure Information Protection，需時約 30 分鐘。"
keywords: 
author: cabailey
manager: mbaldwin
ms.date: 09/25/2016
ms.topic: get-started-article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 4e59a3b3-f0f4-4535-8b96-cac68303d855
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 1af9f3b3451bf8ceafbaf3cddd2b26c37fe9d597
ms.openlocfilehash: d607c19d37da6b6fb23513067e9e30f33f0260de


---


# 步驟 5︰了解受保護的檔案如何共用以及追蹤文件 

>*適用於：Azure Information Protection*

在本教學課程的最後一個步驟中，找出您已建立且會傳送給夥伴或同事的 Word 文件。 在本教學課程中，這份文件實際包含什麼文字並不重要，但您勢必會想讓它包含一些文字，以便可以更輕鬆地確認獲得授權的收件者可以讀取此文件。

接著，您就可以安全地透過電子郵件共用這份文件。 

## 安全地透過電子郵件共用文件

1.  在 Word 中開啟文件。 您會看到再次自動套用預設標籤**內部**。 

2.  在 [首頁] 索引標籤的 [RMS] 群組中，按一下 [共用保護的檔案]，然後按一下功能表的 [共用保護的檔案]：

    ![Azure Information Protection 快速入門教學課程步驟 5 - 共用保護的檔案](../media/share-protected-callout.png)

    您會看到 [共用保護的檔案] 對話方塊，類似此圖片︰

    ![Azure Information Protection 快速入門教學課程步驟 5 - 共用保護的對話方塊](../media/example-share-protected-dialog.png)

3. 在 [使用者] 方塊中輸入一或多個商業電子郵件地址，就和您傳送文件給與您的組織有業務往來的人一樣。 或者，您可以指定同事的電子郵件地址。 請確定您指定的是公司電子郵件地址，例如 **janetm@contoso.com** 或 **p.dover@fabrikam.com**，因為 Azure Information Protection 不支援個人電子郵件地址。 

    別擔心文件的收件者有沒有 Azure Information Protectin。

4. 選取 **[檢閱者 - 僅檢視]**。

    這表示我們的收件者將能夠檢視文件，但不能進行編輯或列印。

5. 選取 **[有人嘗試開啟這些文件時傳送電子郵件給我]**。

    每當收件者嘗試開啟附件以及有其他人嘗試開啟時，例如收件者將電子郵件轉寄給同事，您就會收到電子郵件通知。 如果是轉寄的文件，您會看到存取遭到拒絕，而且您可以從使用者詳細資料來決定是否要傳送一份文件給該名人員，以便其能夠開啟。

6. 選取 **[允許我立即撤銷這些文件的存取權]**。

    若選取這個選項，收件者每次開啟附件時都必須要有網際網路連線，但好處是如果您稍後撤銷文件，收件者下次嘗試開啟附件時，將不會成功。 

4.  按一下 [傳送] 查看有預設指示文字，隨時可傳送給指定收件者的電子郵件訊息。 例如：

    ![共用保護的檔案時的範例電子郵件訊息](../media/example-email-share-protected.png)
    
    **注意**︰安裝 Azure Information Protection 用戶端時，Outlook 如已開啟，就看不到上圖顯示的 Information Protection 列︰示範共用受保護文件的這個步驟不會特別使用它，因此完成本教學課程不必關閉再重新開啟 Outlook。 安裝 Azure Information Protection 用戶端之後如已開啟 Outlook，您會看到此電子郵件訊息，像第一次開啟 Word 文件那樣，預設套用了 [內部] 標籤，這是 Azure Information Protection 原則設定此通用設定的結果。
    
    您可能會注意到有兩份附件，原有的 Word 文件，以及同名但副檔名為 **.ppdf** 的檔案。 .ppdf 版本是受保護的 PDF 檔案，由 Rights Management 共用應用程式自動建立，以免收件者沒有支援受保護文件的 Office 版本。 此額外的檔案可讓收件者使用隨 Rights Management 共用應用程式一起安裝的檢視器，讀取受保護的文件。

    按一下電子郵件訊息的 [傳送]。

現在您已送出受保護的文件，因此您可以要求收件者等候其送達，然後將其開啟。 但請不要關閉 Word，因為最後一個步驟會再次用它來追蹤共用的文件。

## 要求收件者開啟以電子郵件送達的文件

收件者可以使用多種裝置來讀取您以電子郵件附件傳送的受保護文件。 這些裝置包括 iPad、iPhone、Android 平板電腦和手機、Mac 電腦以及 Windows 電腦。

請要求他們閱讀您傳送的電子郵件。 假設這是他們第一次收到 Rights Management 保護的附件，請他們按一下 [說明] 連結。 他們會看到 [Welcome to Microsoft RMS!](https://portal.azurerms.com/#/rmshelp) (歡迎使用 Microsoft RMS！) 頁面及 RMS 共用應用程式的安裝指示，如有必要請註冊免費帳戶。 然後他們就可以讀取受保護的附件。

### 收件者指示：檢視受保護的文件附件

1. 開啟其中一份附件來讀取文件︰
    
    - 如果裝置上有支援 Rights Management 的 Office 版本：
    
        -  開啟副檔名為 **.docx** 的文件。
        
    - 如果沒有支援 Rights Management 的 Office 版本或不確定，或只是要嘗試 Rights Management 共用應用程式的檢視器︰ 
    
        - 開啟副檔名為 **.ppdf** 的文件。

2.  如果系統提示您輸入使用者名稱和密碼，請輸入與您用來傳送電子郵件和附件的電子郵件地址格式相同的使用者名稱。 例如，janetm@contoso.com 或 p.dover@fabrikam.com。 至於密碼，請輸入您註冊個人版 RMS 時所提供的密碼。 或者，貴組織若使用 Office 365 等雲端服務或使用 Azure，請輸入您平常工作的密碼。

3. 在文件開啟時閱讀取其內容。 因為是唯讀文件，您並無法變更其內容。

有一個選擇性步驟是，收件者可以將電子郵件轉寄給不是原始電子郵件指定收件者的其他人。 這些人無法開啟附件。 當系統提示他們輸入使用者名稱時，他們對於文件的存取便會遭到拒絕。

現在收件者已開啟附件並選擇性地將它轉寄給其他人，請期待您會收到報告此活動的電子郵件通知。 然而由於電子郵件很容易在經過一段時間後遺失，因此若要追蹤有誰存取過您的文件，比較好的方法是使用文件追蹤網站，最後一道程序便是在講述這個方法。

## 追蹤受保護的文件

1.  回到 Word，在 [首頁] 索引標籤的 [RMS] 群組中，按一下 [共用保護的檔案]，然後按一下功能表的 [追蹤使用情況]：

    ![[追蹤使用情況] 選項](../media/track-usage-callout.png)

    這會帶您前往文件追蹤網站。

2.  如果您看到 [Protect and share on your terms (由您保護和共用)] 頁面，請按一下 [登入] 並再次提供您的使用者名稱和密碼。

3.  在 [Your shared documents] (您共用的文件) 頁面上，您會看到您共用的文件名稱。 此時只有顯示這個檔案，若您共用其他受保護的文件，清單將會增加。

    在這個頁面中，您會看到文件的共用時間 (您何時傳送有受保護附加的電子郵件)、最後一次活動的日期，以及電子郵件寄送到的目標收件者的名稱。 按一下文件名稱以獲得其他詳細資料。

4.  在有您所點按之檔案名稱的新網頁上，您只會看到該文件的摘要詳細資料，以及該文件可用的其他選項清單 ([清單]、[時間表]、[對應]、[設定])。

    按一下每個選項來瀏覽受保護文件的不同追蹤方式。 或是留在 [摘要] 頁面上，按一下 [在 Excel 中開啟] 將資訊匯出到試算表，或按一下 [撤銷存取權] 停止共用文件。

有必要時，您就可以回到這個網站來進一步追蹤受保護文件的活動，或撤銷其存取權。 您甚至可以從您的行動裝置或平板電腦的瀏覽器使用下列連結存取這個網站：[文件追蹤](http://go.microsoft.com/fwlink/?LinkId=529562)



|如果您想要更多的資訊|其他資訊|
|--------------------------------|--------------------------|
|保護透過電子郵件共用之檔案的完整指示和其他方法|[藉由使用 Rights Management 共用應用程式，保護您透過電子郵件共用的檔案](../rms-client/sharing-app-protect-by-email.md)|
|關於 [共用保護] 對話方塊中的選項|[Rights Management 共用應用程式的對話方塊選項](../rms-client/sharing-app-dialog-box.md)|
|有關供其他使用者註冊的免費帳戶|[個人版 RMS 和 Azure Rights Management](../understand-explore/rms-for-individuals.md)|
|有關使用文件追蹤網站|[追蹤及撤銷您的文件](../rms-client/sharing-app-track-revoke.md)


## 後續步驟

現在您已了解預設 Azure Information Protection 原則及其自訂方法，也了解 Word 文件的標記如何運作，請嘗試一些其他設定，看看它們如何在支援 Azure Information Protection 的其他 Office 應用程式中運作︰Excel、PowerPoint 及 Outlook。 如果在安裝 Azure Information Protection 用戶端時，這些應用程式已開啟，請關閉並重新開啟它們，然後再嘗試使用 Azure Information Protection。

嘗試共用更多文件並追蹤其使用方式，確認撤銷文件的運作方式。

您也許會發現閱讀 Azure Information Protection 的[常見問題集](faqs.md)，以及探索一些其他的文件文章很有用。 但若已準備開始部署貴組織的 Azure Information Protection，下一步應該是 [Azure Rights Management 部署藍圖](../plan-design/deployment-roadmap.md)。 


<!--HONumber=Sep16_HO4-->


