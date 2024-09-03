# PointCLM-tutorials
This is a repository to share workflows, analyses and more for people getting started using the Community Land Model (CLM)

To get started you can:
1. Fork this repository, this will give you your own copy of the repo on github.
2. Clone your fork locally on derecho (or another system)
```
  cd ~
  git clone --origin origin https://github.com/{$USER}/PointCLM-tutorials.git PointCLM-tutorials
  cd PointCLM-tutorials
```
  - you'll replace _$USER_ with your own github user name
  - this will clone your remote repository as the 'origin' with the same name on derecho

3. Link to the upsteam repository
```
  git remote add upstream https://github.com/wwieder/PointCLM-tutorials.git
```
Check that it worked with: `git remote -v`

4. Checkout a branch to work on.
```
  git checkout -b branch_test
```
Check what branches you have now with:`git branch`
You can also see the log of commits with: `git log --oneline --decorate`

5. You may want to fetch and pull the latest from the remote repository, this avoids conflicts
```
  git checkout main
  git fetch upstream
  git pull
```

Some [basics of git are here](https://git-scm.com/about)
For more on setting up CLM, see the [CTSM wiki](https://github.com/ESCOMP/CTSM/wiki/Quick-start-to-CTSM-development-with-git)
