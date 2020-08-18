

# Active Directory Authentication for Flash Array

These Playbooks will help you setup Active Directory Authentication, and configure AD roles to manage Flash Array


## Prerequisites


steps to capture

## create protection group and add volume to it

repl.yaml

## create a pg snapshot

pg.yaml


## need to add the target manually at this time. 


## deploy app on new site. 

./make

## spin down mysql

kubectl scale --current-replicas=1 --replicas=0 deployment/wordpress-mysql


## restore the volume from pg snapshot

pgrestore.yaml


## scale the app back up

kubectl scale --current-replicas=0 --replicas=1 deployment/wordpress-mysql


## show app is now restored to new site. 



## Authors

* **Andy Parsons** - - [opslounge](https://github.com/opslounge)

# app_recovery_CBS
