---
# required metadata

title: 規劃及實作 Azure Rights Management 租用戶金鑰 | Azure RMS
description:
keywords:
author: cabailey
manager: mbaldwin
ms.date: 05/20/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: f0d33c5f-a6a6-44a1-bdec-5be1bc8e1e14

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: esaggese
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# 規劃及實作 Azure Rights Management 租用戶金鑰

*適用於︰Azure Rights Management、Office 365*

請使用本文件的資訊來協助您規劃和管理 Azure RMS 的 Rights Management (RMS) 租用戶金鑰。 例如，不是 Microsoft 管理租用戶金鑰 (預設值)，而是您可能想要管理您自己的租用戶金鑰，以遵循適用於貴組織的特定法規。  管理您自己的租用戶金鑰也稱為整合您自己的金鑰或 BYOK。

> [!NOTE]
> RMS 租用戶金鑰也稱為「伺服器授權人憑證 (SLC)」金鑰。 Azure RMS 為訂閱 Azure RMS 的每個組織維護一或多個金鑰。 只要組織內的 RMS 使用金鑰時 (例如使用者金鑰、電腦金鑰、文件加密金鑰)，便會以加密編譯的方式鏈結至您的 RMS 租用戶金鑰。

**概覽：** 使用下表做為您建議的租用戶金鑰拓撲的快速指南。 然後，如需詳細資訊，請使用其他文件。

如果您使用 Microsoft 管理的租用戶金鑰部署 Azure RMS，則稍後可以變更為 BYOK。 不過，您目前無法將 Azure RMS 租用戶金鑰從 BYOK 變更為 Microsoft 管理的租用戶金鑰。

|商務需求|建議的租用戶金鑰拓撲|
|------------------------|-----------------------------------|
|快速部署 Azure RMS 且不需要特殊硬體|由 Microsoft 管理|
|在 Exchange Online (含 Azure RMS) 中需要完整的 IRM 功能|由 Microsoft 管理|
|您的金鑰是由您建立，並以硬體安全性模組 (HSM) 加以保護|BYOK<br /><br />目前，此組態將在 Exchange Online 中導致精簡的 IRM 功能。 如需詳細資訊，請參閱 [BYOK 定價和限制](byok-price-restrictions.md)。|

## 選擇您的租用戶金鑰拓撲：由 Microsoft 管理 (預設) 或由您管理 (BYOK)
決定最適合您組織的租用戶金鑰拓撲。 依預設，Azure RMS 會產生您的租用戶金鑰，並管理租用戶金鑰生命週期的大多數作業。 這是系統管理負擔最小的最簡單選項。 在大多數情況下，您甚至無需知道您擁有租用戶金鑰。 您只要申請 Azure RMS，Microsoft 會為您處理金鑰管理程序的剩餘部分。

此外，您可能想要完整控制您的租用戶金鑰，包含建立您的租用戶金鑰，並在您的部署中保留主要複本。 這種案例通常稱為「整合您自己的金鑰 (BYOK)」。 使用此選項時會發生下列狀況：

1.  您會依據您的 IT 原則在部署上產生租用戶金鑰。

2.  您可從擁有的硬體安全模組 (HSM) 中，將租用戶金鑰安全地傳輸至 Microsoft 擁有及管理的 HSM。 在整個程序中，您的租用戶金鑰絕對不會離開硬體防護範圍。

3.  當您將租用戶金鑰傳輸到 Microsoft 時，Thales HSM 會持續保護該金鑰。 Microsoft 與 Thales 合作，確保您的租用戶金鑰無法從 Microsoft 的 HSM 擷取。

雖然是選用項，您也可能想要使用來自 Azure RMS 幾近即時的使用記錄，查看您的租用戶金鑰目前的實際使用方式與時間。

> [!NOTE]
> 作為其他防護措施，Azure RMS 對其在北美、EMEA (歐洲、中東和非洲) 和亞洲的資料中心使用不同的安全園地。 當您管理自己的租用戶金鑰時，它會連結到您 RMS 租用戶所登錄地區的安全園地。 例如，歐洲客戶的租用戶金鑰無法在北美或亞洲的資料中心使用。

## 租用戶金鑰生命週期
若您決定 Microsoft 應管理您的租用戶金鑰，Microsoft 會處理大多數金鑰生命週期作業。 不過，若您決定管理您的租用戶金鑰，則您必須負責許多金鑰生命週期作業和其他部分程序。

