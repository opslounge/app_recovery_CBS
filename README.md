

# Kubernetes (k8's) application recovery to the cloud

This repo contains the playbooks and instructions to setup an application recovery to a secondary 
array using Flash Array async replication and ansible to restore an application running 
inside a kubernetes cluster on-prem. to another kubernetes cluster running either in the cloud,
or another secondary array.  


## Prerequisites


steps to capture

## create protection group and add volume to it
```
ansible-playbook pgroup.yaml
```
## create a pg snapshot

```
ansible-playbook pgsnap.yaml
```

## add target for replication 
```
ansible-playbook target.yaml
```
## enable replication of volume
```
ansible-playbook enablerepl.yaml
```

## deploy app on new site. 
```
./make
```
## spin down mysql
```
kubectl scale --current-replicas=1 --replicas=0 deployment/wordpress-mysql
```

## restore the volume from pg snapshot
```
ansible-playbook pgrestore.yaml
```

## scale the app back up
```
kubectl scale --current-replicas=0 --replicas=1 deployment/wordpress-mysql
```

## show app is now restored to new site. 



## Authors

* **Andy Parsons** - - [opslounge](https://github.com/opslounge)

# app_recovery_CBS
