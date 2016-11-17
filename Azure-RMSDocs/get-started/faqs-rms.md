---
title: "Azure 資訊保護之資料保護服務 Azure Rights Management 的常見問題集 | Azure 資訊保護"
description: "Azure 資訊保護之資料保護服務 Azure Rights Management (Azure RMS) 的一些常見問題集。"
author: cabailey
manager: mbaldwin
ms.date: 10/24/2016
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 90df11c5-355c-4ae6-a762-351b05d0fbed
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 6566e0ce901097bcf5f30d76be67522d3464f100
ms.openlocfilehash: c92e35b0cb9f892f7859511365027c241d0f1ef6


---

# Azure 資訊保護中資料保護的常見問題集

>*適用於︰Azure 資訊保護、Office 365*

對 Azure 資訊保護的資料保護服務 Azure Rights Management 有疑問？ 看看此處是否有解答。 

## 檔案必須存在於雲端中才能受到 Azure Rights Management 保護嗎？
否，這是一個常見的誤解。 Azure Rights Management Service (和 Microsoft) 不會在資訊保護程序中查看或儲存您的資料。 您所保護的資訊永遠不會傳送至或儲存在 Azure 中，除非您明確地將它儲存在 Azure 中，或使用將它儲存在 Azure 中的另一項雲端服務。 

如需詳細資訊，請參閱 [Azure RMS 如何運作？請參閱背後原理](../understand-explore/how-does-it-work.md)，以便了解在內部部署建立和儲存的可樂機密配方如何受到 Azure Rights Management Service 保護，但是仍然在內部部署。

