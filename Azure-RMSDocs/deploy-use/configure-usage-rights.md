---
# required metadata

title: 設定 Azure Rights Management 的使用權限 | Azure RMS
description:
keywords:
author: cabailey
manager: mbaldwin
ms.date: 06/08/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 97ddde38-b91b-42a5-8eb4-3ce6ce15393d

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: esaggese
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# 設定 Azure Rights Management 的使用權限

*適用於︰Azure Rights Management、Office 365*

當您使用 Azure Rights Management (Azure RMS) 在檔案或電子郵件上設定保護，且沒有使用範本時，您必須自行設定使用權限。 此外，當您為 Azure RMS 設定自訂範本時，您會選取使用權限，而當使用者、系統管理員或設定的服務選取範本時，自動套用會您選取的使用權限。 例如，在 Azure 傳統入口網站，您可以選取角色來設定使用權限的邏輯群組，也可以設定個別權限。

使用本文來協助您設定您使用的應用程式所需的使用權限，並了解應用程式如何解讀這些權限。

## 使用權限和描述
下列章節列出並描述 Rights Management 支援的使用權限，以及如何使用和解讀這些權限。 它們會按**一般名稱**列出，通常是您可能看到某處顯示或提及的使用權限，比程式碼中使用的單一字詞值 (**原則中的編碼**值) 更易於了解。 **API 常數或值**是 MSIPC API 呼叫的 SDK 名稱，當您撰寫啟用 RMS 的應用程式來檢查使用權限或將使用權限加入至原則時會用到。


### 編輯內容，編輯

允許使用者修改、重新排列、格式化或篩選應用程式內的內容。 不授與權限來儲存編輯過的複本。

**原則中的編碼**：DOCEDIT

**Office 自訂權限中的實作**︰為 [變更] 和 [完全控制] 選項的一部分。

**Azure 傳統入口網站中的名稱**：[編輯內容]

**AD RMS 範本中的名稱**：[編輯]

**API 常數或值**：[不適用]

---

### 儲存

可讓使用者將文件儲存在目前的位置。

**原則中的編碼**：EDIT

**Office 自訂權限中的實作**︰為 [變更] 和 [完全控制] 選項的一部分。

**Azure 傳統入口網站中的名稱**：[儲存檔案]

**AD RMS 範本中的名稱**：[儲存]

**API 常數或值**：IPC_GENERIC_WRITEL"EDIT"

在 Office 應用程式中，這個權限也允許使用者修改文件。

---

### 註解

啟用這個選項可將註解或意見加入至內容。

**原則中的編碼**：COMMENT

**Office 自訂權限中的實作**：未實作。

**Azure 傳統入口網站中的名稱**：未實作。

**AD RMS 範本中的名稱**：未實作。

**API 常數或值**：IPC_GENERIC_COMMENTL"COMMENT

此權限可在 SDK 中使用、在 Windows PowerShell 的 RMS 保護模組中可作為特定原則使用，而且在某些軟體廠商應用程式中已實作。 不過，尚未廣泛使用，Office 應用程式目前也不支援。

---

### 另存新檔，匯出

啟用這個選項可將內容儲存為不同的檔案名稱 (另存新檔)。 對於 Office 文件，檔案會以未受保護的方式進行儲存。

**原則中的編碼：**EXPORT

**Office 自訂權限中的實作：**為 [變更] 和 [完全控制] 選項的一部分。

**Azure 傳統入口網站中的名稱：**[匯出內容 (另存新檔)]

**AD RMS 範本中的名稱：**[匯出 (另存新檔)]

**API 常數或值：**IPC_GENERIC_EXPORTL"EXPORT"

這個權限也允許使用者在應用程式中執行其他匯出選項，例如 [傳送到 OneNote]。

---

### 轉寄

啟用這個選項可轉寄電子郵件訊息和將收件者新增到 [收件者] 和 [副本] 行。 此權限未套用至文件；僅電子郵件訊息。

**原則中的編碼：**FORWARD

**Office 自訂權限中的實作：**使用 [不要轉寄] 標準原則時拒絕。

**Azure 傳統入口網站中的名稱：**[轉寄]

**AD RMS 範本中的名稱：**[轉寄]

**API 常數或值：** IPC_EMAIL_FORWARDL"FORWARD"

