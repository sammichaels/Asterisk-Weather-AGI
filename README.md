# Asterisk Weather AGI

This is a bash script which obtains National Weather Service METAR data and uses Asterisk to speak the current temperature and humidity.

## Precision math in Bash

Humidity and celsius to fahrenheit conversions are done in awk for precision.

## Asterisk configuration

This is executed as part of an IVR which plays a recorded greeting, the date/time, the weather info, a recorded sponsor message, a recorded weather forecast, and a recorded closing message.  The IVR configuration from extensions.conf is:

```
[voicemenu-custom-5]
exten = s,1,NoOp(Weatherline Main)
exten = s,2,Answer()
exten = s,3,Playback(greeting)
exten = s,4,Wait(1)
exten = s,5,Playback(current-time-is)
exten = s,6,SayUnixTime(,CST6CDT,ABdY 'digits/at' IMp)
exten = s,7,AGI(wx.agi)
exten = s,8,Wait(1)
exten = s,9,Playback(sponsor)
exten = s,10,Wait(1)
exten = s,11,Playback(forecast)
exten = s,12,Wait(1)
exten = s,13,Playback(close)
exten = s,14,Hangup()
```

There are other IVR menu trees to record the greeting, sponsor, forecast and closing.

## Purpose

This is a replacement for the aging (and mostly broken) hardware WeatherLine appliance.

## Listen to it via phone

To listen: +1 (214) 520-4300
