# TryFi for Home Assistant
![beta_badge](https://img.shields.io/badge/maturity-Beta-yellow.png?style=for-the-badge)
[![](https://img.shields.io/github/release/sbabcock23/hass-tryfi/all.svg?style=for-the-badge)](https://github.com/sbabcock23/hass-tryfi/releases)
![release_date](https://img.shields.io/github/release-date/sbabcock23/hass-tryfi.svg?style=for-the-badge)
[![hacs_badge](https://img.shields.io/badge/HACS-Default-orange.svg?style=for-the-badge)](https://github.com/hacs/integration)
[![](https://img.shields.io/github/license/sbabcock23/hass-tryfi?style=for-the-badge)](LICENSE)
[![](https://img.shields.io/github/workflow/status/sbabcock23/hass-tryfi/Validate%20with%20hassfest?style=for-the-badge)](https://github.com/sbabcock23/hass-tryfi/actions)

This allows you to integrate [TryFi](https://tryfi.com) Smart GPS Collars with Home Assistant. 

## Features
Current functionality includes:
* Device Tracker - your pet will show up in HA using the GPS coordinates from the collar
* Step Counter - it will report your pets daily, weekly, and monthly steps
* Distance Counter - it will report your pets daily, weekly and monthly distance
* Battery Level - it will report your Pet's collar battery level
* Collar Light - you can control the light on the collar by turning it on and off (color selection coming soon!)
* Lost Dog Mode - allows you to "unlock" your dog if it is lost and "lock" it when it is found
* Bases - reports the status of the base (online/offline)

## Donate
If you would like to donate you can use my TryFi referral code "[395FX4](https://shop.tryfi.com/r/395FX4/?utm_source=referrals)" on your next purchase.

# Installation
## Pre-Requisities
* Home Assistant >= 0.0.117
* TryFi dog collar with active cellular subscription
* [HACS](https://github.com/custom-components/hacs) is already installed

## Installation Methods

### HACS Install
1. Search for `TryFi` under `Integrations` in the HACS Store tab.
2. Add the [Integration](#configuration) to your HA and configure.

### Manual Install
1. In your `/config` directory, create a `custom_components` folder if one does not exist.
2. Copy the [tryfi](https://github.com/sbabcock23/hass-tryfi/tree/master/custom_components) folder and all of it's contents to your `custom_components` directory.
3. Restart Home Assistant.
4. Add the [Integration](#configuration) to your HA and configure.

## Configuration
1. After installing TryFi go to Configuration --> Integrations and add a new Integration
2. Search for TryFi
3. Enter in your TryFi username and password. Optionally you can select a polling frequency option (in seconds). Suggestion is nothing less then 5.
4. Click Submit

![Setup](https://github.com/sbabcock23/hass-tryfi/blob/master/docs/setup.jpg?raw=true)

## Validation
Once you have added the integration, you will see 1 or more devices and entities associated with this integration. To validate its accuracy, you can review the steps and distance counters for your pet or its current whereabouts.

![Integration](https://github.com/sbabcock23/hass-tryfi/blob/master/docs/tryfiaftersetup.jpg?raw=true)

### Dog Device and Entities
#### Device

![Dog Device](https://github.com/sbabcock23/hass-tryfi/blob/master/docs/dogdevice.jpg?raw=true)

#### Entities

![Dog Entities](https://github.com/sbabcock23/hass-tryfi/blob/master/docs/dogentities.jpg?raw=true)

### Base Device and Entities

![Base Device and Entities](https://github.com/sbabcock23/hass-tryfi/blob/master/docs/dogbase.jpg?raw=true)

# How to Use
## Light Collar
The light on your Pet's collar is represented as a light switch in HA. It can either be turned on or off. 

![Lovelace](https://github.com/sbabcock23/hass-tryfi/blob/master/docs/doglight.jpg?raw=true)

## Lost Dog Mode
TryFi is equiped with a "Lost Dog Mode" functionality. In HA this is represented by a "lock" device similar to a lock in your home. If the pet is "locked" then everything is safe and secure. If the pet is unlocked then it must be lost :(

![Lovelace](https://github.com/sbabcock23/hass-tryfi/blob/master/docs/doglostmode.jpg?raw=true)

# Lovelace

## Entities
```
type: entities
entities:
  - entity: lock.harley_lost_state
  - entity: sensor.harley_collar_battery_level
  - entity: sensor.home_base
  - entity: sensor.harley_daily_steps
  - entity: sensor.harley_weekly_steps
  - entity: sensor.harley_monthly_steps
  - entity: sensor.harley_daily_distance
  - entity: sensor.harley_weekly_distance
  - entity: sensor.harley_monthly_distance
```
## Light
```
type: light
entity: light.harley_collar_light
```

# Automation Examples
## Turn on the Collar Light After Dark
Turns on the collar light after dark if the pet is not home.
```
- id: '1604060166498'
  alias: Turn on Light After Dark If Not Home
  description: ''
  trigger:
  - platform: sun
    event: sunset
  condition:
  - condition: and
    conditions:
    - condition: device
      device_id: a7237a6c1144fcd90828b21de2572603
      domain: device_tracker
      entity_id: device_tracker.pet_tracker
      type: is_not_home
  action:
  - type: turn_on
    device_id: a7237a6c1144fcd90828b21de2572603
    entity_id: light.pet_collar_light
    domain: light
  mode: single
```

# Known Issues
* It sometimes takes time for the status to accurately refresh in HA. For example the light on/off status and the lock/unlock status.

# Future Enhacements
* Allow for the selection of the LED light color
* Enable possibility of if pet not home and not with owner then trigger lost dog mode

# Version History
## 0.0.9
* Updated dependency version of pytryfi
* Fixed [Issue #30](https://github.com/sbabcock23/hass-tryfi/issues/30) - Convert to Async
## 0.0.8
* Updating dependency version of pytryfi
## 0.0.7
* Updating dependency version of pytryfi
## 0.0.6
* Steps unit was added to enable charting of dogs steps over time.
## 0.0.5
* Fixed [Issue #15](https://github.com/sbabcock23/hass-tryfi/issues/15) - dependency update
## 0.0.4
* Fixed [Issue #17](https://github.com/sbabcock23/hass-tryfi/issues/17) - converted to async
## 0.0.3
* Multiple bases fix
## 0.0.2
* Documentation updates
## 0.0.1
* Initial Release with basic functionality including light on/off, device tracker, lock mode of dog and general stats

# Links
* [Python TryFi Interface](https://github.com/sbabcock23/pytryfi)
* [TryFi]((https://tryfi.com/))