不允許轉寄者在轉寄動作中授與權限給其他使用者。

---

### 完全控制

授與文件的所有權限，可以執行所有可用的動作。

**原則中的編碼：**OWNER

**Office 自訂權限中的實作：**作為 [完全控制] 自訂選項。

**Azure 傳統入口網站中的名稱：**[完全控制]

**AD RMS 範本中的名稱：**[完全控制]

**API 常數或值：**IPC_GENERIC_ALLL"OWNER"

包括能夠移除保護。

---

### Print

啟用列印內容的選項。

**原則中的編碼：**PRINT

**Office 自訂權限中的實作：**作為自訂權限中的 [列印內容] 選項。 不是個別收件者設定。

**Azure 傳統入口網站中的名稱：**[列印]

**AD RMS 範本中的名稱：**[列印]

**API 常數或值：**IPC_GENERIC_PRINTL"PRINT

---

### 回覆

在電子郵件用戶端中啟用 [回覆] 選項，不允許變更 [收件者] 或 [副本] 行。

**原則中的編碼：**REPLY

**Office 自訂權限中的實作：**：不適用

**Azure 傳統入口網站中的名稱：**[回覆]

**AD RMS 範本中的名稱：**[回覆]

**API 常數或值：**IPC_EMAIL_REPLY

---

### 全部回覆

在電子郵件用戶端中啟用 [全部回覆] 選項，但不允許使用者將收件者新增至 [收件者] 或 [副本] 行。

**原則中的編碼：**REPLYALL

**Office 自訂權限中的實作：**：不適用

**Azure 傳統入口網站中的名稱：**[全部回覆]

**AD RMS 範本中的名稱：**[全部回覆]

**API 常數或值：**IPC_EMAIL_REPLYALLL"REPLYALL"

---

### 檢視，開啟，讀取

可讓使用者開啟文件並看見內容。

**原則中的編碼：**VIEW

**Office 自訂權限中的實作：**作為 [讀取] 自訂原則、[檢視] 選項。

**Azure 傳統入口網站中的名稱：**[檢視內容]

**AD RMS 範本中的名稱：**[檢視]

**API 常數或值：**IPC_GENERIC_READL"VIEW"

---

### 複製

啟用將文件中的資料 (包括螢幕擷取畫面) 複製到相同或不同文件的選項。

**原則中的編碼：**EXTRACT

**Office 自訂權限中的實作：**作為 *[允許具有讀取存取權的使用者複製內容]* 自訂原則選項。

**Azure 傳統入口網站中的名稱：***複製並擷取內容*

**AD RMS 範本中的名稱：***擷取*

**API 常數或值：**IPC_GENERIC_EXTRACTL"EXTRACT"

在某些應用程式中，這也允許以未受保護的形式儲存整份文件。

---


### 允許巨集

啟用這個選項可對文件中的內容執行巨集，或對執行其他程式設計或遠端存取。

**原則中的編碼：**OBJMODEL

**Office 自訂權限中的實作：**作為 [允許程式設計存取] 自訂原則選項。 不是個別收件者設定。

**Azure 傳統入口網站中的名稱：**[允許巨集]

**AD RMS 範本中的名稱：**[允許巨集]

**API 常數或值：**不適用


## 權限層級中包含的權限

有些應用程式群組使用權限會組成權限層級，以便選取通常一起使用的使用權限。 這些權限層級有助於為使用者釐清複雜的權限，以便他們選擇以角色為基礎的選項。  例如，[檢閱者] 和 [共同作者]。 雖然這些選項通常會對使用者顯示權限的摘要，但可能不包括上表所列的每個權限。

使用下表來取得這些權限層級的清單以及它們所含權限的完整清單。

