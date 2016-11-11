---
title: "RMS 用戶端部署注意事項 | Azure Information Protection"
description: "資訊包括 Rights Management Service 用戶端 (RMS 用戶端) 版本 2 的重新發佈、安裝、支援的作業系統、登錄設定及服務探索，其亦稱作 MSIPC 用戶端。"
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 10/28/2016
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 03cc8c6f-3b63-4794-8d92-a5df4cdf598f
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 6b1b134aa8a0c7ef7cded627a7d25df4a90e9faa
ms.openlocfilehash: 811622757a4e44afb84ec2df84341ecbcd2e7a8f


---

# <a name="rms-client-deployment-notes"></a>RMS 用戶端部署注意事項

>*適用於︰Active Directory Rights Management Services、Azure Information Protectin、Windows 7 SP1、Windows 8、Windows 8.1、Windows 10、Windows Server 2008、Windows Server 2008 R2、Windows Server 2012、Windows Server 2012 R2、Windows Server 2016、Windows Vista*

Rights Management Service 用戶端 (RMS 用戶端) 第 2 版也稱為 MSIPC 用戶端。 它是 Windows 電腦軟體，可在內部部署上或雲端中與 Microsoft Rights Management Service 通訊，以在資訊流過應用程式和裝置時，在您組織的界限內或那些受管理界限外，協助保護資訊的存取和使用。 

