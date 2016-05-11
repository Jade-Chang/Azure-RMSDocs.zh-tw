---
# required metadata

title: Azure Rights Management 部署藍圖 | Azure RMS
description:
keywords:
author: cabailey
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 086600c2-c5d8-47ec-a4c0-c782e1797486

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: esaggese
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Azure Rights Management 部署藍圖
使用下列步驟來為貴組織準備、實作及管理 Azure Rights Management (Azure RMS)。

不過，如果您只想要快速自行嘗試 Azure RMS，而不是在生產環境中導入它，請參閱 [Azure Rights Management 的快速入門教學課程](../get-started/quick-start-tutorial.md)。

> [!IMPORTANT]
> 執行下列步驟之前，請確定您已經檢閱 [Azure Rights Management 的需求](../get-started/requirements-azure-rms.md)。

## 步驟 1：確認您有包含 Azure Rights Management 的訂用帳戶
沒有多種類型的訂用帳戶包含 [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)]。 請參閱[支援 Azure RMS 的雲端訂閱](../get-started/requirements-subscriptions.md)，並檢查您的訂閱是否包含您要在貴組織中使用的功能，方法為參考[比較 Rights Management Services (RMS) 供應項目](https://technet.microsoft.com/dn858608)中的資料表。 您必須從這個訂閱中將授權指派給組織的每位使用者，這些使用者將使用 Azure RMS 來保護檔案和電子郵件。

## 步驟 2：準備您的租用戶帳戶以使用 Rights Management
開始使用 [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)] 之前，請進行下列準備：

1.  請確定您的 Azure 或 Office 365 租用戶所包含的使用者帳戶和群組，將被 Azure rms 用來驗證貴組織中的使用者。 如有需要，請建立這些帳戶和群組，或從內部部署目錄同步處理它們。 如需詳細資訊，請參閱[準備 Azure Rights Management](prepare.md)。

2.  決定是否要讓 Microsoft 管理您的租用戶金鑰 (預設)，或自行產生並管理租用戶金鑰 (稱為自帶金鑰或 BYOK)。 請注意，目前如果您使用 Exchange Online，則無法使用 BYOK。 如需詳細資訊，請參閱[規劃及實作 Azure Rights Management 租用戶金鑰](plan-implement-tenant-key.md)。

3.  在至少一部具有網際網路存取的電腦上安裝適用於 [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)] 的 Windows PowerShell 模組。 您可以現在執行這個步驟，或稍後再執行。 如需詳細資訊，請參閱[針對 Azure Rights Management 安裝 Windows PowerShell](../deploy-use/install-powershell.md)。

4.  如果您目前正在使用內部部署 Rights Management 服務：執行移轉以將金鑰、範本和 URL 移至雲端。 如需詳細資訊，請參閱[從 AD RMS 移轉至 Azure Rights Management](migrate-from-ad-rms-to-azure-rms.md)。

5.  啟用 Rights Management 以便開始使用服務。 如果需要分階段部署，請設定使用者登入控制項以限制特定使用者的使用。 如需詳細資訊，請參閱[啟用 Azure Rights Management](../deploy-use/activate-service.md)。

您也可以選擇考慮設定下列各項：

-   如果預設的權限原則範本無法滿足貴組織的使用目的，您可以設定自訂範本。 您可以現在執行這個步驟，或稍後再執行。 如需詳細資訊，請參閱[設定 Azure Rights Management 的自訂範本](../deploy-use/configure-custom-templates.md)。

-   設定使用狀況記錄功能，以便讓您能夠監視貴組織如何使用 Rights Management。 您可以現在執行這個步驟，或稍後再執行。 如需詳細資訊，請參閱[記錄和分析 Azure Rights Management 使用情況](../deploy-use/log-analyze-usage.md)。

## 步驟 3：設定您的應用程式和服務以使用 Rights Management
設定您的應用程式和服務可包含安裝 Rights Management 共用應用程式，以及啟用 SharePoint Online 或 Exchange Online 中的資訊版權管理 (IRM) 功能支援。 如需詳細資訊，請參閱[設定 Azure Rights Management 的應用程式](../deploy-use/configure-applications.md)。

如果您的現有 IT 服務需要檢查 Azure RMS 將保護的檔案 (例如預防資料遺漏 (DLP) 方案、內容加密閘道 (CEG) 和反惡意程式碼產品)，請將服務帳戶設定為 Azure RMS 的進階使用者。 如需詳細資訊，請參閱[設定 Azure Rights Management 和探索服務或資料復原的進階使用者](../deploy-use/configure-super-users.md)。

如果您有要與 Azure Rights Management 搭配使用的內部部署服務，請安裝並設定 Rights Management 連接器。 如需詳細資訊，請參閱[部署 Azure Rights Management 連接器](../deploy-use/deploy-rms-connector.md)。

## 步驟 4：發佈及使用受版權保護的內容
您現在準備好發佈和取用受保護的內容，並記錄貴公司如何使用 Rights Management。 如需詳細資訊，請參閱[協助使用者使用 Azure Rights Management 來保護檔案](../deploy-use/help-users.md)和[記錄和分析 Azure Rights Management 使用情況](../deploy-use/log-analyze-usage.md)。

## 步驟 5：視需要管理您租用戶帳戶的 Rights Management
開始使用 [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)] 時，您可能會發現適用於 Windows PowerShell 的 [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)] 模組相當實用，可協助執行系統管理變更的指令碼處理或自動化。 如需詳細資訊，請參閱[使用 Windows PowerShell 管理 Azure Rights Management](../deploy-use/administer-powershell.md)。




<!--HONumber=Apr16_HO3-->


