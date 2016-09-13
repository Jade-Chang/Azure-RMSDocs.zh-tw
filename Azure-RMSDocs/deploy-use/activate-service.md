---
title: "啟用 Azure Rights Management | Azure RMS"
description: "您必須啟用 (Azure RMS)，您的組織才可以開始使用支援資訊保護解決方案的應用程式與服務來保護重要資料。"
author: cabailey
manager: mbaldwin
ms.date: 08/25/2016
ms.topic: article
ms.prod: 
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: f8707e01-b239-4d1a-a1ea-0d1cf9a8d214
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: ad32910b482ca9d92b4ac8f3f123eda195db29cd
ms.openlocfilehash: 2a0e1984e76ae355bfab099e0aced956ef93a7de


---

# 啟用 Azure Rights Management

>*適用於︰Azure Rights Management、Office 365*

當您啟用 [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)] (Azure RMS) 時，您的組織就可以開始使用支援資訊保護解決方案的應用程式與服務保護重要資料。 系統管理員也可以管理與監控您的組織所擁有的受保護檔案及電子郵件。 您必須先啟動 [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)]，才能開始在 Office、SharePoint 和 Exchange 中使用資訊版權管理 (IRM) 功能，並保護任何敏感或機密檔案。

如果您想要在啟動服務之前先深入了解 Azure Rights Management，例如，它可以解決哪些商務問題、幾個一般使用案例，及運作方式，請參閱[什麼是 Azure Rights Management？](../understand-explore/what-is-azure-rms.md)

> [!IMPORTANT]
> 啟動 [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)] 之前，請確定您的組織具有包含 [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)] 服務的服務方案。 如果沒有，您將無法啟動 Azure RMS。
>
> 如需詳細資訊，請參閱[支援 Azure RMS 的雲端訂閱](../get-started/requirements-subscriptions.md)。

啟動 Azure RMS 之後，您組織中的所有使用者都可以在他們的檔案上套用資訊保護，且所有使用者都可以開啟 (使用) 受 Azure RMS 保護的檔案。 不過，如果您要的話，您可以限制誰可以套用資訊保護，方法是在分階段部署中使用登入控制項。 如需詳細資訊，請參閱本文中的[設定分階段部署的登入控制項](#configuring-onboarding-controls-for-a-phased-deployment)一節。

如需如何從管理入口網站啟用 Rights Management 的指示，請選取要使用 Office 365 系統管理中心 (預覽或傳統)，或是 Azure 傳統管理入口網站︰


- [Office 365 系統管理中心 - 預覽](activate-office365-preview.md)
- [Office 365 系統管理中心 - 傳統](activate-office365-classic.md)
- [Azure 傳統入口網站](activate-azure-classic.md)

您也可以使用 Windows PowerShell 來啟用 [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)]：

1. 安裝可安裝 Azure Rights Management 管理模組的 Azure Rights Management 管理工具。 如需指示，請參閱[安裝 Windows PowerShell for Azure Rights Management](../deploy-use/install-powershell.md)。

2. 從 Windows PowerShell 工作階段中，執行 [Connect-AadrmService](https://msdn.microsoft.com/library/windowsazure/dn629415.aspx)，並在系統出現提示時，提供 Azure RMS 租用戶的全域管理員帳戶詳細資料。

3. 執行可啟用 Azure RMS 服務的 [Enable-Aadrm](http://msdn.microsoft.com/library/windowsazure/dn629412.aspx)。

## 設定分階段部署的登入控制項
如果您不想要讓所有使用者能夠藉由使用 Azure RMS 以立即保護檔案，您可以設定使用者上線控制，方法是使用 [Set-AadrmOnboardingControlPolicy](http://msdn.microsoft.com/library/azure/dn857521.aspx) Windows PowerShell 命令。 您可以在啟動 Azure RMS 前後執行此命令。

> [!IMPORTANT]
> 若要使用此命令，您至少必須有 **2.1.0.0** 版的 [Azure RMS Windows PowerShell 模組](http://go.microsoft.com/fwlink/?LinkId=257721)。
>
> 若要檢查已安裝的版本，請執行︰**(Get-Module aadrm –ListAvailable).Version**

例如，如果基於測試目的，您一開始只希望 “IT department” 群組中的管理員 (包含 fbb99ded-32a0-45f1-b038-38b519009503 物件識別碼) 能夠保護內容，請使用下列命令：

```
Set-AadrmOnboardingControlPolicy – SecurityGroupObjectId fbb99ded-32a0-45f1-b038-38b519009503
```
請注意，您必須針對此組態選項指定一個群組；您無法指定個人使用者。

或者，如果您要確保只有已正確授權使用 Azure RMS 的使用者才能保護內容：

```
Set-AadrmOnboardingControlPolicy -UseRmsUserLicense $true
```
當您使用這些登入控制項時，組織中的所有使用者一律可以使用受部分使用者保護的受保護內容，但他們無法從用戶端應用程式中自行套用資訊保護。 例如，他們無法在 Office 用戶端中看到啟動 Azure RMS 時會自動發佈的預設範本，或您所設定的自訂範本。  伺服器端應用程式 (例如 Exchange) 可針對 RMS 整合實作個別使用者的控制，以達成相同結果。


## 後續步驟
現在您已為您的組織啟動 [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)]，請使用 [Azure Rights Management 部署藍圖](../plan-design/deployment-roadmap.md)檢查將 [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)] 轉出給使用者和系統管理員之前，是否還需要執行其他設定步驟。 

例如，您可能想要使用[自訂範本](configure-custom-templates.md)讓使用者更容易將資訊保護套用至檔案，藉由安裝 [RMS 連接器](deploy-rms-connector.md)來連接您的內部部署伺服器以使用 [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)]，並且部署 [Rights Management 共用應用程式](../rms-client/sharing-app-windows.md)，支援保護所有裝置上的所有檔案類型。 

Office 服務 (例如 Exchange Online 及and SharePoint Online) 都需要先進行其他設定，才能使用其資訊版權管理 (IRM) 功能。 如需關於您的應用程式如何與 [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)] 搭配使用的詳細資訊，請參閱[應用程式如何支援 Azure Rights Management](../understand-explore/applications-support.md)。




<!--HONumber=Aug16_HO4-->