下列圖表顯示並比較這兩個選項。 第一個圖表顯示當 Microsoft 管理租用戶金鑰時，您在預設設定下承受的系統管理員負擔是如此的低。

![Azure RMS 租用戶金鑰週期 - 預設由 Microsoft 管理](../media/RMS_BYOK_cloud.png)

第二張圖顯示當您管理自己的租用戶金鑰時所需執行的其他步驟。

![Azure RMS 租用戶金鑰週期 - 預設由您 BYOK 管理](../media/RMS_BYOK_onprem.png)

若您決定讓 Microsoft 管理您的租用戶金鑰，則您在產生金鑰時無需採取進一步動作，並可直接前往[後續步驟](plan-implement-tenant-key.md#next-steps)。

若您決定自行管理租用戶金鑰，請閱讀下列各節以取得詳細資訊。

## 實作 Azure Rights Management 租用戶金鑰

若您已決定產生並管理您的租用戶金鑰，請使用本節的資訊和程序；整合您自己的金鑰 (BYOK) 案例：


> [!IMPORTANT]
> 若已開始使用 [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)] (服務已啟動)，且具執行 Office 2010 的使用者，請先連絡 Microsoft 客戶支援服務 (CSS)，再執行這些程序。 依據您的案例和需求，您仍可使用 BYOK，但會有一些限制或其他步驟。
> 
> 如果您的組織具有處理金鑰的特殊原則，亦請連絡 CSS。

### BYOK 的必要條件
請參閱下表以取得「整合您自己的金鑰 (BYOK)」的必要條件清單。

