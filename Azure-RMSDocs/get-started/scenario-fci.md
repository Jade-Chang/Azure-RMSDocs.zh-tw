---
title: "案例 - 保護檔案伺服器共用上的檔案 | Azure RMS"
description: 
keywords: 
author: cabailey
manager: mbaldwin
ms.date: 05/20/2016
ms.topic: get-started-article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 283c7db3-5730-439e-a215-40a1088ed506
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 332e102cb27854314b93a71bfeae82a95c9a7812
ms.openlocfilehash: c16098a2d0fe41748280704716a2eeef8921a6fa


---

# 案例 - 保護檔案伺服器共用上的檔案

*適用於︰Azure Rights Management、Office 365*

此案例和支援使用者文件會使用 Azure Rights Management 來大量保護您想要在檔案伺服器上保護的所有檔案，以確保只有貴組織的員工都可以存取它們，即使檔案被複製並儲存到不在您的 IT 部門的控制下的儲存體，或以電子郵件傳送檔案給其他人。

這些指示會使用其中一個預設範本，它會對具有所有使用權限的所有員工限制存取。 但如有需要，您可以藉由設定自訂的範本，而不是使用預設範本，進一步限制存取和使用權限。

指示適用於下列一組情況：

-   您要保護所有檔案類型而不只是 Office 檔案。 無法由 Azure RMS 原生保護的檔案會以一般方式保護。

-   指定的路徑 (包括子資料夾) 中的所有檔案會受到保護。

-   所有檔案都會依排程重新保護，以確保對權限原則範本的任何變更會套用至受保護的檔案。

## 部署指示
![Azure RMS 快速部署的系統管理員指示](../media/AzRMS_AdminBanner.png)

請確定符合下列需求，然後依照支援程序的指示，再繼續進行使用者文件。

## 此案例的需求
此案例的指示要能運作，必須滿足下列條件：

