---
# required metadata

title: 開始使用 | Azure RMS
description: RMS SDK 2.1 平台可讓開發人員建置運用 RMS 資訊保護的應用程式。
keywords:
author: bruceperlerms
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 728113C9-FCF9-4280-BE1D-6AF5C15E449E
# optional metadata

#ROBOTS:
audience: developer
#ms.devlang:
ms.reviewer: shubhamp
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---
# 使用者入門

Rights Management Services SDK 2.1 平台可讓開發人員建置透過 RMS Server 或 Azure RMS 運用 RMS 資訊保護的應用程式。 平台處理複雜的安全性作法，例如金鑰管理、加密和解密處理，並提供一個簡化的 API 以輕鬆開發應用程式。

## 開始使用 RMS SDK 2.1

本主題會引導您在測試環境中完成已啟用權限應用程式的設定和執行程序。 下列主題討論如何設定您的開發環境，並依據建議的工作執行順序列出。

## 本節內容

| 主題 | 說明 |
|-------|-------------|
| [版本資訊](release-notes-rtm.md) | 本主題包含此版和舊版 RMS SDK 2.1 的相關重要資訊。|
| [安裝 SDK](install-the-rms-sdk.md) | 本主題會引導您安裝開發人員工具。|
| [設定 Visual Studio](how-to-configure-a-visual-studio-project-to-use-the-ad-rms-sdk-2-0.md) | 本主題包含如何設定 Visual Studio 專案以使用 RMS SDK 2.1 的指示。|
| [開發您的應用程式](developing-your-application.md) | 本主題包含已啟用 RMS 應用程式的核心層面基本指導，可以當作您的專屬應用程式開發基礎。|
| [測試您的應用程式](running-your-first-application.md) |本主題包含如何設定以進行應用程式測試的指示。|
| [部署到生產環境](deploying-your-application.md) |本主題引導您完成已啟用權限應用程式的部署選項。|

一旦您開始使用，請查看我們的一些其他 [RMS 範例](samples.md)。 然後，隨時注意我們的 [RMS 開發人員的專屬部落格](http://blogs.msdn.com/b/rms/)。


請藉由遵循下列主題中的指引來嘗試使用 RMS SDK 2.1︰

-   [安裝 SDK](install-the-rms-sdk.md)
-   [測試具備權限的應用程式](running-your-first-application.md)
-   [IPCHelloWorld - 範例應用程式](how-to-build-your-first-application.md)

### 為何要使用 RMS SDK 2.1 保護您的內容

對於想要將 RMS 支援新增至其新的現有應用程式的開發人員，RMS SDK 2.1 可協助更容易執行下列項目︰

-   作者可管理、相容且功能強大的 RMS 感知應用程式。
-   持續加密使用者資料。 不論環境、裝置或作業系統，資料都會保留加密。
-   強制執行一組豐富的使用限制，例如預防機密資料的螢幕擷取。
-   支援企業管理的保護原則。
-   在新的驗證機制和加密演算法可供使用時支援其使用。

RMS SDK 2.1 支援重要的用戶端和伺服器平台範圍。 如需詳細資訊，請參閱[支援的平台](supported-platforms.md)。

## 核心原則

**簡化**—AD RMS SDK 1.0 的意見反應和使用模式會加以分析，而資料會用來簡化或自動化最困難的程式設計工作。 使用 RMS SDK 2.1 所撰寫的 RMS 應用程式需要的 RMS 程式碼列數通常比使用 AD RMS SDK 1.0 所撰寫的 RMS 應用程式還要少 5-10 倍。
**一次撰寫**—RMS SDK 2.1 應用程式不需要變更程式碼或重新編譯就能使用最新的 RMS 功能。 新的 RMS 功能會在新增至 RMS 伺服器時立即可供現有的應用程式使用。
**一致性**—RMS SDK 2.1 可協助您輕鬆撰寫應用程式，它們會一致採用不同的 RMS 組態。 它也會大幅減少您身為應用程式開發人員所需撰寫的 RMS 使用者介面數量，鼓勵一致的外觀及操作，並減少使用者教育的需求。

## 相關主題

* [AD RMS 範例](samples.md)
* [AD RMS 開發人員的專屬部落格](http://blogs.msdn.com/b/rms/)
* [安裝 SDK](install-the-rms-sdk.md)
* [IPCHelloWorld - 範例應用程式](how-to-build-your-first-application.md)
* [概觀](ad-rms-overview.md)
* [支援的平台](supported-platforms.md)
 

 


<!--HONumber=Jun16_HO2-->


