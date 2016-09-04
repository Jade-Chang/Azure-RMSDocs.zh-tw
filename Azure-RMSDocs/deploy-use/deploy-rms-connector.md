---
title: "部署 Azure Rights Management 連接器 | Azure RMS"
description: "使用此資訊來深入瞭解 Azure Rights Management (RMS) 連接器，以及您如何搭配使用該連接器與使用 Microsoft Exchange Server、Microsoft SharePoint Server，或執行 Windows Server 之檔案伺服器的現有內部部署，及使用檔案伺服器資源管理員的檔案分類基礎結構 (FCI) 功能，藉此提供資訊保護。"
author: cabailey
manager: mbaldwin
ms.date: 08/24/2016
ms.topic: article
ms.prod: 
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 90e7e33f-9ecc-497b-89c5-09205ffc5066
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 024a29d7c7db2e4c0578a95c93e22f8e7a5b173e
ms.openlocfilehash: 003dcc6a000d303fc42204d61145cf067dc16d32


---

# 部署 Azure Rights Management 連接器

>*適用於︰Azure Rights Management、Windows Server 2012、Windows Server 2012 R2*

使用此資訊來深入瞭解 Azure Rights Management (RMS) 連接器，以及您如何搭配使用該連接器與使用 Microsoft Exchange Server、Microsoft SharePoint Server，或執行 Windows Server 之檔案伺服器的現有內部部署，及使用檔案伺服器資源管理員的檔案分類基礎結構 (FCI) 功能，藉此提供資訊保護。

