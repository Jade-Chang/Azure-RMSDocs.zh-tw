---
title: "最新消息和版本資訊 | Azure RMS"
description: "概述這個新版 RMS SDK 中的重要變更與功能。"
author: bruceperlerms
ms.author: bruceper
manager: mbaldwin
ms.date: 10/31/2016
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 4fa1c686-b00b-4734-9abb-141ce582a6af
audience: developer
ms.reviewer: shubhamp
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 60e64b1fb1184aaa51b6664ecb5288d6ff861413
ms.openlocfilehash: 04364bc5daec881fe3c55d5cd41e7be11ac91ae7


---

# <a name="whats-new-and-release-notes"></a>最新消息和版本資訊

## <a name="whats-new"></a>新功能
Microsoft Rights Management SDK 4.2 將 RMS 應用程式啟用的方便與彈性帶入全新境界。 本主題概述此版 RMS SDK 的重要變更與功能。

### <a name="new-for-june-2016"></a>2016 年 6 月的新功能

- **新式驗證支援** - 這會將 Active Directory 驗證庫 (ADAL) 登入整合到啟用 RMS 的應用程式中。 這可啟用登入功能，例如 Multi-Factor Authentication (MFA)、SAML 型協力廠商身分識別提供者與 RMS 用戶端應用程式、智慧卡和憑證型驗證，並讓啟用 RMS 的應用程式不再需要使用基本驗證通訊協定。
- **文件追蹤支援** - 開發人員現在可以在保護應用程式中的文件時啟用文件追蹤
- 效能改善
- 錯誤修正


### <a name="december-2015-update"></a>2015 年 12 月更新

在此版本中，裝置的 RMS SDK 現在是 4.2 版且新增︰

