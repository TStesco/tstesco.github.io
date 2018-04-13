---
layout: post
title: Atmena Indoor Environment Quality System
date: 2018-03-03 00:00:00 -0000
github: https://github.com/TStesco
tags: [software, hardware, buildings]
image: atmena_sensors_v1_inside.jpg
type: project
---
Atmena is an indoor environment quality sensing and analysis system built by [Nathan Woltman][Nathan], [Andrew Gillies][Andrew], [Aayush Rajasekaran][Aayush], and myself for the SE 491 UW capstone course in June 2016. The project idea was to test newly available cheap environmental sensors and connect the good ones to a microcontroller with WLAN, then send the measurements to our web server for processing, storage, and analytics. We could then use the information to benchmark and communicate how to improve indoor environments _as a service_. This is a retrospective write up of the project: hardware, firmware, and web service.

## Hardware

There was a relatively step learning curve to testing and integrating all the cheap environmental sensors. For application in health and comfort in typical buildings We wanted to provide a relatively complete environmental sensing suite including:

* Temperature
* Humidity
* Air flow
* Barometric pressure
* Sound
* Light
* Carbon dioxide (CO2)
* Carbon monoxide (CO)
* Oxygen (O2)
* Volatile Organic Compounds (VOC)
* Particulate Matter (PM)
* Ozone (O3)
* Nitrogen oxide (NOx)
* Gas leak (CH4 and LPG)

This meant we ended up having to order and test a lot of sensors. The integration of each sensor to our hacky testing board was quite laborious given the sensors had different output types, voltages, and power requirements. With a multimeter, soldering iron, helping hand, and a few late nights we got through it. You can see the detailed specs of all the sensors we tested in the [test hardware spec sheet][Atmena_Test_Hardware_Specs]. Thankfully the UW Software Engineering department generously reimbursed us for the cost of the electronics.

<div style="text-align: center;">
{% include captioned-image.html url="atmena_sensors_v0.jpg" description="Fig 1: Hacky sensor testing evaluation board" style="height: auto; width: auto; max-height: 700px;" %}
</div>

Despite looking like garbage our testing allowed us to whittle our list of sensors down to the ones that actually worked and provided more benefit than headache. Ya, the cheap fire-hazard  O2 and CO sensors didn't make the cut (drawing ~1A they got surprisingly hot!). The following list shows the specific sensors we greenlit for use in our prototype design. 


| Parameter | Sensor Name |
| --- | --- |
| Temperature/humidity | [Adafruit HTU21D][AdaHTU21D] |
| Air flow | [Wind Sensor Rev. C][wind_sensor] |
| Barometric pressure | [Adafruit BMP180][barometer] |
| Sound | [Phidgets Sound Sensor][sound_sensor] |
| Luminosity | [Adafruit TSL2561][AdaTSL2561] |
| Carbon dioxide | [K30 10,000ppm][k30] |
| Carbon monoxide and NOx| [MiCS-6814][gas_multi] |
| Volatile organic compounds | [MiCS-VZ-86/89][MiCS-VZ-86_89]|
| Particulate Matter | [Sharp GP2Y1010AU0F][Sharp_GP2Y1010AU0F]|
| Ozone | [MICS-2614][MICS-2614] |

<br>

Our design is shown below and with the cost for all components around $660 CAD including shipping. You can see the full cost breakdown in this [hardware budget sheet][Atmena_Hardware_Cost_v1].

<div style="text-align: center;">
{% include captioned-image.html url="atmena_sensors_v1_inside.jpg" description="Fig 2: First full iteration board inside v1.0 sensor case." style="height: auto; width: auto; max-height: 700px;" %}
</div>

We did a quick case design in SolidWorks and got it printed at the UW 3D print shop. We put in some perforations to let in light, air, and a wall-wart power cord.

<div style="text-align: center;">
{% include captioned-image.html url="Atmena_case.png" description="Fig 3: SolidWorks case design" style="height: auto; width: auto; max-height: 700px;" %}
</div>

Here is what our prototype looked like.

<div style="text-align: center;">
{% include captioned-image.html url="atmena_sensors_v1.jpg" description="Fig 4: Assembled prototype" style="height: auto; width: auto; max-height: 700px;" %}
</div>

## Firmware
<div class="page-links">
<a class="btn btn-secondary" href="https://github.com/TStesco/IEQ-firmware">Firmware Repo</a>
</div>
<br>

