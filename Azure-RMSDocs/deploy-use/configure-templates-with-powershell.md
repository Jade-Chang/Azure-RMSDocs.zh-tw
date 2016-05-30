---
# required metadata

title: 自訂範本的 PowerShell 參考 | Azure RMS
description:
keywords:
author: cabailey
manager: mbaldwin
ms.date: 05/20/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 30ee2f77-ce16-4113-bcda-6089131849ec

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: esaggese
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---



# 自訂範本的 PowerShell 參考

*適用於︰Azure Rights Management、Office 365*

您在 Azure 傳統入口網站中建立和管理範本所執行的一切動作，也可以從命令列利用 PowerShell 來完成。 此外，您還可以匯出和匯入範本，以便在租用戶之間複製範本，或對範本中複雜的屬性進行整批編輯，例如多語系名稱和說明。

您可以也使用匯出和匯入來備份和還原您的自訂範本。最佳做法是定期備份您的自訂範本，而如果您進行意外的變更，即可輕易地復原為前一版。

> [!IMPORTANT] 若要使用 Windows PowerShell 建立和管理 Azure RMS 權限原則範本，您必須至少擁有 2.0.0.0 版的[適用於 Azure RMS 的 Windows PowerShell 模組](http://go.microsoft.com/fwlink/?LinkId=257721)。
> 
> 如果您先前已安裝此 PowerShell 模組，請在 PowerShell 視窗中執行下列命令來檢查版本號碼： `(Get-Module aadrm -ListAvailable).Version`

如需安裝指示，請參閱[安裝 Windows PowerShell for Azure Rights Management](install-powershell.md)。

支援建立和管理範本的 Cmdlet：

-   [Add-AadrmTemplate](https://msdn.microsoft.com/library/azure/dn727075.aspx)

-   [Exp或 [新增]t-AadrmTemplate](https://msdn.microsoft.com/library/azure/dn727078.aspx)

-   [Get-AadrmTemplate](https://msdn.microsoft.com/library/azure/dn727079.aspx)

-   [Get-AadrmTemplateProperty](https://msdn.microsoft.com/library/azure/dn727081.aspx)

-   [Imp或 [新增]t-AadrmTemplate](https://msdn.microsoft.com/library/azure/dn727077.aspx)

-   [New-AadrmRightsDefinition](https://msdn.microsoft.com/library/azure/dn727080.aspx)

-   [Remove-AadrmTemplate](https://msdn.microsoft.com/library/azure/dn727082.aspx)

-   [Set-AadrmTemplateProperty](https://msdn.microsoft.com/library/azure/dn727076.aspx)



## 另請參閱
[設定 Azure Rights Management 的自訂範本](configure-custom-templates.md)

<!--HONumber=May16_HO3-->


