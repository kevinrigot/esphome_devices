# esphome_devices
Devices of ESP_HOME
- [Room humidity sensor](./humidity-sensor.md): Record the room temperature and humidity every hour

## Secrets
In ESPHOME configure the followin secrets
- wifi_ssid: "YOUR WIFI SSID"
- wifi_password: "YOUR WIFI PASSWORD"
- hass_api_password: "Home assistant API PASSWORD"
- mqtt_url: "MQTT broker ip address"
- mqtt_user: "MQTT broker user"
- mqtt_password: "MQTT broker password"

## MQTT client
MQTT explorer - http://mqtt-explorer.com/

## Over the air upload and deep sleep
Publish a message ${device_name}/ota_mode with raw value "ON" and with mqtt retain flag. This will prevent the device to go in deep sleep next time it wakes up. You can wait the device wakes up, or just press the button reset.

Once the upload is finished and code change is OK, republish a message ${device_name}/ota_mode with raw value "OFF" and with mqtt retain flag. Then publish another message ${device_name}/sleep_mode with raw value "ON" and without mqtt retain flag.

## ESP tips
### Wemos D1 mini vs NodeMcu
- The Wemos D1 mini consumes almost nothing while in deep sleep (0,15ma) while the NodeMcu still consumes 9ma.
- The Wemos D1 mini has a good LDO Voltage regulator builtin (ME6211 - dropout 260mV). So you can connect a 18650 3,7-4,2V on the 5V pin.
The NodeMcu has an AMS1117 which has a drop out voltage of 0,7V at 200mA. It means the 18650 wont be able to operate when the battery is at 50% (more or less).
You can add another LDO like MCP1700 and connect it to the 3.3V.