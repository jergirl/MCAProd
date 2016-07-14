---

copyright:
  years: 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}


# Getting started with {{site.data.keyword.iot_short_notm}} Starter
{: #gettingstartedtemplate}
<!-- Provide and appropriate ID above -->
*Last updated: 27 June 2016*
{: .last-updated}

Get started with {{site.data.keyword.iot_full}} by using the {{site.data.keyword.iot_short_notm}} Starter boilerplate. With the Starter, you can quickly simulate a device, create cards, generate data, and begin analyzing and displaying data in the {{site.data.keyword.iot_short_notm}} dashboard.
{: shortdesc}

The Starter automatically deploys and connects these services:

{{site.data.keyword.iot_short_notm}} - The platform gives you a versatile IoT toolkit that includes gateway devices, device management, and powerful application access. By using {{site.data.keyword.iot_short_notm}}, you can collect connected device data and perform analytics on real-time data from your organization.

{{site.data.keyword.sdk4nodefull}} - creates a runtime environment in which Node-RED runs.

{{site.data.keyword.cloudantfull}} - a database in which Node-RED stores metadata.

## About {{site.data.keyword.iot_short_notm}}
{: #about_iotplatform}
{{site.data.keyword.iot_short_notm}} provides powerful application access to IoT devices and data to help you rapidly compose analytics applications, visualization dashboards, and mobile IoT apps.
{{site.data.keyword.iot_short_notm}} allows you to perform powerful device management operations, and store and access device data, connect a wide variety of devices and gateway devices. {{site.data.keyword.iot_short_notm}} provides secure communication to and from your devices by using MQTT and TLS.

## About Node-RED
{: #about_nodered}
Node-RED is a tool for wiring together hardware devices, APIs, and online services in new and interesting ways.  You can use Node-RED to create a simulated thermostat that sends simulated data to your {{site.data.keyword.iot_short_notm}} service. You can create cards to display real-time data in the {{site.data.keyword.iot_short_notm}} dashboard. For more information, see the [Node-RED documentation](https://console.ng.bluemix.net/docs/starters/Node-RED/nodered.html#nodered).

## Getting Around
{: #gettingaround}
As you perform the following steps, you will use three different tabs in your browser:
  1. *{{site.data.keyword.Bluemix_notm}} dashboards* - Use the {{site.data.keyword.Bluemix_notm}} dashboard to see the state of your deployment, read documentation and to launch the dashboards.
  2. *{{site.data.keyword.iot_short_notm}} dashboard* - Use the dashboard to work with this service. You'll use the dashboard to define device types, register devices, monitor incoming sensor data, create data visualization cards, and see live data visualizations.
  3. *Node-RED* - Running as a node.js web application, you'll configure and run the device simulator flow, and work with other flows to process data from {{site.data.keyword.iot_short_notm}}.

## Defining a simulated device in {{site.data.keyword.iot_short_notm}}
{: #definingsimdev}
Register your device with {{site.data.keyword.iot_short_notm}}:
  1.	In {{site.data.keyword.Bluemix_notm}}, go to the overview tab for your deployed application.
  2.	Click the {{site.data.keyword.iot_short_notm}} box in the Connections section or tab.
  3.	Click Launch dashboard to open the {{site.data.keyword.iot_short_notm}} dashboard in a new browser window.
  4.	Select Devices
  5.	Click Add Device
  6.	Click Create device type in the Add Device dialog.
  7.	Click Create device type in the Create Device Type dialog.
  8. Enter a descriptive name and description for the device type, such as thermostat.
  9.	Skip: Define Template.
  10.	Skip Metadata.
  11.	Click Create to add the new device type.
  12.	Click Next to add your device (Choose Device Type is preselected).
  13.	Enter a device ID such as LivingRoomThermo1.
  14.	Skip: Enter device metadata.
  15.	Click Next to add a device connection with an auto-generated authentication token.
  16.	Verify that the summary information is correct, and then click Add to add the connection.
  17.	In the device information page that opens, copy and save the device information:
      -	Organization ID
      -	Device Type
      -	Device ID
      - Authentication Method
      - Authentication Token

**Tip**: You will need Organization ID, Device Type, and Device ID in the next few steps to finalize the configuration of the Node-RED application to complete the connection.

## Configuring and running the Node-RED device simulator.
{: #confignodered}
Configure the Node-RED device simulator. Use the device simulator to send MQTT device messages to {{site.data.keyword.iot_short_notm}}. The device simulator sends temperature and humidity information to {{site.data.keyword.iot_short_notm}}.

1. In your Bluemix dashboard, open Node-RED by selecting **View App** or clicking the link (for example, http:// myIoTApp.mybluemix.net).
2.	Click **Go to your Node-RED flow editor** to open the editor.
3.	Double-click the blue **Send** to {{site.data.keyword.iot_short_notm}} node in the Device Simulator flow.
  1.	Verify that Authentication = Bluemix Service
  2.	Paste the Device Type from the device you registered.
  3.	Paste the Device ID from the device you registered.
  4.	Click OK.
4.	In the upper right corner of the Node-RED flow editor, click **Deploy**.
5.	Configure the Node-RED Temperature Monitor flow
  1.	Double-click the blue IBM IoT App In node in the Device Simulator flow.
  2.	Change Authentication to Bluemix Service
  3.	Select All for Device Type, Device Id, Event, and Format
  4.	Click OK.
6.	In the upper right corner of the Node-RED flow editor, click **Deploy**.
7.	Validate the device connection
  1.	In your other browser tab or window, return to the {{site.data.keyword.iot_short_notm}} dashboard.
  2.	Select Devices and click LivingRoomThermo1 or the name of the device that you added, if different.  
  The device information page opens. This view lets you see the connection status for your device. The device status is disconnected.
  3.	Back in your Node-RED flow editor, click the button on the gray Send Data node to generate an asset payload.
  The payload contains the following data points:
  ```
  {"d":{"temp":15,"humidity":50,"location":{"longitude":-98.49,"latitude":29.42}}}
  ```
  4.	In the debug tab of the right pane, verify that messages are created.
  5.	In the {{site.data.keyword.iot_short_notm}} device information page, verify that you see the same data points received from the device in the Sensor Information section.

8.	Connect your sample IoT device to {{site.data.keyword.iot_short_notm}} to view device data.

## Creating cards in {{site.data.keyword.iot_short_notm}} to show live data
{: #createcards}
To create cards, perform the following tasks.

### Automatically generate data every 3 seconds
1. In the Node-RED tab, double-click the Send Data node
2.	Set Repeat to Interval Every 3 seconds
3.	Deploy

### Create new cards in the dashboard
1. Go to the {{site.data.keyword.iot_short_notm}} dashboard browser tab.
2. Select BOARDS.
3. Click Create New Board.
4. Give it a name like Home Environment.
5. Create.
6. Click Add New Card (for temperature).
   1.	Under Devices, select Realtime chart.
   2.	Card source data, check your Device "LivingRoomThermo1", then click Next.
   3. Connect new data set.
       - Name: Temperature
       - Event: update
       - Property: temp
       - Type: Float
       - Unit: °C
       - Precision: 2
       - Min: 0
       - Max: 50
       - Next
  4. Card preview.
       - Select L
       - Next
  5. Card information.
       - Title: Temperature
  6.	Submit.
  7.	The temperature card appears on the dashboard and includes a graph of the live temperature data.
7.	Click Add New Card (for humidity).
  1.	Under Devices, select Show more.
  2.	Select Gauge.
  3.	Card source data, check your Device, then click Next.
  4.	Connect new data set.
       -	Name: Humidity
       -	Event: update
       -	Property: humidity
       -	Type: Float
       -	Unit: "% relative humidity"
       -	Precision: 1
       -	Min: 10
       -	Max: 95
       -	Next
  5.	Card preview.
       -	Settings
          -	Lower threshold: 40 and fair
          -	Middle: good
          -	Upper threshold: 50% and fair
       -	Select M
       -	Next
  6.	Card information.
       -	Title: Humidity
  7.	Submit.
  8.	The humidity card appears on the dashboard and includes a gauge that shows the live humidity data.
8.	Click Add New Card (for location).
  1.	Under Devices, select Show more.
  2.	Select Value.
  3.	Card source data, check your Device. "LivingRoomThermo1", then click Next.
  4.	Connect new data set.
       -	Name: Latitude
       -	Event: update
       -	Property: location.latitude
       -	Type: Float
       -	Unit: "°N"
       -	Precision: 2
       -	Min: -180
       -	Max: 180
  5. Connect new data set.
       -	Name: Longitude
       -	Event: update
       -	Property: location.longitude
       -	Type: Float
       -	Unit: "°E"
       -	Precision: 2
       -	Min: -180
       -	Max: 180
       -  Next
  6.	Card preview.
       -	Select L
       -	Next
  7.	Card information.
       -	Title: Location
  8.	Submit.
9.	Watch your new cards update in real time with the simulator data generated by the Node-RED flow.
**Note**: Node-RED continues to send data until you stop it.
10.	In the Node-RED flow editor, update the Send Data node to Repeat: none.
11.	Deploy.

## What's next?
{: #whatsnext}
Now that your simulated device is sending data to {{site.data.keyword.iot_short_notm}}, you can continue to iterate on your IoT project.

1. [Search our IoT Recipes](https://developer.ibm.com/recipes/?post_type=tutorials&s=watson+iot) to connect a physical device such as a Raspberry Pi and send data to {{site.data.keyword.iot_short_notm}}.
2. [Deploy a sample node.js application to visualize device data.](https://www.bluemix.net/docs/services/IoT/visualizingdata_sample.html)
3.	Password protect the Node-RED flow editor. By default, the editor is open for anyone to access and modify flows. To password-protect the editor, perform the following tasks:
  1.	In the Bluemix dashboard, select the 'Environment Variables' page for your application.
  2.	Add the following user-defined variables:
       -	NODE_RED_USERNAME - the username to secure the editor
       -	NODE_RED_PASSWORD - the password to secure the editor
  3.	Click Save.


# Related Links
{: #rellinks}

## Tutorials and Samples
{: #samples}
* [Recipes for connecting your devices](https://developer.ibm.com/recipes/?post_type=tutorials&s=iot){:new_window}
* [{{site.data.keyword.iot_short}} Play organization](https://play.internetofthings.ibmcloud.com/){:new_window}
* [Connecting an Intel Galileo to the {{site.data.keyword.iot_short}}](https://developer.ibm.com/recipes/tutorials/connect-an-intel-galileo-to-the-internet-of-things-foundation-connect/){:new_window}
* [Connecting an ARM&reg; mbed&trade; IoT Starter Kit](https://developer.ibm.com/recipes/tutorials/arm-mbed-iot-starter-kit-part-1/){:new_window}
* [Connecting a Raspberry Pi to {{site.data.keyword.iot_short}}](https://developer.ibm.com/recipes/tutorials/raspberry-pi-4/){:new_window}

## API Reference
{: #api}
* [{{site.data.keyword.iot_short}} API Documentation](https://docs.internetofthings.ibmcloud.com/swagger/v0002.html#/){:new_window}


## Related Links
{: #general}
* [{{site.data.keyword.iot_short_notm}} Documentation](https://www.bluemix.net/docs/services/IoT/iotplatform_overview.html){:new_window}
* [{{site.data.keyword.sdk4nodefull}} starter documentation](https://console.ng.bluemix.net/docs/starters/Node-RED/nodered.html){:new_window}
