---
title: "iOS/OS X 程式碼範例 | Azure RMS"
description: "本主題將介紹 iOS/OS X 版本的 RMS SDK 的重要程式碼元素。"
keywords: 
author: bruceperlerms
ms.author: bruceper
manager: mbaldwin
ms.date: 09/25/2016
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 7E12EBF2-5A19-4A8D-AA99-531B09DA256A
audience: developer
ms.reviewer: shubhamp
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: faa1f33d1151a2d4700cc64556510994c708a414
ms.openlocfilehash: ef311877b1deb71a62d3554e513ef6fdab443c28


---

# <a name="iosos-x-code-examples"></a>iOS/OS X 程式碼範例

本主題將介紹 iOS/OS X 版本的 RMS SDK 的重要程式碼元素。

**注意**：在範例程式碼和後續的說明中，我們使用詞彙 MSIPC (Microsoft 資訊保護與控制) 來參考用戶端程序。



## <a name="using-the-microsoft-rights-management-sdk-42-key-scenarios"></a>使用 Microsoft Rights Management SDK 4.2 - 重要案例


以下是來自較大範例應用程式的 **Objective C** 程式碼範例，表示導向此 SDK 的重要開發案例。 這些示範了參考受保護檔案的 Microsoft 受保護的檔案格式的用法、自訂受保護的檔案格式的使用，和自訂 UI 控制項的使用。

### <a name="scenario-consume-an-rms-protected-file"></a>案例︰取用 RMS 受保護的檔案


