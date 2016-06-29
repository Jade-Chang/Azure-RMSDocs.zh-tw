---
# required metadata

title: 設定 Azure Rights Management 連接器的伺服器 | Azure RMS
description:
keywords:
author: cabailey
manager: mbaldwin
ms.date: 06/08/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 75846ee1-2370-4360-81ad-e2b6afe3ebc9

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: esaggese
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# 設定 Azure Rights Management 連接器的伺服器

*適用於︰Azure Rights Management、Windows Server 2012、Windows Server 2012 R2*


使用下列資訊可協助您設定將使用 Azure Rights Management (RMS) 連接器的內部部署伺服器。 這些程序涵蓋[部署 Azure Rights Management 連接器](deploy-rms-connector.md)的步驟 5。

開始之前，請確定已安裝並設定 RMS 連接器，並檢查將使用連接器之伺服器所適用的任何[必要條件](deploy-rms-connector.md#prerequisites-for-the-rms-connector)。


## 設定伺服器使用 RMS 連接器
安裝並設定好 RMS 連接器之後，即準備好要設定將會使用 Rights Management 並以該連接器連線至 Azure RMS 的內部部署伺服器。 這表示要設定下列伺服器：

-   **若為 Exchange 2016 和 Exchange 2013**：用戶端存取伺服器和信箱伺服器

-   **若為 Exchange 2010**：用戶端存取伺服器和集線傳輸伺服器

-   **若為 SharePoint**：前端 SharePoint 網頁伺服器，包括裝載中央管理伺服器者

-   **若為檔案分類基礎結構**：已安裝檔案資源管理員的 Windows Server 電腦

此設定需要登錄設定。 若要這樣做，您有兩個選項︰[為 Microsoft RMS 連接器使用伺服器設定工具以自動執行] 或 [藉由編輯登錄手動執行]。

---

**為 Microsoft RMS 連接器使用伺服器設定工具以自動執行：**

- 優點：

    - 不需要直接編輯登錄。 系統會使用指令碼自動執行此工作。

    - 無需執行 Windows PowerShell 指令程式即可取得您的 Microsoft RMS URL。

    - 必要條件是如果您在本機上執行，則自動為您檢查 (但不會自動補救)。

缺點：

- 執行工具時，必須連線到已執行 RMS 連接器的伺服器。

---

**藉由編輯登錄手動執行：**

- 優點：

    - 無需連線至執行 RMS 連接器的伺服器。

- 缺點：

    - 更多容易出錯的系統管理負擔。

    - 您必須執行 Windows PowerShell 命令來取得您的 Microsoft RMS URL。

    - 您必須一律自行檢查所有必要條件。


---

> [!IMPORTANT] 在這兩種情況下，您都必須手動安裝任何必要條件，並設定 Exchange、SharePoint 和檔案分類基礎結構來使用 Rights Management。

對大多數組織而言，使用 Microsoft RMS 連接器的伺服器設定工具以自動設定是較好的選項，因為相較於手動設定，自動設定提供更好的效率和可靠性。

在這些伺服器上進行設定變更後，如果這些伺服器是執行 Exchange 或 SharePoint，而先前已設定為使用 AD RMS，則您必須重新啟動這些伺服器。 如果您是首次設定這些伺服器使用 Rights Management，則不需要重新啟動這些伺服器。 但對於使用檔案分類基礎結構的檔案伺服器，則在這些檔案伺服器上進行設定變更後，務必要重新啟動檔案伺服器。

### 如何使用 Microsoft RMS 連接器的伺服器設定工具

1.  如果尚未下載 Microsoft RMS 連接器 (GenConnectorConfig.ps1) 的伺服器設定工具的指令碼，請從 [Microsoft 下載中心](http://go.microsoft.com/fwlink/?LinkId=314106)取得。

2.  在將執行工具的電腦上儲存 GenConnectorConfig.ps1 檔案。 如果您將會在本機執行此工具，此本機必須是您想要設定來與 RMS 連接器通訊的伺服器。 否則，您可以將它儲存在任何電腦上。

3.  決定如何執行工具：

    -   **本機瀏覽**：您可以在要設定來與 RMS 連接器通訊的伺服器上，以互動方式執行此工具。 這對一次性設定 (例如測試環境) 很有用。

    -   **軟體部署**：您可執行工具來產生登錄檔，接著使用支援軟體部署的系統管理應用程式部署至一或多個相關伺服器，例如 System Center Configuration Manager。

    -   **群組原則**：您可以執行工具來產生指令碼，將指令碼提供給系統管理員，使其對要設定的伺服器建立群組原則物件。 此指令碼會為要設定的每種伺服器類型建立一個群組原則物件，系統管理員接著可將其指派給相關伺服器。

    > [!NOTE]
    > 此工具會設定本節開頭所列、將會與 RMS 連接器通訊的伺服器。 請勿在執行 RMS 連接器的伺服器上執行這項工具。

4.  使用 [以系統管理員身分執行] 選項啟動 Windows PowerShell，並使用 Get-help 命令來閱讀如何為您所選擇設定方法使用工具的指示：

    ```
    Get-help .\GenConnectorConfig.ps1 -detailed
    ```

當執行指令碼時，您必須為組織輸入 RMS 連接器的 URL。 輸入通訊協定首碼 (HTTP:// 或 HTTPS://)，及您在 DNS 中為連接器的負載平衡位址所定義的連接器名稱。 例如，https://connector.contoso.com。 工具接著會使用該 URL 來連線執行 RMS 連接器的伺服器，並取得用來建立必要設定的其他參數。

> [!IMPORTANT] 當您執行這項工具時，請確定您指定的是貴組織之負載平衡型 RMS 連接器的名稱，而不是執行 RMS 連接器服務之單一伺服器的名稱。

如需每種服務類型的特定資訊，請使用下列各節：

-   [設定 Exchange 伺服器使用連接器](#configuring-an-exchange-server-to-use-the-connector)

-   [設定 SharePoint 伺服器使用連接器](#configuring-a-sharepoint-server-to-use-the-connector)

-   [設定檔案分類基礎結構的檔案伺服器以使用連接器](#configuring-a-file-server-for-file-classification-infrastructure-to-use-the-connector)

> [!NOTE]
> 設定這些伺服器來使用連接器後，這些伺服器上本機安裝的用戶端應用程式可能無法使用 RMS。 發生這種情況時，可能是因為應用程式嘗試使用連接器而非直接使用 RMS，而這是不受支援的作法。
>
> 此外，如果 Office 2010 是安裝在 Exchange 伺服器的本機，則在設定伺服器使用連接器之後，用戶端應用程式的 IRM 功能可能可以從該電腦運作，但是這樣的做法並不受支援。
>
> 在兩種情況下，您必須在未設定使用連接器的不同電腦上安裝用戶端應用程式。 接著它們會正確且直接使用 RMS。

## 設定 Exchange 伺服器使用連接器
下列 Exchange 角色會與 RMS 連接器通訊：

-   若為 Exchange 2016 和 Exchange 2013：用戶端存取伺服器和信箱伺服器

-   若為 Exchange 2010：用戶端存取伺服器和集線傳輸伺服器

若要使用 RMS 連接器，這些執行 Exchange 的伺服器必須執行下列其中一個軟體版本：

-   Exchange Server 2016

-   Exchange Server 2013 (含 Exchange 2013 累積更新 3)

-   Exchange Server 2010 (含 Exchange 2010 Service Pack 3 彙總套件更新 6)

您亦將需於伺服器上安裝包含支援 RMS 密碼編譯模式 2 的 RMS 用戶端版本。 Windows Server 2008 所支援的最低版本內含於 Hotfix 中，該 hotfix 可從 [Windows Server 2008 R2 和 Windows Server 2008 中之 AD RMS 的 RSA 金鑰長度會增加至 2048 位元](http://support.microsoft.com/kb/2627272)下載取得。 可從 [在 Windows 7 或 Windows Server 2008 R2 中的 AD RMS 的 RSA 金鑰長度增加至 2048 位元](http://support.microsoft.com/kb/2627273)下載 Windows Server 2008 R2 的最小版本。 Windows Server 2012 和 Windows Server 2012 R2 原生支援密碼編譯模式 2。

> [!IMPORTANT]
> 若未安裝這些版本或更新版的 Exchange 和 RMS 用戶端，您將無法設定 Exchange 使用連接器。 先確定已安裝這些版本再繼續。

### 若要設定 Exchange 伺服器使用連接器

1. 確定 Exchange 伺服器有權使用 RMS 連接器，方法是使用 RMS 連接器系統管理工具和[授授權伺服器使用 RMS 連接器](install-configure-rms-connector.md#authorizing-servers-to-use-the-rms-connector)一節的資訊。 若要讓 Exchange 使用 RMS 連接器，需要此設定。

2.  在與 RMS 連接器通訊的 Exchange 伺服器角色上，執行下列其中一項動作：

    -   執行 Microsoft RMS 連接器的伺服器設定工具。 如需詳細資訊，請參閱本文的[如何使用 Microsoft RMS 連接器的伺服器設定工具](#how-to-use-the-server-configuration-tool-for-microsoft-rms-connector)。

        例如，在本機上執行工具以設定執行 Exchange 2016 或 Exchange 2013 的伺服器：

        ```
        .\GenConnectorConfig.ps1 -ConnectorUri https://rmsconnector.contoso.com -SetExchange2013
        ```

    -   使用 [RMS 連接器的登錄設定](rms-connector-registry-settings.md)的資訊，在伺服器上手動新增登錄設定以進行手動編輯登錄。 

3.  啟用 Exchange 中的 IRM 功能。 如需詳細資訊，請參閱 Exchange 文件庫中的[資訊版權管理程序](https://technet.microsoft.com/library/dd351212%28v=exchg.150%29.aspx)。

    > [!NOTE]
    > 根據預設，當您執行 **Set-IRMConfiguration -InternalLicensingEnabled $true** 之後，會針對 Outlook Web App 和行動裝置自動啟用 IRM，以及針對信箱啟用 IRM。 不過，系統管理員可以在不同的層級停用 IRM，例如，對於 Client Access Server、Outlook Web App 虛擬目錄或 Outlook Web App 信箱原則，以及行動裝置信箱原則。 如果使用者可以在 Outlook 用戶端中看到任何 Azure RMS 範本，但在 Outlook Web App (等候一天之後) 中或行動裝置上看不到這些範本，請檢查相關設定以確定未停用 IRM。 如需詳細資訊，請參閱 Exchange 文件中的 [啟用或停用 Client Access Server 上的資訊版權管理](https://technet.microsoft.com/library/dd876938(v=exchg.150).aspx)。 


## 設定 SharePoint 伺服器使用連接器
下列 SharePoint 角色會與 RMS 連接器通訊：

-   前端 SharePoint 網頁伺服器，包括裝載中央管理伺服器者

若要使用 RMS 連接器，這些執行 SharePoint 的伺服器必須執行下列其中一個軟體版本：

-   SharePoint Server 2016

-   SharePoint Server 2013

-   SharePoint Server 2010

執行 SharePoint 2016 或 SharePoint 2013 的伺服器也必須執行支援 RMS 連接器的 MSIPC 用戶端 2.1 版本。 若要確保您具有受支援的版本，請從 [Microsoft 下載中心](http://www.microsoft.com/download/details.aspx?id=38396)下載最新的用戶端。

> [!WARNING] MSIPC 2.1 用戶端有多個版本，因此請確定您具有 1.0.2004.0 版本或更新版本。
>
> 您可以檢查位於 **\Program Files\Active Directory Rights Management Services Client 2.1** 中 MSIPC.dll 的版本號碼來確認用戶端版本。 屬性對話方塊中會顯示 MSIPC 2.1 用戶端的版本號碼。

執行 SharePoint 2010 的伺服器必須安裝包含 RMS 密碼編譯模式 2 的 MSDRM 用戶端版本。 Windows Server 2008 所支援的最低版本內含於 Hotfix 中，該 hotfix 可從 [Windows Server 2008 R2 和 Windows Server 2008 中之 AD RMS 的 RSA 金鑰長度會增加至 2048 位元](http://support.microsoft.com/kb/2627272)下載取得，並可從 [Windows 7 或 Windows Server 2008 R2 中 AD RMS 的 RSA 金鑰長度增加為 2048 位元](http://support.microsoft.com/kb/2627273)下載 Windows Server 2008 R2 的最低版本。 Windows Server 2012 和 Windows Server 2012 R2 原生支援密碼編譯模式 2。

### 若要設定 SharePoint 伺服器使用連接器

1. 確定 SharePoint 伺服器有權使用 RMS 連接器，方法是使用 RMS 連接器系統管理工具和[授授權伺服器使用 RMS 連接器](install-configure-rms-connector.md#authorizing-servers-to-use-the-rms-connector)一節的資訊。 若要讓 Exchange 使用 RMS 連接器，需要此設定。

2.  在與 RMS 連接器通訊的 SharePoint 伺服器上，執行下列其中一項動作：

    -   執行 Microsoft RMS 連接器的伺服器設定工具。 如需詳細資訊，請參閱本文的[如何使用 Microsoft RMS 連接器的伺服器設定工具](#how-to-use-the-server-configuration-tool-for-microsoft-rms-connector)。

        例如，在本機上執行工具以設定執行 SharePoint 2016 或 SharePoint 2013 的伺服器：

        ```
        .\GenConnectorConfig.ps1 -ConnectorUri https://rmsconnector.contoso.com -SetSharePoint2013
        ```

    -   若是使用 SharePoint 2016 或 SharePoint 2013，請使用 [RMS 連接器的登錄設定](rms-connector-registry-settings.md) 的資訊，在伺服器上手動新增登錄設定以進行手動登錄編輯。 

3.  在 SharePoint 中啟用 IRM。 如需詳細資訊，請參閱 SharePoint 程式庫中的 [設定資訊權管理 (SharePoint Server 2010)](https://technet.microsoft.com/library/hh545607%28v=office.14%29.aspx)。

    當您遵循這些指示時，您必須設定 SharePoint 使用連接器，方法是指定 [使用此 RMS 伺服器]，然後輸入您設定的負載平衡連接器 URL。 輸入通訊協定首碼 (HTTP:// 或 HTTPS://)，及您在 DNS 中為連接器的負載平衡位址所定義的連接器名稱。 例如，如果您的連接器名稱為 https://connector.contoso.com，您的組態看起來會類似下列圖片：

    ![設定 RMS 連接器的 SharePoint Server](../media/AzRMS_SharePointConnector.png)

    在 SharePoint 伺服器陣列上啟用 IRM 後，您可對每個程式庫，使用 [程式庫設定]  頁面的 [資訊版權管理]  選項在個別程式庫上啟用 IRM。


## 設定檔案分類基礎結構的檔案伺服器以使用連接器
若要使用 RMS 連接器和檔案分類基礎結構來保護 Office 文件，檔案伺服器必須正在執行下列其中一種作業系統：

-   Windows Server 2012 R2

-   Windows Server 2012

### 若要設定檔案伺服器使用連接器

1.  確定檔案伺服器有權使用 RMS 連接器，方法是使用 RMS 連接器系統管理工具和[授授權伺服器使用 RMS 連接器](install-configure-rms-connector.md#authorizing-servers-to-use-the-rms-connector)一節的資訊。 若要讓 Exchange 使用 RMS 連接器，需要此設定。

2.  在設定來使用檔案分類基礎結構、且會與 RMS 連接器通訊的檔案伺服器上，執行下列其中一項動作：

    -   執行 Microsoft RMS 連接器的伺服器設定工具。 如需詳細資訊，請參閱本文的[如何使用 Microsoft RMS 連接器的伺服器設定工具](#how-to-use-the-server-configuration-tool-for-microsoft-rms-connector)。

        例如，在本機上執行工具以設定執行 FCI 的檔案伺服器：

        ```
        .\GenConnectorConfig.ps1 -ConnectorUri https://rmsconnector.contoso.com -SetFCI2012
        ```

    - 使用 [RMS 連接器的登錄設定](rms-connector-registry-settings.md)的資訊，在伺服器上手動新增登錄設定以進行手動編輯登錄。 

3.  建立分類規則和檔案管理工作來對文件加上 RMS 加密保護，然後指定 RMS 範本來自動套用 RMS 原則。 如需詳細資訊，請參閱 Windows Server 文件庫的 [檔案伺服器資源管理員概觀](http://technet.microsoft.com/library/hh831701.aspx) 。

## 後續步驟
您已安裝和設定 RMS 連接器，並設定伺服器使用該連接器，現在 IT 管理員和使用者可以使用 Azure RMS 來保護及取用電子郵件訊息和文件。 為了方便使用者使用，請部署 RMS 共用應用程式；該應用程式會安裝 Office 附加元件，並將新的滑鼠右鍵選項加入至 [檔案總管]。 如需詳細資訊，請參閱[Rights Management 共用應用程式系統管理員指南](../rms-client/sharing-app-admin-guide.md)。

您可以使用 [Azure Rights Management 部署藍圖](../plan-design/deployment-roadmap.md)來檢查將 [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)] 轉出給使用者和系統管理員之前，是否還需要執行其他設定步驟。

若要監視 RMS 連接器，請參閱 [Monitor the Azure Rights Management connector](monitor-rms-connector.md) (監視 Azure Rights Management 連接器)。 


<!--HONumber=Jun16_HO2-->


