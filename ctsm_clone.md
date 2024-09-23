## Quickstart for CTSM
**Note:** there is more information on git workflows on the [CTSM wiki](https://github.com/ESCOMP/CTSM/wiki).

The example here is intended to get you started running CTSM quickly on derecho and running a NEON case

### Log onto derecho
First you need to log onto derecho from a terminal window

```
ssh -Y <$USER>@derecho.hpc.ucar.edu
```
You'll need to add your user name to the line above.
Then enter your password and duo 2 factor authentication


### Clone CTSM
After logging onto derecho you'll clone CTSM. To do this you will:
- Pull from the head of the CTSM development branch and
- Create a clone in your home directory

```
cd ~
git clone https://github.com/ESCOMP/CTSM.git ctsm
cd ctsm
```

Now you've cloned ctsm into your home directory

### Get additional components
Next we'll update additional _"components"_ that are needed to run CTSM.  
These components refers to seperate git repositories, such as FATES and MOSART or mizuRoute (river models)

To do this we'll run git-fliximod

```
./bin/git-fleximod update
```

### Create a few custom settings
There are a few other things that will be helpful to making cases run more easily on derecho

One is copying the project or account codes you want to charge to.
The easiest way to do this is by copying this file from someone else (here from Will) and will put the project codes in your home directory.

```
cp ~/../wwieder/.cesm_proj ~/.
```

I also like having a soft link to my scratch directory in my home directory.
You can do this by creating a soft link:
```
ln -s /glade/derecho/scratch/$USER ~/scratch
```

### Run a NEON case!


This is the 'regular' way of creating a new case

**NOTE** in this example the case name and usermods are for the NEON site Guanica, GUAN,
but you can chose any NEON site you like

```
cd ~/ctsm/cime/scripts
./create_newcase --case GUAN_SP_test --res CLM_USRDAT --compset 2000_DATM%1PT_CLM60%SP_SICE_SOCN_SROF_SGLC_SWAV_SESP --run-unsupported --user-mods-dir NEON/GUAN
```
- case name is for 
- resolution is user defined, here a single point
- compset is: 
    - year 2000 data atmosphere, 
    - single point CLM6 physics with satelite phenology
    - stub components for everything else (ocean, runoff, glacier, etc)
- user-mod directories are helpful for setting up details of your case

More on creating a new case can be found on the [CESM tutorial website](https://escomp.github.io/CESM/release-cesm2/quickstart.html#create-a-case)
### Set up, build, and submit the case

We'll also get the latest NEON data for our case

```
cd GUAN_SP_test
./xmlchange NEONVERSION=latest
./case.setup 
./case.build
./case.setup
```

## Alternate use run_neon to create, build, and run a case

### Activate a conda environment
First you need to load conda (a python package manager) and activate an environment. This example is specific for derecho.

```
ml conda
conda activate npl-2024b
```

Note, the _right_ way to do this is to use ctsm_pylib, but creating conda environments is really slow on derecho.
The short cut above should work, but if you want to play by the rules (or are working on a different machine) do this:
```
cd ~/ctsm
./py_env_create
conda activate ctsm_pylib
```
You can see all your conda environments with `conda env list`

### Create a run a NEON case

```
cd ~/ctsm/tools/site_and_regional
./run_neon --neon-sites GUAN --output-root ~/scratch/neon_cases
```

There are lots of options with run_neon you can learn more with `./run_neon --help` 
