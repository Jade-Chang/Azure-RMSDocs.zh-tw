---
# required metadata

title: 客戶管理 - 租用戶金鑰生命週期作業 |Azure RMS
description:
keywords:
author: cabailey
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: c5b19c59-812d-420c-9c54-d9776309636c

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: esaggese
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---


# 客戶管理：租用戶金鑰生命週期作業
如果您自行管理 Azure Rights Management 的租用戶金鑰 (整合您自己的金鑰案例，簡稱為 BYOK)，請參閱下列各節，以了解與此拓撲有關的生命週期作業的詳細資訊。

## 撤銷租用戶金鑰
當您取消訂閱 Azure RMS 時，Azure RMS 會停止使用您的租用戶金鑰，您不必採取任何動作。

## 更換租用戶金鑰
更換金鑰又稱為輪換金鑰。 除非真有必要，請不要更換租用戶金鑰。 舊版的用戶端 (例如 Office 2010) 無法正確處理金鑰變更。 在此情況下，您必須使用群組原則或同等的機制來清除電腦上的 RMS 狀態。 不過，有些法律事件可能迫使您不得不更換租用戶金鑰。 例如：

-   您的公司分拆成兩家以上的公司。 當您更換租用戶金鑰時，新公司將無法存取您的員工所發佈的新內容。 只要他們有一份舊的租用戶金鑰，就可以存取舊的內容。

-   您認為租用戶金鑰的正本 (您擁有的副本) 被盜。

當您更換租用戶金鑰時，新的內容會以新的租用戶金鑰來保護。 這是分階段逐步進行，所以在一段期間內，有些新的內容會持續以舊的租用戶金鑰來保護。 先前保護的內容仍然是以舊的租用戶金鑰來保護。 為了支援此案例，Azure RMS 會保留舊的租用戶金鑰，所以可以為舊的內容發出授權。

若要更換租用戶金鑰，請使用[規劃及實作 Azure Rights Management 租用戶金鑰](..\plan-design\plan-implement-tenant-key.md)主題的[實作整合您自己的金鑰 (BYOK)](..\plan-design\plan-implement-tenant-key.md#implementing-your-azure-rights-management-tenant-key) 一節中的程序，以透過網際網路或親自產生與建立新的金鑰。

## 備份和復原租用戶金鑰
您負責備份租用戶金鑰。 如果是在 Thales HSM 中產生租用戶金鑰，若要備份金鑰，只需要備份信號化金鑰檔案、園地檔案及系統管理員卡。

如果您藉由遵循[規劃及實作 Azure Rights Management 租用戶金鑰](../plan-design/plan-implement-tenant-key.md)一文的[實作整合您自己的金鑰 (BYOK)](../plan-design/plan-implement-tenant-key.md#implementing-your-azure-rights-management-tenant-key) 一節中的程序來傳輸金鑰，Azure RMS 會保留信號化金鑰檔案，以防止任何 Azure RMS 節點的失敗。 然而，這並不算是完整備份。 例如，若您還是可能需要在 Thales HSM 以外使用金鑰的純文字副本，則 Azure RMS 無法擷取它，因為它只有無法復原的副本。

## 匯出租用戶金鑰
如果您使用 BYOK，您無法從 Azure RMS 匯出租用戶金鑰。 Azure RMS 中是無法復原的副本。 如果您想要刪除這個金鑰不再使用，請連絡 Microsoft 客戶服務支援 (CSS)。

## 漏洞應變
安全性系統不論多麼堅固，不可能完美到沒有任何漏洞應變程序。 租用戶金鑰可能已外洩或遭竊。 即使受到嚴密保護，最新一代 HSM 技術或目前的金鑰長度和演算法仍可能有弱點。

Microsoft 有專屬團隊負責對產品與服務中的安全性事件做出應變。 每當有可靠的報告指出有事件發生，此團隊就會立即介入來調查範圍、根本原因及防護措施。 如果此事件影響到您的資產，Microsoft 會以您訂閱時所提供的地址，以電子郵件來通知您的 Azure RMS 租用戶管理員。

如果發生漏洞，您或 Microsoft 可採取的最佳行動取決於漏洞的範圍；Microsoft 會與您一起完成此過程。 下表顯示一些常見的情況和可能的反應，但確切的反應取決於調查期間揭露的所有資訊。

|事件描述|可能的反應|
|------------------------|-------------------|
|租用戶金鑰外洩。|更換租用戶金鑰。 請參閱[更換租用戶金鑰](#re-key-your-tenant-key)。|
|未獲授權的人或惡意程式碼可能取得權限來使用您的租用戶金鑰，但金鑰本身並未外洩。|更換租用戶金鑰在此無濟於事，必須分析根本原因。 如果是程序或軟體的錯誤導致未獲授權的人取得存取權，則必須解決這種情況。|
|最新一代 HSM 技術中發現的弱點。|Microsoft 必須更新 HSM。 如果確信弱點已暴露金鑰，則 Microsoft 會指示所有客戶更新其租用戶金鑰。|
|經由運算可找出 RSA 演算法、金鑰長度或暴力密碼破解攻擊的弱點。|Microsoft 必須更新 Azure RMS 來支援更強韌的新演算法和更長的金鑰長度，並指示所有客戶更新其租用戶金鑰。|




<!--HONumber=Apr16_HO3-->