> [!TIP]
> 如需含螢幕擷取畫面的高階範例案例，請參閱 [Azure RMS 運作方式](../understand-explore/what-admins-users-see.md)文章的[在執行 Windows Server 和檔案分類基礎結構的檔案伺服器上自動保護檔案](../understand-explore/what-admins-users-see.md#automatically-protecting-files-on-file-servers-running-windows-server-and-file-classification-infrastructure)一節。

## Microsoft Rights Management 連接器概觀
Microsoft Rights Management (RMS) 連接器可讓您快速啟用現有的內部部署伺服器，以搭配使用其資訊版權管理 (IRM) 功能與雲端架構 Microsoft Rights Management 服務 (Azure RMS)。 利用此功能，IT 和使用者可輕鬆保護您組織內部和外部的文件和圖片，無需安裝其他基礎結構或與其他組織建立信任關係。 在混合式案例中，即使某些使用者已連接到線上服務，您仍可使用此連接器。 例如，某些使用者的信箱使用 Exchange Online，而某些使用者的信箱使用 Exchange Server。 安裝 RMS 連接器之後，所有使用者皆可藉由使用 Azure RMS 保護並取用電子郵件和附件，而資訊保護會在兩個部署組態之間順暢地運作。

RMS 連接器是個占用資源很少的服務，您可安裝於執行 Windows Server 2012 R2、Windows Server 2012 或 Windows Server 2008 R2 之伺服器的內部部署中。 除了在實體電腦上執行連接器，您也可以在包括 Azure IaaS VM 的虛擬機器上執行它。 安裝和設定連接器後，其會成為內部部署伺服器與雲端服務之間的通訊介面 (轉送)。

如果您針對 Azure RMS 管理自己的租用戶金鑰 (攜帶您自己的金鑰，即 BYOK 案例)，RMS 連接器和使用該連接器的內部部署伺服器不會存取含您租用戶金鑰的硬體安全性模組 (HSM)。 這是因為所有使用租用戶金鑰的密碼編譯作業都是在 Azure RMS 執行，而不是在內部。

![RMS 連接器架構概觀](../media/RMS_connector.png)

RMS 連接器支援下列內部部署伺服器：Exchange Server、SharePoint Server，以及執行 Windows Server 的檔案伺服器，並使用檔案分類基礎結構來分類原則，且將原則套用至資料夾中的 Office 文件。 如果您想要使用檔案分類保護所有檔案類型，請勿使用 RMS 連接器，但請改用 [RMS 保護 cmdlet](https://msdn.microsoft.com/library/azure/mt433195.aspx)。

> [!NOTE]
> 如需這些內部部署伺服器的支援版本，請參閱[支援 Azure RMS 的內部部署伺服器](..\get-started\requirements-servers.md)。

使用下列資訊以協助您規劃、安裝和設定 RMS 連接器。 接著，您必須執行某些安裝後的設定，讓您的伺服器得以使用連接器。

-   [RMS 連接器的必要條件](deploy-rms-connector.md#prerequisites-for-the-rms-connector)

-   **步驟 1：**[安裝 RMS 連接器](install-configure-rms-connector.md#installing-the-rms-connector)

-   **步驟 2：**[輸入認證](install-configure-rms-connector.md#entering-credentials)

-   **步驟 3：**[授權伺服器使用 RMS 連接器](install-configure-rms-connector.md#authorizing-servers-to-use-the-rms-connector)

-   **步驟 4：**[設定負載平衡和高可用性](install-configure-rms-connector.md#configuring-load-balancing-and-high-availability)

-   選用：[設定 RMS 連接器使用 HTTPS](install-configure-rms-connector.md#configuring-the-rms-connector-to-use-https)

-   選用：[設定 Web Proxy 伺服器的 RMS 連接器](install-configure-rms-connector.md#configuring-the-rms-connector-for-a-web-proxy-server)

-   選用：[在系統管理電腦上安裝 RMS 連接器系統管理工具](install-configure-rms-connector.md#installing-the-rms-connector-administration-tool-on-administrative-computers)

-   **步驟 5：**[設定伺服器使用 RMS 連接器](configure-servers-rms-connector.md)

    -   [設定 Exchange 伺服器使用連接器](configure-servers-rms-connector.md#configuring-an-exchange-server-to-use-the-connector)

    -   [設定 SharePoint 伺服器使用連接器](configure-servers-rms-connector.md#configuring-a-sharepoint-server-to-use-the-connector)

    -   [設定檔案分類基礎結構的檔案伺服器以使用連接器](configure-servers-rms-connector.md#configuring-a-file-server-for-file-classification-infrastructure-to-use-the-connector)


## RMS 連接器的必要條件
安裝 RMS 連接器之前，請確定下列需求已備妥

|需求|詳細資訊|
|---------------|--------------------|
|啟動 Rights Management (RMS) 服務|[啟用 Azure Rights Management](activate-service.md)|
|內部部署 Active Directory 樹系與 Azure Active Directory 之間的目錄同步|啟動 RMS 之後，必須先設定 Azure Active Directory 以使用 Active Directory 資料庫中的使用者和群組。<br /><br />**重要**：您必須執行此目錄同步處理步驟，RMS 連接器才能運作，即使是在測試網路中也一樣。 雖然您可使用 Azure Active Directory 中手動建立的帳戶來使用 Office 365 和 Azure Active Directory，但此連接器要求 Azure Active Directory 中的帳戶與 Active Directory 網域服務同步。密碼手動同步處理並不夠。<br /><br />如需詳細資訊，請參閱下列資源：<br /><br />[整合內部部署身分識別與 Azure Active Directory](/active-directory/active-directory-aadconnect)<br /><br />[混合式身分識別目錄整合工具比較](/active-directory/active-directory-hybrid-identity-design-considerations-tools-comparison)|
|選用項但建議使用：<br /><br />啟用您內部部署 Active Directory 與 Azure Active Directory 之間的同盟|您可啟用您內部部署目錄與 Azure Active Directory 之間的識別同盟。 此設定可對 RMS 服務使用單一登入，藉此啟用更完美的使用者體驗。 若無單一登入，系統會先提示使用者出示其認證，再允許使用者使用受版權保護的內容。<br /><br />如需在 Active Directory 網域服務與 Azure Active Directory 之間使用 Active Directory Federation Services (AD FS) 以設定同盟的指示，請參閱 Windows Server 程式庫中的[檢查清單：使用 AD FS 實作和管理單一登入](http://technet.microsoft.com/library/jj205462.aspx)。|
|最少有兩部安裝 RMS 連接器的成員電腦：<br /><br />- 執行下列其中一個作業系統的 64 位元實體或虛擬電腦：Windows Server 2012 R2、Windows Server 2012 或 Windows Server 2008 R2。<br /><br />- 至少需要 1 GB RAM。<br /><br />- 至少需要 64 GB 磁碟空間。<br /><br />- 至少需要一個網路介面。<br /><br />- 透過無需驗證的防火牆 (或 Web Proxy) 存取網際網路。<br /><br />- 必須位於信任組織中其他樹系的樹系或網域，該組織安裝了您要與 RMS 連接器一起使用的 Exchange 或 SharePoint 伺服器。|對於容錯和高可用性，您至少必須在兩部電腦上安裝 RMS 連接器。<br /><br />**提示**：如果您使用 Outlook Web Access 或使用 Exchange ActiveSync IRM 的行動裝置，而且必須維護對 Azure RMS 所保護之電子郵件與附件的存取，我們建議您部署負載平衡型連接器伺服器群組，以確保高度可用性。<br /><br />您不需要有專門的伺服器來執行連接器，但必須將連接器安裝在使用連接器之伺服器以外的其他電腦上。<br /><br />**重要**：若要搭配使用這些服務的功能與 Azure RMS，請勿在執行 Exchange Server、SharePoint Server 的電腦，或對檔案分類基礎結構設定的檔案伺服器上安裝連接器。 此外，請勿將此連接器安裝在網域控制站上。|

## 後續步驟

移至[安裝和設定 Azure Rights Management 連接器](install-configure-rms-connector.md)。


<!--HONumber=Aug16_HO4-->


