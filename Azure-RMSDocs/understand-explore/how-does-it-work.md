---
title: "Azure RMS 如何運作 | Azure RMS"
description: "了解 Azure RMS 運作方式的一大要點就是 Rights Management 服務 (和 Microsoft) 不會在資訊保護程序中查看或儲存您的資料。 您所保護的資訊永遠不會傳送至或儲存在 Azure 中，除非您明確地將它儲存在 Azure 中，或使用將它儲存在 Azure 中的另一項雲端服務。 Azure RMS 只是讓授權使用者和服務以外的任何人都無法讀取文件中的資料。"
author: cabailey
manager: mbaldwin
ms.date: 06/02/2016
ms.topic: article
ms.prod: 
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: ed6c964e-4701-4663-a816-7c48cbcaf619
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 26b043f1f9e7a1e0cd00c2f31c28f7d6685f0232
ms.openlocfilehash: 527af70532f390330fdb65bc27b04bb366289748


---


# Azure RMS 如何運作？ 背後原理

>*適用於︰Azure Rights Management、Office 365*

了解 Azure RMS 運作方式的一大要點就是 Rights Management 服務 (和 Microsoft) 不會在資訊保護程序中查看或儲存您的資料。 您所保護的資訊永遠不會傳送至或儲存在 Azure 中，除非您明確地將它儲存在 Azure 中，或使用將它儲存在 Azure 中的另一項雲端服務。 Azure RMS 只是讓授權使用者和服務以外的任何人都無法讀取文件中的資料：

-   資料會在應用程式層級加密，並包含一個原則來定義該文件的授權使用。

-   當合法使用者使用受保護的文件或由已授權的服務進行處理時，文件中的資料會解密並強制執行原則中定義的權限。

在高層級，您可以在下圖中看到這個程序的運作方式。 包含密碼公式的文件會受到保護，並由授權的使用者或服務成功開啟。 此文件受內容金鑰 (此圖中的綠色金鑰) 保護。 每份文件的內容金鑰都是唯一的並放置在檔案標頭中，由 RMS 租用戶根金鑰 (此圖中的紅色金鑰) 所保護。 租用戶金鑰可以由 Microsoft 產生和管理，您也可以產生和管理自己的租用戶金鑰。

在 Azure RMS 進行加密和解密、授權以及強制執行限制的保護程序中，密碼公式永遠不會傳送至 Azure。

![Azure RMS 如何保護檔案](../media/AzRMS_SecretColaFormula_final.png)

