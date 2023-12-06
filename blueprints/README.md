# Blueprints

## Importing blueprints
You should be able to import these blueprints by clicking links below. If you want to do this manually, see instructions from Home Assistant documentation: https://www.home-assistant.io/docs/automation/using_blueprints/#importing-blueprints

## Automation blueprints

| Use Case / "I want to..."| What blueprint to use |
| --- | --- |
| ... allow/turn on device during cheapest n hours of the day <br> OR <br> ... allow/turn on device when price is below X €/kW <br> OR <br> ... allow/turn on device when price is below X €/kWh or during cheapest n hours of the day <br> OR <br> ... allow/turn on device when price is below X €/kWh and during cheapest n hours of the day | [![Open your Home Assistant instance and show the blueprint import dialog with a specific blueprint pre-filled.](https://my.home-assistant.io/badges/blueprint_import.svg)](https://my.home-assistant.io/redirect/blueprint_import/?blueprint_url=https%3A%2F%2Fgithub.com%2FT3m3z%2Fshf-spotprices2ha%2Ftree%2Fmain%2Fblueprints%2Fautomation%2Fspotprices2ha%2Frank-automation.yaml) . |
| ... allow/turn on device when cheapest adjacent n hours starts between two times  | Create a new time helper (Settings->Devices&Services->Helpers->Create Helper->"Date and/or time" + select "Date and Time"). <br><br> Then:<br> [![Open your Home Assistant instance and show the blueprint import dialog with a specific blueprint pre-filled.](https://my.home-assistant.io/badges/blueprint_import.svg)](https://my.home-assistant.io/redirect/blueprint_import/?blueprint_url=https%3A%2F%2Fgithub.com%2FT3m3z%2Fshf-spotprices2ha%2Ftree%2Fmain%2Fblueprints%2Fautomation%2Fspotprices2ha%2Fcheapest-period.yaml)  |
| ... continuously control for example a thermostat temperature during the day based on relative difference to the max price of today | [![Open your Home Assistant instance and show the blueprint import dialog with a specific blueprint pre-filled.](https://my.home-assistant.io/badges/blueprint_import.svg)](https://my.home-assistant.io/redirect/blueprint_import/?blueprint_url=https%3A%2F%2Fgithub.com%2FT3m3z%2Fspotprices2ha%2Ftree%2Fmain%2Fblueprints%2Fautomation%2Fshf-spotprices2ha%2Fcontinuous-control.yaml) |
| ... continuously control for example a thermostat temperature during the day based on your own curve based on electricity price. Can handle also other use cases where numerical state of an entity should be mapped to another value and some actions should be called. |[![Open your Home Assistant instance and show the blueprint import dialog with a specific blueprint pre-filled.](https://my.home-assistant.io/badges/blueprint_import.svg)](https://my.home-assistant.io/redirect/blueprint_import/?blueprint_url=https%3A%2F%2Fgithub.com%2FT3m3z%2Fshf-spotprices2ha%2Ftree%2Fmain%2Fblueprints%2Fautomation%2Fspotprices2ha%2Fmap-value.yaml) |

## Disclaimer

This package is a hobby project. I cannot guarantee that is works every time correctly and works in every situation as expected. There are most probably some bugs. You use this package at your own risk. Test what happens to your automation if your network connection is down and new prices aren't updated accordingly.
