---
# required metadata

title: 案例 - 將工作資料夾設定為持續保護 | Azure RMS
description:
keywords:
author: cabailey
manager: mbaldwin
ms.date: 05/20/2016
ms.topic: get-started-article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 1f189345-a69e-4bf5-8a45-eb0fe5bb542b

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: esaggese
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# 案例 - 將工作資料夾設定為持續保護

*適用於︰Azure Rights Management、Office 365*

此案例和支援的使用者文件使用 Azure Rights Management 將保護持續套用至[工作資料夾](https://technet.microsoft.com/library/dn265974.aspx)中的 Office 文件。 工作資料夾使用執行 Windows Server 的檔案伺服器角色服務，可提供一致的方式讓使用者從他們的電腦和裝置存取工作檔案。 雖然工作資料夾提供它自己的加密來保護檔案，如果將檔案移至工作資料夾環境以外的地方，便會失去這項保護。 例如，使用者將已同步的檔案複製並將儲存到不在您 IT 部門控制下的存放裝置，或是以電子郵件傳送給其他人。

Azure Rights Management 提供的額外保護，可防止檔案被組織外的人員檢視，有助於避免資料意外遺失。 若要這樣做，您可以使用內建的預設權限原則範本之一。 不過，部署本案例之前，請考慮使用者是否可能需要合法與組織外的人共用這些檔案。 例如，使用者草擬價格表之後，以電子郵件將最終版本寄給另一個組織中的客戶。 當您在工作資料夾使用預設的 Rights Management 範本時，這名在其他組織中的客戶無法讀取這份以電子郵件寄送的文件。 您可以建立自訂範本，讓使用者將新的權限原則套用至檔案 (會將針對所有員工的原始限制改為限制其電子郵件中指定的人員)，以符合這項需求。

> [!NOTE]
> 當您使用為此案例記載的自訂範本，雖然使用者可以刻意與您未在範本中定義的人共用檔案，您以 Azure Rights Management 套用的額外保護會提供許多優點。 如果內容被移到工作資料夾界限之外，這項額外的保護可防止資料意外遺失，因為不論內容是靜止不動或是已傳送，依然會防範未經授權的使用者。 例如，使用者遺失了使用工作資料夾的裝置或裝置遭竊，又或者，透過不安全的基礎結構傳送與此裝置同步的內容。
> 
> 如果使用者使用 Rights Management 共用應用程式的「分享受保護的內容」功能，與另一個組織中的某個人共用內容，而這個使用者以自己的保護原則取代原始保護。 結果，內容仍會防範未經授權的存取，只有使用者指定的人可以存取此內容。

您可以對使用者的工作資料夾中的所有 Office 文件套用這項持續保護，或只套用至包含機密或高商業影響資料的檔案。

指示適用於下列一組情況：

-   您想要使用持續保護來保護的工作資料夾檔案是 Office 檔案。 這些檔案受到 Azure Right Management 的原生保護，不會變更副檔名或需要用不同的工作流程來開啟它們。

-   您想要對使用者的工作資料夾中的所有 Office 檔案套用持續保護，或套用至從 Windows Server 中「檔案伺服器資源管理員」使用「檔案分類基礎結構」識別的選擇性檔案。

-   針對必須與權限原則範本中未指定的人共用的檔案 (例如，另一個組織中的使用者)，使用者必須套用新的權限原則來取代原始的權限原則保護。

## 部署指示
![Azure RMS 快速部署的系統管理員指示](../media/AzRMS_AdminBanner.png)

請確定符合下列需求，然後依照支援程序的指示，再繼續進行使用者文件。

## 此案例的需求
此案例的指示要能運作，必須滿足下列條件：

|需求|如果需要更多資訊|
|---------------|--------------------------------|
|Azure Rights Management 已啟動|[啟用 Azure Rights Management](https://technet.microsoft.com/library/jj658941.aspx)|
|您已同步處理您的內部部署 Active Directory 使用者帳戶與 Azure Active Directory 或 Office 365，包括其電子郵件地址。 這對使用工作資料夾的所有使用者為必要。|[準備 Azure Rights Management](https://technet.microsoft.com/library/jj585029.aspx)|
|發生下列情形之一：<br /><br />- 若要對不允許使用者套用新權限原則的所有使用者使用預設範本︰您沒有封存預設範本 **[&lt;組織名稱&gt; - 機密]**<br /><br />- 若要使用適合讓使用者套用新權限原則的自訂範本︰使用接下來的指示來建立自訂範本|[設定 Azure Rights Management 的自訂範本](https://technet.microsoft.com/library/dn642472.aspx)|
|已安裝 Rights Management 連接器，且已授權其使用 Windows Server 電腦，並設定為 **FCI 伺服器**角色。|[部署 Azure Rights Management 連接器](https://technet.microsoft.com/library/dn375964.aspx)|
|Rights Management 共用應用程式已部署至執行 Windows 的使用者電腦|[自動部署 Microsoft Rights Management 共用應用程式](https://technet.microsoft.com/library/dn339003%28v=ws.10%29.aspx)|

### 設定自訂權限原則範本，讓使用者可以在組織外共用工作資料夾的檔案

1.  登入 Azure 傳統入口網站，瀏覽至 Azure Rights Management 範本。

2.  複製 **[&lt;組織名稱&gt; - 機密]** 範本，並提供此工作資料夾案例的名稱和描述。 我們的建議如下：

    -   名稱︰**工作資料夾所保護的內容**

    -   描述︰**此內容受到工作資料夾的保護，並只限公司員工存取。若要與組織外的人共用此內容，將文件附加到電子郵件，並使用「分享受保護的內容」功能。**

3.  在 [權限] 頁面︰

    -   將現有的權限從 [自訂] 變更為 [共同擁有者]。

4.  在 [設定] 頁面︰

    -   請確定 [狀態] 設為 [發佈]

    -   在 [名稱和描述]，刪除您未使用之語言項目。 針對您使用的語言，使用指定的語言更新 [名稱] 和 [描述]，使其符合您提供給此範本的名稱和描述。

5.  儲存範本。

### 設定工作資料夾套用持續保護至 Office 檔案

1.  為您的使用者實作工作資料夾，使本機儲存的檔案與檔案伺服器資料夾同步處理，這稱為*同步共用*。 檔案伺服器上的同步共用，不能位在執行 Rights Management 連接器的同一伺服器上。

    此解決方案需要伺服器管理員中的「工作資料夾」角色，以用於「檔案和存放服務」角色。 檔案伺服器必須執行最低 Windows Server 2012 R2 版本，且此檔案伺服器可以是內部部署或在 Azure 中的虛擬機器。 如需工作資料夾的詳細資訊，請參閱[工作資料夾概觀](https://technet.microsoft.com/library/dn265974.aspx)。

    如需部署指示，請參閱[部署工作資料夾](https://technet.microsoft.com/library/dn528861.aspx)。 請確定您選取了內建的加密 ([加密工作資料夾] 選項)，系統會套用它以及 Azure Rights Management 加密。 此外：

    -   當您在同步伺服器上繫結 SSL 憑證 (步驟 4)︰使用 netsh 命令 (而不是 IIS 管理主控台) 將憑證繫結至預設網站 HTTPS 介面。

    -   若要避免使用者遇到工作資料夾安裝錯誤「**套用安全性原則時發生問題**」，以及它們必須是在加入網域的電腦上的本機系統管理員的要求︰使用 [Set-SyncShare](https://technet.microsoft.com/library/dn296649%28v=wps.630%29.aspx) Cmdlet 搭配 PasswordAutolockExcludeDomain 參數，並指定這些電腦所在的網域名稱 (例如 contoso.com)。

2.  完成 Azure Rights Management 連接器的設定：

    1.  使用「檔案伺服器資源管理員」，建立會將同步共用資料夾識別為範圍的檔案管理工作。

    2.  在這個操作中，選擇 [RMS 加密]，然後選取範本︰

        -   如果您因為不想讓使用者能夠與組織外的人共用檔案而未建立自訂範本，請選取 **[&lt;組織名稱&gt; - 機密]** 範本名稱。 例如，**VanArsdel, Ltd - 機密**。

        -   如果您使用上述指示建立自訂範本，請選取此範本。 例如，**工作資料夾所保護的內容**。

    3.  指定一個允許 Azure Rights Management 用充裕的時間加密所有 Office 檔案的排程，並指定 [持續在新檔案上執行] 選項。

3.  若要手動測試此設定，請確定該資料夾包含一些 Office 檔案，然後使用 [立即執行檔案管理工作] 選項，並選取 [等待工作完成]。

    等候 [正在執行檔案管理工作]  對話方塊關閉，然後再檢視自動顯示報告中的結果。 您應該會在 [檔案]  欄位中看到您所選擇的資料夾中的檔案數目。 確認您所選擇的資料夾中的檔案現在受到 Azure Rights Management 保護。 例如，開啟檔案，並確認您在文件頂端看到的資訊橫幅顯示 Rights Management 範本的名稱和描述。

4.  如果您決定要使用「檔案分類基礎結構」來選擇性地保護檔案，請設定您的分類規則和排程，然後修改檔案管理工作，加入此分類屬性做為條件。

## 使用者文件指示
如果您使用 Azure Rights Management 所保護的檔案不需要與組織外的人共用，您不必為使用者提供使用工作資料夾之指示以外的指示。 當使用者開啟受 Azure Rights Management 和預設範本保護的檔案時，檔案會在 Office 中如常開啟，唯一的差別在於使用者可能會看到要求他們進行驗證的提示，而且他們會在文件頂端看到資訊列，通知他們內容包含專屬的資訊僅適用於內部使用者。

如果您如本案例所述設定自訂範本，使用者會在資訊列中看到範本描述︰**此內容受到工作資料夾的保護，並只限公司員工存取。。若要與組織外的人共用此內容，將文件附加到電子郵件，並使用「分享受保護的內容」功能。** 雖然這項描述會提供摘要，說明如何將檔案共用至組織外，使用者可能會需要詳細如何執行這項操作的說明，尤其是前幾次這麼做時。 若要支援此後續案例，使用[案例 - 與其他組織的使用者共用 Office 檔案](scenario-share-office-file-externally.md)中的系統管理員和使用者指示。

> [!TIP]
> 如果您決定不使用這些指示中的自訂範本，因為不想讓使用者在沒有 IT 監看的情況下與組織外部共用檔案，請讓技術支援人員知道，如此一來，如果共用的需求是合法的，便可用任何最適合您企業的機制來達成。 例如，某位[進階使用者](https://technet.microsoft.com/library/mt147272.aspx)可能會套用新範本至內容，以授予「完整控制」權限給要求的使用者，好讓這位使用者接下來可以使用「分享受保護的內容」功能。
> 
> 一段時間後，如果您發現有許多這類要求，您可能會決定針對此種案例定義自己的自訂範本，以授予特定使用者 (如管理員、技術服務人員)「共同擁有者」選項，並授予標準使用者「共同作者」或任何您認為適當的[權限](https://technet.microsoft.com/library/mt169423.aspx)。



<!--HONumber=May16_HO3-->


