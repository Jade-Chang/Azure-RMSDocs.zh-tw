---
title: "步驟 2：軟體保護的金鑰移轉至 HSM 保護的金鑰 | Azure Information Protection"
description: "這些指示屬於將路徑從 AD RMS 移轉至 Azure Information Protection，且只有在您的 AD RMS 金鑰是受軟體所保護，而且您想要使用 Azure 金鑰保存庫中受 HSM 保護的租用戶金鑰來移轉至 Azure Information Protection 時才適用。"
author: cabailey
manager: mbaldwin
ms.date: 09/25/2016
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: c5f4c6ea-fd2a-423a-9fcb-07671b3c2f4f
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 931642ea9070a7581b428bcd04756048673fe3c0
ms.openlocfilehash: ae530a9ae861bce8f82fa2e535e5b2281f1c9ffe


---

# 步驟 2：軟體保護的金鑰移轉至 HSM 保護的金鑰

>*適用於︰Active Directory Rights Management Services、Azure Information Protection*


這些指示屬於[將路徑從 AD RMS 移轉至 Azure Information Protection](migrate-from-ad-rms-to-azure-rms.md)，且只有在您的 AD RMS 金鑰是受軟體所保護，而且您想要使用 Azure 金鑰保存庫中受 HSM 保護的租用戶金鑰來移轉至 Azure Information Protection 時才適用。 

