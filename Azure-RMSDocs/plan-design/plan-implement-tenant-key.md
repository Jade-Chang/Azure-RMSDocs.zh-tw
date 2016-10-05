---
title: "規劃及實作 Azure Rights Management 租用戶金鑰 | Azure Information Protection"
description: "協助您規劃和管理 Azure Information Protection 租用戶金鑰的資訊。 不是 Microsoft 管理租用戶金鑰 (預設值)，而是您可能想要管理您自己的租用戶金鑰，以遵循適用於貴組織的特定法規。 管理您自己的租用戶金鑰也稱為自備金鑰或 BYOK。"
author: cabailey
manager: mbaldwin
ms.date: 09/25/2016
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: f0d33c5f-a6a6-44a1-bdec-5be1bc8e1e14
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: d7e21c2bb07e82bc243e5ab01c0a21aa0fe274d1
ms.openlocfilehash: 967eda9a180f24bc847b55d4315c97dfabb90714


---

# 規劃及實作 Azure Information Protection 租用戶金鑰

>*適用於︰Azure Information Protection、Office 365*

使用本文資訊協助您規劃和管理 Azure Information Protection 租用戶金鑰。 例如，不是 Microsoft 管理租用戶金鑰 (預設值)，而是您可能想要管理您自己的租用戶金鑰，以遵循適用於貴組織的特定法規。 管理您自己的租用戶金鑰也稱為自備金鑰或 BYOK。

> [!NOTE]
> 相當於 Azure Information Protection 租用戶金鑰的內部部署，稱為伺服器授權人憑證 (SLC) 金鑰。 Azure Information Protection 為擁有 Azure Information Protection 訂用帳戶的每個組織維護一或多個金鑰。 只要組織內的 Azure Information Protection 使用金鑰時 (例如使用者金鑰、電腦金鑰、文件加密金鑰)，便會以加密編譯的方式鏈結至您的 Azure Information Protection 租用戶金鑰。

**概覽：** 使用下表做為您建議的租用戶金鑰拓撲的快速指南。 然後，如需詳細資訊，請使用其他文件。

如果您使用 Microsoft 管理的租用戶金鑰部署 Azure Information Protection，則稍後可以變更為 BYOK。 不過，您目前無法將 Azure Information Protection 租用戶金鑰從 BYOK 變更為 Microsoft 管理的租用戶金鑰。

|商務需求|建議的租用戶金鑰拓撲|
|------------------------|-----------------------------------|
|快速部署 Azure Information Protection 且不需要特殊硬體|由 Microsoft 管理|
|在 Exchange Online (含 Azure Rights Management Service) 中需要完整的 IRM 功能|由 Microsoft 管理|
|您的金鑰是由您建立，並以硬體安全性模組 (HSM) 加以保護|BYOK<br /><br />目前，此組態將在 Exchange Online 中導致精簡的 IRM 功能。 如需詳細資訊，請參閱 [BYOK 定價和限制](byok-price-restrictions.md)。|

## 選擇您的租用戶金鑰拓撲：由 Microsoft 管理 (預設) 或由您管理 (BYOK)
決定最適合您組織的租用戶金鑰拓撲。 根據預設，Azure Information Protection 會產生您的租用戶金鑰，並管理租用戶金鑰生命週期的大多數作業。 這是系統管理負擔最小的最簡單選項。 在大多數情況下，您甚至無需知道您擁有租用戶金鑰。 您只要申請 Azure Information Protection，Microsoft 會為您處理金鑰管理程序的剩餘部分。

