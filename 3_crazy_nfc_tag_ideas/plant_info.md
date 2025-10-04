# Get plant info

Example automation:

```yaml
alias: Get geranium info
description: ""
triggers:
  - trigger: tag
    tag_id: Geranium
conditions: []
actions:
  - action: persistent_notification.create
    metadata: {}
    data:
      message: >-
        Water 💧 Once a week, check if top 1-2 inches are dry.<br>Sun ☀️ At
        least 6 hours full sun<br>Soil 🧪 Neutral to slightly alkaline (pH 6.0 -
        6.5)<br>Fertilizer 🌱Every month during spring/fall, none in winter.
        <br>Notes: Clip flower buds as soon as they're done blooming.
      title: Geranium Info!
mode: single
```
