<span align="center">

# homebridge-eufy-clean
A Homebridge plugin for eufy RoboVac devices.

</span>

## Plugin Information
This Homebridge plugin enables you to control your eufy RoboVac using the Home App on your Apple devices via HomeKit.

## Features
* Switch On & Off: Switching "On" performs that same action as tapping "Clean" in the eufy Clean app. Switching Off performs the same action as tapping "Recharge" in the eufy Clean app. This stops any in progress cleaning and your eufy RoboVac device will return to its charging base.
<!-- These are a work in progress and not currently available in the plugin.
* Displays Battery Charging State & Level: You will also receive low battery notifications.
* Allows you to use Find My Robot: This performs the same action as tapping "Find My Robot" in the eufy Clean app.
-->

## Prerequisites
To install and use this plugin you must:
* Homebridge installed (version 1.7.0 and later).
* The latest version of supported Node.js LTS is installed, this is currently v18.19.1 or v20.11.1.
* For configuration, using Homebridge UI is recommended.


## Configuration

### Getting the "device ID" & "local key"

Configuration of your eufy RoboVac device requires you to find your eufy RoboVac's device ID and local key. To find out what your eufy RoboVacs device ID and local key are, you must use the "eufy Clean device ID & local key grabber".

Download the [`eufy-clean-local-key-grabber`](https://github.com/Rjevski/eufy-clean-local-key-grabber/tree/master).

Using Python 3.9 (other versions are untested), execute the following commands in the directory that the "eufy Clean device ID & local key grabber" was extracted to:

```bash
pip install -r requirements.txt
python -m eufy_local_id_grabber "<EUFY ACCOUNT EMAIL>" "<EUFY ACCOUNT PASSWORD>"
```

It will return the following outputs:

```
Home: <home ID>
Device: RoboVac, device ID <device ID>, local key <local key>
```

There may be more than one device returned if you have multiple devices in your eufy Clean "Home". Make note of all the device ID & local Key for all the devices you want to configure with this plugin.

### Installing & Configuring the Plugin Using the Homebridge UI

The easiest way to install & configure this plugin is to use the Homebridge UI.

Using the Homebridge UI, simply enter the required information to add your eufy RoboVac device:
* RoboVac Name
* RoboVac IP Address
* device ID
* local key

The plugin will then discover & add your eufy RoboVac device.

It is recommended you then configure the plugin as a Child Bridge for optimal performance of Homebridge and the plugin.

### Installing & Configuring the Plugin Manually

To install the plugin manually, run the below command:
```bash
npm install -g homebridge-eufy-clean
```

You can configure the plugin manually by modifying your Homebridge's `config.json` file and adding to below to the `accessories` section:
  ```json
    {
      "accessoryType": "Eufy RoboVac",
      "accessoryName": "<The name of your eufy RoboVac>",
      "accessoryIp": "<The IP address of your eufy RoboVac>",
      "deviceId": "<deviceId>",
      "localKey": "<localKey>",
      "displayAs": "<switch | fan, defaults to switch>",
      "enableDebugLog": "<true | false, defaults to false>"
    }
  ``` 

### Advanced Configuration

#### Home App Configuration

Since HomeKit does not currently natively support vacuums, your eufy RoboVac device will be displayed in the Home app as either a Switch (default) or Fan. This depends on what choice you make when configuring the plugin. For Homebridge UI users, this is configured in the "eufy RoboVac Accessory Type" dropdown menu, for manual configuration users, edit the JSON Config to include the below:
  ```json
      "displayAs": "switch"
  ``` 

<!-- Not currently enabled in the plugin.
If Find My Robot is disabled, the find functionality with not be present in the Home app. Find My Robot can be disabled by adding the below into the JSON configuration:
  ```json
      "hideFindButton": true
  ``` 
-->

<!-- Not currently enabled in the plugin.
Your eufy RoboVac can report errors via the Home app using a "Motion Sensor". The Motion Sensor is activated when an error is reported. You can use this to configure alerts and other automations in the Home app. This can be disabled by adding the below into the JSON configuration:
  ```json
      "hideErrorSensor": true
  ``` 
-->
#### Debug Logging
This plugin can output additional logging into the Homebridge log output. This can be useful for troubleshooting purposes or to report issues with the plugin. 

For Homebridge UI users, this is configured by selecting "Enable Debug Log", for manual configuration users, edit the JSON Config to include the below:
  ```json
      "enableDebugLog": true
  ``` 

## Disclaimer
* I am in no way affiliated with eufy or Anker. This Homebridge plugin is a personal project is maintained in my free time.
* Use of this Homebridge plugin entirely at your own risk. Please see license for more information.

<!--
README.md Version History

v2024.02.14 - Initial README.md creation.