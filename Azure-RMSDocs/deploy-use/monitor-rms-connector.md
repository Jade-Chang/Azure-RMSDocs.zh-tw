---
title: "監視 Azure Rights Management 連接器 | Azure RMS"
description: 
keywords: 
author: cabailey
manager: mbaldwin
ms.date: 07/08/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 8a1b3e54-f788-4f84-b9d7-5d5079e50b4e
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: f8e23e8bcbfb25092cb31f7af76d17239f3063a7
ms.openlocfilehash: 32c3c93d55bd82f45fa7a081e55ae7ebe8f5956f


---

# 監視 Azure Rights Management 連接器

*適用於︰Azure Rights Management、Windows Server 2012、Windows Server 2012 R2*

在您安裝並設定 RMS 連接器後，可以使用下列方法和資訊，協助您監視連接器和您組織的 Azure RMS 使用狀況。

## 應用程式事件記錄檔項目

RMS 連接器會使用應用程式事件記錄檔，記錄 **Microsoft RMS 連接器**的項目。 

以資訊事件舉例，ID 1000 表示確認連接器服務已啟動、ID 1002 表示伺服器成功連接至 RMS 連接器，而 ID 1004 表示授權的帳戶 (列出每個帳戶) 清單每次都會下載到連接器。 

如果您未設定讓連接器使用 HTTPS，應該會看見警告 ID 2002，表示用戶端使用不安全 (HTTP) 連線。

如果連接器無法連線到 Azure RMS，您很可能會看到錯誤 3001。 例如，這可能是因為發生 DNS 問題，或有一或多個執行 RMS 連接器的伺服器缺少網際網路存取。 

> [!TIP]
> 若 RMS 連接器伺服器無法連線到 Azure RMS，通常是因為 Web Proxy 設定的緣故。

對於所有事件記錄檔項目，都請向內切入訊息以取得詳細資訊。

除了在您第一次部署連接器時檢查事件記錄檔，也請持續檢查警告和錯誤。 例如，連接器一開始可能會正常運作，但其他系統管理員可能會變更相依設定。 例如，其他系統管理員變更 Web Proxy 伺服器設定，使 RMS 連接器伺服器無法再存取網際網路 (錯誤 3001)，或從您指定為已授權使用連接器的群組移除電腦帳戶 (警告 2001)。

### 事件記錄識別碼和描述

請使用下列各節來識別可能的事件識別碼、描述和任何其他資訊。

-----

資訊 **1000**

**Microsoft RMS 連接器的 Web 服務已啟動。**

當 RMS 連接器初次嘗試啟動時，系統即會記錄此事件。

----

資訊 **1001**

**Microsoft RMS 連接器的 Web 服務已停止。**

當 RMS 連接器因正常運作結果而停止時，系統即會記錄此事件。 例如，在重新啟動 IIS 或電腦關機時。 

----

資訊 **1002**

**允許授權伺服器存取 Microsoft RMS 連接器。**

當內部部署伺服器的帳戶初次連接至 RMS 連接器時，一旦帳戶已在 RMS 連接器系統管理員工具中獲得 Azure RMS 系統管理員授權，系統即會記錄此事件。 事件訊息中會包含 SID、帳戶名稱和連線電腦的名稱。

----

資訊 **1003**

**來自下列用戶端的連線已從不安全的 (HTTP) 連線切換到安全的 (HTTPS) 連線。**

當內部部署伺服器與 RMS 連接器的連線已從 HTTP (較不安全) 切換為 HTTPS (較安全) 連線時，系統即會記錄此事件。 事件訊息中會包含 SID、帳戶名稱和連線電腦的名稱。

----

資訊 **1004**

**授權的帳戶清單已更新。**

當 RMS 連接器已下載最新獲授權使用 RMS 連接器帳戶的清單 (現有的帳戶和任何變更) 時，系統即會記錄此事件。 這份清單每隔 15 分鐘會下載一次，以讓 RMS 連接器與 Azure RMS 進行通訊。

----

警告 **2000**

**HTTP 內容中的使用者主體已遺失或無效，請確認 Microsoft RMS 連接器的網站 IIS 已停用 [匿名驗證]，並僅啟用 [Windows 驗證]。**

當 RMS 連接器無法唯一識別嘗試連接至 RMS 連接器的帳戶時，系統即會記錄此事件。 此結果可能是由於 IIS 誤設為匿名驗證，或該帳戶是來自不受信任的樹系所致。

----

警告 **2001**

**未經授權嘗試存取 Microsoft RMS 連接器。**

當帳戶嘗試連接至 RMS 連接器但失敗時，系統即會記錄此事件。 最常見的原因是因為進行連線的帳戶不在授權帳戶清單中 (RMS 連接器會從 Azure RMS 下載這份清單)。 例如，尚未下載最新的清單 (每隔 15 分鐘) 或清單中缺漏此帳戶。 

另一個可能原因是，您將 RMS 連接器安裝在設為使用連接器的相同伺服器上。 例如，您在執行 Exchange Server 的伺服器上安裝 RMS 連接器，並授與 Exchange 帳戶使用連接器的權限。 系統不支援此設定，因為當帳戶嘗試連接時，RMS 連接器無法正確識別該帳戶。

事件訊息包含嘗試連接至 RMS 連接器的帳戶和電腦相關資訊：

