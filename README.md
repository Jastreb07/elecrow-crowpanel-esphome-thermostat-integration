# Smart Thermostat Knob — Home Assistant Integration

[![Open your Home Assistant instance and open a repository inside the Home Assistant Community Store.](https://my.home-assistant.io/badges/hacs_repository.svg)](https://my.home-assistant.io/redirect/hacs_repository/?owner=Jastreb07&repository=elecrow-crowpanel-esphome-thermostat-integration&category=integration)

This is the companion Home Assistant integration for the
[Smart Thermostat Knob firmware](https://github.com/Jastreb07/elecrow-crowpanel-esphome-thermostat)
(ESPHome firmware for Elecrow CrowPanel ESP32-S3 rotary displays). It is a
configuration helper only — it does not add new entities to Home Assistant
and does not talk to the ESP device over the network. It creates one
configuration sensor per physical Smart Knob and exposes the climate, light,
and cover entities you pick for it, in the JSON attribute format the
firmware reads.

If you don't have the firmware installed on a device yet, start there —
this integration has nothing to configure without it:
**[Smart Thermostat Knob firmware repository](https://github.com/Jastreb07/elecrow-crowpanel-esphome-thermostat)**.

## Video Walkthrough

| 1.28" (240x240) | 2.1" (480x480) |
|---|---|
| [![240x240 demo](https://img.youtube.com/vi/F0mFrxt4jac/0.jpg)](https://www.youtube.com/watch?v=F0mFrxt4jac) | [![480x480 demo](https://img.youtube.com/vi/REPLACE_WITH_480_VIDEO_ID/0.jpg)](https://www.youtube.com/watch?v=REPLACE_WITH_480_VIDEO_ID) |

GitHub strips `<iframe>` embeds from rendered READMEs, so a YouTube video
can't play inline here — clicking a thumbnail opens it on YouTube instead.
Once we have local `.mp4` exports of these recordings, we can switch to a
native `<video>` tag pointing at a file committed to this repo, which
GitHub *does* play inline without leaving the page.

## Screens

The knob's on-device screens, controlled by this integration's entity
selection:

| Loading | Home | Thermostat |
|---|---|---|
| ![Loading screen](images/screen_loading.png) | ![Home screen](images/screen_home.png) | ![Thermostat screen](images/screen_thermostat.png) |

| Light brightness | Light temperature | Light color |
|---|---|---|
| ![Light brightness screen](images/screen_light_brightness.png) | ![Light temperature screen](images/screen_light_temperature.png) | ![Light color screen](images/screen_light_color.png) |

| Cover | Entity navigation |
|---|---|
| ![Cover screen](images/screen_cover.png) | ![Navigation screen](images/screen_navigation.png) |

## Hardware

| CrowPanel 1.28" (240x240) | CrowPanel 2.1" (480x480) |
|---|---|
| [![Elecrow CrowPanel 1.28" 240x240 rotary display](images/Elecrow-CrowPanel-240x240.png)](https://www.elecrow.com/crowpanel-1-28inch-hmi-esp32-rotary-display-240-240-ips-round-touch-knob-screen.html) | [![Elecrow CrowPanel 2.1" 480x480 rotary display](images/Elecrow-CrowPanel-480x480.png)](https://www.elecrow.com/crowpanel-2-1inch-hmi-esp32-rotary-display-480-480-ips-round-touch-knob-screen.html) |

## Installation via HACS

1. Click the badge above, or in Home Assistant open **HACS > Integrations >
   the three-dot menu (top right) > Custom repositories**, add
   `https://github.com/Jastreb07/elecrow-crowpanel-esphome-thermostat-integration`
   as category **Integration**.
2. Search for **Smart Thermostat Knob** in HACS and install it.
3. Restart Home Assistant.
4. Continue with **Settings > Devices & services > Add integration** below.

## Manual installation

Copy this repository's contents to the Home Assistant configuration
directory as:

```text
/homeassistant/custom_components/smart_thermostat_knob
```

Restart Home Assistant. Then open **Settings > Devices & services > Add
integration**, search for **Smart Thermostat Knob**, give the knob a
recognizable name, and select its climate, light, and cover entities.
Repeat **Add integration** for every additional Smart Knob.

![Home Assistant entity picker used by the Smart Thermostat Knob integration](images/ha-integration-helper.png)

Optionally select the knob's ESPHome text entity **Home Assistant Config
Entity**. The integration writes its own configuration sensor entity ID to
that text entity and automatically finds the restart button on the same
ESPHome device. The ESP restarts once after initial mapping and after every
later reconfiguration of this helper.

To rename a knob or change its assigned entities later, open that specific
integration entry and select **Reconfigure**. Other Smart Knob entries are
not affected.

At least one climate entity is required. Light and cover entities are
optional. The screen order follows the selector order, and display names
come from the Home Assistant friendly names. To change a displayed name,
rename the entity and reload this integration.

Each entry creates its own sensor, with an entity ID derived from the
chosen name, for example `sensor.living_room_knob_config`. If that ID is
already used, Home Assistant adds a suffix. Set the corresponding ESPHome
text entity **Home Assistant Config Entity** to that knob's actual sensor
entity ID. The value is persisted by the ESP.

## Related

- [Smart Thermostat Knob firmware](https://github.com/Jastreb07/elecrow-crowpanel-esphome-thermostat) —
  the ESPHome firmware this integration configures. See its
  [SETUP.md](https://github.com/Jastreb07/elecrow-crowpanel-esphome-thermostat/blob/master/SETUP.md#home-assistant-setup)
  for the full Home Assistant setup flow, including the manual
  Template-Entity alternative to this integration.
