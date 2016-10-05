---
title: "從 AD RMS 移轉至 Azure Information Protection | Azure Information Protection"
description: "將 Active Directory Rights Management Services (AD RMS) 部署移轉至 Azure Information Protection 的指示。 移轉之後，使用者仍然可以存取您組織使用 AD RMS 保護的文件及電子郵件訊息，但以後會使用 Azure Information Protection 保護內容。"
author: cabailey
manager: mbaldwin
ms.date: 09/25/2016
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 828cf1f7-d0e7-4edf-8525-91896dbe3172
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: bb240b92a86bfc37685556ba2ce71b9eea56ae88
ms.openlocfilehash: c3e926b48dfc66da71e4e3f16f9359b3cb8322c6


---

# 從 AD RMS 移轉至 Azure Information Protection

>*適用於︰Active Directory Rights Management Services、Azure Information Protection、Office 365*

使用下列一組指令來將您的 Active Directory Rights Management Services (AD RMS) 部署移轉至 Azure Information Protection。 移轉之後，使用者仍然可以存取您組織使用 AD RMS 保護的文件及電子郵件訊息，但以後會使用 Azure Information Protection 的 Azure Rights Management Service 保護內容。

不確定您的組織是否適合 AD RMS 移轉？

-   如需 Azure Information Protection 簡介，請參閱 [What is Azure Azure Information Protection?](../understand-explore/what-is-information-protection.md) (什麼是 Azure Information Protection？)。

-   如需 Azure Information Protection 和 AD RMS 的比較，請參閱[比較 Azure Information Protection 與 AD RMS](../understand-explore/compare-azure-rms-ad-rms.md)。

## 從 AD RMS 移轉至 Azure Information Protection 的必要條件
請確定您符合下列必要條件且了解所有限制，再開始移轉至 Azure Information Protection。

