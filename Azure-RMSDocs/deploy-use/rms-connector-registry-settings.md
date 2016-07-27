---
title: "RMS 連接器的登錄設定 | Azure RMS"
description: 
keywords: 
author: cabailey
manager: mbaldwin
ms.date: 07/13/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: ed3e9a3d-0f7c-4abc-9d0b-aa3b18403d39
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 935c354f9bcd3be23a953cdeb08c7860257637d6
ms.openlocfilehash: 5099a10a183f1c78595794511654226265e740c8


---


# Rights Management 連接器的登錄設定

*適用於︰Azure Rights Management、Office 365*


只有當您想在執行 Exchange、SharePoint 或 Windows Server 的伺服器上手動新增或檢查登錄設定，也就是設定伺服器使用 [RMS 連接器](deploy-rms-connector.md)時，才使用下列各節的表格。 若要設定這些伺服器，建議的方法是使用 Microsoft RMS 連接器的伺服器設定工具。

使用這些設定時的指示：

-   *MicrosoftRMSURL* 是您組織的 Microsoft RMS 服務 URL。 若要尋找此值：

    1.  執行 Azure RMS 的 [Get-AadrmConfiguration](http://msdn.microsoft.com/library/windowsazure/dn629410.aspx) Cmdlet。 如果您尚未針對 Azure RMS 安裝 Windows PowerShell 模組，請參閱[針對 Azure Rights Management 安裝 Windows PowerShell](install-powershell.md)。

    2.  從輸出中找出 **LicensingIntranetDistributionPointUrl** 值。

        例如：**LicensingIntranetDistributionPointUrl   : https://5c6bb73b-1038-4eec-863d-49bded473437.rms.na.aadrm.com/_wmcs/licensing**

    3.  從該值，移除此字串的 **/_wmcs/licensing**。 剩餘的字串是您的 Microsoft RMS URL。 在我們的範例中，Microsoft RMS URL 將為下列值：

        **https://5c6bb73b-1038-4eec-863d-49bded473437.rms.na.aadrm.com**

-   *ConnectorFQDN* 是您於 DNS 中為連接器定義的負載平衡名稱。 例如， **rmsconnector.contoso.com**。

-   若已設定連接器，讓連接器使用 HTTPS 與您的內部部署伺服器通訊，請為連接器 URL 使用 HTTPS 首碼。 如需詳細資訊，請參閱主要指示中的 [設定 RMS 連接器使用 HTTPS](install-configure-rms-connector.md#configuring-the-rms-connector-to-use-https) 一節。 Microsoft RMS URL 一律使用 HTTPS。


## Exchange 2016 或 Exchange 2013 登錄設定

**登錄路徑：**HKEY_LOCAL_MACHINE\Software\Microsoft\MSDRM\ServiceLocation\Activation

**類型：**Reg_SZ

**值︰**預設

**資料：**https://*MicrosoftRMSURL*/_wmcs/certification

---

**登錄路徑：**HKEY_LOCAL_MACHINE\Software\Microsoft\MSDRM\ServiceLocation\EnterprisePublishing

**類型：**Reg_SZ

**值︰**預設

**資料：**https://*MicrosoftRMSURL*/_wmcs/Licensing

---

**登錄路徑：**HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\ExchangeServer\v15\IRM\CertificationServerRedirection

**類型：**Reg_SZ

**值︰**https://*MicrosoftRMSURL*


**資料：**下列其中一項，視您於 Exchange 伺服器至 RMS 連接器中使用 HTTP 或 HTTPS 而定：

- http://*ConnectorFQDN*

- https://*ConnectorFQDN*

---

**登錄路徑：**HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\ExchangeServer\v15\IRM\LicenseServerRedirection

**類型：**Reg_SZ

**值︰**https://*MicrosoftRMSURL*


**資料：**下列其中一項，視您於 Exchange 伺服器至 RMS 連接器中使用 HTTP 或 HTTPS 而定：

- http://*ConnectorFQDN*

- https://*ConnectorFQDN*


## Exchange 2010 登錄設定

**登錄路徑：**HKEY_LOCAL_MACHINE\Software\Microsoft\MSDRM\ServiceLocation\Activation

**類型：**Reg_SZ

**值︰**預設

**資料：**https://*MicrosoftRMSURL*/_wmcs/certification

---

**登錄路徑：**HKEY_LOCAL_MACHINE\Software\Microsoft\MSDRM\ServiceLocation\EnterprisePublishing

**類型：**Reg_SZ

**值︰**預設

**資料：**https://*MicrosoftRMSURL*/_wmcs/Licensing

---

**登錄路徑：**HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\ExchangeServer\v14\IRM\CertificationServerRedirection

**類型：**Reg_SZ

**值︰**https://*MicrosoftRMSURL*

**資料：**下列其中一項，視您於 Exchange 伺服器至 RMS 連接器中使用 HTTP 或 HTTPS 而定：

- http://*ConnectorFQDN*

- https://*ConnectorFQDN*

---

**登錄路徑：**HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\ExchangeServer\v14\IRM\LicenseServerRedirection

**類型：**Reg_SZ

**值︰**https://*MicrosoftRMSURL*

**資料：**下列其中一項，視您於 Exchange 伺服器至 RMS 連接器中使用 HTTP 或 HTTPS 而定：

- http://*ConnectorFQDN*

- https://*ConnectorFQDN*


## SharePoint 2016 或 SharePoint 2013 登錄設定

**登錄路徑：**HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSIPC\ServiceLocation\LicensingRedirection

**類型：**Reg_SZ

**值︰**https://*MicrosoftRMSURL*/_wmcs/licensing


**資料：**下列其中一項，視您於 SharePoint 伺服器至 RMS 連接器中使用 HTTP 或 HTTPS 而定：

- http://*ConnectorFQDN*/_wmcs/licensing

- https://*ConnectorFQDN*/_wmcs/licensing

---

**登錄路徑：**HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSIPC\ServiceLocation\EnterpriseCertification

**類型：**Reg_SZ

**值︰**預設

**資料：**下列其中一項，視您於 SharePoint 伺服器至 RMS 連接器中使用 HTTP 或 HTTPS 而定：

- http://*ConnectorFQDN*/_wmcs/certification

- https://*ConnectorFQDN*/_wmcs/certification

---

**登錄路徑：**HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSIPC\ServiceLocation\EnterprisePublishing

**類型：**Reg_SZ

**值︰**預設


**資料：**下列其中一項，視您於 SharePoint 伺服器至 RMS 連接器中使用 HTTP 或 HTTPS 而定：

- http://*ConnectorFQDN*/_wmcs/licensing

- https://*ConnectorFQDN*/_wmcs/licensing




## 檔案伺服器和檔案分類基礎結構登錄設定

**登錄路徑：**HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSDRM\ServiceLocation\EnterprisePublishing

**類型：**Reg_SZ

**值︰**預設

**資料：**http://*ConnectorFQDN*/_wmcs/licensing

---

**登錄路徑：**HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSDRM\ServiceLocation\Activation

**類型：**Reg_SZ

**值︰**預設

**資料：**http://*ConnectorFQDN*/_wmcs/certification


回到[部署 Azure Rights Management 連接器](deploy-rms-connector.md)


<!--HONumber=Jul16_HO3-->


