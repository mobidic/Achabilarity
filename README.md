# ACHABILARITY

AchabInsinguLARITY, a container to use captainAchab workflow easier ! 

<img src="img/achab_logo.png" width="350">


## Goals 

Use a Singularity container which already has all tools to run captainAchab workflow. 
![captain achab workflow description](/img/captainAchab.svg)


## Run 

**First, build**

```bash
singularity build <filename.simg> Singularity 
```

**Then run**
```bash
singularity run -B </PATH/TO/ANNOVAR> <filename.simg> -i workflow_inputs.json
```

**Singularity help**
```bash
singularity help <filename.simg>
```

## Options

**-c | --conf <file.conf>** : To add a conf file  
**-o | --option <option.json>** : To add an option file   
**-v | --verbosity <1, 2, 3 or 4>** : To set verbosity level (ERROR : 1 | WARNING : 2 | INFO [default] : 3 | DEBUG : 4)   
**-h | --help** : Print help message in terminal and close the script (Help provided by -h concerns wrapper using)   


## More informations 

Achabilarity is currently using a part of [MobiDL](https://github.com/mobidic/MobiDL) which is [CaptainAchab](https://github.com/mobidic/Captain-ACHAB) workflow.  
This Singularity contains CentOS environnement and all requirements to run Captain Achab workflow (MPA, Phenolyzer, Achab) and few others (BCFTools, GATK4 ...).  
**Make sure you already have Annovar (and its database) to bind it. It is not include in this container.**
Binding of ANNOVAR and data folder (inputs) will look like:
```bash
singularity run -B /path/to/annovar/:/media -B /path/to/data/:/mnt achabilarity.simg -c /path/to/conf -i /path/to/json
```
The container will execute specific wrapper of cromwell ([Crom-wellWrapped](https://github.com/mobidic/Crom-wellWrapped)) which will generate the right cromwell command depending on options and arguments.

--------------------------------------------------------------------------------

**Montpellier Bioinformatique pour le Diagnostique Clinique (MoBiDiC)**

*CHU de Montpellier*

France

![MoBiDiC](img/logo-mobidic.png)

[Visit our website](https://neuro-2.iurc.montp.inserm.fr/mobidic/)

--------------------------------------------------------------------------------
