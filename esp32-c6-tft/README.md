# ESP32-C6 Screen Test

A simple ESPHome project for testing an ST7789V display with an ESP32-C6 development board.

## Hardware Requirements

- **ESP32-C6 Super Mini** board
- **ST7789V display** (240x240 pixels)
- **TrueType font file** (`fonts/arial.ttf`)

## Pin Configuration

| Function | GPIO Pin | Description |
|----------|----------|-------------|
| SPI CLK | GPIO7 | SPI Clock (SCL/SCLK) |
| SPI MOSI | GPIO16 | SPI Data (SDA/MOSI) |
| Display CS | GPIO14 | Chip Select |
| Display DC | GPIO19 | Data/Command |
| Display Reset | GPIO20 | Reset |
| Display Backlight | GPIO18 | Backlight Control |

## Features

### Display
- **ST7789V** 240x240 pixel TFT display
- Custom configuration for generic ST7789 displays
- 5-second update interval
- Real-time system information display

### Sensors & Monitoring
- **WiFi Signal Strength** - Updates every 60 seconds
- **System Uptime** - Formatted display (minutes/hours)
- **Internal Temperature** - ESP32-C6 internal temperature sensor
- **Device Information** - MAC address, reset reason, device info

### Display Information
The screen shows:
- System uptime (orange text)
- Internal temperature in Celsius (red text)
- WiFi signal strength in dBm (cyan text)
- System status (yellow text)

## Setup Instructions

1. **Prepare the font file**: Place `arial.ttf` in a `fonts/` directory in your ESPHome project folder.

2. **Configure secrets**: Create a `secrets.yaml` file with your WiFi credentials:
   ```yaml
   wifi_ssid: "Your_WiFi_SSID"
   wifi_password: "Your_WiFi_Password"
   ```

3. **Update API encryption key**: Replace the `xxx` placeholder in the API encryption key with your actual key.

4. **Update OTA password**: Replace the `xxx` placeholder in the OTA password with your actual password.

5. **Flash the device**: Use ESPHome to compile and flash the configuration to your ESP32-C6.

## Configuration Details

### Framework
- Uses **ESP-IDF** framework for ESP32-C6 compatibility
- Logging level set to INFO

### Display Configuration
- **Model**: Custom ST7789V configuration
- **Resolution**: 240x240 pixels
- **Rotation**: 0 degrees (portrait)
- **Colors**: Supports full color range with custom text colors
- **Update Rate**: 5 seconds

### Connectivity
- **WiFi**: Configured via secrets file
- **API**: Encrypted communication enabled
- **OTA**: Over-the-air updates supported

## Remote Control
- **Restart Switch**: Remotely restart the device via Home Assistant or ESPHome dashboard

## Troubleshooting

### Display Not Working
- Verify all pin connections match the configuration
- Ensure the display is compatible with ST7789V driver
- Check power supply to the display

### WiFi Connection Issues
- Verify WiFi credentials in `secrets.yaml`
- Check WiFi signal strength in the area
- Ensure 2.4GHz WiFi network compatibility

### Font Issues
- Ensure `arial.ttf` is in the correct `fonts/` directory
- Verify the font file is not corrupted
- Check that required glyphs are included in the font configuration

## License

This project is open source. Modify and distribute as needed for your projects.
