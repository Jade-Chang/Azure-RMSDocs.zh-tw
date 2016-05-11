---
# required metadata

title: 使用者如何申請個人版 RMS | Azure RMS
description:
keywords:
author: cabailey
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: a60731bd-f78d-4f00-bb3e-354637b312ab

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: esaggese
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# 使用者如何申請個人版 RMS
若要註冊此免費帳戶，使用者可造訪 [Microsoft Rights Management 頁面](https://portal.aadrm.com/)來申請註冊，並提供工作或學校電子郵件地址。 

使用者將會被導向至這個註冊頁面的最常見方式是，他們收到包含註冊方式說明之受保護附件的電子郵件訊息。 他們會收到 Microsoft 的電子郵件回應，然後即可輸入詳細資料建立其帳戶以完成註冊程序。 當他們從 Microsoft 取得電子郵件確認時，此最終電子郵件訊息會傳送至一個頁面，可以在其中下載不同裝置之共用應用程式，以及使用者指南的連結。

## 若要申請個人版 RMS

1.  使用 Windows 或 Mac 電腦時，請移至 [Microsoft Rights Management 頁面](https://portal.aadrm.com)。

2.  鍵入您用於組織的電子郵件地址，例如 janetm@contoso.com 或 p.dover@fabrikam.com。

    > [!IMPORTANT]
    > 不支援個人電子郵件帳戶，因此請勿輸入 Microsoft 帳戶 (先前稱為 Microsoft Live ID 帳戶)，或您在家中可能使用的網際網路提供者的其他個人帳戶。

3.  按一下 [開始使用] 。

    Microsoft 會使用您的電子郵件地址來檢查您的組織是否已具有[包含 Azure RMS 的付費定用帳戶](../get-started/requirements-subscriptions.md)。 如果是這種情況，您就不需要個人版 RMS，即可立即登入並取消個人版 RMS 的自助註冊。 如果找不到 Azure RMS 的付費訂用帳戶，您將會繼續進行下一個步驟。

4.  等候確認電子郵件訊息傳送至您所提供的位址。 它將來自 Microsoft (DoNotReply@microsoft.com) 且主旨為 Microsoft RMS。

5.  收到電子郵件時，請按一下指示中的連結來完成申請程序。

6.  此連結會將您帶到新的 [Microsoft Rights Management]  頁面，可讓您在頁面中提供您帳戶的詳細資料。 輸入您的名字和姓氏、輸入並確認您選擇的密碼、從下拉式清單選取您的國家/地區 (如果為列出您的國家/地區，則選取最接近的國家/地區)，然後按一下 [建立] 。

7.  等候來自 Microsoft 的另一則電子郵件訊息，該訊息現在會確認您的帳戶已準備好使用。

8.  接收電子郵件時，請按一下連結登入並詳閱指示以下載和安裝共用應用程式，或按一下 [說明] 連結來閱讀共用應用程式使用者指南。

現在已建立您的帳戶，您可以準備好開始保護檔案和讀取其他人已保護的檔案。 系統提示您登入以保護或讀取受保護檔案時，請輸入您用來建立個人版 RMS 帳戶的電子郵件地址和密碼。

## 註冊程序的技術概觀
個人版 RMS 會使用自助式註冊程序，其他使用 Microsoft 雲端架構技術驗證使用者的服務也會使用此程序。

當使用者註冊個人版 RMS 且其組織沒有 Office 365 訂閱或 Azure 訂閱，使得 Azure 中沒有目錄可驗證使用者時，便會在背景啟用下列程序：

1.  當組織的第一個使用者要求個人版 RMS 訂閱時，會檢查其電子郵件地址中提供的網域名稱，查看其是否已與 Azure 租用戶相關聯。 如果沒有任何現有的租用戶，會自動為組織建立包含第一個使用者之帳戶的新租用戶與 Azure 目錄。 與 Azure 的付費訂用帳戶不同，第一個帳戶不是全域系統管理員，而是標準使用者。 新帳戶使用的是使用者提供的電子郵件地址及密碼。

    > [!NOTE]
    > 有些網域名稱無法用來建立目錄，因此無法用於個人版 RMS。 可從此「JavaScript 物件標記法」檔案檢視封鎖的網域名稱清單： [http://portal.aadrm.com/content/blocked_domains.json](http://portal.aadrm.com/content/blocked_domains.json)

    如果找到現有的租用戶，系統會檢查它以查看是否已經有 Azure RMS 的訂用帳戶。 找不到訂用帳戶時，可以新增免費個人版 RMS 訂用帳戶。

2.  此個人版 RMS 訂用帳戶可授與組織。 使用者現在可由 Azure 驗證，然後可以保護檔案，並讀取其他人已保護的檔案。 若要保護和讀取受保護檔案，使用者必須具有已啟用 RMS 的應用程式，例如安裝免費的 [Rights Management 共用應用程式](../rms-client/sharing-app-windows.md)。

3.  當相同組織的第二個使用者要求個人版 RMS 訂閱時，可使用組織的個人版 RMS 訂閱，將新使用者帳戶新增至先前建立的 Azure 目錄。 第二個使用者可執行第一名使用者可執行的每個動作 (保護檔案和讀取受保護檔案)，此外，這兩名使用者現在可安全且更輕易地共同作業，因為他們可將預設範本快速套用至檔案，對其組織之 Azure 目錄的帳戶存取設定限制。

4.  相同組織的使用者後續可遵循相同的模式，在新使用者登入時將使用者帳戶新增至組織的 Azure 目錄。 新增至目錄的帳戶愈多，就有愈多使用者可與同事和合作夥伴安全地共同作業，並更輕易地防止未經授權 (沒有存取權) 的人員讀取他們的檔案。

在整個程序中，組織完全無需付費，IT 部門也無需執行任何工作。 不過，IT 部門可選擇執行下列其中一項作業：

-   管理帳戶及登入程序：IT 系統管理員可取得在 Azure 中自動建立之目錄與帳戶的擁有權。 他們可接著實作目錄整合方案 (例如密碼同步和單一登入) 來管理帳戶。 或者，他們也可防止使用者建立帳戶或註冊個人版 RMS。

    如需詳細資訊，請參閱[系統管理員如何控制個人版 RMS 建立的帳戶](rms-for-individuals-take-control.md)。

-   管理 Rights Management：IT 系統管理員可將組織的個人版 RMS 訂閱轉換為包含 Azure Rights Management 的付費訂閱。 當他們這麼做時，會保留現有的 Azure 目錄和帳戶，供仍在使用個人版 RMS 的現有使用者進行無縫轉換。 仍將遵循相同的原則保護其先前保護的任何檔案，且其授予檔案使用權限的人員仍可以相同的方式使用檔案。

    採取此類行動時，您的的組織可將 Rights Management 整合至其工作流程、服務和資料存放區而從中受益。 此外，您現在可管理 Rights Management，因為您擁有您組織 Azure Rights Management 租用戶金鑰的控制權。 您現在可執行下列動作：

    -   設定 Exchange 和 SharePoint 以支援 Azure Rights Management，即使它們正在執行內部部署也是如此。 Exchange 和 SharePoint 原生支援線上服務，並受內部部署伺服器的連接器支援。 如需詳細資訊，請參閱下列內容：

        -   [Office 365：用戶端和線上服務的設定](../deploy-use/configure-office365.md)的 Exchange Online 和 SharePoint Online 章節

        -   [部署 Azure Rights Management 連接器](../deploy-use/deploy-rms-connector.md)

    -   在公司擁有的資料上執行 e-discovery，必要時解密使用 Rights Management 所保護的檔案。 如需詳細資訊，請參閱[設定 Azure Rights Management 和探索服務或資料復原的進階使用者](../deploy-use/configure-super-users.md)。

    -   記錄組織中所使用 Rights Management 的所有活動。 這是極強大的功能，因為您不僅可監視正在保護哪些檔案，及監視正在成功存取那些受保護檔案的人員，亦可識別未授權人員正在嘗試存取受保護檔案的可疑行為。 如需詳細資訊，請參閱[記錄和分析 Azure Rights Management 使用情況](../deploy-use/log-analyze-usage.md)。

    -   如果您的 [Azure RMS 訂用帳戶](https://technet.microsoft.com/dn858608)支援這些功能，請提供使用者此功能以追蹤及撤銷其受保護文件。 如需詳細資訊，請參閱 [RMS 共用應用程式使用者指南](../rms-client/sharing-app-user-guide.md)中的[追蹤及撤銷您的檔案](../rms-client/sharing-app-track-revoke.md)。

    -   實作「整合您自己的金鑰方案 (BYOK)」，根據您的 IT 原則，在內部部署中產生 Azure Rights Management 的租用戶金鑰，並使用「硬體安全模組 (HSM)」安全地傳輸到 Microsoft。 如需詳細資訊，請參閱[規劃及實作 Azure Rights Management 租用戶金鑰](../plan-design/plan-implement-tenant-key.md)。


## 後續步驟
請參閱[系統管理員如何控制個人版 RMS 建立的帳戶](rms-for-individuals-take-control.md)。




<!--HONumber=Apr16_HO3-->


