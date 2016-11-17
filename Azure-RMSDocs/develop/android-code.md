---
title: "Android 程式碼範例 | Azure RMS"
description: "本主題將介紹 Android 版本的 RMS SDK 的重要程式碼元素。"
keywords: 
author: bruceperlerms
ms.author: bruceper
manager: mbaldwin
ms.date: 09/25/2016
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 58CC2E50-1E4D-4621-A947-25312C3FF519
audience: developer
ms.reviewer: shubhamp
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 503a99f01335f3085b5d13c9faaf0a6f05063490
ms.openlocfilehash: febc212cb6bc4b91058aa0e9f18d1e51f751b552


---

# <a name="android-code-examples"></a>Android 程式碼範例

本主題將介紹 Android 版本的 RMS SDK 的重要程式碼元素。

**注意**：在範例程式碼和後續的說明中，我們使用詞彙 MSIPC (Microsoft 資訊保護與控制) 來參考用戶端程序。


## <a name="using-the-microsoft-rights-management-sdk-42-key-scenarios"></a>使用 Microsoft Rights Management SDK 4.2 - 重要案例

以下是來自較大範例應用程式的程式碼範例，表示導向此 SDK 的重要開發案例。 這些示範了參考受保護檔案的 Microsoft 受保護的檔案格式的用法、自訂受保護的檔案格式的使用，和自訂 UI 控制項的使用。



