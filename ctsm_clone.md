## Quickstart for CTSM
**Note:** there is more information on git workflows on the [CTSM wiki](https://github.com/ESCOMP/CTSM/wiki).

The example here is intended to get you started running ctsm quickly on Derecho.  To do this you will: 
- Pull from the head of the CTSM development branch and
- Create a clone in your home directory 

First you need to log onto derecho from a terminal window
```
ssh -Y <$USER>@derecho.hpc.ucar.edu
```
You'll need to add your user name to the line above.
Then enter your password and duo 2 factor authentication

After logging onto derecho you'll clone CTSM

```
cd ~
git clone https://github.com/ESCOMP/CTSM.git ctsm
cd ctsm
```

Now you've cloned ctsm into your home directory

Next we'll update additional _"components"_ that are needed to run CTSM.  
These components refers to seperate git repositories, such as FATES and MOSART or mizuRoute (river models)

To do this we'll run git-fliximod

```
./bin/git-fleximod update
```

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

Next we'll load conda and activate an environment
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

Finally, let's run a NEON case!

```
cd ~/ctsm/tools/site_and_regional
./run_neon --neon-sites GUAN --output-root ~/scratch/neon_cases
```

There are lots of options with run_neon you can learn more with `./run_neon --help` 
