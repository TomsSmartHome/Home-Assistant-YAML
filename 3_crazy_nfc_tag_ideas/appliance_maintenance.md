# Appliance maintenance

Change / Add for your appliances as needed.

Add an input datetime for each appliance

Then add this sensor to measure number of days since that appliance was last updated:

```jinja
{{ ( now().strftime('%Y-%m-%d') | as_datetime - states('input_datetime.last_dishwasher_maintenance') | as_datetime ).days }}
```

Automations
```yaml
alias: Reset dishwasher maintenance
description: ""
triggers:
  - trigger: tag
    tag_id: Dishwasher_maintenance
conditions: []
actions:
  - action: input_datetime.set_datetime
    metadata: {}
    data:
      date: "{{ now().strftime('%Y-%m-%d') }}"
    target:
      entity_id: input_datetime.last_dishwasher_maintenance
mode: single
```

Notify when it's been too long since last maintenance:

```yaml
alias: Notify when dishwasher filter needs cleaning
description: ""
triggers:
  - trigger: numeric_state
    entity_id:
      - sensor.number_of_days_since_last_dishwasher_maintenance
    above: 90
conditions: []
actions:
  - action: persistent_notification.create
    metadata: {}
    data:
      title: Dishwasher filter needs cleaning!
      message: DO IT NOW!!
mode: single
```
