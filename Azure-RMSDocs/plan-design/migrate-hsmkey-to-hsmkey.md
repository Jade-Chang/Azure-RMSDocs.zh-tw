---
title: "步驟 2：受 HSM 保護的金鑰移轉至受 HSM 保護的金鑰 | Azure RMS"
description: 
keywords: 
author: cabailey
manager: mbaldwin
ms.date: 08/17/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: c5bbf37e-f1bf-4010-a60f-37177c9e9b39
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 437afd88efebd9719a3db98f8ab0ae07403053f7
ms.openlocfilehash: 86f7bd025824b23c8eecdb05b62d83204ae1ccb4


---

# 步驟 2：HSM 保護的金鑰移轉至 HSM 保護的金鑰

*適用於︰Active Directory Rights Management Services、Azure Rights Management*


這些指示屬於[將路徑從 AD RMS 移轉至 Azure Rights Management](migrate-from-ad-rms-to-azure-rms.md)，且只有在您的 AD RMS 金鑰是 HSM 保護的，而且您想要使用 Azure 金鑰保存庫中受 HSM 保護的租用戶金鑰移轉至 Azure Rights Management 時才適用。 

如果這不是所選的設定案例，請回到[步驟 2.從 AD RMS 匯出設定資料，並將它匯入 Azure RMS](migrate-from-ad-rms-phase1.md#step-2-export-configuration-data-from-ad-rms-and-import-it-to-azure-rms)，然後選擇不同的設定。

> [!NOTE]
> 這些指示假設您的 AD RMS 金鑰是模組保護的。 這是最典型的情況。 

它是兩部分的程序，可將 HSM 金鑰和 AD RMS 設定匯入至 Azure RMS，以產生由您管理 (BYOK) 的 Azure RMS 租用戶金鑰。

由於您的 Azure RMS 租用戶金鑰將由 Azure 金鑰保存庫儲存和管理，因此這部分的移轉除了 Azure 金鑰 RMS 外，還需要 Azure 金鑰保存庫中的管理。 若您組織的 Azure 金鑰保存庫並非由您管理，而是由其他系統管理員所管理，則您需要與該名系統管理員共同合作，才能完成這些程序。

在開始之前，請確定您的組織已在 Azure 金鑰保存庫中建立金鑰保存庫，且其支援 HSM 保護的金鑰。 雖然並非必要，但仍建議您具備 Azure RMS 的專用金鑰保存庫。 此金鑰保存庫將設定為允許 Azure RMS 進行存取，所以此金鑰保存庫所儲存的金鑰應僅限於 Azure RMS 金鑰。


> [!TIP]
> 若您將進行 Azure 金鑰保存庫的設定步驟，但不熟悉這項 Azure 服務，建議您先檢閱[開始使用 Azure 金鑰保存庫](https://azure.microsoft.com/documentation/articles/key-vault-get-started/)。 


## 第 1 篇：將您的 HSM 金鑰傳輸至 Azure 金鑰保存庫

這些程序由 Azure 金鑰保存庫的系統管理員完成。

1.  遵循 Azure 金鑰保存庫文件中的指示，使用[實作 Azure 金鑰保存庫的自備金鑰 (BYOK)](https://azure.microsoft.com/documentation/articles/key-vault-hsm-protected-keys/#implementing-bring-your-own-key-byok-for-azure-key-vault)，但其中有項例外︰

    - 請勿執行**產生您的租用戶金鑰**步驟，因為您已從 AD RMS 部署取得對等項目。 您需改為從 Thales 安裝中找出 AD RMS 伺服器所使用的金鑰，並在移轉期間使用這個金鑰。 Thales 加密金鑰檔案在本機伺服器上的命名通常是 **key<*keyAppName*><*keyIdentifier*>**。

    您會在金鑰上傳至 Azure 金鑰保存庫時看到金鑰的屬性，其中包含金鑰識別碼。 識別碼類似於：https://contosorms-kv.vault.azure.net/keys/contosorms-byok/aaaabbbbcccc111122223333。 由於 Azure RMS 系統管理員需要此 URL 才能告知 Azure RMS 對其租用戶金鑰使用此金鑰，因此請記下此 URL。

2. 在連線到網際網路的工作站上 PowerShell 工作階段中使用 [Set-AzureRmKeyVaultAccessPolicy](https://msdn.microsoft.com/library/mt603625.aspx ) Cmdlet，授權 Azure RMS 服務主體 (Microsoft.Azure.RMS) 存取將儲存 Azure RMS 租用戶金鑰的金鑰保存庫。 所需的權限包括解密、加密、解除包裝金鑰、包裝金鑰、驗證及簽署。
    
    例如，若您已建立的 Azure RMS 金鑰保存庫名為 contoso-byok-ky，且資源群組名為 contoso-byok-rg，則執行下列命令︰
    
        Set-AzureRmKeyVaultAccessPolicy -VaultName "contoso-byok-kv" -ResourceGroupName "contoso-byok-rg" -ServicePrincipalName Microsoft.Azure.RMS -PermissionsToKeys decrypt,encrypt,unwrapkey,wrapkey,verify,sign


現在您已在 Azure RMS 的 Azure 金鑰保存庫中備妥 HSM 金鑰，可開始匯入您的 AD RMS 設定資料。

## 第 2 篇：將設定資料匯入 Azure RMS

這些程序由 Azure RMS 的系統管理員完成。

1.  在連線到網際網路的工作站上及 PowerShell 工作階段中，使用 [Connnect-AadrmService](https://msdn.microsoft.com/library/dn629415.aspx ) Cmdlet 連接至 Azure RMS。
    
    接著使用 [Import-AadrmTpd](https://msdn.microsoft.com/library/dn857523.aspx) Cmdlet 上傳第一個匯出的信任發行網域 (.xml) 檔案。 如果您因為擁有多個信任的發佈網域，而使得所擁有的 .xml 檔案不只一個，則您所選擇的檔案除了應包含已匯出的信任發佈網域外，該網域更應對應至您在轉移後要用來在 Azure RMS 保護內容的 HSM 金鑰。 
    
    若要執行此 Cmdlet，您需要上一個步驟中所找到之金鑰的 URL。
    
    例如，使用上一個步驟的金鑰 URL 值及 C:\contoso-tpd1.xml 的 TPD 檔案，您會執行︰
    
    ```
    Import-AadrmTpd -TpdFile "C:\contoso-tpd1.xml" -ProtectionPassword –KeyVaultStringUrl https://contoso-byok-kv.vault.azure.net/keys/contosorms-byok/aaaabbbbcccc111122223333 -Active $True -Verbose
    ```
    
    系統提示時，請輸入您稍早指定的密碼，並確認您想要執行此動作。

2.  當命令完成時，針對匯出信任發行網域而建立的每個 .xml 檔案重複步驟 1。 但為這些檔案執行匯入命令時，請將 **-Active** 設為 **false**。  

3.  使用 [Disconnect-AadrmService](http://msdn.microsoft.com/library/windowsazure/dn629416.aspx) Cmdlet 來中斷 Azure RMS 服務的連線：

    ```
    Disconnect-AadrmService
    ```

    > [!NOTE]
    > 若您稍後需要確認 Azure RMS 租用戶金鑰在 Azure 金鑰保存庫中使用哪個金鑰，請使用 [Get-AadrmKeys](https://msdn.microsoft.com/library/dn629420.aspx) Azure RMS Cmdlet。

您現在可以繼續進行[步驟 3：啟動您的 RMS 租用戶](migrate-from-ad-rms-phase1.md#step-3-activate-your-rms-tenant)。




<!--HONumber=Aug16_HO3-->