|需求|如果需要更多資訊|
|---------------|--------------------------------|
|Azure Rights Management 已啟動|[啟用 Azure Rights Management](https://technet.microsoft.com/library/jj658941.aspx)|
|您已同步處理您的內部部署 Active Directory 使用者帳戶與 Azure Active Directory 或 Office 365，包括其電子郵件地址。 所有使用者都需要此項，才能存取受到 FCI 和 Azure Rights Management 保護的檔案。|[準備 Azure Rights Management](https://technet.microsoft.com/library/jj585029.aspx)|
|發生下列情形之一：<br /><br />- 若要對所有使用者使用預設範本︰您尚未封存預設的 [&lt;組織名稱&gt; - 機密]<br /><br />- 若要對特定使用者使用自訂範本︰您已建立並發佈此自訂範本|[設定 Azure Rights Management 的自訂範本](https://technet.microsoft.com/library/dn642472.aspx)|
|Rights Management 共用應用程式已部署至執行 Windows 的使用者電腦|[自動部署 Microsoft Rights Management 共用應用程式](https://technet.microsoft.com/library/dn339003%28v=ws.10%29.aspx)|
|您已下載 RMS 保護工具，並設定 Azure RMS 的必要條件|如需相關下載工具和必要條件的指示︰[RMS 保護 Cmdlet](https://msdn.microsoft.com/library/mt433195.aspx)<br /><br />若要設定 Azure RMS 的其他先決條件，例如服務主體帳戶︰[about_RMSProtection_AzureRMS](https://msdn.microsoft.com/library/mt433202.aspx)|

### 使用 Azure RMS 與具有檔案分類基礎結構的檔案伺服器資源管理員來設定檔案伺服器，以保護所有檔案

1.  啟動 Windows PowerShell 工作階段。 您不需以系統管理員身分執行此工作階段。

2.  向 Azure RMS 進行驗證︰

    ```
    Set-RMSServerAuthentication
    ```
    出現提示時，提供您為 RMS 保護 Cmdlet 的必要元件所建立的服務主體帳戶值。

3.  執行下列命令來識別將用來保護檔案的範本識別碼︰

    ```
    Get-RMSTemplate
    ```
    若要使用會對具有所有使用權限之所有員工限制存取的預設範本，請尋找範本名稱 [**&lt;組織名稱&gt; - 機密**]。 例如，**VanArsdel, Ltd - 機密**。

4.  請遵循[具有 Windows Server 檔案分類基礎結構 (FCI) 的 RMS 保護](https://technet.microsoft.com/library/mt601315%28v=ws.10%29.aspx)中的逐步指示。

    這些指示包含一個 Windows PowerShell 指令碼，您會指定在檔案伺服器資源管理員中以自訂可執行檔形式執行。 指示中也包含如何驗證這些檔案受到 Azure Rights Management 保護。

## 使用者文件指示
如果您要保護的檔案僅僅是 Office 檔案，則可能不需為使用者提供受保護檔案的任何指示。 當授權的使用者開啟這些文件時，他們會如往常般在 Office 中開啟，唯一的差別在於可能會提示使用者進行驗證，而他們可能會在文件頂端看到資訊列，通知他們該文件已受到保護。

如果受保護的檔案有 **.ppdf** 副檔名，或者它們是受保護的文字或影像檔 (例如，有 **.ptxt** 或 **.pjpg** 副檔名)，這些檔案現在會是唯讀而無法編輯。 使用者可以使用會自動載入這些檔案類型的 RMS 共用應用程式檢視器來檢視它們。 這些檔案會原生受 Azure RMS 保護，並從您設定的範本套用所有的原則設定 (除了使用權限以外)，因為檔案本身為唯讀。 除非您知道您將會保護這些檔案類型，在此案例下，您可能不太需要使用者指示，但請提醒技術支援人員，他們可能需要向使用者說明為什麼無法編輯這些檔案。

如果受保護的檔案有 **.pfile** 副檔名，使用者可以檢視這些檔案，但如果使用者想要編輯並儲存變更，檔案必須以其原始的檔案名稱儲存 (移除 .pfile 副檔名)。 這些檔案一般會受 Azure RMS 保護，並且無法從您套用的範本強制執行使用權限，這表示如果使用新名稱儲存檔案，會失去保護。 此案例需要使用者的指示。

使用下列範本，將使用者指示複製並貼上，使他們知道如何編輯一般受保護的檔案。 進行這些修改，以反映您的環境︰

-   以一般會受到保護的檔案類型和檔案伺服器共用的名稱來取代 *&lt;檔案類型&gt;* 和 *&lt;檔案伺服器共用&gt;*。

-   以您的組織名稱取代 *&lt;組織名稱&gt;*，因為它會顯示在您的預設 Azure Rights Management 範本上。

-   以您的組織名稱取代 *&lt;組織名稱&gt;*。

-   以這個檔案類型的特定應用程式指示取代 *&lt;指示如何儲存檔案及移除 .pfile 副檔名&gt;*。

-   將連絡人詳細資料取代為您的使用者可以與技術支援人員連絡的指示，例如網站連結、電子郵件地址或電話號碼。

-   對此指示集進行任何其他修改，然後將它傳送給這些使用者。

範例文件會顯示這些指示在您的自訂之後，就使用者看來的可能外觀如何。

![Azure RMS 快速部署的範本使用者文件](../media/AzRMS_UsersBanner.png)

### 如何從 &lt;檔案伺服器共用編輯 &lt;檔案類型&gt;&gt;

1.  按兩下檔案將其開啟。 系統不會提示您提供認證。

2.  您會看到來自 Microsoft Rights Management 共用應用程式的 **[受保護的檔案]** 對話方塊，它會告訴您，您應遵守 **&lt;組織名稱&gt; - 機密**的權限。 這表示，若他人未替 &lt;組織名稱&gt; 工作，請勿與其共用此文件。

3.  按一下 [開啟]。

4.  若要編輯檔案，請先儲存檔案，然後移除 .pfile 副檔名︰

    -   &lt;指示如何儲存檔案及移除 .pfile 副檔名&gt;

5.  您現在可以像往常一樣編輯然後儲存檔案。

將定期重新保護檔案，這樣會再次加入 .pfile 副檔名，而您必須重複這些步驟。

**需要協助嗎？**

-   如需其他資訊：

    -   [檢視及使用受保護的檔案](https://technet.microsoft.com/library/dn574741%28v=ws.10%29)

-   連絡技術支援人員：

    -   *&lt;連絡人詳細資料&gt;*

### 自訂使用者文件的範例
![Azure RMS 快速部署的範例使用者文件](../media/AzRMS_ExampleBanner.png)

#### 如何從 ProjectNextGen 共用編輯 CAD 繪圖

1.  按兩下檔案將其開啟。 系統不會提示您提供認證。

2.  您會看到來自 Microsoft Rights Management 共用應用程式的 [受保護的檔案] 對話方塊，它會告訴您，您應遵守 **VanArsdel, Ltd - 機密**的權限。 這表示，若他人未替 VanArsdel, Ltd 工作，請勿與其共用此文件。

3.  按一下 [開啟]。

4.  若要編輯檔案，請先儲存檔案，然後移除 .pfile 副檔名︰

    -   **[檔案]** &gt; **[另存新檔]**

    -   從檔案名稱結尾刪除 **.pfile**，然後按一下 [確定]。

5.  您現在可以像往常一樣編輯然後儲存檔案。

將定期重新保護檔案，這樣會再次加入 .pfile 副檔名，而您必須重複這些步驟。

**需要協助嗎？**

-   如需其他資訊：

    -   [檢視及使用受保護的檔案](https://technet.microsoft.com/library/dn574741%28v=ws.10%29)

-   請連絡技術支援人員：helpdesk@vanarsdelltd.com




<!--HONumber=Jun16_HO4-->


