---

copyright:
  years: 2015, 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Extending device management
{: #custom_actions}
*Last updated: 6 July 2016*
{: .last-updated}

You can extend the device management capabilities in your {{site.data.keyword.iot_full}} to suit your requirements by adding device management extensions through either the REST API or the dashboard that is provided in {{site.data.keyword.Bluemix_notm}}.

By default, the following device management actions are provided and supported by the {{site.data.keyword.iot_short_notm}}:
- Device reboot
- Factory reset
- Firmware download
- Firmware update

If the default device actions that are provided by {{site.data.keyword.iot_short_notm}} are not sufficient for your devices and applications, consider developing further device management capabilities by implementing a device management extension package.

## Device management extension packages
{: #device_management_ext}

A device management extension package is a JSON document that defines a set of device management actions. The actions can be initiated against one or more devices that support those actions. The actions are initiated in the same way as the default device management actions by using either the {{site.data.keyword.iot_short_notm}} dashboard or the device management REST API commands.

The following code sample outlines the typical format of a device management extension package:

```

	{
		"bundleId": "<unique identifier>",
		"displayName": {
			"<locale 0>": "<localized display name 0>"
		},
		"description": {
			"<locale 0>": "<localized description 0>"
		},
		"version": "<bundle version>",
		"provider": "<bundle provider>",
		"actions": {
			"<actionId 0>": {
				"actionDisplayName": {
					"<locale 0>": "<localized action display name 0>"
				},
				"description": {
					"<locale 0>": "<localized description>"
				},
				"parameters": [
					{
						"name": "<parameterId>",
						"value": "<regex pattern for value checking>",
						"required": false,
						"defaultValue": "<default>"
					}
				]
			}
		}
	}

```

### Extension package properties

A device management extension package contains the following properties:

|Property|Description|Required
|:---|:---|:---|
|``bundleId``|Unique identifier for a device management extension.|Yes|
|``version``|Version string for a device management extension.|No|
|``provider``|Provider string for a device management extension that must be no greater than 1024 characters.|No|
|``displayName``|Map of ``locale``: ``String`` key-value pairs that are used for display in the {{site.data.keyword.iot_short_notm}} dashboard. You must specify at least one entry.|Yes|
|``description``|Map of ``locale``: ``String`` key-value pairs that are used for display in the {{site.data.keyword.iot_short_notm}} dashboard. If defined, you must specify at least one entry.|No|
|``actions``| Map of ``actionId``: ``<action>`` key-value pairs that define the actions that are contained within a device management extension. You must specify at least one entry.|Yes|

### Properties per action:

|Property|Description|Required
|:---|:---|
|``actionDisplayName``|Map of ``locale``: ``String`` key-value pairs that are used for display in the {{site.data.keyword.iot_short_notm}} dashboard. You must specify at least one entry.|Yes|
|``description``|Map of ``locale``: ``String`` key-value pairs that are used for display in the {{site.data.keyword.iot_short_notm}} dashboard. Optional. You must specify at least one entry.|No|
|``parameters``|Array of parameters that are allowed for a particular action. If defined, you must specify at least one entry.|No|

### Properties per action parameter:

|Property|Description|Required
|:---|:---|
|``name``|Unique identifier for a parameter within an action|Yes|
|``value``|Regular expression that is used to validate parameter values when a request is initiated. If not specified, validation does not occur.|No|
|``required``|Boolean value that determines whether the parameter is required. The value is set by default to false. |No|
|``defaultValue``|Value to be used if the parameter is not provided when a request is initiated|No|

**Note:** The ``bundleId``, ``version``, ``actionId``, and ``parameterId`` values can contain no more than  255 characters and can consist of only alpha-numeric characters (a-z, A-Z, 0-9) and the following special characters:
 - dash (-)
 - underscore (_)
 - dot (.)

## REST APIs
{: #rest_api}

Use the following {{site.data.keyword.iot_short_notm}} REST API commands to manage your extension packages:

- To get a list of all device management extension packages:
  `GET https://<orgId>.internetofthings.ibmcloud.com:443/api/v0002/mgmt/custom/bundle`
- To create a new device management extension package:
  `POST https://<orgId>.internetofthings.ibmcloud.com:443/api/v0002/mgmt/custom/bundle`
- To get a specific device management extension package:
  `GET https://<orgId>.internetofthings.ibmcloud.com:443/api/v0002/mgmt/custom/bundle/{bundleId}`
- To update a device management extension package:
  `PUT https://<orgId>.internetofthings.ibmcloud.com:443/api/v0002/mgmt/custom/bundle/{bundleId}`
- To delete a device management extension package:
  `DELETE https://<orgId>.internetofthings.ibmcloud.com:443/api/v0002/mgmt/custom/bundle/{bundleId}`

For more information about the REST APIs for device management extension packages, see the [{{site.data.keyword.iot_short_notm}} API V2](https://docs.internetofthings.ibmcloud.com/swagger/v0002.html){: new_window} documentation.


##Supporting custom device management actions
{: #supporting_custom_device_management_actions}

Device management actions that are defined in your extension packages can be initiated only by devices that support those actions. When a device publishes a manage request to the {{site.data.keyword.iot_short_notm}}, the device specifies the types of actions that it can  support.

To receive custom actions from an extension package, the device must specify the bundle identifier for the extension package in the supports object of the request, as outlined in the following example:

```
	Outgoing message from device:

	Topic: iotdevice-1/mgmt/manage
	{
		"d": {
			"supports": {
				"deviceActions": false,
				"firmwareActions": false,
				"<bundleId>": true
			}
		},
		"reqId": "<request id>"
	}

	Incoming response from server:

	Topic: iotdm-1/response
	{
		"rc": 200,
		"reqId": "<request id>"
	}

```

For more information about device manage requests, see [Device Management Protocol](index.html){: new_window}.

## Initiating custom device management actions
{: #initiating_custom_dm_actions}

To initiate custom device management actions, use the following REST API command, which is the default command for initiating device management actions.

`POST https://<orgId>.internetofthings.ibmcloud.com:443/api/v0002/mgmt/requests`

You must provide the following information when you initiate a request:

- The action ``<bundleId>/<actionId>``
- A list of devices to initiate the action against, up to a maximum of 5000 devices
- A list of parameters, as defined in the custom action definition

The payload for initiating a request is in the following format:

```
	{
		"action": "<bundleId>/<actionId>",
		"devices": [
			{
				"typeId": "<deviceType 0>",
				"deviceId": "<deviceId 0>"
			}
		],
		"parameters": [
			{
				"name": "<parameter0>",
				"value": "<parameter0 value>"
			}
		]
	}

```


## Handling custom device management actions
{: #handling_custom_dm_actions}

When a custom action is initiated against a device, an MQTT message is published to the device. The MQTT message contains any parameters that were specified as part of the request. When the device
receives the MQTT message, it either runs the action or responds with an error code that indicates why it cannot currently complete the action.

When a device action is successfully completed, the device publishes a response whereby the ``rc`` value is set to ``200``.

The following extract provides an example of the exchange that occurs between a server and a device.

```
	Incoming message from the server:

	Topic: iotdm-1/mgmt/custom/<bundleId>/<actionId>
	{
		"d": {
			"fields": [
				{
					"field": "<parameter0>",
					"value": "<parameter0 value>"
				}
			]
		},
		"reqId": "<request id>"
	}

	... device carries out the requested action ...

	Outgoing message from the device:

	Topic: iotdevice-1/response
	{
		"rc": 200,
		"reqId": "<request id>"
	}

```

## Example
{: #example}

The following example demonstrates how you can define a new device management extension and execute an action defined within that extension.

Some companies manufacture ``exampleDeviceType`` devices. You can install and manage plug-ins to run on ``exampleDeviceType`` devices. To facilitate remote management of plug-ins on ``exampleDeviceType`` devices, the manufacturer typically provides a device management extension that you can import into your {{site.data.keyword.iot_short_notm}} organization.

The following extension JSON document is used in this example:

```
	{
		"bundleId": "exampleDeviceType-actions-v1",
		"displayName": {
			"en_US": "exampleDeviceType Actions v1"
		},
		"description": {
			"en_US": "Device management actions for exampleDeviceType devices"
		},
		"version": "1.0",
		"provider": "some company",
		"actions": {
			"installPlugin": {
				"actionDisplayName": {
					"en_US": "Install Plug-in"
				},
				"description": {
					"en_US": "Install a new plug-in on the device"
				},
				"parameters": [
					{
						"name": "pluginId",
						"value": "\\w+",
						"required": true
					},
					{
						"name": "pluginURI",
						"value": "((http:\\/\\/|https:\\/\\/)(.*)+)",
						"required": true
					}
				]
			},
			"enablePlugin": {
				"actionDisplayName": {
					"en_US": "Enable Plug-in"
				},
				"description": {
					"en_US": "Enables a plug-in on the device"
				},
				"parameters": [
					{
						"name": "pluginId",
						"value": "\\w+",
						"required": true
					}
				]
			},
			"disablePlugin": {
				"actionDisplayName": {
					"en_US": "Disable Plug-in"
				},
				"description": {
					"en_US": "Disables a plug-in on the device"
				},
				"parameters": [
					{
						"name": "pluginId",
						"value": "\\w+",
						"required": true
					}
				]
			},
			"uninstallPlugin": {
				"actionDisplayName": {
					"en_US": "Uninstall Plug-in"
				},
				"description": {
					"en_US": "Uninstall a plug-in from the device"
				},
				"parameters": [
					{
						"name": "pluginId",
						"value": "\\w+",
						"required": true
					}
				]
			}
		}
	}

```
In this device management extension package, the following actions are defined:

- **installPlugin**
- **enablePlugin**
- **disablePlugin**
- **uninstallPlugin**

To add the extension, use the following REST API command:

`POST https://<orgId>.internetofthings.ibmcloud.com:443/api/v0002/mgmt/custom/bundle`

Devices that are registered to the organization ``<orgId>`` can specify that they support ``exampleDeviceType-actions-v1`` actions when they publish a manage request, as outlined in the following example:

```
	Outgoing message from device:

	Topic: iotdevice-1/mgmt/manage
	{
		"d": {
			"supports": {
				"exampleDeviceType-actions-v1": true
			}
		},
		"reqId": "f38faafc-53de-47a8-a940-e697552c3194"
	}

```
The device in question receives the following response from the {{site.data.keyword.iot_short_notm}}:

```
	Incoming message from server:

	Topic: iotdm-1/response
	{
		"rc": 200,
		"reqId": "f38faafc-53de-47a8-a940-e697552c3194"
	}

```
At this point, you can initiate the device actions that you defined in the ``exampleIoT-exampleDeviceType-v1`` extension.

The payload for initiating an ``installPlugin`` action is as follows:

```
	{
		"action": "exampleDeviceType-actions-v1/installPlugin",
		"devices": [
			{
				"typeId": "exampleDeviceType",
				"deviceId": "device0"
			},
			{
				"typeId": "exampleDeviceType",
				"deviceId": "device1"
			}
		],
		"parameters": [
			{
				"name": "pluginId",
				"value": "testPluginA"
			},
			{
				"name": "pluginURI",
				"value": "http://www.example.com/testPluginA.zip"
			}
		]
	}

```
Initiate the request by using the following REST API command:

`POST https://<orgId>.internetofthings.ibmcloud.com:443/api/v0002/mgmt/requests`

When the command is submitted, devices ``device0`` and ``device1`` of type ``exampleDeviceType`` receive the following MQTT message:

```
	Incoming message from server:

	Topic: iotdm-1/mgmt/custom/exampleDeviceType-actions-v1/installPlugin
	{
		"d": {
			"fields": [
				{
					"field": "pluginId",
					"value": "testPluginA"
				},
				{
					"field": "pluginURI",
					"value": "http://www.exampleiot.com/testPluginA.zip"
				}
			]
		},
		"reqId": "d38faafc-53de-47a8-a940-e697552c3194"
	}

```

Each device takes an action on the message and installs the specified plug-in. When the installation is finished, the devices submit a message to indicate that the action was completed successfully.

```
	Outgoing message from device:

	Topic: iotdevice-1/response
	{
		"rc": 200,
		"reqId": "d38faafc-53de-47a8-a940-e697552c3194"
	}

```

At this point, the ``installPlugin`` device management action is completed.

## API examples
{: #api_examples}

Use the following API requests to manage your devices:

- To create a new device management extension:

`curl -XPOST -d '<insert payload here>' -H "Content-Type: application/json" -u "<apiKey>:<apiToken>" https://<orgId>.internetofthings.ibmcloud.com:443/api/v0002/mgmt/custom/bundle`

- To list device management extensions:

`curl -XGET -H "Content-Type: application/json" -u "<apiKey>:<apiToken>" https://<orgId>.internetofthings.ibmcloud.com:443/api/v0002/mgmt/custom/bundle`

- To initiate a device management request:

`curl -XPOST -d '<insert payload here>' -H "Content-Type: application/json" -u "<apiKey>:<apiToken>" https://<orgId>.internetofthings.ibmcloud.com:443/api/v0002/mgmt/requests`

- To list device management requests that are either in progress or completed:

`curl -XGET -H "Content-Type: application/json" -u "<apiKey>:<apiToken>" https://<orgId>.internetofthings.ibmcloud.com:443/api/v0002/mgmt/requests`

- To view the status of a particular device management request:

`curl -XGET -H "Content-Type: application/json" -u "<apiKey>:<apiToken>" https://<orgId>.internetofthings.ibmcloud.com:443/api/v0002/mgmt/requests/<requestId>`
