---
title: "記錄和分析 Azure Rights Management Service 的使用方式 | Azure Information Protection"
description: "如何以使用記錄搭配 Azure Rights Management (Azure RMS) 的資訊和指示。"
author: cabailey
manager: mbaldwin
ms.date: 09/25/2016
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: a735f3f7-6eb2-4901-9084-8c3cd3a9087e
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: e33f1e54c21507999d30dcee2ce63c8eb2d69895
ms.openlocfilehash: 33520bcfc36ed0a022b87c4b2db1e6fcd7a6eb14


---

# 記錄和分析 Azure Rights Management Service 的使用方式

>*適用於︰Azure Information Protection、Office 365*

使用此資訊以利了解如何使用 Azure Information Protection 的 Azure Rights Management Service 的使用記錄。 此服務為貴組織的文件與電子郵件提供資料保護，並可記錄向它提出的每一項要求，包含使用者的要求、此服務系統管理員執行的動作，以及 Microsoft 運算子為支援 Azure Information Protection 部署所執行的動作。

然後，您可以利用這些 Azure Rights Management Service 記錄來支援下列商務案例：

-   **分析商業見解**

    Azure Rights Management Service 產生的記錄可以匯入您選擇的存放庫 (例如資料庫、線上分析處理 (OLAP) 系統或 map-reduce 系統)，以分析資訊並產生報告。 例如，您可以識別誰在存取保護的資料。 您可以判斷使用者存取保護的哪些資料，以及從什麼裝置和從哪裡存取。 您可以查明使用者是否可順利讀取受保護的內容。 您也可以識別哪些使用者已讀取受保護的重要文件。

-   **監督濫用情形**

    Azure Rights Management 記錄為您提供的幾乎都是即時資訊，所以您可以持續監視公司如何使用 Azure Rights Management Service。 99.9% 的記錄會在服務起始動作之後的 15 分鐘內產生。

    例如，當正常工作時段外突然有許多使用者讀取保護的資料，您可能希望獲得警示，這可能表示有惡意使用者正在收集資訊來販售給競爭對手。 或者，同一個使用者很明顯在極短的時間內從兩個不同的 IP 位址存取資料，這可能表示使用者帳戶已被盜用。

-   **執行取證分析**

    如果發生資訊外洩，您可能會被問及誰最近存取特定的文件，以及可疑人士最近存取什麼資訊。 只要有使用此記錄，您就能夠回答這幾種問題，因為使用受保護內容的人一定要取得 Azure Rights Management Service 授權才能開啟 Azure Rights Management 所保護的文件和圖片，即使這些檔案由電子郵件移動，或複製到 USB 磁碟機或其他存放裝置也一樣。 這表示當您使用 Azure Rights Management Service 來保護資料時，這些記錄可當作可靠的資訊來源以進行蒐證分析。