|權限層級|應用程式|包含的權限 (一般名稱)|
|---------------------|----------------|---------------------------------|
|檢視者|Azure 傳統入口網站<br /><br />適用於 Windows 的 Rights Management 共用應用程式|檢視，開啟，讀取；回覆；全部回覆|
|檢閱者|Azure 傳統入口網站<br /><br />適用於 Windows 的 Rights Management 共用應用程式|檢視，開啟，讀取；儲存；編輯內容，編輯；回覆 [[1]](#footnote-1)；全部回覆 [[1]](#footnote-1)；轉寄 [[1]](#footnote-1)|
|共同作者|Azure 傳統入口網站<br /><br />適用於 Windows 的 Rights Management 共用應用程式|檢視，開啟，讀取；儲存；編輯內容，編輯；複製；檢視權限；變更權限；允許巨集；另存新檔，匯出；列印；回覆 [[1]](#footnote-1)；全部回覆 [[1]](#footnote-1)；轉寄 [[1]](#footnote-1)|
|共同擁有者|Azure 傳統入口網站<br /><br />適用於 Windows 的 Rights Management 共用應用程式|檢視，開啟，讀取；儲存；編輯內容，編輯；複製；檢視權限；變更權限；允許巨集；另存新檔，匯出；列印；回覆 [[1]](#footnote-1)；全部回覆 [[1]](#footnote-1)；轉寄 [[1]](#footnote-1)；完全控制|

----

###### 註腳 1
不適用於 Windows 的 Rights Management 共用應用程式。

## 預設範本中包含的權限
預設範本中包含的權限如下所示：

|顯示名稱|包含的權限 (一般名稱)|
|----------------|---------------------------------|
|&lt;*組織名稱*&gt; *- 僅限機密檢視*|檢視，開啟，讀取|
|&lt;*組織名稱*&gt; *- 機密*|檢視，開啟，讀取；儲存；編輯內容，編輯；檢視權限；允許巨集；轉寄；回覆；全部回覆|

## 電子郵件的 [不要轉寄] 選項

Exchange 用戶端及服務 (例如 Outlook 用戶端、Outlook Web Access 應用程式及 Exchange 傳輸規則) 有一個額外的電子郵件資訊版權保護選項︰**[不要轉寄]**。 

雖然此選項在使用者 (Exchange 管理員) 看來像是可供選取的預設 Rights Management 範本，但 **[不要轉寄]** 不是範本。 這就是為什麼您在檢視及管理 Azure RMS 的範本時，不會在 Azure 傳統入口網站中看到此選項。 **[不要轉寄]** 其實是使用者會自動套用到電子郵件收件者的一組權限。

當 **[不要轉寄]** 選項套用到電子郵件時，收件者無法加以轉寄、列印、複製、或儲存其附件或另存為其他名稱。 例如在 Outlook 用戶端中，無法使用 [轉寄] 按鈕以及 **[另存新檔]**、**[儲存附件]** 及 **[列印]** 功能表選項，您也無法新增或變更 **[收件者]**、**[副本]** 或 **[密件副本]** 方塊中的收件者。

套用 **[不要轉寄]** 選項與套用不授與電子郵件 [轉寄] 權限的範本，兩者之間有重要的差異︰**[不要轉寄]** 選項根據使用者在原始電子郵件中選擇的收件者，使用授權使用者動態清單；而範本中的權限則有管理員先前指定的授權使用者靜態清單。 有什麼不同？ 以下舉例說明： 

某位使用者想要透過電子郵件將某些資訊傳送給行銷部門中的特定人員，而這些資訊不應該與任何人共用。 她應該要使用將權限 (檢視、回覆及儲存) 限制在行銷部門的範本保護電子郵件？  還是應該選擇 **[不要轉寄]** 選項？ 這兩種選項都會讓收件者無法轉寄電子郵件。 

- 如果她套用了範本，收件者仍然可以和行銷部門中的其他人共用資訊。 例如，收件者可以使用檔案總管將電子郵件拖放到共用位置或 USB 磁碟機。 如此一來，可存取此位置的行銷部門所有人員 (及電子郵件擁有者) 就都能檢視這封電子郵件中的資訊。
 
- 如果她套用 **[不要轉寄]** 選項，收件者將無法藉由將電子郵件移到另一個位置，與行銷部門中的任何人共用資訊。 在此案例中，只有原始收件者 (及電子郵件擁有者) 能夠檢視電子郵件中的資訊。

> [!NOTE] 在只有寄件者選擇的收件者應該看到電子郵件中的資訊時，請使用 **[不要轉寄]**。 除了寄件者選擇的收件者以外，要將權限限制在管理員事先指定的某群人時，則對電子郵件使用範本。




## 另請參閱
[設定 Azure Rights Management 的自訂範本](configure-custom-templates.md)



<!--HONumber=Jun16_HO2-->


