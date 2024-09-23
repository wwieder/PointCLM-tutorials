## Quickstart for CTSM
This will: 
- Pull from the head of the CTSM development branch and
- Create a clone in your home directory 
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
ln -s /glade/derecho/scratch/$USER scratch
```

