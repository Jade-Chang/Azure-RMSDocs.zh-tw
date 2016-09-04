---
title: "執行 Windows Server 並使用檔案分類基礎結構 (FCI) 的檔案伺服器 | Azure RMS"
description: "設定 Windows Server 使用檔案分類基礎結構時，這項檔案伺服器資源管理員功能可以掃描本機檔案，並判斷它們是否包含敏感性資料。 符合這個準則的檔案會被標記系統管理員所定義的分類屬性。 接著，檔案分類基礎結構便可根據分類採取自動動作。 其中一個動作是使用 Azure Rights Management 和 Rights Management 連接器 (又稱為 RMS 連接器) 部署來套用資訊保護。 Azure RMS 就會自動保護 Office 檔案。"
author: cabailey
manager: mbaldwin
ms.date: 08/24/2016
ms.topic: article
ms.prod: 
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 8fdad425-5daf-4ce1-822f-9d2fb0b87df1
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 024a29d7c7db2e4c0578a95c93e22f8e7a5b173e
ms.openlocfilehash: 3ba4230674d387c100752f2e8698010afc8773b2


---


# 執行 Windows Server 並使用檔案分類基礎結構 (FCI) 的檔案伺服器

>*適用於︰Azure Rights Management、Office 365*


設定 Windows Server 使用檔案分類基礎結構時，這項檔案伺服器資源管理員功能可以掃描本機檔案，並判斷它們是否包含敏感性資料。 符合這個準則的檔案會被標記系統管理員所定義的分類屬性。 接著，檔案分類基礎結構便可根據分類採取自動動作。 其中一個動作是使用 [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)] 和 Rights Management 連接器 (又稱為 RMS 連接器) 部署來套用資訊保護。 Azure RMS 就會自動保護 Office 檔案。

若要保護所有檔案類型，請勿使用 RMS 連接器，而是改成從 [RMS 保護工具](https://www.microsoft.com/en-us/download/details.aspx?id=47256)使用 Cmdlet 執行 Windows PowerShell 指令碼。

分類原則既可完全設定又極具延伸性，可讓您防止可能由未獲授權和已獲授權的使用者引起的資料外洩。 它甚至可以協助降低由網路系統管理員引起的資料外洩風險，因為您可以設定不需要這些系統管理員存取檔案的原則。

如需部署和配置 Office 檔案之 RMS 連接器的指示，請參閱[部署 Azure Rights Management 連接器](../deploy-use/deploy-rms-connector.md)。

如需為所有檔案類型使用 Windows PowerShell 指令碼的指示，請參閱[具有 Windows Server 檔案分類基礎結構 (FCI) 的 RMS 保護](../rms-client/configure-fci.md)。



## 後續步驟
現在您瞭解應用程式和服務如何支援 Azure RMS，您可能想要比較 Azure RMS 與內部部署版本的 Rights Management、Active Directory Rights Management Services (AD RMS)。 如需功能、需求和安全性控制項的比較，請參閱[比較 Azure Rights Management 與 AD RMS](compare-azure-rms-ad-rms.md)。





<!--HONumber=Aug16_HO4-->


