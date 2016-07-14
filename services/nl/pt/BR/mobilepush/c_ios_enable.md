---

copyright:
 years: 2015, 2016

---

# Ativando aplicativos iOS para receber notificações push
{: #enable-push-ios-notifications}

Ative aplicativos iOS para receber notificações push e
enviar notificações push para seus dispositivos.


##Instalando o CocoaPods
{: #enable-push-ios-notifications-install}

Para um projeto Xcode existente, é possível configurar o SDK do cliente Bluemix Mobile Services usando a ferramenta de gerenciamento de dependência CocoaPods. Uma alternativa é instalar o SDK manualmente.

**Nota**: para visualizar o arquivo leia-me de Push do Swift, acesse https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-push/tree/master



1. Instale o CocoaPods usando o comando a seguir em seu terminal Mac.
```
$ sudo gem install cocoapods
```
2. Insira o comando a seguir no terminal para inicializar o CocoaPods. Ao emitir esse comando, certifique-se de executá-lo no diretório em que está o projeto Xcode. O comando `pod init` cria um título de arquivo.  
```
$ pod init
```
3. No Podfile gerado, inclua as dependências necessárias de SDK. Copie o Podfile a seguir.

   Objective-C

    ```
    source 'https://github.com/CocoaPods/Specs.git'
	Copy the following list as is and remove the dependencies you do not need
	pod 'IMFCore'
	pod 'IMFPush'
	```

   Swift

	```
	source 'https://github.com/CocoaPods/Specs.git'
	// Copy the following list as is and remove the dependencies you do not need.
	use_frameworks!

	target 'MyApp' do
	    platform :ios, '8.0'
	    pod 'BMSCore'
	    pod 'BMSPush'
      pod 'BMSAnalyticsAPI'
	end
	```
3. No Terminal, acesse a pasta do projeto e instale as dependências com o comando a seguir:
```
$ pod update
```
Esse comando instala suas dependências e cria uma nova área de trabalho Xcode.  **Nota**: assegure-se de sempre abrir a nova área de trabalho do Xcode, em vez do arquivo de projeto do Xcode original:

	```
	$ open App.xcworkspace
	```
A área de trabalho contém o projeto original e o projeto Pods que contém suas dependências. Se você desejar modificar uma pasta de origem do Bluemix Mobile Services, será possível localizá-la no projeto Pods, em `Pods/yourImportedSourceFolder`, por exemplo: `Pods/BMSPush`.
##Carthage
{: #carthage}

Inclua estruturas em seu projeto usando [Carthage](https://github.com/Carthage/Carthage#if-youre-building-for-ios-tvos-or-watchos). (https://github.com/Carthage/Carthage#if-youre-building-for-ios-tvos-or-watchos%29.)

1. Inclua as estruturas `BMSPush` em seu Cartfile:
```
github "github "ibm-bluemix-mobile-services/bms-clientsdk-swift-push" ~> 1.0"
```
2. Execute o comando `carthage update`. Quando a construção for concluída, arraste `BMSPush.framework`, `BMSCore.framework` e `BMSAnalyticsAPI.framework` até seu projeto Xcode.
3. Siga as instruções no site [Carthage](https://github.com/Carthage/Carthage#if-youre-building-for-ios-tvos-or-watchos) para concluir a integração.

##Usando estruturas importadas e pastas de origem

Referencie o SDK no código.


### Objective-C

Escreva diretivas #import para os cabeçalhos relevantes, por exemplo:

```
//Objective-C
#import <IMFCore/IMFCore.h>
#import <IMFPush/IMFPush.h>
```

**Nota**: a atualização de seu projeto Pods usando os comandos CocoaPods `pod install` ou `pod update` poderá substituir as pastas de origem do Bluemix Mobile Services. Para reter as versões customizadas dos arquivos originais, assegure-se de que sejam submetidas a backup antes de emitir um destes comandos.

###Swift

**Pré-requisitos**

- iOS 8.0 ou superior
- Xcode 7


Escreva diretivas #import para os cabeçalhos relevantes, por exemplo:

```
//swift
import BMSCore
import BMSPush
```
**Atenção**: para visualizar o arquivo leia-me de Swift Push, acesse [Leia-me](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-push/tree/master)
##Configurações de Compilação

Acesse **Xcode > Configurações de criação > Opções de criação e configure Ativar Bitcode** como **Não**.

**Atenção**: desde o iOS 9, mudanças no recurso App Transport Security (ATS) podem afetar a maneira de manipular o processo de autenticação. As postagens do blog a seguir descrevem mais informações sobre as mudanças:[ATS e Bitcode no iOS 9](https://developer.ibm.com/mobilefirstplatform/2015/09/09/ats-and-bitcode-in-ios9/) e [Conecte seu app iOS 9 ao Bluemix hoje](https://developer.ibm.com/bluemix/2015/09/16/connect-your-ios-9-app-to-bluemix/)




## Inicializando apps Push SDK para iOS
{: #enable-push-ios-notifications-initialize}

Um local comum para colocar o código de inicialização é no aplicativo delegado do aplicativo iOS. Clique no link **Opções móveis** no Bluemix
Application Dashboard para obter a rota e o GUID do aplicativo.

###Inicializando o SDK principal

####Objective-C

```
// Initialize the SDK for Object-C with IBM Bluemix GUID and route
IMFClient *imfClient = [IMFClient sharedInstance];
[imfClient initializeWithBackendRoute:"add_your_applicationRoute_here" backendGUID:"add_your_appId_here"];
```

####Swift

```
// Initialize the Core SDK for Swift with IBM Bluemix GUID, route, and region
let myBMSClient = BMSClient.sharedInstance

myBMSClient.initializeWithBluemixAppRoute("BluemixAppRoute", bluemixAppGUID: "APPGUID", bluemixRegion:"Location where your app Hosted")
myBMSClient.defaultRequestTimeout = 10.0 // Timput in seconds
```


###Inicializando o SDK de Push do cliente

####Objective-C

```
//Initialize client Push SDK for Objective-C
IMFPushClient _pushService = [IMFPushClient sharedInstance];
```

####Swift

```
//Initialize client Push SDK for Swift
let push = BMSPushClient.sharedInstance
```

### Rota, GUID e região do Bluemix

**appRoute**

Especifica a rota que é designada ao aplicativo do servidor que você criou no Bluemix.

**GUID**

Especifica a chave exclusiva que é designada ao aplicativo que você criou no Bluemix. Esse valor faz distinção entre maiúsculas e minúsculas.

**bluemixRegionSuffix**

Especifica o local em que o app está hospedado. O parâmetro `bluemixRegion` especifica qual implementação do Bluemix você está usando. É possível configurar esse valor com uma propriedade estática `BMSClient.REGION` e use um dos três valores:

- BMSClient.REGION_US_SOUTH
- BMSClient.REGION_UK
- BMSClient.REGION_SYDNEY




## Registrando aplicativos e dispositivos iOS
{: #enable-push-ios-notifications-register}


Um aplicativo (app) deve se registrar com APNS para receber notificações remotas, o que geralmente ocorre após o aplicativo ser instalado em um dispositivo. Após o
token de dispositivo gerado pelo APNS ser recebido pelo aplicativo, ele deverá ser transmitido novamente para o Serviço de Notificações Push.

Para registrar aplicativos e dispositivos iOS:

1. Crie um aplicativo backend
2. Passe o token para as Notificações push


###Crie um aplicativo backend

Crie um aplicativo backend no catálogo do Bluemix® da seção Modelos que ligará automaticamente o serviço de Push a esse aplicativo. Se também já tiver criado um app backend, certifique-se de ligar o app ao Push Notification Service.

####Objective-C

```
	//For Objective-C
	- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
	if ([[[UIDevice currentDevice] systemVersion] floatValue] >= 8.0){
	    [[UIApplication sharedApplication] registerUserNotificationSettings:[UIUserNotificationSettings settingsForTypes:(UIUserNotificationTypeSound | UIUserNotificationTypeAlert | UIUserNotificationTypeBadge) categories:categories]];
	    [[UIApplication sharedApplication] registerForRemoteNotifications];
	    }
	    else{
	    [[UIApplication sharedApplication] registerForRemoteNotificationTypes:
	    (UIUserNotificationTypeBadge | UIUserNotificationTypeSound | UIUserNotificationTypeAlert)];
	    }
	    return YES;
	}
```

####Swift

```
	//For Swift
	func application(application: UIApplication, didFinishLaunchingWithOptions launchOptions: [NSObject: AnyObject]?) -> Bool {
		let notificationTypes: UIUserNotificationType = UIUserNotificationType.Badge | UIUserNotificationType.Alert | UIUserNotificationType.Sound
		let notificationSettings: UIUserNotificationSettings = UIUserNotificationSettings(forTypes: notificationTypes, categories: categories)
		application.registerUserNotificationSettings(notificationSettings)
		application.registerForRemoteNotifications()
	}
```

###Passe o token para as Notificações push

Após o token ser recebido do APNS, transmita o token para Notificações push como parte do método `registerDevice:withDeviceToken`.

####Objective-C

```
//For Objective-C
-( void) application:( UIApplication *)application didRegisterForRemoteNotificationsWithDeviceToken:( NSData *)deviceToken{

   IMFClient *client = [IMFClient sharedInstance];

 [client initializeWithBackendRoute:@"your-backend-route-here" backendGUID:@"Your-backend-GUID-here"];


 // get Push instance
IMFPushClient* push = [IMFPushClient sharedInstance];
[push registerDeviceToken:deviceToken completionHandler:^(IMFResponse *response,  NSError *error) {
   if (error){
     [ self  updateMessage:error .description];
  }  else {
    [ self updateMessage:response .responseJson .description];
}
}];
```

####Swift

Após o token ser recebido do APNS, transmita o token para Notificações push como parte do método `didRegisterForRemoteNotificationsWithDeviceToken`.

```
func application (application: UIApplication, didRegisterForRemoteNotificationsWithDeviceToken deviceToken: NSData){
   let push =  BMSPushClient.sharedInstance
   push.registerDeviceToken(deviceToken) { (response, statusCode, error) -> Void in
        if error.isEmpty {
            print( "Response during device registration : \(response)")
            print( "status code during device registration : \(statusCode)")
        }
        else{
            print( "Error during device registration \(error) ")
            print( "Error during device registration \n  - status code: \(statusCode) \n Error :\(error) \n")
        }
    }

}
```



## Recebendo notificações push em dispositivos iOS
{: #enable-push-ios-notifications-receiving}

Receba notificações push em dispositivos iOS

###Objective-C
Para receber notificações push em dispositivos iOS, inclua o método Objective-C a seguir na delegação de seu aplicativo.

```
// For Objective-C
-(void)application:(UIApplication *)application didReceiveRemoteNotification:(NSDictionary *)userInfo {
//O dicionário userInfo conterá dados enviados do servidor.
}
```

###Swift
Para receber notificações push em dispositivos iOS, inclua o método Swift a seguir na delegação de seu aplicativo.

```
 // For Swift
func application(application: UIApplication, didReceiveRemoteNotification userInfo: [NSObject : AnyObject], fetchCompletionHandler completionHandler: (UIBackgroundFetchResult) -> Void) {
       //UserInfo dictionary will contain data sent from the
server
   }

```



## Enviando notificações push básicas
{: #send}

Depois de desenvolver seus aplicativos, é possível enviar notificações push básicas (sem usar tags, badges, cargas úteis adicionais ou arquivos de som).


Envie notificações push básicas.

1. Em **Escolher o público**, selecione um dos seguintes públicos: **Todos os dispositivos** ou por plataforma: **Apenas dispositivos iOS** ou **Apenas
dispositivos Android**. 

	**Nota**: ao selecionar a opção **Todos os dispositivos**, todos os dispositivos inscritos para notificações push recebem sua notificação.

	![Tela de notificações](images/tag_notification.jpg)

2. Em **Criar sua notificação**, insira sua mensagem e clique em **Enviar**.
3. Verifique se seus dispositivos receberam sua notificação.

	A captura de tela a seguir mostra uma caixa de alerta que manipula uma notificação push no primeiro plano e no segundo plano em um dispositivo iOS.

	![Notificação push de primeiro plano no Android](images/Android_Screenshot.jpg)

	![Notificação push de primeiro plano no iOS](images/iOS_Screenshot.jpg)




## Etapas Seguintes
{: #next_steps_tags}

Depois de configurar com êxito notificações básicas, é possível configurar notificações baseadas em tag e opções avançadas.

Inclua esses recursos do Serviço de notificações push em seu app.
Para usar notificações baseadas em tag, consulte [Notificações baseadas em tag](c_tag_basednotifications.html).
Para usar opções de notificações avançadas, consulte [Notificações push avançadas](t_advance_notifications.html).
