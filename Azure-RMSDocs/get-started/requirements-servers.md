---
title: "Azure RMS 需求：支援 Azure Rights Management 的內部部署伺服器 | Azure RMS"
description: 
keywords: 
author: cabailey
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: get-started-article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: e7d91f2d-d6a7-4c7e-821f-c94e4be9967d
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: ed50d87138c428fadfd22cd5b3ef3c7f7e421848
ms.openlocfilehash: 7e718d8178dd7c4b18ea7a19eb3165ee06dc4b36


---


# Azure RMS 需求：支援 Azure RMS 的內部部署伺服器

*適用於︰Azure Rights Management、Office 365*

當您使用 Azure RMS 連接器時可搭配使用下列內部部署伺服器產品與 Azure RMS，其作為內部部署伺服器與 Azure RMS 之間的通訊介面 (轉送)。 此外，此設定需要您在 Active Directory 樹系與 Azure Active Directory 之間設定目錄同步。

-   **Exchange Server**：

    -   Exchange Server 2016

    -   Exchange Server 2013

    -   Exchange Server 2010

-   **Office SharePoint Server**：

    -   Office SharePoint Server 2016

    -   Office SharePoint Server 2013

    -   Office SharePoint Server 2010

-   **執行 Windows Server 並使用檔案分類基礎結構 (FCI) 的檔案伺服器**：

    -   Windows Server 2012 R2

    -   Windows Server 2012

    > [!NOTE]
    > 因為執行 Windows Server 2008 R2 的檔案伺服器沒有內建的檔案管理工作動作可套用 RMS 保護，您在此情況下無法使用 RMS 連接器。 不過，若您設定自訂檔案管理工作來執行可執行檔或指令檔，而這些檔案可使用 Azure RMS 來保護檔案，則您可以在這些作業系統上使用檔案分類基礎結構和 Azure RMS。 例如，使用 [RMS 保護 Cmdlet](https://msdn.microsoft.com/library/azure/mt433195.aspx) 的 Windows PowerShell 指令碼。
    > 
    > 您也可以對執行較新版本 Windows Server 的伺服器使用這些 Cmdlet，好處是這些 Cmdlet 可以保護所有檔案類型。 RMS 連接器只保護 Office 檔案。 如需做法指示，請參閱[具有 Windows Server 檔案分類基礎結構 (FCI) 的 RMS 保護](../rms-client/configure-fci.md)。

RMS 連接器在 Windows Server 2012 R2、Windows Server 2012 和 Windows Server 2008 R2 上受到支援。

如需有關如何為這些內部部署伺服器設定 RMS 連接器的詳細資訊，請參閱[部署 Azure Rights Management 連接器](../deploy-use/deploy-rms-connector.md)。

## 後續步驟
若要檢查其他需求，請參閱 [Azure Rights Management 的需求](requirements-azure-rms.md)。



<!--HONumber=Jun16_HO4-->


