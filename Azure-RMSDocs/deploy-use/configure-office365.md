---
title: "Office 365&colon;用戶端和線上服務的組態 | Azure RMS"
description: "適用於系統管理員設定 Office 365 以搭配 Azure Rights Management (Azure RMS) 使用的資訊和指示。"
author: cabailey
manager: mbaldwin
ms.date: 08/25/2016
ms.topic: article
ms.prod: 
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 0a6ce612-1b6b-4e21-b7fd-bcf79e492c3b
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: ad32910b482ca9d92b4ac8f3f123eda195db29cd
ms.openlocfilehash: 5e9ecbdef4adb4995199b059903902df078471e5


---

# Office 365：用戶端和線上服務的設定

>*適用於︰Azure Rights Management、Office 365*

由於 Office 365 原生支援 Azure RMS，因此無需用戶端電腦設定，便能支援 Word、Excel、PowerPoint、Outlook 和 Outlook Web App 等應用程式的資訊版權管理 (IRM) 功能。 所有使用者唯一要做的便是使用其 [!INCLUDE[o365_1](../includes/o365_1_md.md)] 認證登入其 Office 應用程式，並可保護檔案和電子郵件，及使用已接受他人保護的檔案和電子郵件。

不過，我們建議您使用 Rights Management 共用應用程式補充這些應用程式，讓使用者獲得 Office 增益集的好處。 如需詳細資訊，請參閱 [Rights Management 共用應用程式：用戶端的安裝和設定](configure-sharing-app.md)。

