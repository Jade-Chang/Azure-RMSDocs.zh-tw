---
title: "解除委任並停用 Azure Rights Management Service| Azure Information Protection"
description: "您決定不想再使用 Azure Information Protection 之資訊保護服務時的資訊和指示。"
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 09/25/2016
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 0b1c2064-0d01-45ae-a541-cebd7fd762ad
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 9d8354f2d68f211d349226970fd2f83dd0ce810b
ms.openlocfilehash: 865913eae3e0956c18d2caef4e68ab1dc07d74de


---

# <a name="decommissioning-and-deactivating-azure-rights-management"></a>解除委任並停用 Azure Rights Management

>*適用對象︰Azure Information Protection、Office 365*

您永遠可以藉由使用 Azure Information Protection 的 Azure Rights Management Service 控制您的組織是否保護內容，而且如果您決定不想再使用此資訊保護服務，也可保證您將不會被鎖定在先前受保護的內容之外。 如果您不需要繼續存取先前受保護的內容，您只需要停用服務即可讓 Azure Information Protection 的訂用帳戶過期。 例如，此情況適用於已完成測試 Azure Information Protection 時，但在生產環境中進行部署之前。

不過，如果您已在生產環境中部署 Azure Information Protection，請確定您擁有 Azure Information Protection 租用戶金鑰的複本，然後才停用 Azure Rights Management Service，且需在您的訂用帳戶到期之前執行這項操作，因為這樣可確保您可以在服務停用之後，保留由 Azure Rights Management 所保護之內容的存取權。 如果您使用您在其中以 HSM 產生及管理本身金鑰的「自備金鑰」(BYOK) 解決方案，您已經具有您的 Azure Information Protection 租用戶金鑰。 但如果它是由 Microsoft (預設值) 管理，請參閱 [Azure Rights Management 租用戶金鑰的作業](operations-tenant-key.md)文章中的指示以匯出您的租用戶金鑰。

> [!TIP]
> 即使您的訂用帳戶過期之後，您的 Azure Information Protection 租用戶仍然可長時間用於取得內容。 不過，您將不再能夠匯出您的租用戶金鑰。

當您擁有 Azure Information Protection 租用戶金鑰時，您可以在內部部署 Rights Management (AD RMS) 並匯入您的租用戶金鑰作為信任發行網域 (TPD)。 您接著可以有下列選項來解除委任 Azure Information Protection 部署：

