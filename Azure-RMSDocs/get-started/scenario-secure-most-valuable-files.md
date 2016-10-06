---
title: "案例 - 保護您最重要的 (幾個) 檔案 | Azure Information Protection"
description: "此案例和支援使用者文件會使用 Azure Rights Management 來手動和自訂保護少數幾個您認為最有價值的檔案，這可保證具備最高層級的保護，而不受未經授權的存取。"
author: cabailey
manager: mbaldwin
ms.date: 09/25/2016
ms.topic: get-started-article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 95f1844a-612c-4e67-bbe6-4b6b92295221
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: ea299f402e5e188b498bf6e3cacf9d4dc7e0f6e8
ms.openlocfilehash: 2001b13c15ebfd1c1f939d342ac2a7006c18c0f8


---

# 案例 - 保護您最重要的 (幾個)檔案

>*適用於︰Azure Information Protection、Office 365*

此案例和支援的使用者文件使用 Azure Information Protection 的 Azure Rights Management 技術來手動和自訂保護少數幾個您認為最重要的檔案，這可保證具備最高層級的保護，而不受未經授權的存取。 這些通常是應該只有少數人能存取的檔案。 例如，公司的特色食品配方指示或在指定日期之前不應該公開的收購計劃。

指示適用於下列一組情況：

-   您已找到少部分要保護的檔案。

-   檔案會採用支援 Rights Management Office 的其中一種檔案格式。 如果檔案採用其他檔案格式 (例如 CAD 檔案)，確保這些格式都支援 Azure RMS，並且您將部署原生支援 Azure RMS 的應用程式。 如需詳細資訊，請參閱[應用程式如何支援 Azure Rights Management Service](../understand-explore/applications-support.md)。

-   檔案包含應該僅供少數人存取的高度機密、敏感性資訊。

-   對這些人來說，需要網際網路連線來授權對檔案的每個個別存取是可接受的取捨，因為它提供更高的安全性。

-   這些人不需要與其他人進一步分享這項資訊，但是它們可以修改資訊並儲存變更。

-   系統管理員必須能夠追蹤何時、誰正在存取檔案，並在必要時撤銷存取權。

## 部署指示
![Azure RMS 快速部署的系統管理員指示](../media/AzRMS_AdminBanner.png)

請確定符合下列需求，然後依照支援程序的指示，再繼續進行使用者文件。

## 此案例的需求
針對此案例，必須滿足下列條件：

