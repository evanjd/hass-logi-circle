# hass-logi-circle

This is a temporary staging area for the Logi Circle home assistant component, modified to work within the `custom_components` folder. All real development will occur on the `home-assistant` repo, and this repo will be closed once it's been validated that everything's working.

To use, download the ZIP and extract into the `custom_components` folder. The folder tree should look like:

- `custom_components` [folder]
  - `logi.py` [file]
  - `camera` [folder]
    - `logi.py` [file]
  - `sensor` [folder]
    - `logi.py` [file]

## Configuration

In your configuration.yaml, add the following:

```
logi:
  username: your@email.com
  password: your_password

camera:
  - platform: logi

sensor:
  - platform: logi
```

You can optionally filter out monitoring conditions you're not interested from the logi sensor. For example, if you only wanted to show battery level, last activity and signal strength, you can configure the sensor as follows:

```
sensor:
 - platform: logi
   monitored_conditions:
     - battery_level
     - last_activity_time
     - signal_strength_category
```

The full list of supported conditions is: `battery_level`, `last_activity_time`, `privacy_mode`, `signal_strength_category`, `signal_strength_percentage`

## Services

The camera entities exposes a few services. Those are:

- `logi_set_mode`: Allows you to set the `led`, `privacy_mode` or `streaming_mode` statuses. LED and privacy mode expect a boolean (`true`/`false`), streaming mode expects a string (`'on'`, `'off'`, `'onAlert'`).

Example payloads:

```json
{
  "entity_id": "camera.living_room",
  "mode": "led",
  "value": true
}
```

```json
{
  "entity_id": "camera.living_room",
  "mode": "privacy_mode",
  "value": true
}
```

```json
{
  "entity_id": "camera.living_room",
  "mode": "streaming_mode",
  "value": "onAlert"
}
```

---

- `logi_livestream_snapshot`: Takes a JPEG snapshot from the livestream. Takes the same JSON payload as the native `snapshot` method, but should take the snapshot at the instant you request it, rather than using the cached image.

Example payload:

```json
{
  "entity_id": "camera.living_room",
  "filename": "/tmp/snapshot_{{ entity_id }}.jpg"
}
```

---

- `logi_download_livestream`: Downloads the livestream to an MP4 at the duration specified (in seconds).

Example payload:

```json
{
  "entity_id": "camera.living_room",
  "filename": "/tmp/stream_{{ entity_id }}.mp4",
  "duration": 30
}
```

---

Lastly, the camera entity supports the `turn_on` and `turn_off` service. `turn_off` should disable streaming on the target entity (meaning no live stream and no activity recordings), `turn_on` should activate streaming.