除了隨附於[適用於 Windows 的 Rights Management 共用應用程式](sharing-app-windows.md)外，RMS 用戶端也可以[當作選擇性下載項目](http://www.microsoft.com/download/details.aspx?id=38396)提供，如此只要確認並接受其授權合約，即可搭配協力廠商軟體免費散發，讓用戶端可以保護和取用 Rights Management Service 所保護的內容。


## <a name="redistributing-the-rms-client"></a>轉散發 RMS 用戶端
RMS 用戶端可以免費轉散發，並與其他應用程式和 IT 解決方案組成套件。 如果您是應用程式開發人員或解決方案提供者，而且想要轉散發 RMS 用戶端，則您有兩個選項：

-   建議：將 RMS 用戶端安裝程式嵌入您的應用程式安裝，並以無訊息模式執行 (**/quiet** 參數，下一節會詳加說明)。

-   使 RMS 用戶端成為應用程式的必要條件。 使用此選項時，您可能需要為使用者提供其他指示，讓他們可以取得、安裝和更新其電腦與用戶端，然後再使用您的應用程式。

## <a name="installing-the-rms-client"></a>安裝 RMS 用戶端
RMS 用戶端包含在名為 **setup_msipc_***<arch>***.exe** 的安裝程式可執行檔中，其中 *<arch>* 是 **x86** (針對 32 位元用戶端電腦) 或 **x64** (針對 64 位元用戶端電腦)。 64 位元 (x64) 安裝程式套件會同時安裝 32 位元執行階段可執行檔，以與 64 位元作業系統安裝上執行的 32 位元應用程式相容，以及安裝 64 位元執行階段，支援原生 64 位元應用程式。 32 位元 (x86) 安裝程式不會在 64 位元 Windows 安裝上執行。

> [!NOTE]
> 您必須具備較高的權限，才能安裝 RMS 用戶端，例如本機電腦上的 Administrators 群組成員。

您可以使用下列其中一 種安裝方法來安裝 RMS 用戶端：

-   **無訊息模式。** 使用 **/quiet** 參數作為命令列選項的一部分，您可以用無訊息方式在電腦上安裝 RMS 用戶端。 下列範例顯示 64 位元用戶端電腦上 RMS 用戶端的無訊息模式安裝：

    ```
    setup_msipc_x64.exe /quiet
    ```

-   **互動模式。** 或者，您可以使用 RMS 用戶端安裝精靈所提供的 GUI 安裝程式來安裝 RMS 用戶端。 若要這樣做，請按兩下資料夾中的 RMS 用戶端安裝程式封裝 (**setup_msipc_***<arch>***.exe**)，而此資料夾正是先前在本機電腦上複製或下載它之處。

## <a name="questions-and-answers-about-the-rms-client"></a>有關 RMS 用戶端的問題與回答
下節包含有關 RMS 用戶端的常見問題集，以及它們的回答。

### <a name="which-operating-systems-support-the-rms-client"></a>哪些作業系統支援 RMS 用戶端？
下列作業系統支援 RMS 用戶端：

|Windows Server 作業系統|Windows 用戶端作業系統|
|-----------------------------------|-----------------------------------|
|Windows Server 2016|Windows 10|
|Windows Server 2012 R2|Windows 8.1|
|Windows Server 2012|Windows 8|
|Windows Server 2008 R2|Windows 7 (至少含 SP1)|
|Windows Server 2008 (僅限 AD RMS)|Windows Vista (至少含 SP2，僅限 AD RMS)|

### <a name="which-processors-or-platforms-support-the-rms-client"></a>哪些處理器或平台支援 RMS 用戶端？
x86 和 x64 運算平台支援 RMS 用戶端。

### <a name="where-is-the-rms-client-installed"></a>安裝 RMS 用戶端的位置？
依預設，RMS 用戶端安裝在 %ProgramFiles%\Active Directory Rights Management Services Client 2.<minor version number> 中。

### <a name="what-files-are-associated-with-the-rms-client-software"></a>哪些檔案與 RMS 用戶端軟體與相關聯？
下列檔案會安裝為 RMS 用戶端軟體的一部分：

-   Msipc。dll

-   Ipcsecproc.dll

-   Ipcsecproc_ssp.dll

-   MSIPCEvents.man

除了這些檔案外，RMS 用戶端還會安裝 44 種語言的多語系使用者介面 (MUI) 支援檔案。 若要確認支援的語言，請執行 RMS 用戶端安裝，並在安裝完成時，檢閱預設路徑下多語系支援資料夾的內容。

### <a name="is-the-rms-client-included-by-default-when-i-install-a-supported-operating-system"></a>當安裝支援的作業系統時，預設會包含 RMS 用戶端嗎？
否。 這個版本的 RMS 用戶端是以選擇性下載項目提供，可個別安裝在執行支援的 Microsoft Windows 作業系統版本的電腦上。

### <a name="is-the-rms-client-automatically-updated-by-microsoft-update"></a>Microsoft update 會自動更新 RMS 用戶端嗎?
如果您已使用無訊息安裝選項來安裝此 RMS 用戶端，則 RMS 用戶端會繼承目前的 Microsoft Update 設定。 如果您已使用 GUI 安裝程式安裝 RMS 用戶端，則 RMS 用戶端安裝精靈會提示您啟用 Microsoft Update。

## <a name="rms-client-settings"></a>RMS 用戶端設定
下節包含有關 RMS 用戶端的設定資訊。 如果您有使用 RMS 用戶端的應用程式或服務方面的問題，這項資訊可能很有幫助。

> [!NOTE]
> 某些設定取決於啟用 RMS 的應用程式是以用戶端模式應用程式執行 (例如 Microsoft Word 和 Outlook，或 RMS 共用應用程式)，還是以伺服器模式應用程式執行 (例如 SharePoint 和 Exchange)。 在下列資料表中，這些設定會分別識別為 **用戶端模式** 和 **伺服器模式**。

### <a name="where-the-rms-client-stores-licenses-on-client-computers"></a>用戶端電腦上 RMS 用戶端儲存授權的位置
RMS 用戶端會在本機磁碟上儲存授權，也會快取 Windows 登錄中的某些資訊。

|說明|用戶端模式路徑|伺服器模式路徑|
|---------------|---------------------|---------------------|
|授權儲存位置|%localappdata%\Microsoft\MSIPC|%allusersprofile%\Microsoft\MSIPC\Server\*<SID>*\|
|範本儲存位置|%localappdata%\Microsoft\MSIPC\Templates|%allusersprofile%\Microsoft\MSIPC\Server\Templates\*<SID>*\|
|登錄位置|HKEY_CURRENT_USER<br /> \Software<br /> \Classes<br /> \Local Settings<br /> \Software<br /> \Microsoft<br /> \MSIPC|HKEY_CURRENT_USER<br /> \Software<br /> \Microsoft<br /> \MSIPC<br /> \Server<br /> \*<SID>*|
> [!NOTE]
> *<SID>* 是執行伺服器應用程式之帳戶的安全識別碼 (SID)。 例如，如果應用程式是在內建的網路服務帳戶下執行，請將 *<SID>* 取代為該帳戶的已知 SID 值 (S-1-5-20)。

### <a name="windows-registry-settings-for-the-rms-client"></a>RMS 用戶端的 Windows 登錄設定
您可以使用 Windows 登錄機碼，來設定或修改某些 RMS 用戶端組態。 例如，作為與 AD RMS 伺服器通訊並啟用 RMS 之應用程式的系統管理員，您可能會想要更新企業服務位置 (覆寫目前為發行所選取的 AD RMS 伺服器)，取決於您的 Active Directory 拓樸內用戶端電腦的目前位置而定。 或者，您可能想要在用戶端電腦啟用 RMS 追蹤，以協助疑難排解啟用 RMS 的應用程式的問題。 請使用下表來識別您可以對 RMS 用戶端變更的登錄設定。

|工作|設定|
|--------|------------|
|僅限 AD RMS：更新用戶端電腦的企業服務位置|更新下列登錄機碼：<br /><br />HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSIPC\ServiceLocation\EnterpriseCertification<br />REG_SZ：default<br /><br />**值：**<http or https>:// *RMS 叢集名稱*/_wmcs/Certification<br /><br />HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSIPC\ServiceLocation\EnterprisePublishing<br />REG_SZ：default<br /><br />**值：** <http or https>:// *RMS 叢集名稱*/_wmcs/Licensing|
|啟用和停用追蹤|更新下列登錄機碼：<br /><br />HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSIPC<br />REG_DWORD: Trace<br /><br />**值：** 1 表示啟用追蹤，0 表示停用追蹤 (預設值)|
|變更以天為單位的頻率來重新整理範本|下列登錄值指定，如果未設定 TemplateUpdateFrequencyInSeconds 值，將在使用者的電腦上重新整理範本的頻率。  如果都未設定這些值，則使用 RMS 用戶端 (版本 1.0.1784.0) 下載範本之應用程式的預設重新整理間隔為 1 天。 在此之前的版本，其預設值為每 7 天。<br /><br />**用戶端模式：**<br /><br />HKEY_CURRENT_USER\Software\Classes\Local Settings\Software\Microsoft\MSIPC<br />REG_DWORD: TemplateUpdateFrequency<br /><br />**值：** 指定下載之間的天數 (最少 1 天) 的整數值。<br /><br />**伺服器模式：**<br /><br />HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSIPC\Server\\*\<SID\>\*<br />REG_DWORD: TemplateUpdateFrequency<br /><br />**值：** 指定下載之間的天數 (最少 1 天) 的整數值。|
|變更以秒為單位的頻率來重新整理範本<br /><br />重要：如果指定此項，則會忽略重新整理範本的值 (以天為單位)。 指定其中一個或另一個，不能同時指定兩者。|下列登錄值指定將在使用者的電腦上重新整理範本的頻率。 如果未設定此值或變更以天為單位之頻率 (TemplateUpdateFrequency) 的值，則使用 RMS 用戶端 (版本 1.0.1784.0) 下載範本之應用程式的預設重新整理間隔為 1 天。 在此之前的版本，其預設值為每 7 天。<br /><br />**用戶端模式：**<br /><br />HKEY_CURRENT_USER\Software\Classes\Local Settings\Software\Microsoft\MSIPC<br />REG_DWORD: TemplateUpdateFrequencyInSeconds<br /><br />**值：** 指定下載之間的秒數 (最少 1 秒) 的整數值。<br /><br />**伺服器模式：**<br /><br />HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSIPC\Server\\*\<SID\>\*<br />REG_DWORD: TemplateUpdateFrequencyInSeconds<br /><br />**值：** 指定下載之間的秒數 (最少 1) 的整數值。|
|僅限 AD RMS：在下次發佈要求時立即下載範本|在測試和評估期間，您可能想要 RMS 用戶端盡快下載範本。 若要這樣做，請移除下列登錄機碼，然後 RMS 用戶端將在下次發佈要求時立即下載範本，而不是等待 TemplateUpdateFrequency 登錄設定所指定的時間：<br /><br />HKEY_CURRENT_USER\Software\Classes\Local Settings\Software\Microsoft\MSIPC\<伺服器名稱>\Template<br /><br />**注意**：<Server Name> 可能具有外部 (corprights.contoso.com) 和內部 (corprights) URL，因此為兩個不同的項目。|
|僅限 AD RMS：啟用同盟驗證的支援|如果 RMS 用戶端電腦使用同盟信任連接至 AD RMS 叢集，您必須設定同盟主領域。<br /><br />HKEY_LOCAL_MACHINE\Software\Microsoft\MSIPC\Federation<br />REG_SZ: FederationHomeRealm<br /><br />**值：**此登錄項目的值是同盟服務 (例如，"http://TreyADFS.trey.net/adfs/services/trust") 的統一資源識別項 (URI)。<br /><br /> **注意**：對於此值，請務必指定 http，而非 https。 此外，如果在 64 位元版本的 Windows 上執行 32 位元 MSIPC 應用程式，位置將是 HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\MSIPC\Federation。 如需範例組態，請參閱 [使用 Active Directory Federation Services 部署 Active Directory Rights Management Services](https://technet.microsoft.com/library/dn758110.aspx)。|
|僅限 AD RMS：支援需要使用者輸入進行表單型驗證的夥伴同盟伺服器|根據預設，RMS 用戶端會以無訊息模式運作，因此不需要使用者輸入。 不過，夥伴同盟伺服器可能會設定為需要使用者輸入，例如藉由表單型驗證。 在此情況下，您必須設定 RMS 用戶端忽略無訊息模式，讓同盟驗證表單出現在瀏覽器視窗，並升級使用者進行驗證。<br /><br />HKEY_LOCAL_MACHINE\Software\Microsoft\MSIPC\Federation<br />REG_DWORD: EnableBrowser<br /><br />**注意**：如果同盟伺服器已設定為使用表單型驗證，則需要此金鑰。 如果同盟伺服器已設定為使用 Windows 整合式驗證，則不需要此金鑰。|
|僅限 AD RMS：封鎖 ILS 服務取用|根據預設，RMS 用戶端會啟用 ILS 服務所保護的取用內容，但您可以設定下列登錄機碼，將用戶端設定為封鎖這項服務。 如果這個登錄機碼設定為封鎖 ILS 服務，只要嘗試開啟並取用由 ILS 服務保護的內容，就會傳回下列錯誤：<br />HRESULT_FROM_WIN32(ERROR_ACCESS_DISABLED_BY_POLICY)<br /><br />HKEY_CURRENT_USER\Software\Classes\Local Settings\Software\Microsoft\MSIPC<br />REG_DWORD: **DisablePassportCertification**<br /><br />**值：** 1 表示封鎖 ILS 取用，0 表示允許 ILS 取用 (預設值)|

### <a name="managing-template-distribution-for-the-rms-client"></a>管理 RMS 用戶端的範本散發
範本可讓使用者和管理員輕鬆且快速地套用 Rights Management 保護，而且 RMS 用戶端會從其 RMS 伺服器或服務自動下載範本 (如果您將範本放在下列資料夾位置的話)、RMS 用戶端不會從其預設位置下載任何範本，而是下載置於此資料夾的範本。 RMS 用戶端可能會繼續從其他可用的 RMS 伺服器下載範本。

**用戶端模式：**%localappdata%\Microsoft\MSIPC\UnmanagedTemplates

**伺服器模式：** %allusersprofile%\Microsoft\MSIPC\Server\UnmanagedTemplates\\*\<SID\>\*

當您使用此資料夾時，不需要任何特殊命名慣例，但範本應由 RMS 伺服器或服務發行，而且它們必須具有.xml 副檔名。 例如，Contoso Confidential.xml 或 Contoso ReadOnly.xml 是有效的名稱。

## <a name="ad-rms-only-limiting-the-rms-client-to-use-trusted-ad-rms-servers"></a>僅限 AD RMS：限制 RMS 用戶端使用信任的 AD RMS 伺服器
RMS 用戶端可以限制為只使用特定信任的 AD RMS 伺服器，方法為對本機電腦上的 Windows 登錄進行下列變更。

**啟用將 RMS 用戶端限制為僅使用信任的 AD RMS 伺服器**

-   HKEY_LOCAL_MACHINE\Software\Microsoft\MSIPC\TrustedServers\
    REG_DWORD: AllowTrustedServersOnly

    **值：**如果指定非零值，則 RMS 用戶端將只信任指定的伺服器，而這些伺服器設定在 TrustedServers 清單和 Azure Rights Management Service 中。

**將成員新增至信任的 AD RMS 伺服器的清單**

-   HKEY_LOCAL_MACHINE\Software\Microsoft\MSIPC\TrustedServers\
    REG_SZ：*<URL 或主機名稱>*

    **值：**此登錄機碼位置中加入的字串值可以是 DNS 網域名稱格式 (例如，**adrms.contoso.com**) 或信任的 AD RMS 伺服器的完整 URL (例如，**https://adrms.contoso.com**)。 如果指定的 URL 以 **https://** 開頭，則 RMS 用戶端會使用 SSL 或 TLS 來連絡指定的 AD RMS 伺服器。

## <a name="rms-service-discovery"></a>RMS 服務探索
RMS 服務探索可讓 RMS 用戶端在保護內容之前，檢查要與哪一個 RMS 伺服器或服務通訊。 服務探索也可能會發生在 RMS 用戶端取用保護內容時，但是很少發生，原因是附加至內容的原則包含慣用的 RMS 伺服器或服務，而且只在不成功時，用戶端才會執行服務探索。

若要執行服務探索，RMS 用戶端會檢查下列情況：

1. **本機電腦上的 Windows 登錄**：如果已在登錄中設定服務探索設定，則會先嘗試這些設定。 

    根據預設，這些設定不會在登錄中設定，但管理員可為 AD RMS 加以設定，如[下列章節](#enabling-client-side-service-discovery-by-using-the-windows-registry)所述。 管理員通常會在 AD RMS 至 Azure 資訊保護的[移轉程序](../plan-design/migrate-from-ad-rms-phase2.md)期間，設定 Azure Rights Management 服務的這些設定。

2. **Active Directory Domain Services**：已加入網域的電腦會查詢 Active Directory，以取得服務連線點 (SCP)。 

    如果已依照[下列章節](#ad-rms-only-enabling-server-side-service-discovery-by-using-active-directory)所述登錄 SCP，則 AD RMS 伺服器的 URL 會傳回給 RMS 用戶端，供其使用。

3. **Azure Rights Management 探索服務**：RMS 用戶端連接至 **https://discover.aadrm.com**，這會提示使用者進行驗證。

    驗證成功時，驗證的使用者名稱 (及網域) 會用來識別要使用的 Azure 資訊保護租用戶。 該使用者帳戶所要使用的 Azure 資訊保護 URL 會傳回至 RMS 用戶端。 URL 會以下列格式呈現︰**https://**\<YourTenantURL\>**/_wmcs/licensing** 

    例如︰5c6bb73b-1038-4eec-863d-49bded473437.rms.na.aadrm.com/_wmcs/licensing

    *\<YourTenantURL\>* 的格式如下：**{GUID}.rms.[Region].aadrm.com**。在針對 Azure RMS 執行 [Get-AadrmConfiguration](http://msdn.microsoft.com/library/windowsazure/dn629410.aspx) Cmdlet 時，您可以藉由辨識 **RightsManagementServiceId** 值來找出該值。

> [!NOTE]
> 此服務探索流程有三個重要例外狀況︰
> 
> - 行動裝置最適合使用雲端服務，因此預設會使用 Azure Rights Management 服務的服務探索 (https://discover.aadrm.com)。 若要加以覆寫以便行動裝置使用 AD RMS，而不使用 Azure Rights Management 服務，您必須在 DNS 中指定 SRV 記錄，並安裝行動裝置延伸模組，如 [Active Directory Rights Management Services 行動裝置延伸模組](https://technet.microsoft.com/library/dn673574\(v=ws.11\).aspx)中所述。 
>
> - Azure 資訊保護標籤叫用 Rights Management 服務時，即不會執行服務探索。 相反地，URL 會直接在 Azure 資訊保護原則中所設定的標籤設定中指定。  

> - 使用者起始從 Office 應用程式登入時，驗證的使用者名稱 (及網域) 會用來識別要使用的 Azure 資訊保護租用戶。 在此情況下，不需要登錄設定，且不會檢查 SCP。

### <a name="ad-rms-only-enabling-serverside-service-discovery-by-using-active-directory"></a>僅限 AD RMS：使用 Active Directory 啟用伺服器端服務探索
如果您的帳戶具有足夠的權限 (AD RMS 伺服器的 Enterprise Admins 和本機系統管理員)，則您在安裝 AD RMS 根叢集伺服器時可以自動登錄服務連線點 (SCP) 。 如果 SCP 已存在於樹系中，您必須先刪除現有的 SCP，然後才能登錄新的 SCP。

在安裝 AD RMS 之後，您可以使用下列程序，登錄並刪除 SCP。 在開始之前，請確定您的帳戶具有必要的權限 (AD RMS 伺服器的 Enterprise Admins 和本機系統管理員)。

#### <a name="to-enable-ad-rms-service-discovery-by-registering-an-scp-in-active-directory"></a>在 Active Directory 中登錄 SCP 來啟用 AD RMS 服務探索

1.  在 AD RMS 伺服器開啟 Active Directory Management Service 主控台：

    -   如果您是使用 Windows Server 2008 R2 或 Windows Server 2008，請依序按一下 [ **開始**]、[ **系統管理工具**] 和 [ **Active Directory Rights Management Service**]。

    -   如果您是使用 Windows Server 2012 R2 或 Windows Server 2012，請在 [伺服器管理員] 中依序按一下 [工具] 和 [ Active Directory Rights Management Service]。

2.  在 AD RMS 主控台中，以滑鼠右鍵按一下 AD RMS 叢集，然後按一下 [內容]。

3.  按一下 [ **SCP** ] 索引標籤。

4.  選取 [ **變更 SCP** ] 核取方塊。

5.  選取 [ **設定 SCP 為目前的憑證叢集** ] 選項，然後按一下 [ **確定**]。

### <a name="enabling-clientside-service-discovery-by-using-the-windows-registry"></a>使用 Windows 登錄啟用用戶端服務探索
作為使用 SCP 或 SCP 不存在時的替代方案，您可以在用戶端電腦上設定登錄，讓 RMS 用戶端可以找出其 AD RMS 伺服器。

#### <a name="to-enable-clientside-ad-rms-service-discovery-by-using-the-windows-registry"></a>使用 Windows 登錄啟用用戶端 AD RMS 服務探索

1.  開啟 Windows 登錄編輯程式 Regedit.exe：

    -   在用戶端電腦的 [執行] 視窗中，輸入 **regedit**，然後按 Enter 鍵以開啟登錄編輯器。

2.  在登錄編輯器中，瀏覽至 **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSIPC**。

    > [!IMPORTANT]
    > 如果您是在 64 位元電腦上執行 32 位元應用程式，路徑會如下：**HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\MSIPC**

3.  若要建立 ServiceLocation 子機碼，請以滑鼠右鍵按一下 [MSIPC]、指向 [新增]、按一下 [機碼]，然後輸入 [ServiceLocation]。

4.  若要建立 EnterpriseCertification 子機碼，請以滑鼠右鍵按一下 [ServiceLocation]、指向 [新增]、按一下 [機碼]，然後輸入 [EnterpriseCertification]。

5.  若要設定企業憑證 URL，請連按兩下 **[EnterpriseCertification]** 子機碼下的 **[(預設值)]** 值，然後在 **[編輯字串]** 對話方塊出現時，針對 **[數值資料]**，輸入 <http or https>://*AD RMS 叢集名稱*/_wmcs/Certification，然後按一下 **[確定]**。

6.  若要建立 EnterprisePublishing 子機碼，請以滑鼠右鍵按一下 [ServiceLocation]、指向 [新增]、按一下 [機碼]，然後輸入 EnterprisePublishing。

7.  若要設定企業發佈 URL，請連按兩下 **[EnterprisePublishing]** 子機碼下的 **[(預設值)]**，然後在 **[編輯字串]** 對話方塊出現時，針對 **[數值資料]**，輸入下列 <http or https>://*AD RMS 叢集名稱*/_wmcs/Licensing，然後按一下 **[確定]**。

8.  關閉登錄編輯器。

如果 RMS 用戶端無法藉由查詢 Active Directory 找到 SCP，而且它未指定於登錄中，則 AD RMS 的服務探索呼叫將會失敗。

### <a name="redirecting-licensing-server-traffic"></a>重新導向授權伺服器流量
在某些情況下，您可能需要在服務探索期間重新導向流量，例如，當兩個組織合併，而且某個組織中的舊授權伺服器已停用，因此用戶端需要重新導向至新的授權伺服器時。 或者，從 AD RMS 移轉至 Azure RMS。 若要啟用授權重新導向，請使用下列程序。

#### <a name="to-enable-rms-licensing-redirection-by-using-the-windows-registry"></a>使用 Windows 登錄啟用 RMS 授權重新導向

1.  開啟 Windows 登錄編輯程式 Regedit.exe：

    -   在用戶端電腦的 [執行] 視窗中，輸入 **regedit**，然後按 Enter 鍵以開啟登錄編輯器。

2.  在登錄編輯器中，瀏覽至下列其中一項：

    -   x64 平台上的 64 位元版本 Office︰HKLM\SOFTWARE\Microsoft\MSIPC\Servicelocation

    -   x64 平台上的 32 位元版本 Office︰HKLM\SOFTWARE\Wow6432Node\Microsoft\MSIPC\Servicelocation

3.  建立一個 LicensingRedirection 子機碼，方法為以滑鼠右鍵按一下 [Servicelocation]、指向 [新增]、按一下 [機碼]，然後輸入 [LicensingRedirection]。

4.  若要設定授權重新導向，請以滑鼠右鍵按一下 [LicensingRedirection] 子機碼、選取 [新增]，然後選取 [字串值]。  針對 [ **名稱**]，指定先前的伺服器授權 URL，針對 [ **值** ]，則指定新的伺服器授權 URL。

    例如，若要將授權從 Contoso.com 中的伺服器重新導向至 Fabrikam.com 中的伺服器，您可能輸入下列值：

    **名稱：** https://contoso.com/_wmcs/licensing

    **值：** https://fabrikam.com/_wmcs/licensing

    > [!NOTE]
    > 如果舊授權伺服器同時指定了內部網路和外部網路 URL，則必須在 LicensingRedirection 機碼下，對這兩個 URL 設定新的名稱和值對應。

5.  針對需要重新導向的所有伺服器重複前一個步驟。

6.  關閉登錄編輯器。




<!--HONumber=Oct16_HO5-->


