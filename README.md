# Tablet Rules

- tablets are configured:
`adb shell settings put system screen_off_timeout 30000          # in milliseconds`

tablets run wallpanel.xyz

Motion triggers screens to change from web-screensaver to showing the dashboard

```
service: mqtt.publish
data:
  topic_template: wallpanel/{{ trigger.to_state.object_id }}/command
  payload: "{\"wake\": true}"
```

"wakeTime": 180}




Certain rooms should go off at night
- bedroom1
- bedroom2
- bedroom3

Motion should not 