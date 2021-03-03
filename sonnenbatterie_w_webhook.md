Webhook

The following action creates the webhook and sets the received value to two input_number helpers:
```yaml
alias: Sonnen Webhook get power meter
description: ''
trigger:
  - platform: webhook
    webhook_id: sonnen_power_meter
condition: []
action:
  - service: input_number.set_value
    data:
      entity_id: input_number.webhook_consumption
      value: '{{ trigger.json[1][''kwh_imported''] }}'
  - service: input_number.set_value
    data:
      entity_id: input_number.webhook_production
      value: '{{ trigger.json[0][''kwh_imported''] }}'
mode: single
```

The input_number can be used with utility_meter like this:
```yaml
utility_meter:
  daily_energy_consumption_from_webhook:
    source: input_number.webhook_consumption
    cycle: daily
```
And finally add the webhook in sonnen-Dashboard:
![image](https://user-images.githubusercontent.com/117189/109875203-6fdf0400-7c70-11eb-9c02-90b52b4ca8fc.png)
