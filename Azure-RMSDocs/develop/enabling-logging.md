---
title: "作法：啟用錯誤和效能記錄 | Azure RMS"
description: "Microsoft Rights Management SDK 4.2 透過單一裝置屬性來管理診斷和效能記錄檔上傳。"
keywords: 
author: bruceperlerms
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: F5AD3826-2292-4A25-AF5C-D17D083F5742
audience: developer
ms.reviewer: shubhamp
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 79e58b8092ea7cb057229d4c464d79f3694296e6
ms.openlocfilehash: 5faea360de8aa9ecb82abf25b5c1392d52d0afad


---

# 作法：啟用錯誤和效能記錄
Microsoft Rights Management SDK 4.2 透過單一裝置屬性來管理診斷和效能記錄檔上傳。

## 概觀 ##
您可以將診斷和效能記錄自動上傳至 Microsoft，以改善您的使用者體驗和疑難排解。 若要接受使用者隱私權，身為應用程式開發人員的您必須先要求使用者同意，才能啟用自動記錄。

您將會透過兩個屬性來管理記錄控制。

-   透過 **IpcCustomerExperienceDataCollectionEnabled** 屬性啟用記錄。 這是跨裝置重設的持續性設定。
-   使用下列設定，透過 **IpcLogLevel** 屬性控制記錄層級。

    * 1 - 詳細資訊
    * 2 - 資訊
    * 3 - 警告
    * 4 - 錯誤
    * 5 - 重大

在下列每個程式碼片段範例中，呼叫應用程式可以設定或查詢屬性。

### Android ###
啟用自動記錄

    SharedPreferences preferences = PreferenceManager.getDefaultSharedPreferences(context);
    SharedPreferences.Editor editor = preferences.edit();
    editor.putBoolean(&quot;IpcCustomerExperienceDataCollectionEnabled&quot;, true);
    editor.commit();

取得目前的記錄控制旗標設定

    SharedPreferences preferences = PreferenceManager.getDefaultSharedPreferences(context);
    Boolean isLogUploadEnabled = preferences.getBoolean(&quot;IpcCustomerExperienceDataCollectionEnabled&quot;, false);

## iOS ##
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
 

## Windows ##
啟用自動記錄

    CustomerExperienceConfiguration::Option = CustomerExperienceOptions::LoggingEnabledNow;

如需選用設定的詳細資訊，請參閱 [CustomerExperienceOptions](/rights-management/sdk/4.2/api/winrt/Microsoft.RightsManagement#msipcthin2_customerexperienceoptions)。

取得目前的記錄控制旗標設定

    CustomerExperienceOptions loggingOption = CustomerExperienceConfiguration::Option;


**注意** - 上述是 C++ 中的 Windows 程式碼片段。 若是 C\#，請將 ‘::’ 取代為 ‘.’ 以更新語法 。

**Linux / C++** - 此 SDK 有一些基本記錄，不如其他平台廣泛。 如需詳細資訊，請參閱[可攜 C++ 的 RMS SDK](https://github.com/AzureAD/rms-sdk-for-cpp#troubleshooting) 上 "README.md" 的**疑難排解**一節。

 

 



<!--HONumber=Jul16_HO3-->


