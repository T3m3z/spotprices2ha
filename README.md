# API.SPOT-HINTA.FI / Electricity Prices to Home Assistant 
Simple copy-paste approach to fetch Finnish Electricity Spot price data from api.spot-hinta.fi (see this site https://spot-hinta.fi for more info in Finnish and consider supporting that project) to Home Assistant. Includes simple sensors and UI elements to ease automation work. Intended for beginners who are not familiar with custom components which are more advanced integrations.

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
  packages: # NEW AND IMPORTANT ROW, NOTE INDENTATION
    pack_1: !include spot-price.yaml # NEW AND IMPORTANT ROW, NOTE INDENTATION
  # There might be code here. Leave it as is.
```
4. Restart Home Assistant. Settings>System>top right Restart button.

## Automation ideas

| Use Case / "I want to..."| What sensor to use |
| --- | --- |
| ... allow/turn on device during cheapest n hours of the day | Set value of *SHF Max Rank allowed* and use sensor *SHF Rank acceptable* in automations. |
| ... allow/turn on device when price is below X €/kWh | Set value of *SHF Max Price allowed* and use sensor *SHF Price acceptable* in automations. |
| ... allow/turn on device when price is below X €/kWh or during cheapest n hours of the day | Set value of *SHF Max Price allowed* and *SHF Max Rank allowed*. Then use sensor *SHF Price or Rank acceptable* in automations. |
| ... allow/turn on device when cheapest adjacent n hours starts (today or tomorrow)  | Create a new time helper (Settings->Devices&Services->Helpers->Create Helper->"Date and/or time" + select "Time"). Create automation which updates this helper (see example-of-cheapest-period-automation.yaml for an example). Then use the newly created helper in automations. ![Example Time Trigger based on Datetime helper](/img/example-time-trigger.png) |
| ... continuously control for example a thermostat temperature during the day based on relative difference to the max price of today | Use either sensor *SHF Control Factor 0-1* (outputs number between 0 and 1) or sensor *SHF Control Factor +-1* (outputs number between -1 and +1). You can see the difference between Rank and control factors in the following image. ![Rank versus control factor](/img/rank-versus-controlfactor.PNG) An example of automation action could be something like this: ![Automation action](/img/continuous-control.png) |

## Margin and transmission fees

If you want, you can add transmission and other extra fees to the spot prices. Price2 is added to prices between SHF Price2 start and SHF Price2 stop (only hours matter in the UI even though you can set minutes). Outside those hours Price1 will be added and used in the internal logic.

![Controlling of extra fees](/img/extra-fees.PNG)

## Visualization of the price data

After you have completed the installation, you can visualize the price data by installing chart code 

1. Download apexcharts-card.js from here: https://github.com/RomRider/apexcharts-card/releases
2. Access folder /config again by using File Editor. 
3. Create a new folder called www and upload apexcharts-card.js to the newly created folder.
4. Go to HomeAssistant "homepage" > press three dots at top right > Edit Dashboard > again press the three dots > Manage Resources.
5. Press Add Resource. Fill in URL /local/apexcharts-card.js and choose "JavaScript Module". Press Update.
6. Go to HomeAssistant "homepage" and make sure that you are in the edit mode (first part of step 4). Press Add Card > Search for "Manual" and select it.
7. Copy code from [here](/apexchart-card-visualisations/current_electricity_price.yaml) to the left side of the dialog.
8. Press save and enjoy.

![Example Chart](/img/chart.png)

## Misc

Sensors are prefixed with "SHF" to prevent collision with possibly pre-existing sensors in your HomeAssistant instance. SHF is derived from Spot-Hinta.Fi.

# Version history

| Version | New features/notes |
| --- | --- |
| 0.2.2 | "SHF Rank now" sensor takes now into account transmission fees etc configured using SHF Price 1/2 |
| 0.2.1 | Add validation automation for SHF Price2 start/stop |
| 0.2.0 | Major rework of the code to address daylight saving time related problems. Reduces errors on System->Logs. New feature: Script can be used to get variable length "cheapest period" with configurable start and end times. Breaking changes: old "SHF Cheapest Period Start" removed due to adding new script based approach. |
| 0.1.11 | Bugfix as the code was not compatible with HomeAssistant 2023.05+ |
| 0.1.10 | Fixed rounding error with "SHF Cheapest Period Start". Old code rounded values to 1/10ths of a cent and sometimes this wasn't precise enough causing wrong hour to be selected. |
| 0.1.9 | Fix for "SHF Cheapest Period Start". Calculates now cheapest period between today 15 o'clock and tomorrow 15 o'clock. Ensures that there is one period during 24 hours and can utilize periods spanning on two separate days (for example starting at 23 o'clock). |
| 0.1.8 | Add sensor for 7 day average price. |
| 0.1.7 | Bug fixes in order to ensure smooth data load. |
| 0.1.6 | Added price margins in order to add transmission fees to the prices.  |
| 0.1.5 | Adds attributes to sensors "SHF Control Factor 0-1" and "SHF Control Factor +-1" to allow charting future control. |
| 0.1.4 | Initial implementation for sensors "SHF Control Factor 0-1" and "SHF Control Factor +-1" to allow continuous control.  |
| 0.1.3 | Fixed bug in data loading which could prevent loading of the new prices.  |
| 0.1.2 | Sensor "SHF Electricity Price Now" has now attributes (for example today average price) which can be used in charts etc.  |
| 0.1.1 | Breaking change: add SHF prefix to all sensors etc. |
| 0.1 | Initial version |

# Disclaimer

This package is a hobby project. I cannot guarantee that is works every time correctly and works in every situation as expected. There are most probably some bugs. You use this package at your own risk. Test what happens to your automation if your network connection is down and new prices aren't updated accordingly.