|需求|詳細資訊|
|---------------|--------------------|
|支援 Azure RMS 的訂用帳戶。|如需可用訂閱的詳細資訊，請參閱[支援 Azure RMS 的雲端訂閱](../get-started/requirements-subscriptions.md)。|
|您未使用個人版 RMS 或 Exchange Online。 或者，如果使用 Exchange Online，您了解並接受使用 BYOK 與此組態搭配的限制。|如需 BYOK 限制和目前限制的詳細資訊，請參閱 [BYOK 定價和限制](byok-price-restrictions.md)。<br /><br />**重要**：目前，BYOK 與 Exchange Online 不相容。|
|Thales HSM、智慧卡和支援軟體。<br /><br />**注意**：如果您使用軟體金鑰對硬體金鑰從 AD RMS 移轉到 Azure RMS，則 Thales 驅動程式的版本至少必須是 11.62 版。|您必須擁有 Thales 硬體安全模組的存取權並具備 Thales HSM 的基礎操作知識。 如需相容模組清單，或 HSM 的購買資訊 (如果您還沒有)，請參閱 [Thales 硬體安全模組](http://www.thales-esecurity.com/msrms/buy) (英文)。|
|若要透過網際網路傳輸您的租用戶金鑰，而非實體遞交到美國的雷德蒙德。 需要符合 3 個需求︰<br /><br />1：一部離線 x64 工作站，至少安裝 Windows 7 的 Windows 作業系統，及至少為 11.62 版的 Thales nShield 軟體。<br /><br />若此工作站執行 Windows 7，您必須 [安裝 Microsoft .NET Framework 4.5](http://go.microsoft.com/fwlink/?LinkId=225702)。<br /><br />2：連線至網際網路的工作站，至少有 Windows 7 的 Windows 作業系統。<br /><br />3：至少有 16 MB 可用空間的 USB 磁碟機或其他可攜式儲存裝置。|如果您去雷德蒙德並親自轉交您的租用戶金鑰，則無需符合這些必要條件。<br /><br />基於安全考量，我們建議您不要將第一個工作站連線至網路。 但無法透過設計程式完成這項工作。<br /><br />注意：在接下來的指示中，此第一個工作站稱為**中斷連線的工作站**。<br /><br />此外，若您的租用戶金鑰適用於生產網路，則我們建議您使用第二部個別工作站來下載工具組並上傳租用戶金鑰。 但為了測試用途，您可以使用第一部工作站。<br /><br />注意：在接下來的指示中，此第二部工作站稱為**連線網際網路的工作站**。|

您自己之租用戶金鑰的產生和使用程序，視您要透過網際網路還是親自交付而定：

-   **透過網際網路：** 這需要執行一些額外的設定步驟，例如下載及使用工具組和 Windows PowerShell Cmdlet。 不過，您不必親自光臨 Microsoft 機構就能傳輸您的租用戶金鑰。 可藉由下列方法維護安全性：

    -   您可從離線工作站產生租用戶金鑰，從而縮小攻擊面。

    -   租用戶金鑰是使用「金鑰互換 (KEK)」加密，將金鑰傳輸至 Azure RMS HSM 之前會持續加密該金鑰。 只有租用戶金鑰的加密版本會離開原始工作站。

    -   工具會在您的租用戶金鑰上設定屬性，以便將您的租用戶金鑰繫結至 Azure RMS 安全園地。 因此在 Azure RMS HSM 接收和解密租用戶金鑰後，只有這些 HSM 可使用該金鑰。 您的租用戶金鑰無法匯出。 此繫結是由 Thales HSM 強制執行。

    -   用來加密租用戶金鑰的「金鑰互換 (KEK)」是在 Azure RMS HSM 內部產生，而且無法匯出。 在該處強制執行該動作的 HSM 在 HSM 外部可能沒有全新的 KEK 版本。 此外，工具組包含了 Thales 的認證，證明 KEK 無法匯出，且是在 Thales 製造的正版 HSM 內部產生。

    -   工具組包含了 Thales 的認證，證明 Azure RMS 安全園地也是在 Thales 製造的正版 HSM 上產生。 這向您證明 Microsoft 正在使用正版硬體。

    -   Microsoft 在每個地理區使用不同的 KEK 與安全園地，如此可確保您的租用戶金鑰只能在加密該金鑰的地區資料中心內使用。 例如，歐洲客戶的租用戶金鑰無法在北美或亞洲的資料中心使用。

    > [!NOTE]
    > 您的租用戶金鑰可在不受信任的電腦和網路之間安全地移動，因為金鑰經過加密，並以存取控制層級權限保護，確保僅可在您 HSM 及 Microsoft 的 Azure RMS HSM 中使用。 您可使用工具組提供的指令碼來確認安全性措施，並從 Thales 閱讀這項工作的詳細資訊： [RMS 雲端中的硬體金鑰管理](https://www.thales-esecurity.com/knowledge-base/white-papers/hardware-key-management-in-the-rms-cloud)(英文)。

-   **親自轉交：** 您需要連絡 Microsoft 客戶支援服務 (CSS) 來安排 Azure RMS 金鑰轉交事宜。 您必須到美國華盛頓州雷德蒙德的 Microsoft 辦事處，將您的租用戶金鑰轉交給 Azure RMS 安全園地。

如需作法指示，選取要透過網際網路或親自產生和傳輸租用戶金鑰︰ 

- [透過網際網路](generate-tenant-key-internet.md)
- [親自轉交](generate-tenant-key-in-person.md)


## 後續步驟

既然您已規劃在需要時產生租用戶金鑰，請執行下列作業︰

1.  開始使用您的租用戶金鑰：

    -   若您尚未這麼做，則現在必須啟用 Rights Management，如此您的組織才能開始使用 RMS。 使用者會立即開始使用您的租用戶金鑰 (由 Microsoft 管理或由您自行管理)。

        如需啟用的詳細資訊，請參閱[啟用 Azure Rights Management](../deploy-use/activate-service.md)。

    -   如果您已啟用 Rights Management，然後決定管理您自己的租用戶金鑰，使用者會逐漸從舊租用戶金鑰轉移至新租用戶金鑰，而此交錯轉移可能會耗費數週才能完成。 授權的使用者仍可存取舊租用戶金鑰所保護的文件和檔案。

2.  請考慮使用使用記錄，它會記錄 RMS 執行的每筆交易。

    如果您決定管理您自己的租用戶金鑰，記錄將包含您租用戶金鑰的相關使用資訊。 請參閱 Excel 中顯示的下列記錄檔範例，其中 **Decrypt** 和 **SignDigest** 要求類型會顯示正在使用的租用戶金鑰。

    ![使用租用戶金鑰的 Excel 記錄檔](../media/RMS_Logging.gif)

    如需使用記錄的詳細資訊，請參閱[記錄和分析 Azure Rights Management 使用情況](../deploy-use/log-analyze-usage.md)。

3.  維護您的租用戶金鑰。

    如需詳細資訊，請參閱 [Azure Rights Management 租用戶金鑰的作業](../deploy-use/operations-tenant-key.md)。



<!--HONumber=May16_HO3-->


