---
# required metadata

title: 部署您的應用程式 | Azure RMS
description: 本主題概要說明並引導您完成啟用權限的應用程式的部署選項
keywords:
author: bruceperlerms
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 4B785564-6839-49ED-A243-E2A6DFF88B2E
# optional metadata

#ROBOTS:
audience: developer
#ms.devlang:
ms.reviewer: shubhamp
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---
** 這個 SDK 內容不是最新版本。 很快就可以在 MSDN 上找到文件的[目前版本](https://msdn.microsoft.com/library/windows/desktop/hh535290(v=vs.85).aspx)。 **
# 部署您的應用程式


本主題概要說明並引導您完成啟用權限的應用程式的部署選項。

> [!IMPORTANT]
> 建議的最佳作法是先針對 RMS 伺服器，使用 RMS 生產前環境來測試 Rights Management Services SDK 2.1 應用程式。 然後，如果您希望客戶能夠搭配使用您的應用程式與 Azure RMS 服務，請移至測試該環境。 如需詳細資訊，請參閱[啟用您的服務應用程式以使用以雲端為基礎的 RMS](how-to-use-file-api-with-aadrm-cloud.md)。

 

## Active Directory Rights Management Services Client 2.1 的安裝選項

一旦使用生產憑證建立資訊清單檔，應用程式已準備好進行部署。 假設您使用 RMS SDK 2.1，您需要在使用者電腦上部署 Active Directory Rights Management Services Client 2.1。

### AD RMS Client 2.1

AD RMS Client 2.1 是專為您的用戶端電腦設計的軟體，可透過使用 RMS 的應用程式協助保護資訊流通的存取和使用 (不論是安裝在內部部署或 Microsoft 資料中心)。

AD RMS Client 2.1 不是 Windows 作業系統元件。 AD RMS Client 2.1 隨附為選擇性的下載，可以透過確認並接受其授權合約，與協力廠商軟體一起自由發佈，以啟用透過在環境中使用與部署 RMS 伺服器保護權限的用戶端存取內容。

> [!IMPORTANT] AD RMS Client 2.1 為架構限定，必須符合目標作業系統的架構。


## AD RMS Client 2.1 安裝選項

-   **重新發佈 AD RMS Client 2.1**

    建議的方法是使用您慣用的安裝技術，組合 RMS 用戶端安裝程式套件與您的應用程式或解決方案。 RMS 用戶端可以免費轉散發，並與其他應用程式和 IT 解決方案組成套件。

    您可以選擇從 AD RMS Client 2.1 安裝程式以互動方式安裝 AD RMS Client 2.1，或以無訊息方式安裝它。 整合步驟會是︰

    -   下載 RMS Client 2.1 安裝程式
    -   整合執行 AD RMS Client 2.1 安裝程式與您的應用程式安裝程式

    整合 AD RMS Client 2.1 與您的應用程式有兩個很好的例子，即 RMS SDK 2.1 安裝程式套件和權限受保護資料夾總管套件。 自行嘗試安裝它們以了解方法。

-   **將 AD RMS Client 2.1 製作成應用程式安裝的必要條件。**

    在此情況下，您將建立必要條件，如此當 AD RMS Client 2.1 未出現在使用者電腦時，您的應用程式安裝將會失敗。

    如果不存在用戶端則提供錯誤訊息，通知使用者是否可以下載 AD RMS Client 2.1 的複本

    如果出現用戶端，則繼續進行應用程式安裝。

## 使用您的應用程式啟用 Azure Rights Management Services

> [!NOTE]
> 如果您已移轉至新的 ADAL 模型進行驗證，您不需要安裝 SIA。 如需詳細資訊，請參閱您的 RMS 啟用應用程式的 ADAL 驗證。

- **為 Windows 10 認證您的應用程式**︰藉由更新應用程式來使用 ADAL 驗證而不是 Microsoft Online 登入小幫手，您和您的客戶將能夠︰
  - 利用多重要素驗證
  - 安裝 RMS 2.1 用戶端，而不需要電腦的系統管理權限
 
  為了讓您的使用者利用 Azure Rights Management 服務，您必須部署 *Online Services 登入小幫手*。 身為應用程式開發人員，您不知道使用者要使用 RMS (內部部署) 或 Azure Rights Management 服務 (雲端服務)。

> [!IMPORTANT]
> 若要使用 Azure RMS 執行 RMS SDK 2.1 用戶端應用程式，您需要申請 Azure RMS 租用戶。 透過租用戶要求傳送郵件給 <rmcstbeta@microsoft.com>。

-   從 Microsoft 下載中心下載 [Microsoft Online Services 登入小幫手](http://www.microsoft.com/en-us/download/details.aspx?id=28177)。
-   請確定您的權限啟用應用程式部署，包含此服務選項的必要條件檢查。
-   如需您自己的測試，和您的使用者的線上服務使用等詳細資訊，請參閱 TechNet 主題，[設定 Rights Management](https://TechNet.Microsoft.Com/en-us/library/jj585002.aspx)。

如需有關啟用應用程式以使用 Azure Rights Management 服務的 RMS，請參閱[啟用您的應用程式以使用以雲端為基礎的 RMS](how-to-use-file-api-with-aadrm-cloud.md)。

## 相關主題

* [如何使用](how-to-use-msipc.md)
* [Microsoft Online Services 登入小幫手](http://www.microsoft.com/en-us/download/details.aspx?id=28177)
* [設定 Rights Management](https://TechNet.Microsoft.Com/en-us/library/jj585002.aspx)
* [啟用您的應用程式以使用以雲端為基礎的 RMS](how-to-use-file-api-with-aadrm-cloud.md)
 

 





<!--HONumber=Jun16_HO1-->


