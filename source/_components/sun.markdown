---
layout: page
title: "Sun"
description: "Instructions how to track the sun within Home Assistant."
date: 2015-01-24 14:39
sidebar: true
comments: false
sharing: true
footer: true
logo: home-assistant.png
ha_category: Weather
---

The sun component will use your current location to track if the sun is above or below the horizon.The sun can be used within automation as [a trigger with an optional offset to simulate dawn/dusk][automation-trigger].

[automation-trigger]: /getting-started/automation-trigger/#sun-trigger

```yaml
# Example configuration.yaml entry
homeassistant:
  latitude: 32.87336
  longitude: -117.22743

sun:
  elevation: 102
```

Configuration variables:

- **elevation** (*Optional*): The (physical) elevation of your location, in metres above sea level. If ommitted will be retrieved from Google Maps.

<p class='img'>
<img src='/images/screenshots/more-info-dialog-sun.png' />
</p>

### {% linkable_title Implementation Details %}

The suns event listener will call the service when the sun rises or sets with an offset.

The sun event need to have the type 'sun', which service to call, which event (sunset or sunrise) and the offset.

```json
{
    "type": "sun",
    "service": "switch.turn_on",
    "event": "sunset",
    "offset": "-01:00:00"
}
```

#### {% linkable_title Maintains entity `sun.sun` %}

| Possible state | Description |
| --------- | ----------- |
| `above_horizon` | When the sun is above the horizon.
| `below_horizon` | When the sun is below the horizon.



| State Attributes | Description |
| --------- | ----------- |
| `next_rising` | Date and time of the next sun rising (in UTC).
| `next_setting` | Date and time of the next sun setting (in UTC).
| `elevation` |  Solar elevation. This is the angle between the sun and the horizon. Negative values mean the sun is below the horizon.
