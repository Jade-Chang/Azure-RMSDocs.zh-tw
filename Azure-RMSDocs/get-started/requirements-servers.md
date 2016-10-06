---
title: "資料保護的內部部署伺服器支援 | Azure Information Protection"
description: "利用 Rights Management 連接器找出可以使用 Azure Information Protection 之 Azure Rights Management Service 的內部部署伺服器產品。"
author: cabailey
manager: mbaldwin
ms.date: 09/25/2016
ms.topic: get-started-article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: e7d91f2d-d6a7-4c7e-821f-c94e4be9967d
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 976281d2b1f9c87bbb0806fef98b2520772c507c
ms.openlocfilehash: 22f63cae58f6dfe7e0381a561ffb348177585809


---


# 支援 Azure Rights Management 資料保護的內部部署伺服器

>*適用於︰Azure Information Protection、Office 365*

當您使用 Azure Rights Management 連接器時，下列內部部署伺服器產品支援 Azure Information Protection。 此連接器作用如同內部部署伺服器與 Azure Information Protection 用以保護 Office 文件和電子郵件的 Azure Rights Management Service 之間的通訊介面 (轉送)。 

若要使用此連接器，您必須設定 Active Directory 樹系與 Azure Active Directory 之間的目錄同步處理。

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
    > 因為執行 Windows Server 2008 R2 的檔案伺服器沒有內建的檔案管理工作動作可套用 Rights Management 保護，所以您在此情況下無法使用 Rights Management 連接器。 不過，若您設定自訂檔案管理工作來執行可執行檔或指令檔，而這些檔案可使用 Azure RMS 來保護檔案，則您可以在這些作業系統上使用檔案分類基礎結構和 Azure RMS。 例如，使用 [RMS 保護 Cmdlet](https://msdn.microsoft.com/library/azure/mt433195.aspx) 的 Windows PowerShell 指令碼。
    > 
    > 您也可以對執行較新版本 Windows Server 的伺服器使用這些 Cmdlet，好處是這些 Cmdlet 可以保護所有檔案類型。 RMS 連接器只保護 Office 檔案。 如需做法指示，請參閱[具有 Windows Server 檔案分類基礎結構 (FCI) 的 RMS 保護](../rms-client/configure-fci.md)。

Rights Management 連接器在 Windows Server 2012 R2、Windows Server 2012 和 Windows Server 2008 R2 上受到支援。

如需如何為這些內部部署伺服器設定 Rights Management 連接器的詳細資訊，請參閱[部署 Azure Rights Management 連接器](../deploy-use/deploy-rms-connector.md)。

## 後續步驟
若要檢查其他需求，請參閱 [Azure Rights Management 的需求](requirements-azure-rms.md)。



<!--HONumber=Sep16_HO5-->


