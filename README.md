# Anniversaries

[![hacs_badge](https://img.shields.io/badge/HACS-Default-orange.svg)](https://github.com/custom-components/hacs)
[![GitHub release (latest by date)](https://img.shields.io/github/v/release/pinkywafer/Anniversaries)](https://github.com/pinkywafer/Anniversaries/releases)
![GitHub Release Date](https://img.shields.io/github/release-date/pinkywafer/Anniversaries)
[![GitHub](https://img.shields.io/github/license/pinkywafer/Anniversaries)](LICENSE)

[![Maintenance](https://img.shields.io/badge/Maintained%3F-Yes-brightgreen.svg)](https://github.com/pinkywafer/Anniversaries/graphs/commit-activity)
[![GitHub issues](https://img.shields.io/github/issues/pinkywafer/Anniversaries)](https://github.com/pinkywafer/Anniversaries/issues)

[![Buy me a coffee](https://img.shields.io/static/v1.svg?label=Buy%20me%20a%20coffee&logo=buy%20me%20a%20coffee&logoColor=white&labelColor=ff69b4&message=donate&color=Black)](https://www.buymeacoffee.com/V3q9id4)

[![Support Pinkywafer on Patreon][patreon-shield]][patreon]

The 'anniversaries' component is a Home Assistant custom sensor which counts down to a recurring date such as birthdays, but can be used for any anniversary which occurs annually on the same date.

## Table of Contents

* [Installation](#installation)
  * [Manual Installation](#manual-installation)
  * [Installation via HACS](#installation-via-hacs)
* [Configuration](#configuration)
  * [Configuration Parameters](#configuration-parameters)
* [State and Attributes](#state-and-attributes)
  * [State](#state)
  * [Attributes](#attributes)
  * [Notes about unit of measurement](#notes-about-unit-of-measurement)

## Installation

### MANUAL INSTALLATION

1. Download the `anniversaries.zip` file from the
   [latest release](https://github.com/pinkywafer/anniversaries/releases/latest).
2. Unpack the release and copy the `custom_components/anniversaries` directory
   into the `custom_components` directory of your Home Assistant
   installation.
3. Configure the `anniversaries` sensor.
4. Restart Home Assistant.

### INSTALLATION VIA HACS

1. Ensure that [HACS](https://custom-components.github.io/hacs/) is installed.
2. Search for and install the "anniversaries" integration.
3. Configure the `anniversaries` sensor.
4. Restart Home Assistant.

## Configuration

Anniversaries can be configured on the integrations menu or in configuration.yaml

### Config Flow

In Configuration/Integrations click on the + button, select Anniversaries and configure the options on the form.

### configuration.yaml

Add `anniversaries` sensor in your `configuration.yaml`. The following example adds two sensors - Shakespeare's birthday and wedding anniversary!

```yaml
# Example configuration.yaml entry

anniversaries:
  sensors:
  - name: Shakespeare's Birthday
    date: '1564-04-23'
  - name: Shakespeare's Wedding Anniversary
    date: '1582-11-27'
```

### CONFIGURATION PARAMETERS

|Parameter |Optional|Description
|:----------|----------|------------
| `name` | No | Friendly name
|`date` | Either `date` or `date_template` MUST be included | date in format `'YYYY-MM-DD'` (or `'MM-DD'` if year is unknown)
|`date_template` | Either `date` or `date_template` MUST be included | Template to evaluate date from _(Note this is ONLY available in YAML configuration)_ The template must return a string in either `'YYYY-MM-DD'` or `'MM-DD'` format
| `count_up` | Yes | `true` or `false` changes the state to count up from a date (can be useful for non-recurring events) **Default**: `false`
| `one_time` | Yes | `true` or `false`. For a one-time event (Non-recurring) **Default**: `false`
| `show_half_anniversary` | Yes | `true` or `false`. Enables the `half_anniversary_date` and `days_until_half_anniversary` attributes. **Default**: `false`
| `unit_of_measurement` | Yes | Your choice of label N.B. The sensor always returns Days, but this option allows you to express this in the language of your choice without needing a customization
| `id_prefix` | Yes | Your choice of prefix for the entity_id **Default**: `anniversary_` NB. the entity_id cannot be changed from within the integration once it has been created.  You muse either delete your entity and re-create it or manually rename the entity_id on the configuration -> entities page
| `icon_normal` | Yes | Default icon **Default**:  `mdi:calendar-blank`
| `icon_today` | Yes | Icon if the anniversary is today **Default**: `mdi:calendar-star`
| `days_as_soon` | Yes | Days in advance to display the icon defined in `icon_soon` **Default**: 1
| `icon_soon` | Yes | Icon if the anniversary is 'soon' **Default**: `mdi:calendar`

## State and Attributes

### State

* The number of days remaining to the next occurance. (or days since last occurence if you have chosen the count up option)

### Attributes

* years at next anniversary: number of years that will have passed at the next occurrence _(NOT displayed if year is unknown)_
* current years: number of years have passed since the first occurance (ie, current age)  _(NOT displayed if year is unknown)_
* date:  The date of the first occurence _(or the date of the next occurence if year is unknown)_
* weeks_remaining: The number of weeks until the anniversary
* unit_of_measurement: 'Days' By default, this is displayed after the state. _this is NOT translate-able.  See below for work-around_
* half_anniversary_date: The date of the next half anniversary (if enabled by `show_half_anniversary`)
* days_until_half_anniversary: The number of days until the next half anniversary

### Notes about unit of measurement

Unit_of_measurement is *not* translate-able.
You can, however, change the text for unit of measurement in the configuration.  NB the sensor will always report in days, this just allows you to represent this in your own language.

[patreon-shield]: https://c5.patreon.com/external/logo/become_a_patron_button.png
[patreon]: https://www.patreon.com/pinkywafer
