---
title: "從 AD RMS 移轉至 Azure Information Protection - 第 4 階段 | Azure Information Protection"
description: "從 AD RMS 移轉至 Azure Information Protection 的第 4 階段，涵蓋從 AD RMS 移轉至 Azure Information Protection 的步驟 8 至 9。"
author: cabailey
manager: mbaldwin
ms.date: 10/05/2016
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: d51e7bdd-2e5c-4304-98cc-cf2e7858557d
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: f17cf257607b0f74ca8bdaef13130da2f62dd587
ms.openlocfilehash: f86e712ee9d2df1e466ceaabcaa0890dca71da53


---

# 移轉階段 4︰移轉後工作

>*適用於︰Active Directory Rights Management Services、Azure Information Protection、Office 365*


針對從 AD RMS 移轉至 Azure Information Protection 的第 4 階段使用下列資訊。 這些程序涵蓋[從 AD RMS 移轉至 Azure Information Protection](migrate-from-ad-rms-to-azure-rms.md) 的步驟 8 到 9。


## 步驟 8： 解除委任 AD RMS

選擇性：移除 Active Directory 中的服務連線點 (SCP)，以避免電腦探索內部部署 Rights Management 基礎結構。 這是選擇性的做法，取決於您在登錄中設定的重新導向 (如藉由執行移轉指令碼)。 若要移除服務連線點，請使用 [Rights Management Services 管理工具組](http://www.microsoft.com/download/details.aspx?id=1479)中的 AD SCP 註冊工具。

監視 AD RMS 伺服器中的活動，例如，檢查[系統健康情況報告中的要求](https://technet.microsoft.com/library/ee221012%28v=ws.10%29.aspx)、[ServiceRequest 資料表](http://technet.microsoft.com/library/dd772686%28v=ws.10%29.aspx)或[使用者存取受保護內容的稽核](http://social.technet.microsoft.com/wiki/contents/articles/3440.ad-rms-frequently-asked-questions-faq.aspx)。 確認 RMS 用戶端不再與這些伺服器進行通訊而且用戶端順利使用 Azure Information Protection 時，您可以從這些伺服器中移除 AD RMS 伺服器角色。 如果您使用專用伺服器，則可能會想要進行警告性步驟，即先關閉伺服器一段時間，確定未報告任何可能需要重新啟動這些伺服器的問題，以確保在您調查用戶端未使用 Azure Information Protection 的原因時服務不中斷。

解除委任 AD RMS 伺服器之後，您可能會想要利用這個機會在 Azure 傳統入口網站中檢閱範本並將其合併，讓使用者擁有較少的選擇，或重新設定它們，甚至加入新的範本。 這可能也是發佈預設範本的好時機。 如需詳細資訊，請參閱[設定 Azure Rights Management Service 的自訂範本](../deploy-use/configure-custom-templates.md)。

## 步驟 9： 重設 Azure Information Protection 租用戶金鑰
此步驟僅適用於您所選的租用戶金鑰拓撲是由 Microsoft 管理，而非由客戶管理 (BYOK 搭配 Azure 金鑰保存庫) 的情形。

此步驟雖為選用，但若您的 Azure Information Protection 租用戶金鑰是由 Microsoft 管理且已自 AD RMS 移轉，則建議使用。 此案例中的重設金鑰可協助保護您的 Azure Information Protection 租用戶金鑰，免於您 AD RMS 金鑰的潛在安全性缺口。

重設 Azure Information Protection 租用戶金鑰 (也稱為「輪換金鑰」) 時，會建立新的金鑰，並封存原始金鑰。 不過，因為並不會立即從某個金鑰移至另一個金鑰，而是需要幾週的時間，所以請在完成移轉之後立即重新設定 Azure Information Protection 租用戶金鑰，不要等到懷疑原始金鑰有漏洞才進行。

若要重設 Microsoft 管理的 Azure Information Protection 租用戶金鑰，請[連絡 Microsoft 支援服務](../get-started/information-support.md#to-contact-microsoft-support)，並開啟 **Azure Information Protection 支援案例，並要求自 AD RMS 移轉後重設您的 Azure Information Protection 金鑰**。 您必須證明您是 Azure Information Protection 租用戶的管理員，且應了解此程序將需要數天的時間。 標準支援費用適用；重設租用戶金鑰並非免費的支援服務。


## 後續步驟

如需管理 Azure Information Protection 租用戶金鑰的詳細資訊，請參閱 [Azure Rights Management 租用戶金鑰的作業](../deploy-use/operations-tenant-key.md)。

完成移轉之後，請檢閱[部署藍圖](deployment-roadmap.md)來識別您可能必須執行的任何其他部署工作。




<!--HONumber=Oct16_HO1-->