範例應用程式 *MSIPCSampleApp* 可搭配 SDK 用於 Android 作業系統。 請參閱 GitHub 上的 [rms-sdk-ui-for-android](https://github.com/AzureAD/rms-sdk-ui-for-android) 以存取此範例應用程式。

### <a name="scenario-consume-an-rms-protected-file"></a>案例︰取用 RMS 受保護的檔案

-   **步驟 1**︰建立 [ProtectedFileInputStream](https://msdn.microsoft.com/library/dn790851.aspx)

    **來源**︰*MsipcAuthenticationCallback.java*

    **描述**︰透過其建立方法 (使用 [AuthenticationRequestCallback](https://msdn.microsoft.com/library/dn758250.aspx) 實作服務驗證以取得權杖) 來具現化 [ProtectedFileInputStream](https://msdn.microsoft.com/library/dn790851.aspx) 物件，方法是將 **AuthenticationRequestCallback** 的執行個體作為參數 *mRmsAuthCallback* 傳遞給 MSIPC API。 請參閱下列範例程式碼一節結尾附近的 [ProtectedFileInputStream.create](https://msdn.microsoft.com/library/dn790851.aspx) 呼叫。

        public void startContentConsumptionFromPtxtFileFormat(InputStream inputStream)
        {
            CreationCallback<ProtectedFileInputStream> protectedFileInputStreamCreationCallback =
              new CreationCallback<ProtectedFileInputStream>()
            {
                @Override
                public Context getContext()
                {
                   …
               }

                @Override
                public void onCancel()
                {
                   …
                }

                @Override
                public void onFailure(ProtectionException e)
                {
                   …
                }

                @Override
                public void onSuccess(ProtectedFileInputStream protectedFileInputStream)
                {
                   …
                   …
                    byte[] dataChunk = new byte[16384];
                    try
                    {
                        while ((nRead = protectedFileInputStream.read(dataChunk, 0,
                                dataChunk.length)) != -1)
                        {
                            …
                        }
                         …
                        protectedFileInputStream.close();
                    }
                    catch (IOException e)
                    {
                      …
                    }  
              }
            };
            try
            {
               …
                ProtectedFileInputStream.create(inputStream, null, mRmsAuthCallback,
                                                PolicyAcquisitionFlags.NONE,
                                                protectedFileInputStreamCreationCallback);
            }
            catch (com.microsoft.rightsmanagement.exceptions.InvalidParameterException e)
            {
                …
            }
        }


-   **步驟 2**︰使用 Active Directory 驗證程式庫 (ADAL) 的安裝程式驗證。

    **來源**︰*MsipcAuthenticationCallback.java*。

    **描述**︰在此步驟中，您會看到用來實作 [AuthenticationRequestCallback](https://msdn.microsoft.com/library/dn758255.aspx) 與範例驗證參數的 ADAL。 如需如何使用 ADAL 的詳細資訊，請參閱 [Active Directory Authentication Library.NET](https://msdn.microsoft.com/library/jj573266.aspx)。


        class MsipcAuthenticationCallback implements AuthenticationRequestCallback
        {

        …

        @Override
        public void getToken(Map<String, String> authenticationParametersMap,
                             final AuthenticationCompletionCallback authenticationCompletionCallbackToMsipc)
        {
            String authority = authenticationParametersMap.get("oauth2.authority");
            String resource = authenticationParametersMap.get("oauth2.resource");
            String userId = authenticationParametersMap.get("userId");
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
                            }

                            );
                      }


-   **步驟 3**︰透過 [UserPolicy.accessCheck](https://msdn.microsoft.comlibrary/dn790885.aspx) 方法，檢查此使用者是否存在此內容的**編輯**權限。

    **來源**︰*TextEditorFragment.java*


         //check if user has edit rights and apply enforcements
                if (!mUserPolicy.accessCheck(EditableDocumentRights.Edit))
                {
                    mTextEditor.setFocusableInTouchMode(false);
                    mTextEditor.setFocusable(false);
                    mTextEditor.setEnabled(false);
                    …
                }


### <a name="scenario-create-a-new-protected-file-using-a-template"></a>案例︰使用範本建立新的受保護檔案

此案例一開始會取得範本清單，選取第一個範本以建立原則，然後建立並寫入至新的受保護檔案。

-   **步驟 1**︰透過 [TemplateDescriptor](https://msdn.microsoft.com/library/dn790871.aspx) 物件取得範本清單。

    **來源**︰*MsipcTaskFragment.java*



    CreationCallback<List<TemplateDescriptor>> getTemplatesCreationCallback = new CreationCallback<List<TemplateDescriptor>>() { @Override public Context getContext() { …
          }

          @Override
          public void onCancel()
          {
              …
          }

          @Override
          public void onFailure(ProtectionException e)
          {
              …
          }

          @Override
          public void onSuccess(List<TemplateDescriptor> templateDescriptors)
          {
             …
          }
      }; try { …
          mIAsyncControl = TemplateDescriptor.getTemplates(emailId, mRmsAuthCallback, getTemplatesCreationCallback); } catch (com.microsoft.rightsmanagement.exceptions.InvalidParameterException e) { …
      }


-    **步驟 2**︰使用清單中的第一個範本來建立 [UserPolicy](https://msdn.microsoft.com/library/dn790887.aspx)。

    **來源**︰*MsipcTaskFragment.java*



      CreationCallback<UserPolicy> userPolicyCreationCallback = new CreationCallback<UserPolicy>() { @Override public Context getContext() { …
          }

          @Override
          public void onCancel()
          {
              …
          }

          @Override
          public void onFailure(ProtectionException e)
          {
              …
          }

          @Override
          public void onSuccess(final UserPolicy item)
          {
              …
          }
      }; try { …
          mIAsyncControl = UserPolicy.create((TemplateDescriptor)selectedDescriptor, mEmailId, mRmsAuthCallback, UserPolicyCreationFlags.NONE, userPolicyCreationCallback); …
      } catch (InvalidParameterException e) { …
      }


-    **步驟 3**︰建立 [ProtectedFileOutputStream](https://msdn.microsoft.com/library/dn790855.aspx) 並寫入內容。

    **來源**︰*MsipcTaskFragment.java*


    private void createPTxt(final byte[] contentToProtect) { …
            CreationCallback<ProtectedFileOutputStream> protectedFileOutputStreamCreationCallback = new CreationCallback<ProtectedFileOutputStream>() { @Override public Context getContext() { …
                }

                @Override
                public void onCancel()
                {
                 …
                }

                @Override
                public void onFailure(ProtectionException e)
                {
                 …
                }

                @Override
                public void onSuccess(ProtectedFileOutputStream protectedFileOutputStream)
                {
                    try
                    {
                        // write to this stream
                        protectedFileOutputStream.write(contentToProtect);
                        protectedFileOutputStream.flush();
                        protectedFileOutputStream.close();
                        …
                    }
                    catch (IOException e)
                    {
                        …
                    }
                }
            };
            try
            {
                File file = new File(filePath);
                outputStream = new FileOutputStream(file);
                mIAsyncControl = ProtectedFileOutputStream.create(outputStream, mUserPolicy, originalFileExtension,
                        protectedFileOutputStreamCreationCallback);
            }
            catch (FileNotFoundException e)
            {
                 …
            }
            catch (InvalidParameterException e)
            {
                 …
            }
        }



### <a name="scenario-open-a-custom-protected-file"></a>案例︰開啟自訂受保護的檔案

-   **步驟 1**︰從 *serializedContentPolicy* 建立 [UserPolicy](https://msdn.microsoft.com/library/dn790887.aspx)。

    **來源**︰*MsipcTaskFragment.java*


    CreationCallback<UserPolicy> userPolicyCreationCallbackFromSerializedContentPolicy = new CreationCallback<UserPolicy>() { @Override public void onSuccess(UserPolicy userPolicy) { …
                }

                @Override
                public void onFailure(ProtectionException e)
                {
                  …
                }

                @Override
                public void onCancel()
                {
                  …
                }

                @Override
                public Context getContext()
                {
                  …
                }
            };


    try {   ...

      // Read the serializedContentPolicyLength from the inputStream.
      long serializedContentPolicyLength = readUnsignedInt(inputStream);

      // Read the PL bytes from the input stream using the PL size.
      byte[] serializedContentPolicy = new byte[(int)serializedContentPolicyLength]; inputStream.read(serializedContentPolicy);

      ...

      UserPolicy.acquire(serializedContentPolicy, null, mRmsAuthCallback, PolicyAcquisitionFlags.NONE,           userPolicyCreationCallbackFromSerializedContentPolicy); } catch (com.microsoft.rightsmanagement.exceptions.InvalidParameterException e) {   ... } catch (IOException e) {   ... }



-    **步驟 2**︰使用**步驟 1** 的 [UserPolicy](https://msdn.microsoft.com/library/dn790887.aspx) 建立 [CustomProtectedInputStream](https://msdn.microsoft.com/library/dn758271.aspx)。

    **來源**︰*MsipcTaskFragment.java*



      CreationCallback<CustomProtectedInputStream> customProtectedInputStreamCreationCallback = new CreationCallback<CustomProtectedInputStream>() { @Override public Context getContext() { …
         }

         @Override
         public void onCancel()
         {
             …
         }

         @Override
         public void onFailure(ProtectionException e)
         {
             …
         }

         @Override
         public void onSuccess(CustomProtectedInputStream customProtectedInputStream)
         {
            …

             byte[] dataChunk = new byte[16384];
             try
             {
                 while ((nRead = customProtectedInputStream.read(dataChunk, 0, dataChunk.length)) != -1)
                 {
                      …
                 }
                  …
                 customProtectedInputStream.close();
             }
             catch (IOException e)
             {
                …
             }
             …
         }
     };

    try {  ...

      // Retrieve the encrypted content size.
      long encryptedContentLength = readUnsignedInt(inputStream);

      updateTaskStatus(new TaskStatus(TaskState.Starting, "Consuming content", true));

      CustomProtectedInputStream.create(userPolicy, inputStream,                                 encryptedContentLength,                                 customProtectedInputStreamCreationCallback); } catch (com.microsoft.rightsmanagement.exceptions.InvalidParameterException e) {  ... } catch (IOException e) {  ... }


-    **步驟 3**︰從 [CustomProtectedInputStream](https://msdn.microsoft.com/library/dn758271.aspx) 讀取內容到 *mDecryptedContent*，然後關閉。

    **來源**︰*MsipcTaskFragment.java*


    @Override public void onSuccess(CustomProtectedInputStream customProtectedInputStream) {  mUserPolicy = customProtectedInputStream.getUserPolicy();  ByteArrayOutputStream buffer = new ByteArrayOutputStream();

      int nRead;                      
      byte[] dataChunk = new byte[16384];

      try  {    while ((nRead = customProtectedInputStream.read(dataChunk, 0,                                                        dataChunk.length)) != -1)    {       buffer.write(dataChunk, 0, nRead);    }

        buffer.flush();    mDecryptedContent = new String(buffer.toByteArray(), Charset.forName("UTF-8"));

        buffer.close();    customProtectedInputStream.close();  }  catch (IOException e)  {    ...  } }


### <a name="scenario-create-a-custom-protected-file-using-a-custom-adhoc-policy"></a>案例︰使用自訂 (臨機操作) 原則建立自訂受保護的檔案

-   **步驟 1**︰使用使用者所提供的電子郵件地址來建立原則描述元。

    **來源**︰*MsipcTaskFragment.java*

    **描述**︰實際上會使用裝置介面的使用者輸入來建立下列物件；[UserRights](https://msdn.microsoft.com/library/dn790911.aspx) 和 [PolicyDescriptor](https://msdn.microsoft.com/library/dn790843.aspx)。



      // create userRights list   UserRights userRights = new UserRights(Arrays.asList("consumer@domain.com"),     Arrays.asList( CommonRights.View, EditableDocumentRights.Print));   ArrayList<UserRights> usersRigthsList = new ArrayList<UserRights>();   usersRigthsList.add(userRights);

      // Create PolicyDescriptor using userRights list   PolicyDescriptor policyDescriptor = PolicyDescriptor.createPolicyDescriptorFromUserRights(                                                          usersRigthsList);   policyDescriptor.setOfflineCacheLifetimeInDays(10);   policyDescriptor.setContentValidUntil(new Date());



-    **步驟 2**︰從原則描述元 *selectedDescriptor* 建立自訂 [UserPolicy](https://msdn.microsoft.com/library/dn790887.aspx)。

    **來源**︰*MsipcTaskFragment.java*


       mIAsyncControl = UserPolicy.create((PolicyDescriptor)selectedDescriptor,                                          mEmailId, mRmsAuthCallback,                                          UserPolicyCreationFlags.NONE,                                          userPolicyCreationCallback);



-   **步驟 3**︰建立內容並將其寫入到 [CustomProtectedOutputStream](https://msdn.microsoft.com/library/dn758274.aspx)，然後關閉。

    **來源**︰*MsipcTaskFragment.java*


    File file = new File(filePath); final OutputStream outputStream = new FileOutputStream(file); CreationCallback<CustomProtectedOutputStream> customProtectedOutputStreamCreationCallback = new CreationCallback<CustomProtectedOutputStream>() { @Override public Context getContext() { …
            }

            @Override
            public void onCancel()
            {
              …
            }

            @Override
            public void onFailure(ProtectionException e)
            {
              …
            }

            @Override
            public void onSuccess(CustomProtectedOutputStream protectedOutputStream)
            {
                try
                {
                    // write serializedContentPolicy
                    byte[] serializedContentPolicy = mUserPolicy.getSerializedContentPolicy();
                    writeLongAsUnsignedIntToStream(outputStream, serializedContentPolicy.length);
                    outputStream.write(serializedContentPolicy);
                    // write encrypted content
                    if (contentToProtect != null)
                    {
                        writeLongAsUnsignedIntToStream(outputStream,
                                CustomProtectedOutputStream.getEncryptedContentLength(contentToProtect.length,
                                        protectedOutputStream.getUserPolicy()));
                        protectedOutputStream.write(contentToProtect);
                        protectedOutputStream.flush();
                        protectedOutputStream.close();
                    }
                    else
                    {
                        outputStream.flush();
                        outputStream.close();
                    }
                    …
                }
                catch (IOException e)
                {
                  …
                }
            }
        };
        try
        {
            mIAsyncControl = CustomProtectedOutputStream.create(outputStream, mUserPolicy,
                    customProtectedOutputStreamCreationCallback);
        }
        catch (InvalidParameterException e)
        {
          …
        }


 

 



<!--HONumber=Oct16_HO3-->


