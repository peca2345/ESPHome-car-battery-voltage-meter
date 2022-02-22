# ESPHome - car battery meter


## Description

- MCU: ESP8266
- Input voltage: 10 - 15V DC
- Power consumption: 20 mA (in deep sleep 20 uA)


## Schema

![enter image description here](https://photos.app.goo.gl/LGtXwSTnXPz9NPTj8)

## Code

    esphome:
      name: car-battery-voltage
    esp8266:
      board: esp01_1m
    captive_portal:
    logger:
    api:
    ota:
      password: "a0585d60510e89da5ace2456882134ae"
    
    wifi:
      ssid: !secret wifi_ssid
      password: !secret wifi_password
    
    
    sensor:
      - platform: adc
        pin: A0
        name: "car_battery_voltage"
        id: adc_voltage
        update_interval: 60s
        accuracy_decimals: 1
        filters:
          - multiply: 15.25 
          - median:
              window_size: 10
              send_every: 5
              send_first_at: 1
         
    deep_sleep:
      run_duration: 60s 
      sleep_duration: 60min
      id: battery_deep_sleep