- 如果嘗試連接至 RMS 連接器的帳戶是有效的帳戶，請使用 RMS 連接器系統管理員工具，將帳戶新增至授權的帳戶清單。 如需哪些帳戶必須經過授權的詳細資訊，請參閱[將伺服器新增至允許伺服器清單](install-configure-rms-connector.md#add-a-server-to-the-list-of-allowed-servers)。 

- 如果嘗試連接至 RMS 連接器的帳戶與 RMS 連接器伺服器位於同一部電腦上，請將連接器安裝在不同伺服器上。 如需連接器之必要條件的詳細資訊，請參閱 [RMS 連接器的必要條件]( deploy-rms-connector.md#prerequisites-for-the-rms-connector)。

----

警告 **2002**

**來自下列用戶端的連線是使用不安全的 (HTTP) 連線。**

當內部部署伺服器成功連接至 RMS 連接器，但是使用 HTTP (較不安全) 而不是 HTTPS (較安全) 連線時，系統即會記錄此事件。 系統會依據每個帳戶記錄一個事件，而不是依據每次連線來記錄。 如果帳戶已順利切換為使用 HTTPS，但又還原為 HTTP 時，即會再次觸發此事件。

事件訊息包含帳戶 SID、帳戶名稱和連接至 RMS 連接器的電腦名稱。

如需如何設定 RMS 連接器以進行 HTTPS 連線的資訊，請參閱[設定 RMS 連接器使用 HTTPS](install-configure-rms-connector.md#configuring-the-rms-connector-to-use-https)。

----

警告 **2003**

**授權的清單是空的。 在獲連接器授權的使用者和群組清單填入之前，服務都將無法使用。**

當 RMS 連接器沒有授權帳戶清單，並導致內部部署伺服器無法連接到它時，系統即會記錄此事件。 RMS 連接器每隔 15 分鐘會從 Azure RMS 下載這份清單。 

若要指定帳戶，請使用 RMS 連接器系統管理員工具。 如需詳細資訊，請參閱[授權伺服器使用 RMS 連接器]( install-configure-rms-connector.md#authorizing-servers-to-use-the-rms-connector)。 

----

錯誤 **3000**

**Microsoft RMS 連接器發生未處理的例外狀況。**

每當 RMS 連接器發生未預期的錯誤，系統即會記錄此事件，並在事件訊息中包含錯誤的詳細資料。

您可以從事件訊息中的文字**要求失敗，回應空白**識別其中一個可能的原因。 如果看到這段文字，原因可能是您的網路裝置在內部部署伺服器與 RMS 連接器伺服器之間的封包進行 SSL 檢查。 但這不受支援，而且會產生失敗的通訊和此事件記錄檔訊息。

----

錯誤 **3001**

**下載授權資訊時發生例外狀況。**

如果 RMS 連接器無法下載已獲授權使用 RMS 連接器的最新帳戶清單，系統即會記錄此事件，並在事件訊息中包含錯誤的詳細資訊。



----

## 效能計數器

當您安裝 RMS 連接器時，其會自動建立 **Microsoft Rights Management 連接器** 效能計數器，可協助您監控透過連接器使用 Azure RMS 的效能。 

例如，如果在保護文件或電子郵件、或開啟受保護的文件或電子郵件時經常延遲，效能計數器可協助您判斷延遲是否源自於連接器上的處理時間、Azure RMS 或網路延遲的處理時間。 為了協助您識別發生延遲的位置，請尋找包含**連接器處理時間**、**服務回應時間**和**連接器回應時間**平均計數的計數器。 例如︰**Licensing Successful Batched Request Average Connector Response Time**。

如果您最近新增了伺服器帳戶以使用連接器，就適合檢查 **Time since last authorization policy update**，以確認連接器已在更新後下載清單，或您需要再稍候一段時間 (最多 15 分鐘)。

## RMS Analyzer

使用 Rights Management Services Analyzer 工具，協助您監視連接器的健康情況並識別任何設定問題。

如果您尚未下載此工具，您可以從 [下載中心](https://www.microsoft.com/en-us/download/details.aspx?id=46437)予以下載，然後將其安裝在任何具有網際網路存取、且可連接至 RMS 連接器的電腦上。 執行工具，然後在 **歡迎**頁面上，選取 **[Azure RMS 連接器]** 選項。

如需其他資訊和指示，請參閱下載頁面上的**詳細資料**和**安裝指示**。

## 記錄

使用量記錄可協助您識別電子郵件和文件是否受保護和使用。 當使用 RMS 連接器完成此動作後，記錄中的使用者識別碼欄位會包含 RMS 連接器自動產生的服務主體名稱 **Aadrm_S-1-7-0**。

如需使用記錄的詳細資訊，請參閱[記錄和分析 Azure Rights Management 使用情況](log-analyze-usage.md)。

如果您需要更詳細的記錄以進行診斷，可以使用 Windows Sysinternals 的 [Debugview](http://go.microsoft.com/fwlink/?LinkID=309277)，並透過修改 IIS 中預設網站的 web.config 檔案，為 RMS 連接器啟用追蹤。 若要做到這一點，請執行下列動作：

1. 從 **%programfiles%\Microsoft Rights Management connector\Web Service** 找出 web.config 檔案。

2. 找出下列這一行文字：

        <trace enabled="false" requestLimit="10" pageOutput="false" traceMode="SortByTime" localOnly="true"/>

3. 使用下列文字加以取代︰

        <trace enabled="true" requestLimit="10" pageOutput="false" traceMode="SortByTime" localOnly="true"/>

4.  停止及啟動 IIS 以啟用追蹤。 

5.  當您擷取所需的追蹤時，請還原步驟 3 中的行，然後先停止 IIS 再將其重新啟動。




<!--HONumber=Jul16_HO3-->


