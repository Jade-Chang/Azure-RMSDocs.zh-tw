---
title: "使用 Windows PowerShell 管理 Azure Rights Management | Azure RMS"
description: 
keywords: 
author: cabailey
manager: mbaldwin
ms.date: 08/18/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: a890e04a-4b70-41b5-8d5f-3c210a669faa
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: a80866576dc7d6400bcebc2fc1c37bc0367bcdf3
ms.openlocfilehash: d2aec9c4a0c462e9abfa145ee14df0144c60e584


---

# 使用 Windows PowerShell 管理 Azure Rights Management

*適用於︰Azure Rights Management、Office 365*

雖然您可以使用 [!INCLUDE[o365_2](../includes/o365_2_md.md)] 系統管理中心或是 Azure 傳統入口網站來啟用 Microsoft [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)] (Azure RMS)，但是也可以使用適用於 [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)] (AADRM) 的 Windows PowerShell 模組來執行這項操作。

在您啟用 [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)] 之後，可能就不需要進一步管理服務。 不過，有些進階組態案例可能會需要您使用適用於 [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)] 的 Windows PowerShell 模組。 下表列出一些使用 Windows PowerShell 的進階組態案例。 如需可用 Cmdlet 的完整清單和每個項目的詳細資訊，請參閱＜ [Azure Rights Management Cmdlets](http://msdn.microsoft.com/library/azure/dn629398.aspx)＞。

> [!NOTE]
> 如果您需要針對 [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)] 安裝 Windows PowerShell 模組，請參閱[針對 Azure Rights Management 安裝 Windows PowerShell](install-powershell.md)。

