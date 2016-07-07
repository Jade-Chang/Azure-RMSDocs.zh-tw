---
title: "從 AD RMS 移轉至 Azure Rights Management - 階段 1 | Azure RMS"
description: 
keywords: 
author: cabailey
manager: mbaldwin
ms.date: 06/23/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 5a189695-40a6-4b36-afe6-0823c94993ef
ms.reviewer: esaggese
ms.suite: ems
ms.sourcegitcommit: f7dd88d90357c99c69fe4fdde67c1544595e02f8
ms.openlocfilehash: defe008a9b78026ccac584bb06762228456a2916


---

# 移轉階段 1 - AD RMS 的伺服器端設定

*適用於︰Active Directory Rights Management Services、Azure Rights Management*

針對從 AD RMS 移轉至 Azure Rights Management (Azure RMS) 的階段 1 使用下列資訊。 這些程序涵蓋[從 AD RMS 移轉至 Azure Rights Management](migrate-from-ad-rms-to-azure-rms.md) 的步驟 1 到 4。


## 步驟 1：下載 Azure Rights Management 管理工具
移至 Microsoft 下載中心並下載 [Azure Rights Management 管理工具](http://go.microsoft.com/fwlink/?LinkId=257721)，其中包含適用於 Windows PowerShell 的 Azure RMS 管理模組。

安裝此工具。 如需指示，請參閱[安裝 Windows PowerShell for Azure Rights Management](../deploy-use/install-powershell.md)。

## 步驟 2： 從 AD RMS 匯出組態資料，並將它匯入至 Azure RMS
這個步驟是兩部分的程序：

1.  將信任的發佈網域 (TPD) 匯出至 .xml 檔案，以從 AD RMS 匯出組態資料。 所有移轉的這個程序都相同。

2.  將組態資料匯入至 Azure RMS。 根據目前的 AD RMS 部署組態以及 Azure RMS 租用戶金鑰的慣用拓撲，此步驟會有不同的程序。

### 從 AD RMS 匯出組態資料
針對具有您組織受保護內容的所有信任的發佈網域，在所有 AD RMS 叢集上執行下列程序。 您不需要在僅授權叢集上執行此程序。

> [!NOTE]
> 如果您使用 Windows Server 2003 Rights Management 而非這些指示，請依照[在不同的基礎結構中從 Windows RMS 移轉至 AD RMS](http://technet.microsoft.com/library/jj835767%28v=ws.10%29.aspx) 文章的[匯出 SLC、TUD、TPD 和 RMS 私密金鑰](http://technet.microsoft.com/library/jj835767%28v=ws.10%29.aspx)程序。

#### 匯出組態資料 (信任的發佈網域資訊)

1.  以具有 AD RMS 系統管理權限的使用者身分，登入 AD RMS 叢集。

2.  從 AD RMS 管理主控台 ([**Active Directory Rights Management Service**])，依序展開 AD RMS 叢集名稱和 [ **信任原則**]，然後按一下 [ **信任的發佈網域**]。

3.  在結果窗格中，選取信任的發佈網域，然後按一下 [動作] 窗格中的 [ **匯出信任的發佈網域**]。

4.  在 [ **匯出信任的發佈網域** ] 對話方塊中：

    -   按一下 [ **另存新檔** ]，並儲存至您所選擇的路徑和檔案名稱。 請務必指定 **.xml** 做為副檔名 (這不會自動予以附加)。

    -   指定並確認增強式密碼。 請記住這個密碼，因為您稍後將組態資料匯入至 Azure RMS 時會需要它。

    -   請不要選取此核取方塊來儲存 RMS 1.0 版格式的信任的網域檔案。

匯出所有信任的發佈網域之後，即可開始將此資料從 Thales 匯入至 Azure RMS 硬體安全性模組 (HSM) 的程序。 如需詳細資訊， 

### 將組態資料匯入至 Azure RMS
此步驟的確切程序取決於目前的 AD RMS 部署組態以及 Azure RMS 租用戶金鑰的慣用拓撲。

目前的 AD RMS 部署會針對您的伺服器授權人憑證 (SLC) 金鑰使用下列其中一個組態：

-   AD RMS 資料庫中的密碼保護。 這是預設組態。

-   使用 Thales 硬體安全性模組 (HSM) 的 HSM 保護。

-   使用非 Thales 供應商之硬體安全性模組 (HSM) 的 HSM 保護。

-   使用外部加密提供者所保護的密碼。

> [!NOTE]
> 如需搭配使用硬體安全性模組與 AD RMS 的詳細資訊，請參閱 [搭配使用 AD RMS 與硬體安全性模組](http://technet.microsoft.com/library/jj651024.aspx)。

兩個 Azure RMS 租用戶金鑰拓撲選項如下︰Microsoft 管理您的租用戶金鑰 (**由 Microsoft 管理**) 或您管理您的租用戶金鑰 (**由客戶管理**)。 管理您自己的 Azure RMS 租用戶金鑰時，有時稱為「整合您自己的金鑰」(BYOK)，而且需要 Thales 的硬體安全性模組 (HSM)。 如需詳細資訊，請參閱 [規劃及實作 Azure Rights Management 租用戶金鑰](plan-implement-tenant-key.md)文件。

> [!IMPORTANT]
> Exchange Online 目前與 Azure RMS BYOK 不相容。  如果您想要在移轉之後使用 BYOK，並計畫使用 Exchange Online，請確定您了解這項組態如何減少 Exchange online 的 IRM 功能。 檢閱 [BYOK 定價和限制](byok-price-restrictions.md)中的資訊，以協助您選擇最佳的 Azure RMS 租用戶金鑰拓撲進行移轉。

請使用下表來識別要用於移轉的程序。 不支援未列出的組合。

|目前的 AD RMS 部署|選擇的 Azure RMS 租用戶金鑰拓撲|移轉指示|
|-----------------------------|----------------------------------------|--------------------------|
|AD RMS 資料庫中的密碼保護|由 Mcrosoft 管理|請參閱本表之後的**受軟體保護的金鑰移轉至受軟體保護的金鑰**程序。<br /><br />這是最簡單的移轉路徑，而且您只需要將組態資料傳輸至 Azure RMS。|
|使用 Thales nShield 硬體安全性模組 (HSM) 的 HSM 保護|由客戶管理 (BYOK)|請參閱本表之後的 **受 HSM 保護的金鑰移轉至 受 HSM 保護的金鑰**程序。<br /><br />這需要 BYOK 工具組和兩組步驟，以將金鑰從內部部署 HSM 傳輸至 Azure RMS HSM，然後再將組態資料傳輸至 Azure RMS。|
|AD RMS 資料庫中的密碼保護|由客戶管理 (BYOK)|請參閱這個資料表後面的**軟體保護的金鑰移轉至 HSM 保護的金鑰**程序。<br /><br />這需要 BYOK 工具組和三組步驟，先擷取您的軟體金鑰並將它匯入至內部部署 HSM，然後再將金鑰從內部部署 HSM 傳輸至 Azure RMS HSM，最後再將組態資料傳輸至 Azure RMS。|
|使用非 Thales 供應商之硬體安全性模組 (HSM) 的 HSM 保護|由客戶管理 (BYOK)|如需如何將金鑰從此 HSM 傳輸至 Thales nShield 硬體安全性模組 (HSM)的指示，請連絡 HSM 的供應商。 然後，遵循這個資料表後面的 **HSM 保護的金鑰移轉至 HSM 保護的金鑰**程序的指示。|
|使用外部加密提供者所保護的密碼|由客戶管理 (BYOK)|如需如何將金鑰傳輸至 Thales nShield 硬體安全性模組 (HSM)的指示，請連絡加密提供者的供應商。 然後，遵循這個資料表後面的 **HSM 保護的金鑰移轉至 HSM 保護的金鑰**程序的指示。|
啟動這些程序之前，請確定您可以存取先前在匯出信任的發佈網域時所建立的 .xml 檔案。 例如，這些檔案可能儲存至您從 AD RMS 伺服器移至連線網際網路之工作站的 USB 隨身碟。

> [!NOTE]
> 不論您儲存這些檔案的方法為何，由於這些資料含有私密金鑰，因此請使用最佳的安全措施來加以保護。


若要完成步驟 2，請選擇您的移轉路徑的指示︰ 


- [軟體金鑰至軟體金鑰](migrate-softwarekey-to-softwarekey.md)
- [HSM 金鑰至 HSM 金鑰](migrate-hsmkey-to-hsmkey.md)
- [軟體金鑰至 HSM 金鑰](migrate-softwarekey-to-hsmkey.md)


## 步驟 3： 啟動您的 RMS 租用戶
[啟用 Azure Rights Management](../deploy-use/activate-service.md) 文件會完整涵蓋這個步驟的指示。


> [!TIP]
> 如果您有 Office 365 訂閱，則可以從 Office 365 系統管理中心或 Azure 傳統入口網站中啟動 Azure RMS。 建議您使用 Azure 傳統入口網站，因為您將使用此管理入口網站來完成下一個步驟。

**如果已啟用 Azure RMS 租用戶，怎麼辦？** 如果貴組織已啟動 Azure RMS 服務，則使用者可能已經使用 Azure RMS，利用自動產生的租用戶金鑰 (和預設範本) 來保護內容，而不是 AD RMS 提供的現有金鑰 (和範本)。 在您的內部網路上妥善管理的電腦上不太可能發生此情況，因為系統會為您的 AD RMS 基礎結構自動設定它們。 但是，還是有可能發生在工作群組電腦或不常連接至內部網路的電腦上。 不幸的是，也很難找到這些電腦，就是這個原因，我們建議您不要在從 AD RMS 匯入組態資料之前啟動這些服務。

如果已啟動 Azure RMS 租用戶，而且您可以識別這些電腦，請確定您在這些電腦上執行 CleanUpRMS_RUN_Elevated.cmd 指令碼，如步驟 5 中所述。 執行這個指令碼會強制它們重新初始化使用者環境，使他們可以下載更新的租用戶金鑰和匯入的範本。

此外，如果您已建立想要在移轉之後使用的自訂範本，就必須匯出並匯入這些範本。 下一個步驟說明此程序。 

## 步驟 4： 設定匯入的範本
因為所匯入範本的預設狀態為 [ **已封存**]，所以如果您想要使用者能夠搭配使用這些範本與 Azure RMS，則必須將此狀態變更為 [ **已發佈** ]。

從 AD RMS 匯入之範本的外觀和行為就像您可以在 Azure 傳統入口網站中建立的自訂範本一樣。 若要將匯入的範本變更為發佈，以讓使用者看到這些範本並從應用程式中加以選取，請參閱[設定 Azure Rights Management 的自訂範本](../deploy-use/configure-custom-templates.md)。

除了發佈新匯入的範本，您可能還需要進行兩個重要的範本變更，才能繼續移轉。 為了讓使用者在移轉程序期間具有更一致的體驗，請不要對匯入的範本進行其他變更；亦不要發佈 Azure RMS 隨附的兩個預設範本，或在此時建立新的範本。 相反地，請等到完成移轉程序並解除委任 AD RMS 伺服器。

針對此步驟，您可能需要進行的範本變更如下：

- 如果您在移轉之前已於 Azure RMS 中建立自訂範本，則必須手動匯出並匯入這些範本。

- 如果您的 AD RMS 範本有使用 **ANYONE** 群組，就必須手動新增對等的群組和權限。

## 如果您在移轉之前已建立自訂範本，程序如下：

如果您在移轉之前已建立自訂範本，則在移轉之後及啟動 Azure RMS 之前或之後，使用者將無法使用範本，即使這些範本已設為 [已發佈] 亦同。 您必須先執行下列作業，使用者才可以使用範本︰ 

1. 執行 [Get-AadrmTemplate](https://msdn.microsoft.com/library/dn727079.aspx)，以找出這些範本，並記下其範本識別碼。 

2. 使用 [Export-AadrmTemplate](https://msdn.microsoft.com/library/dn727078.aspx) 這個 Azure RMS PowerShell Cmdlet，以匯出範本。

3. 使用 [Import-AadrmTemplate](https://msdn.microsoft.com/library/dn727077.aspx) 這個 Azure RMS PowerShell Cmdlet，以匯入範本。

然後，您可以發佈或封存這些範本，如同在移轉之後建立的任何其他範本一樣。


## 如果您的 AD RMS 範本有使用 **ANYONE** 群組，程序如下：

如果您的 AD RMS 範本有使用 **ANYONE** 群組，在您將範本匯入到 Azure RMS 時，系統會自動移除此群組；您必須手動將對等群組或使用者以及相同的權限新增到已匯入的範本。 Azure RMS 的對等群組稱為 **AllStaff-7184AB3F-CCD1-46F3-8233-3E09E9CF0E66@<tenant_name>.onmicrosoft.com**。 例如，Contoso 的此群組看起來可能如下所示：**AllStaff-7184AB3F-CCD1-46F3-8233-3E09E9CF0E66@contoso.onmicrosoft.com**。

如果您不確定 AD RMS 範本是否包含 ANYONE 群組，可以使用下列 Windows PowerShell 範例指令碼來識別這些範本。 如需使用 Windows PowerShell with AD RMS 的詳細資訊，請參閱[使用 Windows PowerShell 來管理 AD RMS](https://technet.microsoft.com/library/ee221079%28v=ws.10%29.aspx)。

如果您在 Azure 傳統入口網站中複製其中一個預設權限原則範本，就可以看到您的組織自動建立的群組，然後在 [權限] 頁面上識別 [使用者名稱]。 不過，您無法使用 Azure 傳統入口網站將此群組新增至手動建立或匯入的範本，而必須改用下列其中一個 Azure RMS PowerShell 選項：

-   使用 [New-AadrmRightsDefinition](https://msdn.microsoft.com/library/azure/dn727080.aspx) PowerShell Cmdlet 將 "AllStaff" 群組和權限定義為權限定義物件，然後再次為其他各群組或使用者 (其已授予除了 ANYONE 群組以外原始範本中的權限) 執行此命令。 接著，使用 [Set-AadrmTemplateProperty](https://msdn.microsoft.com/library/azure/dn727076.aspx) Cmdlet 將上述所有權限定義物件新增至範本。

-   使用 [Export-AadrmTemplate](https://msdn.microsoft.com/library/azure/dn727078.aspx) Cmdlet 將範本匯出到您可以編輯的 .XML 檔，以將 "AllStaff" 群組和權限新增到現有的群組和權限，然後使用 [Import-AadrmTemplate](https://msdn.microsoft.com/library/azure/dn727077.aspx) Cmdlet 將此變更匯回到 Azure RMS 中。

> [!NOTE]
> 此 "AllStaff" 對等群組與 AD RMS 中的 ANYONE 組不完全相同："AllStaff" 群組包含您的 Azure 租用戶中的所有使用者，而 ANYONE 群組包含所有經過驗證的使用者 (有可能組織外部的使用者)。
> 
> 由於這兩個群組之間的差異，除了 "AllStaff" 群組以外，您可能還需要新增外部使用者。 目前不支援群組的外部電子郵件地址。


### 範例 Windows PowerShell 指令碼來識別包括 ANYONE 群組的 AD RMS 範本
本節包含範例指令碼，以協助您識別有 ANYONE 群組定義的 AD RMS 範本，如前一節所述。

**免責聲明：**這個範例指令碼不受任何 Microsoft 標準支援計劃或服務的支援。 這個範例指令碼是依現狀提供，不含任何種類的擔保。*

```
import-module adrmsadmin 

New-PSDrive -Name MyRmsAdmin -PsProvider AdRmsAdmin -Root https://localhost -Force 

$ListofTemplates=dir MyRmsAdmin:\RightsPolicyTemplate

foreach($Template in $ListofTemplates) 
{ 
                $templateID=$Template.id

                $rights = dir MyRmsAdmin:\RightsPolicyTemplate\$Templateid\userright

     $templateName=$Template.DefaultDisplayName 

        if ($rights.usergroupname -eq "anyone")

                         {
                           $templateName = $Template.defaultdisplayname

                           write-host "Template " -NoNewline

                           write-host -NoNewline $templateName -ForegroundColor Red

                           write-host " contains rights for " -NoNewline

                           write-host ANYONE  -ForegroundColor Red
                         }
 } 
Remove-PSDrive MyRmsAdmin -force
```


## 後續步驟
移至[階段 2-用戶端設定](migrate-from-ad-rms-phase2.md)。




<!--HONumber=Jun16_HO4-->