|需求|如果需要更多資訊|
|---------------|--------------------------------|
|備妥 Office 365 或 Azure Active Directory 的帳戶與群組：<br /><br />名為 **[特殊權限存取]** 的擁有郵件功能的群組，其中包含一些應該存取這些高度機密文件的人員。<br /><br />名為 **[IT 規範管理員]** 的擁有郵件功能的群組，其中包含工作包括 eDiscovery、監視和稽核的人員。<br /><br />- 擁有郵件功能的群組 (名為 **[RMS 系統管理員]**)，所有會設定 Azure RMS 的系統管理員都是這個群組的成員|[準備 Azure Information Protection](../plan-design/deployment-roadmap.md)|
|Azure Rights Management 已啟動|[啟用 Azure Rights Management](../deploy-use/activate-service.md)|
|您已如下所述設定自訂範本|[設定 Azure Rights Management Service 的自訂範本](../deploy-use/configure-custom-templates.md)|
|Rights Management 共用應用程式已部署到您的 Windows 電腦，使得您可以就地保護這些檔案，如下一節中所述|[下載及安裝 Rights Management 共用應用程式](../rms-client/install-sharing-app.md)|
|授權的使用者擁有最低版本的 Office 2013|如果使用者有 Office 2010，他們也必須安裝 Rights Management 共用應用程式。|
|您的 Azure RMS 訂用帳戶包含文件追蹤|如果您的 Azure RMS 訂用帳戶不包含文件追蹤和撤銷，您將無法使用文件追蹤網站來查看誰正在存取這些文件，並在必要時撤銷存取。 在此情況下，請購買支援文件追蹤的訂用帳戶，或接受這項限制。 您也可以考慮 Azure RMS 的[使用量記錄](../deploy-use/log-analyze-usage.md)功能，它可以提供資訊，例如何時、誰存取了每個檔案，來協助您偵測潛在可疑的行為。<br /><br />請查看 Azure Information Protection [定價頁面](https://go.microsoft.com/fwlink/?LinkId=827589)中的訂用帳戶資訊。|

### 設定自訂範本

1.  在 Azure 傳統入口網站中：為 Azure Rights Management 建立新的自訂範本，其中包含下列值及設定：

    -   名稱︰**特殊權限存取**

    -   權限︰授與**特殊權限存取**擁有郵件功能的群組**合著者**權限

    -   範圍︰選取**特殊權限存取**擁有郵件功能的群組，**IT 規範理員**擁有郵件功能的群組，以及 **RMS 系統管理員**擁有郵件功能的群組。

    -   離線存取：**只有使用網際網路連線才能使用內容**

2.  發行新範本。

### 就地保護檔案

1.  在 [檔案總管] 中，瀏覽至包含要保護之檔案的第一個資料夾︰

    -   如果您將保護資料夾中的所有檔案，請選取資料夾。

    -   如果您僅將保護資料夾中的部分檔案，請多重選取要保護的檔案。

2.  以滑鼠右鍵按一下，選取 [利用 RMS 保護]，然後選取 [就地保護]。

3.  選取 [特殊權限存取]。

4.  系統不會提示您提供認證。 等待檔案受保護，然後在看到 [檔案已受保護] 頁面時，按一下 [關閉]。

5.  如果您其他資料夾中有更多要保護的檔案，請對每個資料夾重複步驟 1 到 4。

如需就地保護檔案的詳細資訊，請參閱[使用 Rights Management 共用應用程式保護裝置上的檔案 (就地保護)](../rms-client/sharing-app-protect-in-place.md)

> [!TIP]
> 如果要保護的檔案數目對此手動程序而言過多，請考慮使用 [RMS 保護工具](https://www.microsoft.com/en-us/download/details.aspx?id=47256)利用範本來大量保護。

### 必要時若要監視，請撤銷檔案的存取

1.  在 [檔案總管] 中，以滑鼠右鍵按一下受保護的檔案，選取 [利用 RMS 保護]，然後選取 [追蹤使用情況]。

2.  如果出現提示，請登入以存取文件追蹤網站。

3.  檢查誰存取了檔案和您保護的其他檔案，特別注意失敗的嘗試中是否指出可疑的行為。 若適當，您可以撤銷對每個檔案的存取權。

## 使用者文件指示
此案例因為這些檔案不需要使用者執行任何特殊的動作，所以沒有特定的使用者指示。 這些檔案已由您保護並且將受您監視。 不過，您可能需要通知這些使用者和您的支援人員哪些檔案受到保護，以及這如何可限制文件的使用。 例如，如果授權的使用者沒有網際網路連線，她將無法開啟檔案。

使用下列範本，將公告複製並貼到使用者通訊上，然後進行這些修改︰

1.  提供檔案的實際名稱，或是使用授權使用者可以了解的明確參考。

2.  將 *&lt;連絡人詳細資料&gt;* 替換成這些使用者可以連絡技術支援人員或 IT 部門的方法，以獲得符合這些文件重要性的呈報支援管道的指示。 例如，對高嚴重性支援電話提供 24 小時制的電話號碼。

3.  對公告進行您想要的任何其他修改，然後將其傳送給這些使用者。

範例文件會顯示這項公告在您的自訂之後，就使用者看來的可能外觀如何。

![Azure RMS 快速部署的範本使用者文件](../media/AzRMS_UsersBanner.png)

### IT 公告︰保護 &lt;組織名稱&gt; 的最機密文件。
下列檔案現在會套用極高的保護層級，使得只有 &lt;受限制的使用者&gt; 可以存取及變更這些檔案。 為了要協助保護檔案免於未經授權的存取，每次您開啟這些檔案時，您的應用程式會自動要求授權，因此您現在必須具有檔案的網際網路連線，而且可能會提示您輸入認證︰

-   &lt;最機密文件，類型或位置 1&gt;

-   &lt;最機密文件，類型或位置 2&gt;

-   &lt;最機密文件，類型或位置 3&gt;

**需要協助嗎？**

-   如果您無法存取這些檔案，或如果您注意到 &lt;動作和連絡人的詳細資料&gt; 檔案中有可疑的變更。

#### 自訂使用者文件的範例
![Azure RMS 快速部署的範例使用者文件](../media/AzRMS_ExampleBanner.png)

##### IT 公告︰保護 VanArsdel 的最高層機密文件
下列檔案現在會套用極高的保護層級，使得只有此電子郵件訊息中的 [收件者] 行上的人員可以存取及變更這些檔案。 為了要協助保護檔案免於未經授權的存取，每次您開啟這些檔案時，您的應用程式會自動要求授權，因此您現在必須具有網際網路連線才能開啟檔案，而且可能會提示您輸入認證︰

-   代碼名稱「水星」的設計規格

-   代碼名稱「木星」的設計規格

-   代碼名稱「土星」的設計規格

-   代碼名稱「海王星」的設計規格

**需要協助嗎？**

-   如果您無法存取這些檔案，或如果您在檔案中注意到可疑的變更，請撥打 IT 部門在受保護的電子郵件訊息中傳送給您的 24 小時支援呈報專線。




<!--HONumber=Sep16_HO4-->


