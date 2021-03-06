
---

copyright:
 years: 2015, 2017

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# 步驟 2：取得通知提供者認證
{: #push_step_1}
前次更新：2017 年 6 月 27 日
{: .last-updated}

若要設定 {{site.data.keyword.mobilepushshort}} 服務，您需要從推送通知提供者取得需要的認證。 

## Android
{: #push_step_1_android}

Firebase Cloud Messaging (FCM) 是用來將推送通知遞送至 Android 裝置、Google Chrome 瀏覽器及 Chrome Apps & Extensions 的閘道。若要在主控台上設定 {{site.data.keyword.mobilepushshort}} 服務，您需要取得 FCM 認證（寄件者 ID 及 API 金鑰）。 

API 金鑰會安全地儲存並供 {{site.data.keyword.mobilepushshort}} Service 用來連接至 FCM 伺服器，而適用於 Google Chrome 及 Mozilla Firefox 的 Android SDK 及 JS SDK 在用戶端上使用「傳送端 ID」（專案號碼）。 

若要設定 FCM 並取得認證，請完成下列步驟：

1. 造訪 [Firebase 主控台 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://console.firebase.google.com/?pli=1){: new_window}。Google 使用者帳戶是必要的。 
2. 選取**新增專案**。 
3. 在「建立專案」視窗中，提供專案名稱、選擇國家/地區，然後按一下**建立專案**。
3. 在導覽窗格中，按一下**設定** > **專案設定**。
4. 選擇 Cloud Messaging 標籤，以取得專案認證 -「伺服器 API 金鑰」及「寄件者 ID」。請注意，FCM 中列出的伺服器金鑰與「伺服器 API 金鑰」相同。
   
	![取得 FCM 的認證](images/FCM_settings_2.jpg)

您也需要產生 `google-services.json` 檔案。請完成下列步驟：

1. 在 Firebase 主控台中，按一下**專案設定**圖示。
    
	![Firebase 專案設定](images/FCM_settings_6.jpg)

3. 從應用程式窗格的「一般」標籤中，選取**新增應用程式**或**將 Firebase 新增至 Android 應用程式**圖示。
    
4. 在「將 Firebase 新增至 Android 應用程式」視窗中，先新增 **com.ibm.mobilefirstplatform.clientsdk.android.push** 作為「套件名稱」。應用程式暱稱欄位是選用性的。按一下**註冊應用程式**。 
    
	![「將 Firebase 新增至 Android 應用程式」視窗](images/FCM_1.jpg)

5. 現在，在「將 Firebase 新增至 Android 應用程式」視窗中輸入套件名稱，以包含應用程式的套件名稱。應用程式暱稱欄位是選用性的。按一下**註冊應用程式**。以下是範例：

	![新增應用程式的套件名稱](images/FCM_settings_4.jpg)

6. 會產生 `google-services.json` 檔案。 


取得 FCM 認證並產生 `google-services.json` 檔案之後，下一步是要[建立服務實例](push_step_2.html)。

**附註**：Google 已淘汰 GCM，並且已和 Firebase 整合 Cloud Messaging。您必須將 Android 上的 GCM 用戶端應用程式移轉至 FCM。

## iOS
{: #push_step_1_ios}

對於 iOS 裝置及應用程式，Apple Push Notification Service (APNs) 容許應用程式開發人員將遠端通知從 IBM Cloud（提供者）上的 {{site.data.keyword.mobilepushshort}} 服務實例傳送給 iOS 裝置及應用程式。訊息會傳送至裝置上的目標應用程式。 

您需要取得並配置 APNs 認證。APNs 憑證是透過 {{site.data.keyword.mobilepushshort}} Service 安全地進行管理，並且用來以提供者身分連接至 APNs 伺服器。


### 登錄應用程式 ID
{: #push_step_1_ios_2}

「應用程式 ID」（軟體組 ID）是可識別特定應用程式的唯一 ID。每一個應用程式都需要「應用程式 ID」。{{site.data.keyword.mobilepushshort}} Service 這類服務會配置成「應用程式 ID」。

請確定您有一個 [Apple Developers ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://developer.apple.com/){: new_window} 帳戶。這是必要項目。

2. 移至 [Apple Developer ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://developer.apple.com){: new_window} 入口網站，按一下 **Member Center**，然後選取 **Certificates, Identifiers & Profiles**。
3. 移至 **Identifiers** > **App IDs section**。
3. 在 **Registering App IDs** 頁面的 App ID Description Name 欄位提供應用程式名稱。例如：ACME Push Notifications。
4. 提供 App ID Prefix 的字串。  
4. 針對 App ID Suffix，選擇 **Explicit App ID** 然後提供 Bundle ID 值。建議您提供反向網域名稱樣式的字串。例如：`com.ACME.push`。
5. 選取 **Push Notifications** 勾選框，然後按一下 **Continue**。
6. 檢查您的設定，然後按一下 **Register** > **Done**。

您的應用程式 ID 現在已登錄。 

   ![已登錄應用程式 ID](images/push_ios_register_appid.jpg)
  

### 建立開發及配送 APNs SSL 憑證
{: #push_step_1_ios_3}

您必須先產生憑證簽署要求 (CSR) 並將它提交給 Apple（憑證管理中心 (CA)），才能取得 APNs 憑證。CSR 所含的資訊可識別您的公司，以及用來簽署 Apple Push Notifications 的公開和私密金鑰。然後，在「iOS 開發者入口網站」上產生 SSL 憑證。憑證以及其公開和私密金鑰都儲存在「金鑰鏈存取」中。

您可以透過兩種模式使用 APNs： 

* 沙盤推演模式，用於進行開發及測試。
* 正式作業模式，在透過「應用程式市集」（或其他企業配送機制）配送應用程式時使用。

您必須取得開發及配送環境的個別憑證。憑證是與接收遠端通知之應用程式的「應用程式 ID」相關聯。對於正式作業，您最多可以建立兩個憑證。IBM Cloud 使用憑證來建立與 APNs 的 SSL 連線。

<!-- Create a development and distribution SSL certificate. -->

1. 移至 [Apple Developer ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://developer.apple.com){: new_window} 網站，按一下 **Member Center**，然後選取 **Certificates, Identifiers & Profiles**。
2. 在 **Identifiers** 區域中，按一下 **App IDs**。
3. 從 App IDs 清單中，選取您的應用程式 ID，然後選取 **Edit**。
4. 選取 **Push Notifications** 勾選框，然後：
	-  在 Development SSL certificate 窗格，按一下 **Create Certificate..**。
	-  在 Production SSL certificate 窗格，按一下 **Create Certificate..**。

	![Push Notification SSL 憑證](images/certificate_createssl.jpg)

5. 顯示 **About Creating a Certificate Signing Request (CSR) screen** 畫面時，請在 Mac 上啟動 **Keychain Access** 應用程式，以建立「憑證簽署要求 (CSR)」。按一下 **Continue**。
6. 針對 Upload CSR file 選項，按一下 **Choose File**，然後選取檔案 `CertificateSigningRequest.certSigningRequest`。 
7. 按一下 **Continue**。
8. 在 Download, Install and Backup 窗格，按一下 **Download**。便會下載 `aps_development.cer` 檔案。
	
	![下載憑證](images/push_certificate_download.jpg)	
	
6. 從功能表中，選取**金鑰鏈存取 > 憑證助理 > 從憑證管理中心要求憑證...** 
7. 在**憑證資訊**中，輸入與「應用程式開發人員」帳戶及通用名稱相關聯的電子郵件位址。請提供有意義的名稱，協助您識別它是用於開發（沙盤推演）還是配送（正式作業）的憑證；例如，_sandbox-apns-certificate_ 或 _production-apns-certificate_。
8. 選取**儲存至磁碟**，以將 `.certSigningRequest` 檔案下載至您的桌面，然後按一下**繼續**。
9. 在**另存新檔**功能表選項中，命名 `.certSigningRequest` 檔案，然後按一下**儲存**。
10. 按一下**完成**。您現在有 CSR。
11. 回到**關於建立憑證簽署要求 (CSR)** 視窗，然後按一下**繼續**。 
12. 從**產生**畫面中，按一下**選擇檔案...**，然後選取您儲存在桌面上的 CSR 檔案。然後按一下 **Generate**。

	![產生憑證](images/generate_certificate.jpg)
13. 您的憑證備妥之後，請按一下**完成**。
14. 在 **Push Notifications** 畫面上，按一下 **Download** 以下載您的憑證，然後按一下 **Done**。 
	
	![下載憑證](images/certificate_download.jpg)

15. 在 Mac 上，移至**金鑰鏈存取 > 我的憑證**，然後尋找新安裝的憑證。按兩下憑證，以將它安裝至「金鑰鏈存取」。
16. 選取憑證及私密金鑰，然後選取 **Export**，以將憑證轉換為個人資訊交換格式（`.p12` 格式）。


	![匯出憑證及金鑰](images/keychain_export_key.jpg)
17. 在**另存新檔**欄位中，提供有意義的憑證名稱（例如，`sandbox_apns.p12_certifcate` 或 `production_apns.p12`），然後按一下 **Save**。

	
	![匯出憑證及金鑰](images/certificate_p12v2.jpg)
18. 在**輸入密碼**欄位中，輸入密碼以保護匯出的項目，然後按一下**確定**。您可以使用此密碼，在 Push Notifications 服務主控台上配置 APNs 設定。
	
	![匯出憑證及金鑰](images/export_p12.jpg)
19. **Key Access.app** 會提示您從**金鑰鏈**畫面匯出金鑰。請輸入您的管理密碼，以便 Mac 容許您的系統匯出這些項目，然後選取**一律容許**選項。`.p12` 憑證會在桌面上產生。


### 建立開發佈建設定檔
{: #create-push-credentials-dev-profile}

佈建設定檔與「應用程式 ID」搭配使用，以判定可安裝及執行應用程式的裝置以及您的應用程式可存取的服務。對於每一個「應用程式 ID」，您可以建立兩個佈建設定檔：一個用於開發，另一個用於配送。Xcode 使用開發佈建設定檔來判定容許建置應用程式的開發人員，以及容許在應用程式上進行測試的裝置。

請確定您已登錄「應用程式 ID」、已針對 {{site.data.keyword.mobilepushshort}} 服務予以啟用，以及配置它來使用開發及正式作業 APNs SSL 憑證。

建立開發佈建設定檔，如下所示：

1. 移至 [Apple Developer ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://developer.apple.com){: new_window} 入口網站，按一下 **Member Center**，然後選取 **Certificates, Identifiers & Profiles**。
2. 移至 [Mac Developer Library ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://developer.apple.com/library/mac/documentation/IDEs/Conceptual/AppDistributionGuide/MaintainingProfiles/MaintainingProfiles.html#//apple_ref/doc/uid/TP40012582-CH30-SW62site){: new_window}，捲動至 **Creating Development Provisioning Profiles** 區段，並遵循指示以建立開發設定檔。
**附註**：配置開發佈建設定檔時，請選取下列選項：
	* **iOS 應用程式開發**
	* **對於 iOS 及 watchOS 應用程式**


### 建立市集配送佈建設定檔
{: #create-push-credentials-apns-distribute_profile}

使用市集佈建設定檔，將要進行配送的應用程式提交給「應用程式市集」。

1. 移至 [Apple Developer ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://developer.apple.com){: new_window} 入口網站，按一下 **Member Center**，然後選取 **Certificates, Identifiers & Profiles**。
2. 按兩下下載的佈建設定檔，以將它安裝至 Xcode。

取得認證之後，下一步是要[配置服務實例](push_step_2.html)。

## Web 瀏覽器及 Chrome Apps & Extensions
{: #configure-credential-for-browsers}

IBM {{site.data.keyword.mobilepushshort}} 服務已擴充功能，可將通知傳送至您的瀏覽器以及 Chrome Apps & Extensions。

{{site.data.keyword.mobilepushshort}} 服務需要您網站的網站 URL 或網域名稱，以識別需要被容許的要求。 

例如，`https://www.acmebanks.com`

{{site.data.keyword.mobilepushshort}} 服務實例一次僅支援一個網域名稱。因此，請確保針對 Chrome、Firefox 及 Safari 設定相同的值。Chrome 及 Safari 瀏覽器需要其他配置才能進行 Web 推送。您將需要 FCM API 金鑰用作 FCM 端點，用來在 Chrome 中遞送訊息。 

若要針對 Chrome、Firefox 瀏覽器及 Chrome Apps & Extensions 設定服務，請參閱[配置服務實例](push_step_2.html)。


### Safari Web 推送的配置 
{: #configure-safari}

Safari 上 {{site.data.keyword.mobilepushshort}} 服務的支援版本為 10.0。需要透過您的 Apple Developer 帳戶產生憑證，才能配置您的瀏覽器來接收通知。

#### 產生憑證
{: #certificate-generation}

請確定您具有 Apple Developer 帳戶。您需要登錄一個 Website Push ID 並產生一個憑證，才能配置 Safari 瀏覽器來接收通知。下列步驟將協助您開始使用。

1. 在 Apple Developer Member Center 中，按一下 **Certificates, ID & Profiles**。 
2. 依序按一下 **Identifiers** 及 **Website Push IDs**。
3. 選取加號圖示來選擇建立新的項目。
  ![Push Notifications 主控台](images/safari_1.jpg)

4. 在 Register Website Push ID 畫面中，提供適當的 Website Push ID 說明及識別 ID。建議採用反向網域名稱格式，起始於 `web`。例如：`web.com.acmebanks`。
5. 登錄 Website Push ID。您現在有了自己的 Website Push ID。 
6. 選取 **Edit** 以建立憑證，用於 Website Push ID。
7. 在 Certificate Information 的 Certificate Assistant 視窗中，提供您的電子郵件 ID 及通用名稱。讓 Certificate Authority 的電子郵件位址保留為空白。
8. 按一下 **Save to disk**，然後選取 **Continue**。
9. 選擇將憑證儲存至適當的資料夾。
10. 選擇在精靈中被提示產生憑證時，在磁碟上建立的 `.certSigningRequest`。請確定您下載以 `. cer` 格式建立的網站推送憑證。
11. 在 KeyChain Access 工具中開啟憑證。按一下滑鼠右鍵並匯出為 p12 憑證。請記下在產生 p12 憑證的期間所提供的密碼。

產生憑證之後，下一步是要[配置服務實例](push_step_2.html)。

