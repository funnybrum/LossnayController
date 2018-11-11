# Lossnay energy recovery ventilator controller

I got a Lossnay LGH-15RVX-E! And since I'm trying to build a smart home - it needs a controller. The device can be installed and operated with no remote by a microcontroller. Smart home needs connectivity and WiFi is the simplest one. For that I'll use ESP8266 to expose WiFi REST endpoint.

The Wemos D1 mini will do the job. Below is the pin mapping.


## D1 as output to turn on/off the device (TM2).

The device must be turned on before operating it. Untill it is turned on - the speed settings have no effect. Thank you Mitsubishi for having such unclear documentation on that!

This will be implemented with optocoupler. The output of it will "ground" TM2-1 to TM2-3. The current is a few mA.

## D0/D5/D6/D7 as output to controll the 4 fan speeds (CN17).

There are two options for that - with 0VDC to 10VDC on CN26 (pins 4 and 5) or with 4 switches on CN17. I'm choosing the second option as it looks a bit simpler to implement.

This will be achived with 4 optocoplers. Grounding any of the CN17-2, CN17-3, CN17-4 and CN17-5 to CN17-1 will control the fan speed. 

##  D2 as output to controll the bypass valve (CN26).

In hot summer nights it would be a bit better to turn on the bypass mode. This will allow to cool down the house. Again - optocoupler on CN26-1 and CN26-2. Grounding CN26-2 to CN26-1 will set bypass mode. Disconnecting them will set lossnay mode.

## D3/D4 pins for Wire communication to 2 BME280 sensors.

These are pulled up high, so they can't be used for optocuplers. Especially D3 that needs to be high during startup. So they will be used for connecting the sensors.

Two sensors will be attached. One configured at 0x77 and one configured at 0x76. One of them will be monitoring the exhaust air entering the energy recovering ventilator. The other will be monitoring the fresh air going out of it.


## A0 as input to monitor for the bypass valve state.

And we are almost out of digital pins (D8 is still available), but we have an analog one! It will be used to monitor the bypass and malfunction monitor outputs at TM3.