---
layout: page
title: "Forecast.io"
description: "How to integrate Forecast.io within Home Assistant."
date: 2015-04-25 9:06
sidebar: true
comments: false
sharing: true
footer: true
logo: forecast.png
ha_category: Deprecated
featured: False
ha_release: pre 0.7
---

<p class='note warning'>
**This platform has been deprecated in favor of the "[darksky](/components/sensor.darksky/)" platform and will be removed in the future. Please use the "darksky" platform.**
</p>

The `forecast` platform uses the [Forecast.io](https://forecast.io/) web service as a source of meteorological data for your location. The location is based on the `longitude` and `latitude` coordinates configured in your `configuration.yaml` file. The coordinates are auto-detected but to take advantage of the hyper-local weather reported by forecast.io, you can refine them down to your exact home address. GPS coordinates can be found by using [Google Maps](https://www.google.com/maps) and clicking on your home or [Openstreetmap](http://www.openstreetmap.org/).

You need an API key which is free but requires [registration](https://developer.forecast.io/register). You can make up to 1000 calls per day for free which means that you could make one approximately every 86 seconds.

<p class='note warning'>
[Forecast.io](https://forecast.io/) will charge you $0.0001 per API call if you enter your credit card details and create more than 1000 calls per day.
</p>

To add Forecast.io to your installation, add the following to your `configuration.yaml` file:

```yaml
# Example configuration.yaml entry
sensor:
  - platform: forecast
    api_key: YOUR_APP_KEY
    monitored_conditions:
      - summary
      - icon
      - nearest_storm_distance
      - nearest_storm_bearing
      - precip_type
      - precip_intensity
      - precip_probability
      - temperature
      - apparent_temperature
      - dew_point
      - wind_speed
      - wind_bearing
      - cloud_cover
      - humidity
      - pressure
      - visibility
      - ozone
      - minutely_summary
      - hourly_summary
      - daily_summary
      - temperature_max
      - temperature_min
      - apparent_temperature_max
      - apparent_temperature_min
      - precip_intensity_max
```

Configuration variables:

- **api_key** (*Required*): Your API key for http://forecast.io/.
- **monitored_conditions** array (*Required*): Conditions to display in the frontend.
  - **summary**: A human-readable text summary of the current conditions.
  - **precip_type**: The type of precipitation occurring.
  - **precip_intensity**: The average expected intensity of precipitation occurring.
  - **precip_probability**: A value between 0 and 1 which is representing the probability of precipitation.
  - **temperature**: The current temperature.
  - **apparent_temperature**: A numerical value representing the apparent (or "feels like") temperature.
  - **dew_point**: The dew point.
  - **wind_speed**: The wind speed.
  - **wind_bearing**: Where the wind is coming from in degrees, with true north at 0° and progressing clockwise.
  - **cloud_cover**: The percentage of sky occluded by clouds.
  - **humidity**: The relative humidity.
  - **pressure**: The sea-level air pressure in millibars.
  - **visibility**: The average visibility.
  - **ozone**: The columnar density of total atmospheric ozone in Dobson.
  - **minutely_summary**: A human-readable text summary for the next hour.
  - **hourly_summary**: A human-readable text summary for the next 24 hours.
  - **daily_summary**: A human-readable text summary for the next 7 days.
  - **temperature_max**: Today's expected high temperature.
  - **temperature_min**: Today's expected low temperature.
  - **apparent_temperature_max**: Today's expected apparent high temperature.
  - **apparent_temperature_min**: Today's expected apparent low temperature.
  - **precip_intensity_max**: Today's expected maximum intensity of precipitation.
- **units** (*Optional*): Specify the unit system. Default to `si` or `us` based on the temperature preference in Home Assistant. Other options are `auto`, `us`, `si`, `ca`, and `uk2`.
`auto` will let forecast.io decide the unit system based on location.
- **update_inverval** (*Optional*): Minimum time interval between updates. Default is 2 minutes. Supported formats:
  - `update_interval: 'HH:MM:SS'`
  - `update_interval: 'HH:MM'`
  - Time period dictionary, e.g.:
 <pre>update_interval:
        # At least one of these must be specified:
        days: 0
        hours: 0
        minutes: 3
        seconds: 30
        milliseconds: 0
    </pre>

Details about the API are available in the [Forecast.io documentation](https://developer.forecast.io/docs/v2).
