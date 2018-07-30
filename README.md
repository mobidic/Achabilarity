# ACHABILARITY

AchabInsinguLARITY, a container to use captainAchab workflow easier ! 


## Goals 

Use a Singularity container which already has all tools to run captainAchab workfflow. 


## Run 

**First, build**

```bash
singularity build <filename.simg> Singulairty 
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

The container will execute specific wrapper of cromwell ([Crom-wellWrapped](https://github.com/mobidic/Crom-wellWrapped)) which will generate the right cromwell command depending on options and arguments.
