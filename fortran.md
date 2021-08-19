# FORTRAN

SCM you have to choose right product to let mes and map version show up
svm nzboom  to grab code from there 

>ssh -X nzboom

if you work on ult and version is 9.60.2

list all the reviseion
>chbase    

ctrl+c

> base create scmnumber   9.60.2dev

dev branch is different from release branch, 
release branch is subset of dev branch, 
release branch only pick the function that user wants


>cd ~/projects

>cd basedir

>chbase .

>viewme methodname

>viewme methodname | grep dff

>cd prodsys

>vi *.f  or *.c

>gedit *.f

show what  you have changed

>base status



>meld .


use vi 
>vi prodsys/*.f

ctrl  ]    -> drill in
ctrl t     -> come back


##  debug

in the base folder

>cd kiwibin
>linkpcsmenu

show diff

>meld .  

> cd progs

> ls -lrt

download to your local environment


login svn

cause fortran code is still on svn

## once you good at change

in base dir commit, no need to add scm or kall, it will extract from base dir name

> base commit -m "commit msg"

