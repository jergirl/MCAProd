---

copyright:
  years: 2016

---

#Enabling custom authentication for web applications
{: #custom-web}

*Last updated: 13 July 2016*
{: .last-updated}

Add custom authentication to your web app.

## Before you begin
{: #before-you-begin}

You must have a resource that is protected by an instance of the {{site.data.keyword.amashort}} service that is configured to use a custom identity provider.  For more information, see the following information:
 * [Getting started with {{site.data.keyword.amashort}}](https://console.{DomainName}/docs/services/mobileaccess/getting-started.html)
 * [Using a custom identity provider](https://console.{DomainName}/docs/services/mobileaccess/custom-auth.html)
 * [Creating a custom identity provider](https://console.{DomainName}/docs/services/mobileaccess/custom-auth-identity-provider.html)
 * [Configuring {{site.data.keyword.amashort}} for custom authentication](https://console.{DomainName}/docs/services/mobileaccess/custom-auth-config-mca.html)


##Configuring a custom identity provider 

When creating a custom identity provider you must implement a `/handleChallengeAnswer` endpoint. This endpoint must have the following structure:  

`/apps/:tenantID/<your-realm-name>/handleChallengeAnswer`

`tenantID` is a url parameter and `<YourRealmName>` is any realm name you choose. 

A call to this endpoint must contain two body parameters: `username` and `password`. After validating the user, this endpoint must return a JSON object of the following structure: 
```json
{ 

            status: "success", 
            userIdentity: { 
                userName: <user name>, 
                displayName: <display name> 
     attributes: <additional attributes json> 
            } 
        } 

 ```

**Note:** The attributes field is optional. 

##Configuring {{site.data.keyword.amashort}} for custom authentication 

After you have your custom identity provider configured, you can enable custom authentication in the {{site.data.keyword.amashort}}  dashboard. 

1. Open the {{site.data.keyword.Bluemix_notm}} dashboard. 
2. Click the relevant {{site.data.keyword.amashort}} application tile. The app dashboard loads. 
3. Click the **Configure** button on the Custom tile. 
4. In the **Realm Name** text box, enter the realm name configured in your custom identity provider handler endpoint. 
5. Enter the custom identity provider url. 
6. Enter the Web application redirect URI to be used by {{site.data.keyword.amashort}} dashboard after successful authentication. 
7. Save. 


##Implementing the {{site.data.keyword.amashort}} authorization flow using a custom identity provider 

The `VCAP_SERVICES` environment variable is created automatically for each {{site.data.keyword.amashort}} service instance and contains properties necessary for the authorization process. It consists of a JSON object and can be viewed by clicking  **Enviroment Variables**  in the left-side navigator of your application.

To request user authorization, redirect the browser to the authorization server endpoint. In order to do so: 

1. Retrieve the authorization endpoint (`authorizationEndpoint`) and clientId (`clientId`) from the service credentials stored in `VCAP_SERVICES` environment variable. 

  **Note:** In case you’ve added the Mobile Client Access service to your application before web support was added you might not have token endpoint in service credentials. Use below urls depending on your {{site.data.keyword.Bluemix_notm}}  region instead: 
 
  US South: 
  ```
  https://mobileclientaccess.ng.bluemix.net/oauth/v2/authorization 
  ```
  London: 
  ```
  https://mobileclientaccess.eu-gb.bluemix.net/oauth/v2/authorization 
  ```
  Sydney: 
  ```
  https://mobileclientaccess.au-syd.bluemix.net/oauth/v2/authorization 
  ```
2. Build the authorization server URI supplying response_type ("code"), `client_id`, and `redirect_uri` as query parameters.  
1. Redirect from your web app to the generated URI. 

The following example retrieves the parameters from the `VCAP_SERVICES` variable, builds the URL, and sends the redirect request.

 ```Java
var cfEnv = require("cfenv"); 
app.get("/protected", checkAuthentication, function(req, res, next){ 
  res.send("Hello from protected endpoint"); 
  }
); 


function checkAuthentication(req, res, next){ 
  // Check if user is authenticated 
  if (req.session.userIdentity){ 
    next() 
  } else { 
    // If not - redirect to authorization server 
    var mcaCredentials = cfEnv.getAppEnv().services.AdvancedMobileAccess[0].credentials; 
    var authorizationEndpoint = mcaCredentials.authorizationEndpoint; 
    var clientId = mcaCredentials.clientId; 
    var redirectUri = "http://some-server/oauth/callback"; // Your web application redirect uri 
    var redirectUrl = authorizationEndpoint + "?response_type=code";
    redirectUrl += "&client_id=" + clientId; 
    redirectUrl += "&redirect_uri=" + redirectUri; 
    res.redirect(redirectUrl); 
  } 

} 

 ```
 
Note that the `redirect_uri` parameter represents your web application redirect URI and must be equal to the one defined in the{{site.data.keyword.amashort}} dashboard.  

After redirecting to the authorization end-point the user will get a login form. After user’s credentials are authenticated with the custom identity provider, the {{site.data.keyword.amashort}} service will call your web application redirect URI supplying the grant code as a query parameter.  

After redirecting, the user gets a login form. After the user’s credentials are authenticated by the custom identity provider, the {{site.data.keyword.amashort}} service will calls the web application redirect URI, supplying the grant code as a query parameter. 



The next step is to obtain the access token and identity token using the previously received grant code. In order to do so: 

1. Retrieve `authorizationEndpoint`, `clientId`, and `secret` from service credentials stored in `VCAP_SERVICES` environment variable. 

   **Note:** In case you’ve added the Mobile Client Access service to your application before web support was added you might not have token endpoint in service credentials. In this case use below urls depending on your Bluemix region instead: 

 US South: 
 ```
     https://mobileclientaccess.ng.bluemix.net/oauth/v2/token   
 ```
 London: 
 ```
     https://mobileclientaccess.eu-gb.bluemix.net/oauth/v2/token
 ``` 
 Sydney: 
 ``` 
     https://mobileclientaccess.au-syd.bluemix.net/oauth/v2/token 
 ```
1. Send a post request to the token server URI with `grant_type`, `client_id`, `redirect_uri`, and `code` as form parameters and `clientId` and `secret` as Basic HTTP authentication credentials.


The following example, the following code retrieves the necessary values, and sends them with a post request.


 ```Java
var cfEnv = require("cfenv");
var base64url = require("base64url ");
app.get("/oauth/callback", function(req, res, next){ 
    var mcaCredentials = cfEnv.getAppEnv().services.AdvancedMobileAccess[0].credentials; 
    var tokenEndpoint = mcaCredentials.tokenEndpoint; 

    var formData = { 
      grant_type: "authorization_code", 
      client_id: mcaCredentials.clientId, 
      redirect_uri: "http://some-server/oauth/callback",   // Your web application redirect uri 
      code: req.query.code 
    } 

  request.post({ 
    url: tokenEndpoint, 
    formData: formData 
    }, function (err, response, body){ 
      var parsedBody = JSON.parse(body); 

      req.session.accessToken = parsedBody.access_token; 
      req.session.idToken = parsedBody.id_token; 
      var idTokenComponents = parsedBody.id_token.split("."); // [header, payload, signature] 
      var decodedIdentity= base64url(idTokenComponents[1]);
      req.session.userIdentity = JSON.parse(decodedIdentity)["imf.user"]; 
      res.redirect("/"); 
    }
    ).auth(mcaCredentials.clientId, mcaCredentials.secret); 
  }
); 

 ```
Note that the `redirect_uri` parameter must match the `redirect_uri` used in authorization request previously. The code parameter value should be the grant code received in the response at the end of authorization request. The grant code is valid for 10 minutes only, you will need to to obtain a new code.

The response body will contain `access_token` and `id_token`  in JWT format (https://jwt.io/).

Once you have received access, and identity the tokens, you can flag web session as authenticated and optionally persist these tokens

##Using obtained access and identity token 

The identity token contains information about user identity. In case of a custom authentication, the token will contain all the information returned by the custom identity provider upon authentication. Under the `imf.user` field, the field `displayName` will contain the `displayName` returned by the custom identity provider, and the field `id` will contain the `userName`.  All other values returned by the custom identity provider are returned within the field `attributes` under `imf.user`.  

The access token allows communication with resources protected by Mobile Client Access authorization filters (see [Protecting resources](protecting-resources.html)). In order to make requests to protected resources add an Authorization header to requests with the following structure: 

`Authorization=Bearer <accessToken> <idToken>` 


**Note:** The identity token is optional. In the case where you do not supply the identity token, the protected resource can be accessed, but will not receive any information about the authorized user. 