> [!NOTE]
> 如果您只對記錄 Azure Rights Management Service 的管理工作有興趣，但不想要追蹤使用者使用 Rights Management Service 的方式，您可以針對 Azure Rights Management 使用 Windows PowerShell Cmdlet [Get-AadrmAdminLog](https://msdn.microsoft.com/library/azure/dn629430.aspx)。
> 
> 您也可以使用 Azure 傳統入口網站，取得高階使用情況報告，其中包含 **RMS 摘要**、**RMS 活躍的使用者**、**RMS 裝置平台**，以及 **RMS 應用程式使用情況**。 若要從 Azure 傳統入口網站存取這些報告，請按一下 [Active Directory]、選取並開啟目錄，然後按一下 [報告]。

如需 Azure Rights Management 使用情況記錄的詳細資訊，請參閱下列幾節。

## 如何啟用 Azure Rights Management 使用量記錄
從 2016 年 2 月開始，Azure Rights Management 使用量記錄預設為所有客戶啟用。 這適用於在 2016 年 2 月之前啟動他們的 Azure Rights Management Service 的客戶，和在 2016 年 2 月之後啟動服務的客戶。 

> [!NOTE]
> 記錄儲存體或記錄功能不需要額外成本。
> 
> 如果您使用的 Azure Rights Management 使用量記錄是在 2016年 2 月之前，您需要 Azure 的訂用帳戶以及 Azure 上足夠的儲存體，這已超出上述的情況。



## 如何存取和使用 Azure Rights Management 使用情況記錄
Azure Rights Management Service 會以一連串 Blob 將記錄寫入 Azure 儲存體帳戶。 每一個 Blob 包含一或多筆記錄 (W3C 擴充記錄格式)。 Blob 名稱是依建立順序排列的數字。 本文稍後的[如何解讀 Azure Rights Management 使用量記錄](#how-to-interpret-your-azure-rights-management-usage-logs)一節包含記錄內容及其建立方式的詳細資訊。

發生 Azure Rights Management 動作之後需要一些時間，記錄才會出現在儲存體帳戶中。 大多數記錄會在 15 分鐘內出現。 建議您將記錄下載到本機儲存體，例如本機資料夾、資料庫或 map-reduce 儲存機制。

若要下載您的使用量記錄，您將會使用適用於 Windows PowerShell 的 Azure Rights Management 管理模組。 如需安裝指示，請參閱[安裝 Windows PowerShell for Azure Rights Management](install-powershell.md)。 如果您先前已下載此 Windows PowerShell 模組，請執行下列命令來檢查版本號碼至少為 **2.4.0.0**： `(Get-Module aadrm -ListAvailable).Version` 

### 使用 PowerShell 下載使用情況記錄

1.  使用 [以系統管理員身分執行] 選項啟動 Windows PowerShell，然後使用 [Connect-AadrmService](https://msdn.microsoft.com/library/azure/dn629415.aspx) Cmdlet 來連接 Azure RMS 服務：

    ```
    Connect-AadrmService
    ```
    
2.  執行以下命令，下載特定日期的記錄： 

    ```
    Get-AadrmUserLog -Path <location> -fordate <date>
    ```

    例如，在您的 E 磁碟機上建立一個名為 [記錄] 的資料夾：
    
    * 若要下載特定日期 (例如 2016/2/1) 的記錄，請執行以下命令： `Get-AadrmUserLog -Path E:\Logs -fordate 2/1/2016`
    
    * 若要下載日期範圍 (例如從 2016/2/1 到 2016/2/14) 的記錄，請執行以下命令： `Get-AadrmUserLog -Path E:\Logs -fromdate 2/1/2016 –todate 2/14/2016` 

當您只指定一天，如同我們的範例，時間會假設為您的當地時間的 00:00:00，然後轉換為 UTC。 當您以 -fromdate 或 -todate 參數指定時間時 (例如，-fordate "2/1/2016 15:00:00")，該日期和時間會轉換為 UTC。 然後 Get-AadrmUserLog 命令會取得該 UTC 期間的記錄。

您不能指定要下載少於一整天的時間。

預設情況下，此 Cmdlet 使用三個執行緒來下載記錄。 如果您有足夠的網路頻寬，並且想要減少下載記錄所需的時間，使用 -NumberOfThreads 參數，該參數支援從 1 到 32 的值。 例如，如果您執行以下命令，Cmdlet 會產生 10 個執行緒以下載記錄： `Get-AadrmUserLog -Path E:\Logs -fromdate 2/1/2016 –todate 2/14/2016 -numberofthreads 10`


> [!TIP]
> 您可以使用 [Microsoft 的記錄檔剖析器](https://www.microsoft.com/download/details.aspx?id=24659) (這是用來在各種已知的記錄檔格式之間轉換的工具)，將您的所有已下載記錄檔彙總為 CSV 格式。 您也可以利用此工具將資料轉換成 SYSLOG 格式，或匯入到資料庫中。 安裝此工具之後，請執行 `LogParser.exe /?`，以取得使用此工具的說明和資訊。 
>
> 例如，您可以執行下列命令將所有資訊匯入到 .log 檔案格式： `logparser –i:w3c –o:csv "SELECT * INTO AllLogs.csv FROM *.log"`

#### 如果您手動啟用 2016 年 2 月 22 日記錄變更之前的 Azure Rights Management 使用量記錄


如果您使用記錄變更之前的使用量記錄，會在設定的 Azure 儲存體帳戶中具有使用量記錄。 Microsoft 不會從您的儲存體帳戶將這些記錄複製到新的 Azure Rights Management 受管理的儲存體帳戶，作為此記錄變更的一部分。 您負責管理先前產生的記錄的生命週期，並且可以使用 [Get-AadrmUsageLog](https://msdn.microsoft.com/library/dn629401.aspx) Cmdlet 來下載你舊的記錄。 例如：

- 若要將所有可用的記錄下載到 E:\logs 資料夾： `Get-AadrmUsageLog -Path "E:\Logs"`
    
- 若要下載特定範圍的 Blob： `Get-AadrmUsageLog –Path "E:\Logs" –FromCounter 1024 –ToCounter 2047`

請注意，如果有下列其中一個情形，您不需要使用 Get-AadrmUsageLog Cmdlet 來下載記錄：

-  您在 2016 年 2 月 22 日時或之前啟動 Azure Rights Management Service，但是未啟用使用量記錄功能。

- 您在 2016 年 2 月 22 日之後啟動 Azure Rights Management Service。

## 如何解讀 Azure Rights Management 使用量記錄
使用下列資訊來協助您解讀 Azure Rights Management 使用量記錄。

### 記錄順序
Azure Rights Management Service 會以一連串 Blob 來寫入記錄。 

記錄中的每個項目都有一個 UTC 時間戳記。 因為 Azure Rights Management Service 是跨多個資料中心而在多個伺服器上執行，即使記錄依時間戳記排序，有時也可能不按照順序。 不過，差異很小，通常只在一分鐘內。 在大部分情況下，這不會對記錄分析造成問題。

### Blob 格式
每一個 Blob 都是 W3C 擴充記錄格式。 開頭為下列兩行：

**#軟體：RMS**

**#版本︰1.1**

第一行識別這些是 Azure Rights Management 的記錄。 第二行識別 Blob 的其餘部分都遵循 1.1 版規格。 建議任何可剖析這些記錄的應用程式在繼續剖析 Blob 的其餘部分之前，先驗證這兩行。

第三行列舉以 Tab 鍵分隔的欄位名稱清單：

**#Fields: date            time            row-id        request-type           user-id       result          correlation-id          content-id                owner-email           issuer                     template-id             file-name                  date-published      c-info         c-ip            admin-action            acting-as-user**

後續每一行都是記錄。 欄位的值與前一行的順序相同，以 Tab 鍵隔開。 請使用下表來解讀欄位。

|欄位名稱|W3C 資料類型|說明|範例值|
|--------------|-----------------|---------------|-----------------|
|date|日期|處理要求時的 UTC 日期。<br /><br />來源是處理要求的伺服器的本機時鐘。|2013-06-25|
|time|時間|處理要求的 UTC 時間 (24 小時制)。<br /><br />來源是處理要求的伺服器的本機時鐘。|21:59:28|
|row-id|文字|此記錄的唯一 GUID。 如果值不存在，請使用 correlation-id 值來識別項目。<br /><br />將記錄彙總或將記錄複製成另一種格式時，此值很有用。|1c3fe7a9-d9e0-4654-97b7-14fafa72ea63|
|request-type|名稱|要求的 RMS API 的名稱。|AcquireLicense|
|user-id|字串|提出要求的使用者。<br /><br />值以單引號括住。 如果呼叫是來自您管理的租用戶金鑰 (BYOK)，則該呼叫具有 **"** 值；當要求類型為匿名時也適用此情況。|‘joe@contoso。com’|
|result|字串|'Success' 表示成功處理要求。<br /><br />要求失敗時以單引號括住的錯誤類型。|'Success'|
|correlation-id|文字|某個特定要求在 RMS 用戶端記錄和伺服器記錄之間的共同 GUID。<br /><br />對用戶端問題進行疑難排解時，此值很有用。|cab52088-8925-4371-be34-4b71a3112356|
|content-id|文字|識別受保護內容 (例如文件) 的 GUID (以大括孤括住)。<br /><br />只有當 request-type 是 AcquireLicense 時，此欄位才有值，至於其他所有要求類型，此欄位會空白。|{bb4af47b-cfed-4719-831d-71b98191a4f2}|
|owner-email|字串|文件擁有者的電子郵件地址。|alice@contoso.com|
|issuer|字串|文件簽發者的電子郵件地址。|alice@contoso.com (或) FederatedEmail.4c1f4d-93bf-00a95fa1e042@contoso.onmicrosoft.com'|
|template-id|字串|用來保護文件的範本 ID。|{6d9371a6-4e2d-4e97-9a38-202233fed26e}|
|file-name|字串|受保護的文件的檔案名稱。 <br /><br />目前，某些檔案 (例如 Office 文件) 顯示為 GUID，而不是實際檔案名稱。|TopSecretDocument.docx|
|date-published|日期|文件受保護的日期。|2015-10-15T21:37:00|
|c-info|字串|提出要求的用戶端平台的相關資訊。<br /><br />具體字串隨著應用程式而不同 (例如，作業系統或瀏覽器)。|'MSIPC;version=1.0.623.47;AppName=WINWORD.EXE;AppVersion=15.0.4753.1000;AppArch=x86;OSName=Windows;OSVersion=6.1.7601;OSArch=amd64'|
|c-ip|位址|提出要求的用戶端的 IP 位址。|64.51.202.144|


#### user-id 欄位的例外狀況
雖然 user-id 欄位通常指出提出要求的使用者，但有兩種例外狀況，值不會對應至真正的使用者：

-   值 **'microsoftrmsonline@&lt;YourTenantID&gt;.rms.&lt;region&gt;.aadrm.com'**。

    這指出 Office 365 服務 (例如 Exchange Online 或 SharePoint Online) 正提出要求。 在字串中，*&lt;YourTenantID&gt;* 是租用戶的 GUID，*&lt;region&gt;* 是租用戶註冊的地區。 例如， **na** 代表北美洲、 **eu** 代表歐洲， **ap** 代表亞洲。

-   如果您使用 RMS 連接器，

    會以服務主體名稱 **Aadrm_S-1-7-0** (此名稱會在安裝 RMS 連接器時自動產生) 來記錄來自此連接器的要求。

#### 一般要求類型
Azure Rights Management Service 有許多要求類型，下表指出一些最常用的要求類型。

|要求類型|說明|
|----------------|---------------|
|AcquireLicense|來自 Windows 電腦的用戶端要求對 RMS 保護內容的授權。|
|AcquirePreLicense|用戶端代表使用者要求對 RMS 保護內容的授權。|
|AcquireTemplates|進行呼叫，以取得根據範本 ID 的範本。|
|AcquireTemplateInformation|進行呼叫，以從服務取得範本的 ID。|
|AddTemplate|從 Azure 傳統入口網站進行呼叫，以新增範本。|
|AllDocsCsv|從文件追蹤網站進行呼叫，從 [所有文件] 頁面下載 CSV 檔案。|
|BECreateEndUserLicenseV1|從行動裝置進行呼叫，以建立使用者授權。|
|BEGetAllTemplatesV1|從行動裝置 (後端) 進行呼叫，以取得所有範本。|
|Certify|用戶端認證保護的內容。|
|DeleteTemplateById|從 Azure 傳統入口網站進行呼叫，以刪除範本 ID 的範本。|
|DocumentEventsCsv|從文件追蹤網站進行呼叫，為單一文件下載 CSV 檔案。|
|ExportTemplateById|從 Azure 傳統入口網站進行呼叫，以匯出範本 ID 的範本。|
|FECreateEndUserLicenseV1|類似於 AcquireLicense 要求，來自於行動裝置。|
|FECreatePublishingLicenseV1|與 Certify 結合 GetClientLicensorCert 相同，來自行動用戶端。|
|FEGetAllTemplates|從行動裝置 (前端) 進行呼叫，以取得範本。|
|FindServiceLocationsForUser|進行呼叫以查詢 URL，用呼叫 Certify 或 AcquireLicense。|
|GetAllDocs|從文件追蹤網站進行呼叫，為使用者載入 [所有文件] 頁面，或為租用戶搜尋所有文件。 與 admin-action 和 acting-as-admin 欄位一起使用此值：<br /><br />- admin-action 是空的︰使用者檢視 [所有文件] 頁面，以取得自己的文件。<br /><br />- admin-action 為 true，而 acting-as-user 是空的：系統管理員為租用戶檢視所有文件。<br /><br />- admin-action 為 true，而 acting-as-user 不是空的︰系統管理員為使用者檢視 [所有文件] 頁面。|
|GetAllTemplates|從 Azure 傳統入口網站進行呼叫，以取得所有範本。|
|GetClientLicensorCert|用戶端從 Windows 電腦要求發佈憑證 (稍後用來保護內容)|
|GetConfiguration|呼叫 Azure PowerShell Cmdlet，以取得 Azure RMS 租用戶的組態。|
|GetConnectorAuthorizations|從 RMS 連接器進行呼叫，以從雲端取得其組態。|
|GetRecipients|從文件追蹤網站進行呼叫，為單一文件的瀏覽至清單檢視。|
|GetSingle|從文件追蹤網站進行呼叫，瀏覽至 [單一文件] 頁面。|
|GetTenantFunctionalState|Azure 傳統入口網站檢查 Azure Rights Management Service 是否啟動。|
|GetTemplateById|從 Azure 傳統入口網站進行呼叫，以取得指定範本 ID 的範本。|
|KeyVaultDecryptRequest|用戶端嘗試解密 RMS 保護的內容。 只適用於 Azure 金鑰保存庫中客戶管理的租用戶金鑰 (BYOK)。|
|KeyVaultGetKeyInfoRequest|進行呼叫，以驗證替 Azure Information Protection 租用戶金鑰指定要在 Azure 金鑰保存庫中使用的金鑰可存取且尚未使用。|
|KeyVaultSignDigest|當因為簽章目的而使用 Azure 金鑰保存庫中的客戶管理的租用戶金鑰 (BYOK) 時，進行呼叫。 通常每個 AcquireLicence (或 FECreateEndUserLicenseV1)、Certify 及 GetClientLicensorCert (或 FECreatePublishingLicenseV1) 只會呼叫一次。|
|KMSPDecrypt|用戶端嘗試解密 RMS 保護的內容。 只適用於舊版客戶管理的租用戶金鑰 (BYOK)。|
|KMSPSignDigest|當因為簽章目的而使用舊版客戶管理的租用戶金鑰 (BYOK) 時，進行呼叫。 通常每個 AcquireLicence (或 FECreateEndUserLicenseV1)、Certify 及 GetClientLicensorCert (或 FECreatePublishingLicenseV1) 只會呼叫一次。|
|LoadEventsForMap|從文件追蹤網站進行呼叫，為單一文件瀏覽至地圖檢視。|
|LoadEventsForSummary|從文件追蹤網站進行呼叫，為單一文件瀏覽至時間表檢視。|
|LoadEventsForTimeline|從文件追蹤網站進行呼叫，為單一文件瀏覽至地圖檢視。|
|ImportTemplate|從 Azure 傳統入口網站進行呼叫，以匯入範本。|
|RevokeAccess|從文件追蹤網站進行呼叫，以撤銷文件。|
|SearchUsers |從文件追蹤網站進行呼叫，以搜尋租用戶中的所有使用者。|
|ServerCertify|從已啟用 RMS 的用戶端 (如 SharePoint) 進行呼叫，以認證伺器。|
|SetUsageLogFeatureState|進行呼叫，以啟用使用情況記錄。|
|SetUsageLogStorageAccount|進行呼叫，以指定 Azure Rights Management Service 記錄的位置。|
|UpdateNotificationSettings|從文件追蹤網站進行呼叫，為單一文件變更通知設定。|
|UpdateTemplate|從 Azure 傳統入口網站進行呼叫，以更新現有範本。|


## Windows PowerShell 參考
從 2016 年 2 月開始，您針對 Azure Rights Management 使用量記錄所需的唯一 Windows PowerShell Cmdlet 是 [Get-AadrmUserLog](https://msdn.microsoft.com/library/azure/mt653941.aspx)。 

在此變更之前，Azure Rights Management 使用量記錄需要的下列 Cmdlet，現在已被取代：  

-   [Disable-AadrmUsageLogFeature](https://msdn.microsoft.com/library/azure/dn629404.aspx)

-   [Enable-AadrmUsageLogFeature](https://msdn.microsoft.com/library/azure/dn629421.aspx)

-   [Get-AadrmUsageLog](https://msdn.microsoft.com/library/azure/dn629401.aspx)

-   [Get-AadrmUsageLogFeature](https://msdn.microsoft.com/library/azure/dn629425.aspx)

-   [Get-AadrmUsageLogLastCounterValue](https://msdn.microsoft.com/library/azure/dn629423.aspx)

-   [Get-AadrmUsageLogStorageAccount](https://msdn.microsoft.com/library/azure/dn629419.aspx)

-   [Set-AadrmUsageLogStorageAccount](https://msdn.microsoft.com/library/azure/dn629426.aspx)

如果您在 Azure Rights Management 記錄變更之前在您自己的 Azure 儲存體中有記錄，您可以如同以前一般使用以下較舊的 Cmdlet 進行下載，使用 Get-AadrmUsageLog 和 Get-AadrmUsageLogLastCounterValue。 但是所有新的使用量記錄將會寫入新的 Azure RMS 儲存體，並且必須使用 Get-AadrmUserLog 下載。

如需使用 Windows PowerShell for the Azure Rights Management service 的詳細資訊，請參閱[使用 Windows PowerShell 管理 Azure Rights Management](administer-powershell.md)。






<!--HONumber=Sep16_HO4-->


