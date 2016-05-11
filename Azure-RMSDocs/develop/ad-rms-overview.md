---
# required metadata

title: 概觀 | Azure RMS
description: Rights Management Services (RMS) 是可協助保護數位資訊免於未經授權使用的資訊保護技術。
keywords:
author: bruceperlerms
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: a58894d5-3271-46d7-bb1c-fbd22eae8530

# optional metadata

#ROBOTS:
audience: developer
#ms.devlang:
ms.reviewer: shubhamp
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

﻿
# 概觀

Rights Management Services (RMS) 是可協助保護數位資訊免於未經授權使用的資訊保護技術。 透過具備權限的應用程式，內容擁有者將能夠定義誰可以開啟、修改、列印、轉送內容，或採取其他動作。

## 概觀

AD RMS 包含[伺服器](ad-rms-server.md)和[用戶端](ad-rms-client.md)元件。 伺服器元件包含多個在 Windows Server 上執行的 web 服務，例如 Windows Server 2008 R2 或透過雲端通過 Azure 中的 RMS web 服務。 用戶端元件可以在用戶端或伺服器作業系統上執行，並且包含可讓應用程式加密和解密內容、擷取範本和撤銷清單，從伺服器取得授權和憑證，以及其他相關權限管理工作的功能。

如需詳細資訊，請參閱[應用程式類型](application-types.md)。

以下是幾個可以套用建置在 Rights Management Services SDK 2.1 之應用程式的案例。

-   某法律事務所想要防止列印或轉送機密電子郵件訊息。
-   電腦輔助設計與製造軟體的開發人員想要限制繪圖存取權給研究部門內的少數使用者，而不需要使用密碼。
-   圖形設計網站擁有者想要使用單一授權，可免費檢視其映像的低解析度複本，但是要存取高解析度版本則需要付費。
-   線上文件庫的擁有者想要根據使用者的身分識別啟用檢視、列印或編輯文件的權限。
-   公司想要將敏感的員工資訊發佈至內部網站，針對特定使用者限制檢視和編輯的權限。

如需 AD RMS 伺服器、AD RMS 用戶端和其功能的詳細資訊，請參閱 [AD RMS 的 IT 專業人員文件](https://TechNet.Microsoft.Com/en-us/library/cc771234.aspx)的 TechNet 內容。

若要開始使用，請參閱[開始使用](getting-started-with-ad-rms-2-0.md)。

## 相關主題

* [AD RMS 概念](application-types.md)
* [AD RMS 與 AD RMS 2.1 之間的差異](differences-between-ad-rms-and-ad-rms-2-0.md)
* [使用者入門](getting-started-with-ad-rms-2-0.md)
* [AD RMS 的 IT 專業人員文件](https://TechNet.Microsoft.Com/en-us/library/cc771234.aspx)
* [伺服器](ad-rms-server.md)
* [用戶端](ad-rms-client.md)
 

 





<!--HONumber=Apr16_HO3-->


