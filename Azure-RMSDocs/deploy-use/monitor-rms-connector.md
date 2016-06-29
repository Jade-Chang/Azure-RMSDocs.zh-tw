---
# required metadata

title: 監視 Azure Rights Management 連接器 | Azure RMS
description:
keywords:
author: cabailey
manager: mbaldwin
ms.date: 06/09/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 8a1b3e54-f788-4f84-b9d7-5d5079e50b4e

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: esaggese
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# 監視 Azure Rights Management 連接器

*適用於︰Azure Rights Management、Windows Server 2012、Windows Server 2012 R2*

在您安裝並設定 RMS 連接器後，可以使用下列方法和資訊，協助您監視連接器和您組織的 Azure RMS 使用狀況。

## 應用程式事件記錄檔項目

RMS 連接器會使用應用程式事件記錄檔，記錄 **Microsoft RMS 連接器**的項目。 

以資訊事件舉例，ID 1000 表示確認連接器服務已啟動、ID 1002 表示伺服器成功連接至 RMS 連接器，而 ID 1004 表示授權的帳戶 (列出每個帳戶) 清單每次都會下載到連接器。 

如果您未設定讓連接器使用 HTTPS，應該會看見警告 ID 2002，表示用戶端使用不安全 (HTTP) 連線。

如果連接器無法連線到 Azure RMS，您很可能會看到錯誤 3001。 例如，這可能是因為發生 DNS 問題，或有一或多個執行 RMS 連接器的伺服器缺少網際網路存取。 

> [!TIP] 若 RMS 連接器伺服器無法連線到 Azure RMS，通常是因為 Web Proxy 設定的緣故。

對於所有事件記錄檔項目，都請向內切入訊息以取得詳細資訊。

除了在您第一次部署連接器時檢查事件記錄檔，也請持續檢查警告和錯誤。 例如，連接器一開始可能會正常運作，但其他系統管理員可能會變更相依設定。 例如，其他系統管理員變更 Web Proxy 伺服器設定，使 RMS 連接器伺服器無法再存取網際網路 (錯誤 3001)，或從您指定為已授權使用連接器的群組移除電腦帳戶 (警告 2001)。

## 效能計數器

當您安裝 RMS 連接器時，其會自動建立 **Microsoft Rights Management 連接器** 效能計數器，可協助您監控透過連接器使用 Azure RMS 的效能。 

例如，如果在保護文件或電子郵件、或開啟受保護的文件或電子郵件時經常延遲，效能計數器可協助您判斷延遲是否源自於連接器上的處理時間、Azure RMS 或網路延遲的處理時間。 為了協助您識別發生延遲的位置，請尋找包含**連接器處理時間**、**服務回應時間**和**連接器回應時間**平均計數的計數器。 例如︰**Licensing Successful Batched Request Average Connector Response Time**。

如果您最近新增了伺服器帳戶以使用連接器，就適合檢查 **Time since last authorization policy update**，以確認連接器已在更新後下載清單，或您需要再稍候一段時間 (最多 15 分鐘)。

## RMS Analyzer

使用 Rights Management Services Analyzer 工具，協助您監視連接器的健康情況並識別任何設定問題。

如果您尚未下載此工具，您可以從 [下載中心](https://www.microsoft.com/en-us/download/details.aspx?id=46437)予以下載，然後將其安裝在任何具有網際網路存取、且可連接至 RMS 連接器的電腦上。 執行工具，然後在 **歡迎**頁面上，選取 **[Azure RMS 連接器]** 選項。

如需其他資訊和指示，請參閱下載頁面上的**詳細資料**和**安裝指示**。

## 記錄

使用量記錄可協助您識別電子郵件和文件是否受保護和使用。 當使用 RMS 連接器完成此動作後，記錄中的 [使用者識別碼] 欄位會包含當您安裝 RMS 連接器時自動產生的服務主體名稱。

如需詳細資訊，請參閱[記錄和分析 Azure Rights Management 使用情況](log-analyze-usage.md)。

如果您需要更詳細的記錄以進行診斷，可以使用 Windows Sysinternals 的 [Debugview](http://go.microsoft.com/fwlink/?LinkID=309277)，並透過修改 IIS 中預設網站的 web.config 檔案，為 RMS 連接器啟用追蹤。 若要做到這一點，請執行下列動作：

1. 從 **%programfiles%\Microsoft Rights Management connector\Web Service** 找出 web.config 檔案。

2. 找出下列這一行文字：

        <trace enabled="false" requestLimit="10" pageOutput="false" traceMode="SortByTime" localOnly="true"/>

3. 使用下列文字加以取代︰

        <trace enabled="true" requestLimit="10" pageOutput="false" traceMode="SortByTime" localOnly="true"/>

4.  停止及啟動 IIS 以啟用追蹤。 

5.  當您擷取所需的追蹤時，請還原步驟 3 中的行，然後先停止 IIS 再將其重新啟動。



<!--HONumber=Jun16_HO2-->


