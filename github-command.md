### we fork repos from original repos to own account

#### add remote 
finished clone, stay in default branch (master or main)
```shell
git remote -v    # check configured remote repos
git remote add upstream <repos url>.   # specify a new remote upstream repository that will be synced with the fork
```
#### sync a fork
```shell
git fetch upstream.    # fetch branches and respective commits from up
git checkout master
git rebase upstream/master. # if got conflict you need to fix
git push --force 
```

#### pull commits into own folk
```shell
git checkout BRANCH
git pull orginalRepoURL BRANCH
git push origin BRANCH
```

