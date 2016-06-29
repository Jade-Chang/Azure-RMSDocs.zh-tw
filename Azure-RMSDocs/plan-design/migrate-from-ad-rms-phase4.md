---
# required metadata

title: 從 AD RMS 移轉至 Azure Rights Management - 階段 4 | Azure RMS
description:
keywords:
author: cabailey
manager: mbaldwin
ms.date: 06/14/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: d51e7bdd-2e5c-4304-98cc-cf2e7858557d


# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: esaggese
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# 移轉階段 4︰移轉後工作

*適用於︰Active Directory Rights Management Services、Azure Rights Management*


針對從 AD RMS 移轉至 Azure Rights Management (Azure RMS) 的階段 4 使用下列資訊。 這些程序涵蓋[從 AD RMS 移轉至 Azure Rights Management](migrate-from-ad-rms-to-azure-rms.md) 的步驟 8 到 9。


## 步驟 8： 解除委任 AD RMS

選擇性：移除 Active Directory 中的服務連線點 (SCP)，以避免電腦探索內部部署 Rights Management 基礎結構。 這是選擇性的做法，取決於您在登錄中設定的重新導向 (如藉由執行移轉指令碼)。 若要移除服務連線點，請使用 [Rights Management Services 管理工具組](http://www.microsoft.com/download/details.aspx?id=1479)中的 AD SCP 註冊工具。

監視 AD RMS 伺服器中的活動，例如，檢查[系統健康情況報告中的要求](https://technet.microsoft.com/library/ee221012%28v=ws.10%29.aspx)、[ServiceRequest 資料表](http://technet.microsoft.com/library/dd772686%28v=ws.10%29.aspx)或[使用者存取受保護內容的稽核](http://social.technet.microsoft.com/wiki/contents/articles/3440.ad-rms-frequently-asked-questions-faq.aspx)。 確認 RMS 用戶端不再與這些伺服器進行通訊而且用戶端順利使用 Azure RMS 時，您可以從這些伺服器中移除 AD RMS 伺服器角色。 如果您使用專用伺服器，則可能會想要進行警告性步驟，即先關閉伺服器一段時間，確定未報告任何可能需要重新啟動這些伺服器的問題，以確保在您調查用戶端未使用 Azure RMS 的原因時服務不中斷。

解除委任 AD RMS 伺服器之後，您可能會想要利用這個機會在 Azure 傳統入口網站中檢閱範本並將其合併，讓使用者擁有較少的選擇，或重新設定它們，甚至加入新的範本。 這可能也是發佈預設範本的好時機。 如需詳細資訊，請參閱[設定 Azure Rights Management 的自訂範本](../deploy-use/configure-custom-templates.md)。

## 步驟 9： 重新設定 Azure RMS 租用戶金鑰
因為重新設定金鑰會建立使用「RMS 加密模式 2」的新租用戶金鑰，所以如果 AD RMS 部署使用「RMS 加密模式 1」，則完成移轉時需要這個步驟。 只有在移轉程序期間才支援搭配使用 Azure RMS 與加密模式 1。

這是選擇性步驟，但在完成移轉時建議使用，即使您執行 RMS 加密模式 2 也是一樣，因為它可以協助保護 Azure RMS 租用戶金鑰，使其沒有 AD RMS 金鑰的潛在安全性漏洞。 重新設定 Azure RMS 租用戶金鑰 (也稱為「輪換金鑰」) 時，會建立新的金鑰，並封存原始金鑰。 不過，因為並不會立即從某個金鑰移至另一個金鑰，而是需要幾週的時間，所以請在完成移轉之後立即重新設定 Azure RMS 租用戶金鑰，不要等到懷疑原始金鑰有漏洞才進行。

重新設定 Azure RMS 租用戶金鑰：

-   如果您的 Azure RMS 租用戶金鑰由 Microsoft 管理︰若要這樣做，請[連絡 Microsoft 支援服務](../get-started/information-support#to-contact-microsoft-support)以**使用重設您 Azure RMS 租用戶金鑰的要求開啟 Azure Rights Management 支援案例**。 您必須證明您是 Azure RMS 租用戶的管理員，且應了解此程序將需要數天的時間。 標準支援費用適用；重設租用戶金鑰並非免費的支援服務。

-   如果您的 Azure RMS 租用戶金鑰是由您所管理 (BYOK)：重複 BYOK 程序，以透過網際網路或親自產生及建立新的金鑰。

如需管理 Azure RMS 租用戶金鑰的詳細資訊，請參閱 [Azure Rights Management 租用戶金鑰的作業](../deploy-use/operations-tenant-key.md)。

## 後續步驟

完成移轉之後，請檢閱[部署藍圖](deployment-roadmap.md)來識別您可能必須執行的任何其他部署工作。



<!--HONumber=Jun16_HO2-->


