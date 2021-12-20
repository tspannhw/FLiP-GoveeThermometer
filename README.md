# FLiP-GoveeThermometer

## Let's monitor a simple $15 temperature sensor 

### Govee Hygrometer Thermometer, Wireless Thermometer, Mini Bluetooth Humidity Sensor
### 262 Feet Connecting Range

So this sensor output signs on BLE for use with your phone.   Fortunately I found a library to grab that and send it to MQTT.
In my case I am using Apache Pulsar 2.8.1 to receive BLE (Bluetooth Low Energy) messages.

### Configure the Receiver

You need to download and install the deepcoder C app as well as the paho.mqtt.c library.

Then you need to find your BLE sensor.  I recommend putting it close to your device.   I am reading from my NVIDIA Xavier NX.

### ble_sensor_mqtt_pub.csv - Configure this file with your Pulsar Server, topic and the information on the sensor(s)

```
tcp://pulsar1:1883
persistent://public/default/ble-temp
mac address, type, location
E0:17:54:C1:D8:4C, 6, H5074 Govee Office
```

### Run the Sensor
````

/opt/demo/bluetooth-temperature-sensors/ble_sensor_mqtt_pub 0 1 100 500
````

### Reference

* https://github.com/deepcoder/bluetooth-temperature-sensors
* https://smile.amazon.com/gp/product/B07R586J37
