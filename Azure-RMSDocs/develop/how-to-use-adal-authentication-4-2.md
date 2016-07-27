---
title: "使用 Azure 入口網站設定 RMS 驗證 | Azure RMS"
description: "概述 ADAL 驗證的程序"
keywords: "驗證, RMS, ADAL"
author: bruceperlerms
manager: mbaldwin
ms.date: 06/14/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 2680b399-febb-4bd6-b844-ac3d1e69aca4
audience: developer
ms.reviewer: shubhamp
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 3f43f5605b1c341d7be618327038d1a86a305a5b
ms.openlocfilehash: cb82f0333ed17ee2994608baa3bbb50d42f19073


---

# 如何︰使用 Azure 入口網站設定 RMS 驗證

使用 Azure Active Directory Authentication Library (ADAL) 向 Azure RMS 驗證您的應用程式。

如果要使用此方法，您的應用程式必須管理本身的 OAuth 驗證。 使用這個方法，RMS 用戶端只有在需要驗證時才會執行應用程式所定義的回呼。

## 透過 Azure 入口網站設定
遵循本指南開始透過 Azure 入口網站進行設定，[為 ADAL 驗證設定 Azure RMS](adal-auth.md)。 請務必複製並儲存此程序中的*用戶端識別碼*及*重新導向 URI* 以供後續使用。

## 程式碼範例
以下程式碼片段來自較大的行動用戶端程式碼範例，可啟用 Azure ADAL。 如需詳細資訊，請參閱 [MSIPCSampleApp](https://github.com/AzureAD/rms-sdk-ui-for-android/tree/master/samples/MsipcSampleApp) 中的完整範例

       /**
       * Instantiates a new rms authentication callback.
       *
       * @param parentActivity the parent activity
       * @throws NoSuchAlgorithmException the no such algorithm exception
       * @throws InvalidKeySpecException the invalid key spec exception
       * @throws UnsupportedEncodingException the unsupported encoding exception
       */

       public MsipcAuthenticationCallback(Activity parentActivity) throws NoSuchAlgorithmException, InvalidKeySpecException, UnsupportedEncodingException
       {
         mParentActivity = parentActivity;
         setADALKeyStore();

         /**
         * Note: Following values of are client_id and redirect_uri are for demo purpose only.
         * Your values will come from the preceeding Azure Portal process.
         */
         mClientId = "com.microsoft.rightsmanagement.sampleapp";
         mRedirectURI = mClientId + "://authorize";
       }


## 相關主題

- [MSIPCSampleApp](https://github.com/AzureAD/rms-sdk-ui-for-android/tree/master/samples/MsipcSampleApp)
- [為 ADAL 驗證設定 Azure RMS](adal-auth.md)



<!--HONumber=Jul16_HO3-->