還有一個補充的 Windows PowerShell 模組 **RMSProtection**，可支援 Azure RMS 與 AD RMS。 這個模組支援保護和移除保護多個檔案，比方說，這樣就可以大量保護資料夾中的所有檔案。 如需詳細資訊，請參閱[設定 Azure Rights Management 和探索服務或資料復原的進階使用者](configure-super-users.md)一文中的[進階使用者的指令碼選項](configure-super-users.md#scripting-options-for-super-users)章節。

|如果您需要...|…請使用下列 Cmdlet|
|-------------------|------------------------------|
|從內部部署 Rights Management (AD RMS 或 Windows RMS) 移轉到 [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)]。|[Import-AadrmTpd](http://msdn.microsoft.com/library/azure/dn857523.aspx)|
|連線至貴組織的 [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)] 服務或與其中斷連線。|[Connect-AadrmService](http://msdn.microsoft.com/library/azure/dn629415.aspx)<br /><br />[Disconnect-AadrmService](http://msdn.microsoft.com/library/azure/dn629416.aspx)|
|自行產生並管理租用戶金鑰 – 自備金鑰 (BYOK) 案例。|[Use-AadrmKeyVaultKey](https://msdn.microsoft.com/library/azure/mt759829.aspx)<br /><br />[Get-AadrmKeys](http://msdn.microsoft.com/library/azure/dn629420.aspx)|
|啟用或停用貴組織的 [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)] 服務。|[Enable-Aadrm](http://msdn.microsoft.com/library/azure/dn629412.aspx)<br /><br />[Disable-Aadrm](http://msdn.microsoft.com/library/azure/dn629422.aspx)|
|停用或啟用 Azure Rights management 的文件追蹤網站。|[Disable-AadrmDocumentTrackingFeature](https://msdn.microsoft.com/library/azure/mt548471.aspx)<br /><br />[Enable-AadrmDocumentTrackingFeature](https://msdn.microsoft.com/library/azure/mt548469.aspx)<br /><br />[Get-AadrmDocumentTrackingFeature](https://msdn.microsoft.com/library/azure/mt548470.aspx)|
|設定 Azure Rights Management 階段式部署的上線控制。|[Get-AadrmOnboardingControlPolicy](http://msdn.microsoft.com/library/azure/dn857522.aspx)<br /><br />[Set-AadrmOnboardingControlPolicy](http://msdn.microsoft.com/library/azure/dn857521.aspx)|
|建立和管理組織的權限原則範本。|[Add-AadrmTemplate](http://msdn.microsoft.com/library/azure/dn727075.aspx)<br /><br />[Exp或 [新增]t-AadrmTemplate](http://msdn.microsoft.com/library/azure/dn727078.aspx)<br /><br />[Get-AadrmTemplate](http://msdn.microsoft.com/library/azure/dn727079.aspx)<br /><br />[Get-AadrmTemplateProperty](http://msdn.microsoft.com/library/azure/dn727081.aspx)<br /><br />[Imp或 [新增]t-AadrmTemplate](http://msdn.microsoft.com/library/azure/dn727077.aspx)<br /><br />[New-AadrmRightsDefinition](http://msdn.microsoft.com/library/azure/dn727080.aspx)<br /><br />[Remove-AadrmTemplate](http://msdn.microsoft.com/library/azure/dn727082.aspx)<br /><br />[Set-AadrmTemplateProperty](http://msdn.microsoft.com/library/azure/dn727076.aspx)|
|設定在沒有網際網路連線的情況下，最多有幾天可以存取您的組織所保護的內容 (使用授權有效期間)。|[Get-AadrmMaxUseLicenseValidityTime](https://msdn.microsoft.com/library/azure/dn932062.aspx)<br /><br />[Set-AadrmMaxUseLicenseValidityTime](https://msdn.microsoft.com/library/azure/dn932063.aspx)|
|管理貴組織之 [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)] 的進階使用者功能。|[Enable-AadrmSuperUserFeature](https://msdn.microsoft.com/library/azure/dn629400.aspx)<br /><br />[Disable-AadrmSuperUserFeature](https://msdn.microsoft.com/library/azure/dn629428.aspx)<br /><br />[Add-AadrmSuperUser](http://msdn.microsoft.com/library/azure/dn629411.aspx)<br /><br />[Get-AadrmSuperUser](https://msdn.microsoft.com/library/azure/dn629408.aspx)<br /><br />[Remove-AadrmSuperUser](https://msdn.microsoft.com/library/azure/dn629405.aspx)<br /><br />[Set-AadrmSuperUserGroup](https://msdn.microsoft.com/library/azure/mt653943.aspx)<br /><br />[Get-AadrmSuperUserGroup](https://msdn.microsoft.com/library/azure/mt653942.aspx)<br /><br />[Clear-AadrmSuperUserGroup](https://msdn.microsoft.com/library/azure/mt653944.aspx)|
|管理已獲授權為貴組織管理 [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)] 服務的使用者和群組。|[Add-AadrmRoleBasedAdministrator](http://msdn.microsoft.com/library/azure/dn629417.aspx)<br /><br />[Get-AadrmRoleBasedAdministrator](https://msdn.microsoft.com/library/azure/dn629407.aspx)<br /><br />[Remove-AadrmRoleBasedAdministrator](https://msdn.microsoft.com/library/azure/dn629424.aspx)|
|取得貴組織的 [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)] 管理工作記錄。|[Get-AadrmAdminLog](https://msdn.microsoft.com/library/azure/dn629430.aspx)|
|記錄並分析 [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)] 的使用狀況記錄。|[Get-AadrmUserLog](https://msdn.microsoft.com/library/azure/mt653941.aspx)|
|顯示貴組織目前的 [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)] 服務組態。|[Get-AadrmConfiguration](http://msdn.microsoft.com/library/azure/dn629410.aspx)|
|將貴組織從 [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)] 移轉至內部部署的 AD RMS 部署。|[Set-AadrmMigrationUrl](https://msdn.microsoft.com/library/azure/dn629429.aspx)<br /><br />[Get-AadrmMigrationUrl](http://msdn.microsoft.com/library/azure/dn629403.aspx)|






<!--HONumber=Aug16_HO3-->


