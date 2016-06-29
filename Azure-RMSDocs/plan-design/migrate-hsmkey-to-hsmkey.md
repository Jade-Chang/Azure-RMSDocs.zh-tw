---
# required metadata

title: 步驟 2：受 HSM 保護的金鑰移轉至受 HSM 保護的金鑰 | Azure RMS
description:
keywords:
author: cabailey
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: c5bbf37e-f1bf-4010-a60f-37177c9e9b39

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: esaggese
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# 步驟 2：HSM 保護的金鑰移轉至 HSM 保護的金鑰

*適用於︰Active Directory Rights Management Services、Azure Rights Management*


這些指示是屬於[將路徑從 AD RMS 移轉至 Azure Rights Management](migrate-from-ad-rms-to-azure-rms.md)，且只有在您的 AD RMS 金鑰是 HSM 保護的，而且您想要使用受 HSM 保護的租用戶金鑰移轉至 Azure Rights Management 時才適用。 

如果這不是所選的設定案例，請回到[步驟 2.從 AD RMS 匯出組態資料，並將它匯入至 Azure RMS](migrate-from-ad-rms-to-azure-rms.md#step-2-export-configuration-data-from-ad-rms-and-import-it-to-azure-rms) 並選擇不同的組態。

> [!NOTE]
> 這些指示假設您的 AD RMS 金鑰是模組保護的。 這是常見的情況。 如果您的 AD RMS 金鑰為受 OCS 所保護，請在執行這些指示之前連絡 [AskIPTeam@microsoft.com](mailto: askipteam@microsoft.com?subject=AD%20RMS%20migration%20with%20OCS-protected%20key)。

它是兩部分的程序，可將 HSM 金鑰和 AD RMS 設定匯入至 Azure RMS，以產生由您管理 (BYOK) 的 Azure RMS 租用戶金鑰。

您必須先將 HSM 金鑰封裝，才能將其傳輸至 Azure RMS，然後再與設定資料一併匯入。

## 第 1 篇：封裝 HSM 金鑰使其能傳輸至 Azure RMS

1.  遵循[規劃及實作 Azure Rights Management 租用戶金鑰](plan-implement-tenant-key.md)的[實作整合您自己的金鑰 (BYOK)](plan-implement-tenant-key.md#BKMK_ImplementBYOK) 一節中的步驟，使用**產生並傳輸您的租用戶金鑰 – 透過網際網路**程序，但以部分下除外：

    -   請勿遵循 **產生您的租用戶金鑰**步驟，因為您已經從 AD RMS 部署取得對等項目。 您必須從 Thales 安裝中找出 AD RMS 伺服器所使用的金鑰，並在移轉期間使用這個金鑰。 Thales 加密金鑰檔案在本機伺服器上的命名通常是 **key_(keyAppName)_(keyIdentifier)**。

    -   請勿遵循**將租用戶金鑰傳輸至 Azure RMS** 的步驟，該步驟使用 Add-AadrmKey 命令。  而是要使用 Import-AadrmTpd 命令，在上傳匯出的信任發行網域時，傳輸您備妥的 HSM 金鑰。

2.  在已連線到網際網路的工作站上，在 Windows PowerShell 工作階段中重新連線至 Azure RMS 服務。

現在您已備妥用於 Azure RMS 的 HSM 金鑰，您可以開始匯入您的 HSM 金鑰檔案與 AD RMS 設定資料。

## 第 2 篇：將 HSM 金鑰和設定資訊匯入 Azure RMS

1.  請同樣在連線網際網路的工作站上、Windows PowerShell 工作階段中，上傳第一個匯出的信任發佈網域 (.xml) 檔案： 如果您因為擁有多個信任的發佈網域，而使得所擁有的 .xml 檔案不只一個，則您所選擇的檔案除了應包含已匯出的信任發佈網域外，該網域更應對應至您在轉移後要用來在 Azure RMS 保護內容的 HSM 金鑰。 使用下列命令：

    ```
    Import-AadrmTpd -TpdFile <PathToTpdPackageFile> -ProtectionPassword -HsmKeyFile <PathToBYOKPackage> -Active $True -Verbose
    ```
    例如：**Import -TpdFile E:\no_key_tpd_contosokey1.xml  -HsmKeyFile E:\KeyTransferPackage-contosokey.byok -ProtectionPassword -Active $true -Verbose**

    系統提示時，請輸入您稍早指定的密碼，並確認您想要執行此動作。

2.  當命令完成時，針對匯出信任發行網域而建立的每個 .xml 檔案重複步驟 1。 但為這些檔案執行匯入命令時，請將 **-Active** 設為 **false**。  例如：**Import -TpdFile E:\contosokey2.xml -HsmKeyFile E:\KeyTransferPackage-contosokey.byok -ProtectionPassword -Active $false -Verbose**

3.  使用 [Disconnect-AadrmService](http://msdn.microsoft.com/library/windowsazure/dn629416.aspx) Cmdlet 來中斷 Azure RMS 服務的連線：

    ```
    Disconnect-AadrmService
    ```

您現在可以繼續進行[步驟 3：啟用您的 RMS 租用戶 ](migrate-from-ad-rms-to-azure-rms.md#BKMK_Step3Migration).



<!--HONumber=Apr16_HO4-->


