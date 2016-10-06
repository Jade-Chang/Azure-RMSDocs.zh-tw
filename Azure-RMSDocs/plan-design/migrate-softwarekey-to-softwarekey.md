---
title: "步驟 2：軟體保護的金鑰移轉至軟體保護的金鑰 | Azure Information Protection"
description: "這些指示屬於將路徑從 AD RMS 移轉至 Azure Information Protection，且只有在您的 AD RMS 金鑰是受軟體所保護，而且您想要使用受軟體保護的租用戶金鑰來移轉至 Azure Information Protection 時才適用。"
author: cabailey
manager: mbaldwin
ms.date: 09/25/2016
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 81a5cf4f-c1f3-44a9-ad42-66e95f33ed27
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 931642ea9070a7581b428bcd04756048673fe3c0
ms.openlocfilehash: e6bffd31e7f198a767531fb343b8146246078004


---


# 步驟 2：軟體保護的金鑰移轉至軟體保護的金鑰

>*適用於︰Active Directory Rights Management Services、Azure Information Protection、Office 365*


這些指示屬於[將路徑從 AD RMS 移轉至 Azure Information Protection](migrate-from-ad-rms-to-azure-rms.md)，且只有在您的 AD RMS 金鑰是受軟體所保護，而且您想要使用受軟體保護的租用戶金鑰來移轉至 Azure Information Protection 時才適用。 

如果這不是所選的設定案例，請回到[步驟 2.從 AD RMS 匯出設定資料，並將它匯入 Azure RMS](migrate-from-ad-rms-phase1.md#step-2-export-configuration-data-from-ad-rms-and-import-it-to-azure-rms)，然後選擇不同的設定。

使用下列程序將 AD RMS 組態匯入 Azure Information Protection，以產生由您在 Azure 金鑰保存庫中管理的 Azure Information Protection 租用戶金鑰 (BYOK)。

## 將組態資料匯入 Azure Information Protection

1.  在連線網際網路的工作站上，下載並安裝 Azure Rights Management 的 Windows PowerShell 模組 (最低 2.5.0.0 版)，其中包括 [Import-AadrmTpd](http://msdn.microsoft.com/library/azure/dn857523.aspx) Cmdlet。 Azure Rights Management Service (Azure RMS) 提供 Azure Information Protection 的保護服務。

    > [!TIP]
    > 如果您先前已下載及安裝此模組，請執行下列命令來檢查版本號碼： `(Get-Module aadrm -ListAvailable).Version`

    如需安裝指示，請參閱[安裝 Windows PowerShell for Azure Rights Management](../deploy-use/install-powershell.md)。

2.  使用 [ **以系統管理員身分執行** ] 選項啟動 Windows PowerShell，然後使用 [Connect-AadrmService](http://msdn.microsoft.com/library/azure/dn629415.aspx) Cmdlet 來連接 Azure RMS 服務：

    ```
    Connect-AadrmService
    ```
    出現提示時，輸入您的 [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)] 租用戶系統管理員認證 (通常需要使用 Azure Active Directory 或 Office 365 的全域系統管理員帳戶)。

3.  使用 [Import-AadrmTpd](http://msdn.microsoft.com/library/azure/dn857523.aspx) Cmdlet 上傳第一個匯出的信任發行網域 (.xml) 檔案。 如果您因為擁有多個信任的發佈網域，而使得所擁有的 .xml 檔案不只一個，則您所選擇的檔案應包含已匯出的信任發佈網域，移轉之後您才能使用該網域和 Azure Information Protection 來保護內容。 使用下列命令：

    ```
    Import-AadrmTpd -TpdFile <PathToTpdPackageFile> -ProtectionPassword <secure string> -Active $True -Verbose
    ```
    您可以使用 [ConvertTo-SecureString -AsPlaintext](https://technet.microsoft.com/library/hh849818.aspx) 或 [Read-Host](https://technet.microsoft.com/library/hh849945.aspx) 指定密碼作為安全字串。 當您使用 ConvertTo-SecureString 且密碼有特殊字元時，請在密碼前後加上單引號或逸出特殊字元。
    
    例如：先執行 **$TPD_Password = Read-Host -AsSecureString**，然後輸入您稍早指定的密碼。 接著執行 **Import-AadrmTpd -TpdFile E:\contosokey1.xml -ProtectionPassword $TPD_Password -Active $true -Verbose**。 當系統出現提示時，請確認您要執行此動作。
    
4.  當命令完成時，針對匯出信任發行網域而建立的每個 .xml 檔案重複步驟 3。 但為這些檔案執行匯入命令時，請將 **-Active** 設為 **false**。 例如：**Import-AadrmTpd -TpdFile E:\contosokey2.xml -ProtectionPassword $TPD_Password -Active $false -Verbose**

5.  使用 [Disconnect-AadrmService](http://msdn.microsoft.com/library/azure/dn629416.aspx) Cmdlet 來中斷 Azure Rights Management Service 的連線：

    ```
    Disconnect-AadrmService
    ```


您現在可以繼續進行[步驟 3：啟用 Azure Information Protection 租用戶](migrate-from-ad-rms-phase1.md#step-3-activate-your-rms-tenant)。





<!--HONumber=Sep16_HO4-->


