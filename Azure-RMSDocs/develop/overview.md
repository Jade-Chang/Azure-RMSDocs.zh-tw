---
title: "概觀 - RMS SDK 4.2 | Azure RMS"
description: "AD RMS 和 Azure RMS 是可協助保護數位資訊免於未經授權使用的資訊保護技術。"
keywords: 
author: bruceperlerms
manager: mbaldwin
ms.date: 07/11/2016
ms.topic: article
ms.prod: 
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 8A13494E-C1D7-407D-BCD1-A406915EA578
audience: developer
ms.reviewer: shubhamp
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 5d2339ece646fc51410186d43facdea28ac8fdfe
ms.openlocfilehash: da491f008043b11a04cbfe48acb952e67ad86dda


---

# 概觀

Microsoft Rights Management SDK 4.2 是資訊保護技術，可用於數個平台。  它提供軟體開發人員套件 (SDK) 或架構，其設計對象為用戶端電腦與裝置，可協助保護流動通過具備權限之應用程式的資訊存取和使用。 適用於這些平台的 SDK 提供簡單的 API 應用程式給開發人員保護或取用數位內容、擷取範本並取得伺服器的原則，以及其他相關權限管理工作。

如需目前支援平台的詳細資訊，請參閱開發人員文件入口網站的 [Microsoft Rights Management SDK](active-directory-rights-management-services-multi-platform-thin-client-sdk-portal.md)。

以下是幾個可能的案例︰

-   某法律事務所想要防止列印或轉送行動裝置上的機密電子郵件訊息。
-   電腦輔助設計與製造軟體的開發人員想要限制繪圖存取權給研究部門內的少數使用者，而不需要使用密碼。
-   圖形設計行動應用程式擁有者想要使用單一授權，可免費檢視其映像的低解析度複本，但是要存取高解析度版本則需要付費。
-   線上文件庫的擁有者想要在文件下載至行動裝置時，根據使用者的身分識別啟用檢視、列印或編輯文件的權限。
-   公司想要將敏感的員工資訊發佈至內部網站，針對特定使用者限制檢視和編輯的權限。

MS RMS SDK 4.2 可透過確認並接受其授權合約下載，與協力廠商軟體一起自由發佈，以啟用透過在環境或 Azure RMS 服務中使用與部署 AD RMS 伺服器保護權限的用戶端存取內容。 如需詳細資訊，請參閱[開始使用](get-started.md)。

## SDK 醒目提示


MS RMS SDK 4.2 提供一些新的酷炫功能，包括下列各項︰

-   **重新設計的 API** – MS RMS SDK 4.2 API 針對最高簡易性設計，因此開發人員可以享有簡單透明的加密和解密 API，其提供最省力的一致 RMS 行為。
-   **AD RMS 和 Azure RMS 的混合式支援** – 單一 RMS 啟用的應用程式可以取用和保護來自 AD RMS 伺服器 (使用 AD RMS 的行動裝置擴充功能) 和 Azure RMS 服務的內容。 MS RMS SDK 4.2 可以明確地探索 IT 系統管理員可以設定的相關端點。
-   **備妥您自己的驗證程式庫** – 身為應用程式開發人員，您可以選擇要搭配 MS RMS SDK 4.2 使用的驗證程式庫。 無論是 [Azure AD 驗證程式庫](https://msdn.microsoft.com/library/jj573266.aspx)或貴組織的自訂程式庫，MS RMS SDK 4.2 都會隔離驗證堆疊，因此您可以選擇最符合需求的程式庫。
-   **備妥您自己的使用者介面** - MS RMS SDK 4.2 現在可讓您實作您的自訂使用者介面。 在取用受保護內容時，從保護內容與選擇範本到顯示和變更權限，MS RMS SDK 4.2 都不會在應用程式上強制執行任何內建的 UI。 不過，如果您想要，您可以透過我們的 [GitHub 帳戶](https://github.com/AzureAD/)，將 Microsoft RMS UI 程式庫用於所有平台。
-   **離線存取受保護的內容** – MS RMS SDK 4.2 可讓您的應用程式使用者存取受保護的內容，即使沒有網際網路連線亦然。 MS RMS SDK 4.2 可安全地快取受保護內容的取用原則，讓使用者可以離線存取 RMS 保護的資料。

使用[開始使用](get-started.md)指南來開始受保護的資訊裝置應用程式專案。

## 相關的主題

* [Microsoft Rights Management SDK](active-directory-rights-management-services-multi-platform-thin-client-sdk-portal.md)
* [開始使用](get-started.md)
* [Azure AD 驗證程式庫](https://msdn.microsoft.com/en-us/library/jj573266.aspx)
* [GitHub 帳戶](https://github.com/AzureAD/)
 

 






<!--HONumber=Aug16_HO4-->


