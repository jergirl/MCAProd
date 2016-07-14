---

copyright:
  years: 2015, 2016
  
---
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Setting up the Android SDK
{: #getting-started-android}

*Last updated: 04 July 2016*
{: .last-updated}

Instrument your Android application with the {{site.data.keyword.amashort}} client SDK, initialize the SDK, and make requests to protected and unprotected resources.
{:shortdesc}

## Before you begin
{: #before-you-begin}
You must have:
* An instance of a  {{site.data.keyword.Bluemix_notm}} application that is protected by {{site.data.keyword.amashort}} service. For more information about how to create a {{site.data.keyword.Bluemix_notm}} back-end application, see [Getting started](index.html).
* An Android Studio project, set up to work with Gradle. For more information about how to set up your Android development environment, see [Google Developer Tools](http://developer.android.com/sdk/index.html).


## Installing the {{site.data.keyword.amashort}} client SDK
{: #install-mca-sdk}

The {{site.data.keyword.amashort}} client SDK is distributed with Gradle, a dependency manager for Android projects. Gradle automatically downloads artifacts from repositories, and makes them available to your Android application.

1. Create an Android Studio project or open an existing project.

1. Open the `build.gradle` file for your application (**not** the project `build.gradle` file).



1. Find the **dependencies** section of the `build.gradle` file.  Add a compile dependency for the {{site.data.keyword.amashort}} client SDK:

	```Gradle
	dependencies {
		compile group: 'com.ibm.mobilefirstplatform.clientsdk.android',    
        name:'core',
        version: '1.+',
        ext: 'aar',
        transitive: true
    	// other dependencies  
}
```

1. Synchronize your project with Gradle. Click **Tools &gt; Android &gt; Sync Project with Gradle Files**.

1. Open the `AndroidManifest.xml` file for your Android project. Add internet access permission under the `<manifest>` element:

	```XML
	<uses-permission android:name="android.permission.INTERNET" />
```

## Initializing the {{site.data.keyword.amashort}} client SDK
{: #initalize-mca-sdk}

Initialize the SDK by passing the `context`, `applicationGUID`, `applicationRoute`, and `BMSClient.REGION_UK` parameters to the `initialize` method.


1. From the main page of the {{site.data.keyword.Bluemix_notm}} dashboard, click your app. Click **Mobile Options**. You need the **Application route** and **Application GUID** values to initialize the SDK.

2. Initialize the {{site.data.keyword.amashort}} client SDK in your Android application.  A common, though not mandatory, place to put the initialization code is in the `onCreate` method of the main activity in your Android application.
<br/>Replace the *applicationRoute* and *applicationGUID* with the values from **Mobile Options** in the {{site.data.keyword.Bluemix_notm}} dashboard.

	```Java
	BMSClient.getInstance().initialize(getApplicationContext(),
					"applicationRoute",
					"applicationGUID",
					BMSClient.REGION_UK);
```
Replace the `BMSClient.REGION_UK` with the appropriate region.

## Making a request to your mobile back-end application
{: #request}

After the {{site.data.keyword.amashort}} client SDK is initialized, you can start making requests to your mobile back-end application.

1. Try to send a request to a protected endpoint of your new mobile back-end application. In your browser, open the following URL: `{applicationRoute}/protected`. For example: `http://my-mobile-backend.mybluemix.net/protected`
<br/>The `/protected` endpoint of a mobile back-end application that was created with MobileFirst Services Starter boilerplate is protected with {{site.data.keyword.amashort}}. An `Unauthorized` message is returned in your browser, because this endpoint can only be accessed by mobile applications that are instrumented with the {{site.data.keyword.amashort}} client SDK.

1. Use your Android application to make a request to the same endpoint. Add the following code after you initialize `BMSClient`:

	```Java
	Request request = new Request("/protected", Request.GET);
	request.send(this, new ResponseListener() {
		@Override
		public void onSuccess (Response response) {
			Log.d("Myapp", "onSuccess :: " + response.getResponseText());
		}
		@Override
		public void onFailure (Response response, Throwable t, JSONObject extendedInfo) {
			if (null != t) {
				Log.d("Myapp", "onFailure :: " + t.getMessage());
			} else if (null != extendedInfo) {
				Log.d("Myapp", "onFailure :: " + extendedInfo.toString());
			} else {
				Log.d("Myapp", "onFailure :: " + response.getResponseText());
			}
		}
	});
	```

1. When your request succeeds, you will see the following output in the LogCat utility:

	![image](images/getting-started-android-success.png)

## Next steps
{: #next-steps}

When you connected to the protected endpoint, no credentials were required. To require your users to log in to your application, you must configure Facebook, Google, or custom authentication.
* [Facebook](facebook-auth-android.html)
* [Google](google-auth-android.html)
* [Custom](custom-auth-android.html)
