---
# required metadata

title: 從 AD RMS 移轉至 Azure Rights Management - 階段 3 | Azure RMS
description:
keywords:
author: cabailey
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 8b039ad5-95a6-4c73-9c22-78c7b0e12cb7


# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: esaggese
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# 移轉階段 3︰支援服務組態

*適用於︰Active Directory Rights Management Services、Azure Rights Management*


針對從 AD RMS 移轉至 Azure Rights Management (Azure RMS) 的階段 3 使用下列資訊。 這些程序涵蓋 [從 AD RMS 移轉至 Azure Rights Management](migrate-from-ad-rms-to-azure-rms.md) 的步驟 6 到 7.


## 步驟 6： 設定 Exchange Online 的 IRM 整合

如果先前已將 TPD 從 AD RMS 匯入至 Exchange Online，您必須移除此 TDP，才能在移轉至 Azure RMS 之後避免衝突的範本和原則。 若要這樣做，請使用 Exchange Online 中的 [Remove-RMSTrustedPublishingDomain](https://technet.microsoft.com/en-us/library/jj200720%28v=exchg.150%29.aspx) Cmdlet。

如果您選擇 **Microsoft 管理的**Azure RMS 租用戶金鑰拓撲：

-   請參閱 [Office 365︰用戶端和線上服務的組態](../deploy-use/configure-office365.md)一文中的 [Exchange Online：IRM 組態](../deploy-use/configure-office365.md#exchange-online-irm-configuration)一節。 本節包含一般執行的命令，可連接至 Exchange Online 服務、從 Azure RMS 匯入租用戶金鑰，以及啟用Exchange online 的 IRM 功能。 完成這些步驟之後，您將有完整的 RMS 功能與 Exchange Online 搭配。

如果您選擇**客戶管理 (BYOK) 的** Azure RMS 租用戶金鑰拓撲：

-   您將有精簡的 RMS 功能與 Exchange Online，如 [BYOK 定價和限制](byok-price-restrictions.md)一文所述。

## 步驟 ７： 部署 RMS 連接器
如果您已經搭配使用 Exchange Server 或 SharePoint Server 的資訊版權管理 (IRM) 功能與 AD RMS，則必須先停用這些伺服器上的 IRM，並移除 AD RMS 組態。 然後，部署 Rights Management (RMS) 連接器，它可做為內部部署伺服器與 Azure RMS 之間的通訊介面 (轉送)。

最後，在這個步驟中，如果您已將用來保護電子郵件訊息的多個 TPD 匯入至 Azure RMS，則必須手動編輯 Exchange Server 電腦上的登錄，以將所有 TPD URL 重新導向至 RMS 連接器。

> [!NOTE]
> 在您開始之前，請從 [支援 Azure RMS 的內部部署伺服器](../get-started/requirements-servers.md) 檢查 Azure RMS 支援的內部部署伺服器版本.

### 停用 Exchange Server 上的 IRM 並移除 AD RMS 組態

1.  在每個 Exchange 伺服器上，找到下列資料夾並刪除該資料夾中的所有項目：\ProgramData\Microsoft\DRM\Server\S-1-5-18

2.  從其中一個 Exchange Server 中，使用 Exchange [Set_IRMConfiguration](http://technet.microsoft.com/library/dd979792.aspx) Cmdlet 先停用傳送給內部收件者之訊息的 IRM 功能：

    ```
    Set-IRMConfiguration -InternalLicensingEnabled $false
    ```

3.  然後，使用相同的 Cmdlet 停用傳送給外部收件者之訊息的 IRM 功能：

    ```
    Set-IRMConfiguration -ExternalLicensingEnabled $false
    ```

4.  接下來，使用相同的 Cmdlet 停用 Microsoft Office Outlook Web App 和 Microsoft Exchange ActiveSync 中的 IRM：

    ```
    Set-IRMConfiguration -ClientAccessServerEnabled $false
    ```

5.  最後，使用相同的 Cmdlet 清除任何快取的憑證：

    ```
    Set-IRMConfiguration -RefreshServerCertificates
    ```

6.  在每個 Exchange Server 上，現在請重設 IIS，例如，以系統管理員身分執行命令提示字元，並輸入 **iisreset**.

### 停用 SharePoint Server 上的 IRM 並移除 AD RMS 組態

1.  確定未從 RMS 保護的文件庫中簽出文件。 如果有，則它們在這個程序結束時會變成無法存取。

2.  在 SharePoint 管理中心網站的 **[快速啟動]** 區段中，按一下 **[安全性]**.

3.  在 **[安全性]** 頁面的 **[資訊原則]** 區段中，按一下 **[設定資訊版權管理]**.

4.  在 **[資訊版權管理]** 頁面的 **[資訊版權管理]** 區段中，選取 **[不要在此伺服器使用 IRM]**，然後按一下 **[確定]**.

5.  在每個 SharePoint Server 電腦上，刪除下列資料夾的內容：\ProgramData\Microsoft\MSIPC\Server\*&lt;執行 SharePoint Server 之帳戶的 SID&gt;*.

#### 安裝和設定 RMS 連接器

-   使用[部署 Azure Rights Management 連接器](../deploy-use/deploy-rms-connector.md)一文中的指示。

#### 對於僅 Exchange 和多個 TPD：編輯登錄

-   在每個 Exchange Server 上，針對匯入的每個額外 TPD 手動新增下列登錄機碼，以將 TPD URL 重新導向至 RMS 連接器。 這些登錄項目僅供移轉，而且不是由 Microsoft RMS 連接器的伺服器組態工具所新增。

    進行這些登錄編輯時，請使用下列指示：

    -   將 *ConnectorFQDN* 取代為您在 DNS 中為連接器所定義的名稱。 例如，**rmsconnector.contoso.com**。.

    -   連接器 URL 使用 HTTP 或 HTTPS 前置碼，是取決於設定連接器使用 HTTP 還是 HTTPS 與內部部署伺服器進行通訊。

若為 Exchange 2013 - 登錄編輯 1：


**登錄路徑︰**

HKLM\SOFTWARE\Microsoft\ExchangeServer\v15\IRM\LicenseServerRedirection

**輸入：**

Reg_SZ

**值：**

https://<AD RMS Intranet Licensing URL>/_wmcs/licensing

**資料：**

下列其中一項，視您於 Exchange 伺服器至 RMS 連接器中使用 HTTP 或 HTTPS 而定：

- http：//<connectorFQDN>/_wmcs/licensing

- https://<connectorName>/_wmcs/licensing


---

若為 Exchange 2013 - 登錄編輯 2：

**登錄路徑︰**

HKLM\SOFTWARE\Microsoft\ExchangeServer\v15\IRM\LicenseServerRedirection 


**輸入：**

Reg_SZ

**值：**

https://<AD RMS Extranet Licensing URL>/_wmcs/licensing


**資料：**

下列其中一項，視您於 Exchange 伺服器至 RMS 連接器中使用 HTTP 或 HTTPS 而定：

- http：//<connectorFQDN>/_wmcs/licensing

- https://<connectorFQDN>/_wmcs/licensing

---

若為 Exchange 2010 - 登錄編輯 1：



**登錄路徑︰**

HKLM\SOFTWARE\Microsoft\ExchangeServer\v14\IRM\LicenseServerRedirection

**輸入：**

Reg_SZ

**值：**

https://<AD RMS Intranet Licensing URL>/_wmcs/licensing

**資料：**

下列其中一項，視您於 Exchange 伺服器至 RMS 連接器中使用 HTTP 或 HTTPS 而定：

- http：//<connectorFQDN>/_wmcs/licensing

- https://<connectorName>/_wmcs/licensing


---

若為 Exchange 2010 - 登錄編輯 2：


**登錄路徑︰**

HKLM\SOFTWARE\Microsoft\ExchangeServer\v14\IRM\LicenseServerRedirection
 

**輸入：**

Reg_SZ

**值：**

https://<AD RMS Extranet Licensing URL>/_wmcs/licensing


**資料：**

下列其中一項，視您於 Exchange 伺服器至 RMS 連接器中使用 HTTP 或 HTTPS 而定：

- http：//<connectorFQDN>/_wmcs/licensing

- https://<connectorFQDN>/_wmcs/licensing

---

完成這些程序之後，您已準備好閱讀[部署 Azure Rights Management 連接器](../deploy-use/deploy-rms-connector.md)一文中的**後續步驟**一節。

## 後續步驟
若要繼續移轉，請移至 [階段 4 - 移轉後工作](migrate-from-ad-rms-phase4.md).

<!--HONumber=Apr16_HO4-->


