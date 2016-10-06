---
title: "案例 - 主管安全地交換機密資訊 | Azure Information Protection"
description: "此案例和支援的使用者文件使用 Azure Rights Management 保護，讓主管可以安全地互換電子郵件與電子郵件附件，並有原則會自動限制主管的存取，完全不需要他們採取任何特殊動作。"
author: cabailey
manager: mbaldwin
ms.date: 09/25/2016
ms.topic: get-started-article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: e18cf5df-859e-4028-8d19-39b0842df33d
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: b61b7068e67103c45aea139cf95dacb851fe70e2
ms.openlocfilehash: fb25a5f97580e7d912016bbeb304e6470f8cbba0


---

# 案例 - 主管安全地交換機密資訊

>*適用於︰Azure Information Protection、Office 365*

此案例和支援的使用者文件使用 Azure Information Protection 的 Azure Rights Management 技術，讓主管可以安全地互換電子郵件與電子郵件附件，並有原則會自動限制主管的存取，完全不需要他們採取任何特殊動作。 這些電子郵件及所有附件均由 Azure Rights Management 自動提供保護。

如有需要，您可以在電子郵件訊息主旨中加入規則的例外狀況，例如 DNP (「不保護」) 的縮寫，以便在主管需要將未受保護的電子郵件傳送至其他主管 (例如，用來先檢閱再轉寄給其他人) 時，讓該主管指定此選項。

指示適用於下列一組情況：

-   主管可以互相交換與對他人保密的機密資訊。

-   主管在傳送這些電子郵件時，除了必須將郵件傳送到公司電子郵件地址，而不能傳送到個人電子郵件地址之外，其餘都與一般傳送作業相同。

-   若主管需要將未受保護的電子郵件訊息傳送給其他主管，可以自行覆寫規則。

## 部署指示
![Azure RMS 快速部署的系統管理員指示](../media/AzRMS_AdminBanner.png)

請確定符合下列需求，然後依照支援程序的指示，再繼續進行使用者文件。

## 此案例的需求
此案例的指示要能運作，必須滿足下列條件：

