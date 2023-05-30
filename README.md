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

Blind automations:


// getting warm in the study
//2021-06-29 09:08:36.267 [INFO ] [openhab.event.ItemStateChangedEvent ] - Item 'AstroSunPositionAzimuth' changed from 98.44841911289947 ° to 98.53330377762457 °

//2021-06-29 09:08:36.268 [INFO ] [openhab.event.ItemStateChangedEvent ] - Item 'AstroSunPositionElevation' changed from 36.04113379463482 ° to 36.100583818427694 °



//openhab:send gStreetSideBlinds 100



    // 2021-06-08 08:17:20.053 [INFO ] [openhab.event.ItemStateChangedEvent ] - Item 'AstroSunPositionAzimuth' changed from 87.27133423518193 ° to 89.23082207515762 °  
    // Close first four rooftop windows

    // Morning
    // Close Lounge Blinds


    // 11am 
    // Close Rootop Windows
    // Close Rooftop Blinds


    // Lunchtime


    //3pm 
    // Close Bedroom 1 blinds


    // 2021-06-08 14:57:19.805 [INFO ] [openhab.event.ItemStateChangedEvent ] - Item 'AstroSunPositionAzimuth' changed from 222.93248385799413 ° to 226.40869115976858 °
    // Close kitchen blinds

    if ((SunAngle >=222) && (SunAngle <=230)) {
       // check if KitchenLeft has been updated in the last 10 mins. 

      // KitchenLeft.sendCommand("DOWN")
      logInfo("rollershutter.rules", "Closing Kitchen blinds")
   }

// sunangle of 244 (safe to open street side blinds)


    // 2021-06-07 20:25:01.172 [INFO ] [openhab.event.ItemStateChangedEvent ] - Item 'AstroSunPositionAzimuth' changed from 297.2674583400293 ° to 299.1581172708146 °  
    // Open Kitchen Blinds
   // else {
    //    logInfo("rollershutter.rules", "Nothing to run")

   // }


// Open roof blinds
//'AstroSunPositionElevation' changed from 27.256149453200432 ° to 27.207885737891562 °
// 22.652128501956838


end


rule "Rolladen Wohnzimmer runter wenn Sonne scheint"

when
  Item LocalSun_Position_Azimuth changed
then
  var MustClose = false;
  if ((LocalSun_Position_Elevation.state as Number).intValue > 0){
      var NewSetting = 55;
      if ((LocalSun_Position_Elevation.state as Number).intValue < 54){ 
	      NewSetting = 100 - (LocalSun_Position_Elevation.state as Number).intValue 
      }   
      logInfo("Variables sun", "NewSetting: " + NewSetting + " Azimuth: " + (LocalSun_Position_Azimuth.state as Number).intValue + "Elevation:" + (LocalSun_Position_Elevation.state))

     if ((LocalSun_Position_Azimuth.state as Number).intValue > 216 &&
         (LocalSun_Position_Elevation.state as Number).intValue < 60  &&
         (LocalSun_Position_Elevation.state as Number).intValue > 4.9) {
		    if ((Rolladen_Wohnzimmer_BlindsControl.state as Number).intValue != NewSetting
                 && (Rolladen_Wohnzimmer_BlindsControl.state as Number).intValue > NewSetting ){

				    Rolladen_Wohnzimmer_BlindsControl.sendCommand(NewSetting) 
			}
            logInfo("RolladenWohnzimmer", "Status Wohnzimmer Rolladen: " + (Rolladen_Wohnzimmer_BlindsControl.state as Number))
     }
  }

end