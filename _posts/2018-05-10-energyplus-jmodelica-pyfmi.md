---
layout: post
title: EnergyPlusToFMU example with JModelica and PyFMI
date: 2018-05-10 00:00:00 -0000
tags: [buildings, software]
image: fmu_export_variable.png
type: project
---

I recently started developing a large-scale building simulation and optimization 
framework based off the work of the [IEA EBC Annex 60](http://iea-annex60.org/) 
(now continuing as [IBPSA Project 1](https://ibpsa.github.io/project1/)). 
This led me to use the 
[EnergyPlusToFMU](https://github.com/lbl-srg/EnergyPlusToFMU) library to convert 
an EnergyPlus model from an .idf file into a .fmu [Functional Mock-up Unit](http://fmi-standard.org/).
I couldn't find much documentation on using [JModelica](https://jmodelica.org/) 
with [PyFMI](https://jmodelica.org/pyfmi/index.html) with an EnergyPlus FMU so 
I thought I'd document my testing and hopefully help anyone struggling as I was.

### System setup

Platform: Ubuntu 16.04 <br>
JModelica: 2.2+ (trunk) <br>
python -V: Python 2.7.12 (64 bit) <br>
energyplus -v: 8.9.0-40101eaafd <br>
compilation target: 64 bit (from EnergyPlusToFMU-v2.0.3/Scripts/linux/test-c-exe.sh) <br>
Testing .idf file: EnergyPlusToFMU-v2.0.3/Examples/Variable/_fmu-export-variable.idf <br>

### Making an EnergyPlus FMU

First, increment the version of _fmu-export-variable.idf from 8.5 to 8.9 with 
successive application of IDFVersionUpdater scripts, first being 8.5 to 8.6, 
continue until the .idf file is version 8.9.

Note: where ever <path> appears it needs to be replaced with the correct path in your file system.
```bash
$ <path>/EnergyPlus-8-9-0/PreProcess/IDFVersionUpdater/Transition-V8-5-0-to-V8-6-0 \
_fmu-export-variable.idf
```

Next use the EnergyPlusToFMU python script to make the EnergyPlus.fmu
```bash
$ python <path>/EnergyPlusToFMU-v2.0.3/Scripts/EnergyPlusToFMU.py \
-i V8-9-0-Energy+.idd \
-w USA_IL_Chicago-OHare.Intl.AP.725300_TMY3.epw \
_fmu-export-variable.idf
```

Now the .fmu file can be checked with the 
[FMU compliance checker](https://github.com/modelica-tools/FMUComplianceChecker). 
Make sure FMUComplianceChecker is built correctly for your platform first.
```bash
$ <path>/FMUComplianceChecker/build/fmuCheck.linux64 -h 600 -s 86400 _fmu_export_variable.fmu
```
the -h specifies the step size in seconds, -s is the stop time in seconds. The 
compliance checker gave me errors until I added the stop time being a multiple 
of 86400. The step size needs to be the same as the .idf file specifies, i.e. 
in _fmu-export-variable.idf (line 101):
```
 Timestep,6;
```
This is specified in steps per hour, so 6 steps/h = 600s per step.


### Simulating EnergyPlus FMU with JModelica and PyFMI

The main difficulty I had was making the number of communication points (ncp) 
match up given the final_time. I ran this in JupyterLab (.ipynb) but it should work in 
ipython or in a .py script.

```python
import os
from pymodelica import compile_fmu
from pyfmi import load_fmu
import matplotlib.pyplot as plt

# add energyplus cli script to $PATH, not needed if already in $PATH
os.environ['PATH'] = os.environ['PATH'] +":/opt/EnergyPlus/EnergyPlus-8-9-0"

# load .fmu with pyfmi
fmu_path = '<path>/_fmu_export_variable.fmu'
model = load_fmu(fmu=fmu_path)

# change input variable (default in .idf is given to be 6)
model.set('yShadeFMU', 1)

# get options object
opts = model.simulate_options()

# set number of communication points dependent on final_time and .idf steps per hour
final_time = 60*60*72. # 72 hour simulation
idf_steps_per_hour = 6
ncp = final_time/(3600./idf_steps_per_hour)
opts['ncp'] = ncp

# run simulation and return results
res = model.simulate(start_time=0., final_time=final_time, options=opts)
print(res.keys()) # show result variables names

# plot results
fig, ax1 = plt.subplots()
ax1.plot(res['time'], res['TRoo'], 'b-')
ax1.set_xlabel('time (s)')
ax1.set_ylabel('Room Temperature', color='b')
ax1.tick_params('y', colors='b')

ax2 = ax1.twinx()
ax2.plot(res['time'], res['ISolExt'], 'r.')
ax2.set_ylabel('Solar Radiation', color='r')
ax2.tick_params('y', colors='r')
fig.tight_layout()
plt.show()
```
The output chart should look something like this:
<div style="text-align: center;">
{% include captioned-image.html url="fmu_export_variable.png" description="Fig 1: 
EnergyPlus simulation testing output" style="height: auto; width: auto; max-height: 700px;" %}
</div>

This should generalize to more complicated EnergyPlus models with more states, 
inputs, and outputs allowing for intergration with larger building simulation and 
optimization toolchains.