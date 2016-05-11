---
# required metadata

title: Azure RMS 快速入門教學課程 - 步驟 3 | Azure RMS
description: 教學課程的第三步，可為組織快速試用 Microsoft Azure Rights Management，只有 5 個步驟，花費時間不超過 15 分鐘。
keywords:
author: Cabailey
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: get-started-article
ms.prod: azure
ms.service: rights-management
ms.assetid: c604e749-8918-40e8-8148-6bd000cb2be2

# optional metadata

ROBOTS: 
audience:
ms.devlang:
ms.reviewer: esaggese
ms.suite: ems
ms.tgt_pltfrm:
ms.technology:
ms.custom:

---


# Azure RMS 快速入門步驟 3：以電子郵件傳送您想要保護的文件

跳至︰ 
> [!div class="op_single_selector"]
- [簡介](quick-start-tutorial.md)
- [步驟 1︰啟用 Azure RMS](tutorial-step1.md)
- [步驟 2︰安裝 RMS 共用應用程式](tutorial-step2.md)
- [步驟 3︰傳送機密文件電子郵件](tutorial-step3.md)
- [步驟 4︰收件者讀取文件](tutorial-step4.md)
- [步驟 5︰追蹤您的文件](tutorial-step5.md)


在此步驟中，請先使用 Word 建立並儲存一份文件來代表您想要保護的文件，並將它命名為 Confidential.docx。 在本教學課程中，這份文件實際包含什麼文字並不重要，但您勢必會想讓它包含一些文字，以便可以更輕鬆地確認獲得授權的收件者可以讀取此文件。 例如，您可以輸入： 如果您可以從電子郵件附件讀取這份文件，表示寄件者已成功共用以 Azure RMS 保護的檔案。

接著，您就可以安全地透過電子郵件共用這份文件。

![](../media/AzRMS_Tutorial_3_Screenshots.png)

### 安全地透過電子郵件共用文件

1.  使用 Outlook 建立新的郵件，並附加您剛才建立的檔案。

2.  在 [收件者] 方塊中，輸入一或多個公司電子郵件地址。 請確定您指定的是公司電子郵件地址，例如 janetm@contoso.com 或 p.dover@fabrikam.com，因為 Azure Rights Management 目前並不支援您可能會在家裡使用的網際網路提供者所提供的個人電子郵件地址。 別擔心文件的收件者是否也有 Azure Rights Management。

3.  輸入主旨，例如  機密文件 ，然後在電子郵件中輸入簡短訊息，例如 請閱讀這份機密文件，並請勿與他人共用。

4.  然後，在 [訊息] 索引標籤的 [RMS] 群組中，按一下 [共用保護] ，接著再按一下 [共用保護] ：

5.  在 [共用保護] 對話方塊中：

    1.  選取 [檢閱者 - 僅檢視]。

        這表示我們的收件者將能夠檢視文件，但不能進行編輯或列印。

    2.  選取 [有人嘗試開啟這些文件時傳送電子郵件給我]。

        每當收件者嘗試開啟附件以及有其他人嘗試開啟時，例如收件者將電子郵件轉寄給同事，您就會收到電子郵件通知。 在最後一個案例中，您會看到存取遭到拒絕，而且您可以從使用者詳細資料來決定是否要傳送一份文件給該名人員，以便他能夠開啟。

    3.  選取 [允許我立即撤銷這些文件的存取權]。

        若選取這個選項，收件者每次開啟附件時都必須要有網際網路連線，但好處是如果您稍後撤銷文件，收件者下次嘗試開啟附件時，將不會成功。 如果您沒有選取這個選項，收件者即使沒有網際網路連線也可能可以開啟附件，但壞處是如果您稍後撤銷文件，其效果可能會延遲發生。

    4.  按一下 [立即傳送]。

        帶有附件的電子郵件就會傳送至您指定的電子郵件地址。 除了您寄送的電子郵件外，收件者還會看到相關指示，這些指示會說明如何讀取 Azure Rights Management 所保護的附加文件。

現在您已送出受保護的文件，因此您可以要求收件者等候其送達，然後將其開啟。 但請不要關閉 Outlook，因為我們會在最後一個步驟中再次用到它來追蹤附件。

|如果您想要更多的資訊|其他資訊|
|--------------------------------|--------------------------|
|保護透過電子郵件共用之檔案的完整指示和其他方法|[藉由使用 Rights Management 共用應用程式，保護您透過電子郵件共用的檔案](../rms-client/sharing-app-protect-by-email.md)|
|關於 [共用保護] 對話方塊中的選項|[Rights Management 共用應用程式的對話方塊選項](../rms-client/sharing-app-dialog-box.md)|


>[!div class="step-by-step"]
[« 步驟 2](tutorial-step2.md)
[步驟 4 »](tutorial-step4.md)

<!--HONumber=Apr16_HO3-->


