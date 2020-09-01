

# Using Ansible to Async and restore from secondary array  

You can use this repo to setup async between 2 arrays, add volumes and restore volumes from snapshots
on secondary array.  These playbooks use group_vars, and a handful of ansible modules called via
collections

## Prerequisites

This repo makes the assumption that your replication framework is setup and the repliation array is 
already connected. 
You need to have the 
- Pure pythonSDK libraries 
- Pure flasharray collections. 
- python3


## Set variables in group_vars/all
```
#define the name of the protection group to create
group: "apprecoveryCBS"

#suffix of snapshot to use
suff: andystest

#list the volumes to replicate
volume_a: "primary_site-pvc-ffdb1480-0fce-4358-89bf-0d7c94ce2d6d"   #mysql
volume_b: "primary_site-pvc-4ac6931e-34e4-4bb6-b866-0de4f73f757d"   #web

#target array to replicate to 
target: RedDotX

#volume to restore
restorevolume: "primary_site-pvc-4ac6931e-34e4-4bb6-b866-0de4f73f757d"
#target volume to restore over
targetvolume: "k8s-pvc-1d4ecd20-4dbxxxxxx"

#primary array to protect snap and replicate
primary_array: 10.226.116.xxx
primary_array_token: 4ac5c338-a688-3cxxxxxxxxxxxx

##secondary arrays to replicate to and restore from
secondary_array: 10.226.224.xx
secondary_array_token: aa009fd2-7686-7d48-xxxxxxxxxxx
```
## execute playbook to setup and replicate volumes to secondary array

```
ansible-playbook apprecovery.yaml
```

## Restore volumes on seconary array from replicated snapshots
```
ansible-playbook pgrestore.yaml
```

#variables can now be controlled via group_vars/all

## Authors

* **Andy Parsons** - - [opslounge](https://github.com/opslounge)

# app_recovery_CBS