或者，您可能想要透過使用 [Azure 金鑰保存庫](https://azure.microsoft.com/services/key-vault/)完整控制租用戶金鑰。 此案例包含建立您的租用戶金鑰，以及在您的單位保留主複本。 這種案例通常稱為「自備金鑰 (BYOK)」。 使用此選項時會發生下列狀況：

1.  您會依據您的 IT 原則及安全性原則，在單位上產生租用戶金鑰。

2.  您可從擁有的硬體安全模組 (HSM) 中，使用 Azure 金鑰保存庫，將租用戶金鑰安全地傳輸至 Microsoft 擁有及管理的 HSM。 在整個程序中，您的租用戶金鑰絕對不會離開硬體防護範圍。

3.  當您將租用戶金鑰傳輸到 Microsoft 時，Azure 金鑰保存庫會持續保護該金鑰。

雖然是選用項，您也可能想要使用來自 Azure Information Protection 幾近即時的使用記錄，查看您的租用戶金鑰目前的實際使用方式與時間。

> [!NOTE]
> 作為其他防護措施，Azure 金鑰保存庫對其在北美、EMEA (歐洲、中東和非洲) 和亞洲等區域的資料中心使用不同的安全網域， 而對於 Azure 的不同執行個體，例如 Microsoft Azure 德國及 Azure Government 也是比照辦理。 當您管理自己的租用戶金鑰時，它會連結到您 Azure Information Protection 租用戶所登錄地區或執行個體的安全網域。 例如，歐洲客戶的租用戶金鑰無法在北美或亞洲的資料中心使用。

## 租用戶金鑰生命週期
若您決定 Microsoft 應管理您的租用戶金鑰，Microsoft 會處理大多數金鑰生命週期作業。 不過，若您決定管理您的租用戶金鑰，則您必須負責許多 Azure 金鑰保存庫中的金鑰生命週期作業和其他額外程序。

下列圖表顯示並比較這兩個選項。 第一個圖表顯示當 Microsoft 管理租用戶金鑰時，您在預設設定下承受的系統管理員負擔是如此的低。

![Azure Information Protection 租用戶金鑰週期 - 預設由 Microsoft 管理](../media/RMS_BYOK_cloud.png)

第二張圖顯示當您管理自己的租用戶金鑰時所需執行的其他步驟。

![Azure Information Protection 租用戶金鑰週期 - BYOK 管理](../media/RMS_BYOK_onprem4.png)

若您決定讓 Microsoft 管理您的租用戶金鑰，則您在產生金鑰時無需採取進一步動作，並可直接前往[後續步驟](plan-implement-tenant-key.md#next-steps)。  

若您決定自行管理租用戶金鑰，請閱讀下列各節以取得詳細資訊。

## 實作 Azure Information Protection 租用戶金鑰

若您已決定產生並管理您的租用戶金鑰，請使用本節的資訊和程序；自備金鑰 (BYOK) 案例：


> [!IMPORTANT]
> 如果您已經透過由 Microsoft 管理的租用戶金鑰開始使用 Azure Information Protection，而現在您想要自行管理租用戶金鑰 (移至 BYOK)，您先前受保護的文件和電子郵件仍可使用備份金鑰存取。 不過，如果有使用者執行 Office 2010，在您執行這些程序之前，[請先連絡 Microsoft 支援服務](../get-started/information-support.md#to-contact-microsoft-support)。 這些電腦將需要一些額外設定步驟。
> 
> 如果您的組織具有處理金鑰的特殊原則，亦請[連絡 Microsoft 支援服務](../get-started/information-support.md#to-contact-microsoft-support)。

### BYOK 的必要條件
請參閱下表以取得「自備金鑰 (BYOK)」的必要條件清單。

|需求|詳細資訊|
|---------------|--------------------|
|支援 Azure Information Protection 的訂用帳戶。|如需可用訂用帳戶的詳細資訊，請參閱 Azure Information Protection [定價頁面](https://go.microsoft.com/fwlink/?LinkId=827589)。|
|您未使用個人版 RMS 或 Exchange Online。 或者，如果使用 Exchange Online，您了解並接受使用 BYOK 與此組態搭配的限制。|如需 BYOK 限制和目前限制的詳細資訊，請參閱 [BYOK 定價和限制](byok-price-restrictions.md)。<br /><br />**重要**：目前，BYOK 與 Exchange Online 不相容。|
|為金鑰保存庫 BYOK 所列出的所有必要條件。|請從 Azure 金鑰保存庫文件參閱 [BYOK 的必要條件](https://azure.microsoft.com/documentation/articles/key-vault-hsm-protected-keys/#prerequisites-for-byok)。 <br /><br />**注意**：如果您使用軟體金鑰對硬體金鑰從 AD RMS 移轉到 Azure Information Protection，則 Thales 韌體的版本至少必須是 11.62 版。|
|Windows PowerShell 的 Azure Rights Management 管理模組。|如需安裝指示，請參閱[安裝 Windows PowerShell for Azure Rights Management](../deploy-use/install-powershell.md)。 <br /><br />如果您先前已安裝此 Windows PowerShell 模組，請執行下列命令來檢查版本號碼至少為 **2.5.0.0**： `(Get-Module aadrm -ListAvailable).Version`|

如需 Thales HSM 及其與 Azure 金鑰保存庫搭配使用方式的詳細資訊，請參閱 [Thales 網站](https://www.thales-esecurity.com/msrms/cloud)。

若要產生您自己的租用戶金鑰並將其傳輸至 Azure 金鑰保存庫，請遵循 Azure 金鑰保存庫文件 [How to generate and transfer HSM-protected keys for Azure Key Vault](https://azure.microsoft.com/documentation/articles/key-vault-hsm-protected-keys/) (如何為 Azure 金鑰保存庫產生及傳輸 HSM 保護的金鑰) 中的程序。

當金鑰傳輸至金鑰保存庫時會在其中取得金鑰識別碼，該識別碼為 URL，內含保存庫名稱、金鑰容器、金鑰名稱及金鑰版本。 例如︰**https://contosorms-kv.vault.azure.net/keys/contosorms-byok/aaaabbbbcccc111122223333**。 您必須指定此 URL，藉以通知 Azure Information Protection 的 Azure Rights Management Service。

但必須先將貴組織金鑰保存庫中金鑰的使用權限授與 Azure Rights Management Service，Azure Information Protection 才可以使用金鑰。 為達此目的，Azure 金鑰保存庫系統管理員會使用金鑰保存庫 PowerShell Cmdlet [Set-AzureRmKeyVaultAccessPolicy](https://msdn.microsoft.com/en-us/library/mt603625(v=azure.200\).aspx)，並將權限授與 Azure Rights Management Service 主體 **Microsoft.Azure.RMS**。 例如：

    Set-AzureRmKeyVaultAccessPolicy -VaultName 'ContosoRMS-kv' -ResourceGroupName 'ContosoRMS-byok-rg' -ServicePrincipalName Microsoft.Azure.RMS -PermissionsToKeys decrypt,encrypt,unwrapkey,wrapkey,verify,sign,get

您現在可設定 Azure Information Protection 將此金鑰作為組織的 Azure Information Protection 租用戶金鑰使用。 請使用 Azure RMS Cmdlet，先連接到 Azure Rights Management Service，再登入：

    Connect-AadrmService

接著執行 [Use-AadrmKeyVaultKey Cmdlet](https://msdn.microsoft.com/library/azure/mt759829.aspx)，指定金鑰 URL。 例如：

    Use-AadrmKeyVaultKey -KeyVaultKeyUrl "https://contosorms-kv.vault.azure.net/keys/contosorms-byok/aaaabbbbcccc111122223333"

若需要確認 Azure RMS 服務的 Azure 金鑰保存庫已正確設定金鑰 URL，您可執行 [Get-AzureKeyVaultKey](https://msdn.microsoft.com/library/dn868053.aspx) 來查看金鑰 URL。


## 後續步驟

既然您已規劃在需要時產生租用戶金鑰，請執行下列作業︰

1.  開始使用您的租用戶金鑰：

    -   若您尚未這麼做，則現在必須啟用 Rights Management Service，如此貴組織才能開始使用 Azure Information Protection。 使用者會立即開始使用您的租用戶金鑰 (由 Microsoft 管理或由您在 Azure 金鑰保存庫中自行管理)。

        如需啟用的詳細資訊，請參閱[啟用 Azure Rights Management](../deploy-use/activate-service.md)。

    -   如果您已啟用 Rights Management Service，然後決定管理您自己的租用戶金鑰，使用者會逐漸從舊租用戶金鑰轉移至新租用戶金鑰，而此交錯轉移可能會耗費數週才能完成。 授權的使用者仍可存取舊租用戶金鑰所保護的文件和檔案。

2.  請考慮採用使用記錄，它會記錄 Azure Rights Management Service 執行的每筆交易。

    如果您決定管理您自己的租用戶金鑰，記錄將包含您租用戶金鑰的相關使用資訊。 請參閱 Excel 中顯示的下列記錄檔程式碼片段，其中 **KeyVaultDecryptRequest** 和 **KeyVaultSignRequest** 要求類型會顯示租用戶金鑰正在使用中。

    ![使用租用戶金鑰的 Excel 記錄檔](../media/RMS_Logging.png)

    如需使用記錄的詳細資訊，請參閱[記錄和分析 Azure Rights Management 使用情況](../deploy-use/log-analyze-usage.md)。

3.  維護您的租用戶金鑰。

    如需詳細資訊，請參閱 [Azure Rights Management 租用戶金鑰的作業](../deploy-use/operations-tenant-key.md)。




<!--HONumber=Sep16_HO4-->


