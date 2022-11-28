# API.SPOT-HINTA.FI / Electricity Prices to Home Assistant 
Simple copy-paste approach to fetch data from api.spot-hinta.fi (see https://spot-hinta.fi) to Home Assistant. Includes simple sensors and UI elements to ease automation work. Intended for beginners who are not familiar with custom components which are more advanced integrations.

Example of UI elements (grouping is not included in the package):
![Example UI](/img/example.png)

## Installation instructions
Please make sure that you have made backups of your current implementation. You can find instructional video here: https://www.youtube.com/watch?v=lC_MxbWsh5k

Following instructions are for HassOS. You are most probably running this if you have Raspberry PI installation.

1. Install "File Editor" to be able to edit configuration files and upload configuration. Instructions can be found from here: https://www.home-assistant.io/getting-started/configuration/ Simplified version: Settings>Addons>press Add-on Store>"File Editor">Install>wait for installation to happen>add to sidebar by checking "Show in sidebar">start the add-on by pressing "Start">press Open Web UI. The main objective here is to get access to configuration files which can be achived also by SSH add-on.
2. Press folder icon on top left. Check that you are in /config folder (or the folder containing "configuration.yaml" file). Upload spot-price.yaml here with buttons located top right.
3. Open file "configuration.yaml". Find row "homeassistant:" and edit following rows to be like this:
```yaml
homeassistant: # Find this row and if it doesn't exists, you can copypaste this whole block to the file.
  packages: # NEW AND IMPORTANT ROW, NOTE INTENDATION
    pack_1: !include spot-price.yaml # NEW AND IMPORTANT ROW, NOTE INTENDATION
  # There might be code here. Leave it as is.
```
4. Restart Home Assistant. Settings>System>top right Restart button.

## Automation ideas

You can use slider "SHF Max Rank allowed" to determine how many of cheapest hours of today you want to select. This controls sensor "SHF Rank acceptable". SImilarly slider "SHF Max Price allowed" controls sensor "SHF Price Acceptable". Combination of these two sensors is presented as sensor "SHF Price or Rank acceptable".

Sliders "SHF Max Rank allowed" to determine how many of cheapest hours of today you want to select. This controls sensor "SHF Rank acceptable".

You can use sensor "SHF Cheapest period start" to run action at the start of cheapest N hours. See example below:
![Example Time Trigger based on Datetime helper](/img/example-time-trigger.png)

## Misc

Sensors are prefixed with "SHF" to prevent collision with possibly pre-existing sensors in your HomeAssistant instance. SHF is derived from Spot-Hinta.Fi.
