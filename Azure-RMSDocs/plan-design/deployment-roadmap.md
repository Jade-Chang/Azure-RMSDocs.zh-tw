---
title: "Azure 資訊保護部署藍圖 | Azure 資訊保護"
description: "使用下列步驟為組織準備、實作及管理 Azure 資訊保護。"
author: cabailey
manager: mbaldwin
ms.date: 10/05/2016
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 086600c2-c5d8-47ec-a4c0-c782e1797486
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 4a6d07e9a24293f054915b5598c63e118c9c1430
ms.openlocfilehash: ff205efebf9b02ed0bfb1c7e275d34981870c26a


---

# Azure 資訊保護部署藍圖

>*適用於︰Azure 資訊保護、Office 365*

使用下列步驟為組織準備、實作及管理 Azure 資訊保護。

不過，如果您只想要快速自行試用 Azure 資訊保護，而不是在生產環境中導入它，請參閱 [快速入門教學課程](../get-started/infoprotect-quick-start-tutorial.md)。

> [!IMPORTANT]
> 執行下列步驟之前，請確定您已經檢閱 [Azure 資訊保護的需求](../get-started/requirements-azure-rms.md)。

選擇適合您的組織且符合所需[訂用帳戶功能與特色](https://www.microsoft.com/en-us/cloud-platform/azure-information-protection-features)的部署藍圖：

- [使用分類、標記和保護](#deployment-roadmap-for-classification-labeling-and-protection)

- [只使用資料保護](#deployment-roadmap-for-data-protection-only)


## 分類、標記和保護的部署藍圖

> [!NOTE]
> 已經在使用 Azure Rights Management Service 保護資料嗎？ 您可以跳過許多步驟，並專注於步驟 3 和 5.1。

### 步驟 1︰確認您的訂用帳戶並指派使用者授權
檢閱 Azure 資訊保護網站的[訂用帳戶資訊](https://www.microsoft.com/en-us/cloud-platform/azure-information-protection-pricing)和[功能清單](https://www.microsoft.com/en-us/cloud-platform/azure-information-protection-features)，確認組織具有的訂用帳戶包含預期的功能和特色。 然後，從此訂用帳戶將授權指派給您組織中想要分類、標記及保護文件和電子郵件的每位使用者。

### 步驟 2︰準備要使用 Azure 資訊保護的租用戶帳戶
在您開始使用 Azure 資訊保護之前，請完成下列準備工作：

- 確定您有 Office 365 或 Azure Active Directory 的使用者帳戶和群組，而且 Azure 資訊保護將使用這些帳戶和群組來驗證您組織中的使用者。 如有需要，請建立這些帳戶和群組，或從內部部署目錄同步處理它們。 如需詳細資訊，請參閱[準備 Azure 資訊保護](prepare.md)。

### 步驟 3︰設定及部署分類和標記

如果您還沒有分類策略，請檢閱[預設 Azure 資訊保護原則](../deploy-use/configure-policy-default.md)，並以此作為基準來決定要指派給組織資料的分類標籤。 您可以自訂這些標籤以符合業務需求。 

重新設定預設 Azure 資訊保護標籤，以進行為支援分類決策所需的任何變更。 設定使用者手動標記的原則，並撰寫說明要套用的標籤及何時套用的指引。 如需如何設定 Azure 資訊保護原則的詳細資訊，請參閱[設定 Azure 資訊保護原則](../deploy-use/configure-policy.md)。

然後為使用者部署 Azure 資訊保護用戶端，並藉由提供使用者訓練及何時選取標籤的指示予以支援。 如需安裝用戶端的詳細資訊，請參閱[安裝 Azure 資訊保護用戶端](../rms-client/info-protect-client.md)。

在一段時間之後，當使用者熟悉如何標記其文件和電子郵件時，請引進更進階的組態。 這些組態可能包含下列各項：

- 套用預設標籤

- 如果使用者選擇較低分類層級的標籤，則提示使用者輸入理由

- 規定所有文件和電子郵件使用一個標籤

- 自訂的頁首、頁尾或浮水印

- 支援建議和自動標記的條件

在此階段，請勿選取保護文件和電子郵件的選項。

### 步驟 4︰準備 Rights Management 資料保護

當使用者熟悉如何標記文件和電子郵件時，您就準備好開始對最敏感的資料引進資料保護。 此階段需要針對 Azure Rights Management Service 執行下列準備工作：

1. 決定是否要讓 Microsoft 管理您的租用戶金鑰 (預設)，或自行產生並管理租用戶金鑰 (稱為自帶金鑰或 BYOK)。 請注意，目前如果您使用 Exchange Online，則無法使用 BYOK。 如需詳細資訊，請參閱[規劃及實作 Azure 資訊保護租用戶金鑰](plan-implement-tenant-key.md)。

2. 在至少一部具有網際網路存取的電腦上安裝適用於 [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)] 的 Windows PowerShell 模組。 您可以現在執行這個步驟，或稍後再執行。 如需詳細資訊，請參閱[針對 Azure Rights Management Service 安裝 Windows PowerShell](../deploy-use/install-powershell.md)。

3. 如果您目前正在使用內部部署 Rights Management 服務：執行移轉以將金鑰、範本和 URL 移至雲端。 如需詳細資訊，請參閱[從 AD RMS 移轉至 Information Protection](migrate-from-ad-rms-to-azure-rms.md)。

4. 啟用 Azure Rights Management Service，以便您可以開始保護文件和電子郵件。 如果需要分階段部署，請設定使用者登入控制項以限制特定使用者的使用。 如需詳細資訊，請參閱[啟用 Azure Rights Management](../deploy-use/activate-service.md)。

您也可以選擇考慮設定下列各項：

-   如果預設的權限原則範本無法滿足貴組織的使用目的，您可以設定自訂範本。 您可以現在執行這個步驟，或稍後再執行。 如需詳細資訊，請參閱[設定 Azure Rights Management Service 的自訂範本](../deploy-use/configure-custom-templates.md)。

-   設定使用狀況記錄功能，以便讓您能夠監視貴組織如何使用 Rights Management。 您可以現在執行這個步驟，或稍後再執行。 如需詳細資訊，請參閱[記錄和分析 Azure Rights Management Service 的使用方式](../deploy-use/log-analyze-usage.md)。

### 步驟 5︰設定您的 Azure 資訊保護原則、應用程式和服務，以提供 Rights Management 資料保護

1. 更新您的 Azure 資訊保護原則以套用資料保護
    
    修改您的 Azure 資訊保護原則，讓一或多個標籤套用 Rights Management 保護。 如需詳細資訊，請參閱[如何設定標籤以套用 Rights Management 保護](../deploy-use/configure-policy-protection.md)。

2. 部署 Rights Management 共用應用程式
    
    為使用者安裝 Rights Management 共用應用程式，讓他們可以安全地透過電子郵件共用文件、就地保護檔案，並追蹤他們所保護的共用文件。 提供此應用程式的使用者訓練。 如需詳細資訊，請參閱[適用於 Windows 的 Rights Management 共用應用程式](../rms-client/sharing-app-windows.md)。

3. 設定 Office 應用程式和服務以使用 IRM
    
    設定 Office 應用程式和服務以使用 SharePoint Online 或 Exchange Online 中的資訊版權管理 (IRM) 功能。 如需詳細資訊，請參閱[設定 Azure Rights Management 的應用程式](../deploy-use/configure-applications.md)。

4. 設定進階使用者功能來執行資料復原
    
    如果您的現有 IT 服務需要檢查 Azure Rights Management 將保護的檔案 (例如資料外洩防護 (DLP) 解決方案、內容加密閘道 (CEG) 和反惡意程式碼產品)，請將服務帳戶設定為 Azure Rights Management 的進階使用者。 如需詳細資訊，請參閱[設定 Azure Rights Management 和探索服務或資料復原的進階使用者](../deploy-use/configure-super-users.md)。

5. 大量保護檔案 
    
    若要能夠大量保護或大量取消保護所有檔案類型，請安裝可使用 RMS 保護 PowerShell 模組的 RMS 保護工具。 如需詳細資訊，請參閱 [RMS 保護 Cmdlet](https://msdn.microsoft.com/library/mt433195.aspx)。

6. 部署在內部部署伺服器的連接器
    
    如果您有要與 Azure Rights Management Service 搭配使用的內部部署服務，請安裝並設定 Rights Management 連接器。 如需詳細資訊，請參閱[部署 Azure Rights Management 連接器](../deploy-use/deploy-rms-connector.md)。

### 步驟 4︰使用及監視您的資料保護解決方案
您現在準備好保護您的資料，並記錄貴公司如何使用 Rights Management。 如需支援此部署階段的其他資訊，請參閱[協助使用者使用 Azure Rights Management Service 來保護檔案](../deploy-use/help-users.md)和[記錄和分析 Azure Rights Management Service 的使用方式](../deploy-use/log-analyze-usage.md)。

如果您想要在 Windows 檔案伺服器上使用檔案分類基礎結構來自動保護檔案，請參閱[具有 Windows Server 檔案分類基礎結構 (FCI) 的 RMS 保護](../rms-client/configure-fci.md)。

### 步驟 5：視需要管理您租用戶帳戶的 Rights Management Service
開始使用 Azure Rights Management Service 時，您可能會發現適用於 Windows PowerShell 相當實用，可協助執行系統管理變更的指令碼處理或自動化。 如需詳細資訊，請參閱[使用 Windows PowerShell 管理 Azure Rights Management Service](../deploy-use/administer-powershell.md)。


## 僅限資料保護的部署藍圖

### 步驟 1：確認您有包含 Azure Rights Management 的訂用帳戶
檢閱 Azure 資訊保護網站的[訂用帳戶資訊](https://www.microsoft.com/en-us/cloud-platform/azure-information-protection-pricing)和[功能清單](https://www.microsoft.com/en-us/cloud-platform/azure-information-protection-features)，確認組織具有的訂用帳戶包含預期的功能和特色。 然後，從此訂用帳戶將授權指派給您組織中想要使用 Azure Rights Management Service 來保護文件和電子郵件的每位使用者。

### 步驟 2：準備您的租用戶帳戶以使用 Azure Rights Management Service
開始使用 [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)] 之前，請進行下列準備：

1.  確定您的 Office 365 租用戶包含 Azure 資訊保護將用來驗證您組織中使用者的使用者帳戶和群組。 如有需要，請建立這些帳戶和群組，或從內部部署目錄同步處理它們。 如需詳細資訊，請參閱[準備 Azure Rights Management](prepare.md)。

2. 決定是否要讓 Microsoft 管理您的租用戶金鑰 (預設)，或自行產生並管理租用戶金鑰 (稱為自帶金鑰或 BYOK)。 請注意，目前如果您使用 Exchange Online，則無法使用 BYOK。 如需詳細資訊，請參閱[規劃及實作 Azure 資訊保護租用戶金鑰](plan-implement-tenant-key.md)。

3. 在至少一部具有網際網路存取的電腦上安裝適用於 [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)] 的 Windows PowerShell 模組。 您可以現在執行這個步驟，或稍後再執行。 如需詳細資訊，請參閱[針對 Azure Rights Management 安裝 Windows PowerShell](../deploy-use/install-powershell.md)。

4. 如果您目前正在使用內部部署 Rights Management 服務：執行移轉以將金鑰、範本和 URL 移至雲端。 如需詳細資訊，請參閱[從 AD RMS 移轉至 Azure 資訊保護](migrate-from-ad-rms-to-azure-rms.md)。

5. 啟用 Rights Management 以便開始使用服務。 如果需要分階段部署，請設定使用者登入控制項以限制特定使用者的使用。 如需詳細資訊，請參閱[啟用 Azure Rights Management](../deploy-use/activate-service.md)。

您也可以選擇考慮設定下列各項：

-   如果預設的權限原則範本無法滿足貴組織的使用目的，您可以設定自訂範本。 您可以現在執行這個步驟，或稍後再執行。 如需詳細資訊，請參閱[設定 Azure Rights Management Service 的自訂範本](../deploy-use/configure-custom-templates.md)。

-   設定使用狀況記錄功能，以便讓您能夠監視貴組織如何使用 Rights Management。 您可以現在執行這個步驟，或稍後再執行。 如需詳細資訊，請參閱[記錄和分析 Azure Rights Management Service 的使用方式](../deploy-use/log-analyze-usage.md)。

### 步驟 3：設定您的應用程式和服務以使用 Rights Management

1. 部署 Rights Management 共用應用程式
    
    為使用者安裝 Rights Management 共用應用程式，讓他們可以安全地透過電子郵件共用文件、就地保護檔案，並追蹤他們所保護的共用文件。 提供此應用程式的使用者訓練。 如需詳細資訊，請參閱[適用於 Windows 的 Rights Management 共用應用程式](../rms-client/sharing-app-windows.md)。

2. 設定 Office 應用程式和服務以使用 IRM
    
    設定 Office 應用程式和服務以使用 SharePoint Online 或 Exchange Online 中的資訊版權管理 (IRM) 功能。 如需詳細資訊，請參閱[設定 Azure Rights Management 的應用程式](../deploy-use/configure-applications.md)。

3. 設定進階使用者功能來執行資料復原
    
    如果您的現有 IT 服務需要檢查 Azure Rights Management 將保護的檔案 (例如資料外洩防護 (DLP) 解決方案、內容加密閘道 (CEG) 和反惡意程式碼產品)，請將服務帳戶設定為 Azure Rights Management 的進階使用者。 如需詳細資訊，請參閱[設定 Azure Rights Management 和探索服務或資料復原的進階使用者](../deploy-use/configure-super-users.md)。

4. 大量保護檔案 
    
    若要能夠大量保護或大量取消保護所有檔案類型，請安裝可使用 RMS 保護 PowerShell 模組的 RMS 保護工具。 如需詳細資訊，請參閱 [RMS 保護 Cmdlet](https://msdn.microsoft.com/library/mt433195.aspx)。

5. 部署在內部部署伺服器的連接器
    
    如果您有要與 Azure Rights Management Service 搭配使用的內部部署服務，請安裝並設定 Rights Management 連接器。 如需詳細資訊，請參閱[部署 Azure Rights Management 連接器](../deploy-use/deploy-rms-connector.md)。


### 步驟 4︰使用及監視您的資料保護解決方案
您現在準備好保護您的資料，並記錄貴公司如何使用 Rights Management。 如需支援此部署階段的其他資訊，請參閱[協助使用者使用 Azure Rights Management Service 來保護檔案](../deploy-use/help-users.md)和[記錄和分析 Azure Rights Management Service 的使用方式](../deploy-use/log-analyze-usage.md)。

如果您想要在 Windows 檔案伺服器上使用檔案分類基礎結構來自動保護檔案，請參閱[具有 Windows Server 檔案分類基礎結構 (FCI) 的 RMS 保護](../rms-client/configure-fci.md)。

### 步驟 5：視需要管理您租用戶帳戶的 Rights Management Service
開始使用 Azure Rights Management Service 時，您可能會發現適用於 Windows PowerShell 相當實用，可協助執行系統管理變更的指令碼處理或自動化。 如需詳細資訊，請參閱[使用 Windows PowerShell 管理 Azure Rights Management Service](../deploy-use/administer-powershell.md)。





<!--HONumber=Oct16_HO1-->


