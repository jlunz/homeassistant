For a new (2020) sonnenBatterie 10 system, software is at version 1.5.5

This uses the status endpoint
![image](https://user-images.githubusercontent.com/117189/109875033-30b0b300-7c70-11eb-9176-493a4249e9c7.png)



secrets.yaml
```yaml
sonnen_api_token: your-token-here
```

sensor:
```yaml
sensor:
  # Sonnenbatterie APIV2
  - platform: rest
    name: SonnenAPIV2
    scan_interval: 10
    resource: http://YOUR-IP-HERE:80/api/v2/status
    headers:
      Authorization: !secret sonnen_api_token
    json_attributes:
      - Apparent_output
      - BackupBuffer
      - BatteryCharging
      - BatteryDischarging
      - Consumption_W
      - Fac
      - FlowConsumptionBattery
      - FlowConsumptionGrid
      - FlowConsumptionProduction
      - FlowGridBattery
      - FlowProductionBattery
      - FlowProductionGrid
      - GridFeedIn_W
      - IsSystemInstalled
      - OperatingMode
      - Pac_total_W
      - Production_W
      - RSOC
      - Sac1
      - Sac2
      - Sac3
      - SystemStatus
      - Timestamp
      - USOC
      - Uac
      - Ubat
      - dischargeNotAllowed
      - generator_autostart
    value_template: '{{ value_json.sonnenapiv2 }}'
  - platform: template
    sensors:
      sonnenapiv2_apparent_output:
        friendly_name: 'Apparent_output'
        value_template: '{{ states.sensor.sonnenapiv2.attributes["Apparent_output"] }}'
      sonnenapiv2_backupbuffer:
        friendly_name: 'BackupBuffer'
        value_template: '{{ states.sensor.sonnenapiv2.attributes["BackupBuffer"] }}'
      sonnenapiv2_consumption_w:
        friendly_name: 'Consumption_W'
        value_template: '{{ states.sensor.sonnenapiv2.attributes["Consumption_W"] }}'
        unit_of_measurement: W
        device_class: power
      sonnenapiv2_fac:
        friendly_name: 'Fac'
        value_template: '{{ states.sensor.sonnenapiv2.attributes["Fac"] }}'
        unit_of_measurement: Hz
      sonnenapiv2_gridfeedin_w:
        friendly_name: 'GridFeedIn_W'
        value_template: '{{ states.sensor.sonnenapiv2.attributes["GridFeedIn_W"] }}'
        unit_of_measurement: W
        device_class: power
      sonnenapiv2_issysteminstalled:
        friendly_name: 'IsSystemInstalled'
        value_template: '{{ states.sensor.sonnenapiv2.attributes["IsSystemInstalled"] }}'
      sonnenapiv2_operatingmode:
        friendly_name: 'OperatingMode'
        value_template: '{{ states.sensor.sonnenapiv2.attributes["OperatingMode"] }}'
      sonnenapiv2_pac_total_w:
        friendly_name: 'Pac_total_W'
        value_template: '{{ states.sensor.sonnenapiv2.attributes["Pac_total_W"] }}'
        unit_of_measurement: W
        device_class: power
      sonnenapiv2_production_w:
        friendly_name: 'Production_W'
        value_template: '{{ states.sensor.sonnenapiv2.attributes["Production_W"] }}'
        unit_of_measurement: W
        device_class: power
      sonnenapiv2_rsoc:
        friendly_name: 'RSOC'
        value_template: '{{ states.sensor.sonnenapiv2.attributes["RSOC"] }}'
        unit_of_measurement: '%'
      sonnenapiv2_sac1:
        friendly_name: 'Sac1'
        value_template: '{{ states.sensor.sonnenapiv2.attributes["Sac1"] }}'
      sonnenapiv2_sac2:
        friendly_name: 'Sac2'
        value_template: '{{ states.sensor.sonnenapiv2.attributes["Sac2"] }}'
      sonnenapiv2_sac3:
        friendly_name: 'Sac3'
        value_template: '{{ states.sensor.sonnenapiv2.attributes["Sac3"] }}'
      sonnenapiv2_systemstatus:
        friendly_name: 'SystemStatus'
        value_template: '{{ states.sensor.sonnenapiv2.attributes["SystemStatus"] }}'
      sonnenapiv2_timestamp:
        friendly_name: 'Timestamp'
        value_template: '{{ states.sensor.sonnenapiv2.attributes["Timestamp"] }}'
      sonnenapiv2_usoc:
        friendly_name: 'USOC'
        value_template: '{{ states.sensor.sonnenapiv2.attributes["USOC"] }}'
        unit_of_measurement: '%'
      sonnenapiv2_uac:
        friendly_name: 'Uac'
        value_template: '{{ states.sensor.sonnenapiv2.attributes["Uac"] }}'
        unit_of_measurement: V
        device_class: voltage
      sonnenapiv2_ubat:
        friendly_name: 'Ubat'
        value_template: '{{ states.sensor.sonnenapiv2.attributes["Ubat"] }}'
        unit_of_measurement: V
        device_class: voltage

binary_sensor:
  - platform: template
    sensors:
      sonnenapiv2_flowconsumptionbattery:
        friendly_name: 'FlowConsumptionBattery'
        value_template: '{{ states.sensor.sonnenapiv2.attributes["FlowConsumptionBattery"] }}'
      sonnenapiv2_flowconsumptiongrid:
        friendly_name: 'FlowConsumptionGrid'
        value_template: '{{ states.sensor.sonnenapiv2.attributes["FlowConsumptionGrid"] }}'
      sonnenapiv2_flowconsumptionproduction:
        friendly_name: 'FlowConsumptionProduction'
        value_template: '{{ states.sensor.sonnenapiv2.attributes["FlowConsumptionProduction"] }}'
      sonnenapiv2_flowgridbattery:
        friendly_name: 'FlowGridBattery'
        value_template: '{{ states.sensor.sonnenapiv2.attributes["FlowGridBattery"] }}'
      sonnenapiv2_flowproductionbattery:
        friendly_name: 'FlowProductionBattery'
        value_template: '{{ states.sensor.sonnenapiv2.attributes["FlowProductionBattery"] }}'
      sonnenapiv2_flowproductiongrid:
        friendly_name: 'FlowProductionGrid'
        value_template: '{{ states.sensor.sonnenapiv2.attributes["FlowProductionGrid"] }}'
      sonnenapiv2_batterycharging:
        friendly_name: 'BatteryCharging'
        value_template: '{{ states.sensor.sonnenapiv2.attributes["BatteryCharging"] }}'
      sonnenapiv2_batterydischarging:
        friendly_name: 'BatteryDischarging'
        value_template: '{{ states.sensor.sonnenapiv2.attributes["BatteryDischarging"] }}'
      sonnenapiv2_dischargenotallowed:
        friendly_name: 'dischargeNotAllowed'
        value_template: '{{ states.sensor.sonnenapiv2.attributes["dischargeNotAllowed"] }}'
      sonnenapiv2_generator_autostart:
        friendly_name: 'generator_autostart'
        value_template: '{{ states.sensor.sonnenapiv2.attributes["generator_autostart"] }}'

```