如需詳細的情況說明，請參閱本文中的 [Azure RMS 運作方式的逐步解說：第一次使用、內容保護、內容取用](#walkthrough-of-how-azure-rms-works-first-use-content-protection-content-consumption) 一節。

如需 Azure RMS 使用的演算法和金鑰長度技術詳細資訊，請參閱下一節。

## Azure RMS 使用的密碼編譯控制項：演算法和金鑰長度
即使您本身不需要知道 RMS 運作方式，但系統可能會詢問您有關它所使用的密碼編譯控制項，以確定安全性保護符合業界標準。


|密碼編譯控制項|在 Azure RMS 中使用|
|-|-|
|演算法：AES<br /><br />金鑰長度：128 位元和 256 位元 [[1]](#footnote-1)|文件保護|
|演算法：RSA<br /><br />金鑰長度：2048 位元|金鑰保護|
|SHA-256|憑證簽署|

###### 註腳 1 

當檔案的副檔名為 .ppdf，或檔案為受保護的文字檔或影像檔時 (例如 .ptxt 或 .pjpg)，Rights Management 共用應用程式會使用 256 位元進行一般保護與原生保護。

如何儲存和保護加密編譯金鑰：

- 對於 Azure RMS 保護的每個文件或電子郵件，Azure RMS 會建立單一 AES 金鑰 (「內容金鑰」)，該金鑰會內嵌至文件，在文件的各個版本中持續存在。 

- 內容金鑰是使用組織的 RSA 金鑰 (「Azure RMS 租用戶金鑰」) 保護，做為文件原則的一部分，原則也會由文件的作者簽署。 這個租用戶金鑰通用於受到 Azure RMS 為組織保護的所有文件和電子郵件，當組織使用由客戶管理 (稱為「整合您自己的金鑰」，或 BYOK) 的租用戶金鑰時，這個金鑰只能由 Azure RMS 管理員變更。 

    這個租用戶金鑰是在 Microsoft 的線上服務、高度受控制的環境以及嚴密監控之下受到保護。 當您使用由客戶管理的租用戶金鑰 (BYOK)，此安全性會藉由在每個 Azure 區域中使用高階硬體安全性模組 (HSMs) 的陣列，而獲得增強，在任何情況下都不需要擷取、匯出或共用金鑰。 如需租用戶金鑰和 BYOK 的詳細資訊，請參閱[規劃及實作 Azure Rights Management 租用戶金鑰](../plan-design/plan-implement-tenant-key.md)。

- 傳送給 Windows 裝置的授權和憑證是受到用戶端的裝置私密金鑰保護，這個私密金鑰是在使用者第一次於裝置上使用 Azure RMS 時建立的。 而這個私密金鑰則是由用戶端上的 DPAPI 保護，它會使用從使用者的密碼衍生的金鑰來保護密碼。 在行動裝置上，金鑰只會使用一次，因為它們不會儲存在用戶端上，所以不需要在裝置上保護這些金鑰。 



## Azure RMS 運作方式的逐步解說：第一次使用、內容保護、內容取用
若要進一步了解 Azure RMS 運作方式，讓我們在 [啟動 Azure RMS 服務](../deploy-use/activate-service.md) 之後，以及當使用者第一次在其 Windows 電腦上使用 RMS (有時候也稱為 **初始化使用者環境** 或啟動的程序)、 **保護內容** (文件或電子郵件)，然後 **取用**  (開啟並使用) 其他人所保護的內容時，逐步執行一般流程。

初始化使用者環境之後，該使用者可接著保護文件或取用該電腦上受保護的文件。

> [!NOTE]
> 如果此使用者移到另一部 Windows 電腦，或另一位使用者使用同一部 Windows 電腦，則會重複進行初始化程序。

### 初始化使用者環境
必須在裝置上備妥使用者環境，使用者才能保護內容或取用 Windows 電腦上受保護的內容。 這是一次性程序，而且當使用者嘗試保護或取用受保護的內容時，不需要使用者介入即自動發生：

![RMS 用戶端啟用 - 步驟 1](../media/AzRMS.png)

**步驟 1 中的情況**：電腦上的 RMS 用戶端會先連接至 Azure RMS，並使用 Azure Active Directory 帳戶來驗證使用者。

當使用者的帳戶與 Azure Active Directory 同盟時，系統會自動執行此驗證，而且不會提示使用者輸入認證。

![RMS 用戶端啟用 - 步驟 2](../media/AzRMS_useractivation2.png)

**步驟 2 中的情況**：使用者經過驗證之後，連線會自動重新導向組織的 RMS 租用戶，以發出可讓使用者向 Azure RMS 進行驗證的憑證，進而使用受保護的內容以及離線保護內容。

在 Azure RMS 中會儲存一份使用者的憑證，如果使用者移到另一個裝置，即可使用相同的金鑰建立憑證。

### 內容保護
當使用者保護文件時，RMS 用戶端會對未受保護的文件採取下列動作：

![RMS 文件保護 - 步驟 1](../media/AzRMS_documentprotection1.png)

**步驟 1 中的情況**：RMS 用戶端會建立隨機金鑰 (內容金鑰)，並使用此金鑰搭配 AES 對稱式加密演算法來加密文件。

![RMS 文件保護 - 步驟 2](../media/AzRMS_documentprotection2.png)

**步驟 2 中的情況**：RMS 用戶端會接著根據範本或藉由指定文件的特定權限來建立包含文件原則的憑證。 此原則包含不同使用者或群組的權限以及其他限制，例如到期日。

RMS 用戶端會接著使用在初始化使用者環境時取得的組織金鑰，並使用此金鑰來加密原則和對稱內容金鑰。 RMS 用戶端也會使用在初始化使用者環境時所取得的使用者憑證來簽署原則。

![RMS 文件保護 - 步驟 3](../media/AzRMS_documentprotection3.png)

**步驟 3 中的情況**：最後，RMS 用戶端會將原則嵌入具有先前加密之文件本文的檔案中，一起構成受保護的文件。

這份文件可以儲存在任何地方或使用任何方法進行共用，而且原則永遠與加密的文件並存。

### 內容取用
當使用者想要取用受保護的文件時，RMS 用戶端會從要求 Azure RMS 服務的存取權著手：

![RMS 文件使用 - 步驟 1](../media/AzRMS_documentconsumption1.png)

**步驟 1 中的情況**：經過驗證的使用者會將文件原則和使用者的憑證傳送至 Azure RMS。 服務會解密和評估原則，以及建立使用者對此文件具備的權限清單 (如果有的話)。

![RMS 文件使用 - 步驟 2](../media/AzRMS_documentconsumption2.png)

**步驟 2 中的情況**：服務會接著從解密的原則擷取 AES 內容金鑰。 然後，使用透過要求取得的使用者公開 RSA 金鑰來加密這個金鑰。

重新加密的內容金鑰會接著與使用者權限清單一起內嵌到加密的使用授權中，然後傳回至 RMS 用戶端。

![RMS 文件使用 - 步驟 3](../media/AzRMS_documentconsumption3.png)

**步驟 3 中的情況**：最後，RMS 用戶端會採用加密的使用授權，並使用自己的使用者私密金鑰加以解密。 這可讓 RMS 用戶端視需要將文件的本文解密並呈現在螢幕上。

用戶端也會解密權限清單並將其傳遞至應用程式，以在應用程式的使用者介面中強制執行這些權限。

### 變化
先前的逐步解說內容涵蓋了標準案例，但另外有一些變化案例：

-   **行動裝置**：當行動裝置透過 Azure RMS 保護或取用檔案時，程序流程會簡單許多。 行動裝置不會先經過使用者初始化程序，因為每項交易 (用以保護或取用內容) 都是獨立的。 在 Windows 電腦中，行動裝置會連接至 Azure RMS 服務並進行驗證。 若要保護內容，行動裝置會提交一個原則，而 Azure RMS 會將用以保護文件的發佈授權和對稱金鑰傳送給行動裝置。 若要取用內容，行動裝置在連接至 Azure RMS 服務並進行驗證時，會將此文件原則傳送至 Azure RMS 並要求用以取用文件的使用授權。 Azure RMS 會將必要的金鑰和限制傳送給行動裝置，作為回應。 這兩個程序都使用 TLS 來保護金鑰交換和其他通訊。

-   **RMS 連接器**：當 Azure RMS 搭配 RMS 連接器使用時，程序流程維持不變。 唯一的差別在於連接器會作為內部部署服務 (例如 Exchange Server 和 SharePoint Server) 與 Azure RMS 之間的轉送。 連接器本身不會執行任何作業，例如：初始化使用者環境，或是加密或解密。 它只會轉送通常會送至 AD RMS 伺服器的通訊，並處理每一端使用的通訊協定之間的轉譯。 這種情況下，您可搭配使用 Azure RMS 與內部部署服務。

-   **一般保護 (.pfile)**：當 Azure RMS 保護檔案時，流程基本上與內容保護相同，只不過 RMS 用戶端會建立一個可授與所有權限的原則。 取用檔案時，檔案會先解密，再傳遞至目標應用程式。 即使檔案原本不支援 RMS，這麼做可讓您保護所有的檔案。

-   **保護 PDF (.ppdf)**：當 Azure RMS 以原生方式保護 Office 檔案時，也會建立該檔案的複本並以同樣的方式予以保護。 唯一的差別在於檔案複本為 PPDF 檔案格式，而 RMS 共用應用程式知道如何開啟該種檔案格式僅供檢視。 這種情況下，您可透過電子郵件傳送受保護的附件，而且即使行動裝置沒有原本支援受保護 Office 檔案的應用程式，行動裝置上的收件者仍舊可以讀取附件。

## 後續步驟

若要深入了解 Azure RMS，請使用**了解和探索**一節中的其他文章 (例如[應用程式如何支援 Azure Rights Management](applications-support.md))，了解現有應用程式如何與 Azure RMS 整合，以提供資訊保護解決方案。 

檢閱 [Azure Rights Management 術語](../get-started/terminology.md)以熟悉設定和使用 Azure RMS 時可能會遇到的詞彙，並確定查看 [Azure Rights Management 的需求](../get-started/requirements-azure-rms.md)之後再開始部署。 如果您想要直接開始並且自行嘗試，請使用 [Azure Rights Management 快速入門教學課程](../get-started/quick-start-tutorial.md)。

如果您已準備好開始部署貴組織的 Azure RMS，請使用 [Azure Rights Management 部署藍圖](../plan-design/deployment-roadmap.md)作為您的部署步驟和作法指示的連結。

> [!TIP]
> 如需詳細資訊與說明，請使用 [Azure Rights Management 的資訊與支援](../get-started/information-support.md)中的資源和連結。



<!--HONumber=Aug16_HO4-->


