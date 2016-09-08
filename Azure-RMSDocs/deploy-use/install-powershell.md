---
title: "針對 Azure Rights Management 安裝 Windows PowerShell | Azure RMS"
description: "使用下列資訊可協助您安裝適用於 Microsoft Azure RMS 的 Windows PowerShell。"
author: cabailey
manager: mbaldwin
ms.date: 08/17/2016
ms.topic: article
ms.prod: 
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 0d665ed6-b1de-4d63-854a-bc57c1c49844
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 26b043f1f9e7a1e0cd00c2f31c28f7d6685f0232
ms.openlocfilehash: 0f22d69387b89a590b516d3a93148fec82b23acd


---

# 針對 Azure Rights Management 安裝 Windows PowerShell

>*適用於︰Azure Rights Management、Office 365*

使用下列資訊可協助您安裝適用於 Microsoft [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)] (Azure RMS) 的 Windows PowerShell。

您可以使用此 PowerShell 模組從命令列管理 [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)]，方法是使用任何具有網際網路連線，且符合下一節所列必要條件的電腦。 適用於 [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)] 的 Windows PowerShell 支援自動化的指令碼處理，或可能是進階組態案例的必要項目。 如需有關此模組支援的管理工作與組態等詳細資訊，請參閱[使用 Windows PowerShell 管理 Azure Rights Management](administer-powershell.md)。

## 必要條件
此表列出安裝及使用適用於 [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)] 之 Windows PowerShell 的必要條件。

|需求|詳細資訊|
|---------------|--------------------|
|一個支援 [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)] 管理模組的 Windows 版本|檢查 Azure Rights Management 系統管理工具下載頁面的 **系統必要條件** 章節 [中，支援的作業系統清單](http://go.microsoft.com/fwlink/?LinkId=257721)。|
|Windows PowerShell 最低版本：2.0|Windows PowerShell 2.0 中導入了 [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)] 管理模組支援。<br /><br />大多數 Windows 作業系統預設都至少附帶安裝 2.0 版的 Windows PowerShell。 如果您需要安裝 Windows PowerShell 2.0，請參閱 [安裝 Windows PowerShell 2.0](http://msdn.microsoft.com/library/ff637750.aspx)。<br /><br />提示：您可以在 PowerShell 工作階段中輸入 `$PSVersionTable` 來確認您正在執行的 Windows PowerShell 版本。|
|Microsoft .NET Framework 最低版本：4.5<br /><br />注意：較新版的作業系統會隨附此版 Microsoft .NET Framework，因此只有在用戶端作業系統比 Windows 8.0 還舊或伺服器作業系統比 Windows Server 2012 還舊時，才需要以手動方式加以安裝。|如果尚未安裝 Microsoft .NET Framework 的最低版本，您可以下載 [Microsoft .NET Framework 4.5](http://www.microsoft.com/download/details.aspx?id=30653)。<br /><br />[!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)] 管理模組使用的一些類別需要這個最低版本的 Microsoft .NET Framework。|

> [!NOTE]
> 自 Rights Management 管理模組版本 2.5.0.0 起，不再需要 Microsoft Online Services 登入小幫手。
> 
> 如果您安裝的 Rights Management 管理模組為先前版本，請先使用 [程式和功能] 將 **Windows Azure AD Rights Management 管理**解除安裝後，再安裝最新版本。


## 如何安裝 Rights Management 管理模組

1.  移至 Microsoft 下載中心並[下載 Azure Rights Management 管理工具](https://go.microsoft.com/fwlink/?LinkId=257721)，其中包含適用於 Windows PowerShell 的 [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)] 管理模組。

2.  從您下載並儲存 [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)] 安裝程式檔案的本機資料夾，按兩下您為平台下載的可執行檔 (WindowsAzureADRightsManagementAdministration_x64 or WindowsAzureADRightsManagementAdministration_x86.exe) 來啟動 Azure AD Rights Management 管理安裝程式精靈。

3.  完成精靈。

現在已安裝適用於 [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)] 的Windows PowerShell。

## 後續步驟
若要查看有哪些 Cmdlet 可用，請使用 **[以系統管理員身分執行]** 選項啟動 Windows PowerShell 並輸入下列命令：

```
Get-Command -Module aadrm
```
使用 `the Get-Help <cmdlet_name>` 命令可查看特定 Cmdlet 的說明。

如需詳細資訊：

-   可用 Cmdlet 的完整清單： [Azure Rights Management Cmdlet](https://msdn.microsoft.com/library/windowsazure/dn629398.aspx)

-   支援 Windows PowerShell 的主要組態案例清單︰[使用 Windows PowerShell 管理 Azure Rights Management](administer-powershell.md)

若要執行任何設定 [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)] 服務的命令，您必須先使用 [Connect-AadrmService](https://msdn.microsoft.com/library/windowsazure/dn629415.aspx) Cmdlet 來連線至該服務。 當您執行完想要的組態命令時，請使用 [Disconnect-AadrmService](https://msdn.microsoft.com/library/windowsazure/dn629416.aspx) Cmdlet 中斷服務的連線。

> [!NOTE]
> 如果您尚未啟用 [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)]，可以在連線至該服務之後，使用 [Enable-Aadrm](https://msdn.microsoft.com/library/windowsazure/dn629412.aspx) Cmdlet 來啟用它。

## 另請參閱
[使用 Windows PowerShell 管理 Azure Rights Management](administer-powershell.md)



<!--HONumber=Aug16_HO4-->


