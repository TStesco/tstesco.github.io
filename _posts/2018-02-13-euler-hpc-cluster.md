---
layout: post
title: Python on the ETH Euler HPC Cluster
date: 2018-02-13 00:00:00 -0000
image: euler_hpc_jobs.png
tags: [software]
---
The [Euler HPC cluster](https://scicomp.ethz.ch/wiki/Euler) is an absolutely amazing resource, for starters it's free to use for all ETH members 
that have a [nethz account](https://www.isg.inf.ethz.ch/Main/HelpUserAccountsNethzAccount) with zero paperwork.
I use it frequently for training of bayesian predictive models using MCMC sampling built with [PyMC3](https://github.com/pymc-devs/pymc3).
Here are a few tricks I learned for setting up and executing python batch jobs on the LSF system.

## Connecting to Euler
Access to the HPC clusters is only possible via secure protocols (ssh, sftp, scp, rsync) and must 
be accessed from ETH network or via VPN connection. ETH Recommends using the Cisco AnyConnect Client which they have a quick-install script for (vpnsetup.sh found at https://sslvpn.ethz.ch).
After installing Cisco AnyConnect Client:
```
# connect
/opt/cisco/anyconnect/bin/vpn connect sslvpn.ethz.ch
# disconnect
/opt/cisco/anyconnect/bin/vpn disconnect
```

See ETH HPC docs [here](https://scicomp.ethz.ch/wiki/Getting_started_with_clusters#Euler)

```bash
ssh netz-usernameo@euler.ethz.ch
```
After accepting the user agreement you can [set up ssh-keys](https://scicomp.ethz.ch/wiki/Getting_started_with_clusters#SSH_keys)

# Python setup

ETH HPC docs for python can be found here: [https://scicomp.ethz.ch/wiki/Python](https://scicomp.ethz.ch/wiki/Python) <br>

Set the global python interpreter to 3.6.1. This is important for which version we use to configure our environment.<br>
```bash
module load new gcc/4.8.2 python/3.6.1
```

The #! line in scripts should point to the module selected previously, not OS interpreter.
```bash
#!/usr/bin/env python
```
<br>
### Miniconda
The best method I found to manage third party libraries is miniconda: [https://conda.io/miniconda.html](https://conda.io/miniconda.html)
<br>
I installed miniconda in my personal directory and manage environments from there while cloning code into my $SCRATCH
diretory for processing.
```bash
# environment setup
source $HOME/miniconda3/bin/activates
conda config --add channels conda-forge
conda env create -f environment.yml
# start the environment
source activate pymc3

# to export environment (not needed to run)
# run this on local before and distribute .yml file to remote
conda env export > environment.yml
 
```
<br>
### venv (alternative to miniconda)
Alternative (more difficult) to miniconda is venv environment:
```bash
python3.6 -m venv env
source env/bin/activate
python3.6 -m pip install -r requirements.txt
```
Note: installing pygpu via pip does not appear to work. It can be removed from requirements.txt and not installed without error. <br>
Packages are managed with requirements.txt and the following pip commands:
```bash
# install SomePackage
/env/bin/pip install SomePackage==1.0.4
# generate requirements.txt from installed packages in venv
/env/bin/pip freeze > requirements.txt
# install all required packages
/env/bin/pip install -r requirements.txt
```

# Running Python programs as LSF batch jobs

Info about the ETH LSF batch system [here](https://scicomp.ethz.ch/wiki/Using_the_batch_system) <br>

Python scripts can be run with:
```bash
bsub [LSF options] "python my_python_script.py"
```

where [LSF options] can be:
* -n number_of_processors
* -I (interactive)
* -o output_file
* -R "rusage[mem=XXX]"

or use their [web tool](https://scicomp.ethz.ch/lsf_submission_line_advisor/) to generate LSF options  <br>
Example usage:
```bash
bsub -n 1 -W 4:00 -oo output.txt 'python training.py --njobs 4 --draws 10000'
```
<br><br>
Large groups of batch jobs can be run from bash scripts generated during preprocessing. 
These are to be run also with bsub, not in the bash shell directly. 

```bash
bsub < script.sh
```
<br><br>
output.txt gives the stdout and the LSF end of run information. Desired output can be copied to local using scp.
```bash
scp -r netz-username@euler.ethz.ch:output ./
```
