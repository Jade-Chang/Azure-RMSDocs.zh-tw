---
# required metadata

title: 作法：將驗證新增至您的應用程式 |Azure RMS
description: 描述 RMS 啟用應用程式的使用者驗證基本概念。
keywords:
author: bruceperlerms
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 200D9B23-F35D-4165-9AC4-C482A5CE1D28
# optional metadata

#ROBOTS:
audience: developer
#ms.devlang:
ms.reviewer: shubhamp
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# 作法：將驗證新增至您的應用程式

本主題描述 RMS 啟用應用程式的使用者驗證基本概念。

## 什麼是使用者驗證
使用者驗證是在裝置應用程式與 RMS 基礎結構之間建立通訊的必要步驟。 此驗證程序使用標準 OAuth 2.0 通訊協定，需要下列與目前使用者及其驗證要求相關的資訊；**授權**、**資源**和 **userId**。

**注意**  目前未使用範圍，但可能會也因此會保留供日後使用。

 

**使用者驗證回呼** - Microsoft Rights Management SDK 4.2 會在您未提供存取權杖時、您的存取權杖需要重新整理時、或存取權杖已過期時，使用您的驗證回呼實作。

每個平台的 RMS API 都有必須實作才能啟用使用者驗證的回呼。

-   Android API 會使用 [**AuthenticationRequestCallback**](/rights-management/sdk/4.2/api/android/com.microsoft.rightsmanagement#msipcthin2_authenticationrequestcallback_interface_java) 和 [**AuthenticationCompletionCallback**](/rights-management/sdk/4.2/api/android/authenticationcompletioncallback#msipcthin2_authenticationcompletioncallback_interface_java) 介面。
-   iOS OS X API 會使用 [**MSAuthenticationCallback**](/rights-management/sdk/4.2/api/iOS/iOS#msipcthin2_msauthenticationcallback_protocol_objc) 通訊協定。
-   WinPhone API 會使用 [**IAuthenticationCallback**](/rights-management/sdk/4.2/api/winrt/Microsoft.RightsManagement#msipcthin2_iauthenticationcallback) 介面。
-   Linux API 會使用 [IAuthenticationCallback](http://azuread.github.io/rms-sdk-for-cpp/classrmscore_1_1modernapi_1_1IAuthenticationCallback.html) 介面。

## 哪個程式庫用於驗證

為了實作驗證回呼，您必須下載適當的程式庫並設定開發環境以便使用它。 您會在這些平台的 GitHub 上發現 ADAL 程式庫。 下列每個資源皆包含指引，以設定您的環境並使用程式庫。

-   [iOS 適用的 Windows Azure Active Directory 驗證程式庫 (ADAL)](https://github.com/MSOpenTech/azure-activedirectory-library-for-ios/)
-   [Mac 適用的 Windows Azure Active Directory 驗證程式庫 (ADAL)](https://github.com/MSOpenTech/azure-activedirectory-library-for-ios/)
-   [Android 適用的 Windows Azure Active Directory 驗證程式庫 (ADAL)](https://github.com/MSOpenTech/azure-activedirectory-library-for-android)
-   [dotnet 適用的 Windows Azure Active Directory 驗證程式庫 (ADAL)](https://github.com/AzureAD/azure-activedirectory-library-for-dotnet)
-   若為 Linux SDK，ADAL 程式庫會利用 SDK 來源封裝，可透過 [Github](https://github.com/AzureAD/rms-sdk-for-cpp) 使用。

**注意**  雖然您可能會使用其他驗證程式庫，但仍建議您使用上述其中一個 Active Directory 驗證程式庫 (ADAL)。

## 內含 Azure Active Director 驗證程式庫 (ADAL) 的驗證輸入

ADAL 需要數個參數才能成功驗證使用者至 Azure RMS (或 AD RMS)。 這些是標準 OAuth 2.0 參數，任何 Azure AD 應用程式通常都需要它們，如同 RMS 啟用的應用程式一樣。 您可以在先前所列之相對應 Github 儲存機制的 README 檔案中找到 ADAL 使用方式的目前指導方針。

這些參數和指導方針都是 RMS 工作流程的必要項目︰

-   **授權單位** – 驗證端點的 URL，通常是 AAD 或 ADFS。 這個參數由 RMS SDK 驗證回呼提供給您的應用程式。
-   **資源** - 您嘗試存取的服務應用程式 URL/URI，通常是 Azure RMS 或 AD RMS。 這個參數由 RMS SDK 驗證回呼提供給您的應用程式。
-   **使用者識別碼** – 想要存取應用程式的使用者 UPN，通常是電子郵件地址。 如果使用者仍未知，而且也用來快取使用者權杖，或從快取要求權杖，這個參數可以是空的。 這通常也會用來做為使用者提示的「提示」。
-   **用戶端識別碼** – 用戶端應用程式的識別碼。 這必須是有效的 Azure AD 應用程式識別碼。 如需詳細資訊，請參閱作法：取得 Azure 應用程式識別碼。
-   **重新導向 Uri** – 提供內含 URI 目標的驗證程式庫給驗證碼。 請注意，iOS 和 Android 需要特定的格式，這些格式會在 ADAL 的相對應 GitHub 儲存機制之 README 檔案中說明。

    Android： `msauth://packagename/Base64UrlencodedSignature`

    iOS： `<app-scheme>://<bundle-id>`

**注意**  如果您的應用程式未遵循這些指導方針，Azure RMS 和 Azure AD 工作流程可能會失敗，而且不受 Microsoft.com 支援。 此外，如果在生產應用程式中使用無效的用戶端識別碼，可能會違反 Rights Management 授權合約 (RMLA)。

## 驗證回呼實作的外觀為何

**驗證碼範例** - 此 SDK 有範例程式碼示範驗證回呼的使用。 為了方便起見，這些程式碼範例會在這裡以及後續的每個連結主題出現。

**Android 使用者驗證** - 如需詳細資訊，請參閱 [Android 程式碼範例](android-code.md)，第一個案例的**步驟 2**，「取用 RMS 受保護檔案」。


    class MsipcAuthenticationCallback implements AuthenticationRequestCallback
    {
    ...

    @Override
    public void getToken(Map<String, String> authenticationParametersMap,
                         final AuthenticationCompletionCallback authenticationCompletionCallbackToMsipc)
    {
        String authority = authenticationParametersMap.get("oauth2.authority");
        String resource = authenticationParametersMap.get("oauth2.resource");
        String userId = authenticationParametersMap.get("userId");
        mClientId = “12345678-ABCD-ABCD-ABCD-ABCDEFGHIJ”; // get your registered Azure AD application ID here
        mRedirectUri = “urn:ietf:wg:oauth:2.0:oob”;
        final String userHint = (userId == null)? "" : userId;
        AuthenticationContext authenticationContext = App.getInstance().getAuthenticationContext();
        if (authenticationContext == null || !authenticationContext.getAuthority().equalsIgnoreCase(authority))
        {
            try
            {
                authenticationContext = new AuthenticationContext(App.getInstance().getApplicationContext(), authority, …);
                App.getInstance().setAuthenticationContext(authenticationContext);
            }
            catch (NoSuchAlgorithmException e)
            {
                …
                authenticationCompletionCallbackToMsipc.onFailure();
            }
            catch (NoSuchPaddingException e)
            {
                …
                authenticationCompletionCallbackToMsipc.onFailure();
            }
       }
        App.getInstance().getAuthenticationContext().acquireToken(mParentActivity, resource, mClientId, mRedirectURI, userId, mPromptBehavior,
                       "&USERNAME=" + userHint, new AuthenticationCallback<AuthenticationResult>()
                        {
                            @Override
                            public void onError(Exception exc)
                            {
                                …
                                if (exc instanceof AuthenticationCancelError)
                                {
                                     …
                                    authenticationCompletionCallbackToMsipc.onCancel();
                                }
                                else
                                {
                                     …
                                    authenticationCompletionCallbackToMsipc.onFailure();
                                }
                            }

                            @Override
                            public void onSuccess(AuthenticationResult result)
                            {
                                …
                                if (result == null || result.getAccessToken() == null
                                        || result.getAccessToken().isEmpty())
                                {
                                     …
                                }
                                else
                                {
                                    // request is successful
                                    …
                                    authenticationCompletionCallbackToMsipc.onSuccess(result.getAccessToken());
                                }
                            }
                        });
                         }


**iOS/OS X 使用者驗證** - 如需詳細資訊，請參閱 [iOS/OS X 程式碼範例](ios-os-x-code-examples.md)，

第一個案例的**步驟 2**，「取用 RMS 受保護檔案」。


    // AuthenticationCallback holds the necessary information to retrieve an access token.
    @interface MsipcAuthenticationCallback : NSObject<MSAuthenticationCallback>

    @end

    @implementation MsipcAuthenticationCallback

    - (void)accessTokenWithAuthenticationParameters:
         (MSAuthenticationParameters *)authenticationParameters
                                completionBlock:
         (void(^)(NSString *accessToken, NSError *error))completionBlock
    {
    ADAuthenticationError *error;
    ADAuthenticationContext* context = [ADAuthenticationContext authenticationContextWithAuthority:authenticationParameters.authority error:&error];

    NSString *appClientId = @”12345678-ABCD-ABCD-ABCD-ABCDEFGHIJ”;

    // get your registered Azure AD application ID here

    NSURL *redirectURI = [NSURL URLWithString:@”ms-sample://com.microsoft.sampleapp”];

    // get your <app-scheme>://<bundle-id> here
    // Retrieve token using ADAL
    [context acquireTokenWithResource:authenticationParameters.resource
                             clientId:appClientId
                          redirectUri:redirectURI
                               userId:authenticationParameters.userId
                      completionBlock:^(ADAuthenticationResult *result)
                      {
                          if (result.status != AD_SUCCEEDED)
                          {
                              NSLog(@"Auth Failed");
                              completionBlock(nil, result.error);
                          }
                          else
                          {
                              completionBlock(result.accessToken, result.error);
                          }
                      }

        ];
    }



**Linux / C++ 使用者驗證** - 如需詳細資訊，請參閱 [Linux 程式碼範例](linux-c-code-examples.md)。



    // Class Header
    class AuthCallback : public IAuthenticationCallback {
    private:

      std::shared_ptr<rmsauth::FileCache> FileCachePtr;
      std::string clientId_;
      std::string redirectUrl_;

      public:

      AuthCallback(const std::string& clientId,
               const std::string& redirectUrl);
      virtual std::string GetToken(shared_ptr<AuthenticationParameters>& ap) override;
    };

    class ConsentCallback : public IConsentCallback {
      public:

      virtual ConsentList Consents(ConsentList& consents) override;
    };

    // Class Implementation
    AuthCallback::AuthCallback(const string& clientId, const string& redirectUrl)
    : clientId_(clientId), redirectUrl_(redirectUrl) {
      FileCachePtr = std::make_shared<FileCache>();
    }

    string AuthCallback::GetToken(shared_ptr<AuthenticationParameters>& ap)
    {
      string redirect =
      ap->Scope().empty() ? redirectUrl_ : ap->Scope();

      try
      {
        if (redirect.empty()) {
        throw rmscore::exceptions::RMSInvalidArgumentException(
              "redirect Url is empty");
      }

      if (clientId_.empty()) {
      throw rmscore::exceptions::RMSInvalidArgumentException("client Id is empty");
      }

      AuthenticationContext authContext(
        ap->Authority(), AuthorityValidationType::False, FileCachePtr);

      auto result = authContext.acquireToken(ap->Resource(),
                                           clientId_, redirect,
                                           PromptBehavior::Auto,
                                           ap->UserId());
      return result->accessToken();
      }

      catch (const rmsauth::Exception& ex)
      {
        // out logs
        throw;
      }
    }



 

 


<!--HONumber=Apr16_HO4-->