We built the firmware on the Arduino prototyping platform which uses AVR C/C++ (avr-g++). Using the Arduino IDE is pretty straight forward. We chose to open source the code under the Apache 2.0 license so you can checkout firmware code in the [firmware repo][firmware-repo].

## Data API
<div class="page-links">
<a class="btn btn-secondary" href="https://github.com/TStesco/IEQ-data-api">Data API Repo</a>
</div>
<br>

Of course no analytics system is complete without a web micro-service to do data magic with all those sensor  payloads hitting the server. We built our API using node.js, MySQL, and socket.io. An interesting design decision we made was doing all the raw data conversion to unit values on the server to make rolling updates and calibration more seamless. Checkout the API code in the [data api repo][data-api-repo].

## Web app
<div class="page-links">
<a class="btn btn-secondary" href="https://github.com/TStesco/IEQ-web-app">Web app Repo</a>
</div>
<br>

We put together a bare bones web app using react to host the converted sensor data. You can checkout the [web app repo][web-app-repo] for more details. As the first analytics feature for this service we made a so-called "comfort score" that was a ranking of a specific space using a logistic curve to score the comfort of each part of the indoor environment: thermal, air, sound, and lighting. If you want more information about this have a look at our [presentation][presentation]. The scoring system was pretty last minute and based almost entirely on existing standards.

<div style="text-align: center;">
{% include captioned-image.html url="atmena_website_demo.png" description="Fig 5: Data hosting and analytics website" style="height: auto; width: auto; max-height: 700px;" %}
</div>

[Nathan][Nathan] and I presented this shortly after implementing it during some end of semester madness, we didn't know at the time we were being [filmed][video].

<div style="text-align: center;">
{% include captioned-image.html url="atmena_SE_491_symposium_poster.png" description="Fig 6: Fancy poster" style="height: auto; width: auto; max-height: 700px;" %}
</div>

We recieved some funding from the [Engineer of the Future Fund][eng_trust] to test and deploy better hardware although due to busy schedules post-grad we never took our system to market. We did however learn an awful lot about embedded software, sensors, and tieing them together over the internet - which I am still passionate about. I'm happy to see people today starting to care more about their indoor environment in meaninful ways.


[Aayush]: https://www.collinsdictionary.com/dictionary/english/snazziest
[Andrew]: http://www.dictionary.com/browse/snazzy
[Nathan]: https://www.linkedin.com/in/nathanwoltman/
[Atmena_Test_Hardware_Specs]: https://drive.google.com/open?id=1YJKtf_jAYaNDfUoqoyyPnKs6_yJytHAj1Hm8VMwupms
[Atmena_Hardware_Cost_v1]: https://drive.google.com/open?id=1Jo_asX08Kf-6O257cMALV113JxQAkhwK9KC1dQ3DEPA
[video]: https://www.youtube.com/watch?v=Mk-zCwmBx0Y&index=14&list=PLRqQHlx1JrKzbsgF6DaRSHzECsmkHI_i6
[presentation]: https://drive.google.com/open?id=1N_x6zPVfMs_4S7p16iuxsmsBSp5xF5yKJgJ7vAKGiOM
[firmware-repo]: https://github.com/TStesco/IEQ-firmware
[data-api-repo]: https://github.com/TStesco/IEQ-data-api
[web-app-repo]: https://github.com/TStesco/IEQ-web-app
[AdaHTU21D]: https://www.adafruit.com/product/1899
[AdaTSL2561]:https://www.adafruit.com/product/439
[wind_sensor]: https://moderndevice.com/product/wind-sensor/
[barometer]:https://www.adafruit.com/product/1603
[sound_sensor]:https://www.robotshop.com/ca/en/phidgets-sound-sensor.html
[gas_multi]: https://www.robotshop.com/ca/en/grove-multichannel-gas-sensor.html
[k30]: https://www.co2meter.com/products/k-30-co2-sensor-module
[MICS-2614]: https://aqicn.org/air/view/sensor/spec/o3.sgx-mics2614.pdf
[Sharp_GP2Y1010AU0F]: https://www.robotshop.com/ca/en/dust-sensor.html
[MiCS-VZ-86_89]: https://www.cdiweb.com/datasheets/e2v/Datasheet%20MiCS-VZ-86%20and%20VZ-89%20rev%203.pdf
[eng_trust]: https://uwaterloo.ca/engineering/entrepreneurship/funding/engineer-future-trust