## 我可以整合 Azure Rights Management Service 與我的內部部署伺服器嗎？
是。 Azure Rights Management 可與您的內部部署伺服器整合，例如 Exchange Server、SharePoint 和 Windows 檔案伺服器。 若要這樣做，請使用 [Rights Management 連接器](../deploy-use/deploy-rms-connector.md)。 或者，如果您只想在 Windows Server 上使用檔案分類基礎結構 (FCI)，則可以使用 [Azure Rights Management Protection Cmdlets](https://technet.microsoft.com/library/mt601315%28v=ws.10%29.aspx) (Azure RMS 保護 Cmdlet)。 您也可以同步處理 Active Directory 網域控制站與 Azure AD 並在兩者間建立同盟，以為使用者獲得更順暢的驗證體驗，例如使用 [Azure AD Connect](http://azure.microsoft.com/documentation/articles/active-directory-aadconnect/)。

Azure Rights Management 會在必要時自動產生及管理 XrML 憑證，因此它不會使用內部部署 PKI。 如需 Azure Rights Management 如何使用憑證的詳細資訊，請參閱 [Azure RMS 如何運作](../understand-explore/how-does-it-work.md)一文中的 [Azure RMS 運作方式的逐步解說：第一次使用、內容保護、內容取用](../understand-explore/how-does-it-work.md#walkthrough-of-how-azure-rms-works-first-use-content-protection-content-consumption)一節。

## 在哪裡可以找到整合 Azure RMS 的協力廠商解決方案相關資訊？

許多軟體廠商已經有整合 Azure Rights Management 的解決方案或正在實作這類解決方案，因此廠商清單正快速增加。 您可以參閱 [Enterprise Mobility and Security Blog](https://blogs.technet.microsoft.com/enterprisemobility/?product=azure-rights-management-services) (Enterprise Mobility and Security 部落格) 並從 [Dan Plastina @TheRMSGuy](https://twitter.com/TheRMSGuy) 的 Twitter 帳戶取得最新更新。 不過，如果您有特定問題，請傳送電子郵件訊息給資訊保護小組：askipteam@microsoft.com。

## RMS 連接器是否有管理組件或類似的監視機制？

雖然 Rights Management 連接器會將資訊、警告和錯誤訊息記錄到事件記錄檔中，但並沒有包含監視這些事件之功能的管理組件。 不過，[監視 Azure Rights Management 連接器](../deploy-use/monitor-rms-connector.md)中會記錄事件及其描述的清單，包括可協助您採取更正動作的詳細資訊。

## 僅有全域管理員才能設定 Azure RMS，或是我可以將此作業委派給其他系統管理員？

毫無疑問，Office 365 租用戶或 Azure AD 租用戶的全域管理員可以執行 Azure Rights Management Service 的所有系統管理工作。 不過，如果您想要將系統管理權限指派給其他使用者，可以使用 [Add-AadrmRoleBasedAdministrator](https://msdn.microsoft.com/library/dn629417.aspx) 這個 Azure RMS PowerShell Cmdlet，來進行此作業。 您可以依據使用者帳戶或群組，來指派此系統管理角色。 您可以使用**全域管理員**和**連接器系統管理員**這兩種角色。 

如這些角色的名稱所示，第一個角色具有執行 Azure Rights Management 所有管理工作的權限 (而不需要將其設為其他雲端服務的全域管理員)，而第二個角色僅有執行 Rights Management (RMS) 連接器的權限。

注意事項如下：

- 只有 Office 365 全域管理員和 Azure AD 全域管理員可以使用管理入口網站 (Office 365 系統管理中心或 Azure 傳統入口網站) 來設定 Azure RMS。 若為獲 Azure RMS 全域管理員角色指派的使用者，則必須使用 Azure RMS PowerShell 命令來設定 Azure RMS。 若要找出特定工作的正確 Cmdlet，請參閱[使用 Windows PowerShell 管理 Azure Rights Management](../deploy-use/administer-powershell.md)。

- 如果您已設定[登入控制項](../deploy-use/activate-service.md#configuring-onboarding-controls-for-a-phased-deployment)，這對 Azure RMS 的管理功能沒有影響，但 RMS 連接器除外。 好比說，如果您已設定登入控制項，僅限讓「IT 部門」群組來保護內容，則您必須使用屬於該群組成員的帳戶來安裝和設定 RMS 連接器。 

- Azure RMS 的系統管理員 (租用戶的全域管理員或 Azure RMS 的全域管理員) 皆不能自動取消受 Azure RMS 所保護之電子郵件或文件的保護。 只有在啟用進階使用者功能時，獲指派為 Azure RMS 進階使用者的使用者可以執行這項操作。 不過，租用戶的全域管理員以及任何 Azure RMS 的全域管理員皆可將使用者指派為進階使用者，包括他們自己的帳戶。 他們也可以啟用進階使用者功能。 這些動作都會記錄在 Azure RMS 系統管理員記錄中。 如需詳細資訊，請參閱[設定 Azure Rights Management 和探索服務或資料復原的進階使用者](../deploy-use/configure-super-users.md)的安全性最佳做法一節。 


## 我有 Exchange 的混合式部署，有部分使用者在 Exchange Online 上，而其他的使用者在 Exchange 和其他人在 Exchange Server 上—Azure RMS 支援這個情形嗎？
絕對支援，而且其優點在於，使用者將能夠順暢地跨兩個 Exchange 部署保護和取用受保護的電子郵件和附件。 如需此組態，請[啟用 Azure RMS](../deploy-use/activate-service.md) 並[啟用 Exchange online 的 IRM](https://technet.microsoft.com/library/dn151475%28v=exchg.150%29.aspx)，然後為 Exchange Server [部署和設定 RMS 連接器](../deploy-use/deploy-rms-connector.md)。

## 如果我在生產環境中使用這項保護，我的公司會不會在解決方案中遭到鎖定，或無法存取我們以 Azure RMS 保護之內容的風險？
不會，即使您決定不再使用 Azure Rights Management Service，您隨時都可以完全掌控您的資料，並且可以繼續存取它。 如需詳細資訊，請參閱[解除委任並停用 Azure Rights Management](../deploy-use/decommission-deactivate.md)。

不過，在您解除委任 Azure RMS 部署之前，我們想要聽取您的意見並了解您為什麼這樣決定。 如果 Azure Rights Management 保護無法滿足您的商務需求，請在規劃新功能期間或有替代方案時連絡我們。 請將電子郵件訊息傳送至 [AskIPTeam@Microsoft.com](mailto:askipteam@microsoft.com?subject=Planning%20to%20decommission%20Azure%20RMS) ，我們會很樂意與您討論技術和商務需求。

## 我是否能控制哪些使用者可以使用 Azure RMS 來保護內容？
是，Azure Rights Management Service 具有適用於這種情況的使用者上線控制功能。 如需詳細資訊，請參閱[啟用 Azure Rights Management](../deploy-use/activate-service.md) 文章的[設定分階段部署的登入控制項](../deploy-use/activate-service.md#configuring-onboarding-controls-for-a-phased-deployment)一節。

## 我可以防止使用者與特定組織共用受保護的文件嗎？
使用 Azure Rights Management Service 保護資料的其中一個最大優點是它支援企業對企業共同作業，您不必設定明確信任的每個夥伴組織，因為 Azure AD 會為您處理驗證程序。

沒有管理選項可供用來防止使用者安全地與特定組織共用文件。 例如，您要封鎖您不信任或在業務上與您競爭的組織。 防止 Azure Rights Management Service 將受保護的文件傳送給這些組織中的使用者將是徒勞無功的舉動，因為如此一來您的使用者將會以未受保護的狀態共用文件，這大概是您最不想要在此案例中看到的結果！ 舉例來說，這樣您將無法識別誰在與這些組織中的哪些使用者共用公司的機密文件，但如果文件 (或電子郵件) 有受到 Azure Rights Management Service 保護，您就能加以識別。

## 當我與公司外部人員共用受保護的文件時，如何讓該使用者通過驗證？
Azure Rights Management Service 一律使用 Azure Active Directory 帳戶和相關聯的電子郵件地址進行使用者驗證，讓系統管理員可以順暢進行企業對企業的共同作業。 如果其他組織使用 Azure 服務，使用者將會在 Azure Active Directory 擁有帳戶，即使這些帳戶已進行內部部署建立和管理並且同步處理至 Azure 亦然。 如果組織背後擁有 Office 365，此服務也會將 Azure Active Directory 用於使用者帳戶。 如果使用者的組織在 Azure 中沒有受管理的帳戶，使用者可以註冊[個人版 RMS](../understand-explore/rms-for-individuals.md)，它會利用使用者的帳戶為組織建立未受管理的 Azure 租用戶及目錄，以讓該名使用者 (及後續使用者) 可以通過 Azure Rights Management Service 的驗證。

這些帳戶的驗證方法可能會不同，取決於其他組織中的系統管理員對 Azure Active Directory 帳戶的設定方式。 比方說，他們可以使用為這些帳戶、多因素驗證 (MFA)、聯盟所建立的密碼，或是在 Active Directory 網域服務中建立並同步處理至 Azure Active Directory 的密碼。

## 我可以將外部使用者 (我公司以外的人員) 新增至自訂範本嗎？
可以。 建立使用者 (和系統管理員) 可以從應用程式中選取的自訂範本，可讓使用者快速並輕鬆地使用您指定的預先定義原則套用資訊保護。 範本中的其中一個設定是誰能夠存取內容，而且您可以從組織內指定使用者和群組，從組織外指定使用者。

若要指定來自組織外的使用者，請在設定範本時將他們以連絡人的身分加入您在 Azure 傳統入口網站選取的群組中。 或使用[適用於 Azure Rights Management 的 Windows PowerShell 模組](../deploy-use/install-powershell.md)：

-   **使用權限定義物件來建立或更新範本**。    在您接著用來建立或更新範本的權限定義物件中，指定外部電子郵件地址及其權限。 使用 [New-AadrmRightsDefinition](https://msdn.microsoft.com/library/azure/dn727080.aspx) Cmdlet 來建立變數，然後將此變數提供給具備 [Add-AadrmTemplate](https://msdn.microsoft.com/library/azure/dn727075.aspx) Cmdlet (適用於新的範本) 或 [Set-AadrmTemplateProperty](https://msdn.microsoft.com/library/azure/dn727076.aspx) Cmdlet (用以修改現有的範本) 的 -RightsDefinition 參數，可指定權限定義物件。 不過，如果您要將這些使用者新增到現有的範本，您必須為範本中的現有群組 (而不只是外部使用者) 定義權限定義物件。

如需自訂範本的詳細資訊，請參閱[設定 Azure Rights Management Service 的自訂範本](../deploy-use/configure-custom-templates.md)。

## Azure RMS 是否使用 Azure AD 中的動態群組？
Azure AD Premium 功能可讓您藉由指定[以屬性為基礎的規則](https://azure.microsoft.com/documentation/articles/active-directory-accessmanagement-groups-with-advanced-rules/)，設定群組的動態成員資格。 當您在 Azure AD 中建立安全性群組時，此群組類型支援動態成員資格，但不支援電子郵件地址，因此無法搭配 Azure Rights Management Service 使用。 不過，您現在可以在支援這兩個動態成員資格和擁有郵件功能的 Azure AD 中建立新的群組類型。 當您在 Azure 傳統入口網站中新增群組時，您可在 [群組類型] 中選擇 [Office 365「預覽」]。 因為此群組擁有郵件功能，您可以將其與 Azure Rights Management 保護搭配使用。

如同選項名稱清楚顯示，這個新的群組類型仍在預覽中，使用預期的額外功能和參考的新文件。 同時，我們想要確認您可以搭配使用此新群組類型與 Azure Rights Management 保護。


## Azure RMS 支援哪些裝置和檔案類型？
如需支援 Azure Rights Management Service 的裝置清單，請參閱 [Azure RMS 需求：支援 Azure RMS 的用戶端裝置](../get-started/requirements-client-devices.md)。 目前並非所有支援的裝置都能支援所有 Rights Management 功能，因此請務必另外查看[支援 Azure Rights Management 資料保護的應用程式](../get-started/requirements-applications.md)中的表格。

Azure Rights Management Service 可支援所有檔案類型。 對於文字、影像、Microsoft Office (Word、Excel、PowerPoint) 檔案、.pdf 檔案及部分其他應用程式檔案類型，Azure Rights Management 提供了包含加密和強制執行權限的原生保護功能。 對於所有其他應用程式和檔案類型，一般保護提供檔案封裝及驗證來確認使用者是否獲得開啟檔案授權。

如需 Azure Rights Management 原本就支援的副檔名清單，請參閱 [Rights Management 共用應用程式系統管理員指南](../rms-client/sharing-app-admin-guide.md)的[支援的檔案類型與副檔名](../rms-client/sharing-app-admin-guide-technical.md#supported-file-types-and-file-name-extensions)一節。 使用會自動將一般保護套用到這些檔案的 RMS 共用應用程式可支援未列出的副檔名。

## 當我開啟受 RMS 保護的 Office 文件時，相關聯的暫存檔案是否也會變成受 RMS 保護？

否。 在此案例中，相關聯的暫存檔案不會包含原始文件中的資料，而是只包含使用者在開啟檔案時所輸入的資料。 與原始檔案不同，暫存檔案顯然不是針對共用所設計，而且會保留在裝置上，並受本機安全性控制項 (例如 BitLocker 與 EFS) 保護。

## 我們真的想要搭配使用 BYOK 和 Azure 資訊保護，聽說這樣無法和 Exchange Online 相容 - 有什麼好建議嗎？
請勿讓目前的限制延遲了您使用 Azure 資訊保護的 Azure Rights Management Service。 如果您擁有 Exchange Online 並且想要使用「自備金鑰」(BYOK)，建議您立即以 Microsoft 在其中產生並管理金鑰的預設金鑰管理模式來部署 Azure 資訊保護。 如此一來，您就可以立即取得保護重要檔案和電子郵件的所有優點，並且可以在日後選擇移至 BYOK (例如，當 Exchange Online 可支援 BYOK 時)。 當您執行移至 BYOK 時，仍可使用備份金鑰存取先前所保護的文件和電子郵件。

不過，如果您的公司原則要求您使用硬體安全模組 (HSM)，這樣反而會封鎖您的 Azure 資訊保護部署，另一個選項是立即使用 BYOK 來部署 Azure 資訊保護，但是 Rights Management 對 Exchange 的保護功能會減少。 如需詳細資訊，請參閱[規劃及實作 Azure Rights Management 租用戶金鑰](../plan-design/plan-implement-tenant-key.md)的 [BYOK 定價和限制](../plan-design/byok-price-restrictions.md)。

## 我正在尋找的功能似乎不是使用 SharePoint 受保護程式庫—有規劃對我的功能的支援嗎？
目前，SharePoint 使用 IRM 受保護文件庫支援 Rights Management 受保護文件，該文件庫不支援自訂範本、文件追蹤和一些其他功能。 如需詳細資訊，請參閱 [Office 應用程式和服務](../understand-explore/office-apps-services-support.md)文章的 [SharePoint Online 和 SharePoint Server](../understand-explore/office-apps-services-support.md#sharepoint-online-and-sharepoint-server) 一節。

如果您對尚未支援的特定功能有興趣，請務必留意 [Enterprise Mobility and Security Blog](https://blogs.technet.microsoft.com/enterprisemobility/?product=azure-rights-management-services) (Enterprise Mobility and Security 部落格) 上的公告。

## 如何在 SharePoint Online 中設定商務用 One Drive，讓使用者可以安全地與公司內外的人員共用其檔案？
根據預設，身為 Office 365 的系統管理員，您沒有進行此設定，但使用者已設定。

正如 SharePoint 網站系統管理員可啟用與設定其所擁有之 SharePoint 程式庫的 IRM，商務用 OneDrive 特別為使用者設計，以便啟用與設定本身商務用 OneDrive 程式庫的 IRM。  不過，透過使用 PowerShell，您即可為他們執行此作業。 如需指示，請參閱 [Office 365︰用戶端和線上服務的設定](../deploy-use/configure-office365.md)文章的 [SharePoint Online 和商務用 OneDrive：IRM 設定](../deploy-use/configure-office365.md#sharepoint-online-and-onedrive-for-business-irm-configuration)一節。

## 您是否具有成功部署的任何秘訣或訣竅？
審視許多部署案例並傾聽我們的客戶、夥伴、顧問和支援工程師意見後，我們從經驗中可傳達的其中一個最大秘訣是： **設計和部署簡單適當的原則**。

由於 Azure 資訊保護支援與任何人安全共用，因此您可確保建構完善的資料防護機制。 但請遵循適當的原則謹慎施行。 對許多組織而言，預防資料流失對企業最大的影響是，套用預設的適當原則範本來限制組織中人員的存取。 當然，您可視需要取得更精細的防護，如防止人員列印、編輯等等。但這些更精細的限制不適用於真正需要高層級安全性的文件，且不要只實作這些限制較多的原則一天，而是要將其視為階段性方案加以規劃。

## 我們要如何重新存取現在已離開組織的員工所保護的檔案？
使用 Azure RMS 的進階使用者功能，可以讓獲得授權的使用者擁有貴組織的 RMS 租用戶所授與之所有使用授權的完整擁有權。 此相同功能可在必要時讓獲得授權的服務編製索引並檢查檔案。

如需詳細資訊，請參閱[設定 Azure Rights Management 和探索服務或資料復原的進階使用者](../deploy-use/configure-super-users.md)。

## 在文件追蹤網站中測試撤銷時，有訊息說使用者在 30 天內仍然可以存取文件，這個期限是可以設定的嗎？

是。 此訊息是反映該特定檔案的使用授權。 使用授權是個別文件的憑證，授與開啟受保護檔案或電子郵件訊息的使用者。 此憑證包含該使用者對於檔案或電子郵件訊息的權限，還有用來加密內容的加密金鑰，以及文件原則中定義的額外存取限制。 當使用授權的有效期間過期，而使用者嘗試開啟檔案或電子郵件訊息時，必須再次向 Azure Rights Management Service 提交使用者認證。 

如果撤銷檔案，只有使用者向 Azure Rights Management Service 驗證才會執行該動作。 所以，如果檔案的使用授權有效期間為 30 天，而使用者已開啟文件，則該使用者在使用授權的持續時間內可以繼續存取文件。 當使用授權過期時，使用者必須重新驗證，此時會拒絕使用者存取，因為文件已撤銷。

租用戶的使用授權有效期間預設值是 30 天，您可以使用 PowerShell Cmdlet [Set-AadrmMaxUseLicenseValidityTime](https://msdn.microsoft.com/library/azure/dn932063.aspx) 設定此值。 您可使用自訂範本中更嚴格的設定覆寫這項設定。 

使用者可以在使用 RMS 共用應用程式時，選取選項 [允許我立即撤銷這些文件的存取權]，覆寫設定租用戶和範本設定。 此設定實際上可將使用授權的有效期間設為 0。 

如需使用授權運作方式的詳細資訊和範例，請參閱 [Set-AadrmMaxUseLicenseValidityTime](https://msdn.microsoft.com/library/azure/dn932063.aspx) 的詳細說明。

## Rights Management 可以防止擷取螢幕畫面嗎？
不授與**副本**[使用權](../deploy-use/configure-usage-rights.md)，Rights Management 可以防止在 Windows 平台 (Windows 7、Windows 8.1、Windows 10、Windows Phone) 和 Android 上許多常用的螢幕擷取畫面工具擷取螢幕畫面。 但是，iOS 和 Mac 裝置不允許任何應用程式防止擷取螢幕畫面，且瀏覽器 (例如，與 Outlook Web 應用程式與 Office Online 搭配使用時) 也不能防止擷取螢幕畫面。

防止擷取螢幕畫面可以協助避免意外或疏忽洩漏機密或敏感性資訊。 但是使用者有許多方法可以分享螢幕上顯示的資料，擷取螢幕畫面只有其中一種方法而已。 例如，意圖分享顯示資訊的使用者可以利用其照相手機拍照、重新鍵入資料，或只是以口頭方式傳播給他人。

如這些範例所示，即使支援 Rights Management API 的所有平台和所有軟體阻止擷取螢幕畫面，技術本身無法永遠阻止使用者分享他們不該分享的資料。 Rights Management 可利用授權和使用原則協助保護您的重要資料，但這套企業級權限管理解決方案應搭配其他控制使用。 例如，實作實體安全性，仔細篩選和監督獲得授權存取您的組織資料的人員，以及投入使用者教育，讓使用者瞭解哪些資料不應該分享。

## 使用者以 [不要轉寄] 與不包含 [轉寄] 權限的範本來保護電子郵件，有什麼不同？

除了名稱和外觀以外，**[不要轉寄]** 既不是 [轉寄] 權限的相反，也不是範本。 它其實是一組權限，包括限制複製、列印及儲存附件，以及限制轉寄電子郵件。 這些權限會透過選擇的收件者以動態方式套用到使用者，而不是由管理員以靜態方式指派。 如需詳細資訊，請參閱 [Configuring usage rights for Azure Rights Management](../deploy-use/configure-usage-rights.md) (設定 Azure Rights Management 的使用權限) 中[電子郵件的 [不要轉寄] 選項](../deploy-use/configure-usage-rights.md#do-not-forward-option-for-emails)一節。






<!--HONumber=Oct16_HO4-->


