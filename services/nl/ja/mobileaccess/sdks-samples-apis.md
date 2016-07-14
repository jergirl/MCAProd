---

copyright:
  years: 2015, 2016

---

{:shortdesc: .shortdesc}

# {{site.data.keyword.amashort}} SDK、サンプル、API リファレンス
*最終更新日: 2016 年 4 月 30 日*
{: .last-updated}

{{site.data.keyword.amashort}} SDK をアプリに追加するには、使用する SDK を選択し、依存関係マネージャーを構成して SDK をアプリにプルします。
{:shortdesc}

## Core SDK
{: #coresdk}
Core SDK には、モバイル・アプリでのカスタム認証、モニタリング、およびロギングを可能にするための API が含まれています。

### Android
{: #coresdk-android}
[Git リポジトリー](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-android-core)、
[API リファレンス](https://console.{DomainName}/docs/api/content/api/mobilefirst/android/core-api-doc/overview-summary.html)

#### Gradle を使用した Core SDK のインストール
{: #coresdk-android-gradle}

```Gradle
    compile group: 'com.ibm.mobilefirstplatform.clientsdk.android',    
    	name:'core',
    	version: '1.+',
    	ext: 'aar',
    	transitive: true
```

### iOS (Swift SDK)
{: #coresdk-ios-swift}

[Git リポジトリー](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-security)

#### CocoaPods を使用した Core SDK のインストール
{: #coresdk-ios-siwft-cocoapods}

```
use_frameworks!
pod 'BMSSecurity'
 ```

### iOS (Objective-C SDK)
{: #coresdk-ios}

Objective-C SDK は現在も完全にサポートされており、{{site.data.keyword.Bluemix_notm}} モバイル・サービス用の主要 SDK とされていますが、今年後半には廃止され、新しい Swift SDK が後継になる予定です ([iOS Swift SDK のセットアップ](getting-started-ios-swift-sdk.html) を参照してください)。

[Git リポジトリー](https://hub.jazz.net/git/bluemixmobilesdk/imf-ios-sdk/archive?revstr=master)、
[API リファレンス](https://console.{DomainName}/docs/api/content/api/mobilefirst/ios/IMFCore_api-doc/html/index.html)

#### CocoaPods を使用した Core SDK のインストール
{: #coresdk-ios-cocoapods}

```Bash
pod 'IMFCore'
```

### Cordova
{: #coresdk-cordova}

[Git リポジトリーおよび API リファレンス](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-cordova-plugin-core)

#### Cordova CLI を使用した Core SDK のインストール
{: #coresdk-cordova-cli}

```Bash
cordova plugin add ibm-mfp-core
```

## Facebook 認証用の {{site.data.keyword.amashort}} Client SDK
{: #facebooksdk}

### Android
{: #facebooksdk-android}

[Git リポジトリー](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-android-security-facebookauthentication)、
[API リファレンス](https://console.{DomainName}/docs/api/content/api/mobilefirst/android/facebook-api-doc/index.html)

#### Gradle を使用した Facebook SDK のインストール
{: #facebooksdk-android-gradle}

```Gradle
    compile group: 'com.ibm.mobilefirstplatform.clientsdk.android',    
    	name:'facebookauthentication',
    	version: '2.+',
    	ext: 'aar',
    	transitive: true
```

### iOS (Swift SDK)
{: #facebooksdk-ios-swift}

[Git リポジトリー](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-security-facebookauthentication)

#### CocoaPods を使用した Facebook SDK のインストール
{: #facebooksdk-ios-swift-cocoapods}

```
use_frameworks!
pod 'BMSFacebookAuthentication'
 ```

### iOS (Objective-C SDK)
{: #facebooksdk-ios}

[Git リポジトリー](https://hub.jazz.net/git/bluemixmobilesdk/imf-ios-sdk.git)、
[API リファレンス](https://console.{DomainName}/docs/api/content/api/mobilefirst/ios/IMFFacebookAuthentication_api-doc/html/index.html)

*注:* Objective-C SDK は現在も完全にサポートされており、{{site.data.keyword.Bluemix_notm}} モバイル・サービス用の主要 SDK とされていますが、この SDK は今年後半には廃止され、新しい Swift SDK が後継になる予定です。新規アプリケーションには Swift SDK を使用することを強くお勧めします (『iOS Swift SDK のセットアップ』を参照してください)。
#### CocoaPods を使用した Facebook SDK のインストール
{: #facebooksdk-ios-cocoapods}

```Bash
pod 'IMFFacebookAuthentication'```

### Cordova
{: #facebooksdk-cordova}

[Github リポジトリーおよび API リファレンス](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-cordova-plugin-core)

#### Cordova CLI を使用した Facebook SDK のインストール
{: #facebooksdk-cordova-cli}

```Bash
cordova plugin add ibm-mfp-core```

## Google 認証用の {{site.data.keyword.amashort}} Client SDK
{: #googlesdk}

### Android
{: #googlesdk-android}

[Github リポジトリー](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-android-security-googleauthentication)、
[API リファレンス](https://console.{DomainName}/docs/api/content/api/mobilefirst/android/google-api-doc/index.html)

#### Gradle を使用した Google+ SDK のインストール
{: #googlesdk-android-gradle}

```Gradle
compile group: 'com.ibm.mobilefirstplatform.clientsdk.android',    
    	name:'googleauthentication',
    	version: '2.+',
    	ext: 'aar',
    	transitive: true
```

### iOS (Swift SDK)
{: #googlesdk-ios-swift}

[Git リポジトリー](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-security-googleauthentication)

#### CocoaPods を使用した Google+ SDK のインストール
{: #googlesdk-ios-swift-cocoapods}

```
use_frameworks!
pod 'BMSGoogleAuthentication'
```

### iOS (Objective-C SDK - 非推奨)
{: #googlesdk-ios}

[Git リポジトリー](https://hub.jazz.net/git/bluemixmobilesdk/imf-ios-sdk.git)、
[API リファレンス](https://console.{DomainName}/docs/api/content/api/mobilefirst/ios/IMFGoogleAuthentication_api-doc/html/index.html)

#### CocoaPods を使用した Google+ SDK のインストール
{: #googlesdk-ios-cocoapods}

```Bash
pod 'IMFGoogleAuthentication'```

### Cordova
{: #googlesdk-cordova}

[Git リポジトリーおよび API リファレンス](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-cordova-plugin-core)

#### Cordova CLI を使用した Google+ SDK のインストール
{: #googlesdk-cordova-cli}

```Bash
cordova plugin add ibm-mfp-core```

## {{site.data.keyword.amashort}} Server SDK for Node.js サーバー
{: #serversdk}

[Git リポジトリー](https://github.com/ibm-bluemix-mobile-services/bms-mca-token-validation-strategy)

#### npm を使用した Server SDK のインストール
{: #serversdk-npm}

```Bash
npm install -save bms-mca-token-validation-strategy
```

## {{site.data.keyword.amashort}} Server SDK for Liberty for Java&trade; サーバー
{: #serverlibertysdk}

[TAI 成果物のダウンロード](https://imf-tai.{DomainName}/public/TAI.zip)

## {{site.data.keyword.amashort}} Node.js OAuth SDK
{: #serverlibertysdk-github}

[Git リポジトリー](https://github.com/ibm-bluemix-mobile-services/bms-mca-oauth-sdk)

#### npm を使用した OAuth SDK のインストール
{: #oauthsdk}

```Bash
npm install -save bms-mca-oauth-sdk
```

## カスタム ID プロバイダーのサンプル
{: #customidprovider}

[簡単なサンプル Git リポジトリー](https://github.com/ibm-bluemix-mobile-services/bms-mca-custom-identity-provider-sample)
[高度なサンプル Git リポジトリー](https://github.com/ibm-bluemix-mobile-services/bms-mca-custom-identity-provider-with-user-management)

## IMFURLProtocol
{: #IMFURLProtocol}

[API リファレンス](https://console.{DomainName}/docs/api/content/api/mobilefirst/ios/IMFURLProtocol_api-doc/html/index.html)

#### CocoaPods を使用した IMFURLProtocol のインストール
{: #IMFURLProtocol-cocoapods}

```Bash
pod 'IMFURLProtocol'
```