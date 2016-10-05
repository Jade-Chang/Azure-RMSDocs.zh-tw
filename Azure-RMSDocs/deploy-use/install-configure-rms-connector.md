---
title: "安裝及設定 Azure Rights Management 連接器 | Azure Information Protection"
description: "協助您安裝及設定 Azure Rights Management (RMS) 連接器的資訊。 這些程序涵蓋部署 Azure Rights Management 連接器的步驟 1 到 4。"
author: cabailey
manager: mbaldwin
ms.date: 09/25/2016
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 4fed9d4f-e420-4a7f-9667-569690e0d733
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: d5b6a1fc3fa0a19f3a6b65aa7b8815eda7432cd7
ms.openlocfilehash: 4af8d8b5f95edc7bd95fda93b26da98ee00b5075


---

# 安裝和設定 Azure Rights Management 連接器

>*適用於︰Azure Information Protection、Office 365*

使用下列資訊可協助您安裝及設定 Azure Rights Management (RMS) 連接器。 這些程序涵蓋[部署 Azure Rights Management 連接器](deploy-rms-connector.md)的步驟 1 到 4。

在開始之前，請確定您已檢閱和檢查此部署的[必要條件](deploy-rms-connector.md#prerequisites-for-the-rms-connector)。


## 安裝 RMS 連接器

1.  識別要執行 RMS 連接器的電腦 (至少兩台)。 他們必須符合必要條件列示的最小規格。

    > [!NOTE]
    > 您將為每個租用戶 (Office 365 租用戶或 Azure AD 租用戶) 安裝單一 RMS 連接器 (可能由多部伺服器組成以提供高可用性)。 不像 Active Directory RMS，您無需在每個樹系中安裝 RMS 連接器。

2.  從 [Microsoft 下載中心](http://go.microsoft.com/fwlink/?LinkId=314106)下載 RMS 連接器的來源檔案。

    若要安裝 RMS 連接器，請下載 RMSConnectorSetup.exe。

    此外：

    -   若您稍後想從 32 位元電腦設定連接器，亦請下載 RMSConnectorAdminToolSetup_x86.exe。

    -   若要使用 RMS 連接器的伺服器設定工具，若要在內部部署伺服器上自動化登錄設定的設定，請另外下載 GenConnectorConfig.ps1。

3.  在要安裝 RMS 連接器的電腦上，使用系統管理員權限執行 **RMSConnectorSetup.exe** 。

4.  在 [Microsoft Rights Management 連接器設定] 頁面的 [歡迎] 頁面上，選取 [在電腦上安裝 Microsoft Rights Management 連接器] ，再按 [下一步] 。

5.  閱讀並同意 RMS 連接器授權條款，然後按 [下一步] 。

若要繼續，請輸入帳戶和密碼來設定 RMS 連接器。

## 輸入認證
設定 RMS 連接器之前，必須對具足夠權限以設定 RMS 連接器的帳戶輸入認證。 例如，您可能輸入 **admin@contoso.com**，然後指定此帳戶的密碼。

此密碼有一些字元限制。 您不得使用任何含下列字元的密碼︰連字號 ( **&** )、左角括弧 ( **[** )、右角括弧 ( **]** )、一般引號 ( **"** )，以及單引號 ( **'** )。 如果您的密碼有任何這些字元，RMS 連接器的驗證將會失敗，您會看到錯誤訊息「該使用者名稱和密碼組合不正確」，儘管您在其他案例中可以使用此帳戶和密碼成功登入。 如果您的密碼是這種情形，則使用不同帳戶，其密碼沒有任何這些特殊字元，或者重設您的密碼，讓它不具有任何這些特殊字元。

此外，如果您已實作[登入控制項](activate-service.md#configuring-onboarding-controls-for-a-phased-deployment)，請確定您指定的帳戶能夠保護內容。 比方說，如果您將保護內容的功能限制為「IT 部門」群組，則您在此處指定的帳戶必須是該群組的成員。 否則會看到錯誤訊息：**嘗試探索管理服務和組織的位置失敗。請確定已為您的組織啟用 Microsoft Rights Management 服務。**

您可使用具下列其中一種權限的帳戶：

-   **租用戶的全域管理員**︰您的 Office 365 租用戶或 Azure AD 租用戶的全域管理員帳戶。

-   **Azure Rights Management 全域管理員**︰已獲指派為 Azure RMS 全域管理員角色的 Azure Active Directory 帳戶。

-   **Azure Rights Management 連接器系統管理員**：具有安裝並管理組織之 RMS 連接器權限的 Azure Active Directory 帳戶。

    > [!NOTE]
    > 您可以使用 Azure RMS 的 [Add-AadrmRoleBasedAdministrator](https://msdn.microsoft.com/library/dn629417.aspx) Cmdlet，將 Azure Rights Management 全域管理員角色和 Azure Rights Management 連接器系統管理員角色指派給帳戶。
    > 
    > 若要使用最低權限來執行 RMS 連接器，請執行下列動作，建立此用途專用的帳戶，然後為其指派 Azure RMS 連接器系統管理員角色︰
    >
    > 1.  如果尚未這樣做，請下載並安裝 Windows PowerShell for Rights Management。 如需詳細資訊，請參閱[針對 Azure Rights Management 安裝 Windows PowerShell](install-powershell.md)。
    >
    >     使用 [以系統管理員身分執行] 命令啟動 Windows PowerShell，並使用 [Connect-AadrmService](https://msdn.microsoft.com/library/azure/dn629415.aspx) 命令連接至 Azure RMS 服務：
    >
    >     ```
    >     Connect-AadrmService                   //provide Office 365 tenant administrator or Azure RMS global administrator credentials
    >     ```
    > 2.  然後執行 [Add-AadrmRoleBasedAdministrator](https://msdn.microsoft.com/library/azure/dn629417.aspx) 命令，使用下列其中一個參數：
    >
    >     ```
    >     Add-AadrmRoleBasedAdministrator -EmailAddress <email address> -Role "ConnectorAdministrator"
    >     ```
    >
    >     ```
    >     Add-AadrmRoleBasedAdministrator -ObjectId <object id> -Role "ConnectorAdministrator"
    >     ```
    >
    >     ```
    >     Add-AadrmRoleBasedAdministrator -SecurityGroupDisplayName <group Name> -Role "ConnectorAdministrator"
    >     ```
    >     例如，輸入︰**Add-AadrmRoleBasedAdministrator -EmailAddress melisa@contoso.com -Role "ConnectorAdministrator"**
    >
    >     雖然這些命令會指派連接器系統管理員角色，您還是可以在此使用 GlobalAdministrator 角色。

在 RMS 連接器安裝程序期間，將會驗證並安裝所有必要軟體、安裝 Internet Information Services (IIS) (若尚未出現)，及安裝並設定連接器軟體。 此外，Azure RMS 會建立下列項目來準備設定：

-   授權伺服器的空白資料表以使用連接器與 Azure RMS 進行通訊。 您稍後可將伺服器新增至此資料表。

-   連接器的一組安全性權杖，可利用 Azure RMS 驗證作業。 這些權杖是從 Azure RMS 下載，並安裝於登錄中的本機電腦。 它們藉由使用資料保護應用程式設計介面 (DPAPI) 和本機系統帳戶認證而受到保護。

在精靈的最終頁面上，執行下列工作，然後按一下 [完成] ：

-   如果這是您已安裝的第一個連接器，請勿在此時選取 [啟動連接器系統管理員主控台以授權伺服器]  。 您將於安裝第二個 (或最終) RMS 連接器後選取此選項。 請改為在至少另一部電腦上重新執行精靈。 您必須安裝最少兩個連接器。

-   如已安裝了第二個 (或最後一個) 連接器，請選取 [啟動連接器系統管理員主控台以授權伺服器] 。

> [!TIP]
> 此時，您可以執行驗證測試來測試 RMS 連接器的 Web 服務是否可操作：
>
> -   從網頁瀏覽器中，連線至 **http://&lt;連接器位址&gt;/_wmcs/certification/servercertification.asmx**，以已安裝 RMS 連接器的伺服器位址或名稱取代 *&lt;連接器位址&gt;*。 成功連接後會顯示 **ServerCertificationWebService** 頁面。

如果需要解除安裝 RMS 連接器，請重新執行精靈並選取解除安裝選項。

## 授權伺服器使用 RMS 連接器
在至少兩部電腦上安裝 RMS 連接器後，即準備好授權要使用 RMS 連接器的伺服器與服務。 例如，執行 Exchange Server 2013 或 SharePoint Server 2013 的伺服器。

若要定義這些伺服器，請執行 RMS 連接器系統管理工具，並將項目新增至允許伺服器清單。 您可於 Microsoft Rights Management 連接器設定精靈結尾處選取 [啟動連接器系統管理員主控台以授權伺服器]  時執行此工具，或從精靈加以個別執行。

當您授權這些伺服器時，請注意下列事項：

-   您新增的伺服器會授與特殊權限。 您在連接器設定中為 Exchange Server 角色指定的所有帳戶會在 Azure RMS 中獲得授與[進階使用者角色](configure-super-users.md)，使他們能夠存取此 RMS 租用戶的所有內容。 如有必要，進階使用者功能會在此時自動啟用。 為了避免提升權限所帶來的安全性風險，請小心，只能指定由貴組織的 Exchange 伺服器所使用的帳戶。 會將一般使用者權限授與使用 FCI 之 SharePoint 伺服器或檔案伺服器的所有伺服器。

-   您可指定 Active Directory 安全性或通訊群組，將多部伺服器新增為單一項目，或由多部伺服器使用的一個服務帳戶。 使用此設定時，伺服器群組將共用相同的 RMS 憑證，並將被視為其中任何伺服器已保護內容的擁有者。 若要將系統管理額外負荷降到最低，建議您使用這個單一群組組態 (而不要使用個別伺服器) 來授權貴組織的 Exchange 伺服器或 SharePoint 伺服器陣列。

在 [伺服器允許利用連接器]  頁面上，按一下 [新增] 。

> [!NOTE]
> 授權伺服器是 Azure RMS 中的組態，等同於針對服務或伺服器電腦帳戶，將 NTFS 權限手動套用至 ServerCertification.asmx 的 AD RMS 組態，並以手動方式授與使用者的 Exchange 帳戶的進階權限。 不需要在連接器上將 NTFS 權限套用至 ServerCertification.asmx。


### 將伺服器新增至允許伺服器清單
在 [允許伺服器利用連接器]  頁面上，輸入物件名稱，或加以瀏覽以識別要授權的物件。

請務必授權正確的物件。 若要讓伺服器使用連接器，必須選取授權執行內部部署服務的帳戶 (例如，Exchange 或 SharePoint)。 例如，若將服務作為設定的服務帳戶執行，請將該服務帳戶的名稱新增至清單。 若正在將服務作為本機系統執行，則新增電腦物件的名稱 (例如，SERVERNAME$)。 最佳作法是建立包含這些帳戶的群組，並指定該群組而非個別伺服器名稱。

不同伺服器角色的更多詳細資訊：

-   若為執行 Exchange 的伺服器：您必須指定安全性群組，且可使用預設群組 ([Exchange 伺服器])，後者是 Exchange 為樹系中所有 Exchange 伺服器自動建立並維護的群組。

-   若為執行 SharePoint 的伺服器：

    -   如果 SharePoint 2010 伺服器設定為以本機系統 (不使用服務帳戶) 執行，以手動方式在 Active Directory 網域服務中建立安全性群組，並且將此組態中伺服器的電腦名稱物件新增至此群組。

    -   如果 SharePoint 伺服器設定為使用服務帳戶 (適用於 SharePoint 2010 的建議做法和適用於 SharePoint 2016 和 SharePoint 2013 的唯一選項)，請執行下列作業：

        1.  新增執行 SharePoint 管理中心服務的服務帳戶，以啟用由其系統管理員主控台設定的 SharePoint。

        2.  新增為 SharePoint 應用程式集區設定的帳戶。

        > [!TIP]
        > 如果這兩個帳戶不同，請考慮建立包含這兩個帳戶的單一群組，以將系統管理負擔降至最低。

-   若為使用檔案分類基礎結構的檔案伺服器，關聯的服務將作為本機系統帳戶執行，因此您必須為檔案伺服器授權電腦帳戶 (例如，SERVERNAME$)，或為包含那些電腦帳戶的群組進行授權。

將伺服器新增至清單後，按一下 [關閉] 。

如果您尚未這麼做，現在就必須為已安裝 RMS 連接器的伺服器設定負載平衡，並考慮是否要針對這些伺服器與您剛才授權之伺服器之間的連線使用 HTTPS。

## 設定負載平衡和高可用性
安裝 RMS 連接器的第二個或最後一個執行個體後，定義連接器 URL 伺服器名稱和設定負載平衡系統。

連接器 URL 伺服器名稱可為您所控制命名空間下的任何名稱。 例如，您可於 DNS 系統中為 **rmsconnector.contoso.com** 建立項目，並在負載平衡系統中設定此項目以使用 IP 位址。 對於這個名稱並沒有任何特殊要求，而且也不一定要在連接器伺服器本身設定它。 除非您的 Exchange 和 SharePoint 伺服器將透過網際網路與連接器進行通訊，否則不一定要在網際網路上解析這個名稱。

> [!IMPORTANT]
> 建議您在設定 Exchange 或 SharePoint 伺服器使用連接器之後不要變更這個名稱，因為您接著將必須從所有 IRM 組態中清除這些伺服器，然後重新設定它們。

在 DNS 中建立名稱，並為 IP 位址進行設定之後，請為該位址設定負載平衡，以將流量導向連接器伺服器。 您可以此用途使用任何 IP 架構負載平衡器，此包含在 Windows Server 中的網路負載平衡 (NLB) 功能。 如需詳細資訊，請參閱[負載平衡部署指南](http://technet.microsoft.com/library/cc754833%28v=WS.10%29.aspx)。

使用下列設定來設定 NLB 叢集：

-   連接埠：80 (適用於 HTTP) 或 443 (適用於 HTTPS)

    如需是否使用 HTTP 或 HTTPS 的詳細資料，請參閱下一節。

-   同質：None

-   散發方法：等於

您為負載平衡型系統 (用於執行 RMS 連接器服務的伺服器) 定義的這個名稱，是您稍後設定內部部署伺服器來使用 Azure RMS 時，要使用之貴組織的 RMS 連接器名稱。

## 設定 RMS 連接器使用 HTTPS
> [!NOTE]
> 這是選用的設定步驟，但建議執行以提升安全性。

雖然 RMS 連接器可選擇是否使用 TLS 或 SSL，但我們建議任何 HTTP 架構的安全敏感服務加以使用。 此設定可對使用連接器的 Exchange 和 SharePoint 伺服器，驗證執行該連接器的伺服器。 此外，從這些伺服器傳送至連接器的所有資料會進行加密。

若要啟用 RMS 連接器以使用 TLS，請在執行 RMS 連接器的每一部伺服器上安裝伺服器驗證憑證，該憑證必須包含將使用於連接器的名稱。 例如，如果您在 DNS 中定義的 RMS 連接器名稱為 **rmsconnector.contoso.com**，請部署在憑證主體中含 **rmsconnector.contoso.com** 做為一般名稱的伺服器驗證憑證。 或者，在憑證替代名稱中指定 **rmsconnector.contoso.com** 做為 DNS 值。 憑證不一定要包含伺服器的名稱。 接著在 IIS 中，將此憑證繫結至預設網站。

如果使用 HTTPS 選項，請確定執行連接器的所有伺服器皆具備有效的伺服器驗證憑證，且該憑證必須鏈結至您 Exchange 和 SharePoint 伺服器信任的根 CA。 此外，若為連接器伺服器發行憑證的憑證授權單位 (CA) 發佈憑證撤銷清單 (CRL)，Exchange 和 SharePoint 伺服器必須可下載此 CRL。

> [!TIP]
> 您可使用下列資訊和資源來協助您要求和安裝伺服器驗證憑證，並將此憑證繫結至 IIS 中的預設網站：
>
> -   如果使用 Active Directory 憑證服務 (AD CS) 和企業憑證授權單位 (CA) 來部署這些伺服器驗證憑證，您可進行複製，然後使用網頁伺服器憑證範本。 此憑證範本為憑證主體名稱使用 [在要求中提供]  ，這表示您可在要求憑證時，為憑證主體名稱或主體替代名稱提供 RMS 連接器名稱的 FQDN。
> -   如果您使用獨立 CA，或從另一家公司購買此憑證，請參閱 TechNet 上[網頁伺服器 (IIS)](http://technet.microsoft.com/library/cc753433%28v=ws.10%29.aspx) 文件庫的[設定網際網路伺服器憑證 (IIS 7)](http://technet.microsoft.com/library/cc731977%28v=ws.10%29.aspx)。
> -   若要設定 IIS 使用憑證，請參閱 TechNet 上[網頁伺服器 (IIS)](http://technet.microsoft.com/library/cc753433%28v=ws.10%29.aspx) 文件庫的[新增繫結至網站 (IIS 7)](http://technet.microsoft.com/library/cc731692.aspx)。

## 設定 Web Proxy 伺服器的 RMS 連接器
若連接器伺服器是安裝在沒有網際網路直接連線的網路中，且您需要為傳出網際網路存取手動設定 Web Proxy 伺服器，您必須在這些伺服器上設定 RMS 連接器的登錄。

#### 設定 RMS 連接器以使用 Web Proxy 伺服器

1.  在每部執行 RMS 連接器的伺服器上開啟登錄編輯程式，如 Regedit。

2.  導覽至 **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\AADRM\Connector**

3.  新增字串值 **ProxyAddress**，然後將此值的 Data 設為 **http://&lt;我的 Proxy 網域或 IP 位址&gt;:&lt;我的 Proxy 連接埠&gt;**

    例如：**http://proxyserver.contoso.com:8080**

4.  關閉登錄編輯程式，然後重新啟動伺服器，或執行 IISReset 命令以重新啟動 IIS。

## 在系統管理電腦上安裝 RMS 連接器系統管理工具
您可從未安裝 RMS 連接器的電腦執行 RMS 連接器系統管理工具，但該電腦必須符合下列需求：

-   執行 Windows Server 2012 或 Windows Server 2012 R2 (所有版本)、Windows Server 2008 R2 或 Windows Server 2008 R2 Service Pack 1 (所有版本)、Windows 8.1、Windows 8 或 Windows 7 的實體或虛擬電腦。

-   至少需要 1 GB RAM。

-   至少需要 64 GB 磁碟空間。

-   至少需要一個網路介面。

-   透過防火牆 (或 Web Proxy) 存取網際網路。

若要安裝 RMS 連接器系統管理工具，請執行下列檔案：

-   對於 32 位元電腦︰RMSConnectorAdminToolSetup_x86.exe

-   對於 64 位元電腦︰RMSConnectorSetup.exe

如果尚未下載這些檔案，您可以從 [Microsoft 下載中心](http://go.microsoft.com/fwlink/?LinkId=314106)取得。


## 後續步驟
既然已安裝和設定 RMS 連接器，您已準備好設定內部部署伺服器來使用它。 移至[設定 Azure Rights Management 連接器的伺服器](configure-servers-rms-connector.md)。


<!--HONumber=Sep16_HO4-->


