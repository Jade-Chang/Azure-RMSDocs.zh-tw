---
# required metadata

title: 設定 Azure Rights Management 和探索服務或資料復原的進階使用者 | Azure RMS
description:
keywords:
author: cabailey
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: acb4c00b-d3a9-4d74-94fe-91eeb481f7e3

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: esaggese
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# 設定 Azure Rights Management 和探索服務或資料復原的進階使用者
Microsoft [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)] (Azure RMS) 的進階使用者功能可確保獲得授權的人員和服務可以永遠讀取及檢查 Azure RMS 為貴組織保護的資料。 並且視需要移除保護或變更先前套用的保護。 進階使用者針對組織的 RMS 租用戶授與的所有使用授權，一律具有完整的擁有者權限。 這個功能有時又稱為「資料的推理」，是維護組織資料控制權的一個關鍵要素。 例如，您會對下列任何案例使用這項功能：

-   員工離職而且您需要讀取他們保護的檔案。

-   IT 系統管理員必須移除已針對檔案設定的目前保護原則，並且套用新的保護原則。

-   Exchange Server 需要針對搜尋作業為信箱編製索引。

-   您對於需要檢查已受保護檔案的資料外洩防護 (DLP) 方案、內容加密閘道 (CEG) 和反惡意程式碼產品有現有 IT 服務。

-   您需要針對稽核、法律或其他法務遵循因素大量解密檔案。

根據預設，未啟用進階使用者功能，而且沒有任何使用者被指派這個角色。 如果您設定適用於 Exchange 的 Rights Management 連接器，且不是執行 Exchange Online、SharePoint Online 或 SharePoint Server 的標準服務必須的項目，則它會為您自動啟用。

如果您需要以手動方式啟用進階使用者功能，使用 Windows PowerShell Cmdlet [Enable-AadrmSuperUserFeature](https://msdn.microsoft.com/library/azure/dn629400.aspx)，然後視需要指派使用者 (或服務帳戶)，方法是使用 [Add-AadrmSuperUser](https://msdn.microsoft.com/library/azure/dn629411.aspx) Cmdlet，或者視需要使用 [Set-AadrmSuperUserGroup](https://msdn.microsoft.com/library/azure/mt653943.aspx) Cmdlet 並且將使用者 (或其他群組) 加入至此群組。 

> [!NOTE]
> 如果您尚未針對 [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)] 安裝 Windows PowerShell 模組，請參閱[針對 Azure Rights Management 安裝 Windows PowerShell](install-powershell.md)。

進階使用者功能的安全性最佳做法：

-   限制和監視被指派 Office 365 或 Azure RMS 租用戶的全域系統管理員的系統管理員，或被指派 GlobalAdministrator 角色的使用者，方法是使用 [Add-AadrmRoleBasedAdministrator](https://msdn.microsoft.com/library/azure/dn629417.aspx) Cmdlet。 這些使用者可以啟用進階使用者功能並且指派使用者 (和本身) 為進階使用者，以及潛在解密您的組織保護的所有檔案。

-   若要查看哪些使用者和服務帳戶已被個別指派為進階使用者，使用 [Get-AadrmSuperUser Cmdlet](https://msdn.microsoft.com/library/azure/dn629408.aspx)。 若要查看是否已設定進階使用者群組，請使用 [Get-AadrmSuperUser](https://msdn.microsoft.com/library/azure/mt653942.aspx) Cmdlet，您的標準使用者管理工具會檢查那些使用者是此群組的成員。 像所有系統管理動作一樣，啟用或停用進階功能，以及新增或移除進階使用者可以使用 [Get-AadrmAdminLog](https://msdn.microsoft.com/library/azure/dn629430.aspx) 命令進行記錄和稽核。 當進階使用者解密檔案時，這個動作可以使用[流量記錄](log-analyze-usage.md)進行記錄和稽核。

-   如果您對於日常服務不需要進階使用者功能，則只有在需要時啟用此功能，並且使用 [Disable-AadrmSuperUserFeature](https://msdn.microsoft.com/library/azure/dn629428.aspx) Cmdlet 再次停用它。

下列記錄擷取顯示使用 Get-AadrmAdminLog Cmdlet 的一些範例項目。 在此範例中，Contoso Ltd 的系統管理員確認進階使用者功能已停用，新增 Richard Simone 做為進階使用者，檢查 Richard 是針對 Azure RMS 設定的唯一進階使用者，然後啟用進階使用者功能，讓 Richard 現在可以解密現在已離職之員工所保護的某些檔案。

`2015-08-01T18:58:20    admin@contoso.com   GetSuperUserFeatureState    Passed  Disabled`

`2015-08-01T18:59:44    admin@contoso.com   AddSuperUser -id rsimone@contoso.com    Passed  True`

`2015-08-01T19:00:51    admin@contoso.com   GetSuperUser    Passed  rsimone@contoso.com`

`2015-08-01T19:01:45    admin@contoso.com   SetSuperUserFeatureState -state Enabled Passed  True`

## 適用於進階使用者的指令碼選項
通常，指派為 [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)] 之進階使用者的人必須從多個位置中的多個檔案移除保護。 雖然可以手動執行這項操作，但是使用指令碼會更有效率 (且通常更可靠)。 若要這樣做，請 [下載 RMS 保護工具](http://www.microsoft.com/en-us/download/details.aspx?id=47256)。 然後，視需要使用 [Unprotect-RMSFile](https://msdn.microsoft.com/library/azure/mt433200.aspx) Cmdlet 和 [Protect-RMSFile](https://msdn.microsoft.com/library/azure/mt433201.aspx) Cmdlet。

如需有關這些 Cmdlet 的詳細資訊，請參閱 [RMS 保護 Cmdlet](https://msdn.microsoft.com/library/azure/mt433195.aspx)。

> [!NOTE]
> RMS 保護工具隨附的 RMS Protection PowerShell 模組不同於主要 [Azure Rights Management 的 Windows PowerShell 模組](administer-powershell.md)的補充。 RMS 保護模組支援 Azure RMS 與 AD RMS。




<!--HONumber=Apr16_HO3-->


