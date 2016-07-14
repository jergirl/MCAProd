---

copyright:
  years: 2015, 2016

---
{:screen:  .screen}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}

# Ativando a autenticação do Facebook para apps iOS (Objective-C SDK)
{: #facebook-auth-ios}


*Última atualização: 15 de junho de 2016*
{: .last-updated}


Para usar o Facebook como provedor de identidade em seus aplicativos iOS, inclua e configure a Plataforma iOS para seu aplicativo Facebook.
{:shortdesc}

**Nota:** embora o Objective-C SDK permaneça totalmente suportado e ainda seja considerado o SDK primário para o {{site.data.keyword.Bluemix}} Mobile Services, há planos para descontinuá-lo posteriormente este ano em favor do novo Swift SDK (consulte [Configurando o iOS Swift SDK](facebook-auth-ios-swift-sdk.html)).

## Antes de Começar
{: #facebook-auth-ios-before}
Você deve ter:
* Um projeto do iOS configurado para trabalhar com CocoaPods. Para obter mais informações, consulte **Instalar o CocoaPods** em [Configurando o iOS SDK](https://console.{DomainName}/docs/services/mobileaccess/getting-started-ios.html).
   **Nota:** não é necessário instalar o {{site.data.keyword.amashort}} client SDK principal antes de continuar.
* Uma instância de um aplicativo {{site.data.keyword.Bluemix_notm}} que seja protegida pelo serviço {{site.data.keyword.amashort}}. Para obter mais informações sobre como criar um backend do {{site.data.keyword.Bluemix_notm}}, consulte [Introdução](index.html).
* Um ID de aplicativo do Facebook. Para obter mais informações, consulte [Obtendo um ID do aplicativo Facebook do Portal do Desenvolvedor do Facebook](https://console.{DomainName}/docs/services/mobileaccess/facebook-auth-overview.html#facebook-appID).

## Configurando seu aplicativo Facebook para a plataforma iOS
{: #facebook-auth-ios-config}


1. Em seu aplicativo Facebook no Portal do Desenvolvedor do Facebook, clique em **Configurações > Incluir plataforma > iOS**.

1. Especifique o *bundleId* de seu aplicativo iOS. Para localizar o *bundleId* de seu aplicativo iOS, procure o **Identificador de pacote configurável** no arquivo `info.plist` ou na guia **Geral** do projeto do Xcode.
**Dica**: considere a ativação do sufixo de esquema URL ou a Conexão única se estiver planejamento usar esses recursos.

1. Clique em **Salvar Configurações**.

## Configurando o {{site.data.keyword.amashort}} para autenticação do Facebook
{: #facebook-auth-ios-configmca}

Depois de configurado o ID do aplicativo Facebook e seu aplicativo Facebook para atender clientes iOS, é possível ativar a autenticação do Facebook no {{site.data.keyword.amashort}}.

1. Abra seu app no painel do {{site.data.keyword.Bluemix}}.

1. Clique em **Opções móveis** e anote a
**Rota** (`applicationRoute`) e o **GUID do
app** (`applicationGUID`). Eles serão necessários ao inicializar o SDK.

1. Clique no ladrilho {{site.data.keyword.amashort}}. O painel do {{site.data.keyword.amashort}} é carregado.

1. Clique no ladrilho **Facebook**.

1. Especifique o ID do aplicativo Facebook e clique em **Salvar**.

## Configurando o {{site.data.keyword.amashort}} client SDK para iOS
{: #facebook-auth-ios-sdk}

### Instalando o CocoaPods
{: #facebook-auth-cocoapods}

O {{site.data.keyword.amashort}} client SDK é distribuído com o CocoaPods, um gerenciador de dependência para projetos iOS. O CocoaPods faz o download automático de artefatos de repositórios e os disponibiliza para o aplicativo iOS.

1. Abra o Terminal e execute o comando `pod --version`. Se você já tiver o CocoaPods instalado, o número da versão será exibido. É possível pular para a próxima seção deste tutorial.

1. Instale o CocoaPods executando `sudo gem install cocoapods`. Consulte o [website do CocoaPods](https://cocoapods.org/) se precisar de orientação adicional.

### Instalando o {{site.data.keyword.amashort}} client SDK com o CocoaPods
{: #facebook-auth-install-cocoapods}

1. Em seu projeto do iOS, edite o `Podfile` e a linha a seguir:

	```
	pod 'IMFFacebookAuthentication'
	```

1. Salve o `Podfile` e execute o comando `pod install` a partir da linha de comandos. O CocoaPods instala as dependências. O progresso e quais componentes foram incluídos são exibidos.
 **Importante**: deve-se abrir agora o projeto usando o arquivo
`xcworkspace` que é gerado pelo CocoaPods. Normalmente, o nome é `{your-project-name}.xcworkspace`.  

1. Execute `open {your-project-name}.xcworkspace` a partir da linha de comandos para abrir sua área de trabalho do projeto do iOS.

### Configurando seu projeto do iOS para autenticação do Facebook
{: #facebook-auth-ios-configproject}

1. Localize o arquivo `info.plist`, normalmente localizado na pasta `Arquivos de apoio` em seu projeto do Xcode.

1. Configure a integração do Facebook incluindo as propriedades a seguir em seu arquivo `info.plist`:

	![image](images/ios-facebook-infoplist-settings.png)

	Atualize o esquema URL e as propriedades FacebookappID com seu ID do aplicativo Facebook

Também é possível atualizar o arquivo `info.plist` clicando com o botão direito no arquivo, selecionando **Abrir como > Código-fonte** e incluindo o XML a seguir:

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
	<string>MyApp</string>
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
Atualize o esquema URL e as propriedades FacebookappID com seu ID do aplicativo Facebook.

 **Importante**: assegure-se de não substituir quaisquer propriedades existentes no arquivo `info.plist`. Se você tiver propriedades de sobreposição, deverá mesclá-las manualmente. Para obter mais informações, consulte [Configurar o projeto do Xcode](https://developers.facebook.com/docs/ios/getting-started/) e [Preparando seus apps para iOS9](https://developers.facebook.com/docs/ios/ios9).

## Inicializando o {{site.data.keyword.amashort}} client SDK
{: #facebook-auth-ios-initalize}

Inicialize o client SDK passando a rota do app (`applicationRoute`) e o GUID do app (`applicationGUID`).

Um local comum, mas não obrigatório, para colocar o código de inicialização é no método `application:didFinishLaunchingWithOptions` de delegado do seu aplicativo.

1. Abra a página principal do painel do {{site.data.keyword.Bluemix_notm}} e clique em seu app. Clique em **Opções móveis** e anote a
**Rota** (`applicationRoute`) e o **GUID do
app** (`applicationGUID`).

1. Importe a estrutura necessária na classe em que deseja usar o {{site.data.keyword.amashort}} client SDK incluindo os cabeçalhos a seguir:

	**Objective-C**

	```Objective-C
	#import <IMFCore/IMFCore.h>
	#import <IMFFacebookAuthentication/IMFFacebookAuthenticationHandler.h>
	#import <FacebookSDK/FacebookSDK.h>
```

	**Swift**

	O {{site.data.keyword.amashort}} client SDK é implementado usando Objective-C; portanto, pode ser necessário incluir um cabeçalho ponte em seu projeto swift.

	1. Clique com o botão direito no projeto em Xcode e selecione **Novo arquivo...**
	* Na categoria **Origem iOS**, selecione `Arquivo de cabeçalho`
	* Atribua um nome a ele `BridgingHeader.h`
	* Inclua importações ao seu cabeçalho de ponte:

	```Objective-C
	#import <IMFCore/IMFCore.h>
	#import <IMFFacebookAuthentication/IMFFacebookAuthenticationHandler.h>
	#import <FacebookSDK/FacebookSDK.h>
```
	* Clique em seu projeto em Xcode e selecione a guia **Configurações de compilação**.
 * Procure **Cabeçalho de ponte do Objective-C**.
	* Configure o valor para o local de seu arquivo `BridgingHeader.h`, por exemplo: `$(SRCROOT)/MyApp/BridgingHeader.h`.
	* Certifique-se de que seu cabeçalho de ponte esteja sendo selecionado pelo Xcode, compilando o seu projeto. Nenhuma mensagem de falha deve ser vista.

3. Inicialize o client SDK. Substitua *applicationRoute* e
*applicationGUID* pelos valores de **Rota** e
**GUID do app** que você obteve das **Opções móveis**
no painel {{site.data.keyword.Bluemix_notm}}.

	**Objective-C**

	```Objective-C
	[[IMFClient sharedInstance]
			initializeWithBackendRoute:@"applicationRoute"
			backendGUID:@"applicationGUID"];
	```

	**Swift**

	```Swift
	IMFClient.sharedInstance().initializeWithBackendRoute("applicationRoute",
	 							backendGUID: "applicationGUID")
	```

1. Notifique o Facebook SDK sobre a ativação do app e registre o Manipulador de autenticação do Facebook incluindo o código a seguir no método `application:didFinishLaunchingWithOptions` no delegado de seu app. Inclua esse código imediatamente após a inicialização da instância IMFClient.

	**Objective-C**

	```Objective-C
		[FBAppEvents activateApp];
		[[IMFFacebookAuthenticationHandler sharedInstance] registerWithDefaultDelegate];
```

	**Swift**

	```Swift
		FBAppEvents.activateApp()
		IMFFacebookAuthenticationHandler.sharedInstance().registerWithDefaultDelegate()
```

1. Inclua o código a seguir no delegado de seu app.

	**Objective-C**

	```Objective-C
	- (BOOL)application:(UIApplication *)application openURL:(NSURL *)url
			sourceApplication:(NSString *)sourceApplication annotation:(id)annotation {

		return [FBAppCall handleOpenURL:url sourceApplication:sourceApplication];

	}
```

	**Swift**

	```Swift
	func application(application: UIApplication, openURL url: NSURL,
					sourceApplication: String?, annotation: AnyObject) -> Bool {

		return FBAppCall.handleOpenURL(url, sourceApplication: sourceApplication)

	}
```

## Testando a autenticação
{: #facebook-auth-ios-testing}
Após a inicialização do client SDK e o registro do Gerenciador de autenticação do Facebook, será possível começar a fazer solicitações para seu backend móvel.

### Antes de iniciar
{: #facebook-auth-ios-testing-before}
Deve-se usar o modelo do {{site.data.keyword.mobilefirstbp}} e já ter um recurso protegido por {{site.data.keyword.amashort}} no terminal `/protected`. Se for necessário configurar um terminal `/protected`, consulte [Protegendo recursos](https://console.{DomainName}/docs/services/mobileaccess/protecting-resources.html).

1. Tente enviar uma solicitação para o terminal protegido de seu backend móvel recém-criado em seu navegador. Abra a URL a seguir: `{applicationRoute}/protected`.
Por exemplo: `http://my-mobile-backend.mybluemix.net/protected`
<br/>O terminal `/protected` de um backend móvel que foi criado com o modelo MobileFirst Services Starter está protegido com o {{site.data.keyword.amashort}}. Uma mensagem `Unauthorized` é retornada no navegador. Essa mensagem é retornada porque esse terminal só pode ser acessado por aplicativos móveis instrumentados com o {{site.data.keyword.amashort}} client SDK.

1. Use seu aplicativo iOS para fazer uma solicitação para o mesmo terminal.

	**Objective-C**

	```Objective-C
	NSString *requestPath = [NSString stringWithFormat:@"%@/protected",
								[[IMFClient sharedInstance] backendRoute]];

	IMFResourceRequest *request =  [IMFResourceRequest requestWithPath:requestPath
																method:@"GET"];

	[request sendWithCompletionHandler:^(IMFResponse *response, NSError *error) {
		if (error){
			NSLog(@"Error :: %@", [error description]);
		} else {
			NSLog(@"Response :: %@", [response responseText]);
			NSLog(@"%@", [[IMFAuthorizationManager sharedInstance] userIdentity]);
		}
	}];
	```

	**Swift**

	```Swift
	let requestPath = IMFClient.sharedInstance().backendRoute + "/protected"

	let request = IMFResourceRequest(path: requestPath, method: "GET");
	request.sendWithCompletionHandler { (response, error) -> Void in
		if (nil != error){
			NSLog("Error :: %@", error.description)
		} else {
			NSLog("Response :: %@", response.responseText)
			NSLog("%@", IMFAuthorizationManager.sharedInstance().userIdentity)
		}
	};
 ```

1. Execute seu aplicativo. Uma tela de login do Facebook é exibida.

	![image](images/ios-facebook-login.png)

	Essa tela poderá parecer um pouco diferente se o app Facebook não estiver instalado em seu dispositivo, ou se você não estiver atualmente conectado ao Facebook.

1. Clique em **OK** para autorizar o {{site.data.keyword.amashort}} a usar a identidade do usuário do Facebook para propósitos de autenticação.

1.	Quando sua solicitação for bem-sucedida, a saída a seguir será exibida no console do Xcode:
	![image](images/ios-facebook-login-success.png)

	Também é possível incluir a funcionalidade de logout incluindo o código a seguir:

	**Objective-C**

	```Objective-C
	[[IMFFacebookAuthenticationHandler sharedInstance] logout : callBack]
	```

	**Swift**

	```Swift
	IMFFacebookAuthenticationHandler.sharedInstance().logout(callBack)
	```

	Se você chamar esse código depois que um usuário estiver conectado ao Facebook e ele tentar efetuar login novamente, ele será solicitado a autorizar o {{site.data.keyword.amashort}} a usar o Facebook para propósitos de autenticação.

	Para alternar usuários, deve-se chamar esse código e o usuário deve efetuar logout do Facebook em seu navegador.

  Passar `callBack` para a função de logout é opcional. Também é possível passar `nil`.
