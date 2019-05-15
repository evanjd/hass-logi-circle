# hass-logi-circle

This branch hosts the private API based version of the Logi Circle integration, compatible with the latest Home Assistant release (0.92 at time of writing).

This is intended for users who are stuck without an API key. If you have an API key, please use the [official integration](https://www.home-assistant.io/components/logi_circle/).

---

To use, download the ZIP and extract into the `custom_components` folder. The folder tree should look like:

- `custom_components` [folder]
  - `logi_circle_legacy` [folder]
    - `manifest.json`
    - `__init.py__`
    - `camera.py`
    - `sensor.py`

Add the following to your `configuration.yaml`:

```yaml
logi_circle_legacy:
    username: YOUR_USERNAME_HERE
    password: YOUR_PASSWORD_HERE

camera:
  - platform: logi_circle_legacy

sensor:
  - platform: logi_circle_legacy
```