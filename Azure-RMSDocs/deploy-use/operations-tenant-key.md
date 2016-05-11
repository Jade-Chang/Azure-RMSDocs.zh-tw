---
# required metadata

title: Azure Rights Management 租用戶金鑰的作業 | Azure RMS
description:
keywords:
author: cabailey
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 1284d0ee-0a72-45ba-a64c-3dcb25846c3d

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: esaggese
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Azure Rights Management 租用戶金鑰的作業
根據租用戶金鑰拓撲而定 (由 Microsoft 管理或客戶管理)，您對實作之後的 Microsoft Azure Rights Management (Azure RMS) 租用戶金鑰會有不同程度的控制與責任。

當您管理自己的租用戶金鑰時，這通常稱為整合您自己的金鑰 (BYOK)。 如需此案例及如何在這兩種租用戶金鑰拓撲之中做選擇的詳細資訊，請參閱[規劃及實作 Azure Rights Management 租用戶金鑰](../plan-design/plan-implement-tenant-key.md)。

下表視您為 Azure RMS 租用戶金鑰選擇的拓撲而定，指出您可以執行的作業。

|生命週期作業|由 Microsoft 管理 (預設)|由客戶管理 (BYOK)|
|-----------------------|-------------------------------|---------------------------|
|撤銷租用戶金鑰|否 (自動)|否 (自動)|
|更換租用戶金鑰|是|是|
|備份和復原租用戶金鑰|否|是|
|匯出租用戶金鑰|是|否|
|漏洞應變|是|是|

識別您已實作的拓撲之後，請選取下列一項，以了解對 Azure RMS 租用戶金鑰執行這些作業的詳細資訊。


- [Microsoft 管理的租用戶金鑰](operations-microsoft-managed-tenant-key.md)
- [客戶管理的租用戶金鑰](operations-customer-managed-tenant-key.md)






<!--HONumber=Apr16_HO3-->


