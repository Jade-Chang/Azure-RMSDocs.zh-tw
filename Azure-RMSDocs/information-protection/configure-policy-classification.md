---
title: "如何設定適用於 Azure Information Protection 的自動與建議分類條件 | Azure Rights Management"
description: 
author: cabailey
manager: mbaldwin
ms.date: 08/10/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: e915f959-eafb-4375-8d2c-2f312edf2d29
translationtype: Human Translation
ms.sourcegitcommit: b2263c212a1b869b778767493645f10ad821828f
ms.openlocfilehash: 80c201dcf316a5aa5e123645d47c6741f8b61f05


---

# 如何設定適用於 Azure Information Protection 的自動與建議分類條件

>*適用於：Azure Information Protection 預覽*

**[本資訊為初步資訊而且可能隨時變更。 ]**

當您設定標籤的條件時，您可以自動將標籤指派給文件或電子郵件。 或者，您可以提示使用者選取您建議的標籤︰ 

- 自動分類會在檔案儲存時套用到 Word、Excel 與 PowerPoint，並在電子郵件傳送時套用到 Outlook。 您無法針對先前已手動標示的檔案使用自動分類。
 
- 建議分類會在檔案儲存時套用到 Word、Excel 與 PowerPoint。

當您設定條件時，您可以使用預先定義的模式，例如 「信用卡號碼」或「美國社會安全碼」。 或者，您可以定義自訂字串或模式，作為自動分類的條件。 如需條件的詳細資訊，請參閱[內建條件的相關資訊](#information-about-the-built-in-conditions)一節。

多個條件套用到超過一個標籤時的評估方式︰

1. 標籤會根據它們在原則中被指定的位置，針對評估進行排序：首先排位的標籤擁有最低的位置 (敏感性最低)，而排位最後的標籤則擁有最高的位置 (敏感性最高)。

2. 系統會套用敏感性最高的標籤。
 
3. 系統會套用最後一個子標籤。

> [!TIP]
>若要取得最佳的使用者體驗並確保商務持續性，我們建議您從使用者建議的分類開始，而不要使用自動分類。 此設定可讓您的使用者接受標記或保護動作，或是在它們都不適合其文件或電子郵件訊息使用時覆寫這些建議。

當您設定條件，將標籤做為建議動作套用時的範例提示 (包含自訂原則提示)：

![Azure Information Protection 偵測和建議](../media/info-protect-recommend-callouts.png)

在此範例中，使用者可以按一下 [立即變更] 以套用建議的標籤，或者將列關閉來覆寫建議。

## 設定標籤的建議或自動分類

1. 如果您尚未這樣做，請登入 [Azure 入口網站](https://portal.azure.com)，然後瀏覽至 [Azure Information Protection] 刀鋒視窗。 
    
    例如，在中樞功能表中，按一下 [瀏覽] 並開始在 [篩選] 方塊中輸入 **Information**。 選取 [Azure Information Protection]。

2. 在 [Azure Information Protection] 刀鋒視窗上，選取您要設定自動或建議分類的標籤。

3. 在 [標籤] 刀鋒視窗上的 [設定自動套用此標籤的條件] 區段中，按一下 [加入新的條件]。

4. 在 [條件] 刀鋒視窗上，如果您想要使用預先定義的條件，請選取 [內建]；如果您想要指定您自己的條件，請選取 [自訂]，然後按一下 [儲存]：

    - 針對 [內建]：從可用的條件清單中選取，然後選取發生次數的最小數目，以及發生次數是否應該具備唯一值以包含在發生計數中。
        
        如需有關這些條件之偵測規則的詳細資訊，以及一些範例，請參閱[內建條件的相關資訊](#information-about-the-built-in-conditions)一節。

    - 針對 [自訂]：指定要比對的名稱與片語 (必須排除引號與特殊字元)。 然後，指定是否要做為規則運算式進行比對、使用區分大小寫、發生次數的最小數目，以及發生次數是否應該具備唯一值以包含在發生計數中。
        
    **發生次數選項的範例**：您選取了內建社會安全碼選項並將發生次數的最小數目設定為 2，以及具有列出兩次之相同社會安全碼的文件：如果您將 [僅包含唯一值的發生計數] 設定為 [開啟]，則條件將會不符；如果您將此選項設定為 [關閉]，則條件將會符合。

5. 在 [標籤] 刀鋒視窗上，設定下列項目，然後按一下 [儲存]：

    - 選擇自動或建議分類︰針對 [選取此標籤的套用方式：自動或建議使用者]，選取 [自動] 或 [建議]。

    - 指定使用者提示或原則提示的文字：保留預設文字，或自行指定字串。

6. 若要讓變更可供使用者使用，請按一下 [Azure Information Protection] 刀鋒視窗上的 [發佈]。

## 內建條件的相關資訊

在預覽期間，您可以選取下列條件︰

- [SWIFT 代碼](#swift-code )

- [信用卡號碼](#credit-card-number )

- [ABA 銀行代號](#aba-routing-number )

- [美國社會安全碼 (SSN)](#usa-social-security-number-ssn)

- [國際銀行帳戶號碼 (IBAN)](#international-banking-account-number-iban)


### SWIFT 代碼

在內容包含下列項目時符合此資訊類型︰  

1. 下列其中一個片語：**swift**、**swiftnumber**、**swiftroutingnumber** 

2. SWIFT 代碼 (格式化模式)：  

    a. 4 個字母 (銀行代碼)  

    b。 2 個字母 (國碼/地區碼)  

    c. 2 個字母或數字 (位置代碼)  

    d. 選擇性的 3 個字母或數字 (分行代碼)  


進行測試的範例︰

- **NEDSZAJJXXX Swiftroutingnumber**

- **NEDSZAJJ100 Swiftnumber** 

----


### 信用卡號碼

在內容包含下列項目時符合此資訊類型︰  

- 通過 [luhn 檢查](https://wikipedia.org/wiki/Luhn_algorithm)的有效信用卡號碼 (處於格式化或未格式化的模式)。 此資訊類型會偵測全球主要品牌的信用卡，包括 Visa、MasterCard、Discover Card、American Express 及 Diners。

    - **格式化**：
    
        - 16 個數字：(dddd-dddd-dddd-dddd)  
        
    - **未格式化**：
    
        - (dddddddddddddddd)  


進行測試的範例︰

- **4242-4242-4242-4242**

- **4242424242424242** 

----

### ABA 銀行代號

在內容包含下列項目時符合此資訊類型︰  

1. 下列至少其中一個片語：**aba**、**rtn**、**routing number** 

2. ABA 銀行代號，包含 9 個數字 (可以是格式化或未格式化的模式)： 

    - **格式化**： 
        
        a. 開頭為 0、1、2、3、6、7 或 8 的四個數字 
        
        b。 連字號 
        
        c. 四個數字 
        
        d. 連字號 
        
        e. 一個數字 
        
        範例︰3456-9876-1 ABA 
        
    - **未格式化**： 
        
        開頭為 0、1、2、3、6、7 或 8 的 9 個連續數字 
        
        範例︰345698761 RTN 
 

進行測試的範例︰

- **3456-9876-1 ABA**

- **345698761 RTN** 

----

### 美國社會安全碼 (SSN)

在內容包含下列項目時符合此資訊類型︰  

1. 至少下列其中一個片語：**ssn**、**social security**、**ssid**、**ss#** 

2. 社會安全號碼：9 個數字 (可以是格式化或未格式化的模式)：

    - **格式化**： 
    
        - 下列格式的 9 個數字：ddd-dd-dddd 或 ddd dd dddd 
        
    - **未格式化**： 
    
        - 下列格式的 9 個數字：ddddddddd 


進行測試的範例︰

- **SSN 123-45-6789**

- **SS# 123456789** 


----

### 國際銀行帳戶號碼 (IBAN)

在內容包含下列項目時符合此資訊類型︰  

1. 下列片語︰**IBAN** 

2. IBAN 號碼：開頭為國碼/地區碼 (兩個字母)，然後是檢核碼 (兩個數字) 及 bban 數字 (最多 (含) 30 個數字)。


進行測試的範例︰

- **GB29 NWBK 6016 1331 9268 19 IBAN**


## 後續步驟

如需關於設定 Azure Information Protection 原則的詳細資訊，請使用[設定組織的原則](configure-policy.md#configuring-your-organization-s-policy)一節中的連結。  






<!--HONumber=Aug16_HO2-->


