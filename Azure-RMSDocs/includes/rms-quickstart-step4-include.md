![Azure RMS 快速入門步驟 4](../media/AzRMS_QuickStartSteps4.PNG)

收件者可以使用多種裝置來讀取您以電子郵件附件傳送的受保護文件。 這些裝置包括 iPad、iPhone、Android 平板電腦和手機、Mac 電腦以及 Windows 電腦。

請要求他們閱讀您傳送的電子郵件。 他們會看到您的電子郵件，不過在此之前會先看到下列文字：

**寄件者已使用 Microsoft RMS 保護附件。您必須** [登入](http://aka.ms/rms)
      **才能開啟附件。**

當他們按下連結時，連結會將他們帶往用來安裝 RMS 共用應用程式以及在必要時註冊免費帳戶的指示。 免費帳戶會授與他們個人版 RMS 訂閱，以確保獲得授權的使用者一律可以讀取受保護的文件，即使其組織沒有 Azure RMS。 然後，他們就可以使用下列指示讀取受保護的附件。

![RM 教學課程螢幕擷取畫面](../media/AzRMS_Tutorial_4_Screenshots.png)

#### 檢視受保護的文件附件

1.  因為 Azure Rights Management 保護了 Word 文件，所以電子郵件內有兩個附件。 這兩個附件實際上是相同檔案的兩個版本，只是它們的副檔名不同。 開啟具有 **.ppdf** 副檔名的版本 (**Confidential.ppdf**)。

    如果[您裝置上的 Office 版本支援 Rights Management](https://technet.microsoft.com/library/dn655136.aspx)，您就可以開啟此檔案的另一個版本 (**Confidential.docx**)，讓它在 Word 中開啟。

2.  如果系統提示您輸入使用者名稱和密碼，請輸入與您用來傳送電子郵件和附件的電子郵件地址格式相同的使用者名稱。 例如，**janetm@contoso.com** 或 **p.dover@fabrikam.com**。 至於密碼，請輸入您註冊個人版 RMS 時所提供的密碼。 或者，如果貴組織擁有 Azure RMS，請輸入您平常的工作密碼。

文件隨即開啟，您現在可以讀取其內容。 例如，內容可能是說：**如果您可以從電子郵件附件讀取這份文件，表示寄件者已成功共用以 Azure RMS 保護的檔案。** 因為是唯讀文件，您並無法變更其內容。

有一個選擇性步驟是，您可以要求收件者將電子郵件轉寄給不是原始電子郵件收件者的其他人。 即使這些人所服務的組織有 Azure Rights Management 或是他們本身申請自己的個人版 RMS 訂閱，他們還是無法開啟附件。 當系統提示他們輸入使用者名稱時，他們對於文件的存取便會遭到拒絕。

現在收件者已開啟附件並選擇性地將它轉寄給其他人，請期待您會收到報告此活動的電子郵件通知。 然而由於電子郵件很容易在經過一段時間後遺失，因此若要追蹤有誰存取過您的文件，比較好的方法是使用文件追蹤網站，最後一個步驟便是在講述這個方法。

|如果您想要更多的資訊|其他資訊|
|--------------------------------|--------------------------|
|用來檢視以 Azure Rights Management 保護之檔案的完整指示   →|[檢視並使用 Rights Management 保護的檔案](../rms-client/sharing-app-view-use-files.md)|
|關於免費的個人版 RMS 訂閱   →|[個人版 RMS 和 Azure Rights Management](../understand-explore/rms-for-individuals.md)|
|關於您看到的附加至電子郵件的兩個檔案版本   →|[自動建立的 .ppdf 檔案是什麼？](../rms-client/sharing-app-dialog-box.md)|



<!--HONumber=Jun16_HO4-->


