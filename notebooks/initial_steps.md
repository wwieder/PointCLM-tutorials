## Initial steps for running single point simulation

1. Subset surface dataset
```
cd ~/CTSM/tools/site_and_regional/
./subset_data point --help
```

2. Subset datm
  - This can be done using subset data (which is currently default for GSWP3 datm data)
  - Also not required, although it makes simulations faster.

3. Create a new case:

4. Adjust:
  - user_nl_clm
  - user_nl_datm_streams
  - xml changes
  - this is easier with usermod directories (which also can be created by subset_data)

## Example
#### Subset data
Below is an example for how this could be done for a case in Boulder, Colorado.

Here we'll subset the surface dataset, datm data, and create usermods (steps 1, 2, & 4, above) with a simple call to `subset_data`

```
ml conda
conda activate npl-2024a

cd ~/CTSM/tools/site_and_regional/
./subset_data point --help

./subset_data point\
  --lat 40.015\ 
  --lon 254.73\ 
  --site BOCO\ 
  --dompft 13\ 
  --create-surface\ 
  --create-datm\ 
  --create-user-mods\ 
  --datm-syr 2000\ 
  --datm-eyr 2009\ 
  --outdir /glade/derecho/scratch/$USER/BOCO

```

Some notes on subset data
- Subset data is supposed to work with the ctsm_pylib conda environmnet, 
but if you don't have that set up yet you can use a preloaded conda environment on derecho (as done above)
- The backslashes at the end of each line just make the text easier to read.
- `--lon` can have negative values for West, or 0-360 degrees, this examples uses the later.
- `--dompft` sets the dominant pft.  This example sets to 100% C3 grass
- `--create-datm` take a bit of time, just pick the years you want to run over.
- `--create-user-mods` makes setting up your cases easier in the next step.

#### Create a new case
Now we'll create a single point case that uses the data we just subset for our single point runs

```
cd ~/CTSM/cime/scripts

./create_newcase\
  --case /glade/derecho/scratch/$USER/BOCO/boco_c3_sp_test1\ 
  --compset 2000_DATM%1PT_CLM60%SP_SICE_SOCN_SROF_SGLC_SWAV_SESP\
  --res CLM_USRDAT\
  --output-root /glade/derecho/scratch/$USER/BOCO\
  --user-mods-dir /glade/derecho/scratch/$USER/BOCO/user_mods\
  --run-unsupported\

```

#### Follow the other steps
Now that you've created a case, you can setup, build and submit your case.  
```
cd /glade/derecho/scratch/$USER/BOCO//boco_c3_sp_test1 
./case_setup
./case_build
./case_submit

```

There are likely some other case customizations you may want to consider

