# home-assistant-blueprints

Blueprints for Home Assistant.

## Philips Hue Dimmer V2 (Z2M)

[`hue_dimmer_v2.yaml`](./hue_dimmer_v2.yaml) — control lights and scenes with a
Philips Hue Dimmer Switch (V2 / RWL022) paired through Zigbee2MQTT.

### Button mapping

| Button   | Short press                 | Hold                                  |
|----------|-----------------------------|---------------------------------------|
| **ON**   | Toggle the light(s)         | Activate a scene (e.g. reset to 100%) |
| **UP**   | Brightness up by one step   | Ramp brightness up until released     |
| **DOWN** | Brightness down by one step | Ramp brightness down until released   |
| **HUE**  | Activate scene (single)     | Activate scene (hold)                 |
| **HUE**  | Activate scene (double)     | —                                     |

The brightness step (used for both single press and each ramp step) is
configurable. Every scene slot is optional — leave one empty to make that
gesture do nothing.

### Prerequisite: a Text helper for double-press

The dimmer does **not** report double-presses natively (Zigbee2MQTT only exposes
`press` / `hold` / `*_release` per button), so the blueprint detects a double
press of the HUE button by timing. Because the automation runs in `restart`
mode (so releasing a held UP/DOWN button cancels the ramp), the press has to be
remembered in a helper entity that survives the restart.

Before importing, create one dedicated **Text** helper:

1. **Settings → Devices & Services → Helpers → Create Helper → Text**
2. Name it something like `Hue Dimmer — Last Press`
3. Select it in the blueprint's **Double-press detection** section

Use a separate Text helper per dimmer if you set up more than one.

### Import

In Home Assistant: **Settings → Automations & Scenes → Blueprints → Import
Blueprint**, then paste this file's URL:

```
https://github.com/ktbgroup-self-hosted/home-assistant-blueprints/blob/main/hue_dimmer_v2.yaml
```