- **支援的 RMS 部署：**
    
    - 下列的 AD RMS 版本皆支援移轉至 Azure Information Protection：
    
        - Windows Server 2008 R2 (x64)
        
        - Windows Server 2012 (x64)
        
        - Windows Server 2012 R2 (x64)
        
    - 密碼編譯模式 2：

        - 必須先在密碼編譯模式 2 中執行 AD RMS 伺服器及用戶端，才能開始移轉至 Azure Information Protection。
        
        雖然目前的伺服器授權人憑證 (SLC) 金鑰必須使用密碼編譯模式 2，但 Azure Information Protection 仍支援設定使用密碼編譯模式 1 的先前金鑰。 如需密碼編譯模式以及如何移至密碼編譯模式 2 的詳細資訊，請參閱 [AD RMS 密碼編譯模式](https://technet.microsoft.com/library/hh867439(v=ws.10).aspx)。
        
    - 支援所有有效的 AD RMS 拓撲：
    
        - 單一樹系、單一 RMS 叢集
        
        - 單一樹系、多個僅授權 RMS 叢集
        
        - 多個樹系、多個 RMS 叢集
        
    注意：多個 RMS 叢集預設會移轉至單一 Azure Information Protection 租用戶。 如果您想要個別的 Azure Information Protection 租用戶，則必須將它們視為不同的移轉。 一個 RMS 叢集的金鑰不能匯入至多個 Azure Information Protection 租用戶。

- **執行 Azure Information Protection ，包括 Azure Information Protection 租用戶 (未啟動) 的所有需求︰**

    請參閱 [Azure Information Protection 的需求](../get-started/requirements-azure-rms.md)。

    雖然您必須有 Azure Information Protection 租用戶，才能從 AD RMS 進行移轉，但是建議您在移轉之前，先不要啟動 Rights Management Service。 從 AD RMS 匯出金鑰和範本並將它們匯入至 Azure Information Protection 之後，移轉程序會包含此步驟。 但若已啟用 Rights Management Service，仍然可以從 AD RMS 移轉。


- **準備 Azure Information Protection：**

    - 內部部署目錄與 Azure Active Directory 之間的目錄同步作業

    - Azure Active Directory 中擁有郵件功能的群組

    請參閱[準備 Azure Information Protection](prepare.md)。


- **如果您曾使用 Exchange Server 的資訊版權管理 (IRM) 功能** (如傳輸規則和 Outlook Web Access) 或 SharePoint Server 來搭配 AD RMS：

    - 規劃 IRM 無法在這些伺服器上使用的一段短期間
 
    移轉之後，您可以繼續使用這些伺服器上的 IRM 與 Azure Rights Management Service。 不過，其中一個移轉步驟是暫時停用 IRM 服務、安裝和設定連接器、重新設定伺服器，然後重新啟用 IRM。

    這是移轉程序期間唯一發生的服務中斷。

- **若想要使用 HSM 保護的金鑰管理您自己的 Azure Information Protection 租用戶金鑰**：

    - 此選用的設定需要 Azure 金鑰保存庫及 Azure 訂用帳戶，其中後者需支援金鑰保存庫及 HSM 保護的金鑰。 如需詳細資訊，請參閱 [Azure 金鑰保存庫定價頁面](https://azure.microsoft.com/en-us/pricing/details/key-vault/)。 


限制：

-   雖然移轉程序支援將伺服器授權憑證 (SLC) 金鑰來移轉至 Azure Information Protection 的硬體安全性模組 (HSM)，但是 Exchange Online 目前不支援 Azure Information Protection 所用的 Rights Management Service 組態。 如果在移轉至 Azure Information Protection 之後，想要完整的 IRM 功能與 Exchange Online，您的 Azure Information Protection 租用戶金鑰必須[由 Microsoft 管理](../plan-design/plan-implement-tenant-key.md#choose-your-tenant-key-topology-managed-by-microsoft-the-default-or-managed-by-you-byok)。 或者，自行管理 Azure Information Protection 租用戶 (BYOK)，在 Exchange Online 中執行功能精簡的 IRM。 如需搭配使用 Exchange Online 與 Azure Rights Management Service 的詳細資訊，請參閱[步驟 6。設定 Exchange Online 的 IRM 整合](migrate-from-ad-rms-phase3.md#step-6-configure-irm-integration-for-exchange-online)。

-   如有軟體和用戶端不受 Azure Information Protection 使用的 Rights Management Service 支援，它們就不能保護或取用受 Azure Rights Management 保護的內容。 請務必檢查 [Azure Rights Management 的需求](../get-started/requirements-azure-rms.md)文件中的支援的應用程式和用戶端節。

-   如果您將內部部署金鑰匯入至 Azure Information Protection，作為保存的金鑰 (您未將 TPD 設定為在匯入程序期間作用)，而且您批次移轉使用者，以進行分段移轉，則由移轉的使用者所新保護的內容無法供仍留在 AD RMS 的使用者存取。 在此案例中，請盡可能保持簡短的移轉時間，並以邏輯批次方式移轉使用者，以便如果他們彼此合作，可以一起移轉它們。

    當您將 TPD 設定為在匯入期間作用中時，這項限制不適用，因為所有使用者將使用相同金鑰來保護內容。 我們建議此組態，因為它可讓您獨立並依自己的步調移轉所有使用者。

-   如果您與外部合作夥伴合作 (如藉由使用信任的使用者網域或同盟)，他們也必須在您移轉至 Azure Information Protection 時同時移轉，亦或是在您移轉後儘快移轉。 若要繼續存取組織先前使用 Azure Information Protection 保護的內容，他們必須進行用戶端組態變更 (類似您所做的變更)，並包括在這份文件內。

    由於合作夥伴之間的組態可能不盡相同，因此本文件不探討本次重新組態的確切指示。 如需說明，請[連絡 Microsoft 支援服務](../get-started/information-support.md#support-options-and-community-resources)。

## 從 AD RMS 移轉至 Azure Information Protection 的步驟概觀


移轉步驟可分成在不同時間完成的 4 個階段，並由不同的系統管理員執行。

[**階段 1︰AD RMS 的伺服器端設定**](migrate-from-ad-rms-phase1.md)

- **步驟 1：下載 Azure RMS Management 系統管理工具**

    移轉程序需要您從與 Azure RMS Management 系統管理工具一起安裝的 Azure RMS 模組中，執行一或多個 Windows PowerShell Cmdlet。

- **步驟 2： 從 AD RMS 匯出組態資料，並將它匯入至 Azure Information Protection**

    您可以將組態資料 (金鑰、範本、URL) 從 AD RMS 匯出為 XML 檔案，然後使用 Import-AadrmTpd Windows PowerShell Cmdlet 將該檔案從 Azure Information Protection 上傳至 Azure Rights Management Service。 可能還需要額外的步驟 (視 AD RMS 金鑰組態而定)：

    - **軟體保護的金鑰移轉至軟體保護的金鑰**：

        AD RMS 中集中管理的密碼金鑰到 Microsoft 管理的 Azure Information Protection 租用戶金鑰。 這是最簡單的移轉路徑，而且不需要任何額外的步驟。

    - **HSM 保護的金鑰移轉至 HSM 保護的金鑰**：

        HSM for AD RMS儲存的金鑰到客戶管理的 Azure Information Protection 租用戶金鑰 (「自備金鑰」(BYOK) 案例)。 這需要額外的步驟，才能將金鑰從內部部署 Thales HSM 傳輸至 Azure 金鑰保存庫，並授權 Azure Rights Management Service 使用此金鑰。 您現有的 HSM 保護金鑰必須是模組保護的；Rights Management 服務不支援 OCS 保護的金鑰。

    - **軟體保護的金鑰移轉至 HSM 保護的金鑰**：

        AD RMS 中集中管理的密碼金鑰到客戶管理的 Azure Information Protection 租用戶金鑰 (「自備金鑰」(BYOK) 案例)。 這需要最多的組態，因為您必須先擷取您的軟體金鑰並將其匯入內部部署 HSM，然後再執行其他步驟，將金鑰從內部部署 Thales HSM 傳輸至 Azure 金鑰保存庫 HSM，並授權 Azure Rights Management Service 使用金鑰保存庫儲存金鑰。

- **步驟 3： 啟用 Azure Information Protection 租用戶**

    可能的話，請在匯入程序之後執行此步驟，而不是在之前執行。

- **步驟 4： 設定匯入的範本**

    匯入權限原則範本時，會封存其狀態。 如果您想要使用者能夠看到並使用它們，則必須在 Azure 傳統入口網站中將範本狀態變更為已發佈。


[**階段 2：用戶端設定**](migrate-from-ad-rms-phase2.md)


- **步驟 5：重新設定用戶端使用 Azure Information Protection**

    現有的 Windows 電腦必須重新設定為使用 Azure Information Protection 服務，而不是 AD RMS。 如果您在執行 AD RMS 時與您組織中的電腦以及合作夥伴組織中的電腦共同作業，則此步驟適用於這些電腦。

    此外，如果您已部署[行動裝置延伸模組](http://technet.microsoft.com/library/dn673574.aspx)來支援 iOS 行動電話和 iPad、Android 行動電話和平板電腦、Windows 行動電話及 Mac 電腦，必須移除 DNS 中重新導向這些用戶端以使用 AD RMS 的 SRV 記錄。


[**階段 3︰支援服務設定**](migrate-from-ad-rms-phase3.md)


- **步驟 6：設定 IRM 與 Exchange Online 整合**

    如果您想要使用 Exchange Online 與 Azure Information Protection 的 Azure Rights Management Service，此為必要步驟。


- **步驟 7：部署 RMS 連接器**

    如果您想要使用下列任何內部部署服務與 Azure Rights Management Service 來保護 Office 文件和電子郵件，此為必要步驟︰

    - Exchange Server (如傳輸規則和 Outlook Web Access)

    - SharePoint Server

    - 執行檔案分類基礎結構 (FCI) 的 Windows Server


[**階段 4︰移轉後工作**](migrate-from-ad-rms-phase4.md )

- **步驟 8. 解除委任 AD RMS**

    確認所有用戶端都使用 Azure Information Protection 而且不再存取 AD RMS 伺服器時，即可解除委任 AD RMS 部署。


- **步驟 9：重設 Azure Information Protection 租用戶金鑰**

    這雖然是選用步驟，但若步驟 2 選擇了 Microsoft 管理的 Azure Information Protection 租用戶金鑰拓撲，建議您使用此步驟。 若選擇了客戶管理 (BYOK) 的 Azure Information Protection 租用戶金鑰拓撲，則此步驟不適用。


## 後續步驟
若要啟動移轉，請移至[階段 1-伺服器端設定](migrate-from-ad-rms-phase1.md)。




<!--HONumber=Sep16_HO4-->


