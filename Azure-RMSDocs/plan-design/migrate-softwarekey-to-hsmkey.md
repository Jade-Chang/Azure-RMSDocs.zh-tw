---
# required metadata

title: 步驟 2：軟體保護的金鑰移轉至 HSM 保護的金鑰 | Azure RMS
description:
keywords:
author: cabailey
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: c5f4c6ea-fd2a-423a-9fcb-07671b3c2f4f

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: esaggese
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# 步驟 2：軟體保護的金鑰移轉至 HSM 保護的金鑰

這些指示是屬於[將路徑從 AD RMS 移轉至 Azure Rights Management](migrate-from-ad-rms-to-azure-rms.md)，且只有在您的 AD RMS 金鑰是軟體保護，而且您想要使用受 HSM 保護的租用戶金鑰移轉至 Azure Rights Management 時才適用。 

如果這不是所選的設定案例，請回到[步驟 2.從 AD RMS 匯出組態資料，並將它匯入至 Azure RMS](migrate-from-ad-rms-to-azure-rms.md#step-2-export-configuration-data-from-ad-rms-and-import-it-to-azure-rms) 並選擇不同的組態。

它是三部分的程序，可將 AD RMS 組態匯入至 Azure RMS，以產生由您管理 (BYOK) 的 Azure RMS 租用戶金鑰。

您必須先從組態資料中擷取伺服器授權人憑證 (SLC) 金鑰，並將金鑰傳輸至內部部署 Thales HSM，再將 HSM 金鑰封裝並傳輸至 Azure RMS，然後匯入組態資料。

## 第 1 篇：從組態資料中擷取 SLC，並將金鑰匯入至內部部署 HSM

1.  使用[規劃及實作 Azure Rights Management 租用戶金鑰](plan-implement-tenant-key.md)主題中[實作整合您自己的金鑰 (BYOK)](plan-implement-tenant-key.md#BKMK_ImplementBYOK) 一節中的下列步驟：

    -   產生並傳輸您的租用戶金鑰 – 透過網際網路：準備連線網際網路的工作站

    -   產生並傳輸您的租用戶金鑰 – 透過網際網路： 準備中斷連線的工作站

    請不要遵循這些步驟來產生租用戶金鑰，因為您在匯出的組態資料 (.xml) 檔案中已經有對等項目。 相反地，您將執行命令，從檔案中擷取這個金鑰，並將它匯入至內部部署 HSM。

2.  在中斷連線的工作站上，執行下列命令：

    ```
    KeyTransferRemote.exe -ImportRmsCentrallyManagedKey -TpdFilePath <TPD> -ProtectionPassword -KeyIdentifier <KeyID> -ExchangeKeyPackage <BYOK-KEK-pka-Region> -NewSecurityWorldPackage <BYOK-SecurityWorld-pkg-Region>
    ```
    例如，若為北美洲：KeyTransferRemote.exe -ImportRmsCentrallyManagedKey -TpdFilePath E:\contosokey1.xml -ProtectionPassword -KeyIdentifier contosorms1key –- -ExchangeKeyPackage &lt;BYOK-KEK-pka-NA-1&gt; -NewSecurityWorldPackage &lt;BYOK-SecurityWorld-pkg-NA-1&gt;

    其他資訊：

    -   ImportRmsCentrallyManagedKey 參數會指出作業是匯入 SLC 金鑰。

    -   如果您未在命令中指定密碼，則系統會提示您指定它。

    -   KeyIdentifier 參數是做為建立金鑰檔名稱的金鑰易記名稱。 您只能使用小寫的 ASCII 字元。

    -   ExchangeKeyPackage 參數會指定名稱開頭為 BYOK-KEK-pkg- 的區域特定金鑰交換金鑰 (KEK) 封裝。

    -   NewSecurityWorldPackage 參數會指定名稱開頭為 BYOK-SecurityWorld-pkg- 的安全性世界封裝。

    此命令會產生下列項目：

    -   HSM 金鑰檔：%NFAST_KMDATA%\local\key_mscapi_&lt;KeyID&gt;

    -   已移除 SLC 的 RMS 組態資料檔：%NFAST_KMDATA%\local\no_key_tpd_&lt;KeyID&gt;.xml

3.  如果您有多個 RMS 組態資料檔，請針對這些檔案的其餘檔案重複步驟 2。

現在已擷取您的 SLC，因此它是 HSM 金鑰，而您已準備好將它封裝並傳輸至 Azure RMS。

## 第 2 篇：將 HSM 金鑰封裝並傳輸至 Azure RMS

1.  使用[規劃及實作 Azure Rights Management 租用戶金鑰](plan-implement-tenant-key.md)的[實作整合您自己的金鑰 (BYOK)](plan-implement-tenant-key.md#BKMK_ImplementBYOK) 一節中的下列步驟：

    -   產生並傳輸您的租用戶金鑰 – 透過網際網路： 準備您的租用戶金鑰進行傳輸

    -   產生並傳輸您的租用戶金鑰 – 透過網際網路： 將租用戶金鑰傳輸至 Azure RMS

現在您已將 HSM 金鑰傳輸至 Azure RMS，可以匯入 AD RMS 組態資料 (僅包含新傳輸之租用戶金鑰的指標)。

## 第 3 篇：將組態資料匯入至 Azure RMS

1.  請同樣在連線網際網路的工作站上、Windows PowerShell 工作階段中，複製已移除 SLC 的 RMS 組態檔 (從中斷連線的工作站，%NFAST_KMDATA%\local\no_key_tpd_&lt;KeyID&gt;.xml)

2.  上傳第一個檔案。 如果您因為擁有多個信任的發佈網域，而使得所擁有的 .xml 檔案不只一個，則您所選擇的檔案除了應包含已匯出的信任發佈網域外，該網域更應對應至您在轉移後要用來在 Azure RMS 保護內容的 HSM 金鑰。 使用下列命令：

    ```
    Import-AadrmTpd -TpdFile <PathToNoKeyTpdPackageFile> -ProtectionPassword -HsmKeyFile <PathToKeyTransferPackage> -Active $true -Verbose
    ```
    例如：Import -TpdFile E:\no_key_tpd_contosorms1key.xml -ProtectionPassword -HsmKeyFile E:\KeyTransferPackage-contosorms1key.byok -Active $true -Verbose

    系統提示時，請輸入您稍早指定的密碼，並確認您想要執行此動作。

3.  當命令完成時，針對匯出信任發行網域而建立的每個 .xml 檔案重複步驟 2。 但為這些檔案執行匯入命令時，請將 -Active 設為 false。 例如：Import -TpdFile E:\no_key_tpd_contosorms2key.xml -ProtectionPassword -HsmKeyFile E:\KeyTransferPackage-contosorms1key.byok -Active $false -Verbose

4.  使用 [Disconnect-AadrmService](http://msdn.microsoft.com/library/windowsazure/dn629416.aspx) Cmdlet 來中斷 Azure RMS 服務的連線：

    ```
    Disconnect-AadrmService
    ```

您現在可以繼續進行[步驟 3：啟動您的 RMS 租用戶](migrate-from-ad-rms-to-azure-rms.md#BKMK_Step3Migration)。




<!--HONumber=Apr16_HO3-->


