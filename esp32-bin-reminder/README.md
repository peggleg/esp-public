# ESP32 Bin Reminder

This project displays the next general waste and recycling collection dates on an ST7789V display, fetching the information from Home Assistant.

## Features

*   **Bin Collection Reminders:** Displays upcoming general waste and recycling collection dates.
*   **Home Assistant Integration:** Retrieves collection data from Home Assistant sensors (`sensor.general_waste` and `sensor.mixed_recycling`).
*   **ST7789V Display:** Utilizes an ST7789V TFT display (240x240) to show information.
*   **Custom Fonts and Images:** Uses a custom font (NotoSans-Regular.ttf) and bin-specific images (general-waste.png, recycling.png).
*   **WiFi Connectivity:** Connects to your local WiFi network.
*   **OTA Updates:** Supports Over-The-Air firmware updates.

## Configuration

Before compiling and uploading, you need to configure the `bin-reminder.yaml` file and ensure you have the necessary secrets and assets.

### Secrets

Create a `secrets.yaml` file in your ESPHome configuration directory with the following entries:

```yaml
iot_wifi_ssid: "YOUR_WIFI_SSID"
iot_wifi_password: "YOUR_WIFI_PASSWORD"
```

### Assets

Ensure the following files are present in the specified paths relative to your `bin-reminder.yaml`:

*   `fonts/NotoSans-Regular.ttf`: A TrueType font file.
*   `images/general-waste.png`: An 80x80 RGB565 image for general waste.
*   `images/recycling.png`: An 80x80 RGB565 image for recycling.

### ESPHome Dashboard

Add this configuration to your ESPHome dashboard. The device name will be `bin-reminder` and its friendly name will be `Bin Reminder`.

### Hardware

This configuration is designed for an `esp32-c6-devkitm-1` board with the following display pin connections:

*   **SPI Clock Pin (CLK):** GPIO7
*   **SPI MOSI Pin (MOSI):** GPIO16
*   **Display Chip Select Pin (CS):** GPIO14
*   **Display Data/Command Pin (DC):** GPIO19
*   **Display Reset Pin (RESET):** GPIO20
*   **Display Backlight Pin (Backlight):** GPIO18

## Home Assistant Sensors

Ensure you have two Home Assistant `text_sensor` entities providing the collection dates. The `entity_id`s expected by this configuration are:

*   `sensor.general_waste`
*   `sensor.mixed_recycling`

These sensors should output states like "Today", "Tomorrow", "in X days", or a date string in "YYYY-MM-DD" format.

Using the following HACS intergation:
https://github.com/mampfes/hacs_waste_collection_schedule

## Display Logic

The display updates every 360 minutes (6 hours) or when a new value is received from the Home Assistant bin collection sensors. It shows:

*   "Time not synced!" if the time is not synchronized with Home Assistant.
*   The next bin collection type (General Waste or Recycling) and the number of days until collection (Today!, Tomorrow!, In X days).
*   An appropriate bin image.
*   If no collection is scheduled within the next 7 days, it displays "No Collection" and "Next 7 Days".

## Build and Upload

Use the ESPHome dashboard or command-line tools to compile and upload the firmware to your ESP32 device.
