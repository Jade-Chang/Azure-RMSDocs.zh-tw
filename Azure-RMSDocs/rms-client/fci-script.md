---
title: "使用檔案伺服器資源管理員 FCI 之 Azure RMS 保護的 Windows PowerShell 指令碼 | Azure Information Protection"
description: "複製和編輯的指令碼範例，如＜具有 Windows Server 檔案分類基礎結構的 RMS 保護＞中的指示所述。"
author: cabailey
manager: mbaldwin
ms.date: 10/24/2016
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: ae6d8d0f-4ebc-43fe-a1f6-26b690fd83d0
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: f2723c4417890411230e9dbab4e2d9e36282b1db
ms.openlocfilehash: 0e2ff499fc7c9890a3d8d7327964e3ed5ac19112


---

# 使用檔案伺服器資源管理員 FCI 的 Windows PowerShell Script for Azure RMS 保護

>*適用於︰Azure Information Protection、Windows Server 2012、Windows Server 2012 R2*

此頁面包含複製和編輯的指令碼範例，如[具有 Windows Server 檔案分類基礎結構的 RMS 保護](configure-fci.md)所示。

此指令碼使用 RMS Protection 模組的最低版本 **2.2.0.0**。 執行下列命令以檢查版本： `(Get-Module RMSProtection -ListAvailable).Version` 

*&#42;&#42;免責聲明&#42;&#42;：這個範例指令碼不受任何 Microsoft 標準支援計劃或服務的支援。這個範例指令碼是*
*依現狀提供，不含任何種類的擔保。*

```
<#
.SYNOPSIS 
     Helper script to protect all file types using the Azure Rights Management service and FCI.
.DESCRIPTION
     Protect files with the Azure Rights Management service and Windows Server FCI, using an RMS template ID and RMS Protection module minimum version 2.2.0.0.   
#>
param(
            [Parameter(Mandatory = $false)]
            [ValidateScript({ If($_ -eq "") {$true} else { if (Test-Path -Path $_ -PathType Leaf) {$true} else {throw "Can't find file specified"} } })]
            [string]$File,

            [Parameter(Mandatory = $false)]
            [string]$TemplateID,

            [Parameter(Mandatory = $false)]
            [string]$OwnerMail,

            [Parameter(Mandatory = $false)]
            [string]$AppPrincipalId = "<enter your AppPrincipalId here>",

            [Parameter(Mandatory = $false)]
            [string]$SymmetricKey = "<enter your key here>",

            [Parameter(Mandatory = $false)]
            [string]$BposTenantId = "<enter your BposTenantId here>"
) 

# script information
[String] $Script:Version = 'version 2.0' 
[String] $Script:Name = "RMS-Protect-FCI.ps1"

#global working variables
[switch] $Script:isScriptProcess = $False # Controls the script process. If false, the script gracefully stops running.

#**Functions (general helper)***************************************
function Get-ScriptName(){ 

    return $MyInvocation.ScriptName.Substring($MyInvocation.ScriptName.LastIndexOf('\') + 1, $MyInvocation.ScriptName.LastIndexOf('.') - $MyInvocation.ScriptName.LastIndexOf('\') - 1)
}

#**Functions (script specific)**************************************

function Check-Module{

    param ([String]$Module = $(Throw "Module name not specified"))

    [bool]$isResult = $False

    #try to load the module
    if (get-module -list -name $Module) {
        import-module $Module

        if (get-module -name $Module ) {

            $isResult = $True
        } else {
            $isResult = $False
        } 

    } else {
            $isResult = $False
    }
    return $isResult
}

function Protect-File ($ffile, $ftemplateId, $fownermail) {

    [bool] $returnValue = $false
    try {
        If ($OwnerMail -eq $null -or $OwnerMail -eq "") {
            $protectReturn = Protect-RMSFile -File $ffile -InPlace -TemplateID $ftemplateId
            $returnValue = $true
            Write-Host ( "Information: " + "Protected File: $ffile with Template: $ftemplateId")
        } else {
            $protectReturn = Protect-RMSFile -File $ffile -InPlace -TemplateID $ftemplateId -OwnerEmail $fownermail
            $returnValue = $true
            Write-Host ( "Information: " + "Protected File: $ffile with Template: $ftemplateId, set Owner: $fownermail")
        }
    } catch {
        Write-Host ( "ERROR" + "During protection of file: $ffile with Template: $ftemplateId")
            }
    return $returnValue
}

function Set-RMSConnection ($fappId, $fkey, $fbposId) {

    [bool] $returnValue = $false
    try {
               Set-RMSServerAuthentication -AppPrincipalId $fappId -Key $fkey -BposTenantId $fbposId
        Write-Host ("Information: " + "Connected to Azure RMS Service with BposTenantId: $fbposId using AppPrincipalId: $fappId")
        $returnValue = $true
    } catch {
        Write-Host ("ERROR" + "During connection to Azure RMS Service with BposTenantId: $fbposId using AppPrincipalId: $fappId")

    }
    return $returnValue
}

#**Main Script (Script)*********************************************
Write-Host ("-== " + $Script:Name + " " + $Version + " ==-")

$Script:isScriptProcess = $True

# Validate Azure RMS connection by checking the module and then connection
if ($Script:isScriptProcess) {
        if (Check-Module -Module RMSProtection){
        $Script:isScriptProcess = $True
    } else {

        Write-Host ("The RMSProtection module is not loaded") -foregroundcolor "yellow" -backgroundcolor "black"            
        $Script:isScriptProcess = $False
    }
}

if ($Script:isScriptProcess) {
    #Write-Host ("Try to connect to Azure RMS with AppId: $AppPrincipalId and BPOSID: $BposTenantId" )  
    if (Set-RMSConnection $AppPrincipalId $SymmetricKey $BposTenantId) {
        Write-Host ("Connected to Azure RMS")

    } else {
        Write-Host ("Couldn't connect to Azure RMS") -foregroundcolor "yellow" -backgroundcolor "black"
        $Script:isScriptProcess = $False
    }
}

#  Start working loop
if ($Script:isScriptProcess) {
    if ( !(($File -eq $null) -or ($File -eq "")) ) {
        if (!(Protect-File -ffile $File -ftemplateId $TemplateID -fownermail $OwnerMail)) {
            $Script:isScriptProcess = $False           
        }
    }
}

# Closing
if (!$Script:isScriptProcess) { Write-Host "ERROR occurred during script process" -foregroundcolor "red" -backgroundcolor "black"}
write-host ("-== " + $Script:Name + " " + $Version + "  ==-")
if (!$Script:isScriptProcess) { exit(-1) } else {exit(0)}
```

---

返回[具有 Windows Server 檔案分類基礎結構的 RMS 保護](configure-fci.md)。



<!--HONumber=Oct16_HO4-->


