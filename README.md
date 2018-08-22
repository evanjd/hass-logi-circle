# hass-logi-circle

This is a temporary staging area for the Logi Circle home assistant component, modified to work within the `custom_components` folder. All real development will occur on the `home-assistant` repo, and this repo will be closed once it's been validated that everything's working.

To use, download the ZIP and extract into the `custom_components` folder. The folder tree should look like:

- custom_components
  - `logi.py` [file]
  - `logi_camera` [folder]
    - bunch of files
  - `camera` [folder]
    - `logi.py` [file]
  - `sensor` [folder]
    - `logi.py` [file]
   

Then in your configuration.yaml, add the following:

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

The full list of supported conditions is: `battery_level`, `last_activity_time`, `speaker_volume`, `microphone_gain`, `privacy_mode`, `signal_strength_category`, `signal_strength_percentage`, `is_streaming`, `temperature`, `humidity`

Lastly, the camera entity supports the `turn_on` and `turn_off` service. Running it should disable streaming on the target entity (meaning no live stream and no activity recordings).
