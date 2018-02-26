---
layout: post
title: Mars Hydroponics and Hydrology
date: 2015-09-20 00:00:00 -0000
github: https://github.com/TStesco/mars-hydroponics-datalogger
image: marsHydroCover2-min.jpg
tags: [cybernetics, hardware, software]
---
In July 2015 as part of CIVE 486 at Waterloo, a course in [hydrology][hydrology], Eric Kohen and I built an experimental Mars mission hydroponic system 
to understand and attempt to model the hydrologic effects of recirculating water within an enclosed hydroponic system using a soil similar to Martian soils.
The project was also featured in the Fall 2015 technology and innovation section of the Water Institute's [Splash Pad][splash-pad] newsletter.

The concept followed that a Mars mission hydroponic system could reduce the required mass of transported food for long duration missions, and thus the overall launch mass, by providing 
food while operating on the Martian surface itself. The NASA Mars Mission DRM 5.0 allocates a mass of 13,240 kg to transit 
habitat food, 26% of the payload for the transit habitat mass. The mass of this system could be reduced by processing 
in-situ resources such as the Martian soil and atmosphere for the plant growth media, water supply, and plant nutrients. 
Producing an in-situ food production system using local resources should then be of great interest under NASA’s Objectives 
Related to Preparation for Sustained Human Presence, in particular Human Habitability/In-Situ Resource Utilization (ISRU).
                    
<h2 class="section-heading">System Design and Data Collection</h2>
<p>
The experimental Mars hydroponic system is a small-scale hydrologic testing appartatus consisting of: a hydroponic growth basin containing a sand soil media and seedlings of lettuce, three reservoirs (interflow, runoff, and main), a blue and red wavelength LED lighting fixture on a timer (outside of the system directing light inside), 27.7 L of reverse osmosis filtered water containing plant nutrients (6g each of: magnesium sulfate, calcium nitrate, and micronutrient mixture), a pump, and a data logging system.
</p>

<div style="text-align: center;">
{% include captioned-image.html url="finishedConstruction-min.jpg" description="Fig 1: Experimental mars hydroponic system" style="height: auto; width: auto; max-height: 700px;" %}
</div>


The system was rigged with internal sensors for: air temperature/humidity, water termperature, soil moisture, and three ultrasonic distance sensors for water level. The specifications for these sensors is presented in the table below. These sensors were controlled by an arduino-like microcontroller (analgous to the leonardo) which took readings from all 5 sensors every 2 seconds and printed the output to the serial port. The serial output was saved to a .csv file every half-hour (900 readings) on a data logging computer running Linux Ubuntu 14.04 and a serial port reading/.csv writing script in Processing which can be found on [Github][github].

<div style="text-align: center;">
{% include captioned-image.html url="marsHydroConstruction-min.jpg" description="Fig 2: Sensor wiring of Mars hydroponic system" style="height: auto; width: auto; max-height: 700px;" %}
</div>
<span class="caption text-muted"><strong>Table 1: Sensor Specifications</strong></span>
<table>
	<tr>
    	<th>Parameter</th>
    	<th>Sensor Name</th>
    	<th>Accuracy/Resolution</th>
    	<th>Range</th>
	</tr>
		<tr>
    	<td>Air temperature</td>
    	<td>DHT22 Temperature and Humidity Sensor</td>
    	<td>±0.5 / 0.1 °C</td>
    	<td>-40 to +80 °C</td>
	</tr>
	<tr>
    	<td> Humidity</td>
    	<td>DHT22 Temperature and Humidity Sensor</td>
    	<td>±2  / 0.1 %RH</td>
    	<td>0 to 100 %RH</td>
	</tr>
	<tr>
    	<td>Water Temperature</td>
    	<td>DS18B20 Digital Thermometer</td>
    	<td>±0.5 / 0.1 °C</td>
    	<td>-10 to +85 °C</td>
	</tr>
	<tr>
		<td>Soil Moisture</td>
    	<td>DFRobot Moisture Sensor</td>
    	<td>n/a</td>
    	<td>n/a</td>
	</tr>
	<tr>
		<td>Water Level</td>
    	<td>HC-SR04 Ultra01+ Ultrasonic Range Finder</td>
    	<td>±3 mm</td>
    	<td>2 cm to 400 cm</td>
	</tr>
</table>
<p><br></p>



<div style="text-align: center;">
{% include captioned-image.html url="PlantAreaDay1-min.jpg" description="Fig 3: Lettuce seedlings after transplanting into system" style="height: auto; width: auto; max-height: 700px;" %}
</div>
<p>
    During experiment we found that of the initial volume of water that was rained onto the lettuce seedlings the bulk flowed through the soil. The rest ranoff quickly during the short rain event and returned to the main reservoir. The infiltration reservoir then filled slowly and eventually refilled the main reservoir. The total of all three reservoirs represents all water in the system minus the amount within the soil.
</p>
<div style="text-align: center;">
{% include captioned-image.html url="graph1.png" description="Fig 4: Graph showing all three reservoir volumes during simulated rain event" style="height: auto; width: auto; max-height: 700px;" %}
</div>

[github]: https://github.com/TStesco/mars-hydroponics-datalogger
[hydrology]: https://en.wikipedia.org/wiki/Hydrology
[splash-pad]: https://uwaterloo.ca/water-institute/sites/ca.water-institute/files/uploads/files/wi_newsletter_fall2015.pdf
