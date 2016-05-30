---
# required metadata

title: BYOK 定價和限制 | Azure RMS
description:
keywords:
author: cabailey
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: f5930ed3-a6cf-4eac-b2ec-fcf63aa4e809

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: esaggese
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# BYOK 定價和限制

*適用於︰Azure Rights Management、Office 365*


具 IT 管理之 Azure 訂閱的組織可免費使用 BYOK 並記錄其使用情況。 使用個人版 RMS 的組織無法使用 BYOK 和記錄，因為它們沒有租用戶系統管理員來設定這些功能。


> [!NOTE]
> 如需個人版 RMS 的詳細資訊，請參閱 [個人版 RMS 和 Azure Rights Management](../understand-explore/rms-for-individuals.md).

![BYOK 不支援 Exchange Online](../media/RMS_BYOK_noExchange.png)

BYOK 和記錄與整合 Azure RMS 的每個應用程式皆能完美合作。 這包括 SharePoint Online 之類的雲端服務、使用 RMS 連接器來執行使用 Azure RMS 的 Exchange 和 SharePoint 的內部部署伺服器，以及 Office 2013 等用戶端應用程式。 無論哪個應用程式要求 Azure RMS，您都會得到金鑰使用記錄。

但有一個例外：目前， **Azure RMS BYOK 與 Exchange Online 不相容**。  如果您想要使用 Exchange Online，我們建議您立即在預設金鑰管理模式中設定 Azure RMS，Microsoft 會在此種模式下產生並管理您的金鑰。 稍後當 Exchange Online 真的支援 Azure RMS BYOK 時，您就可以選擇移至 BYOK。 不過，如果您無法等待，另一個選項為立即部署 Azure RMS 與 BYOK 搭配，如此 Exchange online 將具有精簡的 RMS 功能 (未受保護的電子郵件及未受保護的附件仍然可以完全運作)。

-   無法顯示 Outlook Web Access 中受保護的電子郵件或受保護的附件。

-   無法顯示行動裝置上使用 Exchange ActiveSync IRM 的受保護電子郵件。

-   傳輸解密 (例如掃描惡意程式碼) 和日誌解密不可行，因此將略過受保護的電子郵件和受保護的附件。

-   強制執行 IRM 原則的傳輸保護規則和資料外洩防護 (DLP) 不可行，因此無法使用這些方法套用 RMS 保護。

-   以伺服器為基礎搜尋受保護的電子郵件，因此將略過受保護的電子郵件。

當您使用 Azure RMS BYOK 與 Exchange online 的精簡 RMS 功能搭配時，RMS 將在 Windows 和 Mac 上使用 Outlook 中的電子郵件用戶端，以及其他未使用 Exchange ActiveSync IRM 的電子郵件用戶端。

如果您是從 AD RMS 移轉至 Azure RMS，您可能已將做為信任的發佈網域 (TPD) 的金鑰匯入至 Exchange Online (在 Exchange 術語中也稱為 BYOK，其是從 Azure RMS BYOK 分開的)。 在此案例中，您必須從 Exchange Online 中移除 TPD，才能避免衝突的範本和原則。 如需詳細資訊，請參閱 Exchange Online Cmdlet 文件庫中的 [Remove-RMSTrustedPublishingDomain](https://technet.microsoft.com/library/jj200720%28v=exchg.150%29.aspx)。

有時候，Exchange Online 的 Azure RMS BYOK 實際上不是問題。 例如，需要 BYOK 和記錄的組織會在內部部署上執行其資料應用程式 (Exchange、SharePoint、Office)，並對無法使用內部部署 AD RMS 輕易取得的功能使用 Azure RMS (例如，與其他公司協同作業及從行動用戶端存取)。 BYOK 和記錄在此情況中皆運作正常，且可讓組織完全控制其 Azure RMS 訂閱。

## 後續步驟

如果您已擬定決策來管理您自己的金鑰，請移至 [實作 Azure Rights Management 租用戶金鑰](plan-implement-tenant-key.md#implementing-your-azure-rights-management-tenant-key).

如果您決定要繼續使用 Microsoft 用來管理您的租用戶金鑰的預設組態，請參閱＜規劃及實作 Azure Rights Management 租用戶金鑰＞文章的[後續步驟](plan-implement-tenant-key.md#next-steps)一節。



<!--HONumber=Apr16_HO4-->