|如果這適用於您...|… 做法：|
|----------------------------|--------------|
|您想要所有使用者繼續使用 Rights Management，但是要使用內部部署解決方案而不是使用 Azure Information Protection    →|當現有的使用者在此變更後取用受保護的內容時，使用 [Set-AadrmMigrationUrl](https://msdn.microsoft.com/library/azure/dn629429.aspx) Cmdlet 將他們導向至您的內部部署。 使用者會自動使用 AD RMS 安裝來取用受保護的內容。<br /><br />若要讓使用者取用此變更之前受保護的內容，請使用適用於 Office 2016 或 Office 2013的 **LicensingRedirection** 登錄機碼 (如 RMS 用戶端部署注意事項中的[服務探索一節](../rms-client/client-deployment-notes.md)所述)，以及適用於 Office 2010 的 **LicenseServerRedirection** 登錄機碼 (如 [Office 登錄設定](https://technet.microsoft.com/library/dd772637%28v=ws.10%29.aspx)所述)，將您的用戶端重新導向至內部部署。|
|您想要完全停止使用 Rights Management 技術    →|授與指定的系統管理員[進階使用者權限](../deploy-use/configure-super-users.md)，並提供該人員 [RMS 保護工具](http://www.microsoft.com/en-us/download/details.aspx?id=47256)。<br /><br />此系統管理員接著可以使用工具來大量解密資料夾中受到 Azure Rights Management Service 保護的檔案，以便讓檔案還原成未受保護狀態，因此可以直接讀取而無需使用 Azure Information Protection 或 AD RMS 等 Rights Management 技術。 這項工具可以和 Azure Information Protection 的 Azure Rights Management Service 與 AD RMS 搭配使用，讓您可以選擇在停用 Azure Rights Management Service 之前或之後解密檔案。|
|您無法識別受 Azure Information Protection 之 Azure Rights Management Service 保護的所有檔案，或者您要讓所有使用者都能夠自動讀取已遺失的受保護檔案    →|使用適用於 Office 2016 和 Office 2013的 **LicensingRedirection** 登錄機碼 (如 RMS 用戶端部署注意事項中的[服務探索一節](../rms-client/client-deployment-notes.md)所述)，以及適用於 Office 2010 的 **LicenseServerRedirection** 登錄機碼 (如 [Office 登錄設定](https://technet.microsoft.com/library/dd772637%28v=ws.10%29.aspx)所述)，在所有用戶端電腦上部署登錄設定。<br /><br />也部署另一個登錄設定以防止使用者藉由將 **DisableCreation** 設為 **1** 來保護新檔案，如 [Office 登錄設定](https://technet.microsoft.com/library/dd772637%28v=ws.10%29.aspx)中所述。|
|您想要對已遺失的任何檔案進行受控制的手動復原服務    →|授與資料復原群組中指定的使用者[進階使用者權限](../deploy-use/configure-super-users.md)，並提供他們 [RMS 保護工具](http://www.microsoft.com/en-us/download/details.aspx?id=47256)，讓他們可以在標準使用者提出要求時取消保護檔案。<br /><br />在所有的電腦上，部署登錄設定以防止使用者藉由將 **DisableCreation** 設為 **1** 來保護新檔案，如 [Office 登錄設定](https://technet.microsoft.com/library/dd772637%28v=ws.10%29.aspx)中所述。|
如需此資料表中的程序的詳細資訊，請參閱下列資源：

-   如需 AD RMS 和部署參考的相關資訊，請參閱 [Active Directory Rights Management 服務概觀](https://technet.microsoft.com/library/hh831364.aspx)。

-   如需匯入您的 Azure Information Protection 租用戶金鑰作為 TPD 檔案的指示，請參閱[新增信任發行網域](https://technet.microsoft.com/library/cc771460.aspx)。

-   若要針對 Azure Rights Management 安裝 Windows PowerShell 模組以設定移轉 URL，請參閱[針對 Azure Rights Management 安裝 Windows PowerShell](install-powershell.md)。

當您準備好停用組織的 Azure Rights Management Service 時，請使用下列指示。

## <a name="deactivating-rights-management"></a>停用 Rights Management
使用下列其中一個程序來停用 [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)]。

> [!TIP]
> 您也可以使用 Windows PowerShell Cmdlet [Disable-Aadrm](http://msdn.microsoft.com/library/windowsazure/dn629422.aspx) 來停用 [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)]。

#### <a name="to-deactivate-rights-management-from-the-office-365-admin-center"></a>若要從 Office 365 系統管理中心停用 Rights Management

1.  [使用工作或學校帳戶登入 Office 365](https://portal.office.com/) ，也就是您的 Office 365 部署的系統管理員。

2.  如果 Office 365 系統管理中心未自動顯示，請選取左上角的應用程式啟動器圖示，並選擇 [管理員]。 只有 Office 365 管理員才會看到 [管理員] 磚。

    > [!TIP]
    > 如需系統管理中心說明，請參閱[關於 Office 365 系統管理中心 - 管理員說明](https://support.office.com/article/About-the-Office-365-admin-center-Admin-Help-58537702-d421-4d02-8141-e128e3703547)。

3.  展開左窗格中的 [服務設定]。

4.  按一下 [Rights Management]。

5.  在 **[RIGHTS MANAGEMENT]** 頁面上，按一下 **[管理]**。

6.  按一下 [Rights Management]  頁面上的 [停用] 。

7.  出現 [是否要停用 Rights Management？] 提示時，按一下 [停用] 。

現在應該會顯示 [Rights Management 未啟動]  及要啟動的選項。

#### <a name="to-deactivate-rights-management-from-the-azure-classic-portal"></a>若要從 Azure 傳統入口網站停用 Rights Management

1.  登入 [Azure 傳統入口網站](http://go.microsoft.com/fwlink/p/?LinkID=275081)。

2.  在左窗格中，按一下 [Active Directory]。

3.  從 **[active directory]** 頁面中，按一下 **[RIGHTS MANAGEMENT]**。

4.  選取要對 [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)] 管理的目錄，按一下 [停用]，然後確認您的動作。

**[RIGHTS MANAGEMENT 狀態]** 現在應該會顯示為 **[非作用中]** ，且 **[停用]** 選項會取代為 **[啟動]**。






<!--HONumber=Nov16_HO2-->


