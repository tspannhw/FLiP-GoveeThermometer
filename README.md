# FLiP-GoveeThermometer

## Let's monitor a simple $15 temperature sensor 

### Govee Hygrometer Thermometer, Wireless Thermometer, Mini Bluetooth Humidity Sensor
### 262 Feet Connecting Range

So this sensor output signs on BLE for use with your phone.   Fortunately I found a library to grab that and send it to MQTT.
In my case I am using Apache Pulsar 2.8.1 to receive BLE (Bluetooth Low Energy) messages.

### Configure the Receiver

You need to download and install the deepcoder C app as well as the paho.mqtt.c library.

Then you need to find your BLE sensor.  I recommend putting it close to your device.   I am reading from my NVIDIA Xavier NX.

````
6 = Govee H5074
E0:17:54:C1:D8:4C Govee_H5074_D84C
````


### ble_sensor_mqtt_pub.csv - Configure this file with your Pulsar Server, topic and the information on the sensor(s)

```

tcp://pulsar1:1883
persistent://public/default/ble-temp
mac address, type, location
E0:17:54:C1:D8:4C, 6, H5074 Govee Office

```

### Run

````
root@nvidia-desktop:/home/nvidia/nvme/bluetooth-temperature-sensors# ./runble.sh 
Mon Dec 20 19:50:36 EST 2021
ble_sensor_mqtt_pub v 2.13
1 Bluetooth adapter(s) in system.
Reading configuration file : ble_sensor_mqtt_pub.csv
MQTT server : tcp://pulsar1:1883
MQTT topic  : persistent://public/default/ble-temp
Header      |MAC Address      |Type|Location                      |
Unit  :   0 |E0:17:54:C1:D8:4C|   6|H5074 Govee Office            |
Total devices in configuration file : 1
MQTT client name : ble_sensor_mqtt_pub-A4:B4:15:55:66:70
Bluetooth Adapter : 0 has MAC address : A4:B4:15:55:66:70
Advertising scan type (0=passive, 1=active): 1
Advertising scan window   :  100, 62.5 ms
Advertising scan interval :  500, 312.5 ms
Scanning....
current hour (GMT) = 0
last    hour (GMT) = 23
*********** =========
HOUR ROLLOVER
current hour (GMT) = 1
last    hour (GMT) = 0
Location : E0:17:54:C1:D8:4C packets received in last hour : 6 H5074 Govee Office
payload_buffer JSON : {"timestamp":"20211221010010","E0:17:54:C1:D8:4C":{"count":6, "location":"H5074 Govee Office"},"total_adv_packets":6}

````

### Run the Sensor
````
/home/nvidia/nvme/bluetooth-temperature-sensors/ble_sensor_mqtt_pub 0 1 100 500
````

### Reference

* https://github.com/deepcoder/bluetooth-temperature-sensors
* https://smile.amazon.com/gp/product/B07R586J37
