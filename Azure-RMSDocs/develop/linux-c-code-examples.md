---
# required metadata

title: Linux 程式碼範例 | Azure RMS
description: 本主題介紹 Linux 版 RMS SDK 的重要案例與程式碼元素。
keywords:
author: bruceperlerms
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 0F7714CA-1D3E-4846-B187-739825B7DE26
# optional metadata

#ROBOTS:
audience: developer
#ms.devlang:
ms.reviewer: shubhamp
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Linux 程式碼範例

本主題介紹 Linux 版 RMS SDK 的重要案例與程式碼元素。

下列程式碼片段來自範例應用程式 *rms\_sample* 和 *rmsauth\_sample*。 如需詳細資訊，請參閱 GitHub 儲存機制的[範例](https://github.com/AzureAD/rms-sdk-for-cpp/tree/master/samples)。

## 案例︰從受保護的檔案存取保護原則資訊

**開啟和讀取 RMS 保護的檔案**
**來源**：[rms\_sample/mainwindow.cpp](https://github.com/AzureAD/rms-sdk-for-cpp/tree/master/samples/rms_sample)

**描述**︰從使用者取得檔案名稱之後，讀取憑證 (請參閱 *MainWindow::addCertificates*)、利用用戶端識別碼和重新導向 URL 設定授權回呼、呼叫 *ConvertFromPFile* (請參閱下列程式碼範例)，然後詳閱保護原則名稱、描述和內容有效日期。

**C++**︰

    void MainWindow::ConvertFromPFILE(const string&amp; fileIn,
        const string&amp; clientId,
        const string&amp; redirectUrl,
        const string&amp; clientEmail) 
    {
    // add trusted certificates using HttpHelpers of RMS and Auth SDKs
    addCertificates();
    
    // create shared in/out streams
    auto inFile = make_shared&lt;ifstream&gt;(
    fileIn, ios_base::in | ios_base::binary);
    
    if (!inFile-&gt;is_open()) {
     AddLog(&quot;ERROR: Failed to open &quot;, fileIn.c_str());
    return;
    }
    
    string fileOut;
    
    // generate output filename
    auto pos = fileIn.find_last_of(&#39;.&#39;);
    
    if (pos != string::npos) {
     fileOut = fileIn.substr(0, pos);
    }
    
     // create streams
    auto outFile = make_shared&lt;fstream&gt;(
    fileOut, ios_base::in | ios_base::out | ios_base::trunc | ios_base::binary);
    
    if (!outFile-&gt;is_open()) {
     AddLog(&quot;ERROR: Failed to open &quot;, fileOut.c_str());
     return;
      }
    
    try
    {
    // create authentication context
    AuthCallback auth(clientId, redirectUrl);
    
    // process convertion
    auto pfs = PFileConverter::ConvertFromPFile(
      clientEmail,
      inFile,
      outFile,
      auth,
      this-&gt;consent);
    
    AddLog(&quot;Successfully converted to &quot;, fileOut.c_str());
    }
    catch (const rmsauth::Exception&amp; e)
    {
    AddLog(&quot;ERROR: &quot;, e.error().c_str());
    }
    catch (const rmscore::exceptions::RMSException&amp; e) {
    AddLog(&quot;ERROR: &quot;, e.what());
    }
    inFile-&gt;close();
    outFile-&gt;close();
    }

**建立受保護的檔案資料流**
**來源**︰[rms\_sample/pfileconverter.cpp](https://github.com/AzureAD/rms-sdk-for-cpp/tree/master/samples/rms_sample)

**描述**︰這個方法會透過 SDK 方法從傳入的支援資料流建立受保護的檔案資料流 *ProtectedFileStream::Aquire*，然後傳回給呼叫者。

**C++**︰

    shared_ptr&lt;GetProtectedFileStreamResult&gt;PFileConverter::ConvertFromPFile(
    const string           &amp; userId,
    shared_ptr&lt;istream&gt;      inStream,
    shared_ptr&lt;iostream&gt;     outStream,
    IAuthenticationCallback&amp; auth,
    IConsentCallback       &amp; consent)
    {
    auto inIStream = rmscrypto::api::CreateStreamFromStdStream(inStream);
    
    auto fsResult = ProtectedFileStream::Acquire(
    inIStream,
    userId,
    auth,
    consent,
    POL_None,
    static_cast&lt;ResponseCacheFlags&gt;(RESPONSE_CACHE_INMEMORY
                                    | RESPONSE_CACHE_ONDISK));
    
    if ((fsResult.get() != nullptr) &amp;&amp; (fsResult-&gt;m_status == Success) &amp;&amp;
      (fsResult-&gt;m_stream != nullptr)) {
    auto pfs = fsResult-&gt;m_stream;
    
    // preparing
    readPosition  = 0;
    writePosition = 0;
    totalSize     = pfs-&gt;Size();
    
    // start threads
    for (size_t i = 0; i &lt; THREADS_NUM; ++i) {
      threadPool.push_back(thread(WorkerThread,
                                  static_pointer_cast&lt;iostream&gt;(outStream), pfs,
                                  false));
    }
    
    for (thread&amp; t: threadPool) {
      if (t.joinable()) {
        t.join();
      }
    }
    }
      return fsResult;
    }

## 案例︰使用範本建立新的受保護檔案

**利用使用者選取的範本保護檔案**
**來源**：[rms\_sample/mainwindow.cpp](https://github.com/AzureAD/rms-sdk-for-cpp/tree/master/samples/rms_sample)

**描述**︰從使用者取得檔案名稱、讀取憑證 (請參閱 *MainWindow::addCertificates*) 並利用用戶端識別碼和重新導向 URL 設定授權回呼之後，可透過呼叫 *ConvertToPFileTemplates* (請參閱下列程式碼範例) 保護選取的檔案。

**C++**︰

    void MainWindow::ConvertToPFILEUsingTemplates(const string&amp; fileIn,
                                              const string&amp; clientId,
                                              const string&amp; redirectUrl,
                                              const string&amp; clientEmail) 
    {
    // generate output filename
    string fileOut = fileIn + &quot;.pfile&quot;;
    
    // add trusted certificates using HttpHelpers of RMS and Auth SDKs
    addCertificates();
    
    // create shared in/out streams
    auto inFile = make_shared&lt;ifstream&gt;(
    fileIn, ios_base::in | ios_base::binary);
    auto outFile = make_shared&lt;fstream&gt;(
    fileOut, ios_base::in | ios_base::out | ios_base::trunc | ios_base::binary);
    
    if (!inFile-&gt;is_open()) {
    AddLog(&quot;ERROR: Failed to open &quot;, fileIn.c_str());
    return;
    }
    
    if (!outFile-&gt;is_open()) {
    AddLog(&quot;ERROR: Failed to open &quot;, fileOut.c_str());
    return;
    }
    
    // find file extension
    string fileExt;
    auto   pos = fileIn.find_last_of(&#39;.&#39;);
    
    if (pos != string::npos) {
    fileExt = fileIn.substr(pos);
    }
    
    try {
    // create authentication callback
    AuthCallback auth(clientId, redirectUrl);
    
    // process convertion
    PFileConverter::ConvertToPFileTemplates(
      clientEmail, inFile, fileExt, outFile, auth,
      this-&gt;consent, this-&gt;templates);
    
    AddLog(&quot;Successfully converted to &quot;, fileOut.c_str());
    }
   catch (const rmsauth::Exception&amp; e) {
    AddLog(&quot;ERROR: &quot;, e.error().c_str());
    outFile-&gt;close();
    remove(fileOut.c_str());
    }
    catch (const rmscore::exceptions::RMSException&amp; e) {
    AddLog(&quot;ERROR: &quot;, e.what());
    
    outFile-&gt;close();
    remove(fileOut.c_str());
    }
    inFile-&gt;close();
    outFile-&gt;close();
    }


**使用從範本建立的原則保護檔案**
**來源**︰[rms\_sample/pfileconverter.cpp](https://github.com/AzureAD/rms-sdk-for-cpp/tree/master/samples/rms_sample)

**描述**︰擷取與使用者相關聯的範本清單，然後使用選取的範本建立原則，接著使用該原則保護檔案。

**C++**︰

    void PFileConverter::ConvertToPFileTemplates(const string           &amp; userId,
                                             shared_ptr&lt;istream&gt;      inStream,
                                             const string           &amp; fileExt,
                                             std::shared_ptr&lt;iostream&gt;outStream,
                                             IAuthenticationCallback&amp; auth,
                                             IConsentCallback&amp; /*consent*/,
                                             ITemplatesCallback     &amp; templ)
    {
    auto templates = TemplateDescriptor::GetTemplateList(userId, auth);
    
    rmscore::modernapi::AppDataHashMap signedData;
    
    size_t pos = templ.SelectTemplate(templates);
    
    if (pos &lt; templates.size()) {
    auto policy = UserPolicy::CreateFromTemplateDescriptor(
      templates[pos],
      userId,
      auth,
      USER_AllowAuditedExtraction,
      signedData);
   
    ConvertToPFileUsingPolicy(policy, inStream, fileExt, outStream);
    }
    }

**保護指定原則的檔案**
**來源**︰[rms\_sample/pfileconverter.cpp](https://github.com/AzureAD/rms-sdk-for-cpp/tree/master/samples/rms_sample)

**描述**︰使用指定的原則建立受保護的檔案資料流，然後保護該檔案。

**C++**︰

    void PFileConverter::ConvertToPFileUsingPolicy(shared_ptr&lt;UserPolicy&gt;   policy,
                                               shared_ptr&lt;istream&gt;      inStream,
                                               const string           &amp; fileExt,
                                               std::shared_ptr&lt;iostream&gt;outStream)
    {
    if (policy.get() != nullptr) {
    auto outIStream = rmscrypto::api::CreateStreamFromStdStream(outStream);
    auto pStream    = ProtectedFileStream::Create(policy, outIStream, fileExt);
    
    // preparing
    readPosition  = 0;
    writePosition = pStream-&gt;Size();
    
    inStream-&gt;seekg(0, ios::end);
    totalSize = inStream-&gt;tellg();
    
    // start threads
    for (size_t i = 0; i &lt; THREADS_NUM; ++i) {
      threadPool.push_back(thread(WorkerThread,
                                  static_pointer_cast&lt;iostream&gt;(inStream),
                                  pStream,
                                  true));
    }
    
    for (thread&amp; t: threadPool) {
      if (t.joinable()) {
        t.join();
      }
    }
    
    pStream-&gt;Flush();
    }
    


## 案例︰使用自訂保護來保護檔案

**使用自訂保護來保護檔案**
**來源**：[rms\_sample/mainwindow.cpp](https://github.com/AzureAD/rms-sdk-for-cpp/tree/master/samples/rms_sample)

**描述**︰從使用者取得檔案名稱、讀取憑證 (請參閱 *MainWindow::addCertificates*)、從使用者收集權限資訊並利用用戶端識別碼和重新導向 URL 設定授權回呼之後，可透過呼叫 *ConvertToPFilePredefinedRights* (請參閱下列程式碼範例) 保護選取的檔案。

**C++**︰

    void MainWindow::ConvertToPFILEUsingRights(const string            &amp; fileIn,
                                           const vector&lt;UserRights&gt;&amp; userRights,
                                           const string            &amp; clientId,
                                           const string            &amp; redirectUrl,
                                           const string            &amp; clientEmail)
    {
    // generate output filename
    string fileOut = fileIn + &quot;.pfile&quot;;
    
    // add trusted certificates using HttpHelpers of RMS and Auth SDKs
    addCertificates();
    
    // create shared in/out streams
    auto inFile = make_shared&lt;ifstream&gt;(
    fileIn, ios_base::in | ios_base::binary);
    auto outFile = make_shared&lt;fstream&gt;(
    fileOut, ios_base::in | ios_base::out | ios_base::trunc | ios_base::binary);
    
    if (!inFile-&gt;is_open()) {
    AddLog(&quot;ERROR: Failed to open &quot;, fileIn.c_str());
    return;
    }
    
    if (!outFile-&gt;is_open()) {
    AddLog(&quot;ERROR: Failed to open &quot;, fileOut.c_str());
    return;
    }
    
    // find file extension
    string fileExt;
    auto   pos = fileIn.find_last_of(&#39;.&#39;);
    
    if (pos != string::npos) {
    fileExt = fileIn.substr(pos);
    }
    
    // is anything to add
    if (userRights.size() == 0) {
    AddLog(&quot;ERROR: &quot;, &quot;Please fill email and check rights&quot;);
    return;
    }
    
    
    try {
    // create authentication callback
    AuthCallback auth(clientId, redirectUrl);
    
    // process convertion
    PFileConverter::ConvertToPFilePredefinedRights(
      clientEmail,
      inFile,
      fileExt,
      outFile,
      auth,
      this-&gt;consent,
      userRights);
    
    AddLog(&quot;Successfully converted to &quot;, fileOut.c_str());
    }
    catch (const rmsauth::Exception&amp; e) {
    AddLog(&quot;ERROR: &quot;, e.error().c_str());
    
    outFile-&gt;close();
    remove(fileOut.c_str());
    }
    catch (const rmscore::exceptions::RMSException&amp; e) {
    AddLog(&quot;ERROR: &quot;, e.what());
    
    outFile-&gt;close();
    remove(fileOut.c_str());
    }
    inFile-&gt;close();
    outFile-&gt;close();
    }


**建立保護原則與提供選取的權限給使用者**
**來源**︰[rms\_sample/pfileconverter.cpp](https://github.com/AzureAD/rms-sdk-for-cpp/tree/master/samples/rms_sample)

**描述**︰建立原則描述元，並填入使用者的權限資訊，然後使用原則描述元建立使用者原則。 此原則可用來透過呼叫 *ConvertToPFileUsingPolicy* (請參閱本主題前一節所述的此內容) 保護選取的檔案。

**C++**︰

    void PFileConverter::ConvertToPFilePredefinedRights(
    const string            &amp; userId,
    shared_ptr&lt;istream&gt;       inStream,
    const string            &amp; fileExt,
    shared_ptr&lt;iostream&gt;      outStream,
    IAuthenticationCallback &amp; auth,
    IConsentCallback&amp; /*consent*/,
    const vector&lt;UserRights&gt;&amp; userRights)
    {
    auto endValidation = chrono::system_clock::now() + chrono::hours(48);
    
    
    PolicyDescriptor desc(userRights);
    
    desc.Referrer(make_shared&lt;string&gt;(&quot;https://client.test.app&quot;));
    desc.ContentValidUntil(endValidation);
    desc.AllowOfflineAccess(false);
    desc.Name(&quot;Test Name&quot;);
    desc.Description(&quot;Test Description&quot;);
    
    auto policy = UserPolicy::Create(desc, userId, auth,
                                   USER_AllowAuditedExtraction);
    ConvertToPFileUsingPolicy(policy, inStream, fileExt, outStream);
    

## WorkerThread - 支援的方法


先前的其中兩個範例案例呼叫 *WorkerThread()* 方法；以下列方式**建立受保護的檔案資料流**和**保護指定原則的檔案**︰

**C++**︰

    threadPool.push_back(thread(WorkerThread,
                                  static_pointer_cast&lt;iostream&gt;(outStream), pfs,
                                  false));


**支援的方法，WorkerThread()**

**C++**︰

    static mutex   threadLocker;
    static int64_t totalSize     = 0;
    static int64_t readPosition  = 0;
    static int64_t writePosition = 0;
    static vector&lt;thread&gt; threadPool;
    
    static void WorkerThread(shared_ptr&lt;iostream&gt;           stdStream,
                         shared_ptr&lt;ProtectedFileStream&gt;pStream,
                         bool                           modeWrite) {
    vector&lt;uint8_t&gt; buffer(4096);
    int64_t bufferSize = static_cast&lt;int64_t&gt;(buffer.size());
    
    while (totalSize - readPosition &gt; 0) {
    // lock
    threadLocker.lock();
    
    // check remain
    if (totalSize - readPosition &lt;= 0) {
      threadLocker.unlock();
      return;
    }
    
    // get read/write offset
    int64_t offsetRead  = readPosition;
    int64_t offsetWrite = writePosition;
    int64_t toProcess   = min(bufferSize, totalSize - readPosition);
    readPosition  += toProcess;
    writePosition += toProcess;
    
    // no need to lock more
    threadLocker.unlock();
    
    if (modeWrite) {
      // stdStream is not thread safe!!!
      try {
        threadLocker.lock();
    
        stdStream-&gt;seekg(offsetRead);
        stdStream-&gt;read(reinterpret_cast&lt;char *&gt;(&amp;buffer[0]), toProcess);
        threadLocker.unlock();
        auto written =
          pStream-&gt;WriteAsync(
            buffer.data(), toProcess, offsetWrite, std::launch::deferred).get();
    
        if (written != toProcess) {
          throw rmscore::exceptions::RMSStreamException(&quot;Error while writing data&quot;);
        }
      }
      catch (exception&amp; e) {
        qDebug() &lt;&lt; &quot;Exception: &quot; &lt;&lt; e.what();
      }
    } else {
      auto read =
        pStream-&gt;ReadAsync(&amp;buffer[0],
                           toProcess,
                           offsetRead,
                           std::launch::deferred).get();
    
      if (read == 0) {
        break;
      }
    
      try {
        // stdStream is not thread safe!!!
        threadLocker.lock();
    
        // seek to write
        stdStream-&gt;seekp(offsetWrite);
        stdStream-&gt;write(reinterpret_cast&lt;const char *&gt;(buffer.data()), read);
        threadLocker.unlock();
      }
      catch (exception&amp; e) {
        qDebug() &lt;&lt; &quot;Exception: &quot; &lt;&lt; e.what();
      }
    }
    }
    }


## 案例︰RMS 驗證

下列範例會示範兩種不同的驗證方法；使用和不使用 UI 取得 Azure 驗證 oAuth2 權杖。
**利用 UI 取得 oAuth2 驗證權杖**
**來源**：[rmsauth\_sample/mainwindow.cpp](https://github.com/AzureAD/rms-sdk-for-cpp/tree/master/samples/rmsauth_sample)

**步驟 1**︰建立 **rmsauth::FileCache** 物件的共用點。
描述︰您可以設定快取路徑或使用預設值。

**C++**︰

    auto FileCachePtr = std::make_shared&lt; rmsauth::FileCache&gt;();


**步驟 2**︰建立 **rmsauth::AuthenticationContext** 物件
描述︰指定 Azure *授權單位 URI* 和 *FileCache* 物件。

**C++**︰

    AuthenticationContext authContext(
                              std::string(“https://sts.aadrm.com/_sts/oauth/authorize”),
                              AuthorityValidationType::False,
                              FileCachePtr);


**步驟 3**︰呼叫 **authContext** 物件的 **aquireToken** 方法，並指定下一個參數︰
描述:

-   *要求的資源* - 您想要存取的受保護資源
-   *用戶端唯一識別碼* - 通常是 GUID
-   *重新導向 URI* - 擷取驗證權杖之後重新解決的 URI
-   *驗證提示行為* - 如果您設定 **PromptBehavior::Auto**，程式庫會嘗試使用快取並在必要時重新整理權杖
-   *使用者識別碼* - 提示字元視窗中顯示的使用者名稱

**C++**︰

    auto result = authContext.acquireToken(
                std::string(“api.aadrm.com”),
                std::string(“4a63455a-cfa1-4ac6-bd2e-0d046cf1c3f7”),
                std::string(“https://client.test.app”),
                PromptBehavior::Auto,
                std::string(“john.smith@msopentechtest01.onmicrosoft.com”));


**步驟 4**︰從結果取得存取權杖
描述︰呼叫 **result-&gt; accessToken()** 方法

**注意**  任何驗證程式庫方法都可能會引發 **rmsauth::Exception**

 
**不利用 UI 取得 oAuth2 驗證權杖**
**來源**：[rmsauth\_sample/mainwindow.cpp](https://github.com/AzureAD/rms-sdk-for-cpp/tree/master/samples/rmsauth_sample)

**步驟 1**︰建立 **rmsauth::FileCache** 物件的共用點
描述︰您可以設定快取路徑或使用預設值

**C++**︰

    auto FileCachePtr = std::make_shared&lt; rmsauth::FileCache&gt;();


**步驟 2**︰ 建立 **UserCredential** 物件
描述︰指定*使用者登入*和*密碼*

**C++**︰

    auto userCred = std::make_shared&lt;UserCredential&gt;(&quot;john.smith@msopentechtest01.onmicrosoft.com&quot;,
                                                 &quot;SomePass&quot;);


**步驟 3**︰建立 **rmsauth::AuthenticationContext** 物件
描述︰指定 Azure *授權單位 URI* 和 *FileCache* 物件

**C++**︰

    AuthenticationContext authContext(
                        std::string(“https://sts.aadrm.com/_sts/oauth/authorize”),
                        AuthorityValidationType::False,
                        FileCachePtr);


**步驟 4**︰呼叫 **authContext** 的 **aquireToken** 方法，並指定參數︰
-   *要求的資源* - 您想要存取的受保護資源
-   *用戶端唯一識別碼* - 通常是 GUID
-   *使用者認證* - 傳遞建立的物件

**C++**︰

    auto result = authContext.acquireToken(
                std::string(“api.aadrm.com”),
                std::string(“4a63455a-cfa1-4ac6-bd2e-0d046cf1c3f7”),
                userCred);


**步驟 5**︰從結果取得存取權杖
描述︰呼叫 **result-&gt; accessToken()** 方法

**注意**  任何驗證程式庫方法都可能會引發 **rmsauth::Exception**



<!--HONumber=Apr16_HO4-->