如果這不是所選的設定案例，請回到[步驟 2.從 AD RMS 匯出設定資料，並將它匯入 Azure RMS](migrate-from-ad-rms-phase1.md#step-2-export-configuration-data-from-ad-rms-and-import-it-to-azure-rms)，然後選擇不同的設定。

其為四部分的程序，可將 AD RMS 組態匯入 Azure Information Protection，以產生由您在 Azure 金鑰保存庫中管理的 Azure Information Protection 租用戶金鑰 (BYOK)。

您必須先從 AD RMS 組態資料中擷取伺服器授權人憑證 (SLC) 金鑰，並將金鑰傳輸至內部部署 Thales HSM，再將 HSM 金鑰封裝並傳輸至 Azure 金鑰保存庫，然後授權 Azure Information Protection 的 Azure Rights Management Service 存取您的金鑰保存庫，並匯入組態資料。

由於您的 Azure Information Protection 租用戶金鑰將由 Azure 金鑰保存庫儲存和管理，因此這部分的移轉除了 Azure Information Protection 外，還需要 Azure 金鑰保存庫中的管理。 若您組織的 Azure 金鑰保存庫並非由您管理，而是由其他系統管理員所管理，則您需要與該名系統管理員共同合作，才能完成這些程序。

在開始之前，請確定您的組織已在 Azure 金鑰保存庫中建立金鑰保存庫，且其支援 HSM 保護的金鑰。 雖然並非必要，但仍建議您具備 Azure Information Protection 的專用金鑰保存庫。 此金鑰保存庫會設定為允許 Azure Information Protection 的 Azure Rights Management Service 存取，因此此金鑰保存庫儲存的金鑰應該只限制為 Azure Information Protection 金鑰。


> [!TIP]
> 若您將進行 Azure 金鑰保存庫的設定步驟，但不熟悉這項 Azure 服務，建議您先檢閱[開始使用 Azure 金鑰保存庫](https://azure.microsoft.com/documentation/articles/key-vault-get-started/)。 


## 第 1 篇：從設定資料中擷取 SLC 金鑰，並將金鑰匯入內部部署 HSM

1.  Azure 金鑰保存庫系統管理員︰使用 Azure 金鑰保存庫文件[實作 Azure 金鑰保存庫的自備金鑰 (BYOK)](https://azure.microsoft.com/documentation/articles/key-vault-hsm-protected-keys/#implementing-bring-your-own-key-byok-for-azure-key-vault) 章節中的下列步驟︰

    -   **產生金鑰並將其傳輸至 Azure 金鑰保存庫 HSM**：[步驟 1：準備連線網際網路的工作站](https://azure.microsoft.com/documentation/articles/key-vault-hsm-protected-keys/#step-1-prepare-your-internet-connected-workstation)

    -   **產生並傳輸您的租用戶金鑰 – 透過網際網路**：[步驟 2：準備中斷連線的工作站](https://azure.microsoft.com/documentation/articles/key-vault-hsm-protected-keys/#step-2-prepare-your-disconnected-workstation)

    請不要遵循這些步驟來產生租用戶金鑰，因為您在匯出的組態資料 (.xml) 檔案中已經有對等項目。 相反地，您將執行工具，從檔案中擷取這個金鑰，並將其匯入內部部署 HSM。 此工具會在您加以執行時建立兩個檔案︰

    - 新的組態資料檔沒有金鑰，且隨時可以匯入您的 Azure Information Protection 租用戶中。

    - 具有金鑰的 PEM 檔案 (金鑰容器)，且已就緒匯入您的內部部署 HSM 中。

2. Azure Information Protection 系統管理員或 Azure 金鑰保存庫系統管理員︰在中斷連線的工作站上，執行 [Azure RMS 移轉工具組](https://go.microsoft.com/fwlink/?LinkId=524619) TpdUtil 工具。 例如，若工具安裝在 E 磁碟機上，也就是您複製名為 ContosoTPD.xml 的設定資料檔之處︰

    ```
        E:\TpdUtil.exe /tpd:ContosoTPD.xml /otpd:ContosoTPD.xml /opem:ContosoTPD.pem
    ```

    如果您有多個 RMS 設定資料檔，請針對這些檔案的其餘檔案執行此工具。

    若要查看這項工具的說明 (內含描述、使用方式及範例)，請執行 TpdUtil.exe 而不使用任何參數

    此命令的其他資訊︰

    - **/tpd**︰指定匯出的 AD RMS 設定資料檔的完整路徑及名稱。 完整的參數名稱是 **TpdFilePath**。

    - **/otpd**︰為不具金鑰的設定資料檔指定輸出檔案名稱。 完整的參數名稱是 **OutPfxFile**。 若未指定此參數，輸出檔案預設為原始檔案名稱，尾碼為 **_keyless**，並儲存在目前資料夾中。

    - **/opem**︰指定 PEM 檔案的輸出檔案名稱，其中內含擷取的金鑰。 完整的參數名稱是 **OutPemFile**。 若未指定此參數，輸出檔案預設為原始檔案名稱，尾碼為 **_key**，並儲存在目前資料夾中。

    - 若在執行此命令 (使用 **TpdPassword** 完整參數名稱或 **pwd** 簡短參數名稱) 時未指定密碼，系統將會提示您加以指定。

3. 在相同的中斷連線工作站上，依據您的 Thales 文件附加並設定 Thales HSM。 您現在可以使用下列命令將您的金鑰匯入附加的 Thales HSM 內，其中您必須使用您自己的檔案名稱來替代 ContosoTPD.pem︰

        generatekey --import simple pemreadfile=e:\ContosoTPD.pem plainname=ContosoBYOK protect=module ident=contosobyok type=RSA

    > [!NOTE]
    >若您有多個檔案，則您所選擇的檔案應對應至您在轉移後要用來在 Azure RMS 保護內容的 HSM 金鑰。

    這將會產生類似下列的輸出顯示︰

    **金鑰產生參數︰**

    **作業 &nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 要執行的作業 &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 匯入**

    **應用程式 &nbsp;&nbsp;&nbsp;&nbsp;應用程式&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 簡易**

    **驗證 &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 驗證設定金鑰的安全性&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 是**

    **類型 &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 金鑰類型 &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; RSA**

    **pemreadfile &nbsp;&nbsp; PEM 檔案，其中內含 RSA 金鑰 &nbsp;&nbsp; e:\ContosoTPD.pem**

    **ident &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 金鑰識別碼 &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; contosobyok**

    **plainname &nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 金鑰名稱 &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; ContosoBYOK**

    **已成功匯入金鑰。**

    **金鑰路徑︰C:\ProgramData\nCipher\Key Management Data\local\key_simple_contosobyok**

此輸出確認私密金鑰現已移轉至內部部署 Thales HSM 裝置，且加密複本已儲存至金鑰 (在本例中為 "key_simple_contosobyok")。 

現已擷取 SLC 金鑰並將其匯入內部部署 HSM，您便已就緒封裝 HSM 保護的金鑰，並將其傳輸至 Azure 金鑰保存庫。

> [!IMPORTANT]
> 完成此步驟後，請安全地從中斷連線的工作站清除這些 PEM 檔案，以確保未經授權的人員無法加以存取。 例如，執行 "cipher /w:E" 以便安全地從 E: 磁碟機刪除所有檔案。

## 第 2 篇：將 HSM 金鑰封裝並傳輸至 Azure 金鑰保存庫

1.  Azure 金鑰保存庫系統管理員︰使用 Azure 金鑰保存庫文件[實作 Azure 金鑰保存庫的自備金鑰 (BYOK)](https://azure.microsoft.com/documentation/articles/key-vault-hsm-protected-keys/#implementing-bring-your-own-key-byok-for-azure-key-vault) 章節中的下列步驟︰

    -   [步驟 4：準備傳輸您的金鑰](https://azure.microsoft.com/documentation/articles/key-vault-hsm-protected-keys/#step-4-prepare-your-key-for-transfer)

    -   [步驟 5：將您的金鑰傳輸至 Azure 金鑰保存庫](https://azure.microsoft.com/documentation/articles/key-vault-hsm-protected-keys/#step-5-transfer-your-key-to-azure-key-vault)

    您已具備金鑰，因此請勿遵循這些步驟產生您的金鑰組。 請改為執行命令，從您的內部部署 HSM 傳輸此金鑰 (在本例中，KeyIdentifier 參數使用 "contosobyok")。

    在您將金鑰傳輸至 Azure 金鑰保存庫之前，請確認 KeyTransferRemote.exe 公用程式會在您使用降低權限建立金鑰複本 (步驟 4.1) 及加密金鑰 (步驟 4.3) 時，傳回**結果: SUCCESS**。

    您會在金鑰上傳至 Azure 金鑰保存庫時看到金鑰的屬性，其中包含金鑰識別碼。 識別碼類似於：**https://contosorms-kv.vault.azure.net/keys/contosorms-byok/aaaabbbbcccc111122223333**。 請記下此 URL，因為 Azure Information Protection 管理員會需要它來告知 Azure Information Protection 的 Azure Rights Management Service 將這個金鑰用於其租用戶金鑰。

    現在您已將 HSM 金鑰傳輸至 Azure 金鑰保存庫，可開始匯入您的 AD RMS 設定資料。

## 第 3 篇：將組態資料匯入 Azure Information Protection

1.  Azure Information Protection 系統管理員：在網際網路連線的工作站上及 PowerShell 工作階段中，複製在執行 TpdUtil 工具後移除 SLC 金鑰的新組態資料檔 (.xml)。

2. 使用 [Import-AadrmTpd](https://msdn.microsoft.com/library/dn857523.aspx) Cmdlet 上傳第一個 .xml 檔案。 如果您因為擁有多個信任的發行網域，而使得所擁有的 .xml 檔案不只一個，則您所選擇的檔案應對應至在移轉後和 Azure Information Protection 一起保護內容的 HSM 金鑰。

    若要執行此 Cmdlet，您需要上一個步驟中所找到之金鑰的 URL。

    例如，使用上一個步驟的金鑰 URL 值及 C:\contoso_keyless.xml 的設定資料檔，您會執行︰

    ```
    Import-AadrmTpd -TpdFile "C:\contoso_keyless.xml" -ProtectionPassword –KeyVaultStringUrl https://contoso-byok-kv.vault.azure.net/keys/contosorms-byok/aaaabbbbcccc111122223333 -Active $True -Verbose
    ```

    系統提示時，請輸入您稍早為設定資料檔指定的密碼，並確認您想要執行此動作。

    如果您有多個設定資料檔，請針對這些檔案的其餘檔案重複此命令。 但為這些檔案執行匯入命令時，請將 **-Active** 設為 **false**。



3.  使用 [Disconnect-AadrmService](http://msdn.microsoft.com/library/windowsazure/dn629416.aspx) Cmdlet 來中斷 Azure Rights Management Service 的連線：

    ```
    Disconnect-AadrmService
    ```

    > [!NOTE]
    > 若您稍後需要確認 Azure Information Protection 租用戶金鑰在 Azure 金鑰保存庫中使用哪個金鑰，請使用 [Get-AadrmKeys](https://msdn.microsoft.com/library/dn629420.aspx) Azure RMS Cmdlet。


您現在可以繼續進行[步驟 3：啟用 Azure Information Protection 租用戶](migrate-from-ad-rms-phase1.md#step-3-activate-your-rms-tenant)。






<!--HONumber=Sep16_HO4-->


