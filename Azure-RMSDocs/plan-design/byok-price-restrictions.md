---
title: "BYOK 定價和限制 | Azure 資訊保護"
description: Understand the restrictions when you use customer-managed keys (known as "bring your own key", or BYOK) with Azure RMS.
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 11/04/2016
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: f5930ed3-a6cf-4eac-b2ec-fcf63aa4e809
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: f1fff17f76361f8236974c6aeb21ed317c7d9883
ms.openlocfilehash: e64e87298358b5d1064cda491a10abb48545a98e


---

# <a name="byok-pricing-and-restrictions"></a>BYOK 定價和限制

>*適用對象︰Azure 資訊保護、Office 365*


若組織的訂用帳戶包含 Azure 資訊保護功能，即可將 Azure 資訊保護租用戶設為使用客戶管理的金鑰 (BYOK)，並免費[記錄其使用情況](../deploy-use/log-analyze-usage.md)。 

金鑰必須儲存在 Azure 金鑰保存庫內，其需要付費 (或試用版) 的 Azure 訂用帳戶，且您必須使用 Azure 金鑰保存庫進階服務層以支援受 HSM 保護的金鑰。 在 Azure 金鑰保存庫中使用受 HSM 保護的金鑰會產生每月費用。 如需詳細資訊，請參閱 [Azure 金鑰保存庫定價頁面](https://azure.microsoft.com/en-us/pricing/details/key-vault/)。

若要針對 Azure 資訊保護租用戶金鑰使用 Azure 金鑰保存庫，建議您為這個金鑰選擇專屬訂用帳戶與專屬金鑰保存庫，以確保它僅供 Azure Rights Management Service 使用。 

## <a name="benefits-of-using-azure-key-vault"></a>使用 Azure 金鑰保存庫的優點

除了使用 Azure 資訊保護使用量記錄之外，您還可以搭配 [Azure 金鑰保存庫記錄](https://azure.microsoft.com/documentation/articles/key-vault-logging/)進行交互參照，以獨立監視並進一步確認是否只有 Azure Rights Management Service 使用這個金鑰。 如有必要，您可以立即移除金鑰保存庫的權限來撤銷金鑰的存取權。

針對 Azure 資訊保護租用戶金鑰使用 Azure 金鑰保存庫，還有下列其他優點：

- Azure 金鑰保存庫是一種集中式金鑰管理解決方案，可針對使用加密的各種雲端服務甚至內部部署服務，提供一致的管理解決方案。

- Azure 金鑰保存庫支援多種金鑰管理的內建介面，包括 PowerShell、CLI、REST API 和 Azure 入口網站。 此外，金鑰保存庫也整合了其他服務和工具，以提供針對特定工作最佳化的功能，例如監視。 比方說，您可以透過 Operations Management Suite 的 Log Analytics 來分析金鑰使用量記錄，並設定在符合指定準則時發出警示等等。

- Azure 金鑰保存庫提供角色隔離的環境，其為公認的安全性最佳做法。 Azure 資訊保護的系統管理員可以把重心放在管理資料分類和保護，而 Azure 金鑰保存庫的系統管理員則可專注於管理加密金鑰和為保障安全性或相容性可能需要的任何特殊原則。

- 某些組織有限制主要金鑰的存放位置。 Azure 金鑰保存庫可針對主要金鑰的儲存位置提供高層級的控制，因為許多 Azure 區域皆可使用這項服務。 目前，您可以從 28 個 Azure 區域中進行選擇，且區域數量將會持續增加。 如需詳細資訊，請參閱 Azure 網站上的 [依區域提供的產品] (https://azure.microsoft.com/regions/services/) 頁面。

除了管理金鑰之外，Azure 金鑰保存庫可讓安全性系統管理員擁有相同的管理體驗，來針對使用加密的其他服務及應用程式，儲存、存取和管理憑證與密碼。 

如需 Azure 金鑰保存庫的詳細資訊，請參閱[什麼是 Azure 金鑰保存庫？](https://azure.microsoft.com/documentation/articles/key-vault-whatis/)並瀏覽 [Azure 金鑰保存庫小組部落格](https://blogs.technet.microsoft.com/kv/)以取得最新資訊，並了解其他服務如何使用這項技術。


## <a name="restrictions-when-using-byok"></a>使用 BYOK 的限制

若您的使用者已透過個人版 RMS 註冊免費帳戶，您便無法使用 BYOK 或使用量記錄，因為此設定並沒有租用戶系統管理員，無法設定這些功能。


> [!NOTE]
> 如需個人適用的 RMS 的詳細資訊，請參閱[個人版 RMS 和 Azure Rights Management](../understand-explore/rms-for-individuals.md)。

![BYOK 不支援 Exchange Online](../media/RMS_BYOK_noExchange.png)

BYOK 和使用記錄與整合 Azure 資訊保護所使用之 Azure Rights Management Service (Azure RMS) 的每個應用程式皆能完美合作。 這包括 SharePoint Online 之類的雲端服務、使用 RMS 連接器來執行使用 Azure RMS 的 Exchange 和 SharePoint 的內部部署伺服器，以及 Office 2016 及 Office 2013 等用戶端應用程式。 無論哪個應用程式要求 Azure RMS，您都會得到金鑰使用記錄。

但有一個例外：目前， **Azure RMS BYOK 與 Exchange Online 不相容**。 如果您想要使用 Exchange Online，我們建議您立即在預設金鑰管理模式中設定 Azure RMS，Microsoft 會在此種模式下產生並管理您的金鑰。 稍後當 Exchange Online 真的支援 Azure RMS BYOK 時，您就可以選擇移至 BYOK。 不過，如果您無法等待，另一個選項為立即部署 Azure RMS 與 BYOK 搭配，如此 Exchange online 將具有精簡的 RMS 功能 (未受保護的電子郵件及未受保護的附件仍然可以完全運作)。

-   無法顯示 Outlook Web Access 中受保護的電子郵件或受保護的附件。

-   無法顯示行動裝置上使用 Exchange ActiveSync IRM 的受保護電子郵件。

-   傳輸解密 (例如掃描惡意程式碼) 和日誌解密不可行，因此將略過受保護的電子郵件和受保護的附件。

-   強制執行 IRM 原則的傳輸保護規則和資料外洩防護 (DLP) 不可行，因此無法使用這些方法套用 RMS 保護。

-   以伺服器為基礎搜尋受保護的電子郵件，因此將略過受保護的電子郵件。

當您使用 Azure RMS BYOK 與 Exchange online 的精簡 RMS 功能搭配時，RMS 將在 Windows 和 Mac 上使用 Outlook 中的電子郵件用戶端，以及其他未使用 Exchange ActiveSync IRM 的電子郵件用戶端。

如果您是從 AD RMS 移轉至 Azure RMS，您可能已將金鑰作為信任發行網域 (TPD) 匯入 Exchange Online (在 Exchange 術語中也稱為 BYOK，其與 Azure 金鑰保存庫 BYOK 分開)。 在此案例中，您必須從 Exchange Online 中移除 TPD，才能避免衝突的範本和原則。 如需詳細資訊，請參閱 Exchange Online Cmdlet 文件庫中的 [Remove-RMSTrustedPublishingDomain](https://technet.microsoft.com/library/jj200720%28v=exchg.150%29.aspx)。

有時候，Exchange Online 的 Azure RMS BYOK 實際上不是問題。 例如，需要 BYOK 和記錄的組織會在內部部署上執行其資料應用程式 (Exchange、SharePoint、Office)，並對無法使用內部部署 AD RMS 輕易取得的功能使用 Azure RMS (例如，與其他公司協同作業及從行動用戶端存取)。 BYOK 和記錄在此情況中皆運作正常，且可讓組織完全控制其 Azure RMS 訂閱。

## <a name="next-steps"></a>後續步驟

如果您已擬定決策來管理您自己的金鑰，請移至[實作 Azure Rights Management 租用戶金鑰](plan-implement-tenant-key.md#implementing-your-azure-information-protection-tenant-key)。

如果您決定要繼續使用 Microsoft 用來管理您的租用戶金鑰的預設組態，請參閱＜規劃及實作 Azure Rights Management 租用戶金鑰＞文章的[後續步驟](plan-implement-tenant-key.md#next-steps)一節。




<!--HONumber=Nov16_HO1-->