|需求|如果需要更多資訊|
|---------------|--------------------------------|
|備妥 Office 365 或 Azure Active Directory 的帳戶與群組：<br /><br />- 擁有郵件功能的群組 (名為 **[主管]**)，所有主管都是這個群組的成員<br /><br />- 擁有郵件功能的群組 (名為 **[RMS 系統管理員]**)，所有會設定 Azure RMS 的系統管理員都是這個群組的成員|[準備 Azure Information Protection](../plan-design/prepare.md)|
|您的 Azure Information Protection 租用戶金鑰由 Microsoft 管理；您不會使用 BYOK|[規劃及實作 Azure Information Protection 租用戶金鑰](../plan-design/plan-implement-tenant-key.md)|
|Azure Rights Management 已啟動|[啟用 Azure Rights Management](../deploy-use/activate-service.md)|
|下列其中一個組態：<br /><br />- Azure Rights Management 會啟用 Exchange Online<br /><br />- RMS 連接器已針對 Exchange 內部部署安裝和設定|針對 Exchange Online︰請參閱 [Exchange Online：IRM 組態](../deploy-use/configure-office365.md#exchange-online-irm-configuration)資訊。<br /><br />針對 Exchange 內部部署：[部署 Azure Rights Management 連接器](../deploy-use/deploy-rms-connector.md)|
|您已如下所述設定自訂範本|[設定 Azure Rights Management 的自訂範本](../deploy-use/configure-custom-templates.md)|
|您已如本文稍後所述設定 IRM 的傳輸保護規則|若為 Exchange Online：[郵件流程或傳輸規則](https://technet.microsoft.com/library/jj919238(v=exchg.150).aspx)<br /><br />針對 Exchange 2013：[建立傳輸保護規則](https://technet.microsoft.com/en-us/library/dd302432(v=exchg.150))<br /><br />針對 Exchange 2010：[建立傳輸保護規則](https://technet.microsoft.com/library/dd302432(v=exchg.141))|

### 設定主管的自訂範本

1.  在 Azure 傳統入口網站中：為 Azure Rights Management 建立新的自訂範本，其中包含下列值及設定：

    -   名稱： **主管**

    -   權限：將**共同擁有者**權限授與具備郵件功能的**主管**群組

    -   範圍︰選取具備郵件功能的 [主管] 群組及具備郵件功能的 [RMS 系統管理員] 群組。

2.  發行新範本。

3.  僅適用於 Exchange Online︰使用 Exchange Online 的 Windows PowerShell 命令來重新整理範本：

    ```
    Import-RMSTrustedPublishingDomain -Name "RMS Online -1" -RefreshTemplates -RMSOnline
    ```

### 設定 IRM 的傳輸規則

-   若要使用下列設定建立傳輸規則，請使用資料表中參考的 Exchange 文件的程序資訊︰

    -   名稱：**將主管範本套用至主管電子郵件**

    -   指定 [主管] 群組做為規則和其他條件的寄件者和收件者。

    -   對於動作，選取 [將權限保護套用到具有下列條件的郵件]，然後選取已設定的 [主管] 範本。

    -   在主旨中加入 **DNP** (「不保護」的縮寫) 的例外狀況，或選擇用來識別此例外狀況的文字。

    -   請確定為 [強制] 設定規則。

## 使用者文件指示
除非您想要提供如何指定 **DNP**，或在電子郵件主旨中選擇例外狀況文字或片語的說明，否則此案例沒有特定的使用者程序指示，因為不需要主管執行任何特殊的動作來保護其所接收及傳送的電子郵件。 電子郵件訊息及所有附件均會自動受到保護，只允許 [主管] 群組的成員進行存取。

但您可能需要告知主管與技術支援人員這些電子郵件會自動受到保護，以及他們在使用這類電子郵件時的限制。 例如若將這類電子郵件或附件轉寄給他人，他人可能無法順利閱讀。 如果您設定 DNP (或同等權限) 例外狀況，請確定技術服務人員知道這項組態，讓主管可以自行覆寫規則，而不需要 Exchange 系統管理員的動作。

使用下列範本，將公告複製並貼到使用者通訊上，然後進行這些修改以反映您的環境︰

1.  以您的組織名稱取代 *&lt;組織名稱&gt;* 的執行個體。

2.  如果您從 DNP 選擇免除的不同字串，請據以取代該值與說明。

3.  以您組織的電子郵件網域名稱取代 *&lt;電子郵件網域&gt;*。

4.  將*&lt;連絡人詳細資料&gt;* 取代為您的使用者可以與技術支援人員連絡的指示，例如網站連結、電子郵件地址或電話號碼。

5.  對公告進行您想要的任何其他修改，然後將其傳送給這些使用者。

範例文件會顯示這項公告在您的自訂之後，就使用者看來的可能外觀如何。

![Azure RMS 快速部署的範本使用者文件](../media/AzRMS_UsersBanner.png)

### IT 宣告：&lt;組織名稱&gt; 的主管電子郵件現在會自動受到保護
從現在起，當您傳送電子郵件給公司的另一位 &lt;組織名稱&gt; 的主管時，電子郵件及任何附件的內容都會自動受到保護，只有公司的該名收件主管才能存取，進而閱讀其資訊、列印、複製其中的內容及執行其他作業等等。 當您將電子郵件訊息轉寄給其他人或儲存附件時，也同樣會套用此限制。 此項保護有助於防止機密和敏感資訊的資料遺失。

請注意，若您希望 &lt;組織名稱&gt; 之主管以外的他人也能閱讀及編輯這些電子郵件中傳送的資訊，您必須個別傳送電子郵件給這些人。 或者，若要覆寫自動保護，請在電子郵件訊息主旨中的任何位置輸入字母 **DNP** (做為「不保護」的縮寫)。

將公司機密資訊傳送給另一位 &lt;組織名稱&gt; 的主管時，請務必傳送到該主管的公司電子郵件地址 (*名稱*@&lt;電子郵件網域&gt;)，而不是個人電子郵件地址。

**需要協助嗎？**

-   請連絡技術支援人員：&lt;連絡人詳細資料&gt;

### 範例使用者文件
![Azure RMS 快速部署的範例使用者文件](../media/AzRMS_ExampleBanner.png)

#### IT 公告：VanArsdel 主管電子郵件現在會自動施以保護
從現在起，當您傳送電子郵件給公司的另一位 VanArsdel 主管時，電子郵件及任何附件的內容都會自動施以保護，只有公司的該名收件主管才能存取，進而閱讀其資訊、列印、複製其中的內容及執行其他作業等等。 當您將電子郵件訊息轉寄給其他人或儲存附件時，也同樣會套用此限制。 此項保護有助於防止機密和敏感資訊的資料遺失。

請注意，若您希望 VanArsdel 主管以外的他人也能閱讀及編輯這些電子郵件中傳送的資訊，您必須個別傳送電子郵件給這些人。 或者，若要覆寫自動保護，請在電子郵件訊息主旨中的任何位置輸入字母 **DNP** (做為「不保護」的縮寫)。

將公司機密資訊傳送給另一位 VanArsdel 主管時，請務必傳送到該主管的公司電子郵件地址 (*name*@vanarsdelltd.com)，而不是個人電子郵件地址。

**需要協助嗎？**

-   請連絡技術支援人員：helpdesk@vanarsdelltd.com




<!--HONumber=Sep16_HO4-->


