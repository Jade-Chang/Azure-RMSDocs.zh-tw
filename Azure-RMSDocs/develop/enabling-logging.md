---
title: "作法：啟用錯誤和效能記錄 | Azure RMS"
description: "Microsoft Rights Management SDK 4.2 透過單一裝置屬性來管理診斷和效能記錄檔上傳。"
keywords: 
author: bruceperlerms
ms.author: bruceper
manager: mbaldwin
ms.date: 09/25/2016
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: F5AD3826-2292-4A25-AF5C-D17D083F5742
audience: developer
ms.reviewer: shubhamp
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: ac77c4e0bced244f1cec74f15cbe0d62c9ab4437
ms.openlocfilehash: 66d24f4ed737526525c041de7aeb96de35b37032


---

# <a name="how-to-enable-error-and-performance-logging"></a>作法：啟用錯誤和效能記錄
Microsoft Rights Management SDK 4.2 透過單一裝置屬性來管理診斷和效能記錄檔上傳。

## <a name="overview"></a>概觀 ##
您可以將診斷、效能及遙測記錄資料自動上傳至 Microsoft，以改善您的使用者體驗和疑難排解。 

> [!IMPORTANT] 
> 若要接受使用者隱私權，身為應用程式開發人員的您必須先要求使用者同意，才能啟用自動記錄。

> [!NOTE]
> 例如，以下是 Microsoft 用來記錄通知的標準訊息︰ 
>
> *開啟錯誤及效能記錄後，即表示您同意將錯誤及效能資料傳送至 Microsoft。Microsoft 會在網際網路上收集錯誤及效能資料 (以下稱「資料」)。Microsoft 會使用這項資料，進而提供及改進 Microsoft 產品和服務的品質、安全性及完整性。比方說，我們會分析效能及可靠性，例如使用了哪些功能、功能的回應速度、裝置效能、使用者介面互動，以及任何使用產品時遇到的問題。資料也將包含您軟體的設定相關資訊，例如目前正在執行的軟體以及 IP 位址。*  

您將會透過兩個屬性來管理記錄控制。

-   透過 **IpcCustomerExperienceDataCollectionEnabled** 屬性啟用記錄。 這是跨裝置重設的持續性設定。
-   使用下列設定，透過 **IpcLogLevel** 屬性控制記錄層級。

    * 1 - 詳細資訊
    * 2 - 資訊
    * 3 - 警告
    * 4 - 錯誤
    * 5 - 重大

在下列每個程式碼片段範例中，呼叫應用程式可以設定或查詢屬性。

### <a name="android"></a>Android ###
啟用自動記錄

    SharedPreferences preferences = PreferenceManager.getDefaultSharedPreferences(context);
    SharedPreferences.Editor editor = preferences.edit();
    editor.putBoolean(&quot;IpcCustomerExperienceDataCollectionEnabled&quot;, true);
    editor.commit();

取得目前的記錄控制旗標設定

    SharedPreferences preferences = PreferenceManager.getDefaultSharedPreferences(context);
    Boolean isLogUploadEnabled = preferences.getBoolean(&quot;IpcCustomerExperienceDataCollectionEnabled&quot;, false);

## <a name="ios"></a>iOS ##
啟用自動記錄

    NSUserDefaults \*prefs = [NSUserDefaults standardUserDefaults];
        [prefs setBool:FALSE forKey:@&quot;IpcCustomerExperienceDataCollectionEnabled”];
        [[NSUserDefaults standardUserDefaults] synchronize];

取得目前的記錄控制旗標設定

    [[NSUserDefaults standardUserDefaults] boolForKey:@&quot;IpcCustomerExperienceDataCollectionEnabled&quot;];

設定記錄層級控制

    NSUserDefaults \*prefs = [NSUserDefaults standardUserDefaults];
      [prefs setInteger:1 forKey:@&quot;IpcLogLevel”];
      [[NSUserDefaults standardUserDefaults] synchronize];

取得記錄層級控制設定

    [[NSUserDefaults standardUserDefaults] boolForKey:@&quot;IpcLogLevel&quot;];
 

## <a name="windows"></a>訊息 ##
啟用自動記錄

    CustomerExperienceConfiguration::Option = CustomerExperienceOptions::LoggingEnabledNow;

如需選用設定的詳細資訊，請參閱 [CustomerExperienceOptions](https://msdn.microsoft.com/library/microsoft.rightsmanagement.customerexperienceoptions.aspx)。

取得目前的記錄控制旗標設定

    CustomerExperienceOptions loggingOption = CustomerExperienceConfiguration::Option;


**注意** - 上述是 C++ 中的 Windows 程式碼片段。 若是 C\#，請將 ‘::’ 取代為 ‘.’ 以更新語法 。

**Linux / C++** - 此 SDK 有一些基本記錄，不如其他平台廣泛。 如需詳細資訊，請參閱[可攜 C++ 的 RMS SDK](https://github.com/AzureAD/rms-sdk-for-cpp#troubleshooting) 上 "README.md" 的**疑難排解**一節。

 

 



<!--HONumber=Nov16_HO1-->