- **步驟 1**：建立 [MSProtectedData](https://msdn.microsoft.com/library/dn758348.aspx) 物件

 **描述**︰透過其建立方法 (使用 [MSAuthenticationCallback](https://msdn.microsoft.com/library/dn758312.aspx) 實作服務驗證以取得權杖) 將 [MSProtectedData](https://msdn.microsoft.com/library/dn758348.aspx) 物件具現化，方法是將 **MSAuthenticationCallback** 的執行個體作為參數 *authenticationCallback* 傳給 MSIPC API。 請參閱下列範例程式碼區段中的 [MSProtectedData protectedDataWithProtectedFile](https://msdn.microsoft.com/library/dn758351.aspx) 呼叫。

        + (void)consumePtxtFile:(NSString *)path authenticationCallback:(id<MSAuthenticationCallback>)authenticationCallback
        {
            // userId can be provided as a hint for authentication
            [MSProtectedData protectedDataWithProtectedFile:path
                                                 userId:nil
                                 authenticationCallback:authenticationCallback
                                                options:Default
                                        completionBlock:^(MSProtectedData *data, NSError *error)
            {
                //Read the content from the ProtectedData, this will decrypt the data
                NSData *content = [data retrieveData];
            }];
        }

- **步驟 2**︰使用 Active Directory 驗證程式庫 (ADAL) 的安裝程式驗證。

  **描述**︰在此步驟中，您會看到用來實作 [MSAuthenticationCallback](https://msdn.microsoft.com/library/dn758312.aspx) 與範例驗證參數的 ADAL。 如需有關如何使用 ADAL 的詳細資訊，請參閱 Azure AD 驗證程式庫 (ADAL)。

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
          ADAuthenticationContext* context = [
              ADAuthenticationContext authenticationContextWithAuthority:authenticationParameters.authority
                                                                error:&error
          ];
          NSString *appClientId = @”com.microsoft.sampleapp”;
          NSURL *redirectURI = [NSURL URLWithString:@"local://authorize"];
          // Retrieve token using ADAL
          [context acquireTokenWithResource:authenticationParameters.resource
                                 clientId:appClientId
                              redirectUri:redirectURI
                                   userId:authenticationParameters.userId
                          completionBlock:^(ADAuthenticationResult *result) {
                              if (result.status != AD_SUCCEEDED)
                              {
                                  NSLog(@"Auth Failed");
                                  completionBlock(nil, result.error);
                              }
                              else
                              {
                                  completionBlock(result.accessToken, result.error);
                              }
                          }];
       }

-   **步驟 3**︰透過 [MSUserPolicy](https://msdn.microsoft.com/library/dn790796.aspx) 物件的 [MSUserPolicy accessCheck](https://msdn.microsoft.com/library/dn790789.aspx) 方法，檢查此使用者是否存在此內容的編輯權限。

        - (void)accessCheckWithProtectedData:(MSProtectedData *)protectedData
        {
            //check if user has edit rights and apply enforcements
            if (!protectedData.userPolicy.accessCheck(EditableDocumentRights.Edit))
            {
                // enforce on the UI
                textEditor.focusableInTouchMode = NO;
                textEditor.focusable = NO;
                textEditor.enabled = NO;
            }
        }

### <a name="scenario-create-a-new-protected-file-using-a-template"></a>案例︰使用範本建立新的受保護檔案

此案例開始會取得範本清單，[MSTemplateDescriptor](https://msdn.microsoft.com/library/dn790785.aspx)，選取第一個項目來建立原則，然後建立並寫入至新的受保護檔案。

-   **步驟 1**：取得範本清單

        + (void)templateListUsageWithAuthenticationCallback:(id<MSAuthenticationCallback>)authenticationCallback
        {
            [MSTemplateDescriptor templateListWithUserId:@"user@domain.com"
                            authenticationCallback:authenticationCallback
                                   completionBlock:^(NSArray/*MSTemplateDescriptor*/ *templates, NSError *error)
                                   {
                                     // use templates array of MSTemplateDescriptor (Note: will be nil on error)
                                   }];
        }

-   **步驟 2**︰使用清單中的第一個範本來建立 [MSUserPolicy](https://msdn.microsoft.com/library/dn790796.aspx)。

        + (void)userPolicyCreationFromTemplateWithAuthenticationCallback:(id<MSAuthenticationCallback>)authenticationCallback
        {
            [MSUserPolicy userPolicyWithTemplateDescriptor:[templates objectAtIndex:0]
                                            userId:@"user@domain.com"
                                     signedAppData:nil
                            authenticationCallback:authenticationCallback
                                           options:None
                                   completionBlock:^(MSUserPolicy *userPolicy, NSError *error)
            {
            // use userPolicy (Note: will be nil on error)
            }];
        }

-   **步驟 3**︰建立 [MSMutableProtectedData](https://msdn.microsoft.com/library/dn758325.aspx) 並將內容寫入其中。

        + (void)createPtxtWithUserPolicy:(MSUserPolicy *)userPolicy contentToProtect:(NSData *)contentToProtect
        {
            // create an MSMutableProtectedData to write content
            [contentToProtect protectedDataInFile:filePath
                        originalFileExtension:kDefaultTextFileExtension
                               withUserPolicy:userPolicy
                              completionBlock:^(MSMutableProtectedData *data, NSError *error)
            {
             // use data (Note: will be nil on error)
            }];
        }

### <a name="scenario-open-a-custom-protected-file"></a>案例︰開啟自訂受保護的檔案


-   **步驟 1**︰從 *serializedContentPolicy* 建立 [MSUserPolicy](https://msdn.microsoft.com/library/dn790796.aspx)。

        + (void)userPolicyWith:(NSData *)protectedData
        authenticationCallback:(id<MSAuthenticationCallback>)authenticationCallback
        {
            // Read header information from protectedData and extract the  PL
            /*-------------------------------------------
            | PL length | PL | ContetSizeLength |
            -------------------------------------------*/
            NSUInteger serializedPolicySize;
            NSMutableData *serializedPolicy;
            [protectedData getBytes:&serializedPolicySize length:sizeof(serializedPolicySize)];
            [protectedData getBytes:[serializedPolicy mutableBytes] length:serializedPolicySize];

            // Get the user policy , this is an async method as it hits the REST service
            // for content key and usage restrictions
            // userId provided as a hint for authentication
            [MSUserPolicy userPolicyWithSerializedPolicy:serializedPolicy
                                              userId:@"user@domain.com"
                              authenticationCallback:authenticationCallback
                                             options:Default
                                     completionBlock:^(MSUserPolicy *userPolicy,
                                                       NSError *error)
            {

            }];
         }

-   **步驟 2**︰從**步驟 1** 並從中讀取，使用 [MSUserPolicy](https://msdn.microsoft.com/library/dn790796.aspx) 建立 [MSCustomProtectedData](https://msdn.microsoft.com/library/dn758321.aspx)。

        + (void)customProtectedDataWith:(NSData *)protectedData
        {
            // Read header information from protectedData and extract the  protectedContentSize
            /*-------------------------------------------
            | PL length | PL | ContetSizeLength |
            -------------------------------------------*/
            NSUInteger protectedContentSize;
            [protectedData getBytes:&protectedContentSize
                         length:sizeof(protectedContentSize)];

            // Create the MSCustomProtector used for decrypting the content
            // The content start position is the header length
            [MSCustomProtectedData customProtectedDataWithPolicy:userPolicy
                                               protectedData:protectedData
                                        contentStartPosition:sizeof(NSUInteger) + serializedPolicySize
                                                 contentSize:protectedContentSize
                                             completionBlock:^(MSCustomProtectedData *customProtector,
                                                               NSError *error)
            {
             //Read the content from the custom protector, this will decrypt the data
             NSData *content = [customProtector retrieveData];
             NSLog(@"%@", content);
            }];
         }

### <a name="scenario-create-a-custom-protected-file-using-a-custom-adhoc-policy"></a>案例︰使用自訂 (臨機操作) 原則建立自訂受保護的檔案


-   **步驟 1**︰使用使用者所提供的電子郵件地址來建立原則描述元。

    **描述**︰實際上會使用裝置介面的使用者輸入來建立下列物件；[MSUserRights](https://msdn.microsoft.com/en-us/library/dn790811.aspx) 和 [MSPolicyDescriptor](https://msdn.microsoft.com/library/dn758339.aspx)。

        + (void)policyDescriptor
        {
            MSUserRights *userRights = [[MSUserRights alloc] initWithUsers:[NSArray arrayWithObjects: @"user1@domain.com", @"user2@domain.com", nil] rights:[MSEmailRights all]];

            MSPolicyDescriptor *policyDescriptor = [[MSPolicyDescriptor alloc] initWithUserRights:[NSArray arrayWithObjects:userRights, nil]];
            policyDescriptor.contentValidUntil = [[NSDate alloc] initWithTimeIntervalSinceNow:NSTimeIntervalSince1970 + 3600.0];
            policyDescriptor.offlineCacheLifetimeInDays = 10;
        }

-   **步驟 2**︰從原則描述元 *selectedDescriptor* 建立自訂 [MSUserPolicy](https://msdn.microsoft.com/library/dn790796.aspx)。

        + (void)userPolicyWithPolicyDescriptor:(MSPolicyDescriptor *)policyDescriptor
        {
            [MSUserPolicy userPolicyWithPolicyDescriptor:policyDescriptor
                                          userId:@"user@domain.com"
                          authenticationCallback:authenticationCallback
                                         options:None
                                 completionBlock:^(MSUserPolicy *userPolicy, NSError *error)
            {
              // use userPolicy (Note: will be nil on error)
            }];
        }

-   **步驟 3**︰建立並將內容寫入到 [MSMutableCustomProtectedData](https://msdn.microsoft.com/library/dn758321.aspx)，然後關閉。

        + (void)mutableCustomProtectedData:(NSMutableData *)backingData policy:(MSUserPolicy *)policy contentToProtect:(NSString *)contentToProtect
        {
            //Get the serializedPolicy from a given policy
            NSData *serializedPolicy = [policy serializedPolicy];

            // Write header information to backing data including the PL
            // ------------------------------------
            // | PL length | PL | ContetSizeLength |
            // -------------------------------------
            NSUInteger serializedPolicyLength = [serializedPolicy length];
            [backingData appendData:[NSData dataWithBytes:&serializedPolicyLength length:sizeof(serializedPolicyLength)]];
            [backingData appendData:serializedPolicy];
            NSUInteger protectedContentLength = [MSCustomProtectedData getEncryptedContentLengthWithPolicy:policy contentLength:unprotectedData.length];
            [backingData appendData:[NSData dataWithBytes:&protectedContentLength length:sizeof(protectedContentLength)]];

            NSUInteger headerLength = sizeof(serializedPolicyLength) + serializedPolicyLength + sizeof(protectedContentLength);

            // Create the MSMutableCustomProtector used for encrypting content
            // The content start position is the current length of the backing data
            // The encryptedContentSize content size is 0 since there is no content yet
            [MSMutableCustomProtectedData customProtectorWithUserPolicy:policy
                                                        backingData:backingData
                                             protectedContentOffset:headerLength
                                                    completionBlock:^(MSMutableCustomProtectedData *customProtector,
                                                                      NSError *error)
            {
                //Append data to the custom protector, this will encrypt the data and write it to the backing data
                [customProtector appendData:[contentToProtect dataUsingEncoding:NSUTF8StringEncoding] error:&error];

                //close the custom protector so it will flush and finalise encryption
                [customProtector close:&error];

            }];
          }



<!--HONumber=Oct16_HO3-->


