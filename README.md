# hass-logi-circle

This is a staging area for future enhancements to the Logi Circle integration in Home Assistant.

If you're looking for official support, this repo is not required. Please refer to this link for more information: https://www.home-assistant.io/components/logi_circle/

---

This adds support for showing the last activity video when opening up the camera's live view from Home Assistant. It also resolves an issue with the sensor platform on 0.81+. It requires Home Assistant 0.79 or later.

Activity videos are converted from their original MP4 format into MJPEG stream. A side effect of this conversion is that videos do not play back at the correct speed.

To use, download the ZIP and extract into the `custom_components` folder. The folder tree should look like:

- `custom_components` [folder]
  - `camera` [folder]
    - `logi_circle.py` [file]
  - `sensor` [folder]
    - `logi_circle.py` [file]