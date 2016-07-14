---

copyright:
  years: 2016

---
{:screen: .screen}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}

# iOS アプリ用の Facebook 認証の使用可能化 (Swift SDK)
{: #facebook-auth-ios}

*最終更新日: 2016 年 6 月 15 日*
{: .last-updated}

iOS アプリケーションで Facebook を ID プロバイダーとして使用するには、iOS プラットフォームを追加して Facebook アプリケーション用に構成する必要があります。
{:shortdesc}

## 開始する前に
{: #facebook-auth-ios-before}
以下が必要です。
* CocoaPods と連動して機能するようにセットアップされた iOS プロジェクト。詳しくは、[iOS Swift SDK のセットアップ](https://console.{DomainName}/docs/services/mobileaccess/getting-started-ios-swift-sdk.html)の **CocoaPods のインストール**を参照してください。
   **注:** 先に進む前にコア {{site.data.keyword.amashort}} Client SDK をインストールする必要はありません。
* {{site.data.keyword.amashort}} サービスによって保護された {{site.data.keyword.Bluemix_notm}} アプリケーションのインスタンス。{{site.data.keyword.Bluemix_notm}} バックエンドの作成方法について詳しくは、[入門](index.html)を参照してください。
* Facebook Application ID。詳しくは、[Facebook Developer Portal から Facebook アプリケーション ID を取得する](https://console.{DomainName}/docs/services/mobileaccess/facebook-auth-overview.html#facebook-appID)を参照してください。


**重要:** Facebook 自体の SDK を別個にインストールする必要はありません。Facebook SDK は、下記の `BMSFacebookAuthentication` pod によって自動的にインストールされます。**Facebook Developer Portal** の **Xcode プロジェクトへの Facebook SDK の追加**のステップはスキップできます。

**注:** Objective-C SDK は現在も完全にサポートされており、{{site.data.keyword.Bluemix_notm}} モバイル・サービス用の主要 SDK とされていますが、今年後半には廃止され、この新しい Swift SDK が後継になる予定です。
## iOS プラットフォーム用の Facebook アプリケーションの構成
{: #facebook-auth-ios-config}

1. [自分の Facebook アプリのダッシュボード](https://developers.facebook.com/apps/)にログインします。

1. アプリの**アプリ ID** のメモを取ります。iOS プロジェクトを Facebook 認証用に構成するときに、この値が必要になります。

1. **「設定 (Settings)」>「プラットフォームの追加 (Add Platform)」>「iOS」**とクリックします。

1. iOS アプリケーションの *bundleId* を指定します。ご使用の iOS アプリケーションの *bundleId* を調べるには、`info.plist` ファイル内または Xcode プロジェクトの**「一般 (General)」**タブ内で**「バンドル ID (Bundle Identifier)」**を探します。
**ヒント**: これらの機能を使用する予定がある場合は、URL スキーム・サフィックスまたはシングル・サインオンを使用可能にすることを検討してください。

1. **「設定の保存」**をクリックします。

## Facebook 認証用の {{site.data.keyword.amashort}} の構成
{: #facebook-auth-ios-configmca}

Facebook Application ID および Facebook アプリケーションを iOS クライアントに対して機能するよう構成したら、{{site.data.keyword.amashort}} で Facebook 認証を使用可能にすることができます。

1. {{site.data.keyword.Bluemix}}ダッシュボードでアプリを開きます。

1. **「モバイル・オプション」**をクリックし、**「経路」** (*applicationRoute*) と **「アプリ GUID」** (*applicationGUID*) のメモを取ります。SDK を初期化する際に、これらの値が必要になります。

1. {{site.data.keyword.amashort}} タイルをクリックします。{{site.data.keyword.amashort}} ダッシュボードがロードされます。

1. **「Facebook」**タイルをクリックします。

1. Facebook Application ID を指定して**「保存」**をクリックします。

## iOS 用の {{site.data.keyword.amashort}} Client SDK の構成
{: #facebook-auth-ios-sdk}

### CocoaPods のインストール
{: #install-cocoapods}

1. 端末を開き、**pod --version** コマンドを実行します。既に CocoaPods がインストールされている場合は、バージョン番号が表示されます。次のセクションにスキップして SDK をインストールできます。

1. CocoaPods をインストールしていない場合は、以下を実行します。

```
sudo gem install cocoapods```
詳細については、[CocoaPods の Web サイト](https://cocoapods.org/)を参照してください。### CocoaPods を使用した {{site.data.keyword.amashort}} Client Swift SDK のインストール
{: #facebook-auth-install-swift-cocoapods}

1. iOS プロジェクト内に `Podfile` がない場合、`pod init` を実行してファイルを作成します。

1. `Podfile` を編集して以下の行を追加します。

 ```
use_frameworks!
pod 'BMSFacebookAuthentication'

	```

   **注:** Pod file 内に行 `pod 'BMSSecurity'` がある場合、その行を削除する必要があります。`BMSFacebookAuthentication` pod は、必要なすべてのフレームワークをインストールします。

   **ヒント:** `use_frameworks!` を、Podfile に含めるのではなく、Xcode ターゲットに追加できます。

1. `Podfile` を保存して、コマンド・ラインから `pod install` コマンドを実行します。CocoaPods は依存関係をインストールします。進行状況および追加されたコンポーネントが表示されます。

 **重要**: この時点で、CocoaPods によって生成された `xcworkspace` ファイルを使用してプロジェクトを開く必要があります。通常、名前は `{your-project-name}.xcworkspace` です。  

1. コマンド・ラインから `open {your-project-name}.xcworkspace` を実行して、iOS プロジェクトのワークスペースを開きます。

### Facebook 認証用の iOS プロジェクトの構成
{: #facebook-auth-ios-configproject}

1. `info.plist` ファイルを見つけます。このファイルは、通常、Xcode プロジェクトの `Supporting files` フォルダーにあります。

1. `info.plist` ファイルに以下のプロパティーを追加して、Facebook 統合を構成します。

   ![image](images/ios-facebook-infoplist-settings.png)


   Facebook Application ID を使用して URL スキームおよび FacebookappID プロパティーを更新します

   `info.plist` ファイルの更新は、このファイルを右クリックし、**「指定して開く」>「ソース・コード」**を選択して以下の XML を追加することでも行えます。

   ```XML
	<key>CFBundleURLTypes</key>
	<array>
		<dict>
			<key>CFBundleURLSchemes</key>
			<array>
				<string>fb{your-facebook-application-id}</string>
			</array>
		</dict>
	</array>
	<key>FacebookAppID</key>
	<string>{your-facebook-application-id}</string>
	<key>FacebookDisplayName</key>
	<string>{your-faceebook-application-name}</string>
	<key>LSApplicationQueriesSchemes</key>
	<array>
		<string>fbauth</string>
		<string>fbauth2</string>
	</array>
	<key>NSAppTransportSecurity</key>
	<dict>
	    <key>NSExceptionDomains</key>
	    <dict>
	        <key>facebook.com</key>
	        <dict>
	            <key>NSIncludesSubdomains</key>
	            <true/>                
	            <key>NSThirdPartyExceptionRequiresForwardSecrecy</key>
	            <false/>
	        </dict>
	        <key>fbcdn.net</key>
	        <dict>
	            <key>NSIncludesSubdomains</key>
	            <true/>
	            <key>NSThirdPartyExceptionRequiresForwardSecrecy</key>
	            <false/>
	        </dict>
	        <key>akamaihd.net</key>
	        <dict>
	            <key>NSIncludesSubdomains</key>
	            <true/>
	            <key>NSThirdPartyExceptionRequiresForwardSecrecy</key>
	            <false/>
	        </dict>
	    </dict>
	</dict>
```
   Facebook Application ID を使用して URL スキームおよび FacebookappID プロパティーを更新します。Facebook アプリケーションの名前で FacebookDisplayName を更新します。
**重要**: `info.plist` ファイル内の既存のプロパティーをオーバーライドすることのないようにしてください。重複するプロパティーがある場合は、手動でマージする必要があります。詳しくは、[Xcode プロジェクトの構成 (Configure Xcode Project) ](https://developers.facebook.com/docs/ios/getting-started/)および [iOS9 用のアプリの準備 (Preparing Your Apps for iOS9) ](https://developers.facebook.com/docs/ios/ios9)を参照してください。
## {{site.data.keyword.amashort}} Client Swift SDK の初期化
{: #facebook-auth-ios-initalize-swift}

`applicationGUID` および `applicationRoute` パラメーターを渡すことで、Client SDK を初期化します。初期化コードを入れる場所は一般的に (必須ではありませんが)、アプリケーション代行の `application:didFinishLaunchingWithOptions` メソッドの中です。
1. アプリケーション・パラメーター値を取得します。{{site.data.keyword.Bluemix_notm}}ダッシュボードでアプリを開きます。「**Mobile オプション**」をクリックします。`applicationRoute` と `applicationGUID` の値は、**「経路」**フィールドと**「アプリ GUID」**フィールドに表示されます。
1. 以下のヘッダーを追加することによって、{{site.data.keyword.amashort}} Client SDK を使用したいクラスに、必要なフレームワークをインポートします。

	```swift
 import UIKit
 import BMSCore
 import BMSSecurity
 ```
2. Client SDK を初期化します。`<applicationRoute>` および `<applicationGUID>` を、{{site.data.keyword.Bluemix_notm}} ダッシュボードの**「モバイル・オプション」**から取得した**「経路」**および**「アプリ GUID」**の値に置き換えます。`<applicationBluemixRegion>` を、{{site.data.keyword.Bluemix_notm}} アプリケーションがホストされている地域に置き換えます。{{site.data.keyword.Bluemix_notm}} 地域を表示するには、ダッシュボードの左上隅にある顔アイコン (![face](images/face.jpg "顔アイコン")) をクリックします。

 ```Swift
 let backendURL = "<applicationRoute>"
 let backendGUID = "<applicationGUID>"

 func application(application: UIApplication, didFinishLaunchingWithOptions launchOptions: [NSObject: AnyObject]?) -> Bool {
BMSClient.sharedInstance.initializeWithBluemixAppRoute(backendURL, bluemixAppGUID: backendGUID, bluemixRegion: BMSClient.<applicationBluemixRegion>)

 BMSClient.sharedInstance.authorizationManager = MCAAuthorizationManager.sharedInstance

 FacebookAuthenticationManager.sharedInstance.register()
 ```

1. アプリ代行の ``application:didFinishLaunchingWithOptions`` メソッドに以下のコードを追加することによって、Facebook SDK にアプリのアクティベーションについて通知し、Facebook Authentication Handler を登録します。BMSClient インスタンスを初期化した直後にこのコードを追加し、Facebook を認証マネージャーとして登録します。```Swift
  return FacebookAuthenticationManager.sharedInstance.onFinishLaunching(application, withOptions: launchOptions)
 ```

1. `FacebookAuthenticationManager.swift` ファイルを `BMSFacebookAuthentication` pod ソース・ファイルからプロジェクト・ディレクトリーにコピーします。

1. アプリ代行に以下のコードを追加します。

	```Swift
	func application(application: UIApplication, openURL url: NSURL,
					sourceApplication: String?, annotation: AnyObject) -> Bool {

		return FacebookAuthenticationManager.sharedInstance.onOpenURL(application, url: url, sourceApplication: sourceApplication, annotation: annotation)

	}
 ```

## 認証のテスト
{: #facebook-auth-ios-testing}

Client SDK が初期化され、Facebook 認証マネージャーの登録が完了すると、モバイル・バックエンドに要求を出すことができるようになります。
### 開始する前に
{: #facebook-auth-ios-testing-before}

{{site.data.keyword.mobilefirstbp}} ボイラープレートを使用していて、{{site.data.keyword.amashort}}により`/protected` エンドポイントで保護されているリソースを既に持っている必要があります。`/protected` エンドポイントをセットアップする必要がある場合、[リソースの保護 ](https://console.{DomainName}/docs/services/mobileaccess/protecting-resources.html)を参照してください。
1. ブラウザーで、新しく作成されたモバイル・バックエンドの保護エンドポイントへの要求の送信を試行します。次の URL を開きます。`{applicationRoute}/protected` (例: `http://my-mobile-backend.mybluemix.net/protected`)
<br/>MobileFirst Services Starter ボイラープレートを使用して作成されたモバイル・バックエンドの `/protected` エンドポイントは、{{site.data.keyword.amashort}} で保護されています。 `認証されていない`というメッセージがブラウザーに戻されます。このエンドポイントにアクセスできるのは、{{site.data.keyword.amashort}} Client SDK が装備されたモバイル・アプリケーションのみであるため、このメッセージが返されます。

1. iOS アプリケーションを使用して、同じエンドポイントへ要求を出します。

	```Swift
  let protectedResourceURL = "<Your protected resource URL>" // any protected resource
  let request = Request(url: protectedResourceURL , method: HttpMethod.GET)
  let callBack:BmsCompletionHandler = {(response: Response?, error: NSError?) in

  if error == nil {
     print ("response:\(response?.responseText), no error")
  } else {
     print ("error: \(error)")
  }
  }

  request.sendWithCompletionHandler(callBack)
 ```

1. アプリケーションを実行します。Facebook のログイン画面が表示されます。![image](images/ios-facebook-login.png)

   この画面は、現在 Facebook にログインしていない場合、若干異なって見える可能性があります。
1. **「OK」**をクリックして、{{site.data.keyword.amashort}} が Facebook のユーザー ID を認証目的に使用することを許可します。

1. 	要求が成功すると、以下の出力が Xcode コンソールに表示されます。```
 "onAuthenticationSuccess info = Optional({
     attributes =     {
     };
     deviceId = 218227041863639;
     displayName = "Don+Lon";
     isUserAuthenticated = 1;
     userId = 218227041863639;
 })
 response:Optional("Hello, this is a protected resouce of the mobile backend application!"), no error
 ```
  {: screen}

1. 次のコードを追加してログアウト機能を追加することもできます。

 ```
FacebookAuthenticationManager.sharedInstance.logout(callBack)
```

 ユーザーが Facebook にログインした後でこのコードを呼び出し、そのユーザーが再度ログインしようとする場合、{{site.data.keyword.amashort}} が認証を目的として Facebook を使用することについての許可を求めるプロンプトが出されます。

 ユーザーを切り替えるには、このコードを呼び出す必要があり、ユーザーはブラウザーで Facebook からログアウトしなければなりません。

 ログアウト機能へ `callBack` を渡すことは、オプションです。`nil` を渡すこともできます。