-   文件追蹤，僅限 RMS 線上，適用於 iOS/OS X 和 Android 作業系統。

    如需 iOS/OS X 的詳細資訊和使用指引，請參閱 [MSLicenseMetadata](https://msdn.microsoft.com/library/mt573683.aspx) 類別，可提供追蹤資訊，以及 [MSUserPolicy](https://msdn.microsoft.com/library/dn790796.aspx) 上的其他文件追蹤註冊方法。 Android 對 [LicenseMetadata](https://msdn.microsoft.com/library/mt573675.aspx) 和 [UserPolicy](https://msdn.microsoft.com/library/dn790887.aspx) 有類似的新增項目。

    如需文件追蹤功能的詳細說明，請參閱[作法：使用文件追蹤](how-to-use-document-tracking.md)。

-   一組與非同步版本 Android API 平行的同步方法︰

    [CustomProtectedInputStream.create 同步方法](https://msdn.microsoft.com/library/mt631362.aspx)

    [CustomProtectedOutputStream.create 同步方法](https://msdn.microsoft.com/library/mt631363.aspx)

    [ProtectedFileInputStream.create 同步方法](https://msdn.microsoft.com/library/mt631375.aspx)

    [ProtectedFileOutputStream.create 同步方法](https://msdn.microsoft.com/library/mt631376.aspx)

    [TemplateDescriptor.getTemplates 同步方法](https://msdn.microsoft.com/library/mt631380.aspx)

    [UserPolicy.acquire 同步方法](https://msdn.microsoft.com/library/mt631384.aspx)

    [UserPolicy.create (PolicyDescriptor…) 同步方法**](https://msdn.microsoft.com/library/mt631385.aspx)

    [UserPolicy.create (TempalteDescriptor…) 同步方法](https://msdn.microsoft.com/library/mt631386.aspx)

-   新的 [ProtectedBuffer](https://msdn.microsoft.com/library/mt631369.aspx) 類別已新增至 Android API。
-   改善錯誤訊息和疑難排解體驗的更新。
-   密碼編譯作業的顯著效能改善。

### <a name="july-2015-update-adds-support-for-linux-c-development"></a>2015 年 7 月更新 - 新增 Linux / C++ 開發的支援

此版本新增下列各項︰

-   Linux 平台的 RMS SDK 4.1

    如需詳細資訊，請參閱[開始使用](get-started.md)。

### <a name="may-2015-update-adds-logging-control"></a>2015 年 5 月更新 - 新增記錄控制

此版本新增下列各項的支援︰

-   iOS

    應用程式加密和解密都能獨立及平行運作。

    如需詳細資訊，請參閱 [MSProtector](https://msdn.microsoft.com/library/mt210993.aspx)。

    已啟用記錄層級控制設定。

    如需詳細資訊，請參閱[作法︰啟用錯誤和效能記錄](enabling-logging.md)

    快取新增的清除支援。

    如需詳細資訊，請參閱 [MSProtection:resetStateWithCompletionBlock](https://msdn.microsoft.com/library/mt210991.aspx)。

### <a name="february-2015-update-adds-windows-store-application-support"></a>2015 年 2 月更新 - 新增 Windows 市集應用程式支援

此版本新增 Windows 市集應用程式的支援，並提供 Windows Phone、Android 和 iOS/OS X 版 RMS SDK 4.1 的同等功能。

### <a name="january-2015-update-adds-winphone-platform-support"></a>2015 年 1 月更新 - 新增 WinPhone 平台支援

此版本新增 Windows Phone 作業系統的支援，並提供 Android 和 iOS/OS X 版 RMS SDK 4.1 的同等功能。

### <a name="october-2014-update-upgrade-to-microsoft-rms-sdk-41"></a>2014 年 10 月更新 - 升級至 Microsoft RMS SDK 4.1

4.1 版的 RMS SDK 會將下列新功能新增至 Google Android 和 Apple iOS / OS X。

-   適用於*使用者同意* 處理的 Android 和 iOS/OS X SDK API 擴充功能，可讓使用者確認 SDK 行為。 目前，文件追蹤和存取未知的 AD RMS 服務 URL 是支援的同意類型。

    如需詳細資訊，請參閱範例中 Android API 版的 [ConsentCallback 介面](https://msdn.microsoft.com/library/dn833503.aspx)。

-   現在支援 iOS 8 和 OS X 10.10 (Yosemite)。 也有一些 Xcode 6 所需的屬性名稱變更。

    範例；MSUserPolicy.name 變更為 [MSUserPolicy.policyName](https://msdn.microsoft.com/library/dn790799.aspx)。

## <a name="release-notes"></a>版本資訊

本節概述您身為開發人員想要知道的目前和舊版本 Microsoft Rights Management SDK 4.x API 相關資訊。

**AD RMS SDK 4.1 - iOS / OS X 與 Android 平台全球公開上市版本**

-   **AD RMS 支援** - IT 系統管理員可以使用行動裝置上啟用 RMS 的應用程式，搭配新 AD RMS 伺服器的行動裝置擴充功能。
-   **離線取用** - 使用者可以離線存取 RMS 保護的資料。
-   **隔離的驗證** - 開發人員可以將自己的驗證庫用於 Azure RMS 和 AD RMS (或使用建議的 [Azure AD 驗證庫 (ADAL)](https://MSDN.Microsoft.Com/library/jj573266.aspx))。
-   **隔離 UI** - 開發人員可以建置其使用者介面，以保護和取用 RMS 保護的文件。
-   **重新設計 API** - 開發人員現在可以享有簡單透明的加密和解密 API，其提供最省力的一致 RMS 行為和使用者體驗。

**所有平台通用**

-   RMS SDK 4.x API 並非*安全執行緒*。

**Android**

-   當您在 Amazon® Kindle 裝置上使用範例應用程式檢視 .ptxt 附件時，您必須先下載檔案才能檢視它。

    **解決方案** - 這是已知的問題，並將在稍後解決。

-   如果允許多個執行個體，使用 SDK 的應用程式可能會損毀。

    **解決方案** - 確定應用程式不允許對 Android API 進行多個執行個體呼叫。

-   當我使用的 *array.length* 值長度與 [ProtectedFileOutputStream](https://msdn.microsoft.com/library/dn790855.aspx).write(byte\[\] array, int offset, int length) 方法的長度不同時，之後無法使用 SDK 取用內容。

    **解決方案** - 這是已知問題。 若要減少此狀況，請一律傳遞長度值與長度參數相同 *byte\[\]* array，或使用 [ProtectedFileOutputStream](https://msdn.microsoft.com/library/dn790855.aspx).write(byte\[\] array) 方法。

**iOS 與 OS X**

-   我們的 iOS 和 OS X SDK 支援兩種葡萄牙文方言。 很不幸地，因為一個錯誤，我們目前未完全支援第 1 種方言當地語系化。 由於此錯誤，未完全支援葡萄牙文。 大部分的文字會轉譯，但不包含 UI。

    1. 葡萄牙文

    2. 葡萄牙文 (葡萄牙)

**僅限 iOS**

-   RMS SDK 4.x 不會顯示網路活動指示器。

    根據 Apple 人性化介面指導方針，這是 iOS 的已知選擇性行為。

**僅限 OS X**

-   RMS SDK 4.x 不會顯示網路活動指示器。

    根據 Apple 人性化介面指導方針，這是 OS X 的已知選擇性行為。

-   **解決方案** - 若要使用 OS X SDK 建立多個文件介面 (MDI) 應用程式，請使用下列指引。

    下列方法不得同時執行。 若要監視執行完成；請使用所述的完成區塊方法。

    - [MSProtectedData.protectedDataWithProtectedFile](https://msdn.microsoft.com/library/dn758351.aspx)
    - [MSCustomProtectedData.customProtectedDataWithPolicy](https://msdn.microsoft.com/library/dn758315.aspx)



**注意**  我們的 iOS API 不支援 MDI 應用程式。

## <a name="frequently-asked-questions"></a>常見問題集

**所有平台**

**問**︰我在保護工作流程中沒看到**自訂權限**選擇 UI。 為什麼？

**答**：這是已知的問題，並將在稍後解決。

**問**︰如何讓新的組織租用戶試用 SDK 和範例應用程式？

**答**︰若要為 Azure AD RMS 測試組織申請認證，請傳送電子郵件到 <rmcstbeta@microsoft.com>。

**問**︰我在文件中沒看到任何測試階層討論。 為什麼？

**答**︰沒有測試階層概念與新的 AD RMS SDK。 您可以隨時使用生產階層。

**問**︰在 2.1 版 RMS SDK 中，每個實作資訊保護的應用程式都需要產生的資訊清單，4.0 和更新版本的 SDK 也是這樣嗎？

**答**︰3.0 和更新版本的 Rights Management SDK 不再需要資訊清單。

**Android**

**問**︰SDK 測試過哪些開發環境？

**答**：使用 Google API 15 和更新版本的 Eclipse Juno。

**問**︰我可以從 UI 執行緒呼叫取消方法 cancel() 嗎？
**答**︰您應該從非 UI 執行緒呼叫取消方法 cancel()，因為它可能會中止網路連線。

**iOS**

**問**︰哪些平台通過 SDK 開發驗證？

**答**：Xcode 5.0 與 iOS 7 及更新版本。

**問**︰我在作業時呼叫了 cancel() 方法，不過仍然收到作業完成的通知。 為什麼？

**答**︰並非所有作業都可以取消，因此只能盡可能執行最佳取消作業。

**OS x**

**問**︰範例應用程式架構適用於 Xcode 5，我能夠使用 Xcode 4.6 嗎？

**答**︰OS X SDK 只能使用 Xcode 4.6 和更新版本，以及 OS X 10.8 和更新版本。

 

 



<!--HONumber=Nov16_HO1-->


