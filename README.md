# Sensor_Josuino

Welcome at the new Josuino sensor. Josuino is an Arduino based IoT device, which makes it possible to alter the firmware in the device using the familiar Arduino environment. @WOTS, Josuino prototypes with ID 67, 68 and 69 are active. Please feel free to explore other sensors currently online, they are installed in different locations in the Netherlands and other parts of Europe. 

These are the Rest API commands to retrieve data from any Jose/Josuino sensor currently online. In the examples below sensor 67 is used, of course this can be any number. For more information and examples, please see http://data.smartemission.nl

# 1. Get the list of available devices
GET http://whale.citygis.nl/sensors/v1/devices

{ "devices":  ["/sensors/v1/devices/67", "/sensors/v1/devices/68"] }


# 2. Get metadata for device 67
GET http://whale.citygis.nl/sensors/v1/devices/67

{
  "id": 67,
  "name": "device name", // indien mogelijk ook "owner" en "contact"
  "timeseries": "/sensors/v1/devices/67/timeseries",
  "last" : "/sensors/v1/devices/67/last",
  "outputs": [
    { "name": "s_no2", "uom": "ppb", "description": "..." },
    ...
  ]
}

# 3. Get the available days of timeseries data for device 67
GET http://whale.citygis.nl/sensors/v1/devices/67/timeseries

{
    "id": 67,
    "days": [
        "/sensors/v1/devices/67/timeseries/20151222"
        "/sensors/v1/devices/67/timeseries/20151223"
        ...
    ]
}


# 4. Get the available hours on a specific day for device 67
GET http://whale.citygis.nl/sensors/v1/devices/67/timeseries/20151222

{ "id": 67, "date": "2015/12/22", "hours": [1,2,3,4,5,6,7] }

Notes
- The date should include zero padding, so 1 januari 2016 should be encoded as 20160101 (yyyymmdd)
- The hour numbers range from 1 to 24; 1 means from 0:00:00 until 0:59:59


# 5. Get all sensor data on dec 22nd 2015 during 18:00-19:00 for device 67
GET http://whale.citygis.nl/sensors/v1/devices/67/timeseries/20151222/19

{
  "id": 67,
  "date": "2015/12/22",
  "hour": 19,
  "timeseries":
  [
    {"time": "2015/12/22 18:34:56Z", "s_no2": 234.5, "s_co2": 123.4, ... },
    ...
  ]
}

Notes
- The date should include zero padding, so 1 januari 2016 should be encoded as 20160101
- The hour number ranges from 1 to 24; 1 means from 0:00:00 until 0:59:59


# 6. Get the last sensor values for device 67
GET http://whale.citygis.nl/sensors/v1/devices/67/last

{ "id": 67, "time": "2015/12/22 18:34:56Z", "s_no2": 234.5, "s_co2": 123.4, ... }