## Exchange Online：IRM 設定
若要設定 Exchange Online 來支援 Azure RMS，您必須為 Exchange Online 設定資訊版權管理 (IRM) 服務。 若要這樣做，請使用 Windows PowerShell (不需要安裝個別模組)，並執行 [Exchange Online 的 PowerShell 命令](https://technet.microsoft.com/library/jj200677.aspx)。

> [!NOTE]
> 如果您對 Azure RMS 使用客戶管理的租用戶金鑰 (BYOK)，而不是 Microsoft 管理的租用戶金鑰的預設組態，則目前無法將 Exchange Online 設定為支援 Azure RMS 如需詳細資訊，請參閱 [BYOK 定價和限制](../plan-design/byok-price-restrictions.md)。
>
> 如果您嘗試在 Azure RMS 使用 BYOK 時設定 Exchange Online，則匯入金鑰 (下列程序中的步驟 5) 的命令會失敗，並出現錯誤訊息 **[FailureCategory=Cmdlet-FailedToGetTrustedPublishingDomainFromRmsOnlineException]**。

下列步驟提供一組典型命令，您將執行這些命令，讓 Exchange Online 可以使用 Azure RMS：

1.  如果這是您第一次在電腦上使用 Windows PowerShell for Exchange Online，則必須將 Windows PowerShell 設定為執行已簽署的指令碼。 使用 [ **以系統管理員身分執行** ] 選項來啟動 Windows PowerShell 工作階段，然後輸入：

    ```
    Set-ExecutionPolicy RemoteSigned
    ```

2.  在您的 Windows PowerShell 工作階段中，使用可存取遠端殼層的帳戶登入 Exchange Online。 根據預設，Exchange Online 中建立的所有帳戶都可存取遠端殼層，但只要使用 [Set-User &lt;UserIdentity&gt; -RemotePowerShellEnabled](https://technet.microsoft.com/library/jj984292%28v=exchg.160%29.aspx) 命令就能停用 (啟用) 此存取權。

    若要登入，請輸入：

    ```
    $Cred = Get-Credential
    ```
    在 [ **Windows PowerShell 認證要求** ] 對話方塊中，提供您的 Office 365 使用者名稱和密碼。

3.  執行下列兩個命令連線到 Exchange Online 服務：

    ```
    $Session = New-PSSession -ConfigurationName Microsoft.Exchange -ConnectionUri https://ps.outlook.com/powershell/ -Credential $Cred -Authentication Basic –AllowRedirection
    ```

    ```
    Import-PSSession $Session
    ```

4.  根據您組織的租用戶建立所在的位置指定 Azure RMS 租用戶金鑰的位置：

    適用於北美洲 (以及政府訂用帳戶)：

    ```
    Set-IRMConfiguration -RMSOnlineKeySharingLocation "https://sp-rms.na.aadrm.com/TenantManagement/ServicePartner.svc"
    ```
    適用於歐洲：

    ```
    Set-IRMConfiguration -RMSOnlineKeySharingLocation "https://sp-rms.eu.aadrm.com/TenantManagement/ServicePartner.svc"
    ```
    適用於亞洲：

    ```
    Set-IRMConfiguration -RMSOnlineKeySharingLocation "https://sp-rms.ap.aadrm.com/TenantManagement/ServicePartner.svc"
    ```
    適用於南美洲：

    ```
    Set-IRMConfiguration -RMSOnlineKeySharingLocation "https://sp-rms.sa.aadrm.com/TenantManagement/ServicePartner.svc"
    ```

5.  以信任的發佈網域 (TPD) 形式，將組態資料從 Azure RMS 匯入到 Exchange Online。 這包括 Azure RMS 租用戶金鑰和 Azure RMS 範本：

    ```
    Import-RMSTrustedPublishingDomain -RMSOnline -name "RMS Online"
    ```
    在這個命令中，我們已使用 **RMS Online** 的名稱，代表 Exchange Online 中 Azure RMS 的 TPD 基本名稱。 在匯入 TPD 之後，它會在 Exchange Online 中命名為 **RMS Online - 1**。

6.  啟用 IRM 功能，如此 Azure RMS 功能可供 Exchange Online 使用：

    ```
    Set-IRMConfiguration -InternalLicensingEnabled $true
    ```
    在執行此命令之後，會對 Outlook 用戶端、Outlook Web 應用程式和 Exchange Active Sync 自動啟用 Rights Management。

7.  選擇性地使用下列命令，測試這項組態是否成功：

    ```
    Test-IRMConfiguration -Sender <user email address>
    ```
    例如：**Test-IRMConfiguration -Sender  adams@contoso.com**

    此命令會執行一系列檢查，包含驗證服務的連線、擷取組態、擷取 Uri、授權，以及任何範本。 在 Windows PowerShell 工作階段中，您會在結束時看到每一項的結果，如果所有項目都通過這些檢查的話： **整體結果：通過**

8.  中斷遠端 PowerShell 工作階段的連線：

    ```
    Remove-PSSession $Session
    ```

現在使用者可以使用 Azure RMS 來保護其電子郵件訊息。 例如，在 Outlook Web 應用程式中，從擴充的功能表 ( **...** ) 選取 [**設定權限**]，然後選擇 [ **不可轉寄** ] 或其中一個可用的範本，將資訊保護套用至電子郵件訊息和任何附件。 不過，因為 Outlook Web App 會快取一天的 UI，所以請在嘗試將資訊保護套用至電子郵件訊息之前，以及執行這些組態命令之後，等待這段時間過去。 在 UI 更新以反映新的組態之前，您不會看到任何選項來自 [ **設定權限** ] 功能表。

> [!IMPORTANT]
> 如果您為 Azure RMS 建立新的[自訂範本](configure-custom-templates.md)，或更新範本，則每次您必須執行下列 Exchange Online PowerShell 命令 (如有必要，首先執行步驟 2 和 3)，將這些變更同步至 Exchange Online： `Import-RMSTrustedPublishingDomain -Name "RMS Online - 1" -RefreshTemplates –RMSOnline`

做為 Exchange 系統管理員，您現在可以設定自動套用資訊保護的功能，例如[傳輸規則](https://technet.microsoft.com/library/dd302432.aspx)、[資料外洩防護 (DLP) 原則](https://technet.microsoft.com/library/jj150527%28v=exchg.150%29.aspx)，以及[受保護的語音郵件](https://technet.microsoft.com/library/dn198211%28v=exchg.150%29.aspx) (Unified Messaging)。

如需將 Exchange Online 設定為啟用 IRM 功能的詳細指示，請參閱 Exchange 文件庫中的文件。 例如：

-   [使用遠端 PowerShell 連線到 Exchange Online](https://technet.microsoft.com/library/jj984289%28v=exchg.160%29.aspx)

-   [將 IRM 設定為使用 Azure Rights Management](https://technet.microsoft.com/library/dn151475%28v=exchg.150%29.aspx)

### Office 365 訊息加密
執行上一節所述的相同步驟，但是如果您不想要顯示範本，請在步驟 6 之前，執行下列命令，以防止可在 Outlook Web App 和 Outlook 用戶端中使用 IRM 範本： `Set-IRMConfiguration -ClientAccessServerEnabled $false`

然後，您準備好將 [傳輸規則](https://technet.microsoft.com/library/dd302432.aspx) 設定為當收件者位於組織外部時自動修改訊息安全性，然後選取 [ **套用 Office 365 訊息加密** ] 選項。

如需訊息加密的詳細資訊，請在 Exchange 文件庫中參閱 [Office 365 中的加密](https://technet.microsoft.com/library/dn569286.aspx) 。

## SharePoint Online 和商務用 OneDrive：IRM 設定
若要設定 SharePoint Online 和商務用 OneDrive來支援 Azure RMS，首先您必須使用 SharePoint 系統管理中心來啟用 SharePoint Online 的資訊版權管理 (IRM) 服務。 然後，網站擁有者可以使用 IRM 保護其 SharePoint 清單和文件庫，而使用者可以使用 IRM 保護其商務用 OneDrive 文件庫，以便讓該處所儲存且與他人共用的文件可以自動受到 Azure RMS 的保護。

若要為 SharePoint online 啟用資訊版權管理 (IRM) 服務，請參閱 Office 網站提供的下列指示：

-   [在 SharePoint 系統管理中心設定資訊版權管理 (IRM)](http://office.microsoft.com/office365-sharepoint-online-enterprise-help/set-up-information-rights-management-irm-insharepoint-online-HA102895193.aspx)

此組態是由 Office 365 系統管理員完成。

### 設定文件庫和清單的 IRM
SharePoint 的 IRM 服務啟用後，網站擁有者可以使用 IRM 保護其 SharePoint 文件庫和清單。 如需指示，請參閱 Office 網站提供的下列資訊：

-   [將資訊版權管理套用至清單或文件庫](http://office.microsoft.com/sharepoint-help/apply-information-rights-management-to-a-list-or-library-HA102891460.aspx)

此組態是由 SharePoint 網站系統管理員完成。

### 設定商務用 OneDrive 的 IRM
SharePoint Online 的 IRM 服務啟用後，就能為使用者的商務用 OneDrive 文件庫設定 Rights Management 保護了。  使用者可以使用其 OneDrive 中的 [設定] 圖示，自行設定此作業。 雖然管理員無法使用 SharePoint 管理中心，為使用者的商務用 OneDrive 設定 Rights Management，但是可以使用 Windows PowerShell 來執行此設定。

> [!NOTE]
> 如需設定商務用 OneDrive 的詳細資訊，請參閱 Office 文件[在 Office 365 中設定商務用 OneDrive](https://support.office.com/article/Set-up-OneDrive-for-Business-in-Office-365-3e21f8f0-e0a1-43be-aa3e-8c0236bf11bb)。

#### 使用者的組態
給與使用者下列指示，讓他們可以設定其商務用 OneDrive，並使用 IRM 保護他們的商務檔案。

1.  在 OneDrive，按一下 [ **設定** ] 圖示開啟 [設定] 功能表，然後按一下 [ **網站內容**]。

2.  將滑鼠停留在 [ **文件** ] 磚上，選擇省略符號 (**...**)，然後按一下 [ **設定**]。

3.  在 [ **設定** ] 頁面的 [ **權限與管理** ] 區段中，按一下 [ **資訊版權管理**]。

4.  在 [ **資訊權限管理設定** ] 頁面上，選取 [ **限制在此文件庫下載的權限** ] 核取方塊、指定您為權限選擇的名稱和描述，然後選擇性地按一下 [ **顯示選項** ] 以設定選用組態，然後按一下 [ **確定**]。

    如需有關組態選項的詳細資訊，請參閱 Office 文件所提供之＜ [將資訊版權管理套用至清單或文件庫](https://support.office.com/article/Apply-Information-Rights-Management-to-a-list-or-library-3bdb5c4e-94fc-4741-b02f-4e7cc3c54aa1) ＞中的指示。

因為此組態依賴使用者 (而不是系統管理員) 使用 IRM 保護其商務用 OneDrive 文件庫，所以請教導使用者有關保護其檔案的優點以及保護檔案的方法。 例如，說明當其共用商務用 OneDrive 中的文件時，只有在其設定的任何限制下獲得授權的人員才能存取該文件，即使檔案已重新命名並複製至其他地方也一樣。

#### 系統管理員的組態
雖然您無法使用 SharePoint 管理中心，為使用者的商務用 OneDrive 設定 IRM，但是可以使用 Windows PowerShell 來執行此設定。 若要對這些文件庫啟用 IRM，請遵循下列步驟：

1.  下載並安裝 [SharePoint t Online 用戶端元件 SDK](http://www.microsoft.com/en-us/download/details.aspx?id=42038)。

2.  下載並安裝 [SharePoint Online 管理命令介面](http://www.microsoft.com/en-us/download/details.aspx?id=35588)。

3.  複製下列指令碼的內容，並在電腦上將檔案命名為 Set-IRMOnOneDriveForBusiness.ps1。

    *&#42;&#42;免責聲明&#42;&#42;*：這個範例指令碼不受任何 Microsoft 標準支援計劃或服務的支援。 這個範例指令碼是依現狀提供，不含任何種類的擔保。

    ```
    # Requires Windows PowerShell version 3

    <#
      Description:

        Configures IRM policy settings for OneDrive for Business and can also be used for SharePoint Online libraries and lists

     Script Installation Requirements:

       SharePoint Online Client Components SDK
       http://www.microsoft.com/en-us/download/details.aspx?id=42038

       SharePoint Online Management Shell
       http://www.microsoft.com/en-us/download/details.aspx?id=35588

    ======
    #>

    # URL will be in the format https://<tenant-name>-admin.sharepoint.com
    $sharepointAdminCenterUrl = "https://contoso-admin.sharepoint.com"

    $tenantAdmin = "admin@contoso.com"

    $webUrls = @("https://contoso-my.sharepoint.com/personal/user1_contoso_com",
                 "https://contoso-my.sharepoint.com/personal/user2_contoso_com",
                 "https://contoso-my.sharepoint.com/personal/user3_contoso_com")

    <# As an alternative to specifying the URLs as an array, you can import them from a CSV file (no header, single value per row).
       Then, use: $webUrls = Get-Content -Path "File_path_and_name.csv"

    #>

    $listTitle = "Documents"

    function Load-SharePointOnlineClientComponentAssemblies
    {
        [cmdletbinding()]
        param()

        process
        {
            # assembly location: C:\Program Files\Common Files\microsoft shared\Web Server Extensions\16\ISAPI
            try
            {
                Write-Verbose "Loading Assembly: Microsoft.Office.Client.Policy, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c"
                [System.Reflection.Assembly]::Load("Microsoft.Office.Client.Policy, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c") | Out-Null

                Write-Verbose "Loading Assembly: Microsoft.Office.Client.TranslationServices, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c"
                [System.Reflection.Assembly]::Load("Microsoft.Office.Client.TranslationServices, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c") | Out-Null

                Write-Verbose "Loading Assembly: Microsoft.SharePoint.Client, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c"
                [System.Reflection.Assembly]::Load("Microsoft.SharePoint.Client, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c") | Out-Null

                Write-Verbose "Loading Assembly: Microsoft.SharePoint.Client.DocumentManagement, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c"
                [System.Reflection.Assembly]::Load("Microsoft.SharePoint.Client.DocumentManagement, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c") | Out-Null

                Write-Verbose "Loading Assembly: Microsoft.SharePoint.Client.Publishing, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c"
                [System.Reflection.Assembly]::Load("Microsoft.SharePoint.Client.Publishing, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c") | Out-Null

                Write-Verbose "Loading Assembly: Microsoft.SharePoint.Client.Runtime, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c"
                [System.Reflection.Assembly]::Load("Microsoft.SharePoint.Client.Runtime, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c") | Out-Null

                Write-Verbose "Loading Assembly: Microsoft.SharePoint.Client.Search.Applications, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c"
                [System.Reflection.Assembly]::Load("Microsoft.SharePoint.Client.Search.Applications, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c") | Out-Null

                Write-Verbose "Loading Assembly: Microsoft.SharePoint.Client.Search, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c"
                [System.Reflection.Assembly]::Load("Microsoft.SharePoint.Client.Search, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c") | Out-Null

                Write-Verbose "Loading Assembly: Microsoft.SharePoint.Client.Taxonomy, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c"
                [System.Reflection.Assembly]::Load("Microsoft.SharePoint.Client.Taxonomy, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c") | Out-Null

                Write-Verbose "Loading Assembly: Microsoft.SharePoint.Client.UserProfiles, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c"
                [System.Reflection.Assembly]::Load("Microsoft.SharePoint.Client.UserProfiles, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c") | Out-Null

                return $true
            }
            catch
            {
                if($_.Exception.Message -match "Could not load file or assembly")
                {
                    Write-Error -Message "Unable to load the SharePoint Server 2013 Client Components.`nDownload Location: http://www.microsoft.com/en-us/download/details.aspx?id=42038"
                }
                else
                {
                    Write-Error -Exception $_.Exception
                }
                return $false
            }
        }
    }

    function Load-SharePointOnlineModule
    {
        [cmdletbinding()]
        param()

        process
        {
            do
            {
                # Installation location: C:\Program Files\SharePoint Online Management Shell\Microsoft.Online.SharePoint.PowerShell
                $spoModule = Get-Module -Name Microsoft.Online.SharePoint.PowerShell -ErrorAction SilentlyContinue

                if(-not $spoModule)
                {
                    try
                    {
                        Import-Module Microsoft.Online.SharePoint.PowerShell -DisableNameChecking
                        return $true
                    }
                    catch
                    {
                        if($_.Exception.Message -match "Could not load file or assembly")
                        {
                            Write-Error -Message "Unable to load the SharePoint Online Management Shell.`nDownload Location: http://www.microsoft.com/en-us/download/details.aspx?id=35588"
                        }
                        else
                        {
                            Write-Error -Exception $_.Exception
                        }
                        return $false
                    }
                }
                else
                {
                    return $true
                }
            }
            while(-not $spoModule)
        }
    }

    function Set-IrmConfiguration
    {
        [cmdletbinding()]
        param(
            [parameter(Mandatory=$true)][Microsoft.SharePoint.Client.List]$List,
            [parameter(Mandatory=$true)][string]$PolicyTitle,
            [parameter(Mandatory=$true)][string]$PolicyDescription,
            [parameter(Mandatory=$false)][switch]$IrmReject,
            [parameter(Mandatory=$false)][DateTime]$ProtectionExpirationDate,
            [parameter(Mandatory=$false)][switch]$DisableDocumentBrowserView,
            [parameter(Mandatory=$false)][switch]$AllowPrint,
            [parameter(Mandatory=$false)][switch]$AllowScript,
            [parameter(Mandatory=$false)][switch]$AllowWriteCopy,
            [parameter(Mandatory=$false)][int]$DocumentAccessExpireDays,
            [parameter(Mandatory=$false)][int]$LicenseCacheExpireDays,
            [parameter(Mandatory=$false)][string]$GroupName
        )

        process
        {
            Write-Verbose "Applying IRM Configuration on '$($List.Title)'"

            # reset the value to the default settings
            $list.InformationRightsManagementSettings.Reset()

            $list.IrmEnabled = $true

            # IRM Policy title and description

                $list.InformationRightsManagementSettings.PolicyTitle       = $PolicyTitle
                $list.InformationRightsManagementSettings.PolicyDescription = $PolicyDescription

            # Set additional IRM library settings

                # Do not allow users to upload documents that do not support IRM
                $list.IrmReject = $IrmReject.IsPresent

                $parsedDate = Get-Date
                if([DateTime]::TryParse($ProtectionExpirationDate, [ref]$parsedDate))
                {
                    # Stop restricting access to the library at <date>
                    $list.IrmExpire = $true
                    $list.InformationRightsManagementSettings.DocumentLibraryProtectionExpireDate = $ProtectionExpirationDate
                }

                # Prevent opening documents in the browser for this Document Library
                $list.InformationRightsManagementSettings.DisableDocumentBrowserView = $DisableDocumentBrowserView.IsPresent

            # Configure document access rights

                # Allow viewers to print
                $list.InformationRightsManagementSettings.AllowPrint = $AllowPrint.IsPresent

                # Allow viewers to run script and screen reader to function on downloaded documents
                $list.InformationRightsManagementSettings.AllowScript = $AllowScript.IsPresent

                # Allow viewers to write on a copy of the downloaded document
                $list.InformationRightsManagementSettings.AllowWriteCopy = $AllowWriteCopy.IsPresent

                if($DocumentAccessExpireDays)
                {
                    # After download, document access rights will expire after these number of days (1-365)
                    $list.InformationRightsManagementSettings.EnableDocumentAccessExpire = $true
                    $list.InformationRightsManagementSettings.DocumentAccessExpireDays   = $DocumentAccessExpireDays
                }

            # Set group protection and credentials interval

                if($LicenseCacheExpireDays)
                {
                    # Users must verify their credentials using this interval (days)
                    $list.InformationRightsManagementSettings.EnableLicenseCacheExpire = $true
                    $list.InformationRightsManagementSettings.LicenseCacheExpireDays   = $LicenseCacheExpireDays
                }

                if($GroupName)
                {
                    # Allow group protection. Default group:
                    $list.InformationRightsManagementSettings.EnableGroupProtection = $true
                    $list.InformationRightsManagementSettings.GroupName             = $GroupName
                }
        }
        end
        {
            if($list)
            {
                Write-Verbose "Committing IRM configuration settings on '$($list.Title)'"
                $list.InformationRightsManagementSettings.Update()
                $list.Update()
                $script:clientContext.Load($list)
                $script:clientContext.ExecuteQuery()
            }
        }
    }

    function Get-CredentialFromCredentialCache
    {
        [cmdletbinding()]
        param([string]$CredentialName)

        #if( Test-Path variable:\global:CredentialCache )
        if( Get-Variable O365TenantAdminCredentialCache -Scope Global -ErrorAction SilentlyContinue )
        {
            if($global:O365TenantAdminCredentialCache.ContainsKey($CredentialName))
            {
                Write-Verbose "Credential Cache Hit: $CredentialName"
                return $global:O365TenantAdminCredentialCache[$CredentialName]
            }
        }
        Write-Verbose "Credential Cache Miss: $CredentialName"
        return $null
    }

    function Add-CredentialToCredentialCache
    {
        [cmdletbinding()]
        param([System.Management.Automation.PSCredential]$Credential)

        if(-not (Get-Variable CredentialCache -Scope Global -ErrorAction SilentlyContinue))
        {
            Write-Verbose "Initializing the Credential Cache"
            $global:O365TenantAdminCredentialCache = @{}
        }

        Write-Verbose "Adding Credential to the Credential Cache"
        $global:O365TenantAdminCredentialCache[$Credential.UserName] = $Credential
    }

    # load the required assemblies and Windows PowerShell modules

        if(-not ((Load-SharePointOnlineClientComponentAssemblies) -and (Load-SharePointOnlineModule)) ) { return }

    # Add the credentials to the client context and SharePoint Online service connection

        # check for cached credentials to use
        $o365TenantAdminCredential = Get-CredentialFromCredentialCache -CredentialName $tenantAdmin

        if(-not $o365TenantAdminCredential)
        {
            # when credentials are not cached, prompt for the tenant admin credentials
            $o365TenantAdminCredential = Get-Credential -UserName $tenantAdmin -Message "Enter the password for the Office 365 admin"

            if(-not $o365TenantAdminCredential -or -not $o365TenantAdminCredential.UserName -or $o365TenantAdminCredential.Password.Length -eq 0 )
            {
                Write-Error -Message "Could not validate the supplied tenant admin credentials"
                return
            }

            # add the credentials to the cache
            Add-CredentialToCredentialCache -Credential $o365TenantAdminCredential
        }

    # connect to Office365 first, required for SharePoint Online cmdlets to run

        Connect-SPOService -Url $sharepointAdminCenterUrl -Credential $o365TenantAdminCredential

    # enumerate each of the specified site URLs

        foreach($webUrl in $webUrls)
        {
            $grantedSiteCollectionAdmin = $false

            try
            {
                # establish the client context and set the credentials to connect to the site
                $script:clientContext = New-Object Microsoft.SharePoint.Client.ClientContext($webUrl)
                $script:clientContext.Credentials = New-Object Microsoft.SharePoint.Client.SharePointOnlineCredentials($o365TenantAdminCredential.UserName, $o365TenantAdminCredential.Password)

                # initialize the site and web context
                $script:clientContext.Load($script:clientContext.Site)
                $script:clientContext.Load($script:clientContext.Web)
                $script:clientContext.ExecuteQuery()

                # load and ensure the tenant admin user account if present on the target SharePoint site
                $tenantAdminUser = $script:clientContext.Web.EnsureUser($o365TenantAdminCredential.UserName)
                $script:clientContext.Load($tenantAdminUser)
                $script:clientContext.ExecuteQuery()

                # check if the tenant admin is a site admin
                if( -not $tenantAdminUser.IsSiteAdmin )
                {
                    try
                    {
                        # grant the tenant admin temporary admin rights to the site collection
                        Set-SPOUser -Site $script:clientContext.Site.Url -LoginName $o365TenantAdminCredential.UserName -IsSiteCollectionAdmin $true | Out-Null
                        $grantedSiteCollectionAdmin = $true
                    }
                    catch
                    {
                        Write-Error $_.Exception
                        return
                    }
                }

                try
                {
                    # load the list orlibrary using CSOM

                    $list = $null
                    $list = $script:clientContext.Web.Lists.GetByTitle($listTitle)
                    $script:clientContext.Load($list)
                    $script:clientContext.ExecuteQuery()

                    # **************  ADMIN INSTRUCTIONS  **************
                    # If necessary, modify the following Set-IrmConfiguration parameters to match your required values
                    # The supplied options and values are for example only
                    # Example that shows the Set-IrmConfiguration command with all parameters: Set-IrmConfiguration -List $list -PolicyTitle "Protected Files" -PolicyDescription "This policy restricts access to authorized users" -IrmReject -ProtectionExpirationDate $(Get-Date).AddDays(180) -DisableDocumentBrowserView -AllowPrint -AllowScript -AllowWriteCopy -LicenseCacheExpireDays 25 -DocumentAccessExpireDays 90

                    Set-IrmConfiguration -List $list -PolicyTitle "Protected Files" -PolicyDescription "This policy restricts access to authorized users"  
                }
                catch
                {
                    Write-Error -Message "Error setting IRM configuration on site: $webUrl.`nError Details: $($_.Exception.ToString())"
                }
           }
           finally
           {
                if($grantedSiteCollectionAdmin)
                {
                    # remove the temporary admin rights to the site collection
                    Set-SPOUser -Site $script:clientContext.Site.Url -LoginName $o365TenantAdminCredential.UserName -IsSiteCollectionAdmin $false | Out-Null
                }
           }
        }

    Disconnect-SPOService -ErrorAction SilentlyContinue
    ```

4.  檢閱指令碼並且進行下列變更：

    1.  搜索 `$sharepointAdminCenterUrl`，並將範例值取代為自己的 SharePoint 管理員中心 URL。

        當您進入 SharePoint 系統管理中心時，會發現此值作為基本 URL，而且它具有以下格式：https://*&lt;租用戶名稱&gt;*-admin.sharepoint.com

        例如，如果租用戶名稱為 "contoso"，您將指定：**https://contoso-admin.sharepoint.com**

    2.  搜索 `$tenantAdmin`，並將範例值取代為您對 Office 365 擁有的完整全域管理員帳戶。

        此值與你用來以全域管理員身分登入 Office 365 系統管理入口網站的值相同，而且具有以下格式：使用者名稱@*&lt;租用戶網域名稱&gt;*.com

        例如，如果 "contoso.com" 租用戶網域的Office 365 全域管理員使用者名稱為 "admin"，您將指定：**admin@contoso.com**

    3.  搜索 `$webUrls`，並將範例值取代為您使用者的商務用 OneDrive 網站 URL，然後視需要新增或刪除多個項目。

        或者，請參閱指令碼中關於如何匯入 CSV 檔案來取代此陣列的註解，而此 CSV 檔案包含所有您需要設定的 URL。  我們提供了另一個範例指令碼，自動搜索和擷取 URL 來填入此。CSV 檔案。 當你準備好這樣做時，請使用緊跟在這些步驟後面的[將所有商務用 OneDrive URL 輸出至 CSV 檔案的其他指令碼](#additional-script-to-output-all-onedrive-for-business-urls-to-a-csv-file)一節。

        使用者的商務用 OneDrive 的 Web URL 具有以下格式：https://*&lt;租用戶名稱&gt;*-my.sharepoint.com/personal/*&lt;使用者名稱&gt;*_*&lt;租用戶名稱&gt;*_com

        例如，如果 contoso 租用戶中的使用者具有 "rsimone"的使用者名稱，您將指定：**https://contoso-my.sharepoint.com/personal/rsimone_contoso_com**

    4.  因為我們是使用指令碼來設定商務用 OneDrive，所以請不要變更 `$listTitle` 變數的 **Documents** 值。

    5.  搜尋 `ADMIN INSTRUCTIONS`。 如果您沒有對此區段進行任何變更，將對 IRM 設定使用者的商務用 OneDrive"，原則標題為「受保護的檔案」，而描述為「此原則會限制授權使用者的存取」。  將不設定任何其他 IRM 選項，這可能適用於大多數環境。 然而，你可以變更建議的原則標題和描述，而且也可新增任何適合於您環境的任何 IRM 選項。 請參閱註解中的範例指令碼，以協助您為 IrmConfiguration 命令構建一組專屬的參數。

5.  儲存指令碼並簽署它。 如果您未簽署指令碼 (更安全)，Windows PowerShell 必須在您的電腦設定為執行未簽署的指令碼。 若要這麼做，使用 [以系統管理員身分執行] 選項來執行 Windows PowerShell 工作階段，然後輸入：**Set-ExecutionPolicy Unrestricted**。 不過，這種組態會讓所有未簽署的指令碼執行 (較不安全)。

    如需有關簽署 Windows PowerShell 指令碼的詳細資訊，請參閱 PowerShell 文件庫中的 [about_Signing](https://technet.microsoft.com/library/hh847874.aspx) 。

6.  執行指令碼，如果出現提示，請提供 Office 365 管理員帳戶的密碼。 如果你修改指令碼，並在同一個 Windows PowerShell 工作階段中執行，則不會提示您輸入憑證。

> [!TIP]
> 你也可以使用此指令碼，設定 SharePoint Online 文件庫的 IRM。 對於此組態，您可能希望啟用其他選項 [不允許使用者上載不支援 IRM 的文件]，以確保文件庫只包含受保護的文件。    若要這樣做，請將 `-IrmReject` 參數新增至指令碼中的 Set-IrmConfiguration 命令。
>
> 你還需要修改 `$webUrls` 變數 (例如，**https://contoso.sharepoint.com**) 和 `$listTitle` 變數 (例如，**$Reports**)。

如果您需要對使用者的商務用 OneDrive 程式庫停用 IRM，請參閱[要對商務用 OneDrive 停用 IRM 的指令碼](#script-to-disable-irm-for-onedrive-for-business)一節。

##### 其他要將所有商務用 OneDrive URL 輸出至 CSV 檔案的指令碼
對於上述步驟 4c，你可以使用下列 Windows PowerShell 指令碼，擷取使用者的所有商務用 OneDrive 文件庫的 URL，接著您便可以檢查，視需要編輯，然後匯入至主要指令碼。

此指令碼也需要 [SharePoint Online 用戶端元件 SDK](http://www.microsoft.com/en-us/download/details.aspx?id=42038) 和 [SharePoint Online 管理命令介面](http://www.microsoft.com/en-us/download/details.aspx?id=35588)。 按照相同的指示來複製並貼上它，在本機儲存檔案 (例如，"Report-OneDriveForBusinessSiteInfo.ps1")，如同之前修改 `$sharepointAdminCenterUrl` 和 `$tenantAdmin` 值，然後執行指令碼。

*&#42;&#42;免責聲明&#42;&#42;*：這個範例指令碼不受任何 Microsoft 標準支援計劃或服務的支援。 這個範例指令碼是依現狀提供，不含任何種類的擔保。

```
# Requires Windows PowerShell version 3

<#
  Description:

    Queries the search service of an Office 365 tenant to retrieve all OneDrive for Business sites.  
    Details of the discovered sites are written to a .CSV file (by default,"OneDriveForBusinessSiteInfo_<date>.csv").

 Script Installation Requirements:

   SharePoint Online Client Components SDK
   http://www.microsoft.com/en-us/download/details.aspx?id=42038

   SharePoint Online Management Shell
   http://www.microsoft.com/en-us/download/details.aspx?id=35588

======
#>

# URL will be in the format https://<tenant-name>-admin.sharepoint.com
$sharepointAdminCenterUrl = "https://contoso-admin.sharepoint.com"

$tenantAdmin = "admin@contoso.onmicrosoft.com"                           

$reportName = "OneDriveForBusinessSiteInfo_$((Get-Date).ToString("yyyy-MM-dd_hh.mm.ss")).csv"

$oneDriveForBusinessSiteUrls= @()
$resultsProcessed = 0

function Load-SharePointOnlineClientComponentAssemblies
{
    [cmdletbinding()]
    param()

    process
    {
        # assembly location: C:\Program Files\Common Files\microsoft shared\Web Server Extensions\16\ISAPI
        try
        {
            Write-Verbose "Loading Assembly: Microsoft.Office.Client.Policy, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c"
            [System.Reflection.Assembly]::Load("Microsoft.Office.Client.Policy, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c") | Out-Null

            Write-Verbose "Loading Assembly: Microsoft.Office.Client.TranslationServices, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c"
            [System.Reflection.Assembly]::Load("Microsoft.Office.Client.TranslationServices, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c") | Out-Null

            Write-Verbose "Loading Assembly: Microsoft.SharePoint.Client, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c"
            [System.Reflection.Assembly]::Load("Microsoft.SharePoint.Client, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c") | Out-Null

            Write-Verbose "Loading Assembly: Microsoft.SharePoint.Client.DocumentManagement, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c"
            [System.Reflection.Assembly]::Load("Microsoft.SharePoint.Client.DocumentManagement, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c") | Out-Null

            Write-Verbose "Loading Assembly: Microsoft.SharePoint.Client.Publishing, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c"
            [System.Reflection.Assembly]::Load("Microsoft.SharePoint.Client.Publishing, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c") | Out-Null

            Write-Verbose "Loading Assembly: Microsoft.SharePoint.Client.Runtime, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c"
            [System.Reflection.Assembly]::Load("Microsoft.SharePoint.Client.Runtime, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c") | Out-Null

            Write-Verbose "Loading Assembly: Microsoft.SharePoint.Client.Search.Applications, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c"
            [System.Reflection.Assembly]::Load("Microsoft.SharePoint.Client.Search.Applications, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c") | Out-Null

            Write-Verbose "Loading Assembly: Microsoft.SharePoint.Client.Search, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c"
            [System.Reflection.Assembly]::Load("Microsoft.SharePoint.Client.Search, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c") | Out-Null

            Write-Verbose "Loading Assembly: Microsoft.SharePoint.Client.Taxonomy, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c"
            [System.Reflection.Assembly]::Load("Microsoft.SharePoint.Client.Taxonomy, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c") | Out-Null

            Write-Verbose "Loading Assembly: Microsoft.SharePoint.Client.UserProfiles, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c"
            [System.Reflection.Assembly]::Load("Microsoft.SharePoint.Client.UserProfiles, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c") | Out-Null

            return $true
        }
        catch
        {
            if($_.Exception.Message -match "Could not load file or assembly")
            {
                Write-Error -Message "Unable to load the SharePoint Server 2013 Client Components.`nDownload Location: http://www.microsoft.com/en-us/download/details.aspx?id=42038"
            }
            else
            {
                Write-Error -Exception $_.Exception
            }
            return $false
        }
    }
}

function Load-SharePointOnlineModule
{
    [cmdletbinding()]
    param()

    process
    {
        do
        {
            # Installation location: C:\Program Files\SharePoint Online Management Shell\Microsoft.Online.SharePoint.PowerShell
            $spoModule = Get-Module -Name Microsoft.Online.SharePoint.PowerShell -ErrorAction SilentlyContinue

            if(-not $spoModule)
            {
                try
                {
                    Import-Module Microsoft.Online.SharePoint.PowerShell -DisableNameChecking
                    return $true
                }
                catch
                {
                    if($_.Exception.Message -match "Could not load file or assembly")
                    {
                        Write-Error -Message "Unable to load the SharePoint Online Management Shell.`nDownload Location: http://www.microsoft.com/en-us/download/details.aspx?id=35588"
                    }
                    else
                    {
                        Write-Error -Exception $_.Exception
                    }
                    return $false
                }
            }
            else
            {
                return $true
            }
        }
        while(-not $spoModule)
    }
}

function Get-CredentialFromCredentialCache
{
    [cmdletbinding()]
    param([string]$CredentialName)

    #if( Test-Path variable:\global:CredentialCache )
    if( Get-Variable O365TenantAdminCredentialCache -Scope Global -ErrorAction SilentlyContinue )
    {
        if($global:O365TenantAdminCredentialCache.ContainsKey($CredentialName))
        {
            Write-Verbose "Credential Cache Hit: $CredentialName"
            return $global:O365TenantAdminCredentialCache[$CredentialName]
        }
    }
    Write-Verbose "Credential Cache Miss: $CredentialName"
    return $null
}

function Add-CredentialToCredentialCache
{
    [cmdletbinding()]
    param([System.Management.Automation.PSCredential]$Credential)

    if(-not (Get-Variable CredentialCache -Scope Global -ErrorAction SilentlyContinue))
    {
        Write-Verbose "Initializing the Credential Cache"
        $global:O365TenantAdminCredentialCache = @{}
    }

    Write-Verbose "Adding Credential to the Credential Cache"
    $global:O365TenantAdminCredentialCache[$Credential.UserName] = $Credential
}

# load the required assemblies and Windows PowerShell modules

    if(-not ((Load-SharePointOnlineClientComponentAssemblies) -and (Load-SharePointOnlineModule)) ) { return }

# Add the credentials to the client context and SharePoint Online service connection

    # check for cached credentials to use
    $o365TenantAdminCredential = Get-CredentialFromCredentialCache -CredentialName $tenantAdmin

    if(-not $o365TenantAdminCredential)
    {
        # when credentials are not cached, prompt for the tenant admin credentials
        $o365TenantAdminCredential = Get-Credential -UserName $tenantAdmin -Message "Enter the password for the Office 365 admin"

        if(-not $o365TenantAdminCredential -or -not $o365TenantAdminCredential.UserName -or $o365TenantAdminCredential.Password.Length -eq 0 )
        {
            Write-Error -Message "Could not validate the supplied tenant admin credentials"
            return
        }

        # add the credentials to the cache
        Add-CredentialToCredentialCache -Credential $o365TenantAdminCredential
    }

# establish the client context and set the credentials to connect to the site

    $clientContext = New-Object Microsoft.SharePoint.Client.ClientContext($sharepointAdminCenterUrl)
    $clientContext.Credentials = New-Object Microsoft.SharePoint.Client.SharePointOnlineCredentials($o365TenantAdminCredential.UserName, $o365TenantAdminCredential.Password)

# run a query against the Office 365 tenant search service to retrieve all OneDrive for Business URLs

    do
    {
        # build the query object
        $query = New-Object Microsoft.SharePoint.Client.Search.Query.KeywordQuery($clientContext)
        $query.TrimDuplicates        = $false
        $query.RowLimit              = 500
        $query.QueryText             = "SPSiteUrl:'/personal/' AND contentclass:STS_Site"
        $query.StartRow              = $resultsProcessed
        $query.TotalRowsExactMinimum = 500000

        # run the query
        $searchExecutor = New-Object Microsoft.SharePoint.Client.Search.Query.SearchExecutor($clientContext)
        $queryResults = $searchExecutor.ExecuteQuery($query)
        $clientContext.ExecuteQuery()

        # enumerate the search results and store the site URLs
        $queryResults.Value[0].ResultRows | % {
            $oneDriveForBusinessSiteUrls += $_.Path
            $resultsProcessed++
        }
    }
    while($resultsProcessed -lt $queryResults.Value.TotalRows)

$oneDriveForBusinessSiteUrls | Out-File -FilePath $reportName
```

##### 要對商務用 OneDrive 停用 IRM 的指令碼
如果您需要對使用者的商務用 OneDrive 停用 IRM，請使用下列範例指令碼。

此指令碼也需要 [SharePoint Online 用戶端元件 SDK](http://www.microsoft.com/en-us/download/details.aspx?id=42038) 和 [SharePoint Online 管理命令介面](http://www.microsoft.com/en-us/download/details.aspx?id=35588)。 複製並貼上內容，在本機儲存檔案 (例如，"Disable-IRMOnOneDriveForBusiness.ps1")，並修改 `$sharepointAdminCenterUrl` 和 `$tenantAdmin` 值。 手動指定商務用 OneDrive URL，或使用前一個區段中的指令碼，讓您可以匯入這些 URL，然後執行指令碼。

*&#42;&#42;免責聲明&#42;&#42;*：這個範例指令碼不受任何 Microsoft 標準支援計劃或服務的支援。 這個範例指令碼是依現狀提供，不含任何種類的擔保。

```
# Requires Windows PowerShell version 3

<#
  Description:

    Disables IRM for OneDrive for Business and can also be used for SharePoint Online libraries and lists

 Script Installation Requirements:

   SharePoint Online Client Components SDK
   http://www.microsoft.com/en-us/download/details.aspx?id=42038

   SharePoint Online Management Shell
   http://www.microsoft.com/en-us/download/details.aspx?id=35588

======
#>

$sharepointAdminCenterUrl = "https://contoso-admin.sharepoint.com"

$tenantAdmin = "admin@contoso.com"

$webUrls = @("https://contoso-my.sharepoint.com/personal/user1_contoso_com",
             "https://contoso-my.sharepoint.com/personal/user2_contoso_com",
             "https://contoso-my.sharepoint.com/personal/person3_contoso_com")

<# As an alternative to specifying the URLs as an array, you can import them from a CSV file (no header, single value per row).
   Then, use: $webUrls = Get-Content -Path "File_path_and_name.csv"

#>

$listTitle = "Documents"

function Load-SharePointOnlineClientComponentAssemblies
{
    [cmdletbinding()]
    param()

    process
    {
        # assembly location: C:\Program Files\Common Files\microsoft shared\Web Server Extensions\16\ISAPI
        try
        {
            Write-Verbose "Loading Assembly: Microsoft.Office.Client.Policy, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c"
            [System.Reflection.Assembly]::Load("Microsoft.Office.Client.Policy, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c") | Out-Null

            Write-Verbose "Loading Assembly: Microsoft.Office.Client.TranslationServices, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c"
            [System.Reflection.Assembly]::Load("Microsoft.Office.Client.TranslationServices, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c") | Out-Null

            Write-Verbose "Loading Assembly: Microsoft.SharePoint.Client, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c"
            [System.Reflection.Assembly]::Load("Microsoft.SharePoint.Client, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c") | Out-Null

            Write-Verbose "Loading Assembly: Microsoft.SharePoint.Client.DocumentManagement, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c"
            [System.Reflection.Assembly]::Load("Microsoft.SharePoint.Client.DocumentManagement, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c") | Out-Null

            Write-Verbose "Loading Assembly: Microsoft.SharePoint.Client.Publishing, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c"
            [System.Reflection.Assembly]::Load("Microsoft.SharePoint.Client.Publishing, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c") | Out-Null

            Write-Verbose "Loading Assembly: Microsoft.SharePoint.Client.Runtime, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c"
            [System.Reflection.Assembly]::Load("Microsoft.SharePoint.Client.Runtime, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c") | Out-Null

            Write-Verbose "Loading Assembly: Microsoft.SharePoint.Client.Search.Applications, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c"
            [System.Reflection.Assembly]::Load("Microsoft.SharePoint.Client.Search.Applications, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c") | Out-Null

            Write-Verbose "Loading Assembly: Microsoft.SharePoint.Client.Search, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c"
            [System.Reflection.Assembly]::Load("Microsoft.SharePoint.Client.Search, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c") | Out-Null

            Write-Verbose "Loading Assembly: Microsoft.SharePoint.Client.Taxonomy, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c"
            [System.Reflection.Assembly]::Load("Microsoft.SharePoint.Client.Taxonomy, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c") | Out-Null

            Write-Verbose "Loading Assembly: Microsoft.SharePoint.Client.UserProfiles, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c"
            [System.Reflection.Assembly]::Load("Microsoft.SharePoint.Client.UserProfiles, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c") | Out-Null

            return $true
        }
        catch
        {
            if($_.Exception.Message -match "Could not load file or assembly")
            {
                Write-Error -Message "Unable to load the SharePoint Server 2013 Client Components.`nDownload Location: http://www.microsoft.com/en-us/download/details.aspx?id=42038"
            }
            else
            {
                Write-Error -Exception $_.Exception
            }
            return $false
        }
    }
}

function Load-SharePointOnlineModule
{
    [cmdletbinding()]
    param()

    process
    {
        do
        {
            # Installation location: C:\Program Files\SharePoint Online Management Shell\Microsoft.Online.SharePoint.PowerShell
            $spoModule = Get-Module -Name Microsoft.Online.SharePoint.PowerShell -ErrorAction SilentlyContinue

            if(-not $spoModule)
            {
                try
                {
                    Import-Module Microsoft.Online.SharePoint.PowerShell -DisableNameChecking
                    return $true
                }
                catch
                {
                    if($_.Exception.Message -match "Could not load file or assembly")
                    {
                        Write-Error -Message "Unable to load the SharePoint Online Management Shell.`nDownload Location: http://www.microsoft.com/en-us/download/details.aspx?id=35588"
                    }
                    else
                    {
                        Write-Error -Exception $_.Exception
                    }
                    return $false
                }
            }
            else
            {
                return $true
            }
        }
        while(-not $spoModule)
    }
}

function Remove-IrmConfiguration
{
    [cmdletbinding()]
    param(
        [parameter(Mandatory=$true)][Microsoft.SharePoint.Client.List]$List
    )

    process
    {
        Write-Verbose "Disabling IRM Configuration on '$($List.Title)'"

        $List.IrmEnabled = $false
        $List.IrmExpire  = $false
        $List.IrmReject  = $false
        $List.InformationRightsManagementSettings.Reset()
    }
    end
    {
        if($List)
        {
            Write-Verbose "Committing IRM configuration settings on '$($list.Title)'"
            $list.InformationRightsManagementSettings.Update()
            $list.Update()
            $script:clientContext.Load($list)
            $script:clientContext.ExecuteQuery()
        }
    }
}

function Get-CredentialFromCredentialCache
{
    [cmdletbinding()]
    param([string]$CredentialName)

    #if( Test-Path variable:\global:CredentialCache )
    if( Get-Variable O365TenantAdminCredentialCache -Scope Global -ErrorAction SilentlyContinue )
    {
        if($global:O365TenantAdminCredentialCache.ContainsKey($CredentialName))
        {
            Write-Verbose "Credential Cache Hit: $CredentialName"
            return $global:O365TenantAdminCredentialCache[$CredentialName]
        }
    }
    Write-Verbose "Credential Cache Miss: $CredentialName"
    return $null
}

function Add-CredentialToCredentialCache
{
    [cmdletbinding()]
    param([System.Management.Automation.PSCredential]$Credential)

    if(-not (Get-Variable CredentialCache -Scope Global -ErrorAction SilentlyContinue))
    {
        Write-Verbose "Initializing the Credential Cache"
        $global:O365TenantAdminCredentialCache = @{}
    }

    Write-Verbose "Adding Credential to the Credential Cache"
    $global:O365TenantAdminCredentialCache[$Credential.UserName] = $Credential
}

# load the required assemblies and Windows PowerShell modules

    if(-not ((Load-SharePointOnlineClientComponentAssemblies) -and (Load-SharePointOnlineModule)) ) { return }

# Add the credentials to the client context and SharePoint Online service connection

    # check for cached credentials to use
    $o365TenantAdminCredential = Get-CredentialFromCredentialCache -CredentialName $tenantAdmin

    if(-not $o365TenantAdminCredential)
    {
        # when credentials are not cached, prompt for the tenant admin credentials
        $o365TenantAdminCredential = Get-Credential -UserName $tenantAdmin -Message "Enter the password for the Office 365 admin"

        if(-not $o365TenantAdminCredential -or -not $o365TenantAdminCredential.UserName -or $o365TenantAdminCredential.Password.Length -eq 0 )
        {
            Write-Error -Message "Could not validate the supplied tenant admin credentials"
            return
        }

        # add the credentials to the cache
        Add-CredentialToCredentialCache -Credential $o365TenantAdminCredential
    }

# connect to Office365 first, required for SharePoint Online cmdlets to run

    Connect-SPOService -Url $sharepointAdminCenterUrl -Credential $o365TenantAdminCredential

# enumerate each of the specified site URLs

    foreach($webUrl in $webUrls)
    {
        $grantedSiteCollectionAdmin = $false

        try
        {
            # establish the client context and set the credentials to connect to the site
            $script:clientContext = New-Object Microsoft.SharePoint.Client.ClientContext($webUrl)
            $script:clientContext.Credentials = New-Object Microsoft.SharePoint.Client.SharePointOnlineCredentials($o365TenantAdminCredential.UserName, $o365TenantAdminCredential.Password)

            # initialize the site and web context
            $script:clientContext.Load($script:clientContext.Site)
            $script:clientContext.Load($script:clientContext.Web)
            $script:clientContext.ExecuteQuery()

            # load and ensure the tenant admin user account if present on the target SharePoint site
            $tenantAdminUser = $script:clientContext.Web.EnsureUser($o365TenantAdminCredential.UserName)
            $script:clientContext.Load($tenantAdminUser)
            $script:clientContext.ExecuteQuery()

            # check if the tenant admin is a site admin
            if( -not $tenantAdminUser.IsSiteAdmin )
            {
                try
                {
                    # grant the tenant admin temporary admin rights to the site collection
                    Set-SPOUser -Site $script:clientContext.Site.Url -LoginName $o365TenantAdminCredential.UserName -IsSiteCollectionAdmin $true | Out-Null
                    $grantedSiteCollectionAdmin = $true
                }
                catch
                {
                    Write-Error $_.Exception
                    return
                }
            }

            try
            {
                # load the list orlibrary using CSOM

                $list = $null
                $list = $script:clientContext.Web.Lists.GetByTitle($listTitle)
                $script:clientContext.Load($list)
                $script:clientContext.ExecuteQuery()

               Remove-IrmConfiguration -List $list                 
            }
            catch
            {
                Write-Error -Message "Error setting IRM configuration on site: $webUrl.`nError Details: $($_.Exception.ToString())"
            }
       }
       finally
       {
            if($grantedSiteCollectionAdmin)
            {
                # remove the temporary admin rights to the site collection
                Set-SPOUser -Site $script:clientContext.Site.Url -LoginName $o365TenantAdminCredential.UserName -IsSiteCollectionAdmin $false | Out-Null
            }
       }
    }

Disconnect-SPOService -ErrorAction SilentlyContinue
```




<!--HONumber=Aug16_HO4-->


