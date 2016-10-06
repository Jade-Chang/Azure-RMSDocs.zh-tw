---
title: "使用者如何註冊個人版 RMS | Azure Information Protection"
description: "適用於此免費帳戶的註冊指示，以及此程序如何運作的技術資訊。"
author: cabailey
manager: mbaldwin
ms.date: 09/25/2016
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: a60731bd-f78d-4f00-bb3e-354637b312ab
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 2fd29eb6dec94535d0358fe0a2d9c9285fcd7cd1
ms.openlocfilehash: 362ea0d002e25c830c9e50ac7f1956f1e9ea8bb7


---

# 使用者如何申請個人版 RMS

>*適用於：Azure Information Protection*

若要註冊此免費帳戶，請前往 [Microsoft Rights Management 頁面](https://portal.office.com/signup?sku=rms&ru=https%3A%2F%2Fportal.azurerms.com%2F%23%2Fdownload)提出申請，並請提供您的工作電子郵件地址。 常見的方式是將您從您收到內含受保護附件的電子郵件導向到此註冊頁面，而受保護的附件會提供如何註冊的指示。 您會收到 Microsoft 的電子郵件回應，然後即可輸入詳細資料建立您的帳戶以完成註冊程序。 完成此動作時，頁面中會顯示所提供不同裝置之應用程式的下載位置，並會提供使用者指南的連結，以及原生支援 Rights Management 保護的最新應用程式清單。 

## 若要申請個人版 RMS

1.  若是使用 Windows 或 Mac 電腦或行動裝置，請前往 [Microsoft Azure Rights Management 頁面](https://portal.office.com/signup?sku=rms&ru=https%3A%2F%2Fportal.azurerms.com%2F%23%2Fdownload)。

2.  鍵入您用於組織的電子郵件地址，例如 **janetm@contoso.com** 或 **p.dover@fabrikam.com**。

    > [!IMPORTANT]
    > 不支援個人電子郵件帳戶，因此請勿輸入 Microsoft 帳戶 (先前稱為 Microsoft Live ID 帳戶)，或您在家中可能使用的網際網路提供者的其他個人帳戶。

3.  按一下 [註冊]。

    Microsoft 會使用您的電子郵件地址來檢查您的組織是否已具有[包含 Azure RMS 的付費定用帳戶](../get-started/requirements-subscriptions.md)。 如果是這種情況，您就不需要個人版 RMS，即可立即登入並取消個人版 RMS 的自助註冊。 如果找不到 Azure RMS 的付費訂用帳戶，您將會繼續進行下一個步驟。

4.  等候確認電子郵件訊息傳送至您所提供的位址。 電子郵件會從 Office 365 小組 (support@email.microsoftonline.com) 發出，主旨為 **完成註冊 Microsoft Azure Rights Management**。

5.  當您收到此電子郵件時，請按一下 [沒錯，這是我] 確認您的電子郵件地址，以完成註冊程序。

6.  接著會隨即顯示 [最後提醒事項] 頁面為您提供帳戶的詳細資料。 請輸入您的名字、姓氏，再輸入您選擇的密碼並加以確認，然後按一下 [開始]。

7. 建立您的帳戶時，會顯示新的 Microsoft Rights Management 頁面讓您下載及安裝所提供的應用程式；您也可以按一下 [[更多資訊](../rms-client/sharing-app-user-guide.md)] 連結，閱讀所提供的應用程式使用者指南。

現在已建立您的帳戶，您可以準備好開始保護檔案和讀取其他人已保護的檔案。 當提示您必須登入才能保護或讀取受保護的檔案時，請輸入您建立個人版 RMS 帳戶時所使用的電子郵件地址及密碼。

## 註冊程序的技術概觀
個人版 RMS 會使用自助式註冊程序，其他使用 Microsoft 雲端架構技術驗證使用者的服務也會使用此程序。

當使用者註冊個人版 RMS 且其組織沒有 Office 365 訂閱或 Azure 訂閱，使得 Azure 中沒有目錄可驗證使用者時，便會在背景啟用下列程序：

1.  當組織的第一個使用者要求個人版 RMS 訂閱時，會檢查其電子郵件地址中提供的網域名稱，查看其是否已與 Azure 租用戶相關聯。 如果沒有任何現有的租用戶，會自動為組織建立包含第一個使用者之帳戶的新租用戶與 Azure 目錄。 與 Azure 的付費訂用帳戶不同，第一個帳戶不是全域系統管理員，而是標準使用者。 新帳戶使用的是使用者提供的電子郵件地址及密碼。

    > [!NOTE]
    > 有些網域名稱無法用來建立目錄，因此無法用於個人版 RMS。

    如果找到現有的租用戶，系統會檢查它以查看是否已經有 Azure RMS 的訂用帳戶。 找不到訂用帳戶時，可以新增免費個人版 RMS 訂用帳戶。

2.  此個人版 RMS 訂用帳戶可授與組織。 使用者現在可由 Azure 驗證，然後可以保護檔案，並讀取其他人已保護的檔案。 若要保護和讀取受保護檔案，使用者必須具有已啟用 RMS 的應用程式，例如安裝免費的 [Rights Management 共用應用程式](../rms-client/sharing-app-windows.md)。

3.  當相同組織的第二個使用者要求個人版 RMS 訂閱時，可使用組織的個人版 RMS 訂閱，將新使用者帳戶新增至先前建立的 Azure 目錄。 第二個使用者可執行第一名使用者可執行的每個動作 (保護檔案和讀取受保護檔案)，此外，這兩名使用者現在可安全且更輕易地共同作業，因為他們可將預設範本快速套用至檔案，對其組織之 Azure 目錄的帳戶存取設定限制。

4.  相同組織的使用者後續可遵循相同的模式，在新使用者登入時將使用者帳戶新增至組織的 Azure 目錄。 新增至目錄的帳戶愈多，就有愈多使用者可與同事和合作夥伴安全地共同作業，並更輕易地防止未經授權 (沒有存取權) 的人員讀取他們的檔案。

在整個程序中，組織完全無需付費，IT 部門也無需執行任何工作。 不過，IT 部門可選擇執行下列其中一項作業：

-   **管理帳戶及登入程序**：IT 系統管理員可取得在 Azure 中自動建立之目錄與帳戶的擁有權。 他們可接著實作目錄整合方案 (例如密碼同步和單一登入) 來管理帳戶。 或者，他們也可防止使用者建立帳戶或註冊個人版 RMS。

    如需詳細資訊，請參閱[系統管理員如何控制個人版 RMS 建立的帳戶](rms-for-individuals-take-control.md)。

-   **管理 Rights Management**：IT 系統管理員可將組織的個人版 RMS 訂閱轉換為包含 Azure Rights Management 的付費訂閱。 當他們這麼做時，會保留現有的 Azure 目錄和帳戶，供仍在使用個人版 RMS 的現有使用者進行無縫轉換。 仍將遵循相同的原則保護其先前保護的任何檔案，且其授予檔案使用權限的人員仍可以相同的方式使用檔案。

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





<!--HONumber=Sep16_HO4-->


